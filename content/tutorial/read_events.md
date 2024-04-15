---
title: Read Events
weight: 8
bookToc: false
---

```C
// private
typedef struct monotone_cursor monotone_cursor_t;
typedef struct monotone_event  monotone_event_t;

struct monotone_event
{
	uint64_t id;
	void*    data;
	size_t   data_size;
	int      flags;
};

MONOTONE_API monotone_cursor_t*
monotone_cursor(monotone_t*, const char* options, monotone_event_t* key);

MONOTONE_API int
monotone_read(monotone_cursor_t*, monotone_event_t*);

MONOTONE_API int
monotone_next(monotone_cursor_t*);
```

#### Cursor

The [`monotone_cursor()`](/docs/api/) API function is used to create and position a cursor starting from a provided `key`.
If the `Key` is not defined, the cursor will start from the `minimum` event that currently exists.
Currently, the `options` argument is reserved and not used; `NULL` must be passed.

In case of an error, `NULL` will be returned. [`monotone_error()`](/docs/api/) can be used to check the latest error message.
All log messages are saved in the log file inside the base directory.

[`monotone_read()`](/docs/api/) is used to access the current cursor event. The returned events should not be freed.

In case of an error, `-1` will be returned or `0` in case of end.

[`monotone_next()`](/docs/api/) position cursor to the next, if any.

In case of an error, `-1` will be returned or `0` in case of end.

Cursors perform partition exclusion and work only with partitions that point to the current position.
Each cursor performs a merge join between the partition file region and in-memory storage (Learn more about the [Architecture](/docs/overview/architecture/)).

---

#### Cloud

If the partition is on the cloud, the cursor will make remote requests for each region individually.

{{< hint warning >}}

Storage region size can significantly improve performance on a cloud or slow storage.
Essentially, it affects the total number of round trips necessary to complete the scan. 

{{< /hint >}}

[Downloading](/docs/data/download/) the partition will switch reads to using local file copy.

---

#### Concurrency

The cursor takes locks on each partition and releases them when switching to the next partition.
The most optimal way to work would be to allow readers and writers to work on non-overlapping partitions.

[Refresh](/docs/data/refresh/) and other data management commands are designed to work
with concurrent readers and writers.
