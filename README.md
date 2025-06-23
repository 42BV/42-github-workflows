# GitHub action workflows for 42 organisation.

**Example usage test-workflow**
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

**Example usage release-workflow**
```yaml
# To use the release-workflow, please create a separate file in your .github/workflows-folder (e.g. release.yml).
# In the file, declare the name of the workflow
name: Publish package to the Maven Central Repository

# It is recommended to only ever use the release-workflow, by manual trigger. As such, please declare the following:
on:
  workflow_dispatch:
    # This block determines the variables that can / should be manually set before running the workflow.
    # The variables can be set in GitHub, by opening your project's page, and navigating to Actions.
    # On the left side of the screen, you should see an item with the same name as the name you have given this workflow.
    # Select the item, and click on the "Run workflow"-dropdown. There you will find the text-boxes used to set the variables.
    inputs:
      release-version: 
        required: false # This variable is not required, as the workflow can automatically remove the SNAPSHOT-tag.
        description: Release-version. (not required) # Or whatever floats your boat.
      next-version:
        required: false # Again, not required. The workflow can automatically update the version to the next SNAPSHOT.
        description: Next development-version. (not required)
      java-version:
        required: true # NB. This one is required; however, we set a default. As such, we don't need to change it, as long as it is up-to-date.
        default: '21'
        description: Java-version to use for the deployment.

jobs:
  call-workflow:
  uses: 42BV/42-github-workflows/.github/workflows/maven-release.yml@master
  secrets: inherit # You may want to specify the exact secrets to use. This will work, though.
  with:
    # Passes the values to the template. The workflow is capable of handling empty values.
    release-version: ${{ github.event.inputs.release-version }}
    next-version: ${{ github.event.inputs.next-version }}
    java-version: ${{ github.event.inputs.java-version }}
```
