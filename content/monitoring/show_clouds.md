---
title: Show Clouds
weight: 5
bookToc: false
---

```SQL
SHOW CLOUD name
SHOW CLOUDS
```

Show created clouds using `JSON`.

#### Examples

```SQL
SHOW CLOUD s3
{
  "name": "s3",
  "type": "s3",
  "login": "minioadmin",
  "password": "(secret)",
  "url": "localhost:9000",
  "debug": false
}
```

```SQL
SHOW CLOUDS
{
  "s3": {
    "name": "s3",
    "type": "s3",
    "login": "minioadmin",
    "password": "(secret)",
    "url": "localhost:9000",
    "debug": false
  }
}

```

---

See also [CREATE CLOUD](/docs/cloud/create_cloud/), [DROP CLOUD](/docs/cloud/drop_cloud/),
[ALTER CLOUD](/docs/cloud/alter_cloud/)
