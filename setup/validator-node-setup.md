---
description: >-
  This guide will run you through how to create a Validator Node to an
  Accumulate network.
---

# Validator Node Setup

The validator node connects to the Accumulate network and allows users to record and sign transactions in the Accumulate blockchain.&#x20;

Note: A transaction must be validated and authorized before it can be added to the blockchain.&#x20;

A Validator is the same as a follower, except that it is trusted to check everything. If enough Validators (usually 51% of them) agree on something, it is accepted.&#x20;

This guide is for creating a Validator node on Accumulate using a machine running Linux. &#x20;

&#x20;

### **Prerequisites** &#x20;

1. A Linux machine that matches or exceeds the minimum specification. See [https://accumulatenetwork.io/learn/#validators](https://accumulatenetwork.io/learn/#validators)  &#x20;
2. You need to have git, curl, jq installed. &#x20;
3. It would help if you had Docker & docker-compose. [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/) [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/) (An optional install script is included for Ubuntu) &#x20;

{% hint style="info" %}
These steps are optimized for Linux servers, but you can install it on a personal Linux OS as well, by running the commands as root (use \`sudo su\` to switch to root in your terminal)&#x20;
{% endhint %}

&#x20;

### **Steps to set up the node**&#x20;

**1: Update apt and install prerequisites**&#x20;

```
apt update && apt install git curl jq  
```

**2: Clone the Repo** &#x20;

```
git clone 
https://gitlab.com/accumulatenetwork/accumulate-docker.git
```

**3: Locate accumulate-docker folder** &#x20;

```
cd accumulate-docker  
```

**4: Install docker compose** &#x20;

```
./scripts/install-ubuntu.sh  
```

**5: Run** &#x20;

```
./run  
```

&#x20;The above command will return an output similar to the following: &#x20;

```
======= ACCUMULATE NETWORK =================  
Please select Network  
1. MainNet - Accumulate Mainnet  
2. SeedNode - Accumulate Mainnet Seed Node  
3. SentryNode - Accumulate Mainnet Sentary Node  
4. TestNet - Public Accumulate testnet  
```

**6: Select a Network**&#x20;

In this tutorial, you will select "Testnet," which Is no 4. &#x20;

Enter number 4

```
4  
```

**7: Enter BVN Number** &#x20;

Enter number **0**

```
0
```

**8: Create and Initialize a docker node** &#x20;

Enter number 1

```
1
```

**9: Select Accumulate version**&#x20;

So, I will advise you to select the latest non-develop version, which is number 2 &#x20;

Enter number 2&#x20;

```
2
```

**10: Start the Testnet** &#x20;

Your test net is now running locally on your system. Therefore, you will need to open a new terminal to test the node.&#x20;

&#x20;

**11: Apply to be a validator**&#x20;

Enter number 5 which is Display Registration Info&#x20;

The above command will return an output similar to the following: &#x20;

```
"subnet": "Directory", 
  "address": "C1D90CAA3658648B39175B174CFF2A799D2B9C03", 
  "pubkey": "78c5d97b0b6ffe6af202418604d94c65010c8d6336b6d36084503685ac7cf7a6" 
} 
```

At this point, you need someone from the accumulate team to register your node using the information above.&#x20;

This process will convert your node from a follower to a validator.&#x20;

&#x20;
