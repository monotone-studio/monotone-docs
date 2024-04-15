---
weight: 1
bookFlatSection: false
title: "Get Started"
bookToc: false
---

![image description](/docs/logo.png)

#### Package

Binary package consists of the following files:

```sh
libmonotone.so
monotone.h
monotone
```

* `libmonotone.so` -- shared C library, which must be linked with your application.
* `monotone.h` -- monotone C API header file.
* `monotone` -- monotone CLI application.

Please look at the [Build and Install](/docs/tutorial/build/) section for the manual build instructions.

#### API

Monotone provides simple [C API](/docs/api/).

[Insert](/docs/tutorial/write_events/) (and replace/delete) is done in batches using the event `id` associated with `raw data`.
Data are read using [cursors](/docs/tutorial/read_events/).
Data management, administration, and monitoring are done by using `SQL-style DDL commands`.

#### Data storage

Monotone represents data as a 64-bit-range sparse array of ordered events.
Events are partitioned by fixed [intervals](/docs/tutorial/configuration/), and partitions are automatically created
on [write](/docs/tutorial/write_events/) or [manually](/docs/data/create).

Each partition has an associated inclusive `[min, max]` range.
Partitions never overlap. `Min` range is used as a partition `ID` for data management.

Data management is implemented using partitions as a primary unit.
Data are stored in sorted partition files, which can be stored in local [storage](/docs/storage/create_storage/), an associated [cloud](/docs/cloud/create_cloud/), or both.

An event is a combination of 64-bit id (or time) and key/value raw data `[id, key, value]`.
The event `id` and the optional `key` represent a serial (or time) compound primary key. Events are designed to store any kind of unstructured data.
The key and value data size might be zero.

After [writing](/docs/tutorial/write_events/), events are cached in in-memory storage associated with the partition.
Eventually, the updated partition must be [refreshed](/docs/data/refresh) to sync (or create) the partition file.
Refreshing can happen automatically in the background or manually.

Learn more about the [Architecture](/docs/architecture/).

#### Usage

Typical workflow:

- [Create environment](/docs/tutorial/create_environment/)
- [Configure](/docs/tutorial/configuration/)
- [Open repository](/docs/tutorial/open_repository/)
- [Configure Tiering](/docs/tutorial/data_management/)
- [Write Events](/docs/tutorial/write_events/)
- [Read Events](/docs/tutorial/read_events/)
- [Monitoring](/docs/tutorial/monitoring/)
