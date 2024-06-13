---
subcategory: "Cockpit"
page_title: "Scaleway: scaleway_cockpit_source"
---

# Resource: scaleway_cockpit_source

The `scaleway_cockpit_source` resource allows you to create and manage [data sources](https://www.scaleway.com/en/docs/observability/cockpit/concepts/#data-sources) in Cockpit.

Refer to Cockpit's [product documentation](https://www.scaleway.com/en/docs/observability/cockpit/concepts/) and [API documentation](https://www.scaleway.com/en/developers/api/cockpit/regional-api) for more information.

## Create a data source

The following command shows you how to create a [metrics](https://www.scaleway.com/en/docs/observability/cockpit/concepts/#metric) data source named `my-data-source` in a given Project.

```terraform
resource "scaleway_account_project" "project" {
    name = "test project data source"
}

resource "scaleway_cockpit_source" "main" {
    project_id = scaleway_account_project.project.id
    name       = "my-data-source"
    type       = "metrics"
}
```

## Arguments reference

- `name` - (Required) The name of the data source.
- `type` - (Required) The [type](https://www.scaleway.com/en/docs/observability/cockpit/concepts/#data-types) of data source. Possible values are: `metrics`, `logs`, or `traces`.
- `region` - (Defaults to the region specified in the [provider's configuration](../index.md#region)) The [region](../guides/regions_and_zones.md#regions) where the data source is located.
- `project_id` - (Defaults to the Project ID specified in the [provider's configuration](../index.md#project_id)) The ID of the Project the data source is associated with.

## Attributes reference

This section lists the attributes that are automatically exported when the `cockpit_source` resource is created:

- `id` - The ID of the data source.

~> **Important:** Data sources' IDs are [regional](../guides/regions_and_zones.md#resource-ids), which means they include the region, in the format `{region}/{id}`. For example, if your data source is located in the `fr-par` region, its ID would look like the following: `fr-par/11111111-1111-1111-1111-111111111111`.

- `url` - The URL of the data source.
- `origin` - The origin of the data source.
- `synchronized_with_grafana` - Indicates whether the data source is synchronized with Grafana.
- `created_at` - The date and time the data source was created (in RFC 3339 format).
- `updated_at` - The date and time the data source was last updated (in RFC 3339 format).

## Import

This section explains how to import data sources using the ID of the region they are located in the `{region}/{id}` format.

```bash
$ terraform import scaleway_cockpit_source.main fr-par/11111111-1111-1111-1111-111111111111
```
