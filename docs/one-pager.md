# Model Patcher at a glance

Model Patcher researches small, targeted weight fixes for local language models. The aim is to make a fix's benefits, regressions and compatibility understandable before someone changes a model. The initial focus is exact GGUF variants, with reuse of existing methods and evidence tools where they fit.

**Status as of 9 November 2026: research only.** There is no released patch tool, validated GGUF fix, supported combination or measured delivery route here. The studies establish design requirements and conditional calculations; they do not establish independently measured improvements or monthly evaluation capacity. See the [research status](research-status.md) and [synthesis](research-synthesis.md).

## Intended shape: an index with evidence for each exact variant

The proposed starting point is a small machine-readable catalog of patches, browsable by publisher and model, with Markdown explanations and links to immutable evidence bundles. Scores belong to run records; assessments explain decisions for a specified use. Discovery should retain negative results, refusals, missing evidence and corrections alongside positive findings. This is a proposed design, with no adopted schema or implemented reader yet. A generated index, CLI or hosted service would need a demonstrated need.

Evidence must identify the exact base files and revision, hashes, quantization recipe, tokenizer/template and runtime. A quantization label alone is insufficient. Each consumer profile needs its own baseline and patched outcomes: native-precision gains cannot fill a missing quantized result. Different edit/conversion routes and ordered combinations are distinct treatments. Improvements from individual fixes cannot simply be added to predict a combination. See the [catalog design](catalog-and-evidence.md) and [evaluation design](evaluation-design.md).

The proposed user path is to choose an entry for the exact model, read its evidence and unknowns, preserve the original, and obtain a separate fixed copy through a qualified method. Input mismatches or missing prerequisites should stop application. Output hashes and successful loading establish different facts from useful behavior; compare the original and candidate under matched conditions. No application commands are available yet.

## Economics: completed comparisons within a cash budget

**Owner decision, 8 November 2026: $30 total per month, with no separate daily GPU-hour cap.** The earlier daily and monthly hour ceilings are obsolete. Compare whole completed baseline-plus-candidate jobs, including billing rounding, setup/downloads, conversion, loading, all generated tokens, grading, storage/transfer, failures and remaining reserve. Avoid counting costs twice. Hourly price or short decode speed alone cannot establish capacity or select a hardware winner.

MacBook Pro nights are a possible route, but file size and nominal machine-hours do not prove memory fit or completed evaluations. Runtime memory, other applications, loading/grading, interruptions and supported resumption matter. Actual nightly capacity remains unknown; electricity, SSD use and unavailable developer-machine time also have costs.

Sponsored or free compute remains conditional. Community GPU grants may support a public demo; notebook routes may support bounded work. No award, account entitlement or indefinitely free GPU evaluation capacity is established. Current terms, eligibility, quotas, storage, billing and permission for the intended workload need confirmation. The [compute constraints](compute-constraints.md) separate these leads from measured capacity and available offers.

## Next step and open limits

The [implementation plan](implementation-plan.md) starts by choosing a concrete problem, exact base/profile, sourced fix, rights and application route, then agreeing records and qualifying a bounded evidence path. Quantized benefit, combination behavior, actual resource costs and the repository license remain unresolved. Upstream evidence may suffice; further automation depends on a recurring gap. No model experiment or patch qualification is established by the plan.
