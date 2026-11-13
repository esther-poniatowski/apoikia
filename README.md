# apoikia

Generic materials for administering GitHub organizations: templates, reusable workflows, and the
schema of the values that differ from one organization to the next. Each organization derives its
own instances from apoikia and keeps its specific values in its own private repository.

## Distribution to an organization

An artifact of apoikia reaches an organization through one of three channels, fixed by GitHub
for each kind of artifact:

| Channel | Artifacts | Location in apoikia |
|---|---|---|
| Called in place | Reusable workflows | `.github/workflows/` |
| Rendered into a repository of the organization | `.github` repository: profile, contribution guidelines, commit message template, issue forms, workflow templates | `copier.yml`, `templates/` |
| Applied through the GitHub API | Settings, Actions policy, teams, labels | `schemas/org.schema.json` |

The [channels](docs/channels.md) note states why each artifact takes its channel, and the
[adoption procedure](docs/adopt-an-organization.md) derives the instances of a new organization.

## Layout

```text
.
├── .github/workflows/      # reusable workflows, called by the repositories of each organization
├── copier.yml              # questions shared by every template; selects the template to render
├── templates/
│   └── org-github/         # public `.github` repository of an organization
├── schemas/
│   └── org.schema.json     # values specific to one organization
├── examples/
│   └── org.example.yml     # organization profile validated by the schema
├── docs/                   # design and procedures
└── TODO.md                 # planned components
```

## Requirements

Rendering and validation run in the conda environment `apoikia`, which provides
[Copier](https://copier.readthedocs.io/) (9.4 or later) and
[check-jsonschema](https://check-jsonschema.readthedocs.io/).
