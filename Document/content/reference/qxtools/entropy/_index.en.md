---
title: Entropy and Mnemoic
weight: 3
#pre: "<b>1. </b>"
# chapter: true
---

```bash
entropy (seed) & mnemoic & hd & ec
    entropy               generate a cryptographically secure pseudorandom entropy (seed).
    hd-new                create a new HD(BIP32) private key from an entropy (seed).
    hd-to-ec              convert the HD (BIP32) format private/public key to a EC private/public key.
    hd-to-public          derive the HD (BIP32) public key from a HD private key.
    hd-decode             decode a HD (BIP32) private/public key serialization format.
    hd-derive             Derive a child HD (BIP32) key from another HD public or private key.
    mnemonic-new          create a mnemonic world-list (BIP39) from an entropy.
    mnemonic-to-entropy   return back to the entropy (the random seed) from a mnemonic world list (BIP39).
    mnemonic-to-seed      convert a mnemonic world-list (BIP39) to its 512 bits seed.
    ec-new                create a new EC private key from an entropy (seed).
    ec-to-public          derive the EC public key from an EC private key (the compressed format by default ).
    ec-to-wif             convert an EC private key to a WIF, associates with the compressed public key by default.
    wif-to-ec             convert a WIF private key to an EC private key.
    wif-to-public         derive the EC public key from a WIF private key.
```