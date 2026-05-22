# MVC Study — Tamper-Evidence Anchor Repository

This repository is the registered public tamper-evidence anchor for the MVC (Motivated Violation Construction) Study, per OSF pre-registration §7.4.

## Authoritative source

The full registered package, all hash-locked materials, and the authoritative pre-registration document live on OSF:

- **OSF project:** https://osf.io/6m3sk
- **Pre-registration approved:** 16 May 2026
- **Embargo:** until 15 May 2027

## Pre-registration PDF integrity anchor

The SHA-256 of the authoritative pre-registration PDF (`00_OSF_Pre_Registration.pdf` in the OSF package) is:

d51365f14b1adbcccccf3fed38259f3c28048553acc2aaddca257bd592f25741

This hash is also recorded in `00_README.md` of the OSF package and matches the file deposited there. Any divergence between this hash and the OSF-deposited file indicates a tamper event.

## What lives in this repository

Per pre-reg §7.4 tamper-evidence chain, this repository carries:

- `supplementary/MVC_Deviation_Log.md` — append-only registry of every deviation from the pre-registered protocol. Each entry includes its own commit SHA as a first-line metadata field, so any post-entry edit would break the commit-to-entry correspondence and be detectable in the public git history.
- `LICENSE.md` - CC BY-NC-SA 4.0, applicable to all registered materials.
- `README.md` (this file) — anchor index.

Additional files from the OSF package may be mirrored here on a case-by-case basis, at PI discretion, for reviewer convenience. The OSF deposit remains the canonical source.

## How to audit

1. `git log --all` shows the full append-only history of the deviation log and any subsequent commits.
2. `git diff <commit1> <commit2>` shows the exact textual change between two commits.
3. Each deviation entry records its own commit SHA in metadata; cross-check against `git log` to confirm the entry has not been altered since it was first committed.
4. Compare the SHA-256 of any registered file against its Appendix D digest in the OSF pre-registration PDF.

## Background DOI

MVC theory preprint (background reading only): 10.5281/zenodo.19423437.

## Authority hierarchy

In case of any discrepancy between this repository and the OSF deposit, **the OSF pre-registration is the sole authoritative specification.** This repository exists solely to satisfy pre-reg §7.4 tamper-evidence requirements.

## Contact

Principal Investigator: Emile Boullineau (emile@judgmentalism.org)
Research Associate: José Daniel Muñoz Arciniegas
