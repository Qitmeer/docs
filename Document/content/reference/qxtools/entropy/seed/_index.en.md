---
title: entropy
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

### entropy

generate a cryptographically secure pseudorandom entropy (seed).

{{% notice warning %}}
WARNING: Pseudorandom seeding can introduce cryptographic weakness into your keys. This command is provided as a convenience.
{{% /notice %}}

```bash
~ qx entropy --help

Usage: qx entropy [-s size]
    -s uint
        The length in bits for a seed (entropy) (default 256)
```

#### Example 1

```bash
~ qx entropy

492ac7d4d0eb37eda0a9f40a4dee41acb3df0260502a616ac0baa8838c75c0a6
```

#### Example 2

```bash
# 1024 bit seed
~ qx entropy -s 1024

819f7ad8b044aa076af96155eb85cd3581043065476530d1f4fc0e1ea812f42e484d34f976a726fe6e4cf6269a4f5c7b311407f3657cc33205f4170d5bf2b026708eefde3c64d02571d1de6193d3ac2c03888bed613e278713d72957613e3da34b60dec43bfdd475e460d53628b5ec3c9ecfc24fadf8486461a99e396bd5181d
```