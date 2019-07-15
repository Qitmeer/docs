---
title: sha256
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

Perform a **SHA256** or **SHA3 256** of Base16 data.

### SHA256

calculate SHA256 hash of a base16 data.

```bash
~ qx sha256 --help

Usage: qx sha256 [hexstring]
```

#### Example

```bash
~ qx sha256 900df00d

f0ebe3bd55115e573ba35c2b1b65a923ff64c7a548d0deab73f9314754a9149d
```

----

### sha3-256

calculate SHA3 256 hash of a base16 data.

```bash
~ qx sha3-256 --help

Usage: qx sha3-256 [hexstring]
```

#### Example 1

```bash
~ qx sha3-256 900df00d

e2c74fd95c71ec226e1b8bb5150aa43121ba0759b0977660a2e2b1d71830256e
```
