---
title: Pool Stratum Protocol V1.0
weight: 5
#pre: "<b>1. </b>"
# chapter: true
---

**Q:** POW HASH

**A**: POW Hash [GOlang HashMeerXKeccakV1](https://github.com/Qitmeer/qitmeer/blob/master/common/hash/hashfuncs_meer_crypto.go#L11)

[C CODE HashMeerXKeccakV1](https://github.com/Qitmeer/qitmeer/blob/0.10-dev/cmd/miner/asic/meer/algo_meer.c)

**Q:** Pool Stratum Protocol

**A**: `stateRoot` can get from `GetBlockTemplate` RPC
    
    {"id": null,"method": "mining.notify","params": [
       "job_id",
       "prev_hash",
       "cb1",
       "cb2",
       "cb3",
       "cb4",
       "txs",
       "version",
       "nBits",
       "nTime",
       "stateRoot", // 
       "cleanJobs",
       ]}
       
**Q:** Pow Header

**A**: [POW_HEADER](https://github.com/Qitmeer/qitmeer/blob/0.10-dev/core/types/block.go#L134)

    header = s.Version + prevHash + merkleRootStr2 + stateRoot + s.Nbits + hex.EncodeToString(ntime) +
         hex.EncodeToString([]byte{uint8(s.PowType)}) + nonceStr
       
**Q:** Change Of CoinBase 

**A**: 1. [Coinbase amount struct] https://github.com/Qitmeer/qitmeer-miner/blob/master/symbols/qitmeer/coinbase/common.go#L104-L108

    example
    old : amount : 12000000000
    new : amount { Type : 0, Value: 12000000000}
    
 2. [CoinbaseFee](https://github.com/Qitmeer/qitmeer-miner/blob/master/symbols/qitmeer/coinbase_tx.go#L106)
 3. [Coinbase add extra output](https://github.com/Qitmeer/qitmeer-miner/blob/master/symbols/qitmeer/coinbase/common.go#L138)
        
**Q:** Change Of Miner 

**A**: Submit Data

        {PoolUser, jobID, ExtraNonce2, timestampStr,nonceStr}
 
    