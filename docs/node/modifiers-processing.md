# Ergo Modifiers Processing


This section describes the processing algorithm for Ergo modifiers in all security modes. Unlike most blockchain systems, Ergo has the following types of modifiers: 



**In-memory**

*  Transaction - in-memory modifier.
*  TransactionIdsForHeader - ids of transactions in concrete block.
*  UTXOSnapshotManifest - ids of UTXO chunks and

**Persistent**

*  BlockTransactions - Sequence of transactions, corresponding to 1 block.
*  ADProofs - proof of transaction correctness relative to corresponding UTXO.
*  Header, that contains data required to verify PoW, link to previous block, state root hash and root hash to it's payload (BlockTransactions, ADProofs, Interlinks ...).
*  UTXOSnapshotChunk - part of UTXO.
*  PoPoWProof

Ergo has the following parameters that determine a concrete security regime:

*  ADState: Boolean - keep state roothash only.
*  VerifyTransactions: Boolean - download block transactions and verify them (requires BlocksToKeep == 0 if disabled).
*  PoPoWBootstrap: Boolean - download PoPoW proof only.
*  BlocksToKeep: Int - number of last blocks to keep with transactions; for all other blocks, it keeps header only. Keep all blocks from genesis if negative.
*  MinimalSuffix: Int - minimal suffix size for PoPoW proof (may be a pre-defined constant).


```java
if(VerifyTransactions == false) require(BlocksToKeep == 0)
```

Mode from `multimode.md` can be determined as follows:

```java
mode = if(ADState == false && VerifyTransactions == true
&& PoPoWBootstrap == false && BlocksToKeep < 0) "full"
else if(ADState == false && VerifyTransactions == true
&& PoPoWBootstrap == false && BlocksToKeep >= 0) "pruned-full"
else if(ADState == true && VerifyTransactions == true
&& PoPoWBootstrap == false) "light-full"
else if(ADState == true && VerifyTransactions == false
&& PoPoWBootstrap == true && BlocksToKeep == 0) "light-spv"
else if(ADState == true && VerifyTransactions == true
&& PoPoWBootstrap == true && BlocksToKeep == 0) "light-full-PoPoW"
else //Other combinations are possible
```

## Modifiers processing

```java
def updateHeadersChainToBestInNetwork() = {
  1.2.1. Send ErgoSyncInfo message to connected peers
  1.2.2. Get response with INV message,
  containing ids of blocks, better than our best block
  1.2.3. Request headers for all ids from 1.2.2.
  1.2.4. On receiving header
   if(History.apply(header).isSuccess) {
      if(!(localScore == networkScore)) GOTO 1.2.1
   } else {
      blacklist peer
      GOTO 1.2.1
   }
}
```

## bootstrap

### Download headers:

```java
if(PoPoW) {
 1.1.1. Send GetPoPoWProof(suffix = Max(MinimalSuffix ,BlocksToKeep)) for all connections
 1.1.2. On receive PoPoWProof apply it to History
  /*
  History should be able to determine,
  whether this PoPoWProof is better, than it's current best header chain */
} else {
  updateHeadersChainToBestInNetwork()
}
```

### Download initial State to start processing transactions:

```java
if(ADState == true) {
  Initialize state with state roothash from block header BlocksToKeep ago
} else if(BlocksToKeep < 0 || BlocksToKeep > History.headersHeight) {
  Initialize state with genesis State
} else {
/*
We need to download full state BlocksToKeep back in history
TODO what if we can download state only "BlocksToKeep - N"
or "BlocksToKeep + N" blocks back?
*/
  2.1. Request historical UTXOSnapshotManifest for at least BlocksToKeep back
  2.2. On receiving UTXOSnapshotManifest:
    UTXOSnapshotManifest.chunks.foreach ( chunk => request chunk from sender()
/*Or from random fullnode*/
  2.3. On receiving UTXOSnapshotChunk
  State.applyChunk(UTXOSnapshotChunk) match {
     case Success(Some(newMinimalState)) => GOTO 3
     case Success(None) => stay at 2.3
     /*we need more chunks to construct state. TODO periodicaly request missed chunks*/
     case Failure(e) => ???
     /*UTXOSnapshotChunk or constcucted state roothash is invalid*/
  }
}
```
### Update State to best headers height:
```java
 if(State.bestHeader == History.bestHeader) {
    //Do nothing, State is already updated
  } else if(VerifyTransactions == false) {
/*Just update State rootshash to best header in history*/
    State.setBestHeader(History.bestHeader)
  } else {
/*we have headers chain better than full block */
    3.1.
      assert(history contains header chain from State.bestHeader to History.bestHeaders)
      History.continuation(from = State.bestHeader, size = ???).get.foreach { header =>
        sendToRandomFullNode(GetBlockTransactionsForHeader(header))
        if(ADState == true) sendToRandomFullNode(GetADProofsForHeader(header))
      }
    3.2. On receiving modifiers ADProofs or BlockTransactions
      /*TODO History should return non-empty ProgressInfo
      only if it contains both ADProofs and BlockTransactions,
      or it contains BlockTransactions and ADState==false*/
      if(History.apply(modifier) == Success(ProgressInfo)) {
        if(State().apply(ProgressInfo) == Success((newState, ADProofs))) {
          if(ADState==false) ADProofs.foreach ( ADProof => History.apply(ADProof))
          if(BlocksToKeep>=0)
          /*remove BlockTransactions and ADProofs older than BlocksToKeep from history*/
        } else {
      /*Drop Header from history,
      because it's transaction sequence is not valid*/
          History.drop(modifier.headerId)
        }
      } else {
        blacklistPeer
      }
      GOTO 3
    }
```
### GOTO regular mode.

```java
TODO
```

## Regular
Two infinite loops in different threads with the following functions inside:

*  UpdateHeadersChainToBestInNetwork()
*  Download and update full blocks when needed

```java
 if(State.bestHeader == History.bestHeader) {
    //Do nothing, State is already updated
  } else if(VerifyTransactions == false) {
    //Just update State rootshash to best header in history
    State.setBestHeader(History.bestHeader)
  } else {
    //we have headers chain better then full block
    3.1. Request transaction ids from all headers without transactions
      assert(history contains header chain from State.bestHeader to History.bestHeaders)
      History.continuation(from = State.bestHeader, size = ???).get.foreach { header =>
        sendToRandomFullNode(GetTransactionIdsForHeader(header))
        if(ADState == true) sendToRandomFullNode(GetADProofsForHeader(header))
      }
    3.2. On receiving TransactionIdsForHeader:
      Mempool.apply(TransactionIdsForHeader)
      TransactionIdsForHeader.filter(txId => !MemPool.contains(txId)).foreach { txId =>
        request transaction with txId
      }
    3.3. On receiving a transaction:
      if(Mempool.apply(transaction).isSuccess) {
         Broadcast INV for this transaction
         Mempool.getHeadersWithAllTransactions { BlockTransactions =>
            GOTO 3.4 //now we have BlockTransactions
         }
      }
    3.4. (same as 3.2. from bootstrap)
  }
```
