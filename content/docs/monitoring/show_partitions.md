
---
title: Show Partitions
weight: 7
bookToc: false
---

```SQL
SHOW PARTITIONS [storage_name]
SHOW PARTITION id
```

List partitions using `JSON`.

#### Examples

```SQL
SHOW PARTITIONS

[{
  "min": 0,
  "max": 2999999,
  "events": 3000000,
  "events_heap": 0,
  "regions": 2677,
  "size": 13967985,
  "size_uncompressed": 351203582,
  "size_heap": 0,
  "created": 1712235856124572,
  "refreshed": 1712235856993813,
  "refreshes": 1,
  "on_storage": false,
  "on_cloud": true,
  "storage": "main"
}, {
  "min": 3000000,
  "max": 5999999,
  "events": 3000000,
  "events_heap": 0,
  "regions": 2677,
  "size": 13967294,
  "size_uncompressed": 351203582,
  "size_heap": 0,
  "created": 1712235856993615,
  "refreshed": 1712235857869257,
  "refreshes": 1,
  "on_storage": false,
  "on_cloud": true,
  "storage": "main"
}, {
  "min": 6000000,
  "max": 8999999,
  "events": 634200,
  "events_heap": 634200,
  "regions": 0,
  "size": 0,
  "size_uncompressed": 0,
  "size_heap": 77594624,
  "created": 1712235857869048,
  "refreshed": 0,
  "refreshes": 0,
  "on_storage": false,
  "on_cloud": false,
  "storage": "main"
}]
```

```SQL
SHOW PARTITION 6000000

{
  "min": 6000000,
  "max": 8999999,
  "events": 634200,
  "events_heap": 634200,
  "regions": 0,
  "size": 0,
  "size_uncompressed": 0,
  "size_heap": 77594624,
  "created": 1712235857869048,
  "refreshed": 0,
  "refreshes": 0,
  "on_storage": false,
  "on_cloud": false,
  "storage": "main"
}
```

---

See also [CREATE STORAGE](/docs/storage/create_storage/), [CREATE PARTITIONS](/docs/data/create/)
