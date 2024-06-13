---
subcategory: "Block"
page_title: "Scaleway: scaleway_block_volume"
---

# Resource: scaleway_block_volume

The `scaleway_block_volume` resource is used to create and manage Scaleway Block Storage volumes.

Refer to the Block Storage [product documentation](https://www.scaleway.com/en/docs/storage/block/) and [API documentation](https://www.scaleway.com/en/developers/api/block/) for more information.

## Create a Block Storage volume

The following command shows you how to create a Block Storage volume of 20 GB with the desired [IOPS](https://www.scaleway.com/en/docs/storage/block/concepts/#iops).

```terraform
resource "scaleway_block_volume" "block_volume" {
    iops       = 5000
    name       = "some-volume-name"
    size_in_gb = 20
}
```

## Arguments reference

This section lists the arguments that can be provided to the `scaleway_block_volume` resource:

- `iops` - (Required) The maximum [IOPs](https://www.scaleway.com/en/docs/storage/block/concepts/#iops) expected, must match available options.
- `name` - (Optional) The name of the volume. If not provided, a name will be randomly generated.
- `size_in_gb` - (Optional) The size of the volume in gigabytes. Only one of `size_in_gb`, and `snapshot_id` should be specified.
- `snapshot_id` - (Optional) If set, the new volume will be created from this snapshot. Only one of `size_in_gb`, `snapshot_id` should be specified.
- `tags` - (Optional) A list of tags to apply to the volume.
- `zone` - (Defaults to the zone specified in the [provider's configuration](../index.md#zone)). The [zone](../guides/regions_and_zones.md#zones) in which the volume should be created.
- `project_id` - (Defaults to the Project ID specified in the [provider's configurqtion](../index.md#project_id)). The ID of the Project the volume is associated with.

## Attributes reference

This section lists the attributes that are exported when the `scaleway_block_volume` resource is created:

- `id` - The ID of the volume.

~> **Important:** The IDs of Block Storage volumes are [zoned](../guides/regions_and_zones.md#resource-ids), meaning that the zone is part of the ID, in the form `{zone}/{id}`. For example, a volume ID migt be `fr-par-1/11111111-1111-1111-1111-111111111111`.

- `organization_id` - The Organization ID the volume is associated with.

## Import

This section explains how to import a Block Storage volume using the zoned ID (`{zone}/{id}`) format.

```bash
$ terraform import scaleway_block_volume.block_volume fr-par-1/11111111-1111-1111-1111-111111111111
```
