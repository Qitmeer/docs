---
title: hash160
weight: 6
#pre: "<b>1. </b>"
# chapter: true
---

calculate ripemd160( blake2b256( data ) )

```bash
~ qx hash160 --help

Usage: qx hash160 [hexstring]
```

##### Example

```bash
~ qx hash160 900df00d

a7a99d5c4c2b55f876010dd12f6733c99f1e9c1a
```

Is equivalent to the following example

```bash
~ qx blake2b256 900df00d | qx ripemd160

a7a99d5c4c2b55f876010dd12f6733c99f1e9c1a
```