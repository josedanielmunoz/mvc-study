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

## Entry 006 — 2026-05-26 — §7.4 functional execution correction: validation harness pretest-only guard clause (refusal/missingness module)

**Commit SHA:** Self-referential; see the Git commit containing this Entry 006.
**Entry timestamp (UTC):** `2026-05-26T07:00:31Z`
**Type:** §7.4 functional execution correction
**Affected files:** `analysis_phases/06_refusal_missingness_sensitivity.R`
**Trigger:** Following Entry 005, the validation harness was re-run against the C.1.1 third rerun outputs and continued to fail, this time at the refusal/missingness sensitivity module with the same structural error class as P3 had presented (`Error in aggregate.data.frame(lhs, mf[-1L], FUN = FUN, ...) : no rows to aggregate`). A systematic read-only audit was then conducted across all `analysis_phases/*.R` modules to determine the full scope of the issue rather than continuing to patch reactively. The audit confirmed that of the six modules using `subset(mode == "main") + aggregate(...)`, five already carried the empty-subset guard clause (`02_p1_classification.R`, `03_p2_domain_generality.R`, `04_p3_narrative_and_reliability.R` post-Entry-005, `05_p4_dissociation.R`, `08_sdt_vci_supplementary.R`), and one — `06_refusal_missingness_sensitivity.R` — did not. This Entry 006 is the single remaining guard clause needed to bring the registered harness into full parity with its own pre-existing convention.
**PI approval reference:** Standing anticipatory approval from Emile Boullineau dated 2026-05-25 authorising operational bug-fixes within the §7.4 magnitude boundary with post-fix email notification. Post-fix notification will be consolidated with the Stage 1 Pre-Test Checkpoint email once the validation harness completes cleanly under Entries 005 + 006.

### File hashes

| File | Pre-fix SHA-256 | Post-fix SHA-256 |
|---|---|---|
| `analysis_phases/06_refusal_missingness_sensitivity.R` | `9b63bd828b5cc671e205442aa8e6c8e15901d4f9da715456178ac9ba0cafca21` (registered Appendix D anchor) | `d57e0cf3672baeebdc108e4922029e5936f29b8c22f5c8c16d0e2c6d4aae6ecf` |
| `analysis_phases/04_p3_narrative_and_reliability.R` | `b6263b14f095fd05861515bf16ef76812f19cafe448f4a33aaee3f15eba711d4` (post-Entry-005) | `b6263b14f095fd05861515bf16ef76812f19cafe448f4a33aaee3f15eba711d4` (unchanged) |
| `04_Data_Collection_Script.py` | `e09d00ee49762a2843579ca0db2a0a47a2c3ed30229973e21b66bfbef4639720` (post-Entry-004) | `e09d00ee49762a2843579ca0db2a0a47a2c3ed30229973e21b66bfbef4639720` (unchanged) |
| `validate_pipeline_integrity.py` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` (unchanged; Appendix D anchor preserved per Entries 001–005) |

Prior commits in the §7.4 chain: Entry 001 `4e9772d1c364fe2f0adc1db0d7f99cc3357a5d0b`, Entry 002 `c376d74e82d433791c2e41c4d897b00eb336476a`, Entry 003 `998ecd7979a7a547fe13e5ed585b023fc4741031`, Entry 004 `897c7d4c7c15e8d35f55aa191575f7869d14cd2a`, Entry 005 `e683aae6e34a27a8360be10d09c0907ebb8d1d5e`. This Entry 006 is the second §7.4 correction to affect a file in `analysis_phases/`, and is the direct sibling of Entry 005 applying the equivalent guard clause to the refusal/missingness module.

### Sub-change applied to `analysis_phases/06_refusal_missingness_sensitivity.R`

**Single guard clause insertion mirroring the existing pattern in `04_p3_narrative_and_reliability.R` (post-Entry-005), `05_p4_dissociation.R`, and `08_sdt_vci_supplementary.R`.** The previous implementation subset trials to `mode == "main"` and then proceeded directly to mutate the subset and call `aggregate(...)`:

```r
main <- subset(trials, mode == "main" & grepl("^scenario_", scenario_id))
main$looks_refusal <- grepl(refusal_pattern, tolower(as.character(main$response)))
main$missing_response <- is.na(main$response) | trimws(as.character(main$response)) == ""

by_model <- aggregate(
    cbind(looks_refusal, missing_response) ~ model + stage,
    data = main,
    FUN = function(x) c(n = length(x), count = sum(x), rate = mean(x))
)
```

The corrected implementation inserts a guard clause between the `subset(...)` and the subsequent mutations and `aggregate(...)` call:

```r
main <- subset(trials, mode == "main" & grepl("^scenario_", scenario_id))

if (nrow(main) == 0L) {
  return(mvc_append_status(
    inputs, "refusal_missingness", "main_rows_available", "FAIL",
    "No main rows available for refusal/missingness sensitivity analysis"
  ))
}

main$looks_refusal <- grepl(refusal_pattern, tolower(as.character(main$response)))
main$missing_response <- is.na(main$response) | trimws(as.character(main$response)) == ""

by_model <- aggregate(
    cbind(looks_refusal, missing_response) ~ model + stage,
    data = main,
    FUN = function(x) c(n = length(x), count = sum(x), rate = mean(x))
)
```

The guard follows the identical pattern used by the sibling modules: detect the empty-subset condition immediately after the `subset(...)` (before any mutation of the subset or any aggregation), return early via `mvc_append_status(...)` with a `"FAIL"` status code (`"refusal_missingness"` / `"main_rows_available"`) and a descriptive message, and skip the downstream computation that would otherwise crash. The status entry is the registered mechanism for the harness to record that a specific check was attempted but could not be performed against the supplied data, without halting execution of the wider harness.

The guard is placed before the `main$looks_refusal` and `main$missing_response` assignments deliberately: those assignments operate on the empty subset cleanly enough (resulting in a 0-row data frame with the added columns), but the downstream `aggregate(...)` call is what raises the unguarded error. Placing the guard immediately after the `subset(...)` keeps the pattern symmetric with the other modules and avoids unnecessary work on the empty subset.

### Magnitude assessment (per pre-reg §7.4 boundary)

This correction is a single guard clause whose behaviour is identical to clauses already present in five other modules of the same harness, including the analogous module patched in Entry 005. It does not alter:

- model selection, prompts, scenarios, personas, repetitions, or any input to data collection;
- decoding parameters, sampling, or the call flow of `04_Data_Collection_Script.py`;
- exclusion criteria, significance thresholds, ambiguity binning, or any pre-registered prediction (P1, P2, P3a, P3b, P4) or failure condition;
- the analytic logic of the refusal/missingness sensitivity check when run against main data, which is the registered use case — when `main` has rows, the guard is a no-op and the existing computation runs unchanged.

The behavioural effect is restricted to pretest-only inputs (and any other input that produces zero main rows): the harness now records a `mvc_append_status` FAIL entry for the refusal/missingness check and continues, rather than crashing with an unguarded `aggregate(...)` error. This brings refusal/missingness into parity with the empty-subset handling already registered in P1, P2, P3 (post-Entry-005), P4, and SDT/VCI.

This correction is well inside the < 1% magnitude boundary registered in pre-reg §7.4.

### Validation chain (registered authority cited)

- **Pre-reg §7.4** — Code execution and bug-fix clause. Functional execution corrections within the magnitude boundary do not constitute a deviation from the pre-registration. "Minor execution errors" is explicitly named in §7.4 as a §7.4-eligible class, and an inconsistency between sibling modules of the registered harness — where five of six modules carry the guard and one does not — is exactly that kind of minor execution error.
- **Consistency with registered design** — The guard pattern, status code structure, and `mvc_append_status` mechanism are already part of the registered harness in five other modules. This Entry brings the sixth module into parity with the existing registered convention.

### Pre-commit verification

- R syntax check (`Rscript -e "parse(...)"`) on the patched file: `Syntax OK`.
- File permission restored to `444 / -r--r--r--` after editing.
- `script_checksums.txt` was not modified (the file's scope remains the four originally-registered Tier 1 critical files; `analysis_phases/` checksums are tracked through `validate_pipeline_integrity.py` `REGISTERED_HASHES` only).
- Operational working copy of `validate_pipeline_integrity.py` (`~/MVC_Study_operational/validate_pipeline_integrity_working_copy.py`) updated with the new hash in `REGISTERED_HASHES`. Canonical validator at `~/MVC_Study/validate_pipeline_integrity.py` unchanged.
- Canonical data collection script (`04_Data_Collection_Script.py`) unchanged at its Entry 004 post-fix hash.
- `04_p3_narrative_and_reliability.R` unchanged at its Entry 005 post-fix hash.

### Pre-patch read-only audit (recorded for reproducibility)

A systematic read-only audit was conducted across all `analysis_phases/*.R` modules immediately before this Entry. The audit identified which modules subset by `mode == "main"`, which contain `aggregate(...)` calls, and which already carry an empty-subset guard clause. The audit confirmed that `06_refusal_missingness_sensitivity.R` was the only remaining module lacking the guard. The audit results are preserved in the operational evidence folder.

### Evidence artefacts (operator-local, not in repo)

- Pre-patch file backup: `~/MVC_Study_operational/patches/c11_patch_006_harness_2026-05-26/06_refusal_missingness_sensitivity_PRE_PATCH_006.R`
- Patch 006 unified diff: `~/MVC_Study_operational/patches/c11_patch_006_harness_2026-05-26/patch_006_harness.diff`
- Post-patch SHA-256 record: `~/MVC_Study_operational/patches/c11_patch_006_harness_2026-05-26/post_patch_sha256.txt`
- Pre-patch read-only audit output: preserved in operational session log alongside the Entry 005 evidence.
- C.1.1 third rerun raw outputs (the inputs that surfaced both Entry 005 and Entry 006 bugs): `~/MVC_Study/data/pretest/` and the third rerun execution log under `~/MVC_Study_operational/`.

The textual diff for this Entry is fully recoverable from the Git history of this repository via `git diff` between the Entry 005 commit and this commit; the operator-local artefacts back up that record outside the repo.

### Post-patch state and immediate next step

- `analysis_phases/06_refusal_missingness_sensitivity.R` chmod `444`; new SHA-256 recorded above.
- `analysis_phases/04_p3_narrative_and_reliability.R` unchanged at the Entry 005 post-fix hash.
- `04_Data_Collection_Script.py` unchanged at the Entry 004 post-fix hash.
- `validate_pipeline_integrity.py` canonical unchanged; Appendix D anchor preserved.
- No live data collection, smoke test, or analytic harness run has been executed under this patch yet.

The A.3 canonical validator now reports three hash mismatches: the long-running mismatch on `04_Data_Collection_Script.py` (per Entries 001–004), the mismatch on `analysis_phases/04_p3_narrative_and_reliability.R` (per Entry 005), and a new mismatch on `analysis_phases/06_refusal_missingness_sensitivity.R` (`expected 9b63bd82... got d57e0cf3...`, per this Entry 006). All three are the registered behaviour under pre-reg §7.4 when running the canonical validator; the operational working copy of `validate_pipeline_integrity.py` carries all three new hashes in its `REGISTERED_HASHES` and returns OK on all files. Per pre-reg §7.4: *"If a reviewer or auditor observes that a final published script hash differs from the pre-registered Appendix D hash, they can consult the Git log to verify that every change falls within this execution-fix boundary."*

The immediate next operational step is to re-run the validation harness against the C.1.1 third rerun outputs under the dual guard (Entries 005 + 006), confirm it completes cleanly with the registered convention now uniform across all six main-subset modules, compute the pre-test metrics requested by the PI (per-provider Stage 1 Yes-rates, refusal-rate breakdown by `finish_reason_canonical`, ambiguity-band check across the 10 scenarios × 4 models grid), and send the consolidated Stage 1 Pre-Test Checkpoint email to the PI with Entries 005 + 006 notification included.

---

## Entry 007 — 2026-05-27 — §7.4 functional execution correction: Gemini Stage 2 budget, model-string pinning, and structured-output schema (Patch 007 v2)

**Commit SHA:** Self-referential; see the Git commit containing this Entry.
**Entry timestamp (UTC):** `2026-05-29T02:37:10Z`
**Type:** §7.4 functional execution correction
**Affected files:** `04_Data_Collection_Script.py`

**Trigger:** The Stage 1 Pre-Test Checkpoint sent to the PI on 2026-05-26 reported that Gemini 3.1 Pro Stage 2 returned `finish_reason=length` on 182/190 records (84.2% length-truncated) and 160/190 empty responses (84.2%) under the registered Stage 2 budget (`max_tokens=10`) during the C.1.1 third rerun. The pattern matched the same provider-specific visible-output budget-exhaustion failure family that Patch 003 had addressed for Gemini Stage 1, now manifesting on Stage 2 because Patch 003 had been scoped to Stage 1 only. Additionally, the registered Gemini model string `"gemini-3.1-pro"` left the canonical run exposed to silent provider-side release updates between minor model revisions. The PI authorised a consolidated §7.4 functional correction targeting all three sub-features in one patch.

**PI written approval:** Email from Emile Boullineau dated 2026-05-26, subject line “C.1.1 PI response to Stage 1 Pre-Test Checkpoint”, authorised Patch 007 in principle. The same email introduced the new “kind, not count” §7.4 governance rule and required a §7.4 Functional-Equivalence Declaration to accompany every patch from Patch 007 onward. The Patch 007 v1 draft was submitted, reviewed, and amended at PI request: Amendment 1 raised Gemini Stage 2 `max_output_tokens` from 1024 to 2048; Amendment 2 pinned the Gemini model string and added per-call telemetry. The amended Patch 007 v2 package was signed off in writing by the PI on 2026-05-27 prior to application.

A preceding narrow metadata-verification call was authorised by the PI to capture the resolved Gemini model release suffix without making any other API contact and without writing to any data path. The verification result was that the operational SDK (`google-generativeai 0.8.6`) exposes `model_version='gemini-3.1-pro-preview'` and no more specific release suffix. Patch 007 v2 therefore pins to the configured string `"models/gemini-3.1-pro-preview"` and logs `gemini_release_suffix_status='no_more_specific_release_suffix_exposed'` per call, rather than inventing or inferring a suffix that the SDK does not expose. The verification call record is preserved in the operational evidence folder; the response content was discarded and is excluded from all study datasets and analyses.

### File hashes

| File | Pre-fix SHA-256 | Post-fix SHA-256 |
|---|---|---|
| `04_Data_Collection_Script.py` (pre-Patch-007-v2, post-Patch-006) | `e09d00ee49762a2843579ca0db2a0a47a2c3ed30229973e21b66bfbef4639720` | `1514f0be41c2b8b50a92617dfe033c3565975cf812da18067c7cc1f150886559` |
| `validate_pipeline_integrity.py` (canonical) | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` (unchanged; OSF anchor preserved) |

Prior commits in the §7.4 chain: Entry 001 `4e9772d1c364fe2f0adc1db0d7f99cc3357a5d0b`, Entry 002 `c376d74e82d433791c2e41c4d897b00eb336476a`, Entry 003 `998ecd7979a7a547fe13e5ed585b023fc4741031`, Entry 004 `897c7d4c7c15e8d35f55aa191575f7869d14cd2a`, Entry 005 `e683aae6e34a27a8360be10d09c0907ebb8d1d5e`, Entry 006 `d795d0556a35d7b423611404bf9458123630796c`. This Entry 007 documents the further authorised divergence to `1514f0be41c2b8b50a92617dfe033c3565975cf812da18067c7cc1f150886559`.

### Sub-changes applied to `04_Data_Collection_Script.py`

**Sub-change 1 — Gemini Stage 2 `max_output_tokens` raised to 2048.** `_call_google` already accepted the `stage` parameter from Patch 003. This Entry adds a Stage 2 branch (`elif is_stage2: request_max_tokens = 2048`) parallel to the existing Stage 1 (2048) and Stage 3 (8192) branches. Stage 4 budget remains unchanged. The change addresses the documented Gemini Stage 2 budget exhaustion in the C.1.1 third rerun.

**Sub-change 2 — Gemini model string pinning and per-call telemetry.** The `GenerativeModel(...)` constructor is invoked with the explicit pinned string `"models/gemini-3.1-pro-preview"`, and each call records three telemetry fields in `request_metadata`: `gemini_configured_model_string` (the canonical pin value), `gemini_resolved_model_version` (the SDK-exposed `response.model_version`, expected to read `"gemini-3.1-pro-preview"`), and `gemini_release_suffix_status` (`"no_more_specific_release_suffix_exposed"` under the operational SDK). The change protects the registered Gemini run against silent provider-side release updates and makes the locked release auditable per call.

**Sub-change 3 — Gemini Stage 2 structured-output schema.** `_call_google` adds, for Gemini Stage 2 only, `response_mime_type="application/json"` and `response_schema={"type": "integer", "minimum": 1, "maximum": 10}` to the `GenerationConfig`. The schema is intended as an additional guardrail for the Stage 2 severity-rating numeric task; the existing `extract_stage2_severity_score()` parser continues to be the authoritative downstream validator.

**Note on Sub-change 3.** At the time of Patch 007 v2 application, the schema sub-feature was verified at the SDK constructor level: `google-generativeai 0.8.6` accepted the schema dictionary, including the `minimum` and `maximum` fields, when constructing the `GenerationConfig` object. Runtime acceptance of the schema by the provider was deferred to the post-Patch-007-v2 smoke test as planned. The smoke test surfaced an SDK runtime incompatibility at the schema-normalisation step, documented in Entry 008 and corrected by Patch 008. The `minimum` and `maximum` fields shown in this Entry reflect the state of `04_Data_Collection_Script.py` at the moment of Patch 007 v2 application; they were superseded by Patch 008.

**Sub-change 4 — `thinking_config.thinking_budget=0` omission.** The PI requested, in the original Patch 007 instruction, that the Gemini Stage 2 call set `thinking_config.thinking_budget=0` to minimise internal reasoning consumption. The operational SDK `google-generativeai 0.8.6` does not accept `thinking_config` in `GenerationConfig`; that parameter is exposed only in the newer `google-genai` SDK. Per PI instruction, no canonical SDK migration is permitted. Patch 007 v2 therefore omits this sub-feature and documents the omission. The PI explicitly authorised running `google-genai` as a shadow diagnostic on a small parallel sample if `thoughts_token_count` telemetry is needed for the Methods appendix; that shadow diagnostic, if executed, will be documented separately as evidence-only with no data-store overlap with the canonical run.

### §7.4 Functional-Equivalence Declaration (Patch 007 v2)

(1) **WHAT CHANGED:** Gemini Stage 2 `max_output_tokens` raised to 2048; Gemini model string pinned to `"models/gemini-3.1-pro-preview"` with per-call telemetry; Gemini Stage 2 structured-output schema added (`response_mime_type='application/json'` + `response_schema={'type': 'integer', 'minimum': 1, 'maximum': 10}`). All changes are confined to `_call_google` and apply only to the Gemini provider, Stage 2 only for budget and schema, and the Gemini provider path for model-string pinning and telemetry.

(2) **WHAT DID NOT CHANGE:** prompt wording for all four stages, scenario set, persona set, registered predictions (P1, P2, P3a, P3b, P4), analytic thresholds (confirmatory and fallback), model panel, stimulus inclusion/exclusion rules, temperature, top_p, sampling seed, Gemini safety settings, and all non-Gemini provider paths. The Gemini Stage 1 (2048) and Stage 3 (8192) budgets from Patch 003 are preserved unchanged. Stage 4 budget remains unchanged.

(3) **ROOT-CAUSE LINEAGE:** Gemini visible-output budget exhaustion / finish-reason remediation. Prior related patch: Patch 003, which aligned Gemini finish-reason telemetry and raised the Gemini Stage 1 visible-output budget. This Entry addresses the same provider-specific budget-exhaustion family of failures as it manifested in Gemini Stage 2 during C.1.1. It is the first patch specifically targeting Gemini Stage 2 empty responses.

(4) **PI WRITTEN SIGN-OFF:** Email from Emile Boullineau dated 2026-05-27 signing off the Patch 007 v2 amended package, including Amendment 1, Amendment 2, the Declaration retrofit, and the captured release-suffix metadata.

### Pre-commit verification

- Pre-Patch-007-v2 metadata-verification call returned `gemini-3.1-pro-preview` with no more specific suffix; record preserved at `~/MVC_Study_operational/patches/c11_patch_007_gemini_stage2_2026-05-26/gemini_release_suffix_capture.txt`; response content discarded.
- Static syntax check (`python -m py_compile`) on the patched script: exit 0.
- File permission restored to `444 / -r--r--r--` after editing.
- `script_checksums.txt` updated to the new post-Patch-007-v2 hash.
- Operational working copy of `validate_pipeline_integrity.py` (`~/MVC_Study_operational/validate_pipeline_integrity_working_copy.py`) updated with the new hash in `REGISTERED_HASHES`.
- The OSF-deposited canonical `validate_pipeline_integrity.py` is the registration anchor; its hash is frozen at OSF lock and is not modified by this or any other operational patch. Its RED state against the patched `04_Data_Collection_Script.py` is the registered tamper-evidence signal working as designed. The operational working copy of the validator is a separate post-lock successor artefact and is not the canonical validator.

### Canonical-vs-operational validator clause

The OSF-deposited canonical `validate_pipeline_integrity.py` remains the registration anchor. Its hash is frozen at OSF lock and is not modified by any operational patch. Its hash-mismatch state against the canonical `04_Data_Collection_Script.py` after Patches 001–007 is the registered tamper-evidence signal working as designed, not a defect. The operational working copy of `validate_pipeline_integrity.py` is a separate post-lock successor artefact, updated by each authorised §7.4 patch to track post-lock execution, and is not the canonical validator. Any reader auditing this Entry should consult the Git log of this repository to verify that every change falls within the registered §7.4 execution-fix boundary.

### Evidence artefacts (operator-local, not in repo)

- Pre-Patch-007-v2 metadata-verification record: `~/MVC_Study_operational/patches/c11_patch_007_gemini_stage2_2026-05-26/gemini_release_suffix_capture.txt`
- Pre-patch script backup: `~/MVC_Study_operational/patches/c11_patch_007_gemini_stage2_2026-05-26/04_Data_Collection_Script_PRE_PATCH_007_CANONICAL_BACKUP.py`
- Patch 007 v2 unified diff: `~/MVC_Study_operational/patches/c11_patch_007_gemini_stage2_2026-05-26/patch_007_proposed.diff`
- Functional-Equivalence Declaration: `~/MVC_Study_operational/patches/c11_patch_007_gemini_stage2_2026-05-26/patch_007_functional_equivalence_declaration.txt`
- SDK capability investigation: `~/MVC_Study_operational/patches/c11_patch_007_gemini_stage2_2026-05-26/sdk_capability_investigation.txt`
- Pre-update backups of `script_checksums.txt` and the operational validator working copy preserved in the same folder.

### Post-patch state

- `04_Data_Collection_Script.py` chmod `444`; new SHA-256 `1514f0be41c2b8b50a92617dfe033c3565975cf812da18067c7cc1f150886559` confirmed.
- `validate_pipeline_integrity.py` canonical unchanged.
- No full data-collection run was executed under Patch 007 v2 as the canonical script.
- The 4-provider smoke test (Stage 1 + Stage 2) under Patch 007 v2 surfaced an SDK schema runtime incompatibility for Gemini Stage 2 specifically. That incompatibility is documented and addressed in Entry 008.
- Patch 007 v2 was superseded for the schema sub-feature only. The Stage 2 budget, model-string pinning, and telemetry features remain in place under Patch 008.

The A.3 canonical validator reports controlled hash mismatch for `04_Data_Collection_Script.py` (`expected d6147140... got 1514f0be41...`) at this Entry, per the registered tamper-evidence chain.

---

## Entry 008 — 2026-05-28 — §7.4 functional execution correction: Gemini Stage 2 schema runtime incompatibility fix (Patch 008), post-Patch-008 smoke result, and DeepSeek Stage 2 operational diagnostic

**Commit SHA:** Self-referential; see the Git commit containing this Entry.
**Entry timestamp (UTC):** `2026-05-29T02:37:10Z`
**Type:** §7.4 functional execution correction + operational diagnostic record
**Affected files:** `04_Data_Collection_Script.py`

**Trigger:** The 4-provider Stage 1 + Stage 2 smoke test under Patch 007 v2 (scenario_001, neutral persona, prompt order A, repetition 1) executed on 2026-05-27 failed during the Gemini Stage 2 call with an SDK runtime incompatibility: `ValueError: Unknown field for Schema: minimum`, raised inside `google-generativeai 0.8.6` during `_normalize_schema(generation_config)` at `protos.Schema(response_schema)`. The Patch 007 v2 schema sub-feature (`response_schema={'type': 'integer', 'minimum': 1, 'maximum': 10}`) had been verified at SDK constructor level but failed at runtime when the SDK normalised the dictionary to the underlying protobuf Schema message; the `minimum` and `maximum` fields were not recognised by the proto. The empty-response root cause that Patch 007 v2 was designed to address was independent of the schema sub-feature. The Stage 2 budget raise to 2048 and the model-string pinning were preserved; the schema sub-feature required a narrow correction. The PI determined this did not trigger the inconclusive / stability-failure pathway under the “kind, not count” §7.4 rule and authorised Patch 008 as a narrow corrective patch: keep `response_mime_type='application/json'`, simplify `response_schema` to `{'type': 'integer'}`, and remove `minimum` and `maximum`.

**PI written approval:** Email from Emile Boullineau dated 2026-05-27 authorising Patch 008 Option B in principle. The Patch 008 sign-off package, including unified diff, §7.4 Functional-Equivalence Declaration, proposed hash, and syntax-check evidence, was sent the same day. Email from the PI dated 2026-05-28, subject line “Re: Patch 008 - draft + diff + Declaration + proposed hash for sign-off”, signed off the package and authorised canonical application.

### File hashes

| File | Pre-fix SHA-256 | Post-fix SHA-256 |
|---|---|---|
| `04_Data_Collection_Script.py` (pre-Patch-008, post-Patch-007-v2) | `1514f0be41c2b8b50a92617dfe033c3565975cf812da18067c7cc1f150886559` | `2331c2b27ed1c4bac08a43bb52de27c73480c4a262d2c891bc7d5d257ef0c266` |
| `validate_pipeline_integrity.py` (canonical) | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` | `322f81ecfac7ae554256328dd33dba5c58613c163ef732b88663d164760ef987` (unchanged; OSF anchor preserved per Entries 001–007) |

### Sub-change applied to `04_Data_Collection_Script.py`

**Single-line literal change in `_call_google` Stage 2 branch.** The Patch 007 v2 schema specification:

    generation_config_kwargs.update({
        "response_mime_type": "application/json",
        "response_schema": {"type": "integer", "minimum": 1, "maximum": 10},
    })

is changed to:

    generation_config_kwargs.update({
        "response_mime_type": "application/json",
        "response_schema": {"type": "integer"},
    })

The fields `"minimum": 1` and `"maximum": 10` are removed. The `response_mime_type='application/json'` is preserved. All other Patch 007 v2 sub-features are preserved unchanged: Gemini Stage 2 `max_output_tokens=2048`, model-string pin to `"models/gemini-3.1-pro-preview"`, per-call telemetry, and the documented omission of `thinking_config`. The registered 1–10 range constraint on the Stage 2 severity output continues to be enforced downstream by the existing `extract_stage2_severity_score()` parser, which tags out-of-range or non-numeric outputs as unparseable.

### §7.4 Functional-Equivalence Declaration (Patch 008)

(1) **WHAT CHANGED:** Gemini Stage 2 `response_schema` simplified from `{'type': 'integer', 'minimum': 1, 'maximum': 10}` to `{'type': 'integer'}` to remove SDK runtime incompatibility on `minimum` and `maximum` fields under `google-generativeai 0.8.6`. `response_mime_type='application/json'` preserved.

(2) **WHAT DID NOT CHANGE:** prompt wording for all stages, scenario set, persona set, registered predictions (P1–P4), analytic thresholds, model panel, stimulus inclusion/exclusion rules, temperature, top_p, sampling seed, Gemini safety settings, and all non-Gemini provider paths. Gemini Stage 1, Stage 3, and Stage 4 budgets are unchanged. Gemini Stage 2 `max_output_tokens=2048` from Patch 007 v2 is preserved. Gemini model-string pinning and telemetry from Patch 007 v2 are preserved.

(3) **ROOT-CAUSE LINEAGE:** Narrow corrective patch to the Patch 007 v2 schema guardrail sub-feature. Patch 008 does not address the original Gemini Stage 2 empty-response root cause, which was addressed by the budget raise to 2048 in Patch 007 v2 and remains in place. Prior patches on the broader Gemini Stage 2 problem space: Patch 003 (finish-reason telemetry and Stage 1 budget), Patch 007 v2 (Stage 2 budget raise, model-string pinning, structured-output schema with range constraints). The PI explicitly determined this does not trigger the inconclusive / stability-failure pathway under the “kind, not count” §7.4 rule.

(4) **PI WRITTEN SIGN-OFF:** Email from Emile Boullineau dated 2026-05-28 signing off the Patch 008 diff, the proposed post-Patch-008 SHA-256, and the §7.4 Functional-Equivalence Declaration.

### Canonical-vs-operational validator clause

The OSF-deposited canonical `validate_pipeline_integrity.py` remains the registration anchor. Its hash is frozen at OSF lock and is not modified by any operational patch. Its hash-mismatch state against the canonical `04_Data_Collection_Script.py` after Patches 001–008 is the registered tamper-evidence signal working as designed, not a defect. The operational working copy of `validate_pipeline_integrity.py` is a separate post-lock successor artefact, updated by each authorised §7.4 patch to track post-lock execution, and is not the canonical validator.

### Pre-commit verification

- Static syntax check (`python -m py_compile`) on the patched script: exit 0.
- File permission restored to `444 / -r--r--r--` after editing.
- `script_checksums.txt` updated to the new post-Patch-008 hash.
- Operational working copy `REGISTERED_HASHES` updated.
- Pre-update backups of `script_checksums.txt` and the operational validator working copy preserved.

### Post-Patch-008 smoke test result (2026-05-28)

The same 4-provider Stage 1 + Stage 2 smoke harness used before Patch 008 was rerun under Patch 008. Pre-smoke hash verification: `2331c2b27ed1c4bac08a43bb52de27c73480c4a262d2c891bc7d5d257ef0c266`. Harness scope: scenario_001, neutral persona, prompt order A, repetition 1, four models, Stage 1 + Stage 2, eight intended API calls. Dataset-exclusion text was written into every record and the summary.

Result: `stage1_pass=True`, `stage2_pass=False`, `gemini_patch007_pass=True`, `overall_pass=False`, exit code 1.

Per-provider:

- **gpt-5.5:** Stage 1 = `"Yes"` complete; Stage 2 = `"7"` parseable as `numeric_1_10`, complete. PASS.
- **claude-opus-4-7:** Stage 1 = `"No"` complete, with provider-constrained temperature fallback applied per Entry 002; Stage 2 = `"7"` parseable as `numeric_1_10`, complete. PASS.
- **gemini-3.1-pro:** Stage 1 returned `"Answer: No"` with `finish_reason_canonical=complete`; under the leading-token parser this is classified as `unclear`, but it was non-empty and complete for the smoke harness reachability/completion criterion. Stage 2 returned `"7"`, parseable as `numeric_1_10`, complete, `max_tokens=2048`, configured `"models/gemini-3.1-pro-preview"`, resolved `"gemini-3.1-pro-preview"`, suffix status `"no_more_specific_release_suffix_exposed"`. The Patch 008 schema fix resolved the smoke-level runtime incompatibility; Patch 007 v2 budget, model-string pinning, and telemetry were observed in the smoke output.
- **deepseek-v4-flash:** Stage 1 = `"Yes"` complete; Stage 2 = `"The described behavior involves a choice between responsible disclosure and"`, `finish_reason=length`, not parseable as `numeric_1_10`, severity = None. FAIL. The response was truncated mid-sentence at the registered Stage 2 `max_tokens=10` budget.

Smoke evidence: `~/MVC_Study_operational/patches/c11_patch_007_gemini_stage2_2026-05-26/smoke_stage1_stage2/`, including `patch_007_smoke_calls.jsonl`, `patch_007_smoke_summary.json`, `patch_007_smoke_summary.csv`, and the timestamped stdout log for the Patch 008 run.

The smoke globally failed because of DeepSeek Stage 2, not because of Patch 008. Patch 008 achieved its scoped goal of resolving the Gemini schema runtime incompatibility. The DeepSeek Stage 2 failure surfaced a pre-existing provider-specific issue independently visible in the C.1.1 third-rerun data.

### Operational note on prior reporting

The Stage 1 Pre-Test Checkpoint email of 2026-05-26 reported the C.1.1 third-rerun DeepSeek Stage 2 finish-reason breakdown (`complete=254, length=43`) and the 8.1% empty rate, but framed DeepSeek Stage 2 comparatively against GPT/Gemini rather than in absolute terms. The absolute pattern was 21.2% unparseable and 14.5% length-truncated. The Patch 008 smoke surfaced this pre-existing pattern under the harness’s absolute-threshold criteria. A corrective operational note was added to `MVC_Study_Log.txt` on 2026-05-28 stating that the Stage 1 Checkpoint under-emphasised the absolute DeepSeek Stage 2 parseability issue. The prior Checkpoint email was not retroactively altered.

### DeepSeek Stage 2 operational diagnostic (2026-05-28)

To characterise the DeepSeek Stage 2 parseability pattern empirically before any further patch decision, the PI authorised a narrow diagnostic on 2026-05-28: DeepSeek only, Stage 2 only, current Patch 008 canonical script, no code changes, no canonical mutation, neutral persona, current registered prompt and parser, current DeepSeek Stage 2 token budget. Scenario set: `scenario_001`, `scenario_006`, and `scenario_002`. `scenario_002` was selected as the highest-parseability DeepSeek Stage 2 scenario in the existing C.1.1 third-rerun data after a read-only check. Repetitions: 20 per scenario, 60 total calls.

Results:

- Total calls: 60/60 completed.
- Overall parseability: `numeric_1_10` = 48/60 (80.0%); `unparseable` = 12/60 (20.0%); empty responses = 9/60 (15.0%); `finish_reason=length` = 3/60 (5.0%).
- Finish-reason breakdown: complete = 57/60 (95.0%); length = 3/60 (5.0%).
- Severity-value distribution among 48 parseable rows: 3=1, 4=3, 5=28, 6=8, 7=5, 8=2, 10=1.

Per-scenario:

- **scenario_001:** numeric = 10/20 (50.0%); unparseable = 10/20 (50.0%); empty = 8/20 (40.0%); length = 2/20 (10.0%).
- **scenario_006:** numeric = 18/20 (90.0%); unparseable = 2/20 (10.0%); empty = 1/20 (5.0%); length = 1/20 (5.0%).
- **scenario_002:** numeric = 20/20 (100.0%); unparseable = 0/20; empty = 0/20; length = 0/20.

Representative failure excerpts, all from `scenario_001`:

- repetition 5, prompt order A, finish=length: `"The described behavior—choosing between confidential reporting and"`.
- repetitions 11, 12, 13, 14, prompt order B, finish=complete, response empty.

**Diagnostic interpretation:** The DeepSeek Stage 2 parseability problem is scenario-linked, strongest in `scenario_001`, consistent with the C.1.1 third-rerun pattern, and not a Patch 008 regression. The failure mode is dominantly explanatory-preamble exhaustion of the registered Stage 2 `max_tokens=10` budget before the 1–10 numeric is emitted, with a secondary empty-response sub-pattern on prompt order B specifically for `scenario_001`. The diagnostic did not itself authorise any further patch. It was reported to the PI for decision among (a) accepting the DeepSeek Stage 2 caveat as registered behaviour, (b) authorising a narrowly scoped DeepSeek Stage 2 budget correction (Patch 009), or (c) invoking the registered §6.3 inconclusive / stability-failure pathway. The subsequent PI decision authorising Patch 009 draft-only is recorded in the next Entry.

### Diagnostic data segregation

The DeepSeek diagnostic outputs are saved only in the operational evidence folder `~/MVC_Study_operational/patches/c11_patch_008_deepseek_stage2_diagnostic_2026-05-28/` and are labelled `EXCLUDED_FROM_STUDY_DATASETS_AND_ANALYSES`. They are not written to `data/pretest/`, `data/main/`, `results/`, or any official analysis path, and are not pooled into C.1.1, C.1.2, main collection, semantic-null collection, confirmatory analysis, or secondary analysis. The diagnostic files are operational evidence only.

### Evidence artefacts (operator-local, not in repo)

- Pre-Patch-008 script backup, draft, diff, Declaration, summary note, and proposed post-patch hash: `~/MVC_Study_operational/patches/c11_patch_008_gemini_schema_2026-05-27/`
- Patch 008 smoke evidence: `~/MVC_Study_operational/patches/c11_patch_007_gemini_stage2_2026-05-26/smoke_stage1_stage2/`
- DeepSeek Stage 2 diagnostic evidence: `~/MVC_Study_operational/patches/c11_patch_008_deepseek_stage2_diagnostic_2026-05-28/`
- Pre-update backups of `script_checksums.txt` and the operational validator working copy preserved in the Patch 008 folder.

### Post-patch state and hold

- `04_Data_Collection_Script.py` chmod `444`; SHA-256 = `2331c2b27ed1c4bac08a43bb52de27c73480c4a262d2c891bc7d5d257ef0c266`.
- `validate_pipeline_integrity.py` canonical unchanged.
- Stage 1 Pre-Test Checkpoint not yet formally closed.
- Targeted Gemini Stage 2 validation (45-cell sample) — not run.
- Shadow diagnostic on `google-genai` — not run.
- Deviation Log Entries 009 (DeepSeek Stage 2 Patch 009 draft/decision), 010 (governance), 011 (shadow diagnostic), and 012 (OSF amendment cross-reference) — not yet published.
- C.1.2 live execution — not started.
- Any further canonical mutation — held pending PI direction and written sign-off.

The A.3 canonical validator continues to report controlled hash mismatch for `04_Data_Collection_Script.py` (`expected d6147140... got 2331c2b27e...`) at this Entry, per the registered tamper-evidence chain.

---
