---
title: Configuration
weight: 5
bookToc: false
---

```SQL
-- get a list of all configuration and runtime variables
SHOW CONFIG
{
  "version": "0.0",
  "uuid": "867638f7-380e-f20f-029f-51df1ff5b9c5",
  "directory": "./storage",
  "log": true,
  "log_to_file": true,
  "log_to_stdout": false,
  "mm_page_size": 2097152,
  "mm_limit": false,
  "mm_limit_wm": 8589934592,
  "mm_limit_behaviour": "block",
  "mm_cache": 8589934592,
  "wal": true,
  "wal_rotate_wm": 104857600,
  "wal_sync_on_rotate": true,
  "wal_sync_on_write": false,
  "wal_crc": false,
  "serial": true,
  "interval": 3000000,
  "workers": 3,
  "workers_upload": 1,
  "ssn": 0,
  "lsn": 0
}

-- change partitioning interval
SET interval TO 3000000

-- change number of background workers
SET workers TO 4

-- disable WAL
SET wal TO false
```

Some essential configuration options must be considered after [environment creation](/docs/tutorial/create_environment/) creation and
before [creating or openning](/docs/tutorial/open_repository/) a repository.

Please take a look at the [SHOW CONFIG](/docs/monitoring/show_config/) and [SET](/docs/system/set/) commands.

---

#### Instance UUID

- uuid `string`

Set UUID.

By default, the `UUID` is generated upon creation. In some cases, it might be useful to set it to a predefined value.

{{< hint warning >}}

`UUID` can be changed only before the first opening. 

{{< /hint >}}

See also [CREATE STORAGE](/docs/storage/create_storage/).

---

#### Serial Mode

- serial `bool`

Serial mode allows the assignment of event IDs automatically when written in an auto-increment way.

`It is enabled by default.`


The current serial state is stored inside the `ssn` variable, which can be changed.
Each new event `id` will be assigned as `ssn + 1`. The serial state is persistent.

{{< hint warning >}}

The event ID must be set to `UINT64_MAX` on write. 

{{< /hint >}}

---

#### Partitioning Interval

- interval `int`

Set partitioning interval value.

Each partition has inclusive `min`/`max` interval.

This metric sets the partition range per each new partition as:
`partition min + interval - 1`.

It can be changed during runtime.

See also [CREATE PARTITIONS](/docs/data/create/).

---

#### Write-Ahead Log

Options to control WAL behavior.

{{< hint warning >}}

WAL significantly affects performance and write-amplification in exchange for the per-operation durability.

Disabling WAL and relying only on automatic (or manual) per-partition durability might be a reasonable option.

{{< /hint >}}


- wal `bool`

- wal_rotate_wm `int`

  The number of operations per WAL file. When the current WAL file reaches this value, a new file will be created.

- wal_sync_on_rotate `bool`

  Sync the previous WAL file when a new one is created (`enabled by default`).

- wal_sync_on_write `bool`

  Sync the current WAL file on each write (`disabled by default`).

- wal_crc `bool`

  Calculate and validate crc for each transaction (`disabled by default`).

---

#### Background Workers

- workers `int`

Set the number of background workers. It can be changed only before opening.

It can be set to zero for complete manual control and deterministic testing.

{{< hint warning >}}

Workers share the workload. 

{{< /hint >}}

- workers_upload `int`

Set the number of background workers for upload only. It can be changed only before opening.

If set to zero, regular workers will do the upload.

{{< hint warning >}}

Enabling upload workers to access the cloud is highly recommended.

Running separate upload workers might be necessary in case of a slow network or big partitions.
Workers might stall, which would lead to excessive memory consumption.

If cloud is not used, can be set to zero.

{{< /hint >}}

---

#### Log file

Log messages and errors.

- log `bool`

- log_to_file `string`

  Create and write a log file inside the base directory (`enabled by default`).

- log_to_stdout `bool`

  Duplicate messages from the log file to stdout (`disabled by default`).

---

#### Memory Manager

- mm_limit `bool`

  Turn the memory limit on or off (`disabled by default`).

- mm_limit_wm `int`

  Memory limit watermark value.

- mm_limit_behaviour `string`

  Behavior for memory limit reach. Supported values are `block`, `error`.

- mm_page_size `int`

  Size of a single memory page.

- mm_cache `int`

  Size of a free page cache. Can be set to zero.
