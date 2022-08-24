# GitHub action workflows for 42 organisation.

**Example usage**
```yaml
name: Call maven test workflow

# Specify your own triggers!
on:
  pull_request:
    branches:
      - main

# Trigger the workflows from this repo
jobs:
  call-workflow:
    uses: 42BV/42-github-workflows/.github/workflows/maven-test.yml
    with:
      java-version: 11
```
