---
title: Qitmeer Java SDK
weight: 1
---

# qitmeer-java-sdk

1. Connect RPC
```java
private static Qitmeer q = new Qitmeer("https://127.0.0.1:1234", "", "");
```

2. Get block count
```java
ServiceResult result = q.getBlockCount();
if (result.code == 0) {
    System.out.println("getBlockCount:\r\n" + result.data.toString());
} else {
    System.out.println("getBlockCountFaild:\r\n" + result.msg);
}
```

3. Get block by order
```java
ServiceResult result = q.getBlockByOrder(1, true);
if (result.code == 0) {
    JSONObject recJson = JSON.parseObject(result.data.toString());
    Block b = JSON.toJavaObject(recJson, Block.class);
    System.out.println("getBlockByOrder:\r\n" + b.getHash());
} else {
    System.out.println("getBlockByOrderFaild:\r\n" + result.msg);
}
```

4. Get block by hash
```java
ServiceResult result = q.getBlockByHash("", true);
if (result.code == 0) {
    JSONObject recJson = JSON.parseObject(result.data.toString());
    Block b = JSON.toJavaObject(recJson, Block.class);
    System.out.println("getBlockByhash:\r\n" + b.getHash());
} else {
    System.out.println("getBlockByhashFaild:\r\n" + result.msg);
}
```

4. Get block header by hash
```java
ServiceResult result = q.getBlockHeader("", true);
if (result.code == 0) {
    JSONObject recJson = JSON.parseObject(result.data.toString());
    BlockHeader b = JSON.toJavaObject(recJson, BlockHeader.class);
    System.out.println("getBlockHeader:\r\n" + b.getHash());
} else {
    System.out.println("getBlockHeaderFaild:\r\n" + result.msg);
}
```

5. Get block weight by hash
```java
ServiceResult result = q.getBlockWeight("");
if (result.code == 0) {
    System.out.println("getBlockWeight:\r\n" + result.data.toString());
} else {
    System.out.println("getBlockWeightFaild:\r\n" + result.msg);
}
```

6. Get block hash by order
```java
ServiceResult result = q.getBlockHash(1);
if (result.code == 0) {
    System.out.println("getBlockHash:\r\n" + result.data.toString());
} else {
    System.out.println("getBlockHashFaild:\r\n" + result.msg);
}
```

7. Get best block hash
```java
ServiceResult result = q.getBestBlockHash();
if (result.code == 0) {
    System.out.println("getBestBlockHash:\r\n" + result.data.toString());
} else {
    System.out.println("getBestBlockHashFaild:\r\n" + result.msg);
}
```

8. Block is on main chain
```java
ServiceResult result = q.isOnMainChain(""]);
if (result.code == 0) {
    System.out.println("isOnMainChain:\r\n" + result.data.toString());
} else {
    System.out.println("isOnMainChainFaild:\r\n" + result.msg);
}
```

9. Get utxo
```java
ServiceResult result = q.getUtxo("bae58ff3e0870938e241224fc8736998f5e8f6cf6423c383493bf13133e4d37d", 0, true);
if (result.code == 0) {
    JSONObject recJson = JSON.parseObject(result.data.toString());
    Utxo b = JSON.toJavaObject(recJson, Utxo.class);
    System.out.println("getUtxo:\r\n" + b.getCoinbase());
} else {
    System.out.println("getUtxoFaild:\r\n" + result.msg);
}
```

10. Create Raw Transaction
```java
FromTx u = new FromTx();
u.setTxid("019edb774482a9f619ca02f949881c2c9616a48e014ad27668ee5e56b64182f9");
u.setVout(0);
List<FromTx> list = new ArrayList<>();
list.add(u);
ServiceResult result = q.createRawTransaction(list, "RmQb2VrPtd9nftMvKtRMxN297dzN5VydmMJ", 10, 0);
if (result.code == 0) {
    System.out.println("createRawTransaction:\r\n" + result.data.toString());
} else {
    System.out.println("createRawTransactionFaild:\r\n" + result.msg);
}
```

11. Decode Raw Transaction
```java
ServiceResult result = q.decodeRawTransaction("0100000001f98241b6565eee6876d24a018ea416962c1c8849f902ca19f6a9824477db9e0100000000ffffffff0100000a000000000000001976a9149887f352a02c4e60d99bcd2eab33c8b7b0198b0488ac00000000000000008214a3600100");
if (result.code == 0) {
    System.out.println("decodeRawTransaction:\r\n" + result.data.toString());
} else {
    System.out.println("decodeRawTransactionFaild:\r\n" + result.msg);
}
```

12. Get Raw Transaction By TxId
```java
ServiceResult result = q.getRawTransaction("bae58ff3e0870938e241224fc8736998f5e8f6cf6423c383493bf13133e4d37d", true);
if (result.code == 0) {
    JSONObject recJson = JSON.parseObject(result.data.toString());
    TxRawResult b = JSON.toJavaObject(recJson, TxRawResult.class);
    System.out.println("getRawTransaction:\r\n" + b.getTxid());
} else {
    System.out.println("getRawTransactionFaild:\r\n" + result.msg);
}
```

13. Send Raw Transaction
```java
ServiceResult result = q.sendRawTransaction("0100000001f98241b6565eee6876d24a018ea416962c1c8849f902ca19f6a9824477db9e0100000000ffffffff0178000000000000001976a914bd4d1888cb054b2755d65d93c356573e4d283ead88ac00000000000000000100", true);
if (result.code == 0) {
    JSONObject recJson = JSON.parseObject(result.data.toString());
    Utxo b = JSON.toJavaObject(recJson, Utxo.class);
    System.out.println("sendRawTransaction:\r\n" + result.data.toString());

} else {
    System.out.println("sendRawTransactionFaild:\r\n" + result.msg);
}
```

14. Get Peer Info
```java
ServiceResult result = q.getPeerInfo();
if (result.code == 0) {
    List<PeerInfo> list = JSON.parseArray(result.data.toString(), PeerInfo.class);
    System.out.println("getPeerInfo:\r\n" + list.size());
} else {
    System.out.println("getPeerInfoFaild:\r\n" + result.msg);
}
```

15. Get Node Info
```java
ServiceResult result = q.getNodeInfo();
if (result.code == 0) {
    JSONObject recJson = JSON.parseObject(result.data.toString());
    NodeInfo b = JSON.toJavaObject(recJson, NodeInfo.class);
    System.out.println("getNodeInfo:\r\n" + b.getUUID());
} else {
    System.out.println("getNodeInfoFaild:\r\n" + result.msg);
}
```
