# gha-create-branches

This GitHub Action to be used to automatically create new branches and related and/or dependent repos when triggered.

To limit this workflow from running, it is recommended to only trigger it on `create` or `pull_request`. However, there is logic in place to check if the branch already exists in the other repo and will skip it.

Be mindful that the `dmsi-io/gha-create-branches` action will create a branch from the default branch on the other repos and if you would like to branch from a different branch it is recommended to do that manually instead.

### Usage

```yaml
name: Create Branches

on:
  - create

jobs:
  create-branches:
    runs-on: ubuntu-latest
    name: Create branch on ${{ matrix.repo }}
    strategy:
      matrix:
        # Add all repos that this repo depends on to run in kubernetes
        repo: ['k8s-ingress', 'k8s-redis']
    steps:
      - name: Create Branches
        uses: dmsi-io/gha-create-branches@main
        with:
          repo: ${{ matrix.repo }}
          token: ${{ secrets.GHA_ACCESS_TOKEN }}
```
