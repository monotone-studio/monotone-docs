---
title: Create cloud
weight: 1
bookToc: false
---

```SQL
CREATE CLOUD [IF NOT EXISTS] name (options)
```

Create a cloud object.

An error will be produced if a cloud object with the same `name` already exists unless the
`IF NOT EXISTS` clause is provided.

Cloud objects can be associated with one or more [Storages](/docs/storage/create_storage/).

#### Options

- type `string`

  Set Cloud type. Current supported: `s3`.

- url `string`

  S3 service URL.

- access_key `string`

  Provide S3 access key.

- secret_key `string`

  Provide S3 secret key.

- login `string`

  Alias for access_key.

- password `string`

  Alias for secret_key.

- debug `bool`

  Enable debug mode for the Cloud. Debug information related to the S3 will be written to the log.

#### Examples

```SQL
--
-- Store recent data on SSD for 1 day, then move to S3.
--
CREATE CLOUD s3 (type 's3', access_key 'minioadmin', secret_key 'minioadmin', url 'localhost:9000')
CREATE STORAGE hot (compression 'zstd')
CREATE STORAGE cold (cloud 's3', compression 'zstd', encryption 'aes')

ALTER PIPELINE hot (duration 1day), cold
```

```SQL
--
-- Work on top of S3.
--
CREATE CLOUD s3 (type 's3', access_key 'minioadmin', secret_key 'minioadmin', url 'localhost:9000')
ALTER STORAGE main (cloud 's3', compression 'zstd')
``` 

---

See also [SHOW CLOUDS](/docs/monitoring/show_clouds/), [DROP CLOUD](/docs/cloud/drop_cloud/),
[ALTER CLOUD](/docs/cloud/alter_cloud/)
