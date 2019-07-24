---
title: base58check
weight: 2
#pre: "<b>1. </b>"
# chapter: true
---

### base58check-encode

base16 string into Qitmeer or BTC address.

```bash
~ qx base58check-encode

Usage: qx base58check-encode [-v <ver>] [hexstring]
    -a string
        base58check hasher
    -c int
        base58check checksum size (default 4)
    -m string
        base58check encode mode : [qx|btc] (default "qx")
    -v version
        base58check version [mainnet|testnet|privnet] (default testnet)
```

#### Example 1

```bash
# create qitmeer privnet address by base16
~ qx base58check-encode c1c3092d17c917c2799c041aeaeac18822772149

# base58 string
TmgcbmHLHxEc9LQkpZaqvSD76uLviSJLxjG
```

#### Example 2

```bash
# create qitmeer testnet address by base16
~ qx base58check-encode -v privnet c1c3092d17c917c2799c041aeaeac18822772149

# base58 string
RmPwHCuC2m6gvz9TnVLapHySk1ZU72FTSru
```

#### Example 3

BTC type addresses can be created using -m and -v

*BTC Address version*

| network | pubKeyHash | scriptHash |
| --- | --- | --- |
|mainnet|00|05|
|testnet|6f|c4|

```bash
# create btc address by base16
~ qx base58check-encode -m btc -v 00 c1c3092d17c917c2799c041aeaeac18822772149

# base58 string
1JfX4MNnkEstCCrc91pMcV1xjCwVgyAHwT
```

#### Example 4

Different address types can be created using different hashers, such as double sha256 hasher for BTC and double blake2b256 for HLC

```bash
# create HLC address by base16
~ qx base58check-encode -a dblake2b256 c1c3092d17c917c2799c041aeaeac18822772149

# base58 string
TmgcbmHLHxEc9LQkpZaqvSD76uLviSJLxjG

# equal to
~ qx base58check-encode c1c3092d17c917c2799c041aeaeac18822772149

```

----

### base58check-decode

decode a base58check string.

```bash
~ qx base58check-decode

Usage: qx base58check-decode [hexstring]
    -a hasher
        base58check hasher
    -cs size
        base58check checksum size (default 4)
    -d  show decode details
    -m mode
        base58check decode mode: [qx|btc] (default "qx")
    -vs size
        base58check version size (default 2)
```

#### Example 5

```bash
# decode qitmeer privnet address by base58
~ qx base58check-decode RmPwHCuC2m6gvz9TnVLapHySk1ZU72FTSru

# base58 string
c1c3092d17c917c2799c041aeaeac18822772149
```

#### Example 6

-b show decode details

```bash
~ qx base58check-decode -d RmPwHCuC2m6gvz9TnVLapHySk1ZU72FTSru

mode    : qx
version : 0df1 (hex) 3569 (BE) 61709 (LE)
payload : c1c3092d17c917c2799c041aeaeac18822772149
checksum: b8769d62 (hex) 3094781282 (BE) 1654486712 (LE)
```

#### Example 7

use `-m btc` decode BTC address

```bash
# decode btc address by base58
~ qx base58check-decode -d -m btc 1JfX4MNnkEstCCrc91pMcV1xjCwVgyAHwT

mode    : btc
version : 0000 (hex) 0 (BE) 0 (LE)
payload : c1c3092d17c917c2799c041aeaeac18822772149
checksum: a75521de (hex) 2807374302 (BE) 3726726567 (LE)
```