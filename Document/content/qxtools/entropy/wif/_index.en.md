---
title: WIF
weight: 5
#pre: "<b>1. </b>"
# chapter: true
---

### wif-to-ec

convert a WIF private key to an EC private key.

```bash
~ qx wif-to-ec --help

Usage: qx wif-to-ec [WIF]
```

#### Example

```bash
~ qx wif-to-ec KyLSXswbDdBfrJoN6nPc8kPZJHEF5cBYey7f77dfnTFwGVEw1XGQ

3f2314d615696244ea14e46e43322842b3e09333e62c59c4160220a52bdf6239
```

---

### wif-to-public

derive the EC public key from a WIF private key.

```bash
~ qx wif-to-public --help

Usage: qx wif-to-public [WIF]
    -u   using the uncompressed public key format
```

#### compressed

```bash
~ qx wif-to-public KyLSXswbDdBfrJoN6nPc8kPZJHEF5cBYey7f77dfnTFwGVEw1XGQ

034d09a78b756b80e02200a94d2e24762432518fb29a4a3fd0adf0414e71554d70
```

#### uncompressed

```bash
~ qx wif-to-public -u KyLSXswbDdBfrJoN6nPc8kPZJHEF5cBYey7f77dfnTFwGVEw1XGQ

044d09a78b756b80e02200a94d2e24762432518fb29a4a3fd0adf0414e71554d701df9f31658a5578a8ded7ef2c681033ce0037823f3ed308c06ae7b1b06ce070f
```