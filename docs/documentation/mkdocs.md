# MkDocs
[MkDocs](https://www.mkdocs.org/getting-started/) is a python project to quickly
build a documentation website using markdown file.

## Deploying mkdocs

### Deploy to Github Pages

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
