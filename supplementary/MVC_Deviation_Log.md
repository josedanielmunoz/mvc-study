# MVC Deviation Log

> **Note on placeholder state at registration.** Empty / placeholder entries at registration time are expected by design. The log accumulates real entries only when registered deviations or §7.4 execution-fixes occur post-registration; the registration-time state is therefore a scaffold with explanatory headings and an empty entry table.

**Pre-registration:** Does AI Detect Moral Violations or Construct Them? — Persona-Driven Classification Bias in Large Language Models (OSF: 00_OSF_Pre_Registration.pdf). Tests the Motivated Violation Construction (MVC) framework (Boullineau, 2026, DOI 10.5281/zenodo.19423437).
**Status at registration:** *empty — no deviations recorded.*
**Maintainer:** Research Associate (José Daniel Muñoz Arciniegas), under PI direction.
**Authority:** Pre-registration §7.4 (Deviation Log).
**Scaffold version:** v1.0 — May 2026 (empty at registration; append-only deviation entries to be logged in execution order during data collection).

---

## Purpose

This file is the canonical, append-only registry of every deviation from the pre-registered protocol. Every entry made during the study lifecycle (pre-test → main collection → semantic-null run → robustness/stability checks → narrative coding → analysis) must be added here. Deviations are reported in the final manuscript under a dedicated "Deviations from Pre-Registration" section, citing this log.

## What gets logged here

Per pre-reg §7.4, log:

- API timeouts, rate-limit retries, individual cell re-runs
- Data loss affecting fewer than 5% of total trials within any single model (minor)
- Semantic-null reserve-bank substitutions (the swap and its rationale, per §2.3)
- Model version-string changes detected mid-collection (§3.3)
- Behavioural-drift triggers exceeding 2 SD from the running mean (§3.3)
- Anchor-trial deviations exceeding 1.5 SD from the Day-1 baseline (§3.3)
- Daily-anchor pause events
- Stan retry events (registered automatic retry with `adapt_delta=0.999`, `max_treedepth=18`; per §7.4 this is *not* a deviation, but the retry event itself is logged here with before/after diagnostic counts for transparency)
- Coding-prompt revision cycles (sanity-check failures, §5.4.5)
- Calibration-failure re-attempts and replacements (PI/RA or Auditor; §5.4.2 / §5.4.8)
- Attention-check failures (§5.4.3)
- Any accidental mid-stream code-derived feedback during Phase 1 (registered absence: §5.4.6 — no midpoint κ check, no midpoint drift check, no mid-stream reliability statistic is part of the design).
- Manual coding portal fallback to spreadsheet (§7.4 manual coding contingency)
- Functional code corrections that fall under the bug-fix clause (§7.4); each entry must record the magnitude (≤ 1% absolute change on any reported posterior, p-value, point estimate, or credible/confidence-interval bound) and the diff reference (Git commit hash)
- Auditor withdrawal / replacement events (§5.4.8)

Per pre-reg §7.4 **major** deviations require a formal OSF amendment **before** analysis proceeds; major deviations include:

- Excluding a model (other than under the registered stability-check criterion §3.3)
- Stability-check-driven model exclusion
- Changing persona definitions
- Altering the ambiguity threshold
- Data loss exceeding 5% of total trials within any single model
- Any change to pre-registered predictions, failure conditions, or primary statistical specifications

Each major deviation logged here must reference the corresponding OSF amendment ID and link.

## Entry format

```
### YYYY-MM-DD HH:MM UTC — [MINOR | MAJOR | NOT-A-DEVIATION (§7.4 bug-fix clause)]

**Entry ID (required, format `DEV-YYYY-NNN` or `DEV-YYYY-<TAG>`):** [Unique identifier — mandatory. Consumed by `05a_Resume_Statistical_Analysis.R --accept-deviation-log-entry=<entry_id>` for certified post-fix resume runs (pre-reg §7.5).]

**Commit SHA (this entry):** [Git commit SHA for the commit that records THIS entry — added before the entry is signed off]

**Category:** [API outage / version drift / Stan retry / coding revision / calibration / attention check / portal fallback / functional bug fix / other]

**Affected scope:** [models / scenarios / personas / sub-cells / trials / coders / dimensions]

**What happened:**
[Plain-language description.]

**Justification:**
[Why this deviation was necessary; reference pre-reg section.]

**Impact assessment:**
[Effect on the affected analysis or trial subset; how the affected data are handled downstream; whether the deviation crosses the 1% magnitude boundary in §7.4.]

**Action taken:**
[Concrete steps: re-run, exclude, retain with caveat, file OSF amendment ID, etc.]

**Audit trail anchors:**
[Trial IDs, checkpoint paths, Git commit hash, OSF amendment URL, etc.]

**Post-fix SHA-256 (registered §7.4 bug-fix only):**
- File: `<filename>` (e.g., `05_Statistical_Analysis.R`)
- Post-fix SHA-256: `<64-hex>`
- Pre-fix SHA-256 (for the record): `<64-hex>`
- Magnitude check (before/after_summary.csv path): `<path>`

**Logged by:** [Initials]
```

## Entries

*No entries at registration. New entries are appended below in reverse-chronological order (newest first) once the study lifecycle begins.*

### Worked example (illustrative — not a real deviation)

````
### 2026-MM-DD HH:MM UTC — NOT-A-DEVIATION (§7.4 bug-fix clause)

**Commit SHA (this entry):** (EXAMPLE)

**Category:** functional bug fix

**Affected scope:** `05_Statistical_Analysis.R` Phase P2 specification block

**What happened:**
A functional bug was identified in `05_Statistical_Analysis.R` (illustrative — example only). Fix applied under the §7.4 bug-fix clause.

**Justification:**
Bug-fix clause (§7.4): functional correction that does not alter pre-registered predictions, failure conditions, or primary statistical specifications. Magnitude check confirms ≤ 1% absolute change on all reported quantities.

**Impact assessment:**
See `before/after_summary.csv` (path under "Audit trail anchors"). All reported posteriors, p-values, point estimates, and CI bounds change by ≤ 1% absolute.

**Action taken:**
Bug fix committed; resumed analysis from `after_p1` using the certified-resume path:

```
Rscript 05_Statistical_Analysis.R \
  --resume-from after_p1 \
  --checkpoint-dir results/checkpoints_certified_DEV-2026-EXAMPLE-001 \
  --accept-deviation-log-entry=DEV-2026-EXAMPLE-001
```

**Audit trail anchors:**
Trial IDs: N/A. Checkpoint path: `results/checkpoints_certified_DEV-2026-EXAMPLE-001/`. Git commit hash: (EXAMPLE). OSF amendment URL: N/A (minor — bug-fix clause, no amendment required).

**Post-fix SHA-256 (registered §7.4 bug-fix only):**
- File: `05_Statistical_Analysis.R`
- Post-fix SHA-256: `(EXAMPLE)`
- Pre-fix SHA-256 (for the record): `(EXAMPLE)`
- Magnitude check (before/after_summary.csv path): `results/diagnostics/before_after_summary_DEV-2026-EXAMPLE-001.csv`

**Entry ID:** DEV-2026-EXAMPLE-001
**Logged by:** (EXAMPLE)
````

---

## Milestone SHA-256 Deposit Schedule (registered, pre-reg §7.4)

A running SHA-256 of this `MVC_Deviation_Log.md` is computed and OSF-deposited at four registered milestones:

| Milestone | Trigger | Deposited SHA-256 |
|---|---|---|
| Pre-test lock | Pre-test data collection complete and signed off | _(placeholder — recorded at trigger)_ |
| Main-collection start | First main-study API call made | _(placeholder)_ |
| Coding lock | Both PI and RA Submit Final | _(placeholder)_ |
| Analysis lock | Canonical Level-4 run start | _(placeholder)_ |

Each deposit carries an OSF timestamp. Reviewers can independently audit the log's state at each milestone against these deposited hashes.

---

*This log is co-registered with all other registration package materials. It is **not** Appendix-D-locked because it is an append-only operational record whose post-registration mutations are the entries themselves; instead its state IS recorded at the four registered milestones above (pre-test lock, main-collection start, coding lock, analysis lock), each carrying an OSF-deposited SHA-256 and timestamp so reviewers can independently audit the log's state at each milestone.*
---

## Entry 001 — 2026-05-25 — §7.4 functional execution correction: C.1.1 API error handling patch

**Git commit:** This entry is recorded in the Git commit containing this text. The immediately preceding metadata-staging commit was `0cd20e9dab6f9e98ade913f19844e7cefc804609`; the final public commit SHA is verified from `git log` / GitHub history.
**Entry timestamp (UTC):** `2026-05-24T23:35:58Z`
**Type:** §7.4 functional execution correction
**Affected files:** `04_Data_Collection_Script.py`
**Trigger:** C.1.1 ambiguity pre-test aborted at call 16/1200 due to `openai.BadRequestError: 400 Unsupported parameter: 'logprobs' is not supported with this model`. Post-abort review of the registered file identified two further latent error-handling gaps with the same root cause: API-level provider behaviour that the registered error-handling paths did not cover.
**PI written approval:** Email from Emile Boullineau dated 2026-05-25, in reply to RA's diagnostic email "C.1.1 ambiguity pre-test aborted at 1%, §7.4 functional execution corrections proposed". Verbatim approval clause: *"Approved. Please proceed with the consolidated §7.4 patch as you have described it. I agree with your magnitude assessment: all four sub-changes are limited to API error handling. None of them change model selection, prompts, decoding parameters, sampling, exclusion criteria, significance thresholds, or any registered prediction. The combined size sits well inside the §7.4 boundary."*

### File hashes

| File | Pre-fix SHA-256 | Post-fix SHA-256 |
|---|---|---|
| `04_Data_Collection_Script.py` | `d614714016df41e01adb2908ff6ad38b1f3e64beddaeda332f5fb40c0712f49d` | `db6aaeba5369be93b9dbda0393f8adac5a550ceceec7f3b2d5bd04b0c1fef235` |
| `validate_pipeline_integrity.py` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` (unchanged; reverted to Appendix D anchor) |

### Sub-changes applied to `04_Data_Collection_Script.py`

1. **`_is_provider_constrained_decoding_error` (matcher extension).** The `sampling_param` matcher previously filtered only on `temperature` and `top_p` strings. Extended to also match `logprobs`. This is the precondition for the existing OpenAI fallback path to engage on `logprobs`-rejection 400 responses.

2. **`_call_openai` (fallback block extension).** The existing fallback path (which strips `temperature` and `top_p` from `fallback_kwargs`) was extended to also strip `logprobs` and `top_logprobs`. The log message was updated from `"temperature/top_p"` to `"temperature/top_p/logprobs"` to reflect the actual scope of the fallback.

3. **`_call_anthropic` (try/except wrapper added).** The previous implementation called `self.client.messages.create(**call_args)` directly with no exception handling around the call. Wrapped the call in the same try/except pattern as `_call_openai`, detecting provider-constrained decoding errors and retrying once with `temperature` stripped from the kwargs. The metadata is now populated with the actual `applied_temperature` and `decoding_fallback_applied` / `decoding_fallback_reason` values reflecting the call result, rather than always-`TEMPERATURE` / always-`False`. Brings Anthropic to parity with the existing OpenAI handling.

4. **`_call_google` (SAFETY guard on `response.text`).** The previous implementation accessed `response.text` unconditionally after the `finish_reason` was captured. The Google Generative AI SDK raises `ValueError` when `.text` is accessed on a candidate whose `finish_reason` indicates a safety block (e.g. `finish_reason=2` / `FinishReason.SAFETY`). Added a guard that calls the existing `finish_reason_indicates_safety_block` helper (defined at module scope, no new logic introduced) and returns an empty-string response with the SAFETY `finish_reason` preserved in metadata. A defensive try/except around `response.text` handles edge cases where `.text` raises for reasons not matching the SAFETY markers. Empty-string responses with SAFETY `finish_reason` flow through the existing `classify_stage1_response` chain as `("refusal", "api_safety_finish_reason", False)`, which is the registered treatment per pre-reg §2.7(d).

### Magnitude assessment (per pre-reg §7.4 boundary)

All four sub-changes are confined to API error handling. None alter model structure, covariates, link functions, exclusion criteria, significance thresholds, sampling, prompts, scenarios, personas, repetitions, model selection, or any pre-registered prediction (P1, P2, P3a, P3b, P4) or failure condition.

- Logprobs are registered as supplementary in pre-reg §3.4 (*"Log-probability analyses are supplementary; all primary tests use verbalised binary outputs"*). A logprobs-absent record under fallback does not affect any P1–P4 confirmatory test.
- The temperature fallback path for Anthropic is the registered provider-constrained decoding mechanism from pre-reg §3.4 Table 5a being extended to a second provider where the same API-level need exists. The mechanism itself is registered; this patch widens its scope.
- The SAFETY guard on `_call_google` converts a hard crash into a registered refusal-style outcome, which pre-reg §2.7(d) anticipates as the correct treatment for safety-blocked outputs.

The four sub-changes together are well inside the < 1% magnitude boundary registered in pre-reg §7.4.

### Validation chain (registered authority cited)

- **Pre-reg §7.4** — Code execution and bug-fix clause; functional execution corrections within magnitude boundary do not constitute deviation from the pre-registration. Public Git history is the authoritative diff record.
- **Pre-reg §3.4** — Provider-constrained decoding mechanism; this patch extends the registered fallback path to additional API rejection cases.
- **Pre-reg §2.7(d)** — Safety-blocked outputs treated as registered refusal-style outcome with `api_safety_finish_reason`.

### Evidence artefacts (operator-local, not in repo)

- Aborted run log: `~/MVC_Study_operational/c11_pretest_live_run_20260524_155732.log`
- OpenAI BadRequestError transcript: `~/MVC_Study_operational/patches/c11_logprobs_patch_2026-05-25/openai_error_transcript.txt`
- Patch diff (unified): `~/MVC_Study_operational/patches/c11_logprobs_patch_2026-05-25/04_Data_Collection_Script.patch.diff`
- Pre-patch script backup: `~/MVC_Study_operational/patches/c11_logprobs_patch_2026-05-25/04_Data_Collection_Script.py.pre_patch`

The textual diff for this entry is fully recoverable from the Git history of this repository via `git diff` between the previous commit and this commit; the operator-local artefacts back up that record outside the repo.

### Post-patch state

- `04_Data_Collection_Script.py` chmod `444`; new SHA-256 recorded above.
- `validate_pipeline_integrity.py` reverted to its Appendix D anchor (hash unchanged from registration). The validator self-check (against Appendix D in `00_OSF_Pre_Registration.md`) returns OK.
- `validate_pipeline_integrity.py` `REGISTERED_HASHES[04_Data_Collection_Script.py]` continues to carry the Appendix D pre-fix value. The validator therefore reports a hash mismatch for `04_Data_Collection_Script.py` (expected `d614714016...`, got `db6aaeba53...`). This is the registered behaviour under pre-reg §7.4: *"If a reviewer or auditor observes that a final published script hash differs from the pre-registered Appendix D hash, they can consult the Git log to verify that every change falls within this execution-fix boundary."* The post-§7.4 validator RED for `04_Data_Collection_Script.py` is interpreted in conjunction with this Deviation Log entry; the entry establishes that the divergence is an approved §7.4 correction, not tampering.
- `data/pretest/` cleaned; no live data was written prior to the C.1.1 abort.
- Re-run of C.1.1 is the immediate next operational step.

---

