---
title: transaction
weight: 2
#pre: "<b>1. </b>"
# chapter: true
---

### tx-encode

encode a unsigned transaction.

```bash
~ qx tx-encode --help

Usage: qx tx-encode [-i tx-input] [-l tx-lock-time] [-o tx-output] [-v tx-version] 
  -i value
    	The set of transaction input points encoded as TXHASH:INDEX:SEQUENCE:TXTYPE. 
    	TXHASH is a Base16 transaction hash. INDEX is the 32 bit input index
    	in the context of the transaction. SEQUENCE is the optional 32 bit 
    	input sequence and defaults to the maximum value.
    	TXTYPE is type type
    	TxTypeRegular the standard tx
    	TxTypeGenesisLock the tx try to lock the genesis output to the stake pool
    	TxTypeCrossChainExport Cross chain by import tx
    	TxTypeCrossChainImport Cross chain by vm tx
    	
  -l value
    	the transaction lock time
  -o value
    	The set of transaction output data encoded as TARGET:MEER:COINID:TXTYPE. 
    	TARGET is an address (pay-to-pubkey-hash or pay-to-script-hash).
    	MEER is the 64 bit spend amount in qitmeer.COINID enum {0 => MEER,1=>ETHID}
  -v value
    	the transaction version (default 1)
```

#### Example

- TxTypeRegular

TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw (has 99.989 meer) send 9.988 meer to TnHqTCHGYPfFyNtLQfYKVf5jd4KiQkropmV, with 90 meer left, fee = 0.001.

```bash
~ qx tx-encode -i 04f6d4055fac1e17975f30e345ac8602c9fd4c54351c99af615273950fe43ee8:0:4294967295:TxTypeRegular -l 0 -o TnHqTCHGYPfFyNtLQfYKVf5jd4KiQkropmV:9.988:0:TxTypeRegular -o TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw:90:0:TxTypeRegular
0100000001e83ee40f95735261af991c35544cfdc90286ac45e3305f97171eac5f05d4f60400000000ffffffff020000807a883b000000001976a914441db1582a69878dfa83042b529ba918b74aaf1088ac0000001a7118020000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac0000000000000000c8d360630100-7b22696e707574223a7b2230223a307d2c226f7574707574223a7b2230223a302c2231223a307d7d
```



#### Set Locktime

If nLocktime is not zero and is less than 500 million, it is interpreted as block height, which means that the trade is invalid and is not relayed or included in the block chain before the specified block height.

If it exceeds 500 million, it is interpreted as a Unix era timestamp (the number of seconds since jan-1-1970), and the transaction is not valid until the specified time. The nLocktime transaction that specifies the future block or time must be held by the originating system and sent to the qitmeer network only after it is valid. If the transaction is transmitted to the network before the specified nLocktime, the first node rejects the transaction and is not relayed to other nodes. Using nLocktime is equivalent to a deferred check.

```bash
~ qx tx-encode -i 04f6d4055fac1e17975f30e345ac8602c9fd4c54351c99af615273950fe43ee8:0:4294967295:TxTypeRegular -l 1667895234 -o TnHqTCHGYPfFyNtLQfYKVf5jd4KiQkropmV:9.988:0:TxTypeRegular -o TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw:90:0:TxTypeRegular
0100000001e83ee40f95735261af991c35544cfdc90286ac45e3305f97171eac5f05d4f60400000000feffffff020000807a883b000000002004c20f6a63b17576a914441db1582a69878dfa83042b529ba918b74aaf1088ac0000001a7118020000002004c20f6a63b17576a9142421972d46cedd2283d244665a05bde2aec3446f88acc20f6a6300000000b5d860630100-7b22696e707574223a7b2230223a307d2c226f7574707574223a7b2230223a302c2231223a307d7d
```

---

### tx-decode

decode a transaction in base16 to json format.

```bash
~ qx tx-decode --help

Usage: qx tx-decode [base16_string] 
  -n string
    	decode rawtx for the target network. (mainnet, testnet, privnet) (default "mainnet")
```

#### decode testnet rawtx

- Locktime = 0

```bash
~ qx tx-decode -n testnet 0100000001e83ee40f95735261af991c35544cfdc90286ac45e3305f97171eac5f05d4f60400000000ffffffff020000807a883b000000001976a914441db1582a69878dfa83042b529ba918b74aaf1088ac0000001a7118020000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac0000000000000000c8d360630100-7b22696e707574223a7b2230223a307d2c226f7574707574223a7b2230223a302c2231223a307d7d
```

```json
{
  "txid": "2532595f10645b5550f90c60a6cedac1fd947aba26ff880f609e7c686f7e0401",
  "txhash": "cf6be2dfccf7fc24d0b448fdb92cb7be934505f15d411bce2f4faf4f95d6e79b",
  "version": 1,
  "locktime": 0,
  "expire": 0,
  "vin": [
    {
      "type": "TxTypeRegular",
      "scriptSig": {
        "asm": "",
        "hex": ""
      }
    }
  ],
  "vout": [
    {
      "coin": "MEER Asset",
      "amount": 998800000,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 441db1582a69878dfa83042b529ba918b74aaf10 OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a914441db1582a69878dfa83042b529ba918b74aaf1088ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "TnHqTCHGYPfFyNtLQfYKVf5jd4KiQkropmV"
        ]
      }
    },
    {
      "coin": "MEER Asset",
      "amount": 9000000000,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 2421972d46cedd2283d244665a05bde2aec3446f OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a9142421972d46cedd2283d244665a05bde2aec3446f88ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw"
        ]
      }
    }
  ]
}
```

- Locktime = 1667895234

```bash
~ qx tx-decode -n testnet 0100000001e83ee40f95735261af991c35544cfdc90286ac45e3305f97171eac5f05d4f60400000000feffffff020000807a883b000000002004c20f6a63b17576a914441db1582a69878dfa83042b529ba918b74aaf1088ac0000001a7118020000002004c20f6a63b17576a9142421972d46cedd2283d244665a05bde2aec3446f88acc20f6a6300000000b5d860630100-7b22696e707574223a7b2230223a307d2c226f7574707574223a7b2230223a302c2231223a307d7d
```
```jason
{
  "txid": "40c8a8fcd173ad0ec1ad75a06c3dfe1fd623821345f5417cb7562e4bf7a64aee",
  "txhash": "67acbab1d4c65ca2c1f0b6449d4d3374ff670004cf252087beaa474344e1465a",
  "version": 1,
  "locktime": 1667895234,
  "expire": 0,
  "vin": [
    {
      "type": "TxTypeRegular",
      "scriptSig": {
        "asm": "",
        "hex": ""
      }
    }
  ],
  "vout": [
    {
      "coin": "MEER Asset",
      "amount": 998800000,
      "scriptPubKey": {
        "asm": "c20f6a63 OP_CHECKLOCKTIMEVERIFY OP_DROP OP_DUP OP_HASH160 441db1582a69878dfa83042b529ba918b74aaf10 OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "04c20f6a63b17576a914441db1582a69878dfa83042b529ba918b74aaf1088ac",
        "reqSigs": 1,
        "type": "cltvpubkeyhash",
        "addresses": [
          "TnHqTCHGYPfFyNtLQfYKVf5jd4KiQkropmV"
        ]
      }
    },
    {
      "coin": "MEER Asset",
      "amount": 9000000000,
      "scriptPubKey": {
        "asm": "c20f6a63 OP_CHECKLOCKTIMEVERIFY OP_DROP OP_DUP OP_HASH160 2421972d46cedd2283d244665a05bde2aec3446f OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "04c20f6a63b17576a9142421972d46cedd2283d244665a05bde2aec3446f88ac",
        "reqSigs": 1,
        "type": "cltvpubkeyhash",
        "addresses": [
          "TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw"
        ]
      }
    }
  ]
}
```

---

### tx-sign

sign a transactions using a private key.

```bash
~ qx tx-sign --help

Usage: qx tx-sign [raw_tx_base16_string] 
  -k string
    	the ec private key to sign the raw transaction
  -n string
    	decode rawtx for the target network. (mainnet, testnet, privnet) (default "mainnet")
```

#### Example

{{% notice tip %}}
The column rawtx is not send to the node and is used as an instance only.
{{% /notice %}}

```bash
~ qx tx-sign -k e2ec07936723d6b8c054f1f6bfe2cf1c439733303e5a6f0062d54168d9265b14 -n testnet 0100000001e83ee40f95735261af991c35544cfdc90286ac45e3305f97171eac5f05d4f60400000000ffffffff020000807a883b000000001976a914441db1582a69878dfa83042b529ba918b74aaf1088ac0000001a7118020000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac0000000000000000c8d360630100-7b22696e707574223a7b2230223a307d2c226f7574707574223a7b2230223a302c2231223a307d7d

0100000001e83ee40f95735261af991c35544cfdc90286ac45e3305f97171eac5f05d4f60400000000ffffffff020000807a883b000000001976a914441db1582a69878dfa83042b529ba918b74aaf1088ac0000001a7118020000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac0000000000000000c8d36063016b483045022100981bc66c021d792f53ecb6d2b1fc001ec91f11df055b8fc78f3cf7df88e51c0102200744540c34b4c0a5ab47341f4db48668a2003c85ee8647bf7495747aff6bb5f10121036d16522df27ff0b534fc853e19e1f77fefb6c7341819574b5c83fa1e968f54e8
```
