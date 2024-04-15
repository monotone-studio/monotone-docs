---
title: Move partitions
weight: 5
bookToc: false
---

```SQL
MOVE PARTITION [IF EXISTS] id INTO storage
MOVE PARTITIONS BETWEEN min AND max INTO storage
```

Move one or more partitions between storages manually.

If the partition does not exist, an error will be produced unless the `IF EXISTS` clause is provided.
`MOVE PARTITIONS` will not produce an error if no partitions exist between the `min` and `max` intervals.
`min` and `max` range is inclusive.

Since each storage can have different settings, partitions are recompacted each time.
Implementation-wise, the move is almost identical to the [refresh](/docs/data/refresh/), with the difference of creating partitions for different storage.

If the source or destination storage has an associated cloud, the move will automatically perform the following operations in the exact order:

- [download](/docs/data/download/) partition from the source storage cloud, if any
- [drop](/docs/data/drop/) partition on the source storage cloud, if any
- merge and create a new partition file on the destination storage
- [drop](/docs/data/drop/) partition file on the source storage (atomical with the previous step)
- [upload](/docs/data/upload/) partition to the destination storage cloud, if any
- [drop](/docs/data/drop/) partition file on the destination storage, if the partition is on cloud (can be controlled by the [cloud_drop_local](/docs/storage/create_storage/) option on the storage)

Move and all involved commands do not block partition access during their operation.

#### Examples

```SQL
MOVE PARTITIONS BETWEEN 0 AND 10000 INTO cold_storage
```

---

See also [DROP PARTITIONS](/docs/data/drop/), [CREATE STORAGE](/docs/storage/create_storage/)
