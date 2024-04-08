---
weight: 1
title: "Build and Install"
---

# Build

#### OS

Currently only Linux environments are supported.

#### Dependencies

- cmake
- gcc (recommended) or clang
- libcurl
- openssl
- zstd
- lz4

#### Build Release

```sh
git clone https://github.com/monotone-studio/monotone
cd monotone
make release
```

#### Build Release (pass cmake options directly)

```sh
git clone https://github.com/monotone-studio/monotone
cd monotone
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=<install_path> .
make
```

#### Build Debug

```sh
git clone https://github.com/monotone-studio/monotone
cd monotone
make debug
```

#### Running tests

```sh
make
cd test
./monotone-test
```
