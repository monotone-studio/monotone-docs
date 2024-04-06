---
title: Alter cloud
weight: 3
bookToc: false
---

```SQL
ALTER CLOUD [IF EXISTS] name RENAME TO new_name
ALTER CLOUD [IF EXISTS] name SET (options)
```

Rename the cloud or change its settings.

If the cloud does not exist, an error will be produced unless the `IF EXISTS`
clause is provided.

`RENAME TO` requires that a cloud with the `new name` not exist.

`SET` will change options initially provided by the [CREATE](/docs/cloud/create_cloud/) command.
Cloud `type` cannot be changed.

#### Examples

```SQL
-- Cloud rename
CREATE CLOUD local (type 's3', access_key 'minioadmin', secret_key 'minioadmin', url 'localhost:9000')
ALTER CLOUD local RENAME TO s3
```

```SQL
-- Enable debug to catch connection issues
ALTER CLOUD s3 SET (debug true)
```

---

See also [SHOW CLOUDS](/docs/monitoring/show_clouds/), [CREATE STORAGE](/docs/storage/create_storage/),
[DROP PARTITIONS](/docs/data/drop/)
