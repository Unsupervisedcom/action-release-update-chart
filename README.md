<!-- start title -->

# GitHub Action:Hello World

<!-- end title -->
<!-- start description -->

Greet someone

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: Unsupervisedcom/action-composite-action-template@undefined
  with:
    # Who to greet
    # Default: World
    who-to-greet: ""
```

<!-- end usage -->
   <!-- start inputs -->

| **Input**          | **Description** | **Default** | **Required** |
| :----------------- | :-------------- | :---------: | :----------: |
| **`who-to-greet`** | Who to greet    |   `World`   |   **true**   |

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
      - 'eventstreamapis/**'
      - 'server/**'
      - 'buf.gen.yaml'
      - 'buf.work.yaml'
      - Dockerfile
      - 'go.mod'
      - 'go.sum'
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
