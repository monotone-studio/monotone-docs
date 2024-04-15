---
weight: 11
bookFlatSection: false
title: "Programming Interface"
bookToc: false
---

```C
// private
typedef struct monotone        monotone_t;
typedef struct monotone_cursor monotone_cursor_t;
typedef struct monotone_event  monotone_event_t;

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

typedef int64_t (*monotone_compare_t)(monotone_event_t*,
                                      monotone_event_t*,
                                      void*);

// environment
MONOTONE_API monotone_t*
monotone_init(void);

MONOTONE_API void
monotone_free(void*);

MONOTONE_API const char*
monotone_error(monotone_t*);

MONOTONE_API int
monotone_set_compare(monotone_t*, monotone_compare_t, void* arg);

MONOTONE_API int
monotone_open(monotone_t*, const char* path);

MONOTONE_API int
monotone_execute(monotone_t*, const char* command, char** result);

// batch write
MONOTONE_API int
monotone_write(monotone_t*, monotone_event_t*, int count);

// cursor
MONOTONE_API monotone_cursor_t*
monotone_cursor(monotone_t*, const char* options, monotone_event_t*);

MONOTONE_API int
monotone_read(monotone_cursor_t*, monotone_event_t*);

MONOTONE_API int
monotone_next(monotone_cursor_t*);

```

---

Please look at the tutorial for a more detailed description of usage.
