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
    	The set of transaction input points encoded as TXHASH:INDEX:SEQUENCE:SCRIPTTYPE:[args].
    	TXHASH is a Base16 transaction hash. 
    	INDEX is the 32 bit input index in the context of the transaction. 
    	SEQUENCE is input sequence and defaults to 0xffffffff.
    	SCRIPTTYPE is unlock script type
    	- pubkeyhash PayToAddrScript(pkh)
    	- pubkey PayToAddrScript(pk)
    	- cltvpubkeyhash PayToCLTVPubKeyHashScript(pkh, args)
    	- crossimport the special script, the index need 4294967294 and sequence need 258
    	example: 
    	-i 5fdad6bb6781416b0361a10eb6183dec45fb31edcf2da10d22893ee7bb6502ca:0:4294967295:pubkeyhash
    	-i 5fdad6bb6781416b0361a10eb6183dec45fb31edcf2da10d22893ee7bb6502ca:0:4294967294:cltvpubkeyhash:1667298670
    	
  -l value
    	the transaction lock time
  -o value
    	The set of transaction output data encoded as ADDRESS:AMOUNT:COINID:SCRIPTTYPE:[args].
    	ADDRESS is an address (pay-to-pubkey-hash or pay-to-script-hash).
    	AMOUNT is the 64 bit spend amount in qitmeer.
    	COINID enum {0 => MEERA,1=>MEERB}
    	SCRIPTTYPE is lock script type
    	- pubkeyhash PayToAddrScript(pkh)
    	- pubkey PayToAddrScript(pk)
    	- cltvpubkeyhash PayToCLTVPubKeyHashScript(pkh, LOCKTIME)
    	example: 
    	-o TnTTMZANDBhjeoxbPMAVKb5sM7KuvNpRo2b:9.9999:0:pubkeyhash
    	-o TnTTMZANDBhjeoxbPMAVKb5sM7KuvNpRo2b:9.9999:0:cltvpubkeyhash:1667298670
    	
  -v value
    	the transaction version (default 1)
```

{{% notice tip %}}
The option `-l value=locktime` is the timestamp or blockheight which used to unlock a utxo that has being locked on a `locktime`. The `-l` option is the unlocking time, only affects unlocking, and only used to unlock CLTV type, which should be greater than the maximum time in the input. 
{{% /notice %}}


#### Example

- Standard meer tx

Send 2.2 meer from utxo `de9a6e1b1e03796bace7d62b50e535a534a2cd45ee806c4ea14b457c7afb9206:0 = 84.881 meer` to `TnTLC6wsg2gZH9HYuyhL1GroDyYnsDAcpAj`, fee = 0.0001

```bash
~ qx tx-encode -v 1 -i de9a6e1b1e03796bace7d62b50e535a534a2cd45ee806c4ea14b457c7afb9206:0:4294967295:pubkeyhash -l 0 -o TnTLC6wsg2gZH9HYuyhL1GroDyYnsDAcpAj:2.2:0:pubkeyhash -o TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw:82.6809:0:pubkeyhash
01000000010692fb7a7c454ba14e6c80ee45cda234a535e5502bd6e7ac6b79031e1b6e9ade00000000ffffffff02000000ef1c0d000000001976a914ac464a202e2e5567c0f44937033037e3c6855d0c88ac0000900ad1ec010000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac00000000000000005f5c6a630100-7b22696e707574223a7b2230223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d2c226f7574707574223a7b2230223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d2c2231223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d7d
```

- Unlock utxo

Spend a locked utxo, need the SEQUENCE = 4294967294.

utxo `7426dc6f02aa57b34f4f174c3085330d681acdb83e58e655b0c1dd00289f3627:0`: amount=4.998 locktime = 1667467505

```bash
~ qx tx-encode -v 1 -i 7426dc6f02aa57b34f4f174c3085330d681acdb83e58e655b0c1dd00289f3627:0:4294967294:cltvpubkeyhash:1667467505 -l 1667467505 -o TnHqTCHGYPfFyNtLQfYKVf5jd4KiQkropmV:1:0:pubkeyhash -o TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw:3.997:0:pubkeyhash
010000000127369f2800ddc1b055e6583eb8cd1a680d3385304c174f4fb357aa026fdc267400000000feffffff02000000e1f505000000001976a914441db1582a69878dfa83042b529ba918b74aaf1088ac000020f0d217000000001976a9142421972d46cedd2283d244665a05bde2aec3446f88acf188636300000000f55e6a630100-7b22696e707574223a7b2230223a7b2253637269707454797065223a31322c224c6f636b54696d65223a313636373436373530357d7d2c226f7574707574223a7b2230223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d2c2231223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d7d
```

- Cross chain export (from utxo to evm balance)

CrossChainExport, which means transferring meer from utxo(coinID=0) to evm balance(coinID=1), it will send meer from the pubkeyhash to the pubkey(pkaddr). The output coinID should be 1.

For example: 
Transfer 2.101 meer from utxo `a3e99b717f63e6ba3048399f6e182a1fd1fcc3c11d2684f65f1d23dc4c2c3255:0 (4.286 meer)` to pkaddr `Tk2ccA1wxfrXEseUCYqss7N7RbhHAprVwmZrDvodcE8qcqYxTbDTD`, 2.1849 meer left in `TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw`.

```bash
~ qx tx-encode -v 1 -i a3e99b717f63e6ba3048399f6e182a1fd1fcc3c11d2684f65f1d23dc4c2c3255:0:4294967295:pubkeyhash -l 0 -o Tk2ccA1wxfrXEseUCYqss7N7RbhHAprVwmZrDvodcE8qcqYxTbDTD:2.101:1:pubkey -o TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw:2.1849:0:pubkeyhash
010000000155322c4cdc231d5ff684261dc1c3fcd11f2a186e9f394830bae6637f719be9a300000000ffffffff02010020df850c00000000232102ad6ca4cbfbce01693f759e304bbb520fd316429deb4f4a81527d8b136901e5cdac000090e4050d000000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac00000000000000007e606a630100-7b22696e707574223a7b2230223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d2c226f7574707574223a7b2230223a7b2253637269707454797065223a312c224c6f636b54696d65223a307d2c2231223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d7d
```

- Cross chain import (from evm balance to utxo)

CrossChainImport, which is a special script, it will transfer meer from evm balance(coinID=1) to utxo(coinID=0). The input index need `4294967294` and sequence need `258`, the scripttype need `crossimport`. You can freely construct the input txhash based on the hash `0000000000000000000000000000000000000000000000000000000000000000`, but do not reuse the same hash. The output coinID should be 0.

{{% notice tip %}}
Since the CrossChainImport does not support splitting the amount, it can only transfer all the evm balances to utxo at one time. If you don't want to transfer all balances, you need to send the balances which you don't want to be transferred to anothe evm address firstly.
{{% /notice %}}

For example:

The total evm balance of the address `0xc422793dA8bd1c3eeE72023bC3488e7A4F444f12` is 12.1009 meer. Now, transfer meer from evm to `TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw`. The output amount should be 12.1008 meer, and 0.0001 meer left as fee. If your output amout is 0.0001 meer, the 12.1008 meer will be treated as fee.

```bash
~ ./qx tx-encode -v 1 -i 000000000000000000000000000000000000000000000000000000000000000a:4294967294:258:crossimport -l 0 -o TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw:12.1008:0:pubkeyhash | ./qx tx-sign -k 1c0f7568db440571712adf2e15e5c483eb939d8f509d0c00c9fd17da5beccd06 -n testnet
01000000010a00000000000000000000000000000000000000000000000000000000000000feffffff02010000010000005b2048000000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac000000000000000041646a63017f354d6b36715a51535341764868727a5a4b567064585367316274466b6b754e636b417457686672516b774e6746616231377a4a45343748473044022008065bdde40607faf64dc3ee99281fe87d280378f5b5ab8ff3b1c3ddd97290af02206b4f1d6bdd077768c63dead6fb6eb606802bd6b021340ca4bdc61f3e59e134ae01
```

{{% notice tip %}}
Note: Since the CrossImport is sending transaction from your evm address, you need to sign with the private key of the evm address(which is the child key, not master key).
{{% /notice %}}


#### Set Locktime

If nLocktime is not zero and is less than 500 million, it is interpreted as block height, which means that the trade is invalid and is not relayed or included in the block chain before the specified block height.

If it exceeds 500 million, it is interpreted as a Unix era timestamp (the number of seconds since jan-1-1970), and the transaction is not valid until the specified time. The nLocktime transaction that specifies the future block or time must be held by the originating system and sent to the qitmeer network only after it is valid. If the transaction is transmitted to the network before the specified nLocktime, the first node rejects the transaction and is not relayed to other nodes. Using nLocktime is equivalent to a deferred check.

Example: Send 1 meer from utxo `a10ba6befd031f505cedf7b34afaafcbc3f1db37cd4a804db3a0ad93a380074a:1 = 81.5808 meer` to `TnTLC6wsg2gZH9HYuyhL1GroDyYnsDAcpAj` which only can spend until the `locktime = 1667781205` arrive.

```bash
~ qx tx-encode -v 1 -i a10ba6befd031f505cedf7b34afaafcbc3f1db37cd4a804db3a0ad93a380074a:1:4294967295:pubkeyhash -l 0 -o TnTLC6wsg2gZH9HYuyhL1GroDyYnsDAcpAj:1:0:cltvpubkeyhash:1667781205 -o TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw:80.5807:0:pubkeyhash
01000000014a0780a393ada0b34d804acd37dbf1c3cbaffa4ab3f7ed5c501f03fdbea60ba101000000ffffffff02000000e1f50500000000200455526863b17576a914ac464a202e2e5567c0f44937033037e3c6855d0c88ac0000f0634ce0010000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac0000000000000000815d6a630100-7b22696e707574223a7b2230223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d2c226f7574707574223a7b2230223a7b2253637269707454797065223a31322c224c6f636b54696d65223a307d2c2231223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d7d
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
~ qx tx-decode -n testnet 01000000010692fb7a7c454ba14e6c80ee45cda234a535e5502bd6e7ac6b79031e1b6e9ade00000000ffffffff02000000ef1c0d000000001976a914ac464a202e2e5567c0f44937033037e3c6855d0c88ac0000900ad1ec010000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac00000000000000005f5c6a630100-7b22696e707574223a7b2230223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d2c226f7574707574223a7b2230223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d2c2231223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d7d
```

```json
{
  "txid": "da309d7a80dfeeecb8aae66812d233fa189a0d7d5cdf901e959976cda4b87532",
  "txhash": "45cfec28484bf936f02a7d9e9dbdc333fa16aedfc4ee1f4f082ca54a769558fc",
  "version": 1,
  "locktime": 0,
  "expire": 0,
  "vin": [
    {
      "type": "pubkeyhash",
      "scriptSig": {
        "asm": "",
        "hex": ""
      }
    }
  ],
  "vout": [
    {
      "coin": "MEER Asset",
      "amount": 220000000,
      "scriptPubKey": {
        "asm": "OP_DUP OP_HASH160 ac464a202e2e5567c0f44937033037e3c6855d0c OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "76a914ac464a202e2e5567c0f44937033037e3c6855d0c88ac",
        "reqSigs": 1,
        "type": "pubkeyhash",
        "addresses": [
          "TnTLC6wsg2gZH9HYuyhL1GroDyYnsDAcpAj"
        ]
      }
    },
    {
      "coin": "MEER Asset",
      "amount": 8268090000,
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

- Locktime = 1667781205

```bash
~ qx tx-decode -n testnet 01000000014a0780a393ada0b34d804acd37dbf1c3cbaffa4ab3f7ed5c501f03fdbea60ba101000000ffffffff02000000e1f50500000000200455526863b17576a914ac464a202e2e5567c0f44937033037e3c6855d0c88ac0000f0634ce0010000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac0000000000000000815d6a630100-7b22696e707574223a7b2230223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d2c226f7574707574223a7b2230223a7b2253637269707454797065223a31322c224c6f636b54696d65223a307d2c2231223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d7d
```
```json
{
  "txid": "6838596d19e059914f4e2a1320e5aac9223df27ff26758163088125684d5d0fb",
  "txhash": "415692499a394ffee8a2665ea4b34d74d52f8aa5e7d420b1282d5b6fe52fa836",
  "version": 1,
  "locktime": 0,
  "expire": 0,
  "vin": [
    {
      "type": "pubkeyhash",
      "scriptSig": {
        "asm": "",
        "hex": ""
      }
    }
  ],
  "vout": [
    {
      "coin": "MEER Asset",
      "amount": 100000000,
      "scriptPubKey": {
        "asm": "55526863 OP_CHECKLOCKTIMEVERIFY OP_DROP OP_DUP OP_HASH160 ac464a202e2e5567c0f44937033037e3c6855d0c OP_EQUALVERIFY OP_CHECKSIG",
        "hex": "0455526863b17576a914ac464a202e2e5567c0f44937033037e3c6855d0c88ac",
        "reqSigs": 1,
        "type": "cltvpubkeyhash",
        "addresses": [
          "TnTLC6wsg2gZH9HYuyhL1GroDyYnsDAcpAj"
        ]
      }
    },
    {
      "coin": "MEER Asset",
      "amount": 8058070000,
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

- Unlock utxo

```bash
~ qx tx-decode -n testnet 010000000127369f2800ddc1b055e6583eb8cd1a680d3385304c174f4fb357aa026fdc267400000000feffffff02000000e1f505000000001976a914441db1582a69878dfa83042b529ba918b74aaf1088ac000020f0d217000000001976a9142421972d46cedd2283d244665a05bde2aec3446f88acf188636300000000f55e6a630100-7b22696e707574223a7b2230223a7b2253637269707454797065223a31322c224c6f636b54696d65223a313636373436373530357d7d2c226f7574707574223a7b2230223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d2c2231223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d7d
```
```bash
{
  "txid": "262182c2aedf5a8ad3b11f0279821a7ac12525cf1c1a447b24902d9ae33e4245",
  "txhash": "584818c169a23dcef8a2aa1674b9901423f7d60c1665f49a433bc0f4212446f0",
  "version": 1,
  "locktime": 1667467505,
  "expire": 0,
  "vin": [
    {
      "type": "cltvpubkeyhash",
      "scriptSig": {
        "asm": "",
        "hex": ""
      }
    }
  ],
  "vout": [
    {
      "coin": "MEER Asset",
      "amount": 100000000,
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
      "amount": 399700000,
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

- Cross chain export (from utxo to evm balance)

```bash
~ ./qx tx-encode -v 1 -i a3e99b717f63e6ba3048399f6e182a1fd1fcc3c11d2684f65f1d23dc4c2c3255:0:4294967295:pubkeyhash -l 0 -o Tk2ccA1wxfrXEseUCYqss7N7RbhHAprVwmZrDvodcE8qcqYxTbDTD:2.101:1:pubkey -o TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw:2.1849:0:pubkeyhash | ./qx tx-sign -k e2ec07936723d6b8c054f1f6bfe2cf1c439733303e5a6f0062d54168d9265b14 -n testnet | ./qx tx-decode -n testnet
```
```bash
{
  "txid": "967367665c31084bf248d8fd46953ff2330edb47965df2f71e7117bfcd836c5b",
  "txhash": "aee2ccdd93fd9099b3394b314354c43472e5816d1314f11c3489d45fc2e48726",
  "version": 1,
  "locktime": 0,
  "expire": 0,
  "vin": [
    {
      "txid": "a3e99b717f63e6ba3048399f6e182a1fd1fcc3c11d2684f65f1d23dc4c2c3255",
      "vout": 0,
      "sequence": 4294967295,
      "scriptSig": {
        "asm": "30440220417af9e12ef7140206abcf6194b5de63be5bb63309e10f9d2a5d0a63093b7d3b02205ba49ea57dfcd8a9e14c49a6bdd7ae6acabc082f0f45b61eabbaca0f5819d26001 036d16522df27ff0b534fc853e19e1f77fefb6c7341819574b5c83fa1e968f54e8",
        "hex": "4730440220417af9e12ef7140206abcf6194b5de63be5bb63309e10f9d2a5d0a63093b7d3b02205ba49ea57dfcd8a9e14c49a6bdd7ae6acabc082f0f45b61eabbaca0f5819d2600121036d16522df27ff0b534fc853e19e1f77fefb6c7341819574b5c83fa1e968f54e8"
      }
    }
  ],
  "vout": [
    {
      "coin": "MEER Balance",
      "coinid": 1,
      "amount": 210100000,
      "scriptPubKey": {
        "addresses": [
          "Tk2ccA1wxfrXEseUCYqss7N7RbhHAprVwmZrDvodcE8qcqYxTbDTD"
        ]
      },
      "to": "0xc422793dA8bd1c3eeE72023bC3488e7A4F444f12"
    },
    {
      "coin": "MEER Asset",
      "amount": 218490000,
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


- Cross chain import (from evm balance to utxo)

```bash
~ ./qx tx-encode -v 1 -i 000000000000000000000000000000000000000000000000000000000000000a:4294967294:258:crossimport -l 0 -o TnEvLExwzew6LPL13yXmWKnnZxD1c5Lr8Tw:12.1008:0:pubkeyhash | ./qx tx-sign -k 1c0f7568db440571712adf2e15e5c483eb939d8f509d0c00c9fd17da5beccd06 -n testnet | ./qx tx-decode -n testnet

```
```bash
{
  "txid": "f4b5a2c60b2d8270d65764f9db8476f7bff0ffcd85ff20751cbbe2c0a19d3004",
  "txhash": "6f8364f1f8a36a88d22be78f9d25938d788750e0322a3bb21889f763bfc520fa",
  "version": 1,
  "locktime": 0,
  "expire": 0,
  "vin": [
    {
      "from": "0xc422793dA8bd1c3eeE72023bC3488e7A4F444f12",
      "value": 1210080000
    }
  ],
  "vout": [
    {
      "coin": "MEER Asset",
      "amount": 1210080000,
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
~ qx tx-sign -k e2ec07936723d6b8c054f1f6bfe2cf1c439733303e5a6f0062d54168d9265b14 -n testnet 01000000010692fb7a7c454ba14e6c80ee45cda234a535e5502bd6e7ac6b79031e1b6e9ade00000000ffffffff02000000ef1c0d000000001976a914ac464a202e2e5567c0f44937033037e3c6855d0c88ac0000900ad1ec010000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac00000000000000005f5c6a630100-7b22696e707574223a7b2230223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d2c226f7574707574223a7b2230223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d2c2231223a7b2253637269707454797065223a322c224c6f636b54696d65223a307d7d7d

01000000010692fb7a7c454ba14e6c80ee45cda234a535e5502bd6e7ac6b79031e1b6e9ade00000000ffffffff02000000ef1c0d000000001976a914ac464a202e2e5567c0f44937033037e3c6855d0c88ac0000900ad1ec010000001976a9142421972d46cedd2283d244665a05bde2aec3446f88ac00000000000000006b816763016a47304402205c4948ce286eaf4583e4d3473ea7f1724181bb19cef3454ae22097da3e4c5bd602207267d0382069758a2478439098e0b3eff3c9c53606c9aa72fcbd938d6f9ded230121036d16522df27ff0b534fc853e19e1f77fefb6c7341819574b5c83fa1e968f54e8
```
