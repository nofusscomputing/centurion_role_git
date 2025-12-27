---
title: Configure
description: Centurion Role for Git Repository Documentation.
date: 2025-12-26
template: project.html
about: https://github.com/nofusscomputing/centurion_role_git
---

This section contains documentation for configuring git repositories. By design, the [create](./create.md) task will run first, as it confirms the repository exists and returns the current repository configuration.


## Configure Repository

| Ansible Tag | Action | Check Mode Supported | Required<br>Variables | Description |
|:---:|:---|:---:|:---:|:---|
| `gitea` | - | - |  - | Ensures that Gitea related tasks run. **Mandatory for Gitea**|
| | Configure a repository | Yes | `git_gitea_config` | Configures a git repository |
| _No Tags_ | - | - | - | If no tags are specified, then no task will run. |

Create task enables the creation of a git repository. This includes importing a repository. The Tasks are smart enough to determine between a user and an organization repository.


## Variables

Variables for each task are a mapping of the required keys that form the body of the API request. The mappings for each task are as defined in the table above.


### Configure a Repository

To obtain the keys and values for mapping `git_gitea_create_repo_org`, navigate to your local gitea's swagger docs for endpoint `PATCH /repos/{owner}/{repo}`.

In addition, the following table lists variables, that if you set will be over-ridden. To set the value of the variable, set the value of the source variable.

| Name | Source<br>Variable |
|:---:|:---:|
| `default_branch` | `git_repo_default_branch` |
| `description` | `git_repo_description` |
| `private` | `git_repo_private` |


## Workflow

The create task follows the following workflow.

``` mermaid

flowchart LR


    START(Start)

        START --> BUILD_CONFIG_DIFF


    subgraph Configuration


        BUILD_CONFIG_DIFF[Build Configuration diff]

            BUILD_CONFIG_DIFF --> CONFIG_MATCHES


        CONFIG_MATCHES{matches}

            CONFIG_MATCHES -->| no | PATCH_CONFIG


        PATCH_CONFIG[Create/Update Config]


    end


    CONFIG_MATCHES -->| yes | FINISH

    PATCH_CONFIG --> FINISH


    FINISH[Finished]

```
