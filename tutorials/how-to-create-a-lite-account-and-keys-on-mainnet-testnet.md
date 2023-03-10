# How to create a Lite Account and Keys on mainnet / testnet

Creating a Lite Account and Keys on mainnet or testnet is an important step for anyone interested in using Accumulate. Lite Accounts are a type of account that can be used to transact and interact with blockchain networks, while Lite Keys are used to authenticate and signing transactions on these networks.

This guide will walk you through creating a Lite Account and Keys on both mainnet and testnet. We will cover the basic concepts and tools required to create a Lite Account, including a wallet and private keys.

By the end of this guide, you will have a better understanding of how to create a Lite Account and Keys, and you will be equipped with the knowledge and tools necessary to start using Accumulate protocol. \
\
To use the Accumulate Mainnet, you need to have a lite token account. This is the network where all the real transactions occur (as opposed to the Testnet, which is only for testing purposes). A lite token account is a basic account type in Accumulate and is needed to create an ADI where the more advanced Accumulate features are available.&#x20;

{% hint style="info" %}
Creating a lite account with Mainnet and testnet follows the same steps.
{% endhint %}

Creating a lite token account on Mainnet/ testnet is easy and only takes a few minutes. This article will show you how to create an account using CLI in two simple steps. &#x20;

* Create a wallet&#x20;
* Generate a key&#x20;

{% hint style="info" %}
This guide requires you to set up the Accumulate CLI on your computer. If you have not yet installed the CLI, please click [here](https://docs.accumulatenetwork.io/accumulate/cli/cli-setup)
{% endhint %}

In Accumulate CLI, we have two ways of generating a lite account, `./accumulate account generate`, and `./accumulate key generate [name for this key]`. &#x20;

The first command will generate the lite account with a key and use the public key as the name, which is much less user-friendly, while the second command will generate a lite account with a key and a custom name.

{% hint style="danger" %}
Make sure you are running on Mainnet before continuing. Try running `./accumulate` to see all the flags; check the --server flag. If you see testnet; kindly run the command below to change it to mainnet&#x20;

export ACC\_API=[https://mainnet.accumulatenetwork.io/v2](https://mainnet.accumulatenetwork.io/v2)&#x20;
{% endhint %}

**Create a wallet**&#x20;

This command will create an Accumulate wallet in your CLI.

```
./accumulate wallet init create  
```

For more information on creating a wallet, check our [CLI setup](https://docs.accumulatenetwork.io/accumulate/cli/cli-setup)

2\. You will create a lite account, and that can be done using the two commands

* Generate a lite account
* Generate a key

{% tabs %}
{% tab title="Generate a lite account" %}
Generate random Lite Identity and ACME Lite Token Account &#x20;

**Syntax:**&#x20;

```
./accumulate account generate
```

****

**Command:** &#x20;

```
./accumulate account generate 
```



The above command will return an output similar to the following: &#x20;

```
name : e1a69cb98d884975a857cb73b0f47981cf032459db2d26ee 
lite account : acc://e1a69cb98d884975a857cb73b0f47981cf032459db2d26ee/ACME 
public key : 4332e43d1b603db967fe7a465dbd43c44c633b86a40bfb7582ac14df4ea728ae 
key type : ed25519 
```
{% endtab %}

{% tab title="Generate a key" %}
**Syntax:** &#x20;

```
./accumulate key generate [name for this key]  
```



**Command:** &#x20;

```
./accumulate key generate john 
```

&#x20;

The above command will return an output similar to the following: &#x20;

&#x20;

```

name : john 
lite account : acc://791dca8285c283216701427e551b4be970ad2747dea2cd88/ACME 
public key : 6170f96898f7bc80ff3a72a0191926ac90e96197b9f977d56c1e855c7a43fe44 
key type : ed25519 
```
{% endtab %}
{% endtabs %}

It is necessary to create a key in Accumulate protocol because you will use it in many things:&#x20;

* [Creating an ADI](https://docs.accumulatenetwork.io/accumulate/tutorials/create-an-adi-via-cli)
* [Creating a custom token account](https://docs.accumulatenetwork.io/accumulate/tutorials/how-to-create-a-custom-accumulate-token)
* Creating a Data account.&#x20;

Also, you can view your public key using the **key list** and **account list** commands.&#x20;

{% tabs %}
{% tab title="Key list" %}
This command displays the list of keys available in your wallet.&#x20;

&#x20;

**Command**&#x20;

```
./accumulate key list 
```



The above command will return an output similar to the following: &#x20;

```
Public Key Key name 
4332e43d1b603db967fe7a465dbd43c44c633b86a40bfb7582ac14df4ea728ae e1a69cb98d884975a857cb73b0f47981cf032459db2d26ee 
6170f96898f7bc80ff3a72a0191926ac90e96197b9f977d56c1e855c7a43fe44 john 
d940d2a803e50f40be208c3629ece56949236f7c5c256f641f9f4cbd3fca337a paul 
10d22def144a041cf2a02f020a6e1bdb567d72cfa06c32c70658df858bfa855b paulf 
90161fe58540c3d5cbbc6c00fa70a96531679e8a3722c0d584825b2feff0f7e1 paulff 
6eb9dfa41b3400d4ea226a52a0c93484ae61e3cd02ccee27c5373a8d2049d732 wise 
d23254ea7a4f66c8974d618beecba891b46b9617770e85fb4d8412a35185dba7 wiset 
44bb5f8f4412c66b3dbd1541a417d87a65a5c414f278eef1172f82b2ffb3153e wisez 
```
{% endtab %}

{% tab title="Account list" %}
This command displays the Accumulate account details. \
&#x20;

**Command**&#x20;

```
./accumulate account list 
```

\
&#x20;The above command will return an output similar to the following: &#x20;



```
 key name : paulff 
        lite account : acc://34b0ce6d44b0410b8c236c6242600f0e85403c08cd3324fd/ACME 
        public key : 90161fe58540c3d5cbbc6c00fa70a96531679e8a3722c0d584825b2feff0f7e1 
        key type : ed25519 
        derivation : m/44'/281'/0'/0'/5' 
 
 
 
 
        key name : john 
        lite account : acc://791dca8285c283216701427e551b4be970ad2747dea2cd88/ACME 
        public key : 6170f96898f7bc80ff3a72a0191926ac90e96197b9f977d56c1e855c7a43fe44 
        key type : ed25519 
        derivation : m/44'/281'/0'/0'/0' 
 
 
        key name : paul 
        lite account : acc://931ae14961befb56a37ae1561083a6fec275a6ae5070b7fa/ACME 
        public key : d940d2a803e50f40be208c3629ece56949236f7c5c256f641f9f4cbd3fca337a 
        key type : ed25519 
        derivation : m/44'/281'/0'/0'/2' 
```
{% endtab %}
{% endtabs %}
