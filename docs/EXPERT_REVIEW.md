# Expert review guide

This repository holds computational research and a study protocol. **No patient data has been collected, no experiment has been run, and nothing here has been clinically validated.** The purpose of this guide is to make it easy to attack the work, so that weak claims are found before anyone relies on them.

## What can be reviewed

| Your expertise | Start here | What to try to break |
|---|---|---|
| Gynaecologic or radiation oncology | `docs/thesis/THESIS_52_AGENTIC_CARE_LOOPS.md`, Chapters 3–4; the synthetic board `apps/case_board/demo.html` | Gates, pathway branches, stage logic, timing alerts, whether the pathways fit real practice in a low-resource hospital |
| Pathology | Thesis §4.2 and the report panel on the demo board | The four seeded misreadings and their corrections; anything stated about margins, stage or biomarkers |
| Biostatistics | Thesis §3.7–3.10 | Sample size, interval widths, definition of "acceptable" concordance, blinding, baseline comparator |
| Clinical informatics / ML safety | Thesis §3.6 and §5.1 | Hallucinated evidence, over-trust, privacy, failure modes the boundary table misses |
| Identifiability and dynamical systems | `README.md` key result, `models/`, `validation/` | The 7/17 to 15/17 identifiable-parameter claim, CCLE data handling, whether synthetic validation was fully replaced |
| Research software | `tests/`, `pyproject.toml`, `docs/MERGE_READINESS.md` | Whether results reproduce from a clean install, seeds, hidden parameters |

## A 30-minute path

1. Read `DISCLAIMER.md` (2 minutes) and the "Evidence status" table in the thesis (3 minutes).
2. Open the demo board and step through the five phases (10 minutes). Every finding on it is invented.
3. Open `docs/claims_ledger.csv` and pick the three claims closest to your expertise (10 minutes).
4. Open an issue with the **Expert critique** form (5 minutes).

## The feedback that helps most

- An argument that a specific claim is wrong, with the mechanism, dataset or trial that shows it.
- A test that would falsify a hypothesis (H1–H4) and that this project could run.
- A missed alternative explanation, confounder or failure mode.
- A correction to a reference or to a number transcribed from a trial.

Praise, or general encouragement, helps less than one solid objection.

## How feedback is handled

- Feedback arrives as a public issue, unless the reviewer asks for a private channel.
- Each claim in `docs/claims_ledger.csv` has a status. A valid objection changes the status or the text, and the change is recorded in the issue.
- Reviewers are thanked by name in the acknowledgements only with their written permission.
- Nothing here asks a reviewer to endorse the work.

## Limits stated up front

- The framework is a proposal (E1). The hypotheses are untested (E0).
- Evidence levels: E0 speculation, E1 theoretical proposal, E2 computational or simulation evidence, E3 observational, E4 experimental, E5 clinical or real-world validation. A claim is never moved up a level without new evidence.
- The software and thesis text were produced with AI assistance. The disclosure is in the thesis declaration.
- Reference checks so far cover existence, authors, journal, year and DOI for references 3–9 in the thesis. They do not cover whether each paper supports the sentence it is attached to at full-text level.

## Not in this repository

Real patient reports, identifiers and hospital records are excluded on purpose. See `docs/PRIVACY_AND_CONSENT.md`.
