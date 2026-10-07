# Getting a DOI: ORCID, then Zenodo

Do these in order. ORCID first, because the Zenodo record should carry it.

---

## 1. ORCID (about 5 minutes, no prerequisites)

1. Register at **https://orcid.org/register** with your own email.
2. Add: name, country (Nigeria), education (Nile University of Nigeria, B.Sc. Biotechnology,
   2022), and current activity.
3. Set the visibility of your record to **Everyone**, so publishers and Zenodo can read it.
4. Copy your iD. It looks like `https://orcid.org/0000-0002-1825-0097`.
5. Put it in `CITATION.cff`, replacing the commented placeholder under `authors`:

   ```yaml
   authors:
     - family-names: Ogbonna
       given-names: Kelechi Emeka
       email: kelechiogbonna300@gmail.com
       alias: cloudynirvana
       orcid: "https://orcid.org/0000-0000-0000-0000"
   ```

   Keep the full `https://orcid.org/...` form; that is what the CFF schema expects.

ORCID is yours for life and is independent of any repository or employer. Put it on every
preprint, paper and conference abstract from now on.

---

## 2. Zenodo (about 10 minutes, needs a public GitHub repository)

**Zenodo's GitHub integration only archives public repositories.** That is why this thesis lives
in its own repository rather than in `confluence-evidence`, which is private and must stay that
way.

### Steps

1. Sign in at **https://zenodo.org** using **Log in with GitHub**. This authorises Zenodo to see
   your repositories.
2. Go to your Zenodo account → **GitHub** (`https://zenodo.org/account/settings/github/`).
3. Find `thesis-52-agentic-care-loops` in the list and switch its toggle **ON**.
   - If it is missing, click **Sync now**, and confirm the repository is public.
   - The toggle must be on **before** you create the release. Zenodo only archives releases made
     after it starts watching.
4. On GitHub, go to the repository → **Releases** → **Create a new release**:
   - **Tag:** `v1.0.0`
   - **Title:** `Thesis #52 v1.0.0 — protocol-stage deposit`
   - **Description:** state plainly what this version is. Suggested text:

     > Protocol-stage deposit. Framework specified and demonstrated on one invented (synthetic)
     > cervical cancer case. No outcome data; the four evaluation studies have not been run.
     > References 3–9 verified against PubMed; references 1–2 and 10–15 unverified. Claim-level
     > verification status in `docs/claims_ledger.csv`. Research only — not a medical device.

   - Publish the release.
5. Within a few minutes Zenodo creates the record and mints **two DOIs**:
   - a **concept DOI** that always resolves to the newest version — cite this one normally;
   - a **version DOI** for `v1.0.0` specifically — cite this when you need the exact snapshot.
6. Open the Zenodo record and check its metadata, because the auto-filled version is usually
   thin:
   - **Resource type:** choose *Publication → Thesis* (Zenodo often guesses *Software*).
   - **Authors:** confirm your name and attach your **ORCID iD**.
   - **Description:** paste the abstract from `CITATION.cff`.
   - **Keywords:** copy them from `CITATION.cff`.
   - **Licence:** MIT.
   - **Additional notes:** add the status sentence — protocol stage, synthetic example only, no
     outcome data.
7. Put the concept DOI back into the repository:
   - uncomment and fill the `identifiers` block in `CITATION.cff`;
   - add the DOI to the citation line in `README.md`;
   - optionally add the Zenodo DOI badge to the top of `README.md`:

     ```markdown
     [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)
     ```
8. Commit those edits. For later revisions, tag `v1.1.0` and so on; Zenodo archives each release
   automatically and the concept DOI follows the newest one.

### Before you publish the release

- [ ] The repository is public and contains **no real patient content in any branch** — this one
      was built clean from its first commit, so this holds as long as nothing is added.
- [ ] `docs/PRIVACY_AND_CONSENT.md` is present.
- [ ] `DISCLAIMER.md` is present and the README states the protocol-stage status.
- [ ] The AI-use disclosure in `THESIS.md` names the tools accurately.
- [ ] You accept that a Zenodo DOI is **permanent**. Zenodo is a preservation archive, and
      records are not meant to be withdrawn. Publish only what you are willing to have cited
      and read indefinitely.

---

## 3. After the DOI exists

1. **Add it to the hub.** Update the Thesis #52 row in
   [`research-theses-hub`](https://github.com/cloudynirvana/research-theses-hub) with the DOI.
2. **Claim it on ORCID.** On your ORCID record, use *Add works → Search & link → DataCite* and
   search your name or the DOI; the Zenodo deposit will appear and link in one click.
3. **Google Scholar** indexes Zenodo records, so the thesis becomes discoverable without any
   further action. Set up a Scholar profile and confirm it after a few weeks.
4. **Then ask for review.** With a DOI, the deposit is citable, and the request you send to an
   expert is concrete: *"Here is a protocol with a claims ledger; where is it wrong?"* See
   `docs/EXPERT_REVIEW.md`.

## 4. What a DOI does and does not do

A DOI makes the work **citable, permanent and discoverable**. It does **not** mean the work was
peer reviewed, validated, or accepted anywhere. Do not describe a Zenodo deposit as a
publication. The honest description is: *a citable research deposit with a DOI*.

Peer review comes next, and the routes are separate: a preprint server such as AfricArXiv or
medRxiv, community review through PREreview, then a journal.
