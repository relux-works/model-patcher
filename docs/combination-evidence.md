# Evidence for combinations

**Sources checked: 6 November 2026.** Findings below are supported as documented capabilities or author-reported results; proposed records are design inferences. Untested candidate behavior is unknown.

Small, targeted weight fixes may interact even when each appears useful on its own. The proposed first target is an exact GGUF variant; safetensors may follow. Existing research and reporting systems offer useful evidence practices, but the examples below do not validate any sparse GGUF fix or combination. In particular, pairwise success does not establish compatibility of three or more fixes.

## What existing research shows

[MergeBench](https://arxiv.org/html/2505.10833v5) constructs domain-specialized language models from Llama and Gemma bases, merges them using eight methods, and evaluates task performance, retention of base-model knowledge, and runtime. Its authors report that tuned coefficients and some sparsification methods can improve retention, while merging has costs and can trail multi-task training on in-domain performance. They also report that DARE's random dropping preserved base knowledge less well than the other sparsification strategies discussed. These are results for their models, methods and protocol, not a guarantee for other models or fixes. The benchmark's separation of task gains, forgetting and cost is useful for evaluating combinations.

[ComposLoRA](https://arxiv.org/html/2402.16843v2) is a testbed of 480 composition sets for **text-to-image** LoRA adapters, not sparse language-model edits. The paper studies LoRA Switch and LoRA Composite during image generation and reports improved scores against its LoRA Merge baseline. It also reports that quality declined as more adapters were combined, that frequent switching could distort images, and that the automated evaluator had positional bias; results were averaged over both input orders. A human evaluation involved two raters and 120 images. These findings illustrate both positive and negative outcomes and the importance of evaluator limits; they do not establish a GGUF application method or predict language-model behavior.

These are author-reported research results. Their controlled setups differ from a small edit to a quantized GGUF file. Quantization, conversion, base identity, operation, and interaction between edits all require separate evidence for the actual candidate. Whether any particular sparse GGUF fix can be safely and reproducibly combined with another is currently unknown here.

## Reuse existing reporting

[Hugging Face model cards](https://huggingface.co/docs/hub/en/model-cards) combine readable Markdown and metadata; their `model-index` can record structured evaluation results. The separate [Evaluation Results](https://huggingface.co/docs/hub/eval-results) feature, described as work in progress, stores results in model repositories and can display source, community, leaderboard and verified badges. The documentation defines verified in terms of a valid verification token and a specific evaluation environment; it does not mean a model is generally good or compatible with a patch. A score, card, or badge is not by itself evidence that an exact local GGUF file is the evaluated candidate.

A practical inference is to reuse model cards, existing result records and links to native evaluation outputs, adding ordinary prose for missing facts. There is no need to invent an artifact format or application service to describe a combination. A card should link exact file identities, ordered fix revisions, intermediate states, method versions and evidence, or say which details are unknown. It should link the underlying evaluation rather than treating a score as self-explanatory.

## What a future record should show

For a given exact base, compare the unchanged baseline, each single fix and each relevant ordered combination using a common protocol. Record both orders if both are tested; do not assume one order represents the other. Establish that each step accepts its actual intermediate input. A mismatch, an observed behavioral regression, and a combination that has never been tested are different states. Separate successful application and loading from measured quality.

Record model and artifact revisions, filenames and hashes, quantization, tokenizer and chat template, method and version, and output identity if byte-exact verification is supported. Hashes identify bytes; they do not certify usefulness or compatibility. Describe overlaps and their resolution or rejection when observable; non-overlap does not rule out behavioral interaction. If the input or an intermediate state is unknown, compatibility is unknown.

For each outcome, include dataset revision and split, task, sample count, prompt, runtime, settings, scoring, seeds and repeats; link configurations and lawful per-example outputs. Report improvements, regressions, failures, uncertainty and missing evidence, including restrictions on access. Comparisons across different conditions need explicit qualification. A demonstrated cumulative benefit is a measured comparison against the original and relevant single fixes on named outcomes, not the sum of individual gains. A pair's result does not establish a higher-order combination.
