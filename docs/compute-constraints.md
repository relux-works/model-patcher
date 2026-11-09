# Compute, budget and capacity constraints

**9 November 2026.** This consolidates public-source GPU, full-benchmark, MacBook Pro and sponsored-compute studies completed on 7–8 November. It is not a purchase recommendation, measured patch benchmark or capacity guarantee. Historical source observations and hypothetical inputs are labeled separately.

## Cost the whole completed comparison

**Owner decision, 8 November 2026: $30 total per month, with no separate daily GPU-hour cap.** There is no 30-hour monthly limit. A long job may fit the cash budget; a cheap hourly rate may still lose on completed comparable work.

For session s with rate r_s dollars/hour, billing quantum q_s seconds and total paid duration t_s seconds, the proposed accounting is:

`total = sum_s r_s*(q_s/3600)*ceil(t_s/q_s) + external preparation + other charges + actual failure spend + remaining reserve <= monthly budget`.

Paid duration includes startup, downloads, in-session conversion, loading/switching, prefill, all generated tokens, tool waits, scoring while allocated, idle time and export. Other charges include storage/cache lifetime, transfer, separate CPU/scorer fees and taxes. Do not count preparation, CPU charges or failed-attempt time twice when already inside a session term. Spent reserve reduces remaining reserve. Prepaid credits and their consumption are not two separate expenditures of the same dollars.

**Illustrative cash envelope, not an offer:** at assumed rates $0.501/hour for one RTX 5090 and $0.665/hour for one 128 GB Spark, $30/r gives 59.88 and 45.11 rented hours before extras. Holding $5 for extras and $3 reserve leaves $22/r, or 43.91 and 33.08 hours. All setup and paid scoring consume those hours. The assumed rates, one-device allocation and actual billing terms were not verified as available offers. Neither hour count predicts completed evaluations.

For equal complete work in a **compute-only proportional illustration**, with billing rounding and all additional costs excluded, a higher-rate device costs less exactly when `t_fast/t_slow < r_slow/r_fast`, where t denotes positive unrounded total duration. In the general case, compare each route's rounded session charges plus its own additional costs using the preceding accounting formula; this ratio alone does not determine the all-in cost. **Hypothetical compute-only example, excluding billing rounding and extras:** one-hour work at $1.85/hour costs $1.85; ten minutes at $7.40/hour costs about $1.23. This illustrates why whole-job timing matters; it is not a measured sixfold speedup or a current price quote.

The full-capacity study used invented token-length groups, aggregate prefill/decode rates, batch sizes, setup/scoring durations and one-minute billing. Its optimistic/base/conservative cases are different workload assumptions, not confidence intervals. Whole-batch tails, thinking tokens, repetitions and first-baseline acquisition materially change its counts. Those counts are not carried forward as operational forecasts. The [treatment-union counts](evaluation-design.md#count-arms-and-reuse-observations-explicitly) remain useful exact planning arithmetic for their stated populations.

Before promising capacity, obtain matched whole-job timings, actual output-length tails, peak memory, interruption/retry behavior and all-in billing for the exact profile. Sum arm-specific costs; quantized throughput cannot price native arms. Baseline caching requires the exact reuse contract. Persistent caching saves repeated downloads only if avoided time/transfer cost exceeds its storage cost. Cold setup and later reloads remain separate costs.

## What published GPU results establish

The Qwen3.8-27B studies compared different precisions, runtimes, prompts and concurrency. They do not establish one device ranking for this project's paired evaluation.

| Published evidence | Narrow observation | Limit |
|---|---|---|
| [RTX 5090 author report, pinned source](https://github.com/n3xtgentechitalia/qwen38-27b-5090/blob/6fc737c5cf3706a245e6a5e6299323a73966ef5f/docs/benchmarks.md) | Community NVFP4 short requests: about 130 aggregate output tokens/s at concurrency 1 and 791 at 16 | Approximately 512-token prompts/200-token output cap; raw decode fields have an unresolved inconsistency. Not BF16 equivalence, long-reasoning throughput or patch qualification |
| [Single Spark author report, pinned source](https://github.com/0xBakeer/Qwen3.8-27B-FP8-on-a-single-DGX-Spark/blob/3e94e710ae86ad06ce42ae3d477900fa6047f4d8/RESULTS.md) | Official FP8: one configuration reports 20.05 tokens/s fresh generation; a different configuration reports 52.86–58.49 on edit-heavy output | Thinking disabled; edit output was capped/truncated. Predictable editing speed is not completed reasoning work or a quality result |
| [Completed-task infrastructure study](https://www.zenml.io/benchmarks/serving-infra) | The earlier research reports H200's lowest GPU-only dollars per solved task among that study's H100/H200/B200 configurations | Historical external result with different attempts and execution conditions; excludes some costs and has no matched 5090/Spark arm |

The H200 conclusion is scoped to that completed-task comparison. Short-request PRO 6000/B300 studies, FP8 tests and quantized 5090 results cannot extend it into a universal recommendation. Hardware editions, allocated GPU count, speculation, precision and full task completion matter. No source here measures this project's complete baseline-plus-patch path. The pinned 5090 and Spark report text was accessible on 9 November; this was source inspection, not reproduction. The completed-task result above remains inherited from the 7 November study.

## MacBook Pro nights and model fit

The nighttime study covered M1/M2/M3/M5 **Pro laptops**, with configuration-specific RAM limits. CPU/GPU counts and bandwidth do not establish model speed. The selected smaller reference was Qwen3.5-9B, the priority Qwen3.8-27B, and the larger reference Qwen3.8-Flash-Next. Selection did not establish global popularity leadership.

| Publisher/profile observation in the 8 November study | Represented native tensor size, approximately | Consequence under full residency |
|---|---:|---|
| [Qwen3.5-9B, selected revision](https://huggingface.co/Qwen/Qwen3.5-9B/tree/c202236235762e1c871ad0ccb60c8ee5ba337b9a) | 19.31 GB | Exceeds 16 GB before runtime; larger RAM still needs peak-fit qualification |
| [Qwen3.8-27B, selected revision](https://huggingface.co/Qwen/Qwen3.8-27B/tree/37561816e66b5b9153b1b64c10968c18c1e6f4a0) | 55.56 GB | Exceeds configurations through 48 GB; 64 GB peak fit and backend remain unknown |
| [Qwen3.8-Flash-Next, selected revision](https://huggingface.co/Qwen/Qwen3.8-Flash-Next/tree/812d96e10a0dd82b69d749e68693698cf6c36daa) | 360 GB | Exceeds every Pro laptop configuration in the study; activated MoE parameters do not replace total weights |

These sizes are inherited publisher metadata, not local weight inspection or resident-memory measurements. Selected quantized derivatives were much smaller: roughly 6 GB for 9B and 16 GB for 27B, with different MLX/GGUF recipes and identities. That provides potential headroom, not exact peak fit or patch support. The inspected Flash-Next MLX 4-bit representation was about 111.5 GB. Its separately reported [low-bit SSD-streaming route](https://github.com/nace-ai/kapitsa/blob/main/bench/results/2026-10-30-m5-pro-flash-next-kflash/README.md) changes residency and latency; it is not proof of full-resident or overnight operation.

Require resident weights under the actual placement policy **plus** KV/recurrent state, draft/cache, workspace, runtime, OS and other applications to fit usable memory. File size alone is insufficient. Context, batch and concurrent sequences change allocations. Do not combine RAM from independent laptops as though it were one device.

The [published M3 Pro session](https://github.com/nace-ai/kapitsa/blob/main/bench/results/2026-10-22-m3pro-36gb/README.md) contains useful short-run measurements. Its separate prefill and decode phases do not constitute a full evaluation or eight-hour sustained rate. Some other reports lack exact GPU-core bins or selected-artifact hashes; those omissions cannot qualify every laptop configuration.

Eight hours × 30 nights × 1/2/3 available laptops is **240/480/720 nominal machine-hours**, an illustrative allocation, not completed jobs. The study's chip-independent toy schedule assumed 200 prefill and 20 decode tokens/s, invented lengths/overheads and item-boundary resume; it constructed 5/10/15 full-suite arms. Those counts establish feasibility only inside that fictional schedule, not a chip estimate or optimal schedule. Actual nightly capacity remains unknown. Whole jobs need coverage manifests, loading/grading/checkpoint costs, failure accounting and a supported resume policy; mid-generation resume cannot be presumed. Electricity, SSD use and unavailable developer-machine time also have costs.

## Free and sponsored compute

The 8 November provider study found useful leads, with no award or account-level entitlement verified. The following dispositions are research judgments; current terms, geography, quotas, storage and workload permission require confirmation before operational use.

| Route | Potential role | Unresolved or limiting condition |
|---|---|---|
| [Hugging Face community GPU grants](https://huggingface.co/docs/hub/spaces-gpus#community-gpu-grants) | A public reproducibility/demo Space | Discretionary; hardware, term, renewal, account-plan requirements and unattended benchmark coverage need explicit terms. A Space award does not establish funding for Jobs |
| [Kaggle Notebooks](https://www.kaggle.com/docs/efficient-gpu-usage) | Bounded resumable batch notebook fallback | The earlier quota/session claims relied on official search-index text; direct page retrieval supplied no readable body, including on 9 November. No guaranteed monthly capacity or generic CI permission established |
| [Modal](https://modal.com/docs/guide/gpu) | Custom batch evaluation and separate grading | GPU use requires a payment method; [billing after credits](https://modal.com/docs/guide/billing) prevents treating a recurring allowance as a no-spend guarantee |
| [Hugging Face ZeroGPU](https://huggingface.co/docs/hub/en/spaces-zerogpu) | Short Gradio/PyTorch demonstrations | Dynamic allocation, quotas and compatibility constraints; no general unattended full-suite entitlement inferred |
| [Colab Free](https://research.google.com/colaboratory/faq.html) | Attended notebook development | Resources and usage limits vary; interactive priority and free-tier restrictions preclude a reliable distributed-worker plan |
| [Lightning AI](https://lightning.ai/pricing) | A bounded credit-funded pilot | Earlier research identified signup credits and unclear storage terms. No fixed recurring GPU allocation is established; recheck applicable account terms |

These routes do not establish indefinitely free GPU CI. [GitHub larger runners](https://docs.github.com/en/billing/concepts/product-billing/github-actions) are separately billed, including for public repositories. Academic/startup grants depend on eligibility not established here, and TPU research support would be a separate execution profile. A no-cost CPU record check is a useful first step without implying model quality.

The provider pages for Spaces, ZeroGPU, Modal, Colab and Lightning were inspected again on 9 November for the narrow distinctions above. No account, grant application, billing setting or service was created. A sponsorship proposal would first need an identified applicant, project licensing decision, runnable public demonstration and an explicit request for the intended workload; those are future readiness requirements.
