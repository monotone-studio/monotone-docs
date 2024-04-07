---
title: Show Storages
weight: 6
bookToc: false
---

```SQL
SHOW STORAGE name
SHOW STORAGES
```

Show storages and their statistics using `JSON`.

#### Examples

```SQL
SHOW STORAGE test
{
  "config": {
    "uuid": "e85edbbc-5a6f-1744-384c-50f696769167",
    "name": "test",
    "path": "",
    "cloud": "s3",
    "cloud_drop_local": true,
    "sync": true,
    "crc": false,
    "refresh_wm": 0,
    "region_size": 524288,
    "compression": "zstd",
    "compression_level": 0,
    "encryption": ""
  },
  "stats": {
    "min": 0,
    "max": 102000000,
    "partitions": 34,
    "partitions_local": 0,
    "partitions_cloud": 33,
    "regions": 22110,
    "events": 100140000,
    "events_heap": 1140000,
    "size": 467306599,
    "size_uncompressed": 11589592542,
    "size_heap": 138412032
  }
}
```

```SQL
SHOW STORAGES
{
  "main": {
    "config": {
      "uuid": "17de1198-0078-d0a5-6471-ad8dc03123c7",
      "name": "main",
      "path": "",
      "cloud": "",
      "sync": true,
      "crc": false,
      "refresh_wm": 41943040,
      "region_size": 131072,
      "compression": "",
      "compression_level": 0,
      "encryption": ""
    },
    "stats": {
      "min": 0,
      "max": 0,
      "partitions": 0,
      "partitions_local": 0,
      "partitions_cloud": 0,
      "regions": 0,
      "events": 0,
      "events_heap": 0,
      "size": 0,
      "size_uncompressed": 0,
      "size_heap": 0
    }
  },
  "test": {
    "config": {
      "uuid": "e85edbbc-5a6f-1744-384c-50f696769167",
      "name": "test",
      "path": "",
      "cloud": "s3",
      "sync": true,
      "crc": false,
      "refresh_wm": 0,
      "region_size": 524288,
      "compression": "zstd",
      "compression_level": 0,
      "encryption": "aes"
    },
    "stats": {
      "min": 0,
      "max": 102000000,
      "partitions": 34,
      "partitions_local": 0,
      "partitions_cloud": 33,
      "regions": 22110,
      "events": 100140000,
      "events_heap": 1140000,
      "size": 467306599,
      "size_uncompressed": 11589592542,
      "size_heap": 138412032
    }
  }
}

```

---

See also [CREATE STORAGE](/docs/storage/create_storage/), [DROP STORAGE](/docs/storage/drop_storage/),
[ALTER STORAGE](/docs/storage/alter_storage/)
