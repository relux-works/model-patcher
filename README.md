# Model Patcher

Model Patcher is research into small, targeted weight fixes for local language models. The aim is to address a known problem while making benefits, regressions, and compatibility understandable before someone changes a model. The initial focus is exact GGUF variants; safetensors is a possible later target. The project intends to reuse existing methods and evidence tools where they fit, with only the glue needed to make a supported path clear.

**Status: research only.** No fix, combination, application method, or model variant is currently presented here as validated or available. The existence of a research method or a model card does not establish that it works for a particular model file.

Start with [Model Patcher at a glance](docs/one-pager.md) for the proposed index, evidence requirements, budget and current limits.

## Proposed path

1. Identify the precise model file and variant you use. A future supported entry should name the exact source, revision, file, hash, and relevant runtime.
2. Choose a fix or a prepared combination for that exact model. Read its stated purpose, measured benefits, regressions, and unknowns. An untested or incompatible combination should be marked clearly.
3. Keep your original file. If a validated method and required files become available, follow the instructions for that specific entry to obtain a separate fixed copy. Stop if the input does not match or a prerequisite is missing.
4. Check the resulting file against the published identity and confirm that it loads in the stated runtime. A matching hash identifies bytes; it does not certify quality.
5. Compare the original and candidate on tasks you care about under the same settings. Keep the candidate if it helps; otherwise return to the original.

There are no application commands yet because no candidate path has been validated. A combination needs its own evidence: results for individual fixes do not predict their joint behavior, and evidence for a pair does not prove that a larger combination works.

See the dated [research status and targeted-edit example](docs/research-status.md). Read about [reuse routes](docs/reuse-routes.md), [combination evidence](docs/combination-evidence.md), or [contributing evidence and corrections](CONTRIBUTING.md).

The [research synthesis](docs/research-synthesis.md) brings together catalog design, evaluation methods and compute constraints. The [implementation plan](docs/implementation-plan.md) proposes a staged path from those findings; it does not announce implemented tools or qualified model fixes. [Incremental evaluation](docs/incremental-evaluation.md) records an idea for later: benchmark runs submitted in small shards, so results start early and grow more precise as compute arrives.
