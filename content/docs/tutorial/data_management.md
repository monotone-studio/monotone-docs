---
title: Data Management
weight: 9
bookToc: false
---

#### Data Management and Tiering

Partitions are stored in local [storages](/docs/storage/create_storage/), associated [clouds](/docs/cloud/create_cloud/), or both simultaneously.

Storage can be dynamically [created](/docs/storage/create_storage/), [dropped](/docs/storage/drop_storage/), or [altered](/docs/storage/alter_storage/).

Monotone always creates `main` storage, which points to the base directory and has a `UUID` equal to the current instance.

Partitions can be [created](/docs/data/create/), [dropped](/docs/data/drop/), [moved](/docs/data/move/),
[refreshed](/docs/data/refresh/), [downloaded](/docs/data/download/), or [uploaded](/docs/data/upload/).

[Pipeline](/docs/data_tiering/alter_pipeline/) provides a simple way to automate partitions lifecycle
using storages.
