---
index: "[[_index]]"
---

# Distribution channels

GitHub fixes where each kind of artifact must live for an organization to use it. Therefore, the
location of an artifact decides whether the organization can use the copy in apoikia, needs a
rendered copy of its own, or receives the artifact as settings.

## Called in place

A reusable workflow stays in apoikia. A repository of any organization calls it by path and
reference: `<owner>/apoikia/.github/workflows/python-ci.yml@<tag>`. Two conditions apply:

- apoikia must be public, since a workflow in a private repository can only be called by
  repositories of the same owner;
- the Actions policy of the calling organization must allow public reusable workflows, or list
  apoikia among its selected patterns (`actions.patterns_allowed` in the organization profile).

Each caller pins a tag or a commit, so that a change in apoikia reaches an organization only when
the organization moves its reference.

## Rendered into a repository of the organization

GitHub reads the defaults of an organization only from its own public `.github` repository: issue
forms in `.github/ISSUE_TEMPLATE/`, workflow templates in `workflow-templates/`, the profile in
`profile/README.md`, and the contribution guidelines. No mechanism lets these files point to
another account, so apoikia holds templates and each organization holds a rendered copy.

Copier renders the copy from the values of the organization profile, and records the source
commit in `.copier-answers.yml`. A later `copier update` merges the changes of apoikia into the copy
without discarding the changes made by the organization. The files listed in `_skip_if_exists`
(the profile) belong to the organization after the first rendering, and updates never touch them.

## Applied through the GitHub API

Organization settings, the Actions policy, teams and labels are not files. The organization
profile declares them, under the schema [org.schema.json](../schemas/org.schema.json), and a script
applies them through the API.

## Values specific to one organization

apoikia holds no value specific to one organization. Each organization declares its values once,
in the file `org.yml` of its private administration repository. The same file answers the
questions of Copier and declares the settings applied through the API.
