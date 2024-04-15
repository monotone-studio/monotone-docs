---
title: Create Environment
weight: 2
bookToc: false
---

```C
// private
typedef struct monotone monotone_t;

MONOTONE_API monotone_t*
monotone_init(void);

MONOTONE_API void
monotone_free(void*);
```

#### Environment

The first thing to do is to create a monotone environment object using the [`monotone_init()`](/docs/api/) API function.
It returns `NULL` on error.

#### Shutdown and Free objects

[`monotone_free()`](/docs/api/) must be called to free the monotone objects, such as environment objects and cursors.

All cursors must be freed before freeing the environment objects.
