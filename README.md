<!-- start title -->

# GitHub Action:Release and Update Chart

<!-- end title -->
<!-- start description -->

This action is intended to run on PR merge. It performs a semantic-release, then creates a PR into a helm chart repository with an updated appVersion, using the same PR title and body as the PR that triggered the workflow

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: Unsupervisedcom/action-release-update-chart@undefined
  with:
    # Github token to use, this should be a PAT so that it can trigger workflows on
    # the destination helm repository
    token: ""

    # semantic-release release configuration to use
    # Default: @unsupervised/release-config-general
    release-config: ""

    # The helm chart git repo to update
    # Default: ${{ github.repository_owner }}/chart-${{ github.event.repository.name }}
    helm-repo: ""

    # The helm chart git repo to branch from and PR into
    # Default: alpha
    helm-repo-branch: ""

    # The path to the helm chart in the helm git repo
    # Default: chart
    path-to-chart: ""

    # Labels to apply to the PR. Should be a comma separated string
    # Default: automerge
    labels: ""

    # Delete PR branch after merge
    # Default: true
    delete-branch: ""

    # The prefix for the name of the feature branch
    # Default: automated-code-release-
    branch-prefix: ""
```

<!-- end usage -->
   <!-- start inputs -->

| **Input**              | **Description**                                                                                               |                                **Default**                                 | **Required** |
| :--------------------- | :------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------: | :----------: |
| **`token`**            | Github token to use, this should be a PAT so that it can trigger workflows on the destination helm repository |                                                                            |   **true**   |
| **`release-config`**   | semantic-release release configuration to use                                                                 |                   `@unsupervised/release-config-general`                   |  **false**   |
| **`helm-repo`**        | The helm chart git repo to update                                                                             | `${{ github.repository_owner }}/chart-${{ github.event.repository.name }}` |  **false**   |
| **`helm-repo-branch`** | The helm chart git repo to branch from and PR into                                                            |                                  `alpha`                                   |  **false**   |
| **`path-to-chart`**    | The path to the helm chart in the helm git repo                                                               |                                  `chart`                                   |  **false**   |
| **`labels`**           | Labels to apply to the PR. Should be a comma separated string                                                 |                                `automerge`                                 |  **false**   |
| **`delete-branch`**    | Delete PR branch after merge                                                                                  |                                   `true`                                   |  **false**   |
| **`branch-prefix`**    | The prefix for the name of the feature branch                                                                 |                         `automated-code-release-`                          |  **false**   |

<!-- end inputs -->
   <!-- start outputs -->

| **Output**      | **Description** | **Default** | **Required** |
| :-------------- | :-------------- | ----------- | ------------ |
| `random-number` | Random number   |             |              |

<!-- end outputs -->
   <!-- start examples -->

### Example usage

```yaml
name: Release
on:
  pull_request:
    types:
      - closed
    branches:
      - main
    paths:
      - "eventstreamapis/**"
      - "server/**"
      - "buf.gen.yaml"
      - "buf.work.yaml"
      - Dockerfile
      - "go.mod"
      - "go.sum"
jobs:
  release:
    if: github.event.pull_request.merged == true
    name: Release and update helm chart
    runs-on: ubuntu-latest
    steps:
      - uses: Unsupervisedcom/action-release-update-chart@v1
        with:
          token: ${{ secrets.DEPLOYER_CI_TOKEN }}
```

<!-- end examples -->
<!-- start [.github/ghdocs/examples/] -->
<!-- end [.github/ghdocs/examples/] -->
