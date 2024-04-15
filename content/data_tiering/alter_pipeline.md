---
title: Alter Pipeline
weight: 1
bookToc: false
---

```SQL
ALTER PIPELINE SET storage [(retention options)] [, ...]
ALTER PIPELINE SET first, ..., last

ALTER PIPELINE RESET
```

Define data tiering and retention policy for partitions.

Pipeline provides a simple way to automate partitions lifecycle.
`SET` one or more storages with retention options (tiers).

The `first` tier sets `primary storage`. Primary storage is a storage where all new partitions are created.

`Retention options` allow you to specify conditions when partitions are [moved](/docs/data/move/) from
the current tier to the next one in the chain or [dropped](/docs/data/drop/).

The `last` tier is the final tier. Retention options on a final tier specify conditions for an automatic [DROP](/docs/data/drop/),
and the final tier might have no retention options.

The `first` tier can be the `last` (only one tier in the pipeline).

If the retention condition has been met, the oldest partition in the storage will be used.
The oldest partition is chosen based on its creation time (microseconds).

`RESET` clause sets the pipeline to the default state.

#### Default

If a pipeline is not specified, then `main` storage becomes `primary storage`.

#### Retention options

- *partitions* `int`

  Maximum number of partitions in the storage.

- *size* `int`

  Maximum storage size in bytes.

- *events* `int`

  Maximum number of events in the storage.

- *duration* `int`

  The interval between the current time and the time of the creation of
  the oldest partition (microseconds).

#### Examples

```SQL
--
-- Extend disk storage by hot plugging additional storage device
--
CREATE STORAGE extended_storage (path '/mnt/hot_swap', compression 'zstd')
ALTER PIPELINE extended_storage
```

```SQL
-- Create and keep all new partitions on SSD storage for a short duration
-- of time for a faster refresh and read. Automatically move partitions
-- to cold HDD storage when hot storage reaches its limit. Automatically
-- Delete older partitions from cold storage when they reach their limit.
--
CREATE STORAGE hot (path '/mnt/ssd', compression 'zstd')
CREATE STORAGE cold (path '/mnt/hdd', compression 'zstd')

ALTER PIPELINE hot (size 10G), cold (size 100G)
```

```SQL
--
-- Store recent data on SSD for one day, then move to S3.
--
CREATE CLOUD s3 (type 's3', access_key 'minioadmin', secret_key 'minioadmin', url 'localhost:9000')
CREATE STORAGE hot (compression 'zstd')
CREATE STORAGE cold (cloud 's3', compression 'zstd', encryption 'aes')

ALTER PIPELINE hot (duration 1day), cold
```

---

See also [SHOW PIPELINE](/docs/monitoring/show_pipeline/), [REBALANCE](/docs/data_tiering/rebalance/), [MOVE PARTITIONS](/docs/data/move/), [DROP PARTITIONS](/docs/data/drop/), [CREATE STORAGE](/docs/storage/create_storage/)
