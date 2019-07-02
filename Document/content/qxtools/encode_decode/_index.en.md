---
title: Encode and Decode
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---


## Encoding Commands

Encode/Decocde Qitmeer address & private/pubkey

#### base58-encode

- encode a base16 string to a base58 string

##### Example

```bash
~ qx base58-decode RmCYoUMqKZopUkai2YhUFHR9UeqjeyjTAgW
```

```bash
# base16 string
0df144d959afb6db4ad730a6e2c0daf46ceeb98c53a059cd6527
```

---

#### base58-decode

- decode a base58 string to a base16 string

##### Example

```bash
~ qx base58-decode 1234567890abcdef
```

```bash
# base58 string
43c9JGZmRvE
```

---

#### base58check-encode

- base16 string into Qitmeer or BTC address.

```bash
~ qx base58check-encode
Usage: qx base58check-encode [-v <ver>] [hexstring]
  -a string
    base58check hasher
  -c int
    base58check checksum size (default 4)
  -v version
    base58check version [mainnet|testnet|privnet] (default privnet)
```

##### Example

```bash
# create qitmeer privnet address by base16
~ qx base58check-encode c1c3092d17c917c2799c041aeaeac18822772149

# base58 string
RmPwHCuC2m6gvz9TnVLapHySk1ZU72FTSru
```

```bash
# create btc testnet address by base16
~ qx base58check-encode -v btctestnet c1c3092d17c917c2799c041aeaeac18822772149

# base58 string
myBUMQTmZGK8yKLDranjSQEHbCYCaaywQD
```
