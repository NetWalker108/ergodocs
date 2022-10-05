---
tags:
  - NIPoPoWs
---
# NIPoPoWs

Ergo implements **NIPoPoWs**, or Non-interactive Proof-of-Proof-of-Work. These are short stand-alone strings that a computer program can inspect to verify that an event happened on a proof-of-work-based blockchain without connecting to the blockchain network and downloading all block headers. For example, these proofs can illustrate that a cryptocurrency payment was made.

- [NIPoPoWs on Ergo: Innovations in Blockchain - April, 2022](https://ergoplatform.org/en/blog/2022-04-01-NIPoPoWs-on-ergo-innovations-in-blockchain/)

## Literature

- [Non-Interactive Proofs of Proof-of-Work](https://eprint.iacr.org/2017/963.pdf)
- [Compact Storage of Superblocks for NIPoPoW Applications](https://eprint.iacr.org/2019/1444.pdf)

## Blocks

In Ergo, just like Bitcoin, Ethereum, and other blockchains, blocks are broken into sections. In Bitcoin, there's simply a block header and the transactions themselves. But in Ergo, we have some **extra sections** that enable new functionality:

* Header
* Transactions
* **Extensions**
* **Proofs of UTXO transformation**

The 'extension' section contains certain mandatory fields (including links for NiPoPoW, once per 1,024 block epoch) and parameters for miner voting, such as current block size. It can also contain arbitrary fields.

**What this means in practice is that different types of nodes and clients can download only those sections of the blocks they need – reducing the demands for storage, bandwidth, and CPU cycles.**



## Light Nodes

**Light Clients** are essential when considering the hurdles cryptocurrency faces with mass adoption. Most crypto users do not have the necessary tools to run a full node. Running a full node means having a strong processor with high electricity wattage and more than a hundred gigabytes of memory to store the entire blockchain. Light clients are useful because they enable verification with a limited supply of data providers (nodes) and significantly reduce the amount of data storage and bandwidth needed for everyday users.

The use of light clients with the implementation of NIPoPoWs makes it possible to interact with the blockchain through block headers by using only a couple of kilobytes. Verifying whether a transaction happened on the blockchain becomes simplified. NIPoPoWs can help people interact with the blockchain by using more efficient and convenient mobile wallets.

NIPoPoWs allow very efficient mobile wallets to be created. SPV wallets are already very lightweight compared to full nodes because they only require the download of block headers, not the whole blockchain. NIPoPoW wallets need to download only a small sample of block headers, around 250, when SPV clients need to download half a million block headers. The sample needed changes but doesn't grow much in size as the blockchain grows larger over the years, even after accumulated decades of data.

NIPoPoWs enable Ergo to build a mobile SPV client that requires around just 100KB of block headers to be downloaded.

### SPV Security

A full Bitcoin node checks all the blocks in the blockchain (using headers) and makes sure there are no fraudulent transactions. It's a very secure way of using crypto – but there's a problem. It requires significant bandwidth, storage, and processing power. That kind of commodity hardware is expensive, and using a full node to validate and make transactions is unsuitable for mobile devices. This is particularly true for Bitcoin, where the blockchain is over [270 GB and counting](https://www.blockchain.com/charts/blocks-size).

Simplified Payment Verification (SPV) is designed to address this problem, as described in the [Bitcoin white paper](https://bitcoin.org/bitcoin.pdf):

- *It is possible to verify payments without running a full network node. A user only needs to keep a copy of the block headers of the longest proof-of-work chain, which he can get by querying network nodes until he's convinced he has the longest chain and obtain the Merkle branch linking the transaction to the block it's timestamped in. He can't check the transaction for himself, but by linking it to a place in the chain, he can see that a network node has accepted it and blocks added after it further confirms the network has accepted it.*
 
Satoshi notes that this is not a perfect solution and is vulnerable to an attacker overpowering the network and fooling SPV users.

Moreover, while SPV mode is intended for resource-limited devices, this 'lite' approach is not always feasible. Ethereum's headers alone total around 5 GB to download. Thus Ethereum mobile clients do not validate chain validity and so blindly have to trust third parties.

There are proposals to reduce the requirements for SPV mode by checking just a few random headers instead of all of them. But it's hard to do that securely. 



### Efficient SPV

Several years have been spent researching and developing secure protocols for efficient SPV clients. The two best-known and most reliable protocols are NIPoPoWs and FlyClient.

Ergo implements NIPoPoWs, or Non-interactive Proof-of-Proof-of-Work. You can explore this technology in full on this dedicated website: [https://NIPoPoWs.com](https://NIPoPoWs.com):

- *Non-Interactive Proofs of Proof-of-Work (NIPoPoWs) are short stand-alone strings that a computer program can inspect to verify that an event happened on a proof-of-work-based blockchain without connecting to the blockchain network and without downloading all block headers. For example, these proofs can illustrate that a cryptocurrency payment was made.*

- *NIPoPoWs allow very efficient mobile wallets to be created. [SPV wallets](https://bitcoin.org/en/developer-guide#simplified-payment-verification-spv) are already very lightweight compared to full nodes because they only require the download of block headers, not the whole blockchain. NIPoPoW wallets need to download only a tiny ***sample*** of block headers, around 250 when SPV clients need to download half a million block headers. The sample needed changes but doesn't grow much in size as the blockchain grows more extensive, even after accumulated decades of data.*

This enables us to build a mobile SPV client that requires around **just 100KB** of block headers to be downloaded.

A super-efficient Ergo wallet with SPV security is in development, so stay tuned for more updates!


## Log-Space Mining
Dionysis Zindros explains the technical landscape of Non-Interactive Proofs of Proof-of-Work. Dionysis takes a diligent approach for the Ergo Cast with a detailed rundown of what Non-Interactive Proofs of Proof-of-Work truly are. Furthermore, Dionysis evaluates the operation, implementation, and impact that his primitive delivers upon. Furthermore, we unveil a brand-new piece of research that -as of yet- has never been shared publicly: log-space mining.

- [NIPoPoWs & Log-Space Mining – Ergo Cast Episode #5](https://ergocast.io/episode/NIPoPoWs-ergo-cast-episode-5/)


This section is based on a [recently published](https://eprint.iacr.org/2021/623.pdf) article by IOHK. For an additional resource, please see the following [video.](https://www.youtube.com/watch?v=s05ypkSC7gk)


Miners must constantly maintain the blockchain, whether it is Ergo, Bitcoin, or another PoW consensus model. In addition to using computational resources, miners also use storage resources that maintain all blockchain data from the genesis block.

A new miner's problem: Is downloading all the data from the genesis block strictly necessary? Why is it not possible to download only the most relevant blocks to maintain the network?

The block headers of the blockchain should be enough to access the necessary data. [NIPoPoWs](https://NIPoPoWs.com/) (Non-Interactive Proofs of Proof of Work) can be integrated to form interlinked block header sets that will reduce historical data storage.

When needing to access key blocks in the blockchain, miners should be able to do this from the headers of the old blocks efficiently. That is because each new block must indicate all of the current networks. As new blocks are created, a set of new block headers can be enough to check for the current UTXO set. Since the new blocks contain the data of old stringed block header sets, it enables light mining by eliminating the need to download all the blockchain data.

What are we trying to optimise by stringing old PoW history and compiling it into a snapshot?

If we say C=old blocks and K=new blocks, then included blocks in the snapshot can be growing when K=new blocks are constant, and C=old blocks are linear. But it can also be shrinking depending on the smart contract applications. The problem of maintaining heavy loads of data by the miners can be solved by bootstrapping through NIPoPoWs. 


**NIPoPoW Implementation**

Instead of accessing all of the blocks, superblocks (or light-clients) are enough to verify all of the blocks. This is accomplished by maintaining the historical data of the blockchain through smart contracts. The introduction of these superblock clients on NIPoPoWs can be done via 'velvet' or soft forks, and after that "light" miners can bootstrap through "online" mining.

NIPoPoWs enable smart contracts to maintain historical data so that new "light" miners can work in a so-called "online" fashion. This is the main idea of Logarithmic Space Mining. Instead of saving all the blockchain data locally on nodes, the unnecessary part can be compiled into the blockchain itself. New miners do not need to carry the historical data, and as they continue to mine, new "light" miners will help other "light" miners bootstrap. There will be no need to carry old historical data, and old miners can abandon historical data for lighter mining. This is how the whole miner population can abandon old blocks and make the system much more efficient.



## Sidechains

Another implementation is cross-chain communication with Proof of Stake networks. PoS networks such as Cardano can interact with Ergo through NIPoPoW integration. Such verification schemes can erase the need for centralised DAO structures and create new non-interactive cross-chain operations. 

To put it simply, NIPoPoWs act as sidechains. Two or more separate chains can integrate through NIPoPoWs without the need for change in other chains. Such integration would erase the need for, for example, "Wrapped Tokens," tokens that rely on DAO governance. 

NIPoPoW is a robust tool in creating blockchain networks and provides easier client access. They're also helpful in enhancing scalability by creating Layer 2 organisations. 



**Side chains**, on the other hand, are a completely different component of blockchain. They are beneficial for various elements such as private chains, scalability improvement, and cross-chain interoperability. [Kushti mentioned](https://youtu.be/QCMpVRVrHqI) that he will release a sidechain "cookbook," entitled Ergo-Meta, in the following months. 



One application of NIPoPoWs that we have described in a previous article deals with [logarithmic space mining](https://www.youtube.com/watch?v=s05ypkSC7gk). Logarithmic space mining allows for "light miners." Like light clients, light miners can bootstrap with block headers without downloading the whole blockchain. It is also possible to store just a few necessary blocks to verify the whole blockchain in a blockchain. This essentially eradicates the need for miners to store all of the blockchains. Integrating logarithmic space mining in Ergo is possible via velvet (soft) forks, therefore preventing the need for painful hard forks.



Another application of NIPoPoWs was proposed in the first [ErgoHack](https://curiaregiscrypto.medium.com/ergohack-results-f7d72711a9db) by a team called SmartPools. SmartPools' proposal aims to increase the **Nakamoto Coefficient**, a metric for calculating the decentralisation of the given network. In our case, the proposal aims to increase the decentralisation of the Ergo Platform by bootstrapping mining entities with collateralised smart contracts. The purpose here is to provide returns for non-miner investors and prevent big GPU farms from taking control of the system.



The most well-known example of NIPoPoWs is the implementation of the second layer blockchain. Second layers help interact with different blockchains by increasing scalability and creating private sidechains for enterprise-grade applications. Second layers create blockchains on top of the primary blockchain for different use cases. Because transactions can happen on these second layers without constant synchronous updates, we can lower the network load substantially by keeping everything on the main chain all the time.

**The Ergo blockchain has supported NIPoPoWs since its genesis, yet their use cases are still in their infancy. We continue to develop this field of research with our partners at [IOHK](https://iohk.io/) and [EMURGO](https://emurgo.io/), and we expect their application to increase with continued contributions from the community developers.**











