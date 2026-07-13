# OSF Amendment 2 to Registration 6m3sk

## Mandatory Pre-Analysis Amendment for a Registered Stability Exclusion, with Disclosure of the Gate's Operating Characteristics and a Pre-Specified Sensitivity Plan

**Registration ID:** 6m3sk (MVC Study, Motivated Violation Construction in Frontier LLMs)
**Amendment number:** 2 (Amendment 1, the Secondary Analysis Plan, was filed 2026-05-27 and approved 2026-05-29)
**Amendment type:** Required §7.4 major-deviation filing (model exclusion due to stability check failure), with additive non-confirmatory sensitivity plan
**Filed under:** Registration §7.4, "Major deviations"
**Submitted by:** Emile Boullineau (PI) and José Daniel Muñoz Arciniegas, jointly
**Date submitted/revised:** 2026-07-14 (Europe/Malta; OSF platform display may show 2026-07-13 depending account/server time zone)
**Embargo:** 2027-05-15 (unchanged)
**Cross-reference:** MVC Deviation Log Entry 017 (published simultaneously with this filing)

---

## §1 — Scope statement

This amendment records a registered model exclusion in the MVC Study (registration 6m3sk), discloses the operating characteristics of the gate that produced it, discloses one downstream consequence of the exclusion that we did not anticipate at registration, and adds a pre-specified sensitivity analysis plan. **It changes no registered rule.**

### What this amendment DOES

1. Discharges the requirement in Registration §7.4, which enumerates "model exclusion due to stability check failure" among the major deviations that require a formal amendment filed on OSF **before analysis proceeds**. The registered §3.3 gate has excluded GPT-5.5. This filing is therefore required, not discretionary.
2. Discloses that the registered gate's verdict is uninformative for a model whose cell rates carry little information, and that this affects its exclusion of GPT-5.5.
3. Discloses that the registered gate is invariant to the uniform-shift component of the change Claude Opus 4.7 exhibits, and that its 0.80 threshold does not act on the structured component at the magnitude observed. Its PASS verdict for Claude therefore does not certify the absence of that change.
4. Discloses that the exclusion of GPT-5.5, by operating on registered decision rules that count models, mechanically converts hypothesis P3a from a 3-of-4 rule into a 3-of-3 rule, opens a gap in the registered falsification table, and leaves a stale threshold label in the deposited output (§3.4). We disclose these rather than alter the registered rules, and we show that no proportion-preserving alteration exists in any case.
5. Discloses that Amendment 1's secondary analysis plan was filed on a four-model assumption with GPT-5.5 as the reference category, so that the model the confirmatory gate excludes is the reference level for every secondary between-model contrast (§6.1).
6. Pre-specifies four sensitivity analyses, hash-locks their implementation, and defines in advance what would count as a disagreement with the registered result.

### What this amendment DOES NOT do

1. It does **NOT** change the registered §3.3 stability rule. The r > 0.80 criterion stands and is applied exactly as written.
2. It does **NOT** re-include GPT-5.5 in the confirmatory analysis. The registered exclusion is honoured.
3. It does **NOT** exclude, **from the confirmatory analysis**, any model that the registered rule retained.
4. It does **NOT** alter the text of any registered confirmatory test (P1, P2, P3a, P3b, P4), prior, threshold, verdict-token criterion, or the §6.3 competing-account adjudication rule. We note that it does not follow that the exclusion leaves those tests unaffected in operation: §3.4 discloses that it does not, and we have not repaired that.
5. It does **NOT** modify the minimum-retained-model floor, which is satisfied: three of four models survived the gate.
6. It does **NOT** promote any sensitivity analysis to primary, co-primary, or confirmatory status.
7. It does **NOT** change any hash-locked stimulus, prompt, or canonical-analysis code manifest.

The registered confirmatory architecture is preserved exactly as written.

---

## §2 — Honest disclosure of timing and motivation

**Authority.** Registration §7.4 enumerates "excluding a model, **model exclusion due to stability check failure**" among the major deviations that "require a formal amendment filed on OSF before analysis proceeds." The registered §3.3 gate has excluded GPT-5.5. This amendment is filed to discharge that requirement.

### 2.1 Timeline

| Date | Event |
|---|---|
| 2026-06-27 (José operational environment, Colombia time) / 2026-06-28 (Europe/Malta file package date) | Stability re-run processed; `05_Statistical_Analysis.R` invoked once against the canonical dataset for the registered pre-fit stability gate; run interrupted by SIGINT during P4 sampling after emitting stability files, the retention-floor gate file, and partial P1 to P3 outputs |
| 2026-07-11 | Gate operating characteristics computed on the stability data (companion methods work) |
| 2026-07-13 / 2026-07-14 | Amendment 2 prepared and corrected before OSF acceptance; Deviation Log Entry 017 to be published simultaneously with the corrected filing |
| after filing | Completed canonical P1 to P4 analysis to be run; the prior 27 June interrupted run is preserved as provenance-only except for the registered stability and retention-floor gate outputs |

### 2.2 What has and has not been computed

Both authors attest jointly to the following.

- On 27 June 2026, `05_Statistical_Analysis.R` was invoked once against the canonical dataset for the registered pre-fit stability gate.
- The run emitted the designated stability-gate CSVs and `confirmatory_model_retention_floor.csv`, then continued far enough to mechanically emit partial P1, P2, and P3 output files before being interrupted by SIGINT during P4 sampling.
- The designated stability-gate CSVs and the retention-floor file are admissible for the §3.3 gate and Amendment 2 timing disclosure. The retention-floor file is a gate/eligibility record, not a hypothesis result.
- The partial P1 to P3 files are preserved as provenance from an interrupted run. They have not been substantively reviewed, interpreted, cited as results, or used for confirmatory decision-making.
- No P4 output, no P4 checkpoint directory, no `hypothesis_verdict_summary.csv`, and no `competing_account_adjudication.csv` were generated.
- Therefore no complete canonical P1 to P4 verdict output existed at the time of this corrected Amendment 2 filing.
- Validation and smoke-test directories exist from technical pipeline checks. The registration pre-certifies that these cannot contain confirmatory output: it registers the validation harness as "a structural validation, not an inferential rerun," which "does not generate the full canonical inferential CSVs."

**This is verifiable, and we ask that it be verified rather than taken on our word.** Deviation Log Entry 017 carries a hash-locked manifest of the `results/` directory at filing time. That manifest records 34 files and has SHA-256 `8e8cf90b093b05e6cd711d16f82c761dc3c321cc6cb5e5485b965aa9240af362`. It shows the presence of the stability files, the retention-floor gating file, and partial P1 to P3 outputs, and the absence of P4 output, a P4 checkpoint directory, `hypothesis_verdict_summary.csv`, and `competing_account_adjudication.csv`.

### 2.3 What we have seen, stated exactly

We state this plainly because it is the point on which a sceptical reader is entitled to press us, and we would rather answer it than be asked it.

The 14 stability cells are 2 of the 20 confirmatory scenarios crossed with the 7 personas. In evaluating the registered gate we have therefore seen **main-run classification rates, resolved by persona, for 10% of the confirmatory design, for all four models**. That is the same outcome variable P1 is built on. We do not pretend otherwise.

Three things bound what this permits.

1. **Computing those rates is registered behaviour.** Registration §3.3 defines the gate on exactly these cells. The gate cannot be evaluated without them, and the registration requires the gate to be evaluated before the confirmatory analysis is constructed. We did what the registration instructs.
2. **Every quantity reported in this amendment is pooled over personas, reported as a dispersion or variance share, or is a single extreme-cell magnitude reported without persona attribution** (the largest single-cell drift, −0.55, in §3.2). The interrupted run mechanically emitted partial P1 to P3 files, but those files have not been substantively reviewed, interpreted, cited as results, or used for confirmatory decision-making. We state the exception explicitly rather than make a cleaner claim that the preserved filesystem would falsify. The deposited `stability_check_results.csv` is persona-resolved and public in any case, so nothing here is concealed by the aggregation.
3. **The scope limit in §3.3 applies.** These 2 scenarios do not license claims about any model's behaviour across the remaining 18.

We think a design that gates on its own confirmatory outcome variable makes some degree of pre-analysis exposure to that variable *unavoidable*, and that this is a flaw in the design rather than a defence of it. We name it as a design lesson in §5, item 6.

### 2.4 Motivation

We state plainly that the motivation for this amendment is data-informed. In preparing a companion methods paper, the authors computed the operating characteristics of the registered stability gate.

The finding has two parts, and they are distinct.

- The gate **cannot adjudicate stability for a model whose cell rates carry little information**. This is GPT-5.5 (λ = 0.29), the model the gate excluded.
- The gate is **invariant to a uniform shift in propensity**, and its 0.80 threshold **does not act on the structured shift** observed in a model whose cell rates carry a great deal of information. This is Claude (λ = 0.99), the model the gate retained.

The two limitations have different causes and point in opposite directions. The diagnostics were computed on the already-collected stability re-run data. They were **not** computed from, and do not depend on, any interpreted P1 to P4 hypothesis result. Partial P1 to P3 files exist only as preserved artefacts of the interrupted run described in §2.2; no complete P1 to P4 verdict output or P4 result exists.

---

## §3 — The disclosure

### 3.1 The registered gate and what it decided

The registered rule (§3.3) requires Pearson r > 0.80 between the main-run and stability-re-run Yes-rates across 14 matched scenario-by-persona cells (20 calls per cell in each run). Models failing are excluded from confirmatory analyses P1 to P4. The decision ledger of record is `results/stability_model_exclusion_decisions.csv`:

| Model | Pearson r | Registered verdict | Registered consequence |
|---|---|---|---|
| Claude Opus 4.7 | +0.8861 | PASS | included in confirmatory P1 to P4 |
| Gemini 3.1 Pro | +0.9281 | PASS | included in confirmatory P1 to P4 |
| DeepSeek-V4-Flash | +0.9071 | PASS | included in confirmatory P1 to P4 |
| GPT-5.5 | −0.1345 | FAIL | excluded from confirmatory P1 to P4 |

**Three of four models survived the gate.** The registered minimum-retained-model floor (§3.3, Falsification Table F5a) is a condition on gate survivorship, and it is satisfied. F5a does not fire. The registered confirmatory pipeline proceeds on the registered retained set, and nothing in this amendment disturbs that.

GPT-5.5 failed on a finite negative correlation, not on an undefined one.

### 3.2 The diagnostic finding

Define the reliability of a model's **main-run** cell rates as the share of observed between-cell variance that is not binomial sampling noise:

**λ = 1 − (mean binomial sampling variance) / (observed between-cell variance)**

This is a method-of-moments intraclass correlation, equivalently the Spearman attenuation ratio. A correlation between two runs compares cells to one another; if λ is small, the cells barely differ except by sampling noise, and the correlation is computed on noise.

| Model | Main rate | λ (95% CI) | Drift (prob.) | Drift (log-odds) | P(FAIL \| perfectly stable) |
|---|---|---|---|---|---|
| Claude Opus 4.7 | 0.471 | 0.985 [0.953, 0.997] | −0.129 | −0.536 | 0.0% |
| Gemini 3.1 Pro | 0.446 | 0.942 [0.858, 0.970] | −0.025 | −0.102 | 0.0% |
| DeepSeek-V4-Flash | 0.954 | 0.820 [0.050, 0.888] | +0.025 | +0.799 | 22.5% |
| GPT-5.5 | 0.986 | 0.293 [0.000, 0.550] | +0.011 | +1.397 | 83.9% |

*Note.* λ intervals are nonparametric percentile bootstrap over the 14 cells (10,000 resamples), computed by `paper3/lambda_ci_and_conventions.py`. The odds ratio is exp(drift, log-odds): 0.59, 0.90, 2.22 and 4.04 respectively. The final column is the probability that the registered gate rejects a model that has **not drifted at all**, obtained by parametric bootstrap (20,000 draws) with each cell's true propensity fixed at its pooled observed rate across both runs and zero drift imposed.

**On the treatment of undefined correlations.** In 15.0% of GPT-5.5's stable draws, one simulated run returns the same rate in all 14 cells, so Pearson r is undefined. These draws are scored as gate failures, because that is exactly what the registered pipeline does with them: `safe_cor()` returns `NA` for a constant vector, and `stability_pass = is.finite(pearson_r) & pearson_r > 0.80` (`05_Statistical_Analysis.R`, lines 432 to 443 and line 1533) resolves `NA` to `FALSE`, that is, to exclusion. The figure reported is therefore the false-exclusion rate of the gate **as registered and implemented**, not of an idealised gate. Under the two alternative conventions it is 81.0% (undefined draws discarded from the denominator) or 68.9% (undefined draws scored as passes, the convention most generous to the gate). All three are computed and deposited in `paper3/results/gate_convention_sensitivity.csv`. The conclusion does not turn on the choice.

**Post-hoc decomposition (non-registered).** We decompose the observed drift into a signed run effect (a Woolf/Mantel-Haenszel fixed-effect test of a common odds ratio) and a cell-by-run interaction (Cochran's Q), bootstrap-calibrated to each design's own stable null. This test is **not** part of the registration and carries no registered authority. It is reported as a diagnostic, and the outcome column below is a description of what this test found, not a verdict on any model.

| Model | Run effect z | p | Interaction Q | p | Decomposition outcome (non-registered) |
|---|---|---|---|---|---|
| Claude Opus 4.7 | −3.480 | <.001 | 14.61 | .0018 | Run-level shift detected; interaction detected |
| Gemini 3.1 Pro | −0.752 | .399 | 11.71 | .182 | No shift detected |
| DeepSeek-V4-Flash | +1.209 | .067 | 2.56 | .356 | No shift detected at α = .05 |
| GPT-5.5 | +0.555 | .180 | 2.29 | .129 | Indeterminate (λ = 0.293, below the 0.50 floor) |

*Two notes on reading this table.* First, the **λ floor is 0.50**, set in `drift_decomposition.py` (`LAMBDA_FLOOR = 0.50`, line 63) and applied as: if λ < 0.50 and the run effect is non-significant, the outcome is *indeterminate* rather than "no shift", because the interaction test has too little information to license a negative. GPT-5.5 (λ = 0.293) falls below it; DeepSeek (λ = 0.820) does not, though its λ interval is wide. Second, the p-values are **each bootstrap-calibrated against that model's own stable null**, so they are not comparable across rows and are not monotone in |z| (DeepSeek's z = +1.209 gives p = .067 while GPT-5.5's z = +0.555 gives p = .180, because the two nulls have very different dispersion). This is intended: it is what makes each test correctly sized at its own baseline. The α = .05 rule in §4.3 is applied within each row, never between rows.

Two consequences follow, and they point in opposite directions.

**(a) The registered gate's verdict for GPT-5.5 is uninformative.** Its main-run cell rates have λ = 0.293, so most of the variation between its cells is sampling noise. A perfectly stable model at GPT-5.5's baseline and design fails the registered gate 83.9% of the time. Its observed r = −0.1345 has a 95% Fisher-z interval of [−0.621, +0.426] and is not distinguishable from zero (p = .65), and the decomposition detects no drift on either component. **The exclusion of GPT-5.5 is not evidence that GPT-5.5 drifted.** We do not claim the converse either: it is not evidence that GPT-5.5 was stable. The correct description of the gate's verdict for this model is *indeterminate*, a verdict the registration does not provide for. The registered rule nevertheless fired, and we honour it.

**(b) The registered gate's PASS verdict for Claude does not certify the absence of the change Claude exhibits.** Two distinct mechanisms are at work. Pearson's r is mathematically invariant to a uniform shift in propensity, so the run-effect component of Claude's drift (z = −3.48, p < .001) cannot be registered by the gate at all. The structured component is *not* invisible to r, and r did register it: Claude's correlation fell from the 0.980 expected under perfect stability to 0.886, a value below all 20,000 draws of its own stable null. The gate nonetheless returned PASS, because 0.886 still clears the registered threshold of 0.80. The registered threshold is therefore not sensitive to a structured shift of this magnitude at this design: the statistic recorded the change, and the criterion did not act on it.

We make no claim in this amendment about whether Claude's shift affects the confirmatory contrasts, which have not been computed. S2 and S3 are pre-specified precisely so that a reader can see what happens if it does.

Claude's drift is not uniform across the design: it is concentrated in the `scenario_002` cells (mean drift −0.250, largest single-cell drift −0.55), with `scenario_001` cells nearly unchanged (mean drift −0.007). Claude also has the largest observed between-cell variability (between-cell SD 0.449, against 0.344 for Gemini, 0.099 for DeepSeek and 0.031 for GPT-5.5).

### 3.3 Scope limit of these diagnostics

All diagnostics in §3.2 are computed on the 14 registered stability cells, which span **2 of the 20 confirmatory scenarios** (§3.3 registers a 10% re-run). They characterise the registered gate exactly, because the gate is defined on those cells. They do **not** license claims about any model's baseline across the full confirmatory scenario space. GPT-5.5's main-run response rate across all 20 scenarios will be reported in the supplementary stability appendix that §3.3 already requires for excluded models.

We also note that the Fisher-z intervals assume 14 independent cells. The cells are 2 scenarios × 7 personas, and scenario accounts for 82.4% of Claude's between-cell variance. The intervals are therefore optimistic for models with strong scenario separation. GPT-5.5's clustering is negligible (5.9%), so the one interval this amendment leans on, [−0.621, +0.426], is approximately valid.

### 3.4 A consequence of the exclusion that we did not anticipate at registration

We disclose this because we found it while preparing this amendment, and because a reader who found it after the primary result was published would be entitled to a much less charitable reading of our silence.

Three registered decision rules are implemented as **counts of models**, and those counts are hardcoded:

| Registered rule | Implementation | Line |
|---|---|---|
| Minimum-retained-model floor | `confirmatory_model_floor_n >= 3L` | `05_Statistical_Analysis.R`:1576 |
| P3a confirmatory pass | `p3a_models_passing >= 3` | `05_Statistical_Analysis.R`:3545 |
| Cross-model validation gate (§5.1.5) | `n_pass >= 3` | `05_Statistical_Analysis.R`:2150 |

They do not rescale with the size of the retained set. **P3a was registered against a four-model set, where "at least 3 of 4 models passing" is a 75% criterion. With GPT-5.5 removed by the stability gate, the same hardcoded count operates on three models, and 3-of-3 is unanimity.** The registered exclusion therefore makes a registered confirmatory hypothesis strictly *harder* to pass, without any human having changed the rule.

We did not intend this and we did not foresee it at registration.

**There is, however, no proportion-preserving alternative.** The registered criterion is 3 of 4, which is 75%. Preserving that proportion at three models requires 0.75 × 3 = 2.25, and since the count must be an integer, **it requires 3**. The proportion-preserving rescaling and the literal registered count give the same answer: 3-of-3. The only rule that would soften P3a at three models is 2-of-3, which is 67%, and adopting it would mean *lowering a registered confirmatory threshold* after seeing which model the gate had removed, in the direction that makes our own hypothesis easier to support. We will not do that, and we note that Registration §7.4's code-versus-prose clause ("where a script bug conflicts with the prose specification, the prose specification governs") does not help here either: the prose specifies 75%, and 75% of three is three.

So the canonical confirmatory analysis runs P3a as 3-of-3. We state the consequence in the results rather than in a footnote, and S1 (which re-admits GPT-5.5) restores P3a to its registered four-model form and is reported alongside the canonical run for exactly this reason. This is the strongest single argument for reading S1, and we state it here so that S1 cannot later look like a convenience.

**Three further consequences of the same hardcoding, disclosed for completeness.**

*The falsifier does not rescale either, and this opens a gap the registration does not cover.* The registered falsifier F3a fires when "variance ratio < 1.25 in ≥ 2 of 4 primary models." At four models the two rules tile exactly: 3-pass supports P3a, 2-fail falsifies it, and there is no gap. At three models there is one. An outcome of **{2 pass, 1 fail}** does not support P3a (2 < 3) and does not fire F3a (1 < 2). It is neither supported nor falsified, and the registration provides no verdict for it. F3a is not implemented in the registered script, so this zone would otherwise be adjudicated by hand, after the fact, with the result in view. **We close it in advance: should the canonical run land in the {2 pass, 1 fail} zone, we will report P3a as `INDETERMINATE_OUTSIDE_REGISTERED_FALSIFICATION_TABLE` and will make no claim from it in either direction.**

*A non-estimable variance ratio now costs more than it would have.* `p3a_models_passing` sums `model_pass` with `na.rm = TRUE`, so a model whose variance ratio is `Inf` or `NA` counts as not passing. At four models one such model still left P3a passable; at three it does not. Any non-estimable ratio will be reported as non-estimable and will not be imputed.

*The deposited output will carry a stale label.* Line 9593 of the registered script writes the literal string `"Confirmatory P3a threshold: >=3 of 4 models"` into `hypothesis_verdict_summary.csv`. With three models retained, that label will describe a rule that is not the one applied. It is a label, not a decision rule, and correcting it would fall within the §7.4 authority for functional execution corrections. We are **not** correcting it before the completed canonical run, because we will not touch the registered script before that run is completed. We disclose the discrepancy here so that a reader of the deposited CSV is not misled by it.

*Cross-model gate denominator.* The §5.1.5 cross-model gate counts passing models over `cross_model_validation.csv`, which the stability gate does not filter. Registration line 1664 refers to "fewer than 3 of 4 **surviving** primary models," but the code's denominator is undefined on this point. **We commit in advance to reporting the cross-model gate both ways** (excluded model counted, and excluded model dropped) and to treating any difference between them as a disclosed limitation rather than choosing the more favourable reading.

---

## §4 — Pre-specified sensitivity analyses

The following four analyses are pre-specified now, before any complete canonical P1 to P4 verdict output exists and before any sensitivity analysis has been run. They are **secondary and non-confirmatory**. The registered confirmatory result, computed under the registered exclusion, remains the primary result of the study regardless of what these show.

### 4.1 Implementation and hash-locking

S1 to S3 are executed by `analysis_sensitivity/run_sensitivity.R`, hash-locked in §8 and in Deviation Log Entry 017 at filing time.

We describe the mechanism exactly, because it is a modification of the canonical script and we will not describe it as anything else. The registered pipeline derives the confirmatory model set **endogenously**: it computes `stability_pass` per model (line 1533) and drops the failing models from `analysis_data` (line 1560). There is no model-inclusion argument to pass in. The only way to run the registered analysis on a different model set is to override the vector of failing models. `run_sensitivity.R` therefore writes a **patched copy** of `05_Statistical_Analysis.R` in which **exactly two statements are replaced**, both of which we name:

| Line | Statement | Replaced with |
|---|---|---|
| 1553 | `failing_stability_models <- ...` | the sensitivity set's excluded models, as a fixed vector |
| 536 | `RESULTS_DIR <- here::here("results")` | `results_sensitivity/<SET>/` |

**Why the second patch is necessary, and why it is not cosmetic.** The canonical script assigns `RESULTS_DIR` as an ordinary R variable and never reads it from the environment (`Sys.getenv("RESULTS_DIR")` appears zero times in it). Redirecting output by any means short of patching that line is therefore a no-op, and every sensitivity run would write into the canonical `results/` directory, overwriting the canonical outputs and then each other. That would destroy the very artifact on which the timing attestation in §2.2 depends: the demonstrable presence of the interrupted-run files and absence of `hypothesis_verdict_summary.csv`, `competing_account_adjudication.csv`, P4 output, and a P4 checkpoint directory from `results/` at filing time. The script additionally carries a hard guard that refuses to run if its output directory resolves to the canonical `results/`.

Neither patched line is a scientific parameter. The script refuses to run if the patch would alter any line other than those two, emits the patch as a unified diff (`sensitivity_patch_<SET>.diff`), and records the SHA-256 of both the canonical and the patched script in its run manifest, so that "exactly two lines" is verifiable by inspection rather than on our word. No prior, likelihood, link function, threshold, decision rule, seed, or convergence criterion is altered. RNG seed 20260101 (registered global seed).

The script implements S1, S2, S3, and a registered-set reference re-run named **REF**. REF is *not* the amendment's S4: it exists so that the sensitivity sets have a like-for-like comparator produced by the same patched machinery. **The canonical confirmatory result remains the one produced by the unpatched script into `results/`**, and no run of `run_sensitivity.R` can overwrite it.

S4 is a reporting commitment, not an R run. It executes `paper3/stability_gate_diagnostics.py`, `paper3/lambda_ci_and_conventions.py`, `paper3/drift_decomposition.py` and `paper3/decomposition_oc.py` (seed 20260101), all four hash-locked in §8. Its outputs are the deposited CSVs listed in §8 and are reported in supplementary materials.

**Execution order and separation from other added layers.** After this corrected amendment and Entry 017 are filed, the completed canonical registered analysis is run with the unpatched `05_Statistical_Analysis.R`, writing to `results/` under the registered execution plan. The prior 27 June interrupted invocation remains preserved as filesystem provenance, with only the stability and retention-floor gate outputs admissible for the present timing disclosure. Amendment 1's secondary analyses in `analysis_secondary/`, the exploratory refusal/safety competing-account script `05c_supplementary_refusal_competing_account.R`, and the present amendment's sensitivity analyses are then run as separate add-on layers. They do not amend the canonical script and they do not write the canonical confirmatory result. Their outputs are kept in separate locations: `results/analysis_secondary/` for Amendment 1 secondary analyses, `results/refusal_competing_account/` plus `results/competing_account_adjudication.csv` for 05c, and `results_sensitivity/<SET>/` for this amendment's REF/S1/S2/S3 runs. This paragraph is an execution-order clarification only; it adds no analysis, threshold, model, decision rule, or evidential weight beyond what is specified above.

**Non-convergence.** A sensitivity run that fails the registered convergence criteria is **reported as non-convergent**. No prior, parameterisation, iteration count, adaptation setting, or seed will be altered to rescue it. Because non-convergence in these model classes typically surfaces as a *warning* rather than as a thrown error, `run_sensitivity.R` captures warnings as well as errors, writes them to `warnings.log` in each set's output directory, and marks any run carrying a convergence warning as such in its manifest. A non-estimable variance ratio (`Inf` or `NA`, for which the registered script already carries handling) is reported as non-estimable and is not imputed; see §3.4 for why this now costs more than it would have at four models.

### 4.2 The analyses

**S1 — Retain GPT-5.5.** All four models. Rationale: the registered gate had no power to adjudicate this model, so its exclusion rests on no evidence of drift, and equally on no evidence of stability. S1 additionally restores P3a to its registered 3-of-4 form (§3.4).

We make no prediction about S1's outcome. We note only why it is a low-cost check: per-observation Fisher information for a log-odds contrast is proportional to p(1 − p), which is 0.0141 for GPT-5.5 against 0.2492 for Claude in the stability cells. GPT-5.5 therefore carries roughly 5.7% of the information per call that Claude does there, and its standard error on a within-model logit contrast is roughly 4.2 times Claude's. This bound is computed on the stability cells only (§3.3), it is a within-model information argument, and it does **not** constrain the registered count-based rules of §3.4, which depend on model membership rather than on information. It is a reason to expect S1 to be cheap, not a prediction that S1 will be null.

**S2 — Leave-one-out on the retained set: Gemini + DeepSeek (Claude omitted).** The registered retained set with Claude omitted, GPT-5.5 remaining excluded per the registered rule.

> **S2 returns INCONCLUSIVE by construction, and we say so in advance.** S2 retains two models. The registered floor is hardcoded at `>= 3` (§3.4), so it fails, and `p1_decision_tier` becomes `INCONCLUSIVE_MODEL_RETENTION_FLOOR_FAILED` **regardless of the data**. P3a and the cross-model gate become unpassable, since both require three passing models out of two. This is the registered rule working correctly, not a defect, and **we will not override the floor to rescue S2**. It does mean S2's verdict token carries no information. S2 is therefore reported as **estimates only**: per-model persona contrasts and their intervals, with no verdict. **Its verdict token is excluded from the disagreement trigger in §4.3.** Its two-model basis is stated here so that its low precision is not mistaken for a null. No S2 result will be interpreted as supporting or refuting MVC.

**S3 — Retain GPT-5.5 and omit Claude.** GPT-5.5 (gate verdict indeterminate) plus Gemini and DeepSeek. This is the informative counterpart to S2: it asks the same question without reducing to two models, and it is the primary sensitivity analysis. S3 is secondary and non-confirmatory; the registered floor governs the confirmatory verdict and is unaffected by it.

**S4 — Stability diagnostics for all four models.** Report λ with its bootstrap interval, the parametric-bootstrap false-exclusion rate under perfect stability, the observed r with its Fisher-z interval (noting the clustering caveat in §3.3), the run-effect and interaction statistics, and the drift on both the probability and log-odds scales. A reporting commitment, not an inferential test.

### 4.3 The leave-one-out selection rule, fixed in advance

S2 and S3 both single out Claude, and we will not pretend the rule that selects it was written before the diagnostics were computed. It was not. **This rule is pre-specified relative to the completed canonical verdict and to the sensitivity analyses, which is what matters and which have not been run; it is not pre-specified relative to the decomposition, which had already been computed when we wrote it.** We state it, with its α, so that a reader can see the selection rule rather than infer it from the outcome, and can see exactly what a different α would have added.

**Leave-one-out is pre-specified for any retained model whose post-hoc decomposition detects a shift at α = .05 on either component.** Applying it:

| Model | Run effect | Interaction | Triggers LOO? |
|---|---|---|---|
| Claude Opus 4.7 | z = −3.480, p < .001 | Q = 14.61, p = .0018 | **Yes** |
| Gemini 3.1 Pro | z = −0.752, p = .399 | Q = 11.71, p = .182 | No |
| DeepSeek-V4-Flash | z = +1.209, p = .067 | Q = 2.56, p = .356 | No |

The rule is applied by code, not by assertion: `run_sensitivity.R` re-derives the triggered set from the deposited `decomposition_real_data.csv` at run time and halts if it no longer selects Claude alone.

We record the near-miss explicitly: **DeepSeek's run effect is the largest signed shift of any model not at ceiling (OR = 2.22), and it does not reach α (p = .067).** Under the rule above it does not trigger a leave-one-out, and we do not run one. A reader who thinks the rule should have been α = .10 can see exactly what that would have added: a second leave-one-out, on DeepSeek. We note for completeness that DeepSeek's λ interval is wide ([0.050, 0.888]), though its point estimate (0.820) is far above GPT-5.5's (0.293) and its false-exclusion rate (22.5%) is not comparable to GPT-5.5's (83.9%); we do not claim the gate is as uninformative for DeepSeek as it is for GPT-5.5.

### 4.4 The disagreement trigger, defined in advance

For S1 and S3, **"disagreement with the registered result" is defined as: any element of the registered verdict tuple differs from its value in the canonical run.** The tuple is:

`p1_decision_tier`, `p2_ambiguity_pass`, `p2_domain_pass`, `p3a_confirmatory_pass`, the P4 verdict (the registered SUPPORTED / INTERMEDIATE / FAILURE ladder of §5.5, recorded **before** the Stage-4 modifier is applied, with the modifier reported separately), the §6.2 identification-table row, and the §6.3 verdict token.

We define disagreement on the **whole tuple** rather than on the §6.3 token alone, because the §6.3 token is a function of P4, P2, the semantic null and safety refusals only. A sensitivity run could flip **P1**, the gateway hypothesis and the F1 falsifier, or flip **P3a**, and register no change in the §6.3 token at all. Defining the trigger on that token alone would have left a hole large enough to drive the study's main hypothesis through.

**P3b is deliberately not in the tuple.** The registration treats P3b as descriptive narrative characterisation rather than a confirmatory verdict (F3a explicitly preserves it as "registered descriptive characterization" even when P3a fails), and it produces no verdict token. Its per-model output is reported for every sensitivity set alongside the tuple, but a change in it does not fire the trigger. We say so here so that "any element of the tuple" is a complete claim rather than a partial one.

**The full tuple is reported for every sensitivity analysis, whether or not any element differs.** Where any element differs, the difference is reported in the main text as a robustness sensitivity and described as unresolved. S2's tuple is reported but excluded from the trigger, for the reason given in §4.2. S1 to S4 remain secondary and are not elevated to co-primary status.

---

## §5 — Reporting discipline

1. The registered confirmatory result (GPT-5.5 excluded, three models retained) is the primary result and is reported as such.
2. S1 to S4 are reported in supplementary materials. Where any element of the verdict tuple differs from the registered one, that difference is additionally reported in the main text as a robustness sensitivity, without elevating any sensitivity analysis to confirmatory status.
3. No sensitivity analysis will be described as confirming or disconfirming MVC.
4. The stability gate's operating characteristics will be disclosed in the empirical paper's limitations section, citing the companion methods work rather than re-deriving the argument.
5. If the registered analysis and every sensitivity analysis agree, that agreement will be reported plainly and no further claim will be made from it.
6. **Design lesson.** The empirical paper will state that a stability gate defined on the study's own confirmatory outcome variable requires the analyst to view part of that outcome before the confirmatory analysis is constructed, and that a future registration should either gate on held-out cells or pre-register the gate's operating characteristics alongside its threshold. We record this as a limitation of the design, not as a defence of it.
7. **Release ordering.** The companion methods work reports that the decomposition finds no evidence of drift in the model the registered gate excluded, and evidence of a shift in a model the gate retained. (It does not "reverse both verdicts": one verdict is contradicted, and the other is shown to be indeterminate, which is not the same thing. §3.2 is the governing statement and this item does not extend it.) We will not publish that finding ahead of the empirical paper in a way that presents the registered gate as unsound before the registered result can be read alongside it. Both authors agree that the empirical paper's limitations section and the methods work must be readable together.

---

## §6 — Scope statement on future amendments

This amendment specifies the complete sensitivity plan arising from the stability-gate diagnostics. No further sensitivity analyses on this issue are anticipated. Any further addition would require a separate OSF amendment under the same disclosure discipline: explicit timing, explicit motivation, explicit confirmation that the registered confirmatory architecture is unchanged, hash-locked implementation code, and anticipated reviewer queries with registered responses.

This amendment does not modify the Amendment 1 secondary analysis plan (filed 2026-05-27), which stands unchanged, and it does not affect the §7.4 patch authority.

### 6.1 Interaction with Amendment 1, disclosed

We found this while auditing our own filings for the problem described in §3.4, and it is the same species of problem: a model-set assumption made before the gate fired.

**Amendment 1 was written on the assumption of four models, with GPT-5.5 as the reference category.** Its §4.3 specifies "model (3 contrasts vs **GPT-5.5 as reference**)" and "3 × 6 = 18 interaction parameters", and it does not mention the stability gate anywhere. It was filed on 2026-05-27, a month before the gate was evaluated on 2026-06-28.

The registered gate excludes GPT-5.5 from **confirmatory P1 to P4 only**. That is what Registration §3.3 says and what the registered code does: the decision token it writes is `exclude_confirmatory_p1_p4_report_supplementary`, which on its face preserves the excluded model in supplementary and secondary reporting. **The secondary analyses of Amendment 1 therefore proceed on the full four-model panel, with GPT-5.5 as the reference level, exactly as filed.** This is the registered behaviour and we are not changing it.

We nevertheless disclose the resulting asymmetry plainly, because it is strange on its face and a reader who met it unannounced would be right to be suspicious: **GPT-5.5 is excluded from the confirmatory analysis and is simultaneously the reference category against which every model contrast in the secondary analysis is estimated.** Every secondary between-model contrast is therefore expressed relative to the one model the confirmatory analysis does not contain.

We commit to three things. The secondary analyses will state this in their own reporting rather than leaving it to be inferred from the parameterisation. The per-model secondary summaries will report GPT-5.5's own posterior explicitly, flagged as a model the confirmatory gate excluded. And we will not re-level the model factor to a retained model after seeing the results: the reference level is as filed in Amendment 1, and changing it now, with the gate's outcome known, would be a post-hoc alteration of a filed plan.

---

## §7 — Anticipated reviewer queries, with registered responses

**Q. You discovered your registered gate was flawed and then wrote new analyses. Is this not post hoc?**
The diagnostics were computed on stability re-run data that was already collected, and computing them is what §3.3 instructs. The 27 June interrupted run did mechanically emit partial P1 to P3 files, and §2.2 states this rather than hiding it. Those files have not been substantively reviewed, interpreted, cited as results, or used for confirmatory decision-making. Entry 017's hash-locked manifest of `results/` lets you verify both what exists and what does not: the stability files, retention-floor file, and partial P1 to P3 files exist; P4 output, a P4 checkpoint, `hypothesis_verdict_summary.csv`, and `competing_account_adjudication.csv` do not. The sensitivity analyses are specified here, in advance, and their implementation is hash-locked, precisely so that they cannot be selected or tuned after seeing the completed outcome. The registered exclusion is unchanged.

**Q. You have seen persona-resolved outcome rates for 10% of your confirmatory design. Have you not already peeked?**
We have, and §2.3 sets out exactly what we have seen. Evaluating the registered gate is impossible without those cells, and the registration requires the gate to be evaluated before the confirmatory analysis is built. What we report from them is pooled over personas, reported as a dispersion or variance share, or is a single extreme-cell magnitude given without persona attribution; §2.3 states that exception rather than making a cleaner claim that the filesystem would falsify. The interrupted run mechanically emitted partial P1 to P3 files, but those files have not been substantively reviewed, interpreted, cited as results, or used for confirmatory decision-making. We regard the underlying issue as a design flaw worth naming rather than explaining away, and §5, item 6, names it.

**Q. Why not simply re-include GPT-5.5, since its exclusion rests on no evidence?**
Because the registered rule is the registered rule. We preregistered a criterion, it fired, and we honour it. Overriding a registered exclusion because we later dislike its statistical properties is precisely the researcher degree of freedom that preregistration exists to prevent. Instead we honour the rule, disclose that its verdict was uninformative, and report the alternative as a pre-specified sensitivity analysis.

**Q. Why is Claude not excluded, given the evidence of a shift?**
For the same reason. The registered rule retained Claude. We do not have licence to exclude a model that a registered gate passed, on the basis of a diagnostic we developed afterwards. We disclose the evidence and pre-specify S2 and S3 so that the consequence of it is visible.

**Q. You say P3a is now effectively unanimity. Why not rescale the threshold?**
Because there is nothing to rescale to. The registered criterion is 3 of 4, which is 75%, and 75% of three models is 2.25, which rounds up to three. The proportion-preserving rescaling gives 3-of-3, the same as the literal count. The only rule that would soften P3a is 2-of-3, which is 67%, and adopting it would mean lowering a registered confirmatory threshold after we knew which model the gate had removed, in the direction that makes our own hypothesis easier to support. That is not a repair; it is the thing preregistration prohibits. We disclose the consequence (§3.4), run P3a exactly as registered, and let S1 show what the registered four-model form would have produced.

**Q. Your sensitivity script patches the registered analysis code. Is that not a modification of the registration?**
It is a modification of the *script*, and we say so in §4.1 without euphemism. It is not a modification of the *registration*: the two patched lines are the model set and the output path, neither of which is a scientific parameter, and the script refuses to run if any third line changes. The registered pipeline offers no other way to run itself on a different model set, because it derives that set endogenously. The canonical confirmatory result is produced by the **unpatched** script, and the patched script cannot write to the canonical output directory. The unified diff is deposited so that the "exactly two lines" claim can be checked rather than believed.

**Q. Does this amendment change the study's conclusions?**
It changes no registered specification, and no complete canonical P1 to P4 verdict output has been generated. It does change what a reader will be able to see about how robust the registered conclusion is, and it commits us in advance to reporting that, including in the main text where the verdict tuple moves.

---

## §8 — Hash-locked supporting files

The following files are hash-locked at filing time. Their SHA-256 digests are recorded here and in Deviation Log Entry 017, so that any reader can verify that the diagnostics in §3.2 were computed from the data and code stated, and that neither has changed since filing.

| File | Bytes |
|---|---|
| `OSF_upload/05_Statistical_Analysis.R` (canonical, **unmodified**) | 406,806 |
| `paper3/stability_gate_diagnostics.py` | 7,100 |
| `paper3/drift_decomposition.py` | 9,745 |
| `paper3/decomposition_oc.py` | 5,163 |
| `paper3/lambda_ci_and_conventions.py` | 9,170 |
| `paper3/scenario_variance.py` | 5,608 |
| `analysis_sensitivity/run_sensitivity.R` | 21,607 |
| `paper3/results/table1_four_models.csv` | 1,020 |
| `paper3/results/decomposition_real_data.csv` | 385 |
| `paper3/results/lambda_intervals.csv` | 450 |
| `paper3/results/gate_convention_sensitivity.csv` | 385 |
| `paper3/results/scenario_clustering.csv` | 206 |
| `paper3/results/claude_drift_by_scenario.csv` | 156 |
| `MVC_stability_verification_readonly_2026-06-28/results/stability_check_results.csv` | 3,757 |
| `MVC_stability_verification_readonly_2026-06-28/results/stability_model_exclusion_decisions.csv` | 409 |

```
05_Statistical_Analysis.R
cce3a319ce943f6c2815d2750337dd71f96a9775077b01f616a479994cd6ac4b

stability_gate_diagnostics.py
b8647c955ced47490bab2761994035734a2c491c00c961c154bc1424ff8c1895

drift_decomposition.py
d4301af2830cb20d41faa6c7fdfa68b6147b3cbada03abdfa950358d08240180

decomposition_oc.py
94730dcd583e5908203990a16abe8a85ba9d97c20683194df53469667ca3fe8d

lambda_ci_and_conventions.py
f92e9aa5b1b0530ddae0a2ef486c222c68173aeb2a3d707f2963a5c4b651d006

scenario_variance.py
ea579537056b0412997208eeeaedf70b694cf0845dfa69fb681c829eb1939981

run_sensitivity.R
8545cd41d97ace4207e6bfe0e9d90f67a2042b21ead18ee4c66e6cd1b8ded626

results/table1_four_models.csv
1ad307a838f2642fba27e8818b3923503e8a9f91e899f0acedb17a0b1be1a1c1

results/decomposition_real_data.csv
40bfd437b24563e1a689774c31e8ffcf80206082447c9a0c086282e2d1b9d88b

results/lambda_intervals.csv
77e815db4053fe1d2036360b57a06d34dee6a44b575191a3f5896737bb5567ee

results/gate_convention_sensitivity.csv
e299244e2d54df7f48191d751b20512c292a09d13a8966d918ee663a725eaf31

results/scenario_clustering.csv
b43482fb6c44280477dba663ddc9f45a3573a707c73da369adc1e784349bff20

results/claude_drift_by_scenario.csv
6224d9d4673f89427240668a3f344eece98c9436b22985b48556ba375c6029de

stability_check_results.csv
614ac71f7d61577e270748eaa3220921697a40451b13754257b74979aaf72347

stability_model_exclusion_decisions.csv
c55bc906484df534bf79f4db86aec5530b30b38b5c605e2105c44e1ce2f990e9
```

**The canonical analysis script is unmodified, and this is checkable.** Its digest above, `cce3a319…`, is **byte-for-byte the digest recorded in the registration's own Appendix D**. A reader verifying the §4.1 two-line patch claim can therefore diff the patched copy against a script whose integrity is established by the registration itself, not by this amendment.

**Provenance of every number in this amendment.** Every figure quoted anywhere in this document is regenerated by one of the deposited scripts above, all run from seed 20260101 against `stability_check_results.csv`:

| Numbers | Produced by | Deposited in |
|---|---|---|
| λ point estimates, false-exclusion rates, r with Fisher-z intervals, between-cell SDs, drift on all three scales, null-r means and percentiles | `stability_gate_diagnostics.py` | `results/table1_four_models.csv` |
| λ bootstrap intervals; the three degenerate-draw conventions (83.9%, 81.0%, 68.9%) and the 15.0% undefined-draw share | `lambda_ci_and_conventions.py` | `results/lambda_intervals.csv`, `results/gate_convention_sensitivity.csv` |
| Run-effect z, interaction Q, their bootstrap p-values, and the λ floor | `drift_decomposition.py` | `results/decomposition_real_data.csv` |
| Scenario share of between-cell variance (82.4% Claude, 5.9% GPT-5.5); Claude's drift by scenario (−0.250, −0.007, largest −0.55) | `scenario_variance.py` | `results/scenario_clustering.csv`, `results/claude_drift_by_scenario.csv` |
| Operating characteristics of the decomposition across the simulation grid | `decomposition_oc.py` | reported in the companion methods work |

The Fisher-information figures in §4.2 (0.0141, 0.2492, 5.7%, 4.2×) are arithmetic on the main rates in `table1_four_models.csv` and are shown in full in §4.2 so that they can be checked by hand. **No number in this amendment is reported without deposited code or a shown derivation that regenerates it.**

This amendment document is itself hash-locked in Deviation Log Entry 017 at filing time; its digest cannot appear in its own body.

---

## §9 — Submission and timestamp

**Filed/revised:** 2026-07-14 (Europe/Malta; OSF platform display may show 2026-07-13 depending account/server time zone)
**Filed after:** the 27 June 2026 interrupted invocation of `05_Statistical_Analysis.R` described in §2.2, which emitted stability files, the retention-floor gate file, and partial P1 to P3 files before SIGINT during P4 sampling.
**Filed before:** any complete canonical P1 to P4 verdict output, P4 output, P4 checkpoint, `hypothesis_verdict_summary.csv`, `competing_account_adjudication.csv`, or Amendment 2 sensitivity analysis. Deviation Log Entry 017 carries a hash-locked manifest of `results/` by which this can be verified.
**Registration:** 6m3sk (embargo 2027-05-15, unchanged)
**Filed under:** Registration §7.4, "Major deviations" (model exclusion due to stability check failure)
**Deviation Log cross-reference:** Entry 017, published simultaneously
**Authors:** Emile Boullineau (PI), José Daniel Muñoz Arciniegas. Both authors attest jointly to the timing statement in §2.

---

*End of amendment.*
