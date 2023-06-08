---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "vercel_shared_environment_variable Resource - terraform-provider-vercel"
subcategory: ""
description: |-
  Provides a Shared Environment Variable resource.
  A Shared Environment Variable resource defines an Environment Variable that can be shared between multiple Vercel Projects.
  For more detailed information, please see the Vercel documentation https://vercel.com/docs/concepts/projects/environment-variables/shared-environment-variables.
---

# vercel_shared_environment_variable (Resource)

Provides a Shared Environment Variable resource.

A Shared Environment Variable resource defines an Environment Variable that can be shared between multiple Vercel Projects.

For more detailed information, please see the [Vercel documentation](https://vercel.com/docs/concepts/projects/environment-variables/shared-environment-variables).

## Example Usage

```terraform
resource "vercel_project" "example" {
  name = "example"

  git_repository = {
    type = "github"
    repo = "vercel/some-repo"
  }
}

# A shared environment variable that will be created
# and associated with the "example" project.
resource "vercel_shared_environment_variable" "example" {
  key    = "EXAMPLE"
  value  = "some_value"
  target = ["production"]
  project_ids = [
    vercel_project.example.id
  ]
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `key` (String) The name of the Environment Variable.
- `project_ids` (Set of String) The ID of the Vercel project.
- `target` (Set of String) The environments that the Environment Variable should be present on. Valid targets are either `production`, `preview`, or `development`.
- `value` (String, Sensitive) The value of the Environment Variable.

### Optional

- `team_id` (String) The ID of the Vercel team. Shared environment variables require a team.

### Read-Only

- `id` (String) The ID of the Environment Variable.

## Import

Import is supported using the following syntax:

```shell
# You can import via the team_id and environment variable id.
# - team_id can be found in the team `settings` tab in the Vercel UI.
# - environment variable id can be taken from the network tab on the shared environment variable page.
terraform import vercel_shared_environment_variable.example team_xxxxxxxxxxxxxxxxxxxxxxxx/env_yyyyyyyyyyyyy
```