---
title: HD
weight: 2
#pre: "<b>1. </b>"
# chapter: true
---

### hd-new

create a new HD(BIP32) private key from an entropy (seed).

```bash
~ qx hd-new --help

Usage: qx hd-new [-v version] [entropy]
    -v version
        The HD(BIP32) version [mainnet|testnet|privnet|bip32] (default testnet)
```

#### default

```bash
~ qx hd-new 4ec6a3a135aba433b0d0ae5ec31d69c26eb3bd5ac532496529660f61c674d99e

tprvZUo1ZuEfLLFWgE3tcS9LfwarRt5Pjy1xH4y3yfEarLtP8F7EL2ncFqvS4VW1yY2cUfmA94c9pg563PHGbzS8w96pzGJUu2pipGgckRgnvL7
```

#### use -v parameter

```bash
~ qx hd-new -v mainnet 4ec6a3a135aba433b0d0ae5ec31d69c26eb3bd5ac532496529660f61c674d99e

nprvxSuUxcjDNFNkbPm9y9pMYE9yT4F3MrU8QdsGjgmLA7RLghzj4eKFRYskuqVtYUorJE4iUej8BwgXReSV6kTwNsZKP6iwT5iMCVqiMsUKJwz
```

---

### hd-to-ec

convert the HD (BIP32) format private/public key to a EC private/public key.

```bash
~ qx hd-to-ec --help

Usage: qx hd-to-ec [hd_private_key or hd_public_key]
    -v version
        The HD(BIP32) version [mainnet|testnet|privnet|bip32] (default testnet)
```

#### private key

```bash
~ qx hd-to-ec tprvZUo1ZuEfLLFWgE3tcS9LfwarRt5Pjy1xH4y3yfEarLtP8F7EL2ncFqvS4VW1yY2cUfmA94c9pg563PHGbzS8w96pzGJUu2pipGgckRgnvL7

3f2314d615696244ea14e46e43322842b3e09333e62c59c4160220a52bdf6239
```

#### mainnet private key

```bash
~ qx hd-to-ec -v mainnet nprvxSuUxcjDNFNkbPm9y9pMYE9yT4F3MrU8QdsGjgmLA7RLghzj4eKFRYskuqVtYUorJE4iUej8BwgXReSV6kTwNsZKP6iwT5iMCVqiMsUKJwz

3f2314d615696244ea14e46e43322842b3e09333e62c59c4160220a52bdf6239
```

#### public key

```bash
~ qx hd-to-ec tpubVhnMyQmZAhooti8MiTgM35Xayuut9RjoeHten3eCQgRN13SNsa6roeEuunaefhqrpVPoxKTxpjuGpsWSTjFeoq9L3kgcwntCbHHBL4g2R69

034d09a78b756b80e02200a94d2e24762432518fb29a4a3fd0adf0414e71554d70

# equal to
~ qx ec-new 4ec6a3a135aba433b0d0ae5ec31d69c26eb3bd5ac532496529660f61c674d99e | qx ec-to-public
```

---

### hd-to-public

derive the HD (BIP32) public key from a HD private key.

```bash
~ qx hd-new --help

Usage: qx hd-to-public [hd_private_key]
    -v version
        The HD(BIP32) version [mainnet|testnet|privnet|bip32] (default testnet)
```

#### Example

need HD private key.

```bash
~ qx hd-to-public tprvZUo1ZuEfLLFWgE3tcS9LfwarRt5Pjy1xH4y3yfEarLtP8F7EL2ncFqvS4VW1yY2cUfmA94c9pg563PHGbzS8w96pzGJUu2pipGgckRgnvL7

tpubVhnMyQmZAhooti8MiTgM35Xayuut9RjoeHten3eCQgRN13SNsa6roeEuunaefhqrpVPoxKTxpjuGpsWSTjFeoq9L3kgcwntCbHHBL4g2R69
```

#### Error

```bash
~ qx hd-to-public tpubVhnMyQmZAhooti8MiTgM35Xayuut9RjoeHten3eCQgRN13SNsa6roeEuunaefhqrpVPoxKTxpjuGpsWSTjFeoq9L3kgcwntCbHHBL4g2R69

Qx Error : "tpubVhnMyQmZAhooti8MiTgM35X...BL4g2R69 is not a HD (BIP32) private key"
```

---

### hd-decode

decode a HD (BIP32) private/public key serialization format.

```bash
~ qx hd-decode --help

Usage: qx hd-decode [hd_private_key or hd_public_key]
```

#### Example 1

```bash
~ qx hd-decode tpubVhnMyQmZAhooti8MiTgM35Xayuut9RjoeHten3eCQgRN13SNsa6roeEuunaefhqrpVPoxKTxpjuGpsWSTjFeoq9L3kgcwntCbHHBL4g2R69
    version : 043587d1 (qx testnet)
    depth : 00
    parent fp : 00000000
    hardened : false
    child num : 0 (00000000)
    chain code : f1c00ea9eb51966589c10edc92036250b18141a0faffaa89cfcec91de12eaa9c
    pub key : [03][4d09a78b756b80e02200a94d2e24762432518fb29a4a3fd0adf0414e71554d70] y=odd
    checksum : 136734c2
    hex : 043587d1000000000000000000f1c00ea9eb51966589c10edc92036250b18141a0faffaa89cfcec91de12eaa9c034d09a78b756b80e02200a94d2e24762432518fb29a4a3fd0adf0414e71554d70136734c2
    base58 : tpubVhnMyQmZAhooti8MiTgM35Xayuut9RjoeHten3eCQgRN13SNsa6roeEuunaefhqrpVPoxKTxpjuGpsWSTjFeoq9L3kgcwntCbHHBL4g2R69
```

### hd-derive

Derive a child HD (BIP32) key from another HD public or private key.

```bash
~ qx hd-derive --help

Usage: qx hd-derive [hd_private_key or hd_public_key] 
    -d    create a hardened key
    -i index
        The HD index
    -p path
        hd derive path. ex: m/44'/0'/0'/0
    -v version
        The HD(BIP32) version [mainnet|testnet|privnet|bip32] (default testnet)
```

#### Example 2

```bash
~ qx hd-derive tpubVhnMyQmZAhooti8MiTgM35Xayuut9RjoeHten3eCQgRN13SNsa6roeEuunaefhqrpVPoxKTxpjuGpsWSTjFeoq9L3kgcwntCbHHBL4g2R69

tpubVki4bHPyoZ3URwa1G8WHiB6rxsUVzQreGPF71dKvATNByoP7niivvY4TCsKV374kTas45z6G1ZygNBj1sJo8vRcsDogp7Fb1XnmQtwLAibU
```

