# Evaluation design and claim limits

**9 November 2026.** These are research recommendations and illustrative arithmetic, with no model evaluation performed here. No universal sample size or pass threshold has been adopted.

## Select a question before a benchmark

| Candidate task | Intended evidence | Important limit |
|---|---|---|
| [IFEval](https://huggingface.co/datasets/google/IFEval), 541 prompts | Instruction following, with declared strict/loose and prompt/instruction metrics | A length-restricted or shortened diagnostic is not the full original protocol |
| [HumanEval](https://github.com/openai/human-eval), 164 functions; [HumanEval+](https://github.com/evalplus/evalplus) | Function correctness under original and expanded tests | More tests do not automatically mean more model prompts; generated programs require isolated, bounded grading |
| [GSM8K](https://github.com/openai/grade-school-math), 1,319 test problems | Math under a pinned prompt and extraction rule | Short greedy answers do not reproduce a longer stochastic release protocol |
| [MATH-500](https://github.com/openai/prm800k#math-splits), 500 problems | A targeted math claim under a declared grader | Distinct from full MATH; scoring and data-use terms need separate checks |
| [MMLU-Pro](https://github.com/TIGER-AI-Lab/MMLU-Pro) | Optional knowledge/reasoning domains | No capacity claim here; not interchangeable with MMLU |
| [SWE-bench](https://www.swebench.com/SWE-bench/guides/evaluation/) | Repository issue repair with a named scaffold, environment and tests | Function tests do not establish repository-task performance; setup, tool waits and grading add work |

Call an evaluation **full protocol-comparable** only when population, prompts, scoring, model mode, repetitions and relevant execution conditions match the named reference. A **sampled same-task** result preserves the task/protocol with fewer selected items and appropriate bounds. An **adapted diagnostic** changes conditions and must name them. Merely completing the full population does not establish release comparability.

The bounded planning suite is 541 + 164 + 1,319 + 500 = **2,524 generation requests per treatment**, with one draw per item. It shares HumanEval/HumanEval+ completions only where prompts and generation conditions match, and still charges expanded scoring. A 150-target + 50-instruction + 40-code screen is 240 requests, not full confirmation. Different seeds, additional draws or incompatible code prompts add work.

## Paired observations and evidence levels

A smoke check can find loading, formatting or gross behavioral faults. A small paired diagnostic describes its selected examples. A complete deterministic fixed-test census describes that test exactly. A population or expected-over-decoding claim needs a valid sampling or repeated-run design in addition to retained outcomes. These are different scopes, not automatic certification levels purchased by larger budgets.

Freeze candidate bytes, intended populations, metrics, guardrails, selection, stopping and failure rules before confirmation. Record dataset/item revisions, serialized prompts/template, tokenizer, scorer, runtime/build, precision, thinking/output limits, seeds/draws and lawful output references. Preserve truncations, refusals, parse errors, timeouts and incomplete work under the declared denominator; distinguish infrastructure/scorer faults from model outcomes. Budget exhaustion must not become a passing result.

Let G be baseline-fail/candidate-pass and L baseline-pass/candidate-fail. For n matched binary outcomes, `delta=(G−L)/n`. Retain both-pass and both-fail cells too. **Illustrative:** starting from 400 correct of 500, G=75 and L=25 yields 450 correct, a +10-point fixed-set change. Looking only at the 100 old failures cannot detect damage among the 400 old passes.

Under an **assumed iid paired-population model**, `D=candidate_pass−baseline_pass`, discordance `q=pG+pL`, and `Var(D)=q−delta²`. Two marginal scores do not identify q. The [exact McNemar procedure](https://www.statsmodels.org/stable/generated/statsmodels.stats.contingency_tables.mcnemar.html) uses discordant pairs and a binomial null; it tests a different claim from a practical lower effect bound. Detecting positive change does not establish that improvement is at least ten points. The census description alone needs no task-sampling interval; generalization beyond that set remains unresolved.

For sampling without replacement from known baseline failures/passes, freeze the patch first and sample both strata using recorded inclusion probabilities. With stratum sizes 100 and 400, sampled counts nF/nP and observed repairs x/losses y, the weighted estimate is `.2*x/nF−.8*y/nP`. Those weights change for another baseline. Use a valid finite-population interval and account for the selection design; zero sampled losses do not prove zero total losses. An authored illustrative subset has no executed random-selection provenance and supports no such inference. [Stratified sampling methodology](https://www150.statcan.gc.ca/n1/pub/12-001-x/2015002/article/14249/02-eng.htm).

## Regression, equivalence and repeated use

Specify intended-use domains, practical noninferiority margins and severe-failure vetoes before seeing results. A valid one-sided lower effect bound must exceed the negative margin; a nonsignificant regression test is insufficient. Equivalence needs both directional bounds inside a declared tolerance. A wide interval crossing zero is inconclusive. [Paired equivalence-test structure](https://www.statsmodels.org/stable/generated/statsmodels.stats.weightstats.ttost_paired.html).

Declare the claim family across candidates, profiles, domains, combinations/orders and interim looks. Fixed-family adjustments such as [Holm](https://stat.ethz.ch/R-manual/R-devel/library/stats/html/p.adjust.html) cannot repair holdout overfitting or invalid tests. Protect confirmation data where the intended claim needs it, retain failed submissions, and use fixed stopping unless a valid sequential procedure is specified. Fresh public-task sampling does not establish absence of training exposure or development contamination. [Adaptive-analysis limitations](https://arxiv.org/abs/1411.2664).

Three identical deterministic greedy runs do not supply three independent task samples. Explicit stochastic repetitions require item×draw records and analysis retaining within-item and shared-control dependence. Reproducibility checks and new evidence acquisition have different purposes.

## Count arms and reuse observations explicitly

| Question | Required distinct arms | Full-suite requests, all fresh |
|---|---|---:|
| Total AB benefit | 0, AB | 5,048 |
| Increment after A plus total benefit | 0, A, AB | 7,572 |
| Compare AB with both components | 0, A, B, AB | 10,096 |
| Add reverse-order comparison | 0, A, B, AB, BA | 12,620 |
| Consumer order study plus native A gain | Q0, QA, QB, QAB, QBA, N0, NA | 17,668 |

These are alternative scopes. They assume actual supported treatment routes; the counts do not qualify them. The bill is the union of required observation nodes, with shared arms counted once. AB improvement cannot be predicted by adding singleton gains. The accuracy-scale interaction `S(AB)−S(A)−S(B)+S(0)` needs all four arms and joint uncertainty for inference. Changed scales/routes describe complete recipes, rather than an isolated same-dose interaction.

Exact reuse requires matching artifact/treatment, runtime numerical context, prompt/tokenizer/template, item/draw coverage, decoding/thinking limits, failure policy and scorer, with retained completion and outcome provenance. A bare score or unchanged model name is insufficient. Reuse only matching nodes, disclose historical acquisition separately, and retain induced covariance. A changed scorer may allow symmetric regrading of retained completions; it creates new scoring evidence and cost, not free unchanged outcomes.

In the seven-arm example, reusing only Q0 saves 2,524 requests, leaving 15,144. Reusing both Q0 and N0 leaves 12,620. No baseline transfers between models or consumer profiles. [Cross-profile comparisons](catalog-and-evidence.md#four-arm-illustrative-example) require their own matched arms; native success cannot fill a missing consumer result.
