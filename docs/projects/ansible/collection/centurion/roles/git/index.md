---
title: Centurion Role Git
description: No Fuss Computings Centurion Role for Git Operations.
date: 2025-12-26
template: project.html
about: https://github.com/nofusscomputing/centurion_role_git
---

<span style="text-align: center;">

![Endpoint Badge](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Fnofusscomputing%2Fcenturion_role_git%2Frefs%2Fheads%2Fdevelopment%2F.centurion%2Fproject_status.json)

</span>

A [Centurion ERP Role](../../../../../centurion_erp/index.md) for Git Operations.


## Features / TOC

- [Create / Import a Repository](./create.md)


## Variables

There are variables, both ansible and environmental; That are common to **all** tasks within this role. The common variables are:

| Name | Type | Required | Default<br>Value | Description |
|:---|:---:|:---:|:---:|:---|
| git_repo_clone_addr | `string` | `import_only` | _Not Set_ | The address of the repository to import/migrate. |
| git_repo_default_branch | `string` | `No` | `development` | The branch to use as the repositories default branch. |
| git_repo_description | `string` | `No` | _Not Set_ | The repositories description. |
| git_repo_name | `string` | `Yes` | _Not Set_ | The name of the repository. |
| git_repo_owner | `string` | `Yes` | _Not Set_ | The owner of the repository. either be the user or the organisation name. |
| git_repo_private | `boolean` | `No` | `true` | Is this repository to be marked/set as a private repository. |

Additionally the following environmental variables are available:

- `GIT_API_URL` **Required** _The url to the Git API endpoint. i.e. `https://your-gitea.com/api/v1`_

- `GIT_API_TOKEN` **Required** _The api token that has `repository: write`, `organization: write` and `user: read`_

- `GIT_API_VALIDATE_CERT` **Optional** defaults to `true` Should the API request validate the ssl certificate.

