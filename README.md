# .github
Shared config and templates.

For details on org shared templates, see: [documentation](https://docs.github.com/en/actions/learn-github-actions/sharing-workflows-with-your-organization).

## Layout

- `.github/workflows/` — reusable workflows (`on: workflow_call`) that fog gems
  call cross-repo.
- `workflow-templates/` — starter workflows offered in the org's "New workflow"
  picker. They call the reusable workflows above at a pinned tag.
- `config/dependabot.yml` — reference Dependabot config to copy into a gem.

## Conventions

Third-party actions are pinned to a full commit SHA with the version in a
trailing comment, e.g.

```yaml
- uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1 # v7.0.1
```

A tag or branch ref can be moved to point at different code; a SHA cannot.
Dependabot understands this form and updates the SHA and the comment together.

## Releasing

Callers pin to a tag, so changes to `.github/workflows/` do not reach fog gems
until a new tag is cut. After merging:

1. Tag the merge commit (`vX.Y.0`) and push the tag.
2. Bump the `@vX.Y.0` refs in `workflow-templates/` to match.

Repos that already use the shared workflows get the bump from Dependabot.
