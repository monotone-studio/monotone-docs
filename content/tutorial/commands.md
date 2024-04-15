---
title: Commands
weight: 4
bookToc: false
---

```C
MONOTONE_API int
monotone_execute(monotone_t*, const char* command, char** result);

MONOTONE_API const char*
monotone_error(monotone_t*);
```

#### Command execution

Configuration, data management, and monitoring are controlled using `SQL-style` text commands.


After the environment is [created](/docs/tutorial/create_environment/), the [`monotone_execute()`](/docs/api/) function can be used to execute commands.
The `result` will have a pointer to the allocated text result of the command execution if there is any.
The result can be set to `NULL`.

{{< hint warning >}}

If the returned `result` is not `NULL,` it must be freed using the system `free(3)` function. 

{{< /hint >}}

In case of an error, `-1` will be returned. [`monotone_error()`](/docs/api/) can be used to check the latest error message.
All log messages are saved in the log file inside the base directory.
