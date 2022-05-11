# MkDocs
[MkDocs](https://www.mkdocs.org/getting-started/) is a python project to quickly
build a documentation website using markdown file.

## Deploying mkdocs

### Deploy to Github Pages using Github actions

To deploy MkDocs project to [Github Pages](https://pages.github.com/)
we can follow the steps below:

- create a workflow.yml file inside .github/workflows/ directory
``` bash title="bash script"
touch .github/workflows/workflow.yml
```
- define the workflow base on the template below
``` yaml  title="workflow.yml"
name: workflow 
on:
  push:
    branches:
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: 3.x
      - run: pip install mkdocs
      - run: mkdocs gh-deploy --force
```

### Troubleshoot

#### Github actions permission denied

There are 2 known solutions to solve this issue:

1. Set 
[actions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository) 
permission in the repository settings to read and write
2. Create a personal access 
[token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) 
which will be stored as repository or environment 
[secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)
then pass it to actions/checkout@v3
``` yaml title="workflow.yml" hl_lines="10-12"
name: workflow 
on:
  push:
    branches:
      - main
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
            token: ${{ secrets.PAT }}
      - uses: actions/setup-python@v2
        with:
          python-version: 3.x
      - run: pip install mkdocs
      - run: mkdocs gh-deploy --force
```
