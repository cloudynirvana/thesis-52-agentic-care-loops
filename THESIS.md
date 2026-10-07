# Closed-Loop Agentic Care Planning for Cervical Cancer: A Gated Action–Observation Framework, Synthetic Worked Example and Study Protocol

**Thesis #52. Computational and health-systems research thesis (protocol-stage draft)**  
**Author:** Kelechi Emeka Ogbonna  
**Correspondence:** https://github.com/cloudynirvana  
**Date:** 29 September 2026  
**Format:** B.Sc. project chapters (Nile University style), written as a methods and study-protocol manuscript  
**Status:** Framework specified and demonstrated on one invented (synthetic) case. No outcome data. The evaluation studies in Chapter Three have not been run and need ethics approval first. A worked example from a real pseudonymised report is withheld until consent and ethics permission are in place.
**Citation style:** numbered Vancouver. References marked † must be checked against Crossref before submission.  
**DOI:** none. Do not invent one.  
**Reference verification (29 September 2026):** references 3–9 were matched to PubMed records (authors, journal, year, DOI). References 1–2 and 10–15 have not been checked. No claim has been re-read against full text. Claim-by-claim status is in `docs/claims_ledger.csv`.

---

## Title page

**CLOSED-LOOP AGENTIC CARE PLANNING FOR CERVICAL CANCER: A GATED ACTION–OBSERVATION FRAMEWORK, SYNTHETIC WORKED EXAMPLE AND STUDY PROTOCOL**

BY

**KELECHI EMEKA OGBONNA**

A COMPUTATIONAL AND HEALTH-SYSTEMS RESEARCH THESIS  
(FRAMEWORK AND STUDY PROTOCOL)

PROJECT CONFLUENCE  
INDEPENDENT COMPUTATIONAL RESEARCH

SUPERVISOR: not appointed for this deposit

SEPTEMBER 2026

---

## Declaration

I, Kelechi Emeka Ogbonna, declare that this thesis was carried out by me. The worked example in Chapter Four uses an invented case, and the case-board software that displays it was built with an AI coding agent. No patient was treated, and no treatment was changed or recommended, by this work. No outcome, concordance figure or time saving is reported, because none has been measured.

**AI-use disclosure [author to confirm before submission].** During the preparation of this work the author used Claude (Anthropic, Claude Sonnet 5.5) to structure the manuscript, edit language, check references against PubMed, and build the synthetic demonstration case and case-board software. The author reviewed and edited the content and is responsible for it.

_________________________     _______________________  
Kelechi Emeka Ogbonna         Date

---

## Abstract

A pathology report states what a tumour is. It does not say how far the disease has spread, whether the patient can tolerate treatment, what the local hospital can deliver, or what should happen next. In low-resource settings, the gap between diagnosis and effective treatment is filled by many separate actions, each owned by a different person, and failures in that chain cost lives. In cervical cancer, for example, radiotherapy that runs past about 56 days and radiotherapy given without brachytherapy are both linked to worse survival. Neither is a drug problem.

This thesis treats the care of one patient as a partially observed control problem. The patient's true state is hidden. Actions either gather information (staging imaging, an HIV test, a PD-L1 stain) or change the state (chemoradiation). Each action has an owner and returns an observation. Rules turn the current set of observations into the next action. Gates stop the plan from committing to a regimen until the observations that decide it are present. An AI agent maintains this loop. It reads reports, keeps the state, finds the missing facts, maps observations to guideline options with their evidence, matches trials, and flags safety and timing risks. Humans stage, choose, dose and consent.

The framework is specified as a disease-independent case schema, a rule set per pathology, an evidence store, and a five-phase loop: characterise, decide, treat and monitor, evaluate, and follow up or escalate. It is demonstrated on one invented cervical cancer case. Disease independence is a hypothesis for Study 3, not a result. The demonstration seeds four common misreadings of a biopsy report as test items and checks that the rules state the correction. It does not measure how often the agent detects errors. A demonstration on a real report is withheld pending consent and ethics review.

Seventeen agent capabilities are named and grouped into six layers. Four evaluation studies are proposed: retrospective concordance with tumour-board decisions, process timing, cross-pathology reuse of the schema, and a prospective palliative-care pathway for patients diagnosed at a late stage. Hypotheses are stated with their primary outcomes. None has been tested.

Research only. Not a medical device, not clinical decision support in use, not a dose, and not a cure.

---

## Keywords

agentic medicine; closed-loop care; partially observable decision process; value of information; tumour board; cervical cancer; low-resource oncology; personalised medicine; palliative care; guideline concordance

---

## Table of Contents

- Chapter One: Introduction
  - 1.1 Background to the study
  - 1.2 Statement of research problem
  - 1.3 Justification of study
  - 1.4 Aim and objectives of the study
  - 1.5 Significance of the study
  - 1.6 Scope of the study
- Chapter Two: Literature review
- Chapter Three: Materials and methods
- Chapter Four: Worked example (synthetic case S-01)
- Chapter Five: Discussion, conclusion and recommendation
- References

---

## Evidence status of the main claims

| Claim | Level | Status |
|---|---|---|
| Care can be written as a gated action–observation loop | E1 (theoretical proposal) | Specified, untested |
| An agent can maintain the loop and match tumour-board decisions | E0 (hypothesis H1) | No data |
| Alerts would have fired before delays | E0 (hypothesis H2) | No data |
| The schema transfers across pathologies | E0 (hypothesis H3) | No data |
| Earlier palliative referral improves quality of life in this setting | E0 (hypothesis H4) | No data |
| Literature claims in Chapters One and Two | E3–E5 as cited | See `docs/claims_ledger.csv` |

# CHAPTER ONE

## 1.0 INTRODUCTION

### 1.1 Background to the study

Most of the benefit in modern oncology comes from treatments that already exist, delivered correctly and on time. For locally advanced cervical cancer, the curative backbone is chemoradiation followed by brachytherapy [1,2]. Pembrolizumab added to chemoradiation improved overall survival in KEYNOTE-A18 [3], and six weeks of cheap induction chemotherapy improved it in INTERLACE [4]. Each of these effects is real. Each is also easily lost: radiotherapy prolonged past about 55–56 days lowers pelvic control [5], and omitting brachytherapy is linked to lower survival [6].

Cervical cancer is also where HIV and cancer meet. Women living with HIV have about six times the risk of cervical cancer [7], and tenofovir disoproxil, common in first-line antiretroviral regimens, adds to cisplatin's kidney toxicity [CITATION NEEDED: current Nigerian ART guideline and a nephrotoxicity source]. Getting the right patient the right treatment therefore depends on a chain of ordinary actions: an HIV test, a creatinine clearance, an MRI, a brachytherapy booking. Those actions are owned by different people and usually tracked in no single place.

For patients diagnosed late, the same argument applies to quality of life. Early, integrated palliative care improved quality of life, and in one trial survival, in metastatic lung cancer [8]. That benefit also depends on a referral happening at the right time.

Large language models can now read clinical text, write and run code, retrieve evidence and keep structured state over a long task. An agent built on them could maintain the chain of actions for each patient. Earlier attempts at oncology decision support were limited by recommendations that did not fit local practice and by weak validation [9]. This thesis asks how to build such an agent so that it helps without taking decisions it should not take.

### 1.2 STATEMENT OF RESEARCH PROBLEM

There is no disease-independent, auditable method that takes a single pathology report and maintains a personalised, evidence-linked care loop for that patient: naming what is unknown, who must find it out, what each possible answer would change, and when the plan may safely commit.

### 1.3 JUSTIFICATION OF STUDY

1. **Delays and omissions are measurable and costly.** Treatment time, brachytherapy use and missed co-morbidity tests have known links to outcome [5,6,7].
2. **The same structure recurs across diseases.** Staging, fitness, biomarkers, access, response and escalation appear in almost every complex pathology. A shared schema could be reused, with only the rules and evidence swapped.
3. Lorusso D, Xiang Y, Hasegawa K, et al. Pembrolizumab or placebo with chemoradiotherapy followed by pembrolizumab or placebo for newly diagnosed, high-risk, locally advanced cervical cancer (ENGOT-cx11/GOG-3047/KEYNOTE-A18) [overall survival analysis]. Lancet. 2024. doi:10.1016/S0140-6736(24)01808-7. PMID 39288779. † Volume and pages to add. The first (progression-free survival) analysis is doi:10.1016/S0140-6736(24)00317-9.
4. McCormack M, Eminowicz G, Gallardo D, et al. Induction chemotherapy followed by standard chemoradiotherapy versus standard chemoradiotherapy alone in patients with locally advanced cervical cancer (GCIG INTERLACE). Lancet. 2024. doi:10.1016/S0140-6736(24)01438-7. PMID 39419054. † Volume, pages and survival figures to be checked against the paper.

### 1.4 AIM AND OBJECTIVES OF THE STUDY

**Aim.** To specify, demonstrate and plan the evaluation of a closed-loop agentic framework that turns a pathology report into a gated, personalised care workflow, and that transfers across pathologies.

**Objectives.**

1. Define a disease-independent case schema and a five-phase action–observation loop with explicit decision gates.
2. Name the capabilities an agent needs to maintain that loop, and the boundary between agent and clinician for each.
3. Demonstrate the framework on one pseudonymised cervical cancer case.
4. Write protocols for four evaluation studies: retrospective concordance, process timing, cross-pathology reuse, and a prospective late-stage palliative pathway.
5. State falsifiable hypotheses and primary outcomes for each study. doi:10.1016/0360-3016(94)00635-X. PMID 7635769.

### 1.5 SIGNIFICANCE OF THE STUDY

If the hypotheses hold, the framework would give under-resourced hospitals a way to make sure each patient receives every evidence-based option that is locally possible, on time, with the reason for each step recorded. If they fail, the failures will show where agentic tools should not be used in care planning. Both outcomes are useful.

### 1.6 SCOPE OF THE STUDY

In scope: care planning, evidence mapping, gap detection, safety and timing alerts, trial matching, and research-layer mechanistic modelling. Out of scope: diagnosis from images, staging decisions, prescribing, dosing, consent, and the design of new drugs for patient use. Molecular and structural tools appear only as hypothesis generators. The first pathology is cervical squamous cell carcinoma. Two more are chosen in Study 3.

---

# CHAPTER TWO

## 2.0 LITERATURE REVIEW

### 2.1 Where outcome is lost between diagnosis and treatment

Summarise evidence that process failures change survival: treatment prolongation in cervical radiotherapy [5]; brachytherapy omission [6]; staging by FIGO 2018 and the role of imaging [1]; image-guided adaptive brachytherapy outcomes [2]; HIV and cervical cancer [7]; WHO elimination targets [10]. Add the Nigerian and sub-Saharan literature on time to treatment and radiotherapy access (to be compiled. Suggested search: "cervical cancer" AND (Nigeria OR "sub-Saharan Africa") AND (radiotherapy OR brachytherapy) AND (delay OR access)).

### 2.2 Tumour boards and decision support

Multidisciplinary tumour boards as the reference standard. Concordance studies of earlier oncology decision-support systems exist [9]. Published criticisms of such systems (training on one institution's practice, poor fit to other settings, weak outcome validation) need their own sources [CITATION NEEDED: PubMed search "Watson for Oncology" AND (concordance OR validation OR criticism); "clinical decision support" AND oncology AND external validation]. Evidence grading with GRADE [11].

### 2.3 Acting under partial observation

The partially observable Markov decision process as a formal model of acting when the state is hidden [12]. Value of information: an observation is worth ordering when its possible results would change the decision [13]. In the care loop, a test earns its place by the branch of the pathway it can switch.

### 2.4 Language-model agents in medicine

Review current work on language-model agents that use tools, keep state and plan in clinical tasks, and the known failure modes: fabricated citations, overconfidence, recommendations outside the local formulary, and privacy. (To be compiled at submission. Suggested searches: "large language model" AND (agent OR agentic) AND oncology; "tumor board" AND "language model"; "clinical decision support" AND hallucination AND citation.)

### 2.5 Molecular and structural layers

Pathology foundation models for H&E slides [14]. Protein structure prediction [15]. Neoantigen and HLA binding prediction for virus-driven cancers. These layers can suggest targets and trial eligibility, but they do not reach patient care without wet-lab and clinical validation.

### 2.6 Palliative care in late-stage disease

Early integrated palliative care and quality of life [8]. Patient-reported outcome instruments such as EORTC QLQ-C30 as endpoints.

---

# CHAPTER THREE

## 3.0 MATERIALS AND METHODS

### 3.1 Design

A framework specification (3.2–3.5), a capability taxonomy (3.6), and four study protocols (3.7–3.10).

### 3.2 The case as a partially observed state

Let the patient's true state be *x*: disease extent, biology, host fitness, co-morbidities, and local access. The agent never sees *x*. It holds a record of observations *y*₁…*yₙ*, each with a value, a source, a time and an owner. Actions are of two kinds:

- **Information actions** return an observation and leave *x* unchanged (MRI, HIV test, PD-L1 stain).
- **Therapeutic actions** change *x* and are followed by observations of their effect (chemoradiation, then PET-CT).

A pathway is a function from the observation record to a ranked set of next actions, each linked to evidence.

### 3.3 Gates

A gate is a predicate over the observation record that must be true before the pathway may commit to a class of action. For cervical cancer, the gate for choosing definitive treatment requires stage, HIV status, kidney function and performance status, plus brachytherapy access for locally advanced disease. Gates are declared per pathology and can differ by branch. For example, PD-L1 is critical only for metastatic or recurrent disease. A pathway shown before its gate opens must be labelled as a working assumption.

### 3.4 The five-phase loop

| Phase | Loop step | Leaves the phase when |
|---|---|---|
| 1 Characterise | Observe | All critical gates for the likely branch are satisfied |
| 2 Decide | Decide | The tumour board records a decision and consent |
| 3 Treat and monitor | Act | Treatment completes; toxicity and timing alerts handled |
| 4 Evaluate | Observe | Response is measured |
| 5 Follow up or escalate | Update | No evidence of disease is confirmed on schedule, or escalation re-enters Phase 1 |

Derived alerts (for example anaemia before radiotherapy, rising creatinine on cisplatin, treatment time over 56 days) are raised from observations. They are not stored as separate facts.

### 3.5 Case schema and rule set

The schema is disease-independent: specimen, histology, grade, margins, stroma, proliferation, stage, biomarkers, host factors, co-morbidities, access, decision, treatment status, toxicity, timing, response, follow-up. A pathology adds its rule set (gates, pathways, alerts) and its evidence store (trials with populations and effect sizes). The Case Board in `apps/case_board/` stores one case as a single data object so that a second pathology changes data and rules, not the interface.

### 3.6 Agent capabilities

Each capability lists what the agent does and where the human boundary sits.

**Layer A. Intake and state**

1. **Report structuring.** Read pathology, radiology and laboratory text into the schema, with an uncertainty flag per field. *Boundary:* the pathologist's report is the source of truth.
2. **Longitudinal state keeping.** Hold the observation record across weeks, with source, time and owner for each entry.
3. **De-identification and privacy.** Strip identifiers before anything leaves the hospital. Record consent status.

**Layer B. Reasoning under missing information**

4. **Gap detection.** List unknown observations, ranked by how many pathway branches each one switches (value of information).
5. **Staging and classification rules.** Encode FIGO, TNM and WHO classifications as checks. *Boundary:* stage is assigned by clinicians.
6. **Consistency checking.** Flag contradictions, such as a tumour size above 4 cm on MRI recorded with a stage of IB1 or IB2. Biopsy specimen dimensions are not tumour size and are not used for this check. doi:10.1016/j.ijrobp.2013.05.033. PMID 23849695.

**Layer C. Evidence and guidelines**

7. **Multi-guideline reasoning.** Apply NCCN, ESMO and national guidelines side by side, with version dates, and say where they differ. doi:10.1016/S2214-109X(20)30459-9. PMID 33212031. † PubMed lists online publication on 16 Nov 2020; confirm volume and pages.
8. **Evidence appraisal.** Link each option to its trial, population, effect size and applicability, graded [11]. Never cite from memory without verification. doi:10.1056/NEJMoa1000678. PMID 20818875.
9. **Trial matching.** Parse eligibility against the observation record, including geography and travel. doi:10.1093/annonc/mdx781. PMID 29324970.

**Layer D. Safety and delivery**

10. **Pharmacological safety.** Organ-function eligibility, interactions (for example ART with chemotherapy), cumulative dose limits. *Boundary:* dosing is the prescriber's.
11. **Co-morbidity co-management.** HIV, TB, malaria, diabetes and others as they change the plan.
12. **Resource and logistics reasoning.** What the hospital can deliver, cost, referral timing, and scheduling against critical windows.
13. **Monitoring and escalation.** Toxicity and timing alerts, response assessment, and re-entry into the loop.

**Layer E. The person**

14. **Palliative and supportive care.** Symptom burden, goals of care and timely palliative referral, especially for late-stage diagnoses.
15. **Communication.** Plain-language and local-language explanations for patients and families, and summaries for each team member.

**Layer F. Research and self-evaluation**

16. **Mechanistic and molecular modelling.** Transport, PK/PD and ODE models with identifiability gates, as in Theses 11 and 12. Omics, HLA and epitope prediction, and structure retrieval. *Boundary:* hypotheses only, never used for patient dosing.
17. **Audit and calibration.** Log every suggestion with its reason, compare against what the tumour board decided, and track errors. Say "I don't know" when the evidence does not cover the case.

### 3.7 Study 1: retrospective concordance

- **Design.** Retrospective, with ethics approval and a waiver of consent for de-identified records.
- **Sample.** 50 consecutive cervical cancer cases presented to a tumour board at a Nigerian teaching hospital.
- **Procedure.** The agent receives only the information available at the time of the board meeting. Two blinded oncologists compare its pathway with the board's decision.
- **Primary outcome.** Proportion of cases where the agent's first-ranked option matches the board's decision, or the reviewers judge it acceptable.
- **Secondary outcomes.** Critical observations the agent flagged as missing that were in fact missing; unsafe suggestions (any suggestion reviewers rate as potentially harmful); hallucinated evidence.
- **H1 (descriptive pilot).** Report the proportion of cases with acceptable concordance with its 95% Wilson interval, and the number of unsafe suggestions with an upper 95% bound. With n = 50, an observed 40/50 (80%) has an interval of about 67–89%, so this study can show that concordance is compatible with a target but cannot confirm ≥ 80%. A confirmatory design needs about 49 cases for a ±10-point half-width at an expected 85% (normal approximation), and more if the expected rate is lower. "Acceptable" is defined before unblinding. Two blinded reviewers rate each case, agreement is reported as Cohen's kappa, and a third reviewer resolves differences. A baseline comparator (a guideline checklist or a junior clinician) is run on the same cases, because concordance alone does not show added value. Zero unsafe suggestions in 50 cases only bounds the true unsafe rate below about 6–7%.

### 3.8 Study 2: process timing

- **Design.** Process mining of the same records.
- **Outcomes.** Days from biopsy to staging, from staging to treatment start, and overall radiotherapy treatment time; proportion receiving brachytherapy; proportion tested for HIV before treatment.
- **H2.** The agent's alerts would have fired before at least half of the delays over 14 days, at the point where they could have been acted on. This is a retrospective estimate of opportunity, not a demonstrated time saving.

### 3.9 Study 3: cross-pathology reuse

- **Design.** Apply the framework to two more pathologies: one common cancer (for example breast or prostate) and one non-cancer complex pathology (for example sickle cell disease; see Thesis 36).
- **Outcome.** Fraction of schema fields, loop phases and interface components reused unchanged; effort in hours to write each new rule set.
- **H3.** Report the fraction of schema fields, loop phases and interface components reused unchanged, counted by a developer who did not write the first rule set, together with the hours needed for each new rule set. The earlier 70% target is a working threshold chosen by the author and has no empirical basis, so it is not used as a pass or fail line.

### 3.10 Study 4: prospective late-stage pathway

- **Design.** Prospective pilot, after Studies 1–3 and full ethics review, in patients diagnosed at stage IVB or with recurrence.
- **Outcomes.** Days from diagnosis to palliative-care referral; EORTC QLQ-C30 at baseline, 6 and 12 weeks; proportion with a documented goals-of-care conversation.
- **H4 (exploratory).** Earlier palliative referral and better quality-of-life scores than a matched historical cohort. A historical comparison is confounded by calendar time and referral pathway, so this outcome is exploratory and cannot support a claim of benefit.

### 3.11 What will not be done

No autonomous ordering, prescribing or dosing. No use of the molecular layer to choose a patient's treatment. No public release of any case without consent and de-identification.

---

# CHAPTER FOUR

## 4.0 WORKED EXAMPLE (SYNTHETIC CASE S-01)

An earlier draft demonstrated the method on one real pseudonymised report. That material is withheld from this version until the patient's consent is recorded and the treating institution and an ethics committee have agreed. The case below is invented. It exists to specify and inspect the method, and it is available as `apps/case_board/demo.html`.

### 4.1 Input

Cervical biopsy, fragments totalling 1.5 × 1.2 × 0.4 cm: invasive squamous cell carcinoma, non-keratinizing, moderately differentiated; lymphovascular space invasion present; fibrotic stroma; 8 mitoses per 10 high-power fields; tumour present at the edge of the biopsy. Clinical details give a cervical mass of 4.6 cm on MRI (invented values).

### 4.2 Reading errors used as test items

Four common misreadings are seeded on purpose: (1) tumour at the edge of a biopsy is read as residual disease, when a biopsy edge is expected to be involved; (2) the dimensions of the biopsy fragments are read as tumour size and stage, when stage comes from examination, imaging and pathology together and is assigned by clinicians; (3) necrosis or immune infiltrate is read as predicting checkpoint-inhibitor response, when PD-L1 is the tested biomarker; (4) the goal is stated as a guaranteed cure, when it is no evidence of disease after treatment. These are test items chosen by the author, not findings about the agent. [CITATION NEEDED: pathology and guideline sources for items 1–3.]

### 4.3 Gates at intake

Critical and unknown: stage, HIV status, kidney function, performance status, brachytherapy access. Non-critical and unknown: p16, PD-L1, haemoglobin, immunotherapy access, HER2, MMR. A tumour of 4.6 cm on MRI would be stage IB3 or higher only if confirmed by the clinicians, so the pathway is shown as a working assumption (locally advanced disease).

### 4.4 Branches the missing observations control

| Observation | Branch it switches |
|---|---|
| Stage | Surgery vs chemoradiation vs systemic treatment; pembrolizumab label fit |
| Immunotherapy access | KEYNOTE-A18 vs INTERLACE induction |
| Kidney function | Cisplatin vs carboplatin |
| HIV status | ART co-management; tenofovir switch; infection prophylaxis |
| Brachytherapy access | Referral timing to protect the 56-day window |
| p16 | HPV-targeted trial eligibility |

### 4.5 Artefact

The synthetic Case Board (`apps/case_board/demo.html`) implements the five-phase loop, a ranked queue of next actions, derived alerts, an observation log, an escalation pathway, an overall-survival forest plot, a stroma transport profile, and trials matched from ClinicalTrials.gov. Effect sizes on the board are transcribed from published trials and have not been re-checked against the papers.

### 4.6 What the example does not show

It does not show concordance, time saved, an error-detection rate, or any effect on a patient. It is an invented case used to specify the method.

# CHAPTER FIVE

## 5.0 DISCUSSION, CONCLUSION AND RECOMMENDATION

### 5.1 Discussion

The main claim is structural: personalised care for a complex pathology can be written as a gated action–observation loop, and an agent can maintain that loop. The synthetic example shows what the loop would display and which corrections its rules state. It does not show that the loop detects real reading errors, and one invented case cannot support that claim. Whether it improves care is an empirical question for Studies 1–4.

The largest risks are misplaced trust, recommendations that do not fit local resources, fabricated evidence and privacy breaches. The design answers each with a boundary: humans own stage, choice, dose and consent; the rule set encodes local access; every evidence item links to its source; and nothing leaves the hospital without de-identification and consent.

### 5.2 Conclusion

A single pathology report is the start of a loop, not the end of a diagnosis. The framework here specifies that loop, the agent capabilities that sustain it, and how to test whether it helps.

### 5.3 Recommendations

1. Secure a clinical partner and ethics approval for Study 1 before any further public claims.
2. Record consent, and obtain institutional and ethics permission, before any real case is shown publicly.
3. Build the second and third rule sets (Study 3) in parallel with Study 1.
4. Keep the molecular and structural layers in the research tier until they have wet-lab collaborators.

---

## References

1. Bhatla N, Berek JS, Cuello Fredes M, et al. Revised FIGO staging for carcinoma of the cervix uteri. Int J Gynaecol Obstet. 2019;145(1):129–35.
2. Pötter R, Tanderup K, Schmid MP, et al. MRI-guided adaptive brachytherapy in locally advanced cervical cancer (EMBRACE-I): a multicentre prospective cohort study. Lancet Oncol. 2021;22(4):538–47.
3. Lorusso D, Xiang Y, Hasegawa K, et al. Pembrolizumab or placebo with chemoradiotherapy followed by pembrolizumab or placebo for newly diagnosed, high-risk, locally advanced cervical cancer (ENGOT-cx11/GOG-3047/KEYNOTE-A18). Lancet. 2024. †
4. McCormack M, Eminowicz G, Gallardo D, et al. Induction chemotherapy followed by standard chemoradiotherapy versus standard chemoradiotherapy alone in patients with locally advanced cervical cancer (GCIG INTERLACE). Lancet. 2024. †
5. Petereit DG, Sarkaria JN, Chappell R, et al. The adverse effect of treatment prolongation in cervical carcinoma. Int J Radiat Oncol Biol Phys. 1995;32(5):1301–7.
6. Han K, Milosevic M, Fyles A, Pintilie M, Viswanathan AN. Trends in the utilization of brachytherapy in cervical cancer in the United States. Int J Radiat Oncol Biol Phys. 2013;87(1):111–9.
7. Stelzle D, Tanaka LF, Lee KK, et al. Estimates of the global burden of cervical cancer associated with HIV. Lancet Glob Health. 2021;9(2):e161–9.
8. Temel JS, Greer JA, Muzikansky A, et al. Early palliative care for patients with metastatic non-small-cell lung cancer. N Engl J Med. 2010;363(8):733–42.
9. Somashekhar SP, Sepúlveda MJ, Puglielli S, et al. Watson for Oncology and breast cancer treatment recommendations: agreement with an expert multidisciplinary tumor board. Ann Oncol. 2018;29(2):418–23.
10. World Health Organization. Global strategy to accelerate the elimination of cervical cancer as a public health problem. Geneva: WHO; 2020.
11. Guyatt GH, Oxman AD, Vist GE, et al. GRADE: an emerging consensus on rating quality of evidence and strength of recommendations. BMJ. 2008;336(7650):924–6.
12. Kaelbling LP, Littman ML, Cassandra AR. Planning and acting in partially observable stochastic domains. Artif Intell. 1998;101(1–2):99–134.
13. Howard RA. Information value theory. IEEE Trans Syst Sci Cybern. 1966;2(1):22–6.
14. Chen RJ, Ding T, Lu MY, et al. Towards a general-purpose foundation model for computational pathology. Nat Med. 2024;30(3):850–62.
15. Jumper J, Evans R, Pritzel A, et al. Highly accurate protein structure prediction with AlphaFold. Nature. 2021;596(7873):583–9.

**Series references.** T11 desmoplastic transport identifiability; T19 forcing admission gates; T20 occult modes under a partial liquid-biopsy observer; T22 observation-channel profile composition; T31 NSTG CaseCards as forcing-admission predicates; T36 sickle cell disease hydroxyurea review. All at https://github.com/cloudynirvana.

---

Research only. Not a medical device, not clinical decision support in use, not a dose, and not a cure.
