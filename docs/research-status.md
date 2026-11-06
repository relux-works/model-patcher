# Research status

**6 November 2026.** Model Patcher is a documentation and research project. There is no released patch tool, validated GGUF fix, supported patch combination or measured delivery route in this repository.

**Supported** means the linked primary specification, code or publication supports the stated fact; experimental outcomes remain the authors' reports. **Inferred** marks a proposed design choice or consequence. **Unknown** means the evidence here does not establish the property. Source inspection is not execution or independent reproduction.

## A concrete targeted-weight example

**Supported, author-reported:** the published Qwen3.5-0.8B experiment touched 131,072 weight positions. Its sparse BF16 artifact records 130,188 values whose bits actually changed after rounding, in two tensors. The strongest reported Qwen run used 50 forward-pass feedback calls; gradient-free did not mean feedback-free. This is evidence for a specific targeted edit, not a guarantee that arbitrary models have similarly repairable faults. [Experiment description](https://github.com/RikiyaT/lm_understand-logs/blob/4d09ba6d6a7e891dd8063974dfe81b3d78e3494f/exp8_math/README.md), [sparse-edit manifest](https://github.com/RikiyaT/lm_understand-logs/blob/4d09ba6d6a7e891dd8063974dfe81b3d78e3494f/exp8_math/runs/p50c/edit/manifest.json).

The authors report MATH-500 improving from 7.9% to 48.1% and IFEval from 21.0% to 62.3% under their protocol. Their Gemma follow-up did not establish comparable improvement. These results were not reproduced here, and neither result establishes GGUF performance or combination compatibility. [Original article and negative follow-up](https://rikiyat.github.io/blog/weight-space-programming/).

**Supported:** the supplied applicator checks BF16 tensor shapes and before/after tensor hashes, then replaces indexed values. These checks are Python assertions and do not bind the entire model, tokenizer or configuration. The source is a useful concrete reuse reference, not a qualified general-purpose GGUF tool. [Applicator source](https://github.com/RikiyaT/lm_understand-logs/blob/4d09ba6d6a7e891dd8063974dfe81b3d78e3494f/exp8_math/code/apply_edit.py).

## What the prior art changes

**Inferred:** the appropriate next design choice is to select an existing route for a specific fix, rather than make binary differencing the default for all fixes. Git-Theta and BLAZE-X provide direct tensor-update precedents; NeuronDump and ggufpacker add native GGUF alternatives with different contracts. Existing combination benchmarks and Hub evaluation records also narrow the potential contribution to useful, discoverable evidence about exact fixes and combinations. See the verified capabilities and limitations in [reuse routes](reuse-routes.md) and [combination evidence](combination-evidence.md).

VCDIFF/xdelta remains a candidate for delivering a separately prepared exact target, alongside zstd reference compression and whole-file delivery. It cannot decide which weights to change, and two independently generated deltas from the same base cannot simply be treated as an ordered chain. No codec or route has been selected on measured size, resource use or user friction. [VCDIFF specification](https://www.rfc-editor.org/rfc/rfc3284), [zstd reference mode](https://github.com/facebook/zstd/blob/v1.5.7/programs/zstd.1.md).

## What remains unknown

- Whether the concrete BF16 edit retains its benefit after a particular GGUF conversion and quantization. For example, Q4_0 shares a scale across 32 packed values; a logical coordinate edit can disappear under rounding or affect neighboring reconstructed values. This is a representation-based inference, not a measured quality penalty. [Quantized block definitions](https://github.com/ggml-org/ggml/blob/57e2c2ca2a7cae756b1c4dfafa0cdfef9051d234/src/ggml-common.h).
- Whether two useful targeted fixes exist for the same exact base and improve together, and which orders, scales or quantizations regress.
- Which native tool supports the required coordinate operation, model architecture and output precision with sufficiently strict input checks.
- Which delivery route is simplest on the user's platform, and its actual download, memory, temporary-storage and output costs.
- Whether existing model cards and linked evaluation records are sufficient to describe and find the required evidence. A new format, applicator or service is not justified by these unknowns alone.

A future candidate should name the exact base, operation and tool before claiming a working user path. Keep the original model available for restoration; lossy export does not imply exact reversal. Contributions can improve the evidence now through [documented corrections and research reports](../CONTRIBUTING.md).
