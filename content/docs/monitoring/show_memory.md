---
title: Show Memory
weight: 3
bookToc: false
---

```SQL
SHOW MEMORY
```

Show memory usage and configuration using `JSON`.

#### Examples

```SQL
SHOW MEMORY

{
  "pages": 256,
  "pages_used": 116,
  "pages_free": 140,
  "page_size": 2097152,
  "limit": false,
  "limit_wm": 8589934592,
  "limit_behaviour": "block",
  "limit_hits": 0,
  "cache": 8589934592
}
```

---

See also [SHOW](/docs/monitoring/show/)
