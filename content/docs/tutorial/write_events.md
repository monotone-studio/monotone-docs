---
title: Write Events
weight: 7
bookToc: false
---

```C
typedef struct monotone_event monotone_event_t;

enum
{
	MONOTONE_DELETE = 1
};

struct monotone_event
{
	uint64_t id;
	void*    data;
	size_t   data_size;
	int      flags;
};

MONOTONE_API int
monotone_write(monotone_t*, monotone_event_t*, int count);
```

#### Batch Insert

[`monotone_write()`](/docs/api/) API function is used to do an atomical write `count` of events.

Each event has an associated `id`, `data`, `data_size`, and `flags` fields.
`data_size` can be zero, and the `flags` must be set to zero for insert.

{{< hint warning >}}

In the case of using serial mode, the event `id` must be set to `UINT64_MAX` before write.

After writing, each event `id` will be set to the automatically assigned value.

`Serial mode is enabled by default.`

{{< /hint >}}

Unless a custom comparator is not defined, `id` represents a unique primary key and can be used in
the future to replace or delete that event.

In case of an error, `-1` will be returned. [`monotone_error()`](/docs/api/) can be used to check the latest error message.
All log messages are saved in the log file inside the base directory.

Writing only succeeds if data is written in the Write-ahead log.
WAL logs are automatically deleted when data are saved to partitions.

{{< hint warning >}}

WAL significantly affects performance and write-amplification in exchange for the per-operation durability.

Disabling WAL and relying only on automatic (or [manual](/docs/data/refresh/)) per-partition durability might be a reasonable option.

{{< /hint >}}

All write operations (including delete) never check for the original event's existence, so there
are no unique constraints implemented for performance reasons.

Write is a strictly in-memory operation, with the addition of WAL write, which writes to the current
WAL file (if it is enabled).

Upon successful writing, events get written to their in-memory storage associated with each partition.

Eventually, updated partitions will be synced and [refreshed](/docs/data/refresh/).

---

#### Delete Events

Setting the event `flags` to `MONOTONE_DELETE` will produce a delete operation. In monotone, delete is implemented as a write with a special flag.
If the original event does not exist, the deletion will be ignored automatically during the refresh operation.

{{< hint warning >}}

Please note that deleting individual events might be inefficient.
[Dropping](/docs/data/drop/) individual partitions instead is recommended for managing data. 

{{< /hint >}}

---

#### Concurrency

Write takes locks on each used partition and releases them after WAL writes.

The most optimal way to work would be to allow readers and writers to work on non-overlapping partitions.

{{< hint warning >}}

If you are collecting data, it would be better to have a single writer who always appends.

If you need to improve write performance further, consider shard data (have separate instances) per individual writer thread.

{{< /hint >}}

[Refresh](/docs/data/refresh/) and other data management commands designed to work with concurrent writers.
