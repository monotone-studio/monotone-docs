---
title: Show
weight: 1
bookToc: false
---

```SQL
SHOW command, [...]
```

Get a reply from one or more `SHOW` commands using `JSON.`

#### Examples

```SQL
SHOW uuid

"17de1198-0078-d0a5-6471-ad8dc03123c7"
```

```SQL
SHOW uuid, STORAGE main, WAL

["17de1198-0078-d0a5-6471-ad8dc03123c7", {
  "config": {
    "uuid": "17de1198-0078-d0a5-6471-ad8dc03123c7",
    "name": "main",
    "path": "",
    "cloud": "",
    "sync": true,
    "crc": false,
    "compression": "zstd",
    "compression_level": 0,
    "refresh_wm": 0,
    "region_size": 131072
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
}, {
  "lsn": 0,
  "lsn_min": 1,
  "files": 1
}]

```

---

See also [SET](/docs/system/set/)
