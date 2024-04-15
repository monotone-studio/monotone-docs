---
title: Show Config
weight: 2
bookToc: false
---

```SQL
SHOW CONFIG [name]
SHOW ALL
SHOW name
```

Show config settings using `JSON`.

Config settings can be changed using [SET](/docs/system/set/) command.

#### Examples

```SQL
SHOW uuid

"17de1198-0078-d0a5-6471-ad8dc03123c7"
```

```SQL
SHOW CONFIG

{
  "version": "0.0",
  "uuid": "17de1198-0078-d0a5-6471-ad8dc03123c7",
  "directory": "./repository",
  "log": true,
  "log_to_file": true,
  "log_to_stdout": false,
  "mm_limit": false,
  "mm_limit_wm": 8589934592,
  "mm_limit_behaviour": "block",
  "mm_page_size": 2097152,
  "wal": true,
  "wal_rotate_wm": 104857600,
  "wal_sync_on_rotate": true,
  "wal_sync_on_write": false,
  "wal_crc": false,
  "serial": true,
  "interval": 3000000,
  "compression": "zstd",
  "compression_level": 0,
  "workers": 3,
  "workers_upload": 1,
  "ssn": 0,
  "lsn": 0
}

```

---

See also [SET](/docs/system/set/)
