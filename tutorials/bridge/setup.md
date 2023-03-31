---
description: This guide will explain how to set up an Accumulate bridge node for Ethereum.
---

# Setup

This guide will explain how to set up an Accumulate bridge node for Ethereum. The Accumulate bridge is software that allows for the secure exchange of ERC20 tokens between the [Ethereum](https://ethereum.org/en/developers/docs/) Mainnet and [Accumulate blockchain](https://accumulatenetwork.io/). The bridge is powered by the Accumulate Protocol, a set of smart contracts that facilitate the transfer of tokens and ownership.&#x20;

**Prerequisites**

* You need to install Docker.
* You need a basic understanding of Accumulate CLI.
* The bridge works only on a Linux OS.
* We recommend Infura (https://infura.io/).
* You need an Ethereum address.

The first step is to set up an Ethereum node. We recommend using [Infura](https://infura.io/), which is the most popular Ethereum node provider. Once you have set up your node, you can begin setting up the Accumulate bridge.&#x20;

Next, you will need to create a new account on the Ethereum network that will be used to hold the ERC20 tokens. This account will be known as the bridge account.

{% hint style="info" %}
Bridge repo [https://github.com/AccumulateNetwork/bridge](https://github.com/AccumulateNetwork/bridge)
{% endhint %}

**Copy the config file into your server**&#x20;

The first step is to create a folder in your server&#x20;

```
mkdir ~/.accumulatebridge
```

Change the folder to the new folder.

```
cd ~/.accumulatebridge
```

Then run the command below to generate the config file.

```
 curl -o ~/.accumulatebridge/config.yaml 
https://raw.githubusercontent.com/AccumulateNetwork/bridge/master/config.yaml.EXAMPLE
```

**Modify the configuration file**

Open up the config file in your favorite editor (nano, vscode, or others).

**Example config file**

```bash
app:  
# Node API port
    apiport: 8081  
# Log Level (Debug 1, Info 2, Warn 3, Error 4)
    loglevel: 2 
acme:  
# Accumulate API endpoint, e.g. "https://testnet.accumulatenetwork.io/v2"
     node: "https://mainnet.accumulatenetwork.io/v2" 
# Bridge ADI, usually "bridge.acme"
bridgeadi: "bridge.acme"   
# Bridge keybook, usually "validators"
keybook: "validators"   
# Accumulate ed25519 private key
privatekey: "<your ACME private key>" 
evm:  
# EVM API endpoint (Infura/Quicknode, private node, etc.)
       node: "<your infura node>"  
# EVM chainid (Ethereum mainnet 1, Goerli testnet 5, etc.)
      chainid: 1  
# Gnosis safe smart contract address
      safeaddress: "0x76b1E2d258CC4297e7708345E5d99e8ECa967BB1"  
# Accumulate bridge smart contract address
bridgeaddress: "0xbA050938970C8eAeDA3e970B571a6fe463Db7d0e" privatekey: "<your ETH private key>"  
# (optional) Maximum gas fee (EIP-1559)
maxgasfee: 30  
# (optional) Maximum priority fee (EIP-1559)
maxpriorityfee: 2
```

There are a few constant fields:

* **bridgeadi:** "bridge.acme"
* **keybook:** "validators"
* **safeaddress** "0x76b1E2d258CC4297e7708345E5d99e8ECa967BB1"
* &#x20; **bridgeaddress:** "0xbA050938970C8eAeDA3e970B571a6fe463Db7d0e"\


Next, run this command to start your Accumulate bridge:&#x20;

```
docker run -d --name accumulatebridge -v ~/.accumulatebridge:/home/app/values registry.gitlab.com/accumulatenetwork/evm-bridge:v1-0-1
```

{% hint style="info" %}
You can use \`docker ps -a' or \`docker container ls -a' to see if the docker image is running.&#x20;
{% endhint %}

&#x20;Congratulations, your bridge is running.

&#x20;

&#x20;
