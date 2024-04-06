---
title: Download partitions
weight: 6
bookToc: false
---

```SQL
DOWNLOAD PARTITION [IF EXISTS] id [IF CLOUD]
DOWNLOAD PARTITIONS BETWEEN min AND max [IF CLOUD]
```

Download one or more partitions from the cloud to the local storage.

If a partition does not exist, an error will be produced unless the `IF EXISTS` clause is provided.
`DOWNLOAD PARTITIONS` will not produce an error if no partitions exist between the `min` and `max` intervals.
`min` and `max` range is inclusive.

An error will be produced if partitions have no associated cloud unless a `IF CLOUD` clause is provided.

After successful execution, the partition file will remain on the cloud, but future access will be done using the local copy.
The [DROP](/docs/data/drop/) command can be used to delete a file on the cloud.

#### Examples

```SQL
DOWNLOAD PARTITIONS BETWEEN 0 AND 10000
```

---

See also [DROP PARTITIONS](/docs/data/drop/), [CREATE STORAGE](/docs/storage/create_storage/),
[CREATE CLOUD](/docs/cloud/create_cloud/)
