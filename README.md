# Closed-Loop Agentic Care Planning for Cervical Cancer: A Gated Action–Observation Framework, Synthetic Worked Example and Study Protocol

A pathology report states what a tumour is. It does not say how far the disease has spread,
whether the patient can tolerate treatment, what the local hospital can deliver, or what should
happen next. This thesis treats the care of one patient as a partially observed control problem:
the patient's true state is hidden, actions either gather information or change the state, and
decision gates stop a plan from committing to a therapeutic class until the observations that
decide it are present.

**Thesis #52.** Computational and health-systems research, set out in Nile University B.Sc.
chapter order for handoff.

**Author:** Kelechi Emeka Ogbonna
**Correspondence:** kelechiogbonna300@gmail.com
**GitHub:** https://github.com/cloudynirvana
**Date:** 29 September 2026

---

## Status — read this before citing

- **Protocol stage.** The framework is specified and demonstrated on **one invented (synthetic)
  case**. There is **no outcome data**, no concordance measurement and no time-saving result.
- The four evaluation studies in Chapter Three **have not been run**. Each needs a clinical
  partner and research ethics approval first.
- A worked example from a real pseudonymised pathology report is **withheld** until patient
  consent, institutional permission and ethics approval are recorded. See
  [`docs/PRIVACY_AND_CONSENT.md`](docs/PRIVACY_AND_CONSENT.md).
- **Reference verification:** references 3–9 were matched to PubMed records. References 1–2 and
  10–15 have not been checked, and no claim has been re-read against full text. Claim-by-claim
  status is in [`docs/claims_ledger.csv`](docs/claims_ledger.csv).
- Statements still needing sources are marked `[CITATION NEEDED]` in the manuscript. They are
  left visible on purpose.

This is research only. It is **not** a medical device, **not** clinical decision support in use,
**not** a dose, and **not** a cure. See [DISCLAIMER.md](DISCLAIMER.md).

---

## What the thesis contains

The care of one patient is written as a five-phase loop — characterise, decide, treat and
monitor, evaluate, follow up or escalate — in which every action has an owner and returns an
observation, and every observation opens the next action or changes the pathway.

| Chapter | Contents |
| --- | --- |
| One | Where outcome is lost between diagnosis and treatment; problem statement; objectives |
| Two | Process failures and survival; tumour boards and earlier decision support; acting under partial observation; language-model agents in medicine |
| Three | The case as a partially observed state; gates; the five-phase loop; a 17-capability agent taxonomy in six layers; four evaluation study protocols with hypotheses and sample sizes |
| Four | Synthetic worked example, with four misreadings seeded on purpose as test items |
| Five | Discussion, conclusion, recommendations |

An **evidence-status table** for the main claims sits ahead of Chapter One, and an **AI-use
disclosure** is in the declaration.

## Reviewers

Expert critique is the point of this deposit. Start with
[`docs/EXPERT_REVIEW.md`](docs/EXPERT_REVIEW.md), which names what is being asked of which
speciality, and [`docs/claims_ledger.csv`](docs/claims_ledger.csv), which lists each claim with
its evidence level, basis, verification status and the kind of reviewer it needs.

The most useful review would tell me where a gate is wrong, where a pathway step does not match
practice in a resource-constrained setting, or where a cited paper does not support the sentence
it is attached to.

**Do not paste patient information into issues or comments.** See the privacy policy.

## Files

| Path | Role |
| --- | --- |
| `THESIS.md` | Manuscript (Chapters One to Five, Vancouver citations) |
| `build_pdf.py` | Regenerates `THESIS.pdf` from the Markdown |
| `docs/claims_ledger.csv` | Each claim with evidence level, basis, verification status, reviewer type |
| `docs/EXPERT_REVIEW.md` | What critique is being asked for, and from whom |
| `docs/PRIVACY_AND_CONSENT.md` | Rules on patient content in this repository |
| `apps/case_board/demo.html` | The case board, running an invented case |
| `apps/case_board/index.html` | Landing page |
| `apps/case_board/DEPLOY.md` | Static deployment notes |
| `CITATION.cff` | Citation metadata |
| `DISCLAIMER.md` | Research-only boundary |
| `docs/ZENODO_ORCID.md` | How the DOI was obtained: ORCID, then Zenodo |

## The case board

`apps/case_board/demo.html` is a single static page, no build step and no dependencies beyond a
web font. Open it in a browser, or serve the folder:

```bash
python3 -m http.server --directory apps/case_board 8000
# then open http://127.0.0.1:8000
```

The board runs **one invented case**. Its report text, values and findings are fabricated for
demonstration. Anything a viewer enters stays in that browser; nothing is transmitted or stored
remotely.

## Reproduce the PDF

```bash
python3 -m pip install markdown weasyprint
python3 build_pdf.py
```

## Cite

Ogbonna KE. Closed-loop agentic care planning for cervical cancer: a gated action–observation
framework, synthetic worked example and study protocol [Internet]. Thesis #52 computational and
health-systems research thesis. 29 September 2026 [cited YYYY Mon DD]. Available from:
https://github.com/cloudynirvana/thesis-52-agentic-care-loops

Machine-readable fields are in [`CITATION.cff`](CITATION.cff). **Once a Zenodo release has
minted a DOI, add it to `CITATION.cff` and to the citation above.** Do not add a DOI before one
exists.

Hub index, for cataloguing only:
[research-theses-hub](https://github.com/cloudynirvana/research-theses-hub).

## Related work in this series

| Thesis | Relevance |
| --- | --- |
| [T11](https://github.com/cloudynirvana/thesis-11-desmoplastic-transport-identifiability) | Desmoplastic transport identifiability — why drug delivery through fibrotic stroma is a physics problem a lumped ODE cannot express |
| [T19](https://github.com/cloudynirvana/thesis-19-forcing-admission-gates-tip-ode) | Forcing-admission gates — the discipline that keeps guideline statements from becoming model coefficients |
| [T20](https://github.com/cloudynirvana/thesis-20-occult-modes-partial-liquid-biopsy-observer) | Occult disease modes under sparse, delayed observers |
| [T31](https://github.com/cloudynirvana/thesis-31-casecards-forcing-admission-predicates) | Guideline CaseCards as admission predicates |

The epistemic boundary used across the series:

```text
Knowledge ≠ Evidence ≠ Mechanism ≠ Parameter ≠ Prediction
```

## Licence

Text and code are MIT, with attribution. Computational and health-systems research only.
