---
description: This guide will run you through how to create a Validator Node.
---

# Validator node setup with AccMan

The validator node connects to the Accumulate network and allows users to record and sign transactions in the Accumulate blockchain.&#x20;

Please complete the [follower-node-setup-with-accman.md](follower-node-setup-with-accman.md "mention"). To become a Validator Node, a Follower Node is created first. It is recommended to use Accman for this process. Please&#x20;

{% hint style="info" %}
A Validator is the same as a follower, except it is trusted to check everything. It is accepted if enough Validators (usually 51%) agree. &#x20;
{% endhint %}

{% hint style="info" %}
Click the images to enlarge them.
{% endhint %}

![](<../.gitbook/assets/image (5) (1).png>)

Select "Accumulate - Manage Node" and hit Enter.

![](<../.gitbook/assets/image (6).png>)

Scroll Down to “Display Registration Info” and Click Enter.

![](<../.gitbook/assets/image (1).png>)

The Public Key (pubkey) is what an Operator will provide as their **Validator Key** to the Protocol.

The address is a Hash of the Public Key.

The Operator's Operator Key is recommended to be different from the Validator Key.\


An **Operator Key** can be generated in the Command Line Interface.

**Syntax**

```
./accumulate key generate [Key Name]
```

**Command**

```
./accumulate key generate operatorkey1 
```

The above command will return an output similar to the following:&#x20;

```
name : operatorkey1 lite account : acc://11d3217fda3c863c2e66936826987edb3a4467f540279689/ACME
public key : 1df37076ff875fc2a9c99a647622d33b1c194ff0d821c40b93fffac1743acca2
key type : ed25519
```

The Public Key in the Output will serve as the **Operator Public Key.**

_Please provide the **Validator Public Key** and **Operator Public Key** to a member of the Operator Key Page. Two-thirds of the Operators will sign a transaction to add your **Operator Key** and a second transaction to add your **Validator Key.** For more information, please see the_ [_Operator Onboarding Guide_](https://docs.accumulatenetwork.io/accumulate/nodes/operator-onboarding-guide)_._

When you search on a Web Page, your node's I.P. (I.P. :16592.status), if the voting power is 0, you are running a follower node. If the voting power is 1, you are running a Validator Node.&#x20;

![](<../.gitbook/assets/image (3).png>)

In a future AccMan release, the type of Node you are running will be visible in your AccMan console.

_To verify, your **operator key** is on the **operator key page.**_&#x20;

_Run this command_

```
./accumulate get dn.acme/operators/1 
```

_To verify your **validator key** is in the **networks data account**._

_Run this command_

```
./accumulate get dn.acme/network
```

\
