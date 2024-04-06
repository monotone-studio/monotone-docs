---
title: Create partitions
weight: 2
bookToc: false
---

```SQL
CREATE PARTITION min max
```

Create one or more partitions from `min` to `max` inclusive interval.

Typically, there is no need to use this command since partitions are created automatically on write.
However, this command can manually create partitions of different intervals rather than
using one set globally.

If overlapping partitions exist, this command will create two or more partitions to fill the gap
between the minimum and maximum range.

{{< hint warning >}}

Partitions will be created empty without corresponding partition files or WAL records.
They will not be recreated on restart unless explicitly written by the [REFRESH](/docs/data/refresh/) command.

{{< /hint >}}

#### Global partition interval


It is possible to change global partition interval using `SET` command:

```SQL
SET interval TO 10000
```

#### Examples

```SQL
CREATE PARTITION 0 10000

SHOW PARTITIONS

[{
  "min": 0,
  "max": 10000,
  "events": 0,
  "events_heap": 0,
  "regions": 0,
  "size": 0,
  "size_uncompressed": 0,
  "size_heap": 0,
  "created": 1712235990007596,
  "refreshed": 0,
  "refreshes": 0,
  "on_storage": false,
  "on_cloud": false,
  "storage": "main"
}]
```

---

See also [SHOW PARTITIONS](/docs/monitoring/show_partitions/), [DROP PARTITIONS](/docs/data/drop/), [MOVE PARTITIONS](/docs/data/move/), [CREATE STORAGE](/docs/storage/create_storage/)
