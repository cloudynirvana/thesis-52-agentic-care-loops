# Privacy and consent

## Rules for this repository

1. No real patient report, image, identifier, date of service, hospital name or record number is committed, in any branch that is public or deployed. Case boards published from this repository use synthetic cases only.
2. A real case may be used only when all of these are recorded: the patient's (or legal representative's) informed consent, permission from the treating institution, and approval or a documented waiver from a research ethics committee.
3. Reviewers and data contributors must not paste patient information into issues, pull requests or comments. Issues that contain it will be closed and edited.
4. Datasets offered for validation must arrive with their ethics approval and data-use terms. Use the **Data offer** issue form to describe a dataset without attaching it.

## What to do if patient content was committed

Removing a file in a later commit does not remove it from history. If real patient content was ever committed to a branch, treat that branch as sensitive: keep the repository private, do not make the branch public, and rewrite or delete the branch history before any wider sharing. Deleted deployments and cached previews should be removed too.

## Deployment

The public demo is served from `apps/case_board` and contains only synthetic data. See `apps/case_board/DEPLOY.md`.
