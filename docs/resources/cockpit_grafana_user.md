---
subcategory: "Cockpit"
page_title: "Scaleway: scaleway_cockpit_grafana_user"
---

# Resource: scaleway_cockpit_grafana_user

The `scaleway_cockpit_grafana_user` resource allows you to create and manage [Grafana users](https://www.scaleway.com/en/docs/observability/cockpit/concepts/#grafana-users) in Scaleway Cockpit.

Refer to Cockpit's [product documentation](https://www.scaleway.com/en/docs/observability/cockpit/concepts/) and [API documentation](https://www.scaleway.com/en/developers/api/cockpit/regional-api) for more information.

## Create a Grafana user

The following command shows you how to create a Grafana user within a specific Scaleway Project.

```terraform
resource "scaleway_account_project" "project" {
  name = "test project grafana user"
}

resource "scaleway_cockpit_grafana_user" "main" {
  project_id = scaleway_account_project.project.id
  login = "my-awesome-user"
  role = "editor"
}
```


## Arguments reference

- `login` - (Required) The username of the Grafana user. The `admin` user is not yet available for creation. You need your Grafana username to log in to your Grafana dashboard.
- `role` - (Required) The role assigned to the Grafana user. Must be `editor` or `viewer`.
- `project_id` - (Defaults to Project ID speficied in the [provider's configuration](../index.md#project_id)) The ID of the Project the Cockpit is associated with.

## Attributes reference

This section lists the attributes that are automatically exported when the `cockpit_grafana_user` resource is created:

- `password` - The password of the Grafana user.

## Import

This section explains how to import Grafana users using the ID of the Project associated with Cockpit, and the Grafana user ID in the format `{project_id}/{grafana_user_id}`.

```bash
$ terraform import scaleway_cockpit_grafana_user.main 11111111-1111-1111-1111-111111111111/2
```
