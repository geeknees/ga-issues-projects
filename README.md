# Add issue to project

A javascript github action to add an issue to the first project on the repository.

> **NOTE:** ⚠️ If you are using GitHub projects (classic), use the older version [v0.1](https://github.com/geeknees/ga-issues-projects/tree/v0.1).

# Usage

```yaml
name: 'Add new issue to project board'

on:
  issues:
    types:
    - opened

jobs:
  add_to_project:
    runs-on: ubuntu-latest
    steps:
    - uses: geeknees/ga-issues-projects@master
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        repository: ${{ github.repository }}
        issue: ${{ github.event.issue.number }}
        issue_project_ids: list_of_project_ids # Enter project IDs separated by commas

```

## To get issue_project_ids

https://developer.github.com/v4/explorer/


```graphql
{
  user(login: "username") {
    projectsV2(first: 100) {
      edges {
        node {
          id
          title
          closed
        }
      }
    }
  }
}
```

```graphql
{
  organization(login: "organization") {
    projectsV2(first: 100) {
      edges {
        node {
          id
          title
          closed
        }
      }
    }
  }
}
```


## To create card with private project


1. [Create a personal access token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line)
1. [Create a secret containing the personal access token, call it GITHUB_ACTION](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets)
1. Change the repo-token in the workflow.yml to reference your new token name:

```
        github_token: ${{ secrets.GITHUB_ACTION }}
```
