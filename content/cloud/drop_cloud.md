---
title: Drop cloud
weight: 2
bookToc: false
---

```SQL
DROP CLOUD [IF EXISTS] name
```

Drop cloud object.

If the cloud does not exist, an error will be produced unless the
`IF EXISTS` clause is provided.

A cloud can be dropped only if not associated with any [storage](/docs/storage/create_storage/) object.

#### Examples

```SQL
DROP CLOUD s3
```

---

See also [SHOW CLOUDS](/docs/monitoring/show_clouds/), [CREATE CLOUD](/docs/cloud/create_cloud/),
[ALTER CLOUD](/docs/cloud/alter_cloud/)
