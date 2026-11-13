# TODO

## Before publication

- Choose the licenses: one for code and templates (for example MIT), one for slides and documents
  (for example CC BY 4.0).
- Tag a first release; the organization profiles then pin `apoikia_ref` to that tag instead of
  `main`.

## Templates

- `meetings`: issue forms for the agenda and the minutes of a meeting, rendered into the private
  meetings repository of an organization.
- `org-admin`: skeleton of the private administration repository (`org.yml`, plans, decisions).
- A template Project (fields and views for meetings and action items), copied into each
  organization with `gh project copy`.

## Scripts

- Apply `settings`, `actions`, `teams` and `labels` of `org.yml` through the GitHub API.
- Validate the organization profiles and render every template in CI.

## Workflows

- Conda variant of the reusable Python workflow, for repositories declaring `environment.yml`.

## Training

- Move the presentations on programming practices from techne; the Overleaf presentation needs the
  agreement of its co-author before publication.
