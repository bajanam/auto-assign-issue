# GitHub action that auto-assigns issues to users

## Inputs

| Parameter       | Required | Description                                                                                             |
| --------------- | -------- | ------------------------------------------------------------------------------------------------------- |
| `assignees`     | true     | Comma separated list of user names. Issue will be assigned to those users.                              |
| `numOfAssignee` | false    | Number of assignees that will be randomly picked from `assignees`. If not specified, assigns all users. |

## Example usage

Here's an example flow that auto-assigns all new issues to two users randomly chosen from `octocat`, `cat` and `dog` :

```yml
name: Issue assignment

on:
    issues:
        types: [opened]

jobs:
    auto-assign:
        runs-on: ubuntu-latest
        steps:
            - name: 'Auto-assign issue'
              uses: pozil/auto-assign-issue@v1
              with:
                  assignees: octocat,cat,dog
                  numOfAssignee: 2
```

### Specifying a dynamic user

Instead of hardcoding the user name in the workflow, you can use a secret:

-   create a GitHub secret named `DEFAULT_ISSUE_ASSIGNEE` with the name of the user
-   use this value `${{ secrets.DEFAULT_ISSUE_ASSIGNEE }}` instead of the username in the workflow.
