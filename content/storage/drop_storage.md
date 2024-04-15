---
title: Drop storage
weight: 2
bookToc: false
---

```SQL
DROP STORAGE [IF EXISTS] name
```

Drop a storage.

An error will be produced if storage does not exist unless an `IF EXISTS`
clause is provided.

Storage can be dropped only if it has no partitions and is not included
in the [Pipeline](/docs/data_tiering/alter_pipeline/).

`main` storage cannot be dropped.

#### Examples

```SQL
-- Create first storage
CREATE STORAGE A
ALTER PIPELINE A

-- Create second storage
CREATE STORAGE B
ALTER PIPELINE B

-- Drop first storage
DROP STORAGE A
```

---

See also [SHOW STORAGES](/docs/monitoring/show_storages/), [CREATE STORAGE](/docs/storage/create_storage/),
[DROP PARTITIONS](/docs/data/drop/)
