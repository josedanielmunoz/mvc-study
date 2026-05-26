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

## Entry 002 — 2026-05-25 — §7.4 functional execution correction: Anthropic `deprecated` wording in provider-constrained decoding matcher

**Git commit:** This entry is recorded in the Git commit containing this text. The immediately preceding metadata-staging commit was `c222273df277d352f31ff637b0a6991adb86a953`; the final public commit SHA is verified from `git log` / GitHub history.
**Entry timestamp (UTC):** `2026-05-25T01:26:55Z`
**Type:** §7.4 functional execution correction
**Affected files:** `04_Data_Collection_Script.py`
**Trigger:** C.1.1 ambiguity pre-test re-run (under Entry 001's patched script) aborted at call 74/1200 due to repeated Anthropic `BadRequestError: 400 — temperature is deprecated for this model`. The `_call_anthropic` try/except wrapper installed in Entry 001 was present and active, but the `_is_provider_constrained_decoding_error` matcher did not classify Anthropic's `deprecated` wording as provider-constrained decoding evidence, so the fallback path did not engage. Post-abort review confirmed the matcher's boolean structure required `unsupported`/`not support` AND `default`/`only` to concur with the sampling-parameter mention; Anthropic's actual wording satisfied neither.
**PI written approval:** WhatsApp message from Emile Boullineau dated 2026-05-25, verbatim: *"Ok, you can fix bug without approval and just let me know after by email."* This is anticipatory approval for operational bug-fixes within the §7.4 magnitude boundary, with post-fix email notification (pending immediately after this commit).

### File hashes

| File | Pre-fix SHA-256 | Post-fix SHA-256 |
|---|---|---|
| `04_Data_Collection_Script.py` (pre-Patch-002, post-Patch-001) | `db6aaeba5369be93b9dbda0393f8adac5a550ceceec7f3b2d5bd04b0c1fef235` | `0f3d1d8b74a4f2447e0526bfde00482795da07f500675df5da7970013972d213` |
| `validate_pipeline_integrity.py` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` (unchanged; Appendix D anchor preserved) |

For full chain-of-correction traceability: the original Appendix D registered hash of `04_Data_Collection_Script.py` is `d614714016df41e01adb2908ff6ad38b1f3e64beddaeda332f5fb40c0712f49d`. Entry 001 (commit `4e9772d1c364fe2f0adc1db0d7f99cc3357a5d0b`) authorised the divergence from that hash; this Entry 002 authorises the further divergence to `0f3d1d8b74...`.

### Sub-change applied to `04_Data_Collection_Script.py`

**`_is_provider_constrained_decoding_error` (matcher logic correction).** The matcher's three-condition boolean structure was reworked to recognise the `deprecated` wording that Anthropic now returns when rejecting registered sampling parameters. The previous structure required all three of `(unsupported_phrase ∧ sampling_param ∧ default_or_only_phrase)` to fire. Anthropic's wording (`temperature is deprecated for this model`) satisfies `sampling_param` but neither `unsupported_phrase` nor `default_or_only_phrase`, leaving the fallback path unreachable for the most common Anthropic rejection observed in this study.

The corrected matcher:

- introduces `deprecated` as a separate signal (`"deprecated" in message`);
- expands `default_or_only_phrase` to additionally recognise `"this model"` (a phrase common to both OpenAI's `"is not supported with this model"` and Anthropic's `"is deprecated for this model"`);
- preserves the original conservative conjunction `(unsupported ∧ default_only)` as one valid evidence path;
- adds `deprecated` alone (in conjunction with `sampling_param`) as a second valid evidence path.

The final return clause becomes `sampling_param ∧ ((unsupported ∧ default_only) ∨ deprecated)`. This keeps the matcher narrowly scoped to errors that name a sampling parameter and provide explicit evidence of provider-constrained decoding, while admitting both the OpenAI-style and Anthropic-style wordings observed in the registered providers.

Pre-commit logic verification (4/4 PASS):

- OpenAI logprobs rejection (`Unsupported parameter: 'logprobs' is not supported with this model.`) → matcher returns `True` ✓
- Anthropic deprecated rejection (`temperature is deprecated for this model.`) → matcher returns `True` ✓
- Unrelated 400 (`Invalid request: missing required field 'messages'`) → matcher returns `False` ✓
- Auth error (`Invalid API key provided`) → matcher returns `False` ✓

### Magnitude assessment (per pre-reg §7.4 boundary)

This correction is confined to a single static method governing classification of API error strings. It does not alter:

- model selection, model version strings, or model configuration entries in `MODELS`;
- prompts, scenarios, personas, repetitions, or any input to the API calls;
- decoding parameters as registered in pre-reg §3.4 Table 5a (target temperature 0.7, top-p 1.0, max output tokens, seed handling) — the matcher merely determines when the registered provider-constrained-decoding fallback engages;
- exclusion criteria, significance thresholds, or any pre-registered prediction (P1, P2, P3a, P3b, P4) or failure condition.

The behavioural effect is: a class of provider rejection errors that previously caused the call to fail terminally (and be either retried fruitlessly under the existing retry chain or logged as a missing trial under MAR per §3.4) now correctly trigger the registered fallback path of stripping the rejected parameter and retrying with provider-default decoding. The fallback path itself is the registered provider-constrained-decoding mechanism from pre-reg §3.4; this correction widens the matcher's recognition of when to invoke that mechanism, not the mechanism itself.

The correction is well inside the < 1% magnitude boundary registered in pre-reg §7.4.

### Validation chain (registered authority cited)

- **Pre-reg §7.4** — Code execution and bug-fix clause. Functional execution corrections within the magnitude boundary do not constitute a deviation from the pre-registration. Public Git history is the authoritative diff record.
- **Pre-reg §3.4** — Provider-constrained decoding mechanism. This correction extends the matcher's signal recognition so that the registered fallback path engages on the actual wording observed in production from Anthropic.

### Evidence artefacts (operator-local, not in repo)

- Aborted re-run log (under Entry 001 patched script): `~/MVC_Study_operational/c11_pretest_live_run_rerun_20260524_190523.log`
- Anthropic `deprecated` error transcript (285 lines): `~/MVC_Study_operational/patches/c11_anthropic_deprecated_patch_002_2026-05-25/anthropic_deprecated_error_transcript.txt`
- Patch 002 diff (unified): `~/MVC_Study_operational/patches/c11_anthropic_deprecated_patch_002_2026-05-25/04_Data_Collection_Script.patch_002.diff`
- Pre-Patch-002 script backup: `~/MVC_Study_operational/patches/c11_anthropic_deprecated_patch_002_2026-05-25/04_Data_Collection_Script.py.pre_patch_002`

The textual diff for this entry is fully recoverable from the Git history of this repository via `git diff` between the previous commit (Entry 001, `4e9772d1c364fe2f0adc1db0d7f99cc3357a5d0b`) and this commit; the operator-local artefacts back up that record outside the repo.

### Partial data cleanup

The aborted re-run wrote 88 partial live records before manual interrupt: 60 lines in `data/pretest/gpt-5.5/2026-05-24/calls.jsonl` and 28 lines in `data/pretest/gemini-3.1-pro/2026-05-24/calls.jsonl`. These records were inventoried and removed prior to applying Patch 002. `data/pretest/` is clean at the time of this entry. No partial-data contamination remains in the registered output tree. The aborted re-run log is preserved in the operational evidence folder for audit.

### Post-patch state

- `04_Data_Collection_Script.py` chmod `444`; new SHA-256 recorded above.
- `validate_pipeline_integrity.py` unchanged; `REGISTERED_HASHES` continues to carry the original Appendix D value for `04_Data_Collection_Script.py` (`d614714016...`). The validator self-check against Appendix D in `00_OSF_Pre_Registration.md` returns OK.
- The validator therefore reports a hash mismatch for `04_Data_Collection_Script.py` with the exact wording: `FAIL: hash mismatch for 04_Data_Collection_Script.py: expected d614714016df41e01adb2908ff6ad38b1f3e64beddaeda332f5fb40c0712f49d, got 0f3d1d8b74a4f2447e0526bfde00482795da07f500675df5da7970013972d213`. This is the registered behaviour under pre-reg §7.4: the divergence between the Appendix D hash and the current script hash is the cumulative effect of Entry 001 and this Entry 002, both of which carry written PI approval. Per pre-reg §7.4: *"If a reviewer or auditor observes that a final published script hash differs from the pre-registered Appendix D hash, they can consult the Git log to verify that every change falls within this execution-fix boundary."* This entry, together with Entry 001, establishes that the divergence is the sum of two approved §7.4 corrections, not tampering.
- `data/pretest/` clean.
- Re-run of C.1.1 under the double-patched script is the immediate next operational step.
- Post-fix notification email to PI is pending immediately after this commit, as agreed in the WhatsApp approval message.

---

## Entry 003 — 2026-05-25 — §7.4 functional execution correction: reasoning-model token budgets and Gemini SDK finish_reason alignment

**Commit SHA:** Self-referential; see the Git commit containing this Entry 003.
**Entry timestamp (UTC):** `2026-05-25T20:22:04Z`
**Type:** §7.4 functional execution correction
**Affected files:** `04_Data_Collection_Script.py`
**Trigger:** C.1.1 second rerun (under the double-patched script from Entries 001 + 002) completed 1,200 / 1,200 cells in 2 h 08 min on 2026-05-24 → 2026-05-25, with no abort and no traceback, but post-run diagnostic revealed Stage 1 empty-response patterns of 300/300 (100%) for both `gpt-5.5` and `gemini-3.1-pro`. Root cause analysis identified two converging failure modes specific to reasoning-capable models under the script's registered configuration: (1) GPT-5.5 consumed the Stage 1 `max_tokens=10` budget entirely on internal reasoning before producing visible output, returning `finish_reason=length` on 300/300 Stage 1 records, and (2) Gemini 3.1 Pro likewise exhausted its output budget but additionally was being misclassified as a safety refusal because the script's existing `finish_reason_indicates_safety_block` helper had `"2"` hardcoded as a SAFETY marker, whereas under the current `google-generativeai` SDK the integer value 2 maps to the enum member `MAX_TOKENS` and SAFETY is value 3. Claude (`802/802` clean) and DeepSeek (`29/897` empty, all Stage 2) were unaffected. Full diagnostic was escalated to PI by formal email on 2026-05-25.
**PI written approval:** Email from Emile Boullineau dated 2026-05-25, in reply to the RA's diagnostic escalation email "C.1.1 second rerun: data validity blocker — methodological decision required". The approval email specifies four named fixes (Fix 1 finish_reason alignment, Fix 2 GPT-5.5 token-budget + reasoning-effort, Fix 3 Gemini token-budget + thoughts_token_count, Fix 4 metadata logging fields + per-run `run_metadata.json`) and authorises their consolidated application under §7.4 with magnitude statement explicitly framed as "Confined to API parameter handling and finish-reason canonicalisation. Does not alter model selection, prompts, registered analytic procedure, exclusion criteria, significance thresholds, or any pre-registered prediction. Within §7.4 boundary." The same email instructs the operator to send the diff and the post-fix hash to the PI for written sign-off before any live execution proceeds.

### File hashes

| File | Pre-fix SHA-256 | Post-fix SHA-256 |
|---|---|---|
| `04_Data_Collection_Script.py` (pre-Patch-003, post-Patch-002) | `0f3d1d8b74a4f2447e0526bfde00482795da07f500675df5da7970013972d213` | `82c25f1026242b5223084ae8461b79ff29d7e2e3cf966ad1bf08b8438bf8ddab` |
| `validate_pipeline_integrity.py` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` (unchanged; Appendix D anchor preserved per Entries 001 + 002) |

For full chain-of-correction traceability: the original Appendix D registered hash of `04_Data_Collection_Script.py` is `d614714016df41e01adb2908ff6ad38b1f3e64beddaeda332f5fb40c0712f49d`. Entry 001 (commit `4e9772d1c364fe2f0adc1db0d7f99cc3357a5d0b`) and Entry 002 (commit `c376d74e82d433791c2e41c4d897b00eb336476a`) authorised the prior divergences. This Entry 003 authorises the further divergence to `82c25f1026...` arising from the four named fixes below.

### Sub-changes applied to `04_Data_Collection_Script.py`

**Sub-change 1 — Gemini finish_reason reading aligned with current SDK enum (Fix 1).**

The previous implementation read Gemini's `candidate.finish_reason` as an integer (e.g. `2`) and the helper `finish_reason_indicates_safety_block` treated `"2"` as a SAFETY marker based on an earlier SDK mapping. Under the `google-generativeai` SDK currently active in the operational venv (`0.8.6`), the integer `2` corresponds to the enum member `MAX_TOKENS` and SAFETY is value `3`. The previous reading caused Gemini length-truncation responses to be misclassified as safety refusals.

The corrected implementation introduces a module-level helper `finish_reason_name(finish_reason)` that returns the SDK enum's `.name` attribute when present and falls back to the string representation otherwise, providing a stable string interface across providers. A second helper `canonical_finish_reason(finish_reason)` maps the raw string to one of four registered audit categories: `complete` (`stop`, `end_turn`, `STOP`), `length` (`length`, `max_tokens`, `MAX_TOKENS`), `safety` (`content_filter`, `SAFETY`, `BLOCKLIST`, `PROHIBITED_CONTENT`, `SPII`, `RECITATION`), and `other`. The helper `finish_reason_indicates_safety_block` now reads through `finish_reason_name(...)` and no longer contains the bare `"2"` marker; the SAFETY-block set is now strictly the semantic enum names. `_call_google` uses `finish_reason_name(...)` when extracting the finish reason, so the raw record reflects the SDK string (e.g. `"MAX_TOKENS"`) rather than the integer.

This sub-change aligns the script with pre-reg §2.7(d) (safety-blocked outputs treated as registered refusal-style outcome) under the current SDK enum mapping, without altering the registered handling of true safety blocks.

**Sub-change 2 — GPT-5.5-only reasoning-effort suppression and raised output-token budget (Fix 2).**

`_call_openai` now accepts the `stage` parameter and, only when `self.model_key == "gpt-5.5"`, sets `token_param = "max_completion_tokens"`, raises the request budget to `512` tokens for Stage 1 and `1024` tokens for Stage 3, and adds `reasoning_effort="minimal"` to the request kwargs. Other OpenAI-style branches (including `deepseek-v4-flash`, which is configured under the OpenAI provider with a custom `base_url`) are untouched. The change addresses the observed pattern in which GPT-5.5 consumed the registered Stage 1 `max_tokens=10` budget entirely on internal reasoning before emitting visible output, returning `finish_reason=length` on 300/300 Stage 1 records in the second rerun.

This sub-change is the registered provider-constrained decoding mechanism from pre-reg §3.4 extended to the reasoning-model class observed in production. It does not alter the registered binary verbalisation task in Stage 1 (the model is still asked for a Yes/No response); it raises the budget within which the model may produce that verbalisation.

**Sub-change 3 — Gemini raised output-token budget and reasoning-tokens metadata (Fix 3).**

`_call_google` now accepts the `stage` parameter and raises `max_output_tokens` to `2048` for Stage 1 and `8192` for Stage 3. The request additionally captures `response.usage_metadata.thoughts_token_count` via a defensive `getattr(usage_metadata, "thoughts_token_count", None)` so the field is recorded when present without raising on SDK versions where it is absent. No `safety_settings` are passed to the Gemini SDK; the provider's default safety configuration is preserved.

The change addresses the observed pattern in which Gemini 3.1 Pro consumed its Stage 1 output budget on internal reasoning and produced an empty visible response with `finish_reason=MAX_TOKENS` on the majority of Stage 1 records. Combined with sub-change 1, Gemini length-truncations will now be recorded as `finish_reason_canonical = length` rather than misclassified as safety refusals.

**Sub-change 4 — Per-call metadata fields and per-run `run_metadata.json` (Fix 4).**

Two new metadata fields are written for every API call across all four providers:

- `finish_reason_raw`: the provider SDK's native finish-reason value. For OpenAI and DeepSeek this is `choices[0].finish_reason`; for Anthropic, `stop_reason`; for Gemini, the result of `finish_reason_name(candidate.finish_reason)`.
- `finish_reason_canonical`: the canonical category from `canonical_finish_reason(...)` — one of `complete`, `length`, `safety`, `other`.

These fields are populated in `_call_openai`, `_call_anthropic`, and `_call_google` and are propagated through the existing `last_request_metadata` mechanism into `calls.jsonl`. The existing `response_finish_reason` field is preserved for backward compatibility with downstream consumers.

Additionally, a new module-level function `write_pretest_run_metadata(script_path)` is invoked in `main()` whenever `args.mode == "pretest"`. It writes a single immutable file `data/pretest/<YYYY-MM-DD>/run_metadata.json` containing the run start timestamp (UTC, ISO 8601), the current script SHA-256, and the output of `pip show openai anthropic google-generativeai deepseek` (capturing installed SDK versions). The file is opened with `open(..., "x")` and a prior `metadata_path.exists()` check, so it is idempotent and never overwrites a prior run's metadata.

### Operational note on SDK naming

Emile's approval email references the `google-genai` SDK by name. The script and operational venv currently use `google-generativeai 0.8.6`, which exposes the same `candidate.finish_reason.name` interface targeted by sub-change 1. No SDK migration was performed under this patch; the fix operates on the SDK currently installed. If a future operator migrates to `google-genai`, the `finish_reason_name(...)` helper continues to work because it reads the `.name` attribute generically.

### Magnitude assessment (per pre-reg §7.4 boundary)

All four sub-changes are confined to API parameter handling, finish-reason canonicalisation, and per-call metadata. None alter model selection, model version strings, prompts, scenarios, personas, repetitions, exclusion criteria, significance thresholds, ambiguity-binning thresholds, or any pre-registered prediction (P1, P2, P3a, P3b, P4) or failure condition. Logprobs handling is unchanged from Entries 001 + 002.

The behavioural effect is: reasoning-capable models that previously exhausted their Stage 1 output budget on internal reasoning before producing visible output now have sufficient budget to emit the registered binary verbalisation. Length-truncation outcomes that were previously misclassified as safety refusals (Gemini) are now recorded with their correct canonical category. The registered binary verbalisation task itself is unchanged — Stage 1 still asks for and parses a Yes/No response from `response_text`.

PI's own magnitude statement in the approval email is incorporated by reference: *"Confined to API parameter handling and finish-reason canonicalisation. Does not alter model selection, prompts, registered analytic procedure, exclusion criteria, significance thresholds, or any pre-registered prediction. Within §7.4 boundary."*

This correction is well inside the < 1% magnitude boundary registered in pre-reg §7.4.

### Validation chain (registered authority cited)

- **Pre-reg §7.4** — Code execution and bug-fix clause. Functional execution corrections within the magnitude boundary do not constitute a deviation from the pre-registration. Public Git history is the authoritative diff record.
- **Pre-reg §3.4** — Provider-constrained decoding mechanism. This correction extends the registered fallback behaviour to the reasoning-model token-budget interaction observed in production from GPT-5.5 and Gemini 3.1 Pro.
- **Pre-reg §2.7(d)** — Safety-blocked outputs treated as registered refusal-style outcome. The Gemini SDK alignment in sub-change 1 brings the script's finish_reason reading into line with the current SDK enum, preserving §2.7(d) handling for true safety blocks while preventing length-truncation outcomes from being misclassified as safety refusals.

### Pre-commit verification

The `canonical_finish_reason(...)` helper was unit-verified against fourteen representative finish-reason values spanning all four providers (OpenAI `stop`, `length`, `content_filter`; Anthropic `end_turn`, `max_tokens`; Gemini `STOP`, `MAX_TOKENS`, `SAFETY`, `BLOCKLIST`, `PROHIBITED_CONTENT`, `SPII`, `RECITATION`; plus `None` and an unknown string). All fourteen mapped to the expected canonical category. The script passed static syntax verification via `python -m py_compile` with exit status 0. The script permission was restored to `444 / -r--r--r--` after editing.

### Evidence artefacts (operator-local, not in repo)

- Pre-patch script backup: `~/MVC_Study_operational/patches/c11_patch_003_2026-05-25/04_Data_Collection_Script_PRE_PATCH_003.py`
- Pre-patch SHA-256 record: `~/MVC_Study_operational/patches/c11_patch_003_2026-05-25/pre_patch_sha256.txt`
- Patch 003 unified diff: `~/MVC_Study_operational/patches/c11_patch_003_2026-05-25/patch_003_script.diff`
- Post-patch SHA-256 record: `~/MVC_Study_operational/patches/c11_patch_003_2026-05-25/post_patch_sha256.txt`
- Static-check record: `~/MVC_Study_operational/patches/c11_patch_003_2026-05-25/static_check.txt`
- SDK versions record at the time of the patch: `~/MVC_Study_operational/patches/c11_patch_003_2026-05-25/sdk_versions.txt`
- Aborted second-rerun log (Entries 001 + 002 script, pre-Entry 003): `~/MVC_Study_operational/c11_pretest_live_run_rerun2_20260524_211814.log`
- Second-rerun raw per-provider response files (Gemini 290/300 empties, GPT-5.5 300/300 empties) preserved as audit-trail of the reclassification.

The textual diff for this entry is fully recoverable from the Git history of this repository via `git diff` between the previous commit (Entry 002, `c376d74e82d433791c2e41c4d897b00eb336476a`) and this commit; the operator-local artefacts back up that record outside the repo.

### Partial data and analysis pipeline state

`data/pretest/` was cleared of the contaminated dry-run artefacts prior to Entry 001. The second rerun's outputs (used as diagnostic evidence for this Entry 003) remain in their original location and will be cleared before the next live execution. No live execution has occurred since the Entry 002 commit; the second rerun's outputs are explicitly excluded from any registered analysis. `validated_trials.csv` was not generated; the registered validation harness has not been run on second-rerun data.

The A.3 validator continues to report the hash mismatch for `04_Data_Collection_Script.py` (now `expected d6147140... got 82c25f10...`). This is the registered behaviour under pre-reg §7.4, the cumulative effect of Entries 001 + 002 + 003. Per pre-reg §7.4: *"If a reviewer or auditor observes that a final published script hash differs from the pre-registered Appendix D hash, they can consult the Git log to verify that every change falls within this execution-fix boundary."* The validator self-check against Appendix D in `00_OSF_Pre_Registration.md` returns OK; the validator file itself remains at its registered anchor.

### Post-patch state and immediate next step

- `04_Data_Collection_Script.py` chmod `444`; new SHA-256 recorded above.
- `validate_pipeline_integrity.py` unchanged; Appendix D anchor preserved.
- No data collection, smoke test, dry run, or live run has been executed under this patch.
- `script_checksums.txt` and the operational working copy of `validate_pipeline_integrity.py` `REGISTERED_HASHES` have been updated to the new post-fix hash as part of this Entry's commit cycle.

The patch is now at the gate registered in the PI approval email: the diff and new hash must be sent to the PI for written sign-off before the four-provider smoke test or any subsequent live execution proceeds.

---

## Entry 004 — 2026-05-26 — §7.4 functional execution correction: GPT-5.5 reasoning_effort value alignment

**Commit SHA:** Self-referential; see the Git commit containing this Entry 004.
**Entry timestamp (UTC):** `2026-05-26T01:44:00Z`
**Type:** §7.4 functional execution correction
**Affected files:** `04_Data_Collection_Script.py`
**Trigger:** The four-provider smoke test authorised under Entry 003 (PI sign-off email dated 2026-05-25) was executed on 2026-05-26 to validate Patch 003 against the live provider APIs prior to the C.1.1 full rerun. Three of the four providers passed: Claude Opus 4.7, Gemini 3.1 Pro, and DeepSeek V4 Flash returned non-empty visible text with `finish_reason_canonical = complete`. Gemini's response in particular confirmed the Patch 003 finish_reason alignment (Stage 1 returned `STOP / complete`, no longer misread as safety). GPT-5.5 failed with an OpenAI 400 `BadRequestError`: the value `reasoning_effort="minimal"` set by Patch 003 is not accepted by the current OpenAI API for `gpt-5.5`. The API response specified the supported set: `none, low, medium, high, xhigh`. The value `minimal` had been written into Patch 003 per the PI approval email's wording at the time, but OpenAI's accepted set for this parameter no longer includes it on this model.
**PI approval reference:** WhatsApp message from Emile Boullineau dated 2026-05-25 granting anticipatory approval for operational bug-fixes within §7.4 magnitude boundary, with post-fix email notification. Notification email sent to PI on 2026-05-26 prior to applying this patch, advising the smoke test outcome and the one-literal correction. The post-fix diff and new hash are being sent in the follow-up email after this commit.

### File hashes

| File | Pre-fix SHA-256 | Post-fix SHA-256 |
|---|---|---|
| `04_Data_Collection_Script.py` (pre-Patch-004, post-Patch-003) | `82c25f1026242b5223084ae8461b79ff29d7e2e3cf966ad1bf08b8438bf8ddab` | `e09d00ee49762a2843579ca0db2a0a47a2c3ed30229973e21b66bfbef4639720` |
| `validate_pipeline_integrity.py` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` (unchanged; Appendix D anchor preserved per Entries 001–003) |

Cumulative chain-of-correction reference: the original Appendix D registered hash is `d614714016df41e01adb2908ff6ad38b1f3e64beddaeda332f5fb40c0712f49d`. Prior commits in the chain: Entry 001 `4e9772d1c364fe2f0adc1db0d7f99cc3357a5d0b`, Entry 002 `c376d74e82d433791c2e41c4d897b00eb336476a`, Entry 003 `998ecd7979a7a547fe13e5ed585b023fc4741031`. This Entry 004 authorises the further divergence to `e09d00ee49...`.

### Sub-change applied to `04_Data_Collection_Script.py`

**Single-line literal change in `_call_openai`.** The Patch 003 implementation set:

```python
if self.model_key == "gpt-5.5":
    kwargs["reasoning_effort"] = "minimal"
```

The corrected implementation sets:

```python
if self.model_key == "gpt-5.5":
    kwargs["reasoning_effort"] = "none"
```

The value `"none"` is the lowest setting in OpenAI's currently-accepted set for `reasoning_effort` on `gpt-5.5` (`none, low, medium, high, xhigh`). It satisfies the operational intent of Patch 003 sub-change 2 verbatim — minimise internal reasoning so the registered output budget is spent on the visible Yes/No verbalisation. No other change is made to the script.

### Magnitude assessment (per pre-reg §7.4 boundary)

This correction is a single string literal change in a parameter value, within an existing parameter setting that was itself authorised under Patch 003. It does not introduce new parameters, does not alter model selection, prompts, scenarios, personas, repetitions, exclusion criteria, significance thresholds, or any pre-registered prediction (P1–P4) or failure condition. The operational intent — suppress internal reasoning for GPT-5.5 so Stage 1 visible-output budget is preserved — is unchanged from Patch 003; the literal value is updated to match the current OpenAI accepted set.

Well inside the < 1% magnitude boundary registered in pre-reg §7.4.

### Validation chain (registered authority cited)

- **Pre-reg §7.4** — Code execution and bug-fix clause; "API formatting changes" is named explicitly as an example of a §7.4-eligible correction. The OpenAI accepted-values change for `reasoning_effort` is an API formatting change of exactly that kind.
- **Pre-reg §3.4** — Provider-constrained decoding mechanism; the reasoning-effort suppression for GPT-5.5 is the registered extension authorised in Entry 003 sub-change 2. This Entry only updates the literal value to match the provider's current accepted set.

### Pre-commit verification

- Static syntax check (`python -m py_compile`) on the patched script: exit status 0.
- File permission restored to `444 / -r--r--r--` after editing.
- `__pycache__` byproduct removed.
- `script_checksums.txt` updated with the new post-fix hash.
- Operational working copy of `validate_pipeline_integrity.py` (`~/MVC_Study_operational/validate_pipeline_integrity_working_copy.py`) updated with the new hash in `REGISTERED_HASHES`. Canonical validator at `~/MVC_Study/validate_pipeline_integrity.py` unchanged.

### Evidence artefacts (operator-local, not in repo)

- Pre-patch script backup: `~/MVC_Study_operational/patches/c11_patch_004_2026-05-26/04_Data_Collection_Script_PRE_PATCH_004.py`
- Patch 004 unified diff: `~/MVC_Study_operational/patches/c11_patch_004_2026-05-26/patch_004_script.diff`
- Smoke-test failure stdout log: `~/MVC_Study_operational/smoke_tests/c11_patch_003_smoke_test_stdout_20260526T012144Z.log`
- Smoke-test failure JSON result: `~/MVC_Study_operational/smoke_tests/c11_patch_003_smoke_test_results_20260526T012200Z.json`

The textual diff for this entry is fully recoverable from the Git history of this repository via `git diff` between the Entry 003 commit (`998ecd7979a7a547fe13e5ed585b023fc4741031`) and this commit; the operator-local artefacts back up that record outside the repo.

### Post-patch state and immediate next step

- `04_Data_Collection_Script.py` chmod `444`; new SHA-256 recorded above.
- `validate_pipeline_integrity.py` unchanged; Appendix D anchor preserved.
- No live execution has occurred under this patch. The smoke test will be re-run under Patch 004 as the immediate next operational step.

The A.3 validator continues to report the hash mismatch for `04_Data_Collection_Script.py` (now `expected d6147140... got e09d00ee49...`). This is the registered behaviour under pre-reg §7.4, the cumulative effect of Entries 001 + 002 + 003 + 004. Per pre-reg §7.4: *"If a reviewer or auditor observes that a final published script hash differs from the pre-registered Appendix D hash, they can consult the Git log to verify that every change falls within this execution-fix boundary."*

If the re-run smoke test passes on all four providers, the C.1.1 full rerun proceeds under PI sign-off from the 2026-05-25 email. If the smoke test fails on any provider, the operator halts and emails the PI before any further action.

---

## Entry 005 — 2026-05-26 — §7.4 functional execution correction: validation harness pretest-only guard clause

**Commit SHA:** Self-referential; see the Git commit containing this Entry 005.
**Entry timestamp (UTC):** `2026-05-26T06:24:16Z`
**Type:** §7.4 functional execution correction
**Affected files:** `analysis_phases/04_p3_narrative_and_reliability.R`
**Trigger:** The C.1.1 third rerun completed cleanly on 2026-05-26 under Patches 001–004 (script hash `e09d00ee49762a2843579ca0db2a0a47a2c3ed30229973e21b66bfbef4639720`), with 1,200 / 1,200 cells, 3,386 trial rows in `validated_trials.csv`, and zero retry duplicates. The registered validation harness was then invoked as `Rscript analysis_phases/run_phase.R --phase validation --fast --data-dir data/pretest/` and failed at the P3 narrative-and-reliability module with `Error in aggregate.data.frame(lhs, mf[-1L], FUN = FUN, ...) : no rows to aggregate`. Diagnostic review confirmed the failure was a pretest-only edge case internal to the harness itself, not a data integrity issue: `04_p3_narrative_and_reliability.R` subsets to `mode == "main"` and then immediately calls `aggregate(...)` without first checking whether the subset is empty, while the sibling modules `05_p4_dissociation.R` and `08_sdt_vci_supplementary.R` already contain the equivalent empty-subset guard clause and return a `mvc_append_status(... "FAIL", ...)` graciously. Under pretest-only input, P3's `class_data` was empty (0 main Stage 1 rows; 1,200 pretest Stage 1 rows present) and the unguarded `aggregate(...)` crashed. Raw outputs were preserved intact and no R script was edited prior to PI escalation analysis.
**PI approval reference:** WhatsApp message from Emile Boullineau dated 2026-05-25 granting anticipatory approval for operational bug-fixes within §7.4 magnitude boundary, with post-fix email notification. Post-fix notification will be consolidated with the Stage 1 Pre-Test Checkpoint email after the validation harness completes cleanly under this Entry 005.

### File hashes

| File | Pre-fix SHA-256 | Post-fix SHA-256 |
|---|---|---|
| `analysis_phases/04_p3_narrative_and_reliability.R` | `8d049484dfc9bb0ef0b6601c499ce82a6671cbb3903476dced3238f12ce0923e` (registered Appendix D anchor) | `b6263b14f095fd05861515bf16ef76812f19cafe448f4a33aaee3f15eba711d4` |
| `04_Data_Collection_Script.py` | `e09d00ee49762a2843579ca0db2a0a47a2c3ed30229973e21b66bfbef4639720` | `e09d00ee49762a2843579ca0db2a0a47a2c3ed30229973e21b66bfbef4639720` (unchanged; this Entry does not touch the data collection script) |
| `validate_pipeline_integrity.py` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` (unchanged; Appendix D anchor preserved per Entries 001–004) |

Prior commits in the §7.4 chain: Entry 001 `4e9772d1c364fe2f0adc1db0d7f99cc3357a5d0b`, Entry 002 `c376d74e82d433791c2e41c4d897b00eb336476a`, Entry 003 `998ecd7979a7a547fe13e5ed585b023fc4741031`, Entry 004 `897c7d4c7c15e8d35f55aa191575f7869d14cd2a`. This Entry 005 is the first §7.4 correction to affect a file in `analysis_phases/`; all prior corrections have been confined to `04_Data_Collection_Script.py`.

### Sub-change applied to `analysis_phases/04_p3_narrative_and_reliability.R`

**Single guard clause insertion mirroring the existing pattern in `05_p4_dissociation.R` and `08_sdt_vci_supplementary.R`.** The previous implementation subset trials to `mode == "main" & stage == 1L` and then called `aggregate(...)` directly:

```r
class_data <- subset(inputs$trials, mode == "main" & stage == 1L & grepl("^scenario_", scenario_id))

variance <- aggregate(
    stage1_yes ~ scenario_id + persona + model,
    data = class_data,
    FUN = function(x) c(n = length(x), rate = mean(x), variance = stats::var(as.numeric(x)))
)
```

The corrected implementation inserts a guard clause between the `subset(...)` and the `aggregate(...)`:

```r
class_data <- subset(inputs$trials, mode == "main" & stage == 1L & grepl("^scenario_", scenario_id))

if (nrow(class_data) == 0L) {
  return(mvc_append_status(
    inputs, "p3", "main_stage1_available", "FAIL",
    "No main Stage 1 rows available for P3 narrative/reliability analysis"
  ))
}

variance <- aggregate(
    stage1_yes ~ scenario_id + persona + model,
    data = class_data,
    FUN = function(x) c(n = length(x), rate = mean(x), variance = stats::var(as.numeric(x)))
)
```

The guard follows the identical pattern already used by the sibling modules: detect the empty-subset condition, return early via `mvc_append_status(...)` with a `"FAIL"` status and a descriptive message, and skip downstream computation that would otherwise crash. The status entry is the registered mechanism for the harness to record that a specific check was attempted but could not be performed against the supplied data, without halting execution of the wider harness.

### Magnitude assessment (per pre-reg §7.4 boundary)

This correction is a single guard clause whose behaviour is identical to clauses already present in two other modules of the same harness. It does not alter:

- model selection, prompts, scenarios, personas, repetitions, or any input to data collection;
- decoding parameters, sampling, or the call flow of `04_Data_Collection_Script.py`;
- exclusion criteria, significance thresholds, ambiguity binning, or any pre-registered prediction (P1, P2, P3a, P3b, P4) or failure condition;
- the analytic logic of P3 itself when run against main data, which is the registered use case — when `class_data` has rows, the guard is a no-op and `aggregate(...)` runs unchanged.

The behavioural effect is restricted to pretest-only inputs (and any other input that produces zero main Stage 1 rows): the harness now records a `mvc_append_status` FAIL entry for the P3 check and continues, rather than crashing with an unguarded `aggregate(...)` error. This brings P3 into parity with the empty-subset handling already registered in P4 and the SDT/VCI supplementary module.

This correction is well inside the < 1% magnitude boundary registered in pre-reg §7.4.

### Validation chain (registered authority cited)

- **Pre-reg §7.4** — Code execution and bug-fix clause. Functional execution corrections within the magnitude boundary do not constitute a deviation from the pre-registration. "Minor execution errors" is explicitly named in §7.4 as a §7.4-eligible class, and an inconsistency between sibling modules of the registered harness (two of three modules have the guard, one does not) is exactly that kind of minor execution error.
- **Consistency with registered design** — The guard pattern, status code, and `mvc_append_status` mechanism are already part of the registered harness in `05_p4_dissociation.R` and `08_sdt_vci_supplementary.R`. This Entry brings P3 into parity with the existing registered convention.

### Pre-commit verification

- R syntax check (`Rscript -e "parse(...)"`) on the patched file: `Syntax OK`.
- File permission restored to `444 / -r--r--r--` after editing.
- `script_checksums.txt` was not modified (the file's scope remains the four originally-registered Tier 1 critical files; `analysis_phases/` checksums are tracked through `validate_pipeline_integrity.py` `REGISTERED_HASHES` only).
- Operational working copy of `validate_pipeline_integrity.py` (`~/MVC_Study_operational/validate_pipeline_integrity_working_copy.py`) updated with the new hash in `REGISTERED_HASHES`. Canonical validator at `~/MVC_Study/validate_pipeline_integrity.py` unchanged.
- Canonical data collection script (`04_Data_Collection_Script.py`) unchanged at its Entry 004 post-fix hash.

### Evidence artefacts (operator-local, not in repo)

- Pre-patch file backup: `~/MVC_Study_operational/patches/c11_patch_005_harness_2026-05-26/04_p3_narrative_and_reliability_PRE_PATCH_005.R`
- Patch 005 unified diff: `~/MVC_Study_operational/patches/c11_patch_005_harness_2026-05-26/patch_005_harness.diff`
- Post-patch SHA-256 record: `~/MVC_Study_operational/patches/c11_patch_005_harness_2026-05-26/post_patch_sha256.txt`
- C.1.1 third rerun raw outputs (the inputs that surfaced the bug): `~/MVC_Study/data/pretest/` and the third rerun execution log under `~/MVC_Study_operational/`.

The textual diff for this Entry is fully recoverable from the Git history of this repository via `git diff` between the Entry 004 commit (`897c7d4c7c15e8d35f55aa191575f7869d14cd2a`) and this commit; the operator-local artefacts back up that record outside the repo.

### Post-patch state and immediate next step

- `analysis_phases/04_p3_narrative_and_reliability.R` chmod `444`; new SHA-256 recorded above.
- `04_Data_Collection_Script.py` unchanged at the Entry 004 post-fix hash.
- `validate_pipeline_integrity.py` canonical unchanged; Appendix D anchor preserved.
- No live data collection, smoke test, or analytic harness run has been executed under this patch yet.

The A.3 canonical validator now reports two hash mismatches: the long-running mismatch on `04_Data_Collection_Script.py` (per Entries 001–004) and a new mismatch on `analysis_phases/04_p3_narrative_and_reliability.R` (`expected 8d049484... got b6263b14...`, per this Entry 005). Both are the registered behaviour under pre-reg §7.4 when running the canonical validator; the operational working copy of `validate_pipeline_integrity.py` carries both new hashes in its `REGISTERED_HASHES` and returns OK on both files. Per pre-reg §7.4: *"If a reviewer or auditor observes that a final published script hash differs from the pre-registered Appendix D hash, they can consult the Git log to verify that every change falls within this execution-fix boundary."*

The immediate next operational step is to re-run the validation harness against the C.1.1 third rerun outputs, confirm it completes cleanly with the new guard in place, compute the pre-test metrics requested by the PI (per-provider Stage 1 Yes-rates, refusal-rate breakdown by `finish_reason_canonical`, ambiguity-band check across the 10 scenarios × 4 models grid), and send the consolidated Stage 1 Pre-Test Checkpoint email to the PI with Patch 005 notification included.

---
