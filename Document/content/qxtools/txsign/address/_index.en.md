---
title: address
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

### ec-to-addr

convert an **EC public key** to a paymant address. default is qx address.

```bash
~ qx ec-to-addr --help

Usage: qx ec-to-addr [ec_public_key]
    -v version
       base58check version [mainnet|testnet|privnet] (default testnet)
```

#### creat testnet address

```bash
~ qx ec-to-addr 034d09a78b756b80e02200a94d2e24762432518fb29a4a3fd0adf0414e71554d70

TmPip5CkA4e3fBRp7eo9onDYfVnba547uts

# be equivalent to
~ qx ec-to-public 3f2314d615696244ea14e46e43322842b3e09333e62c59c4160220a52bdf6239 | qx ec-to-addr
```

#### creat mainnet address

```bash
~ qx ec-to-addr -v mainnet 034d09a78b756b80e02200a94d2e24762432518fb29a4a3fd0adf0414e71554d70

NmH2v9uqS9ZwwXvHf1K129pJSi5qTSpXAv6
```