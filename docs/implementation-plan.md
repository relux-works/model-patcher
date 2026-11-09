# Implementation plan draft

**9 November 2026. Proposed work, not an implementation announcement.** Model Patcher remains research only. The plan starts with records and a single useful evidence path, retaining the option to reuse upstream tools or stop without building a CLI or service.

The [research synthesis](research-synthesis.md), [catalog design](catalog-and-evidence.md), [evaluation design](evaluation-design.md) and [compute constraints](compute-constraints.md) define the rationale and claim limits. No schema, reader, applicator or evaluator is introduced by this draft. No download, experiment, spending, account or scheduling step is authorized here.

## 1. Choose the first bounded use

Identify a concrete user problem, exact model/consumer profile and sourced fix. Compare the existing upstream workflow with the smallest catalog addition. Select an application route from the [reuse study](reuse-routes.md) only when it expresses the actual edit. Record distribution/evidence rights, runtime prerequisites, input/intermediate/output identities and remaining unknowns. The repository license remains an owner decision; do not infer it from a model publisher's terms.

**Readiness:** a contributor can explain the intended change, locate exact inputs, name the relevant evaluation question and identify the unsupported cases. **Stop or narrow:** no real recurring need, adequate upstream discovery already exists, rights are unresolved, or the selected route cannot express the edit. A missing qualified fix may leave a useful descriptive research entry, with quality and applicability explicitly unknown.

## 2. Agree the record contract before implementing it

Write the smallest versioned specification covering catalog, profile/artifact, treatment, run, comparison and assessment roles. Decide physical files after checking how the first entry shares evidence. Preserve publisher/model navigation and Markdown explanations. Do not mandate a generated index, registry or automatic migrations.

Specify supported versions; required fields and units; unknown/missing/unsupported semantics; immutable references; discovery completeness; corrections; errors/refusals; sampling versus execution roles; four-arm cross-profile estimands; runtime-adapter identity; and denominator/failure accounting. Consumers must not interpret an unsupported operational constraint as optional description. Define accepted locator and identifier forms positively from the actual upstream formats, with matching forbidden cases, before permitting any future retrieval or application.

**Readiness:** a finite set of clearly labeled synthetic fixtures can represent every positive and negative case below with expected outputs. Include incomplete-but-discoverable entries rather than rejecting every unknown. No synthetic payload hash or score may appear as a real supported artifact. Resolve the boundary between upstream authoritative facts and local evidence before copying metadata.

## 3. Build the smallest offline catalog reader

Proposed implementation language: Go, using standard tests and the repository's eventual supported toolchain/platform policy. Pin those choices when implementation begins; this repository currently has no Go module or build/test entry point. Start with local structured records, reference checking and a readable inventory. Keep I/O behind appropriate interfaces; no remote fetch, model loading or credential handling is required for this milestone.

Validate version/meaning before application eligibility; verify registered bundle bytes and references; retain missing/refused/negative/unassessed entries; expose unresolved corrections. If producing a discovery view, derive it deterministically from a pinned source snapshot. Keep scores in runs and policy decisions in assessments. A successful reader output proves record interpretation only.

**Readiness:** meaningful Go tests pass for the agreed contract, including the regression witnesses below. Add fuzzing for parsers/resolvers and race detection if concurrency is introduced. Require supported-platform checks for any platform-specific code. Do not claim live networking, model compatibility or quality from offline fixtures.

## 4. Specify and qualify one evidence acquisition path

Choose one exact base, one fix and one consumer profile, with matched baseline/candidate arms. Freeze task population, scorer, prompts, thinking/decoding, seeds/repetitions, failure rules, contamination limits, intended-use domains, margins and stopping before confirmation. Prefer full target coverage when its measured incremental cost is modest; otherwise use a declared sampling design with honest scope. Qualification of application/loading precedes quality claims.

For a separately approved future pilot, record peak memory and complete-job time, loading/switching, all generated tokens, grading, storage, retries and paid idle. Establish lawful retention and isolation for generated-code grading. Exercise input mismatch, unavailable prerequisites, timeout/cancellation and interrupted output without overwriting original models or marking incomplete work successful. Use an existing harness and application method where qualified; a new applicator requires its own justification.

**Readiness:** retained item outcomes and resource records bind the exact treatment/protocol, with actual positive and negative controls. A descriptive pilot can remain inconclusive. No result is promoted to supported-for-use until its declared benefit/guardrail/veto policy is satisfied. This milestone requires a new operational decision; the documentation and synthetic checks do not complete it.

## 5. Extend only for the next real question

Add A/B/AB and BA arms only for selected component/order questions. Add N0/NA alongside Q0/QA when a native-versus-consumer gain comparison is needed; preserve four-arm joint outcomes. Qualify runtime adapters separately from materialized outputs. Count the observation union and only reuse exact compatible nodes, retaining shared-control dependence and historical acquisition cost.

Measure each new profile's fit, output tails and whole-job cost. Larger monthly scenarios such as $60/$90 are hypothetical alternatives, not an increased current budget. Repetition of deterministic outputs buys no independent sample size. Publish negative and inconclusive findings alongside positives.

**Readiness:** the added question has its own exact evidence and resource budget. **Defer:** native fit, route support, protected confirmation data or meaningful guardrail coverage is unavailable. No all-subsets combination expansion follows from two useful fixes.

## 6. Decide whether automation is justified

Evaluate a CLI only after repeated use reveals a verified discovery/download/application gap. Keep conversion and model execution delegated to compatible existing tools unless evidence justifies custom code. Evaluate a hosted service or sponsorship only after measured complete-job costs fit the $30 total monthly budget, actual workload permission and account terms are known, and retention/interruption behavior is qualified. MacBook nominal hours and free credits do not satisfy those conditions.

**Readiness:** a named repeated need, measured cost and explicit scope support the next tool. **No-build outcome:** retain the catalog, source links and evidence reports if automation would add maintenance without a demonstrated benefit.

## Planned acceptance checks

These are future acceptance cases, not tests executed by this documentation change. Each positive case needs a corresponding failure or unknown case so that blanket refusal cannot pass.

| Boundary | Positive behavior | Forbidden outcome / regression witness |
|---|---|---|
| Version and units | Known version and documented scale units interpreted as specified; descriptive extension handled by policy | Unsupported version or changed scale meaning silently accepted |
| Exact applicability | Exact base/profile accepted when all required constraints are established | Same display name, changed revision/tokenizer/quantization silently treated as equivalent |
| Discovery | Every registered valid bundle contributes runs, negatives, refusals and unassessed evidence | Positive-only current assessments hide a negative full result or orphan run |
| Corrections | Resolved immutable replacement chain retains originals and reasons | Missing digest, cycle or unresolved fork produces a unique current answer |
| Paired comparison | Matched item/draw outcomes retain denominator and failures | Missing items dropped, authored subset called random, unmatched scorer/protocol compared |
| Consumer evidence | Synthetic native +10-point and consumer −2-point outcomes both visible | Native gain copied into consumer assessment; positive subset erases full-set regression |
| Runtime treatment | Base plus complete adapter stack/configuration identifies the requested treatment | Unchanged base hash conflates A→B and B→A or supplies untested support |
| Shared observations | Unique matching nodes counted once, historical cost and dependence retained | Three deterministic runs counted as three independent task samples; native baseline substituted for consumer |
| Resource accounting | Complete rounded sessions plus extras/spend/reserve remain within declared budget | Obsolete daily cap reintroduced, setup omitted, reserve counted twice or inference speed labeled capacity |
| Future application boundary | Known input yields a separate verified output through the qualified method | Wrong input, cancellation, timeout or partial output overwrites original or reports success |

Offline parser/fixture checks, real application/load checks, statistical-method checks and live quality/resource measurements prove different properties. Record the exact candidate, commands, actual verdicts and unavailable lanes at implementation readiness. An independent review must assess the exact integrated change before release; checking one's own arithmetic is not that review. Post-publication corrections should remain explicit and preserve the prior evidence.
