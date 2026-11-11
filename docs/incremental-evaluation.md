# Incremental evaluation runs

**Idea, recorded 12 November 2026. Nothing here is built.** The Weightspace Index contract v1 records a run as one finished `run.json` with a single score. This note keeps the idea for later: submitting benchmark results in portions of any size, so a run grows from a few items to the full dataset over time.

## Why

- **Compute is expensive.** A full run, for example all 500 items of MATH-500, takes hours. When it dies in the middle (a laptop sleeps, a donated machine disappears, a Space is preempted), all of it is lost.
- **Early answers are useful.** 10/500 items today gives a rough result; 10 more tomorrow narrows it. Precision grows with whatever compute shows up.
- **Many small runners can help.** Developers' machines in spare time, donated machines, Hugging Face grants or short paid bursts can each take a small piece. [Compute constraints](compute-constraints.md) lists what each of these routes actually guarantees.

## Shape: a fixed plan plus shards that are only added

A run becomes a **plan**, written once, and **shards**, added over time.

- **Plan:** profile, protocol, dataset, settings, and the item order: a seeded random permutation of the whole dataset, recorded by its seed and the digest of the ordered item IDs.
- **Shard:** one contiguous range `[start, end)` of that order, with:
  - each item's score, inline (500 items is small);
  - the full outcomes file (generations, grader output) by digest and locator;
  - who ran it, and the runner's environment (runtime build, backend, hardware).
- **Only added, never edited.** This matches the index rule that merged files under `v<N>/` are never modified; files may only be added. A wrong shard is superseded by a new shard for the same range, never edited.
- **The score is generated.** The index computes it from the shards and always shows coverage, for example "accuracy 0.62 on 40/500 items, 95% interval …".

**Why a random order:** any prefix of a random permutation is a simple random sample of the dataset. A partial score therefore estimates the full-dataset score without bias, and its interval narrows as coverage grows (with the finite-population correction, at 500/500 it is the exact score). Running items in file order, often grouped by subject or difficulty, would bias early results.

**Paired comparisons:** the baseline and patched runs of a comparison use the same order, so the comparison uses the items both have covered and reports the paired difference on them. A baseline extended later improves every patch compared against it.

**The generator stays offline.** Because shards carry each item's score inline, the index can compute scores, coverage and paired differences without downloading outcome files. CI checks the inline scores against the outcome files when it downloads them.

## Stopping early

Watching the interval narrow and stopping once a result "looks significant" inflates false positives. [Evaluation design](evaluation-design.md) already requires fixed stopping unless a valid sequential procedure is specified. Options:

- show partial results as provisional only, never as an assessment;
- allow assessments only at checkpoints declared in advance, for example 50, 100, 250 and 500 items;
- use an anytime-valid method, such as confidence sequences, that stays correct however often it is checked.

This has to be decided before any assessment relies on a partial run.

## Runners and scheduling

- **Unit of work: one shard**, sized to finish in minutes to an hour, for example 10–50 items. A failure loses at most one shard. Inside a shard, resume only at item boundaries; resuming mid-generation is not assumed to work.
- **Something hands out ranges** so two runners never do the same items. One candidate is a scheduled GitHub Actions workflow (cron), which only plans: standard hosted runners have no GPU. It reads the index, finds uncovered ranges and publishes claims (issues, or a queue file) with an expiry, so a dead runner's range returns to the pool. Scheduled workflows can be delayed, and GitHub disables them in public repositories after a period without activity; check the current rules before relying on them.
- **Runners pull work and push results.** Each submits its shards as a pull request, or a bot batches several shards into one pull request to keep history readable. CI checks that:
  - the range is in the plan and overlaps no merged shard;
  - the outcome file's digest matches;
  - the inline scores agree with the outcome file.
- **Security:** a self-hosted runner attached to a public repository's Actions can end up running code from pull requests opened from forks. Runners should never run repository workflows on pull-request events. A runner never executes code from a patch or model repository.

## Trust

- **Who measured it.** Shards from runners the maintainers control count as performed by the index. Shards from donated runners are reported by a third party unless audited.
- **Audit by sampling.** Re-run a random handful of a donated shard's items on a runner the maintainers control and compare outcomes. Per-item outcomes make this cheap.
- **Mixing environments.** GPU and backend nondeterminism can change outputs even at temperature 0. The protocol must state whether shards from different runtimes or hardware may be pooled into one run; otherwise each environment gets its own run.

## What it would change in the index

- **`run.json` holds the plan.** `score` and `state` move into generated files, computed from the shards.
- **A new `shard` record**, for example at `runs/<run-id>/shards/<start>-<end>.json`.
- **Coverage in the generated files.** `index.json` and the README results table show coverage.
- **A contract change.** It is cheapest before the first real run is filed.

## Open questions

- Shard size, how ranges are claimed, and how long a claim lasts.
- Which shard wins when two cover the same range, and how a bad shard is superseded.
- The stopping policy (see above).
- Whether shards from different environments may be pooled.
- Whether partial runs appear in the README results by default, marked provisional.
- Who runs the coordinator, and on what budget.
