# Proposed catalog and evidence design

**9 November 2026. Inferred design, not an adopted schema or implemented reader.** The research requires both machine readability and separate publisher/model browsing levels. Unknown applicability and quality must remain visible. Examples and proposed filenames here are illustrative.

## Keep one authority for each fact

The early recommendation was a local README and JSON pair for each fix. Subsequent multi-profile studies favored a small catalog referring to immutable evidence bundles, so that shared runs and negative comparisons do not acquire competing copies. These are logical roles; they need not become separate services or one file per role.

| Role | Authoritative content |
|---|---|
| Catalog | Stable fix identities, publisher/model navigation, registered bundle digests, applicability and missing-evidence declarations, current scoped assessment references |
| Profile and artifact | Immutable source revision; exact files, sizes and digests; native/storage/compute/cache precision; configuration, tokenizer/template, quantizer and calibration; runtime/build and hardware context |
| Treatment | Baseline or exact fix release, method, route, ordered members, scales, targets, conflict policy and intermediate/output identities |
| Run | Protocol and dataset revisions, item/draw coverage, completions or lawful references, errors, outcomes and score |
| Comparison | Referenced arms, estimand, matched outcomes, gains/losses, denominator, selection design, weights, uncertainty and comparability/refusal reasons |
| Assessment | Versioned decision policy, intended use/profile, supporting comparisons, decision and reason; observations remain unchanged |

A possible browse location is `models/<publisher>/<model>/patches/<fix-id>/README.md`, linking the authoritative catalog record and evidence. Stable fix identity survives a directory rename. Fix release, schema version, artifact digest and evaluation protocol answer different questions. An advertised digest is distinct from a locally verified digest; neither proves quality or publisher identity.

## Alternatives considered

| Layout | Useful property | Cost or condition |
|---|---|---|
| Per-fix Markdown and JSON | Contributions are local and readable | Repeated base facts and shared runs need explicit references |
| Shared model metadata plus fix/run records | Reduces actual duplication | Reference resolution and coordinated updates become necessary |
| Structured upstream model card | Reuses an existing authoritative home | Must still bind exact artifacts, combinations and retained evidence; nested local cards are not automatically Hub-indexed |
| Central catalog plus linked Markdown | Simple snapshot for a machine consumer | Concurrent edits and immutable evidence linkage need care |

The recommended catalog/bundle arrangement uses the last option for discovery while allowing local fix explanations. No measured maintenance or usability ranking selects it uniquely. Add a generated discovery view only when a consumer needs it; identify its source snapshot and derive it rather than hand-editing a second authority. A prose-only collection would not meet the machine-readability requirement.

## Identity and refusal rules

GGUF is a container, and a label such as Q4 does not identify a complete quantization recipe. Native BF16, FP16 conversion, Q4_K_M, NF4, NVFP4 and FP8 profiles must not silently alias. Bind tensor mixtures and execution precision separately. Existing [quantization and delivery limits](reuse-routes.md#identity-quantization-and-evidence) explain why logical coordinates, packed bytes and exact output identities differ.

Native-edit→quantize, direct supported quantized editing, dequantize→edit→requantize, merged adapters and runtime adapters are different treatments. A route that changes affected tensors to another precision must expose that output. General adapter documentation does not qualify arbitrary model/format/runtime combinations.

For runtime adapters, identify the unchanged base **and** the ordered adapter payload/configuration digests, scales, resolved targets, composition/conflict policy and runtime/execution settings. There may be no materialized output weight file. A descriptor digest identifies the descriptor, not unseen adapted weights. Changing order creates a different request identity; whether it changes behavior is a separate question. Refuse a support claim for unresolved targets, missing payload identity or unsupported composition, while retaining the request and reason.

Readers should check a documented application-level version before interpreting operational fields. Define absent, unknown and unsupported separately; do not supply application defaults from missing information. Permit ignored descriptive extensions only in a documented area. A new applicability restriction is operational even if its field is optional. An incompatible meaning change requires a new version and a clear unsupported-version response. Automatic migrations remain deferred. JSON Schema's [`$schema`](https://json-schema.org/draft/2020-12/json-schema-core#name-the-schema-keyword) identifies a schema dialect; it is not itself the catalog's application contract version.

## Complete discovery and retained corrections

Discovery should enumerate every run, comparison, assessment and correction in every registered, digest-checked bundle. Include negatives, refused comparisons and unassessed runs. Coverage declarations add missing, unsupported and out-of-scope requests; they do not replace that inventory. Completeness is relative to a pinned registered snapshot. An inaccessible source makes completeness unresolved.

Use bundle-local identifiers internally and digest plus record pointer across bundles, with replaceable retrieval locations. Preserve original records and explicit correction/replacement edges, reasons and the selected current interpretation. Missing, cyclic or unresolved divergent correction chains must not yield a unique current answer. Additional conflicting observations coexist; a policy reassessment does not rewrite a measured score. A positive subset does not supersede a negative full-set observation.

Keep these states distinct: not evaluated, unsupported applicability, refused comparison, observed regression, inconclusive assessment and supported for a specified use. **Reject** requires an adequately established failed criterion or declared veto. **Inconclusive** covers weak design, unresolved identity, missing arms or bounds crossing the decision margin. Successful application/loading and a missing negative result are insufficient for support.

## Four-arm illustrative example

**Synthetic, not measured:** assume one frozen set of 500 items, the same scorer and matched item/draw identities. N0/NP denote native baseline/patched; Q0/QP denote one exact consumer-profile baseline/patched.

| Profile | Baseline | Patched | Within-profile gain |
|---|---:|---:|---:|
| Native | 400/500 = 80% | 450/500 = 90% | +10 percentage points |
| Consumer | 380/500 = 76% | 370/500 = 74% | −2 percentage points |

Define `LQ=S(N0)−S(Q0)`, `GN=S(NP)−S(N0)` and `GQ=S(QP)−S(Q0)`. Here LQ is +4 points and the difference of gains `GQ−GN` is −12 points. This is not a retention ratio. With runtime, hardware or cache changes, LQ and the gain difference compare complete delivery systems; they do not isolate quantization as the cause.

Marginal totals suffice for those descriptive differences, but not their paired uncertainty. Retain each item's four-arm vector and preserve shared-arm dependence in analysis. Refuse an intended paired comparison with missing item/draw provenance, unresolved source digests, undeclared scorer changes or incompatible denominators without an appropriate declared estimator. Intentional profile differences belong only in the named cross-profile contrast. N0→QP cannot substitute for Q0→QP. Missing consumer evidence never inherits native scores.
