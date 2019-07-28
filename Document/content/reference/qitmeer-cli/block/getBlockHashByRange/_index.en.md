---
title: "getBlockHashByRange"
date: 2019-07-29T00:38:09+08:00
weight: 0
---

## getBlockHashByRange

getBlockHashByRange {start} {end};Return the hash range of block from 'start' to 'end'(exclude self)

### Usage

```
qitmeer-cli getBlockHashByRange [flags]
```


	getBlockHashByRange {start} {end};Return the hash range of block from 'start' to 'end'(exclude self)
	if 'end' is equal to zero, 'start' is the number that from the last block to the Gen
	if 'start' is greater than or equal to 'end', it will just return the hash of 'start'

### Alias

- getblockhashbyrange

- GetBlockHashByRange

- getBlockhashByRange

- gethash

### Examples

```

getBlockHashByRange 5 22
	
```

### Options

```
  -h, --help   help for getBlockHashByRange
```

### SEE ALSO

* [qitmeer-cli block](/en/reference/qitmeer-cli/block/)	 

