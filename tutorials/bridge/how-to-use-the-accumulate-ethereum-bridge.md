---
description: Learn how to convert ACME to WACME using the Accumulate Bridge
---

# How to convert ACME to WACME

Wrapped Accumulate (WACME) is an ERC-20 wrapped version of the native ACME token on Ethereum. WACME allows users in the Ethereum ecosystem to use ACME across an array of DeFi platforms, such as Uniswap and Curve.

The Accumulate Bridge offers a simple and user-friendly method to convert ACME to WACME for use on Ethereum. This article will explore the steps in minting wACME with the Accumulate Bridge, providing a comprehensive guide for beginners and experienced users. Whether you are a new or a seasoned user, this guide will help you navigate and empower you to mint wACME with confidence.

### **Prerequisites**

* Ethereum wallet with Web3-connectivity, such as [Metamask](https://metamask.io), [Rabby](https://rabby.io), or any wallet supported by [WalletConnect](https://walletconnect.com)
* Accumulate [mobile wallet](https://accumulatenetwork.io/wallet) or [CLI wallet](../../cli/cli-setup.md)

{% hint style="info" %}
Note: If you would like to test the Bridge on the Goerli Testnet, you can follow the same instructions with the following differences: \
1\. There is a faucet to get ACME on the Accumulate TestNet\
2\. The bridge address you are sending ACME tokens to  acc://bridge.acme/5-ACME\
3\. The contract address for importing WACME to MetaMask for the Goerli Testnet: `0xCD08505D03B6bc1a84A5E706536562546A9c99f9`
{% endhint %}

### **How to add Accumulate to Metamask**

**1.** To use the Accumulate Mainnet Bridge, please go to: [**bridge.accumulatenetwork.io**](https://bridge.accumulatenetwork.io/mint)

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-27 at 14.16.25.png" alt=""><figcaption></figcaption></figure>

**2.** Click on **connect a wallet**. you will see a pop-up similar to the image below.

<div align="left">

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-27 at 14.27.38.png" alt=""><figcaption></figcaption></figure>

</div>

**3.** Choose either **Metamask** or **WalletConnect** depending on your connection method**.**&#x20;

An approval transaction will be sent to your wallet. After approving the transaction, your wallet will be connected to the bridge.

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-27 at 14.33.10.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-27 at 16.23.53.png" alt=""><figcaption></figcaption></figure>

&#x20;**4.** Type in the amount of ACME you would like to convert. &#x20;

![](<../../.gitbook/assets/image (17).png>)



**5.** Click **Next** to view the mint instruction.

![](<../../.gitbook/assets/image (8).png>)

The next step is to transfer ACME tokens to your Metamask wallet.

### **Send tokens to bridge token account**

**6.** Send Tokens to the Bridge Token Account, displayed in the Mint Instructions, and add a Memo field containing your Ethereum address.

{% hint style="info" %}
If you're using the CLI to send the tokens, add `--memo` to the end of the command, followed by your Ethereum address wrapped in quotes (e.g. \`accumulate tx create myAccount.acme myKey acc://bridge.acme/1-ACME 100 --memo "0xF61872468a3b87F5954DeB3b94Ba47a6f63FgK985"&#x20;
{% endhint %}

{% hint style="danger" %}
**WARNING**: Do not send tokens without including a memo with your address, or your tokens will be lost.
{% endhint %}

Congratulations! You should now have WACME in your Ethereum account. Check your address on [Etherscan](https://etherscan.io) to confirm.



### Bonus: showing WACME tokens on Metamask

If you're a Metamask user, you may notice that not all of the tokens in your account show up in your wallet. This is because new tokens do not show up automatically in your wallet. Do not worry, if the tokens appear on Etherscan, than you have them in your account.

#### If you would like to display WACME on your Metamask, follow the below steps:

**1.** In the Metamask window, click on **Assets,** then click **Import tokens**&#x20;

**2.** Click **Add Custom Token**

**3.** Paste this contract address in the **Token contract address** field: `0xDF4Ef6EE483953fE3B84ABd08C6A060445c01170`

![](<../../.gitbook/assets/image (6) (1).png>)

**4.** Finally, click **Import tokens** to add **WACME** to your tokens list.



![](<../../.gitbook/assets/image (12).png>)



{% hint style="info" %}
Ensure you have Eth in your Wallet to Sign Transactions on the Mainnet.\
Use Goerli Eth on the Testnet to Pay for Transactions: [https://goerlifaucet.com/](https://goerlifaucet.com/)
{% endhint %}

{% hint style="info" %}
If you are signing transactions with a Ledger Device connected to MetaMask, you will need to enable [blind signing.](https://www.ledger.com/academy/enable-blind-signing-why-when-and-how-to-stay-safe)
{% endhint %}



\
