# How to use the Accumulate/Ethereum Bridge



## **Will my MetaMask wallet support Accumulate?**

Unfortunately, because Accumulate and Metamask are incompatible, you cannot directly add ACME, Accumulate's native token, to your Metamask wallet.&#x20;

But there may be other approaches to adding Accumulate to Metamask.&#x20;

Only blockchains created using the Ethereum Virtual Machine's primary programming language, Solidity, are supported by Metamask.&#x20;

You can download the browser extension or app to access it via this [link](https://metamask.io/)

### **What is a bridge?**

Bridges exist to connect blockchain networks. They enable connectivity and interoperability between blockchains.

They create a route for transporting tokens, messages, arbitrary data, and even smart contract calls from one blockchain to another.

**Prerequisites**

* Metamask account
* Basic knowledge of [Accumjulate CLI commands](https://docs.accumulatenetwork.io/accumulate/cli/cli-reference)
* Accumulate [CLI Setup](https://docs.accumulatenetwork.io/accumulate/cli/cli-setup)

### Configuring Metamask for Mainnet

1. Open the Metamask browser extension on your pc.
2. Confirm Ethereum Mainnet dropdown&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2022-10-27 at 13.23.46.png" alt=""><figcaption><p>dropdown menu</p></figcaption></figure>

To use the Accumulate Mainnet Bridge please go to: [https://bridge.accumulatenetwork.io/mint](https://bridge.accumulatenetwork.io/mint)

### Configuring Metamask for Goerli Testnet

If you want to use the testnet, click on the Ethereum Mainnet dropdown scroll **Advanced** and toggle the **Show test networks** to **ON**

<figure><img src="../.gitbook/assets/Screenshot 2022-10-27 at 13.26.02.png" alt=""><figcaption><p>Show test network</p></figcaption></figure>

1\. Click on the Goerli test network

To use the Accumulate Testnet Bridge please go to: [https://testnet.bridge.accumulatenetwork.io/mint](https://testnet.bridge.accumulatenetwork.io/mint)



## Sending ACME through the Bridge Example:

Below is an example of using the bridge on the Goerli Testnet sending ACME and mint Wrapped ACME in Ethereum.

{% hint style="info" %}
**The same instructions apply for the Ethereum Mainnet except:**\
**1. There is no faucet to get ACME on the Mainnet.** \
**2. The bridge address you are sending ACME tokens to is also different: acc://bridge.acme/1-ACME**\
**3. The contract address for WACME**&#x20;
{% endhint %}

<figure><img src="../.gitbook/assets/Screenshot 2022-10-27 at 14.16.25.png" alt=""><figcaption></figcaption></figure>

6\. Click on **connect a wallet,** then you will see a pop-up similar to the image below.

<figure><img src="../.gitbook/assets/Screenshot 2022-10-27 at 14.27.38.png" alt=""><figcaption></figcaption></figure>

Click on the **Metamask** button**.** Then a transaction will be sent to your Metamask wallet for your approval.

After approving the transaction, your bridge will be connected to your Metamask wallet.

<figure><img src="../.gitbook/assets/Screenshot 2022-10-27 at 16.23.53.png" alt=""><figcaption></figcaption></figure>

7\. **** Type in the amount of ACME you want to send. &#x20;

In this example, I entered **100 ACME.**

<figure><img src="../.gitbook/assets/Screenshot 2022-10-27 at 14.33.10.png" alt=""><figcaption></figcaption></figure>

8\. Click **Next** to view the mint instruction.

<figure><img src="../.gitbook/assets/Screenshot 2022-10-27 at 14.35.13.png" alt=""><figcaption></figcaption></figure>

You have now successfully connected Accumulate bridge to your Metamask wallet. You can now transfer and receive ACME tokens to any ERC20 token.

The next step is to transfer ACME tokens to your Metamask wallet.

### **Send tokens to bridge token account**

**Generate Lite Token Account**&#x20;

```
./accumulate account generate 
```

The above command will return an output similar to the following:&#x20;

```
name            :       f683b49d4cddd026b410b1e2ea348c13db8ed7d0a776d4c0 
lite account    :       acc://9a4df91123d42b5926b6e84dac256ddc8a1e32f8c5a59554/ACME 
public key      :       021f4c46cbd0d46a5610c8069cecd2691f10275b721ec6ce699769019bb559bb 
key type        :       ed25519 
```

**Faucet Lite Token Account**&#x20;

Add a faucet to your lite token runnig the command below.

```
./accumulate faucet acc://9a4df91123d42b5926b6e84dac256ddc8a1e32f8c5a59554/ACME 
```

&#x20;The above command will return an output similar to the following:&#x20;

```
Transaction Hash        : 517be7d3434b9c1bb23f570cd2602ec73ce15e325574fe9ef02f4ad206693638 
Signature 0 Hash        : b3cb9b1241a896163b85088ed95ec78638f93cc3c5147b74d96329b32e54cc2c 
Simple Hash             : 39100b269703a1546254f3a5ccaffe5d7f891e79d399751e2d168cf1431ef2c1 
Error code              : ok 
Result                  : 
```

**Add Credits to Lite Token Account**&#x20;

Add credit to your lite token account by running the command below.

```
./accumulate credits acc://9a4df91123d42b5926b6e84dac256ddc8a1e32f8c5a59554/ACME acc://9a4df91123d42b5926b6e84dac256ddc8a1e32f8c5a59554/ACME 10000 
```

The above command will return an output similar to the following:&#x20;

```
Transaction Hash        : c618751354ac8cf993d432d3227d7a5739f672143e711f5ec538a4e082de9c00 
Signature 0 Hash        : 5b89c04661b6e4287c5de1127a594b784b4038efb6346ddc6c7ae1af095f7132 
Simple Hash             : a913477ab6b8d2c26ae98757dce48aee5f81d2c8f4c1bbebdcbc5d18f59a4585 
Error code              : ok 
Result                  : Oracle        $0.05 / ACME 
                                  Credits       10000.00 
                                  Amount        2000.00000000 ACME 
```

**Send Tokens to the Bridge Token Account which is Displayed in the Mint Instructions and Add a Memo Field Containing your Ethereum Address shown in your Meta Mask wallet**&#x20;

```
./accumulate tx create acc://9a4df91123d42b5926b6e84dac256ddc8a1e32f8c5a59554/ACME acc://bridge.acme/5-ACME 100 --memo ‘0x2F0A0C3341C63D647FE7f5f3bbFCcb4f6DbE7938'
```

The above command will return an output similar to the following:&#x20;

```
        Transaction Hash        : 37492a17e04e7a18e646c2d26cd287e69dd08b9faaf20470103a6d44bd638309 

        Signature 0 Hash        : 6985294b34b514926f1aaaa8ca3dc95c4a2c352969dd04c8d0cd8ebd423ac3af 

        Simple Hash             : 82967e2be708f03d1c5a8e83881ba2099a990a7c0b75ec0e2540dad9d013f4ce 

        Error code              : ok 

        Result                  : 
```

1. Open your MetaMask

<figure><img src="../.gitbook/assets/Screenshot 2022-10-27 at 16.24.18.png" alt=""><figcaption></figcaption></figure>

2\. In the tab, Click on **Assets** then click **Import tokens** and paste this contract address `0xCD08505D03B6bc1a84A5E706536562546A9c99f9` in the **Token contract address** field&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2022-10-27 at 16.31.42.png" alt=""><figcaption></figcaption></figure>

3\. Click add custom token

<figure><img src="../.gitbook/assets/Screenshot 2022-10-27 at 16.31.59.png" alt=""><figcaption></figcaption></figure>

4\. Finally, click Import tokens

<figure><img src="../.gitbook/assets/Screenshot 2022-10-27 at 16.35.07.png" alt=""><figcaption></figcaption></figure>
