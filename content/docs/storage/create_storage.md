---
title: Create storage
weight: 1
bookToc: false
---

```SQL
CREATE STORAGE [IF NOT EXISTS] name (options)
```

Create new logical storage.

Storage objects allow partitions to be stored on different storage devices using different settings, such as compression.
Any storage can be associated with a [Cloud](/docs/cloud/create_cloud/).

If storage with the same `name` already exists, an error will be produced unless the
`IF NOT EXISTS` clause is provided.

After creation, storage will only be used automatically once included in the [Pipeline](/docs/data_tiering/alter_pipeline/).
Any partitions can be [moved](/docs/data/move/) to or out of the storage or [dropped](/docs/data/drop/).

Each storage has a unique `UUID`, which is generated automatically (or provided in options).

{{< hint warning >}}

The `UUID` will be automatically included as part of the path and `S3 bucket`.

{{< /hint >}}

Monotone always creates `main` storage, which points to the base directory and has a `UUID`
equal to the current instance.

#### Options 

- uuid `string`

  Provide custom `UUID` for this storage.

- path `string`

  Set storage path. It can be absolute or relative to the base directory.
  If the path is not set, the base directory will be used.

- cloud `string`

  Associate cloud object with this storage. Setting this option will lead to bucket creation on S3.

- cloud_drop_local `bool`

  Drop local partition file after upload (`true` by default). This affects [REFRESH](/docs/data/refresh/), [MOVE](/docs/data/move/) and background upload.

- sync `bool`

  Sync partition files after refresh completion.

- crc `bool`

  Calculate and check all data CRC.

- refresh_wm `int`

  Set automatic partition refresh watermark. If any partition in-memory storage size exceeds this value,
  an automatic partition refresh will be scheduled in the background.

- region_size `int`

  Change default region size. Region size can directly affect compression efficiency and performance
  working on the cloud (do more or less round-trips).

- compression `string`

  Set compression type. Supported values are: `none`, `zstd`, `lz4`.

- compression_level `int`

  Set compression level depending on the compression type.

- encryption `string`

  Set encryption type. Supported values are: `none`, `aes`.

- encryption_key `string`

  Set the encryption key. The key must be `256 bits` long. If the key is not set, it will be
  automatically generated and saved inside the configuration file on the `CREATE STORAGE` command.

```SQL
-- Create new storage and set it as a primary
CREATE STORAGE hot_swap (path '/mnt/ssd', compression 'zstd')
ALTER PIPELINE hot_swap
```

```SQL
--
-- Create and keep all new partitions on SSD storage for a short duration
-- of time for a faster refresh and read. Automatically move partitions
-- to cold HDD storage when hot storage reaches its limit. Automatically
-- Delete older partitions from cold storage when they reach their limit.
-- Use different compression settings.
--
CREATE STORAGE hot (path '/mnt/ssd', compression 'lz4')
CREATE STORAGE cold (path '/mnt/hdd', compression 'zstd')

ALTER PIPELINE hot (size 10G), cold (size 100G)
```

---

See also [SHOW STORAGES](/docs/monitoring/show_storages/), [DROP STORAGE](/docs/storage/drop_storage/),
[ALTER STORAGE](/docs/storage/alter_storage/), [ALTER PIPELINE](/docs/data_tiering/alter_pipeline/)
