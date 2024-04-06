---
title: Drop partitions
weight: 3
bookToc: false
---

```SQL
DROP PARTITION [IF EXISTS] id [ON STORAGE | ON CLOUD]
DROP PARTITIONS BETWEEN min AND max [ON STORAGE | ON CLOUD]
```

Drop one or more partitions.

Partition `id` is equal to the partition min interval. `min` and `max` range is inclusive.

If a partition does not exist, an error will be produced unless the `IF EXISTS` clause is provided.
`DROP PARTITIONS` will not produce an error if no partitions exist between the `min` and `max` intervals.

The `ON STORAGE` or `ON CLOUD` clauses allow you to drop a partition file from the
associated cloud or storage. Partition files can be [uploaded](/docs/data/upload/) to or [downloaded](/docs/data/download/) from the cloud.

Partitions are possible without files and with or without pending updates in memory.
If `ON STORAGE` or `ON CLOUD` are not specified, partition files will be dropped from the cloud,
associated storage, and in-memory.

#### Examples

```SQL
DROP PARTITIONS BETWEEN 0 AND 10000
```

---

See also [MOVE PARTITIONS](/docs/data/move/), [CREATE STORAGE](/docs/storage/create_storage/)
