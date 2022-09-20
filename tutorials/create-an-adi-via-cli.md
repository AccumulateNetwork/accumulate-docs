# Create an ADI via CLI

Accumulate Digital Identifiers are human-readable addresses similar to website URLs that are chosen by individuals or assigned by organizations to represent their presence on the blockchain. Digital identifiers are a system for assigning unique digital identities to assets, individuals, or entities on the blockchain.

Using ADIs, Accumulate can serve as the de-facto communication and audit layer between blockchains, enabling the seamless transfer of tokens or other digital assets between ADIs across different chains regardless of their consensus mechanism.

**Prerequisites**

* Basic knowledge of Accumulate(Accumulate link)
* Basic knowledge of CLI
* Basic knowledge of Rest API
* Basic knowledge of VueJS, Javascript
* [Node.js v14 or newer](https://nodejs.org/) installed.
* A JavaScript package manager, you’ll use npm as your JavaScript package manager, which is included when you install Node.

According to the whitepaper, “_Accumulate by-passes the trilemma of security, scalability, and decentralization by implementing a chain-of-chains architecture in which digital identities with the ability to manage keys, tokens, data, and other identities are treated as their independent blockchains.”_

Each ADI is made up of a collection of independent sub-chains that are managed by four account types:

* Token Accounts: For issuing tokens and tracking deposits and withdrawals from a token account.&#x20;
* Data Accounts: For tracking and organizing data approved by an ADI
* Staking Accounts: For staking Accumulate’s ACME tokens to participate in consensus and secure the network&#x20;
* Scratch Accounts: For accruing data needed to build consensus across the Accumulate network and enable the coordination of multisig validation.&#x20;

## **Structure**

Any number of accounts or sub-ADIs can be nested within an ADI. Accounts and sub-ADIs are independent of each other and possess their own sets of keys with which they can manage their assets. The parent ADI possesses an administrative key set that can add, delete, transfer, or modify the security of its accounts or sub-ADIs. Data and token accounts are terminal, meaning they cannot have nested accounts. However, sub-ADIs and accounts can be nested within another sub-ADI.

## **Sub-ADIs | Data Account | Token Account**

{% tabs %}
{% tab title="Sub ADI" %}
An nth generation ADI that is created within another ADI.&#x20;
{% endtab %}

{% tab title="Second Tab" %}
Holds and exchanges tokens that belong to an ADI.&#x20;
{% endtab %}

{% tab title="ADI Data Account" %}
Records data entries that belong to an ADI
{% endtab %}
{% endtabs %}

## **Creating an ADI through the CLI**

This tutorial will create your ADI using an Accumulate lite account.

Steps:

* Generate lite account
* Add a faucet
* Generate a key
* Add credit
* Create ADI

### **Generate a lite account**

This command will generate a new lite account.

**Run command**

```
./accumulate account generate 
```

**The above command will return an output similar to the following:**&#x20;

```
        name : c919b88657932724a037c1ae227bdc493249477901dba032
        lite account : acc://c919b88657932724a037c1ae227bdc493249477901dba032/ACME
        public key : 4a040f87872c39d1a17ca7c85674bfc93905ec26275abda4d7612a9f21f83c71
        key type : ed25519
```

### **Add a Faucet**

This command will add a faucet to your account.

The default number of faucets added to your account per transaction is **50.**

**Run command**

```
./accumulate faucet 
acc://c919b88657932724a037c1ae227bdc493249477901dba032/ACME
```

**The above command will return an output similar to the following:**&#x20;

```
        Transaction Hash : 321ca61d60ef927bba1471be2cad06b2d04b0deb79174f8e68f135e84670dc9f
        Signature 0 Hash : bfdba62c475475e9f669f9afc3e0e6acdd787fe443ae686368fd773128166629
        Simple Hash : a2c78ee8b3f2d3b2703e4475b349f3474f4f023a940c903b6d7b36cb4bdbf2ad
        Error code : ok
        Result : 
```

### **Generate a key**

This command will generate a new key&#x20;

**Run command**

```
./accumulate key generate key1234
```

**The above command will return an output similar to the following:**&#x20;

```
        name : key1234
        lite account : acc://519a89a6107e4f6ba122595c70b7bf72dc76cdd720b4f917/ACME
        public key : 214fccb6e54d8896d4a7ee5daaa85e065fb41a18c4eda5e0eee6947a42c125a4
        key type : ed25519
```

### **Add credit**

This command will add credit(link) to your lite account

**Run command**

```
./accumulate credits acc://c919b88657932724a037c1ae227bdc493249477901dba032/ACME acc://c919b88657932724a037c1ae227bdc493249477901dba032/ACME 1000
```

**The above command will return an output similar to the following:**&#x20;

```
        Transaction Hash : 2524f7fbf3ffd9c13f3ba5d50baef83739f4e12e340c7efca38aafd959239044
        Signature 0 Hash : 9c23ad733b834fb21673b1e94ff27c857a28304aa39b4e09eba26ae115a21b86
        Simple Hash : 0f70d11937a28a825aa0cbb8d17696d748c81f6620c08329315959f41c7db5cf
        Error code : ok
        Result : Oracle $0.05 / ACME
                                  Credits 100.00
                                  Amount 20.00000000 ACME
```

### **Create ADI**

This command creates a new ADI from a lite token account.

**Note:** The minimum credit to create an ADI is 500

**Syntax**

```
accumulate adi create [origin-lite-account] [adi url to create] [public-key or key name] [key-book-name (optional)] [public key page 1 (optional)] 
```

* **Lite account:** You will use the generated lite account; it’s mandatory
* **adi url:** You will choose your ADI url; it’s mandatory
* **key name:** You will use the generated key; it’s mandatory
* **key-book:** it’s optional because the system will create one for you, except you created a key book to add.

{% hint style="info" %}
When public-key one is specified, it will be assigned to the first page. Otherwise, the origin key is used.
{% endhint %}



**Run Command**

```
./accumulate adi create 
acc://c919b88657932724a037c1ae227bdc493249477901dba032/ACME acc://ADItut.acme key1234
```

**The above command will return an output similar to the following:**&#x20;

```
  Transaction Hash : 66b9ca00c35144c08a4a25b452827c669d740389e674e1585c7902cebbaa1ccb
  Signature 0 Hash : 349e9239b2ebdf012a7a2f27f4e764899bd7a8fef9ca3f1eca17f71cbcfdc6f2
  Simple Hash : eaabe4b2c1b08996507224ae6475742d28096bd0d33fe8540ffb779cec3fce9f
  Error code : ok
  Result : 
```

##
