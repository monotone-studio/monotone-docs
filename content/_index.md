---
title: Introduction
type: docs
bookToc: false
---

![image description](/logo.png)

#### Overview

Monotone is a modern embeddable data storage designed from the ground up precisely
for sequential workloads, such as append write and range scans.

Sequential workloads are at the foundation of the following use cases:
`IoT, events, time series, crypto, blockchain, finance, monitoring, logs collection,
and Kafka-style workloads`.

Using Monotone, you can create high-performance `serverless` solutions for storage and
processing data directly within your application.

Made to match the following requirements:

- Collect and process events in large volumes serially or by time (auto-increment by default)
- Write events as fast as possible, maintaining order and persistence
- Delete or Update events by primary key when necessary (but rarely or never needed)
- Read any range of events as fast as possible using a primary key
- Efficiently store and manage large volumes of data using partitions
- Efficiently compress and encrypt data
- Transparently update partitions and recompress, decrypt data without blocking readers and writers
- Extend disk space without downtime by plugging additional storage
- Seamlessly work on top of S3
- Make sense of Hot and Cold data patterns using Data Tiering

The storage architecture
is inspired by a Log-Structured approach and implements a custom-made `memory-disk-cloud`
hybrid engine.

Learn more about its [Architecture](/docs/architecture/).

#### Features

- **Automatic Range Partitioning**

    Automatically partition data by range or time intervals (min/max).
	Transparently create partitions on write.
	Support partitions in the past and future.
	Automatically or manually [refresh](/docs/data/refresh/) partitions on disk or cloud after being updated.

- **Transparent Compression**

    Compress and recompress partitions automatically on [refresh](/docs/data/refresh/) or partition [move](/docs/data/move/).
	Allow different compression types and compression level settings.
	Everything is done transparently without blocking readers and writers.

- **Transparent Encryption**
	
	Encrypt and decrypt partitions automatically on [refresh](/docs/data/refresh/), partition [move](/docs/data/move/), and [read](/docs/tutorial/read_events/).
	Compatible with compression and done transparently without blocking readers and writers.

- **Multiple Storages**

    [Create storage](/docs/storage/create_storage/) to store data on different storage devices.
	Set [different storage settings](/docs/storage/create_storage/), such as compression, associated cloud, etc.
	Manually or automatically [move](/docs/data/move/) partitions between storages.
	Automatic compaction is made when moving to change settings.
	[Create](/docs/storage/create_storage/) or [drop](/docs/storage/drop_storage/) storage online.
	Extend disk space by adding new storage without downtime.

- **Data Tiering**

    Understand Hot and Cold data by creating data policies involving several storages.
	Define [Pipeline](/docs/data_tiering/alter_pipeline/) to specify where partitions are created and when they need to be moved or dropped.
	All are done automatically or manually.

- **Bottomless Storage**

    Associate storage with the [cloud](/docs/cloud/create_cloud/) for extensive and cheaper storage.
	Transparently access partitions on the cloud.
	Automate partitions lifecycle for the cloud using [Pipeline](/docs/data_tiering/alter_pipeline/).

    Automatically or manually handle updates by [reuploading partitions](/docs/data/refresh/) to the [cloud](/docs/cloud/create_cloud/).
	[Download](/docs/data/download/) or [upload](/docs/data/upload/) partitions.
	[Move](/docs/data/move/) partitions between local storage and the cloud.
	[Move](/docs/data/move/) partitions between different cloud services.
