# How to release ACME with the Accumulate Bridge

Releasing ACME can be complex, especially when integrating it with other blockchains. This is where the Accumulate Bridge comes in, as it simplifies releasing ACME by providing an easy-to-use interface for management. This article will explore the steps involved in releasing an Accumulate token in WACME with the Accumulate Bridge.

Burning a wrapped `ACME` in Ethereum will release a comparable amount of `ACME` in Accumulate minus bridge fees.

### Steps in releasing ACME

**1.** Connect your wallet

The first step is to visit the bridge testnet URL and connect your wallet to the bridge.&#x20;

{% tabs %}
{% tab title="Mainnet" %}
[https://bridge.accumulatenetwork.io/mint](https://bridge.accumulatenetwork.io/mint)
{% endtab %}

{% tab title="Testnet" %}
[https://testnet.bridge.accumulatenetwork.io/mint](https://testnet.bridge.accumulatenetwork.io/mint)
{% endtab %}
{% endtabs %}

**2.** Click on the release tab

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-18 at 17.43.50.png" alt=""><figcaption></figcaption></figure>

**3.** Add the amount of `WACME` you want to release, then click **Approve**.

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-18 at 17.45.02.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Visit this URL to request more Gorlie faucets. [https://goerlifaucet.com/ for testnet only](https://goerlifaucet.com/)
{% endhint %}

**4.** Click the **Confirm** button

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-18 at 17.51.14.png" alt=""><figcaption><p>permission to access WACME</p></figcaption></figure>

Then you will be prompted to accept the request on your Metamask.

After accepting the request, the release button will become clickable, meaning you can now release your WACME.

**5.** Click the **Release** button above

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-18 at 17.52.12.png" alt=""><figcaption></figcaption></figure>

**6.** Click the **Confirm** button to accept the transaction.

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-18 at 17.52.47.png" alt=""><figcaption></figcaption></figure>

Your transaction is now successful.

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-18 at 17.53.01.png" alt=""><figcaption></figcaption></figure>

**7.** Query Lite Token Account ACME is being sent via the CLI.

**Command**&#x20;

```
./accumulate get acc://1d9e91f6b97bbe5f4ffad000566126a6c1a2bfd5d495b258/ACME -s https://testnet.accumulatenetwork.io/v2 
```

The above command will return an output similar to the following:

```
      Account Url     :       acc://1d9e91f6b97bbe5f4ffad000566126a6c1a2bfd5d495b258/ACME 

        Token Url       :       acc://ACME 

        Balance         :       386.10300000 ACME 

        CreditBalance   :       988.00 

        Last Used On    :       1970-01-20 02:28:46.978195 -0500 EST 

        Lock Height     :       0 
```

### **Transaction hash**

You can also view the transaction on Etherscan by copying the transaction hash **** below and visiting [https://goerli.etherscan.io/](https://goerli.etherscan.io/)

```
0x88cefde5ff10f4f478ca2f5b765cfa3e033d260bd6f8472a5ce5a05f6be2df20
```

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-18 at 17.55.54.png" alt=""><figcaption></figcaption></figure>
