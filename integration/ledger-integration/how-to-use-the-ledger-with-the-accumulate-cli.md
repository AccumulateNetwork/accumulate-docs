# How to use the Ledger with the Accumulate CLI

This guide will show you how to set up Accumulate Ledger CLI for a few operations like sending tokens, adding Accumulate credits, generate a faucet. Etc.

#### **Clone the accumulate cli repo**

```
git clone https://gitlab.com/accumulatenetwork/core/wallet.git
```

#### **Enter Accumulate folder**&#x20;

```
cd wallet
```

#### **Run Accumulate CLI**

```
go run ./cmd/accumulate
```

#### **Build Accumulate CLI**

```
go build ./cmd/accumulate
```

#### **Make the project**

```
make
```

{% hint style="info" %}
Make sure you plug in your Ledger device at this stage
{% endhint %}

#### **Run make Accumulate command**

```
make accumulate
```

#### **Install go in accumulate folder**

```
go install ./cmd/accumulate
```

#### **Ledger device**

* On your ledger Device,&#x20;
* Open the Accumulate app.
* If the Accumulate ledger app was sideloaded the app will show `app is not genuine.` Press the right button till you see, `Open application.` However, the app store version will not show this.
* Then press both buttons to open the application.
* You will see **Accumulate is ready.**&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-11 at 17.30.11.png" alt=""><figcaption><p>Accumulate is ready</p></figcaption></figure>

#### **Scan for a Ledger device using the CLI**

**Note:**  The Accumulate ledger app must be open and your device unlocked.

<pre><code><strong>accumulate ledger info</strong></code></pre>

The above command will scan the USB port(s) for ledger devices and return an output similar to the following:

```
Wallets:
1	Manufacturer:	Ledger
	Product:	Nano S Plus
	Vendor ID:	11415
	Product ID:	20497
	App Version:	1.0.2
	Status:		ok
	Wallet ID:	acc://c6a629f9a65bf21159c5dfbffbc868ec3ae61ce4651108ec

```

The Wallet ID will reference the device, representing the first Accumulate lite address.

## **Send token to a lite account.**

In this section, you will learn how to send a token to a lite account using the Accumulate Ledger CLI.

{% hint style="info" %}
Version 1.0 of the app only supports Send Tokens and Add Credits.
{% endhint %}

{% hint style="info" %}
Run all your commands in the **`accumulate`** folder
{% endhint %}

To send a token, you need to follow the steps below.&#x20;

* Generate a Ledger key.
* Generate a faucet.
* Add credit to your Accumulate Ledger wallet ID.
* Send token.

#### **1. Generate the Ledger key**

This will store the public key along with the derivation path & wallet id in the wallet database.

&#x20;  **Syntax**

```
accumulate ledger key generate [key label]
```

&#x20;  **Command**

```
./accumulate ledger key generate wise
```

After running the command above, your Ledger device will prompt you to **Review Key Information.**

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-18 at 11.39.59.png" alt=""><figcaption><p>Confirm Key Name</p></figcaption></figure>

* Press the right button till you see, `Approve.`

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-18 at 11.39.43.png" alt=""><figcaption></figcaption></figure>

* Then press both buttons to approve the request.
* Now, you will see **Accumulate is ready.**&#x20;

The above command will return an output similar to the following on your Accumulate Ledger CLI:

```
 name            :       wise
 wallet ID       :       acc://1336bbe9ab0de46cbf2cbe539697ed0f654a0fddfefe8455
 public key      :       6eb9dfa41b3400d4ea226a52a0c93484ae61e3cd02ccee27c5373a8d2049d732
 key type        :       ed25519
```

Congratulations 🥳🥳👏👏🥳👏🥳👏🥳, Accumulate CLI is ready for use. Your key is now registered with the CLI and from this point forward, you can perform transactions using the ledger simply by referencing the registered key name or public key.&#x20;

{% hint style="danger" %}
When using the registered ledger key, your Accumulate ledger app must be open, and your device unlocked.
{% endhint %}

{% hint style="info" %}
Your wallet id is also known as your lite account. You will add**`/ACME`**at the end of the wallet id **`acc://1336bbe9ab0de46cbf2cbe539697ed0f654a0fddfefe8455/ACME`**
{% endhint %}

#### **4. Add credit**

This command will add credit to your lite account.

{% hint style="info" %}
Make sure your Accumulate app is opened on the Ledger device.
{% endhint %}

**Syntax**

```
 accumulate credits [origin token account] [key page or lite identity url] [number of credits wanted] [max acme to spend]
```

**Command**

```
./accumulate credits acc://1336bbe9ab0de46cbf2cbe539697ed0f654a0fddfefe8455/ACME acc://1336bbe9ab0de46cbf2cbe539697ed0f654a0fddfefe8455/ACME 50
```

After running the above command, your Ledger device will prompt you to **Review Add Credits**.

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-31 at 14.39.57.png" alt=""><figcaption></figcaption></figure>



* Press the left button till you see, `Approve.`

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-18 at 11.39.43.png" alt=""><figcaption></figcaption></figure>

* Then press both buttons to approve the request.

The above command will return an output similar to the following:

```
 Transaction Hash : eee36ce9bdde941b3e6a8f5ab1be226053cffefacb629ee985598fcddf7ed6da
 Signature 0 Hash : b54eccd2b600a7b0be112a17e2574bbfb62d04458861435d777a4f2ad0210449
 Simple Hash : 27a61ccf3656b685f4fadfeb6ca293338bc3ade4ac3dd7042bade30515c840ce
 Error code : ok
 Result : Oracle $5000.00 / ACME
                                  Credits 5000.00
                                  Amount 0.01000000 ACME
```

#### **5. Send tokens**

This command will send a token from one lite account to another.

**Syntax**

```
 accumulate tx create [lite token account url] [to] [amount] Create new token tx
```

**Command**

```
./accumulate tx create acc://4fde6a90d5a19af0ff2a745dd8d608c2ceeafdbd098f172a/ACME acc://4fde6a90d5a19af0ff2a745dd8d608c2ceeafdbd098f172a/ACME 10
```

After running the above command, your Ledger device will prompt you to **Review Send Tokens**.

<figure><img src="../../.gitbook/assets/Screenshot 2022-11-04 at 10.53.46.png" alt=""><figcaption></figcaption></figure>

* Press the left button till you see, `Approve.`
* Then press both buttons to approve the request.

The above command will return an output similar to the following:

```
Transaction Hash : 0a00f374aa2c04a9b6040c87eb43b22716437420a17c0cc40193fca2ce65afa9
Signature 0 Hash : 6161371cc457a3f699f1bfff7fb6cc19de0595baacb42e34783ec4ab2a396834
Simple Hash : 4b3158ad75c65a71176e318e95fe0d641a16d111300cf4cf53fe53b0eb016e36
Error code : ok
Result : 
```

### **Get token balance**

The get token command will query the balance to check the token balance of a Lite Token Account. The Token URL in the output specifies the type of Token.

**Syntax**

```
accumulate get [url] Get data by Accumulate URL
```

**Command**

```
./accumulate get acc://4fde6a90d5a19af0ff2a745dd8d608c2ceeafdbd098f172a/ACME
```

The above command will return an output similar to the following:

```
Account Url : acc://4fde6a90d5a19af0ff2a745dd8d608c2ceeafdbd098f172a/ACME
Token Url : acc://ACME
Balance : 2000000.00000000 ACME
```
