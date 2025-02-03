# .github
Shared config and templates.

For details on org shared templates, see: [documentation](https://docs.github.com/en/actions/learn-github-actions/sharing-workflows-with-your-organization).

## Gem release

To release a gem, use the following workflow

```
name: Release

on:
  push:
    # Pattern matched against refs/tags
    tags:
      - '**'

jobs:
  release:
    name: Release gem
    uses: fog/.github/.github/workflows/ci.yml@v1.5.0
    with:
      allowed_owner: MY_USERNAME
    secrets:
      api_key: ${{ secrets.RUBYGEM_API_KEY }}
```
