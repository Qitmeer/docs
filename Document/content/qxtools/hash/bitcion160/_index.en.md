---
title: bitcoin160
weight: 5
#pre: "<b>1. </b>"
# chapter: true
---

calculate ripemd160( sha256( data ) )

```bash
~ qx bitcoin160 --help

Usage: qx bitcoin160 [hexstring]
```

#### Example

```bash
~ qx bitcoin160 900df00d

49f180cdaa4c6564f74a0b0321633bbcba4ef9c5
```

Is equivalent to the following example

```bash
~ qx sha256 900df00d | qx ripemd160

49f180cdaa4c6564f74a0b0321633bbcba4ef9c5
```