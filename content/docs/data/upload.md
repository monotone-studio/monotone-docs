---
title: Upload partitions
weight: 7
bookToc: false
---

```SQL
UPLOAD PARTITION [IF EXISTS] id [IF CLOUD]
UPLOAD PARTITIONS BETWEEN min AND max [IF CLOUD]
```

Upload one or more partitions to the associated cloud.

If a partition does not exist, an error will be produced unless the `IF EXISTS` clause is provided.
`UPLOAD PARTITIONS` will not produce an error if no partitions exist between the `min` and `max` intervals.
`min` and `max` range is inclusive.

An error will be produced if partitions have no associated cloud unless a `IF CLOUD` clause is provided.

After successful execution, the partition file will remain on local storage.
The [DROP](/docs/data/drop/) command can be used to delete the local file and switch to using cloud copy for future access.

#### Examples

```SQL
UPLOAD PARTITIONS BETWEEN 0 AND 10000
```

---

See also [DOWNLOAD PARTITIONS](/docs/data/download/), [DROP PARTITIONS](/docs/data/drop/),
[CREATE STORAGE](/docs/storage/create_storage/), [CREATE CLOUD](/docs/cloud/create_cloud/)
