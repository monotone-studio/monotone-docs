---
title: Open Repository
weight: 6
bookToc: false
---

```C
MONOTONE_API int
monotone_open(monotone_t*, const char* path);

MONOTONE_API const char*
monotone_error(monotone_t*);
```

#### Open or Create

After [environment creation](/docs/tutorial/create_environment/) and [configuration](/docs/tutorial/configuration/),
a repository can be created (or opened).

[`monotone_open()`](/docs/api/) function opens or creates a repository using a specified `path`.

In case of an error, `-1` will be returned. [`monotone_error()`](/docs/api/) can be used to check the latest error message.
All log messages are saved in the log file inside the base directory.

#### Close

[`monotone_free()`](/docs/api/) must be called to free the monotone objects, such as environment objects and cursors.

All cursors must be freed before freeing the environment objects.
