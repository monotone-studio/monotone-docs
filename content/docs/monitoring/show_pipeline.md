---
title: Show Pipeline
weight: 8
bookToc: false
---

```SQL
SHOW PIPELINE
```

Show current [Pipeline](/docs/data_tiering/alter_pipeline/) settings using `JSON`.

#### Examples

```SQL
SHOW PIPELINE
[{
  "name": "test",
  "partitions": -1,
  "size": -1,
  "events": -1,
  "duration": -1
}]
```

---

See also [ALTER PIPELINE](/docs/data_tiering/alter_pipeline/), [REBALANCE](/docs/data_tiering/rebalance/)
