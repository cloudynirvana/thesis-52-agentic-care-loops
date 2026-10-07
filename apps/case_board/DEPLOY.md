# Deploying the synthetic case board on Vercel

The site is static HTML with no build step and contains only a **synthetic** case.

1. In Vercel: **Add New → Project → Import** `cloudynirvana/confluence-evidence`.
2. **Root Directory:** `apps/case_board` (the repo root has Python files, which make Vercel try a Python build and fail).
3. **Framework Preset:** Other. Leave Build Command and Output Directory empty.
4. **Production Branch:** `main`. `vercel.json` skips builds for every other branch (`ignoreCommand`), so branch previews do not publish work in progress.
5. Deploy.

Routes: `/` lists the case, `/demo` is the synthetic board. Pages are marked `noindex`.

## Before you turn off Deployment Protection

Turning protection off applies to the whole Vercel project, including old preview deployments. Earlier previews of this repository (for example from the `claude/amazing-bardeen-lyymm1` branch) served boards built from real patient reports.

- Delete those deployments in Vercel, or use a **new Vercel project** for the public demo and leave the old one protected.
- Do not make the old branch public. See `docs/PRIVACY_AND_CONSENT.md`.
- Only after that, decide whether the demo needs sign-in protection at all.
