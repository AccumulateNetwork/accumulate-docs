# Follower Node Setup

A node is a vital component of the blockchain network, and a decentralized ledger used to keep track of any cryptocurrency.

The primary function of a blockchain node is to check the legitimacy of each subsequent batch of network transactions, known as blocks. Each node's device has a unique identifier that allows it to be recognized by other nodes in the network.

![](<../.gitbook/assets/Screenshot 2022-05-19 at 13.49.32.png>)

**What is an Accumulate follower node?**

The follower node connects to the Accumulate network and allows users to record transactions in the Accumulate blockchain.

When configured and completely synced with the blockchain, you can use Accumulate API, CLI, and SDK’s to build chains and entries in the blockchain using your follower node.\


**Concept of a blockchain node**

* A blockchain is made up of many data blocks.
* These data chunks are stored on nodes ( compared to small servers ).
* All nodes are connected and are constantly exchanging the most recent information on the blockchain.
* Laptops, computers, and servers are typical examples of nodes.

This tutorial will teach you how to set up an Accumulate node on your local machine using a Linux server.

\


**Prerequisites**

1. A Linux server that matches or exceeds the minimum specification. See [https://accumulatenetwork.io/learn/#validators](https://accumulatenetwork.io/learn/#validators)
2. You need to have git, curl, jq installed.
3. It would help if you had Docker & docker-compose. [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/) [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/) (An optional install script is included for Ubuntu)

### **Steps to set up the node**

**1: Update apt**

```
apt update && apt install git curl jq  
```

**2: Clone the Repo**

```
git clone https://gitlab.com/accumulatenetwork/accumulate-docker.git
```

**3: Locate accumulate-docker folder**

```
cd accumulate-docker  
```

4: Install docker compose

```
./scripts/install-ubuntu.sh  
```

5: Run

```
./run  
```

**Result:**

```
======= ACCUMULATE NETWORK =================  
Please select Network  
1. MainNet - Accumulate Mainnet  
2. SeedNode - Accumulate Mainnet Seed Node  
3. SentryNode - Accumulate Mainnet Sentary Node  
4. TestNet - Public Accumulate testnet  
```

**6: Select a Network**

In this tutorial, you will select "Testnet," which Is no 4.

```
4
```

\


**7: Enter BVN Number**

```
0
```

**8: Create and Initialize a docker node**

```
1
```

**9: Select Accumulate version**

So, I will advise you to select the latest non-develop version, which is number 2

```
2
```

**10: Start the Testnet**

Your test net is now running locally on your system. Therefore, you will need to open a new terminal to test the node.

[Video tutorial link](https://www.youtube.com/watch?v=aHrJpkWQbXo)
