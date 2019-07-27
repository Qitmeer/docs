---
title: "txSign"
date: 2019-07-25T10:02:56+08:00
weight: 0
---

## txSign

txSign {private_key} {raw_tx}; sign rawTx

### Usage

```
qitmeer-cli blockChain txSign {private_key} {raw_tx} [flags]
```



### Alias

- txsign

- TxSign

- signRawTx

- signrawtx

- SignRawTx

### Examples

```

//txSign {private_key} {raw_tx}

txSign 2ad045c0df865c8f84479ea06adf00cbbfec705fb9402ea117ce2ef242a9d260 0100000001ff5d53a7070fa9f0a9d12af729d2cbaf355ef1173c106a84cf9ef3a46bff03b202000000ffffffff01005504790a0000001976a914627777996288556166614462639988446255776688ac000000000000000001000000000000000000000000ffffffff00
	
```

### Options

```
  -h, --help   help for txSign
```

### SEE ALSO

* [qitmeer-cli blockChain](/en/reference/qitmeer-cli/blockchain/)	 

