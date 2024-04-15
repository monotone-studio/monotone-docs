---
title: Set Comparator
weight: 3
bookToc: false
---

```C
struct monotone_event
{
	uint64_t id;
	void*    data;
	size_t   data_size;
	int      flags;
};

typedef int64_t (*monotone_compare_t)(monotone_event_t*,
                                      monotone_event_t*,
                                      void*);

MONOTONE_API int
monotone_set_compare(monotone_t*, monotone_compare_t, void* arg);
```

#### Comparator

Using the [`monotone_set_compare()`](/docs/api/) API function, you can set a custom compare function.
This function can be used to implement compound keys.

The event `id` will be used as an event primary key if the compare function is not set.

This is the `default behavior`.

{{< hint warning >}}

A comparator can be changed only until the [`monotone_open()`](/docs/tutorial/open_repository/) call.

{{< /hint >}}

In case of an error, `-1` will be returned. [`monotone_error()`](/docs/api/) can be used to check the latest error message.
All log messages are saved in the log file inside the base directory.
