---
title: Create / Import
description: Create Documentation for Centurion Role Git.
date: 2025-12-26
template: project.html
about: https://github.com/nofusscomputing/centurion_role_git
---

This section contains documentation for repository tasks.


## Create Repository

| Ansible Tag | Action | Check Mode Supported | Required<br>Variables | Description |
| :---:|:---|:---:|:---:|:---|
| `gitea` | - | - |  - | Ensures that Gitea related tasks run. **Mandatory for Gitea**|
| | Create Organisation<br>Repository | Yes | `git_gitea_create_repo_org` | Creates a git repository |
| | Migrate Repository | Yes | `git_gitea_repo_migrate` | Imports a git repository |
| _No Tags_ | - | - | - | If no tags are specified, then no task will run. |

Create task enables the creation of a git repository. This includes importing a repository. The Tasks are smart enough to determine between a user and an organization repository.


## Variables

Variables for each task are a mapping of the required keys that form the body of the API request. The mappings for each task are as defined in the table above.


### Create Organisation Repository

To obtain the keys and values for mapping `git_gitea_create_repo_org`, navigate to your local gitea's swagger docs for endpoint `/repos/{owner}/{repo}`.


### Create User Repository

Not yet supported.


### Migrate repository

To obtain the keys and values for mapping `git_gitea_repo_migrate`, navigate to your local gitea's swagger docs for endpoint `/repos/migrate`.


## Workflow

The create task follows the following workflow.

``` mermaid

flowchart LR


    START(create)

        START --> FETCH_USER


    subgraph Repository

    FETCH_USER[Fetch Authenticated User]

        FETCH_USER --> USER_MATCH


        USER_MATCH{user=-repo_name-}

            USER_MATCH -->| yes | REPO_TYPE_USER

            USER_MATCH -->| no | REPO_TYPE_ORG


        REPO_TYPE_USER[repo_type = user]

            REPO_TYPE_USER --> REPO


        REPO_TYPE_ORG[repo_type = oganisation]

            REPO_TYPE_ORG --> REPO



    REPO[Fetch Repositories]

        REPO --> REPO_EXISTS


        REPO_EXISTS{exists}

            REPO_EXISTS -->| yes | FETCH_REPO

            REPO_EXISTS -->| no | CREATE_REPO


        FETCH_REPO[Fetch Repository]

            FETCH_REPO --> CREATE_REPO_AGGREGATE_CONFIG


    CREATE_REPO[Create Repo]

        CREATE_REPO --> CREATE_REPO_AGGREGATE_CONFIG

    CREATE_REPO_AGGREGATE_CONFIG[Build Config from returned data]


    end

    CREATE_REPO_AGGREGATE_CONFIG --> FINISH

    FINISH[Finished]

```
