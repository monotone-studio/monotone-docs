---
title: Show Wal
weight: 4
bookToc: false
---

```SQL
SHOW MEMORY
```

Show Write-Ahead Log statistics using `JSON`.

#### Examples

```SQL
SHOW WAL

> show wal
{
  "active": true,
  "rotate_wm": 104857600,
  "sync_on_rotate": true,
  "sync_on_write": false,
  "crc": false,
  "lsn": 75179,
  "lsn_min": 74212,
  "files": 1
}
```

---

See also [SHOW](/docs/monitoring/show/)
