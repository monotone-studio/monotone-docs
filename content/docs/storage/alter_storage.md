---
title: Alter storage
weight: 3
bookToc: false
---

```SQL
ALTER STORAGE [IF EXISTS] name RENAME TO new_name
ALTER STORAGE [IF EXISTS] name SET (options)
```

Rename storage or change its settings.

An error will be produced if storage does not exist unless an `IF EXISTS` clause is provided.

`RENAME TO` requires storage with the new name not to exist.

`SET` will change options initially provided by the [CREATE](/docs/storage/create_storage/) command.
Storage `UUID` cannot be changed.

Changing storage `path` requires storage to be empty (without partitions).

Changing the storage `cloud` is possible, but it requires that all partitions be
[downloaded](/docs/data/download/) or [dropped](/docs/data/drop/) from the associated cloud first.

Changing `compression` settings can be done without pre-requirements. Changing `compression` settings will not
update existing partitions. It is possible to simultaneously have compressed and not compressed partitions or
compressed using different compression types. [REFRESH](/docs/data/refresh/) command can update individual
partitions to the current storage settings.

Changing `encryption` settings requires storage to be empty.

#### Examples

```SQL
-- Storage rename
CREATE STORAGE A
ALTER STORAGE A RENAME TO B
```

```SQL
-- Change the main storage compression and region settings
ALTER STORAGE main SET (compression 'zstd', region_wm 150KiB)
```

```SQL
-- Change the main storage settings to use encryption
ALTER STORAGE main set (encryption 'aes', encryption_key '40SWVau0iHMdjhlRADriw74RenH3Gr4F')
```

---

See also [SHOW STORAGES](/docs/monitoring/show_storages/), [CREATE STORAGE](/docs/storage/create_storage/),
[DROP PARTITIONS](/docs/data/drop/)

