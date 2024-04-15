---
title: Refresh partitions
weight: 4
bookToc: false
---

```SQL
REFRESH PARTITION [IF EXISTS] id
REFRESH PARTITIONS BETWEEN min AND max
```

Refresh one or more partitions.

Refresh commands allow manually merging pending in-memory updates with the local partition file.
If the local partition file does not exist, a new one will be created. `min` and `max` range is inclusive.

Typically, there is no need to use these commands since refresh is automated and run by background workers.

If the partition has an associated cloud, refresh will automatically perform the following operations in the exact order:

- [download](/docs/data/download/) the partition from the cloud
- [drop](/docs/data/drop/) partition on the cloud
- merge in-memory storage with the partition file (or create a new one)
- [upload](/docs/data/upload/) partition to the cloud
- [drop](/docs/data/drop/) partition file on the local storage, if the partition is on cloud (can be controlled by the [cloud_drop_local](/docs/storage/create_storage/) option on the storage)

After completion, the refresh command frees the memory associated with the partition and triggers `WAL` cleanup.

Refresh and all involved commands do not block access to the partition during their operation.

#### Examples

```SQL
REFRESH PARTITIONS BETWEEN 0 AND 10000
```

---

See also [MOVE PARTITIONS](/docs/data/move/), [CREATE STORAGE](/docs/storage/create_storage/)
