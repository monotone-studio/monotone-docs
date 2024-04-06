---
title: Checkpoint
weight: 8
bookToc: false
---

```SQL
CHECKPOINT
```

Schedule a background [refresh](/docs/data/move/) for all pending in-memory updates.

This operation is non-blocking and async.

#### Examples

```SQL
CHECKPOINT
```

---

See also [REFRESH PARTITIONS](/docs/data/move/)
