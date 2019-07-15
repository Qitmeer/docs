---
title: blake hash
weight: 2
#pre: "<b>1. </b>"
# chapter: true
---

Perform a **blake2b256** or **blake2b512** or **blake256** of Base16 data.

### blake2b256

calculate Blake2b 256 hash of a base16 data.

```bash
~ qx blake2b256 --help

Usage: qx blak2b256 [hexstring]
```

#### Example

```bash
~ qx blake2b256 900df00d

c2cb5ef4138047b1ca42ce0bed2a2ce7d23768341ff52e6a9e2516257a1d2af9
```

----

### blake2b512

calculate Blake2b 512 hash of a base16 data.

```bash
~ qx blake2b512 --help

Usage: qx blake2b512 [hexstring]
```

#### Example 1

```bash
~ qx blake2b512 900df00d

36b65c58935fcf08307da04ba74bef658958e16a864c6a1a7bcec8fe5a82322f7c06424b70a4f25efc7e6493395562e6bebbe90e41c372dfda948506c54e4cdc
```

----

### blake256

calculate blake256 hash of a base16 data.

```bash
~ qx blake256 --help

Usage: qx blake256 [hexstring]
```

#### Example 2

```bash
~ qx blake256 900df00d

bedb342806616f3866179dab458f5f8a29bac652142689bf59a34136bc8e6d69
```
