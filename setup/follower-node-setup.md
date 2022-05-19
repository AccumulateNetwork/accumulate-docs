# Follower Node Setup

A node is a vital component of the blockchain network, and a decentralized ledger used to keep track of any cryptocurrency. &#x20;

The primary function of a blockchain node is to check the legitimacy of each subsequent batch of network transactions, known as blocks. Each node's device has a unique identifier that allows it to be recognized by other nodes in the network.&#x20;

![](<../.gitbook/assets/Screenshot 2022-05-19 at 13.49.32.png>)

**What is an Accumulate follower node?**&#x20;

The follower node connects to the Accumulate network and allows users to record transactions in the Accumulate blockchain. &#x20;

When configured and completely synced with the blockchain, you can use Accumulate API, CLI, and SDK’s to build chains and entries in the blockchain using your follower node. \
&#x20;

**Concept of a blockchain node** &#x20;

* A blockchain is made up of many data blocks.&#x20;
* These data chunks are stored on nodes ( compared to small servers ).&#x20;
* All nodes are connected and are constantly exchanging the most recent information on the blockchain.&#x20;
* Laptops, computers, and servers are typical examples of nodes.&#x20;

&#x20;&#x20;

This tutorial will teach you how to set up an Accumulate node on your local machine using a Linux server. &#x20;

&#x20;\
&#x20;

**Prerequisites** &#x20;

1. A Linux server that matches or exceeds the minimum specification. See [https://accumulatenetwork.io/learn/#validators](https://accumulatenetwork.io/learn/#validators)  &#x20;
2. You need to have git, curl, jq installed. &#x20;
3. It would help if you had Docker & docker-compose. [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/) [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/) (An optional install script is included for Ubuntu) &#x20;

### &#x20;**Steps to set up the node**&#x20;

&#x20;

**1: Update apt** &#x20;

apt update && apt install git curl jq  \
&#x20;

**2: Clone the Repo** &#x20;

git clone [https://gitlab.com/accumulatenetwork/accumulate-docker.git](https://gitlab.com/accumulatenetwork/accumulate-docker.git) &#x20;

&#x20;

**3: Locate accumulate-docker folder**&#x20;

```
cd accumulate-docker  
```



4: Install docker compose &#x20;

```
./scripts/install-ubuntu.sh  
```



5: Run &#x20;

```
./run  
```



**Result:** &#x20;

```
======= ACCUMULATE NETWORK =================  
Please select Network  
1. MainNet - Accumulate Mainnet  
2. SeedNode - Accumulate Mainnet Seed Node  
3. SentryNode - Accumulate Mainnet Sentary Node  
4. TestNet - Public Accumulate testnet  
```

&#x20;&#x20;

**6: Select a Network** &#x20;

In this tutorial, you will select "Testnet," which Is no 4. &#x20;

```
4
```

&#x20;\
&#x20;

**7: Enter BVN Number** &#x20;

```
0
```



**8: Create and Initialize a docker node**&#x20;

```
1
```



**9: Select Accumulate version** &#x20;

So, I will advise you to select the latest non-develop version, which is number 2 &#x20;

```
2
```

&#x20;

**10: Start the Testnet**&#x20;

Your test net is now running locally on your system. Therefore, you will need to open a new terminal to test the node.&#x20;

[Video tutorial link](https://www.youtube.com/watch?v=aHrJpkWQbXo)
