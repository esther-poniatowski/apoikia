---
index: "[[_index]]"
---

# Adopting an organization

The procedure derives the instances of an organization from apoikia. The commands run in the conda
environment `apoikia`, from a folder holding clones of the repositories of the organization.

## 1. Declare the organization profile

Create a private administration repository in the organization, and write its `org.yml` from
[org.example.yml](../examples/org.example.yml). Validate it against the schema:

```bash
check-jsonschema --schemafile <apoikia>/schemas/org.schema.json org-admin/org.yml
```

## 2. Render the `.github` repository

Clone the `.github` repository of the organization (create it as a public repository if absent),
then render the template into the clone:

```bash
copier copy --data-file org-admin/org.yml --data template=org-github gh:esther-poniatowski/apoikia .github
```

An existing `profile/README.md` is kept. For any other file that already exists, Copier asks before
overwriting it. Review the diff in the clone, then commit and push it.

## 3. Allow the reusable workflows

When the Actions policy of the organization restricts actions, add the pattern of apoikia to the
allowed patterns (Organization settings → Actions → General). The pattern is declared in
`actions.patterns_allowed` of `org.yml`.

## 4. Apply the settings

The script applying `settings`, `actions`, `teams` and `labels` through the API is not written yet
(see [TODO](../TODO.md)). Until then, apply them by hand from `org.yml`.

## Updating an organization

After a change in apoikia, merge it into the rendered copy from the clone of `.github`:

```bash
copier update --data-file ../org-admin/org.yml
```
