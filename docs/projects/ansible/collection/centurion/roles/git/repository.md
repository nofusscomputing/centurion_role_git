---
title: Repositories
description: Centurion Role for Git Repository Documentation.
date: 2025-12-26
template: project.html
about: https://github.com/nofusscomputing/centurion_role_git
---

This section contains documentation for repository tasks.


## Create

| Ansible Tag | Action | Description |
| :---:|:---|:---|
| `gitea` | - | Ensures that Gitea related tasks run. **Mandatory for Gitea**|
| | Create Repository | Creates a git repository |
| _No Tags_ |  | If no tags are specified, then no task will run. |

Create task enables the creation of a git repository. The Tasks are smart enough to determine between a user and an organization repository.


### Workflow

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

        CREATE_REPO_AGGREGATE_CONFIG --> REPO_DATA_MATCHES


    REPO_DATA_MATCHES{data matches}

        REPO_DATA_MATCHES -->| no | PATCH_REPO


    PATCH_REPO>Update repo data]



    end

    REPO_DATA_MATCHES -->| yes | FINISH



    FINISH[Finished]

```
