---
description: >-
  This guide will run you through how to create a Validator Node to an
  Accumulate network.
cover: ../.gitbook/assets/AccMan.png
coverY: 4.783333333333334
---

# Follower Node Setup with Accman

&#x20;A unique type of full node called a validator node takes part in "consensus." By taking part in consensus, validator nodes take on additional responsibilities such as transaction verification, voting, and maintaining a record of transactions.&#x20;

The validator node connects to the Accumulate network and allows users to record and sign transactions in the Accumulate blockchain. &#x20;

{% hint style="info" %}
&#x20;A transaction must be validated and authorized before being added to the blockchain. &#x20;
{% endhint %}

A Validator is the same as a follower, except that it is trusted to check everything. It is accepted if enough Validators (usually 51%) agree on something. &#x20;

![](../.gitbook/assets/AccMan.png)

{% embed url="https://www.youtube.com/watch?v=dN-ocP--Jl0" %}
Video Walkthrough
{% endembed %}

### **AccMan** &#x20;

**AccMan aka (Accumulate Manager runner)**&#x20;

The AccMan is a package that allows you to start the installation process of Accumulate manager.&#x20;

Using the Accumulate manager is the recommended method of running a node on the Accumulate network. For more info about Accumulate manager, click here (Accumulate manager is a tool (watch the video); it is simple but powerful.).&#x20;

**Prerequisites**&#x20;

* Experience using the command line.&#x20;
* Basic knowledge about Accumulate.&#x20;
* You need to have git installed.&#x20;
* A Linux server that matches or exceeds the minimum specification for the intended purpose. See [https://accumulatenetwork.io/learn/#validators](https://accumulatenetwork.io/learn/#validators)  &#x20;
* Ubuntu is recommended (other Debian-based distributions should work out of the box).&#x20;
* It would help if you had Docker & docker-compose. [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/) [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/) (An optional install script is included for Ubuntu) &#x20;

{% hint style="info" %}
These steps are optimized for Linux servers, but you can install it on a personal Linux OS as well, by running the commands as root (use \`sudo su\` to switch to root in your terminal)&#x20;
{% endhint %}

Follow the steps below to set up your Accumulate \`Node\` on your machine.&#x20;

&#x20;**Update apt and install prerequisites**&#x20;

To install `AccMan`, you will need to log in as root.&#x20;

```
apt update && apt -y install git telnet net-tools mtr 
```

**Clone repo**&#x20;

```
git clone https://gitlab.com/accumulatenetwork/accman.git
```

**Locate accman folder**&#x20;

```
cd accman
```

**Run script**&#x20;

This script will install Ubuntu OS and the latest version of Docker.

```
./scripts/install-ubuntu.sh 
```

{% hint style="info" %}
The firewall assumes ssh access is on port 22. Read the firewall section if this is not the case. Failing to do so will lock you out of your server. Also, you will need to open ports for Accumulate to operate if you have an external firewall.&#x20;
{% endhint %}

**Run accman**&#x20;

This command will start Accumulate manager.&#x20;

```
./accman  
```

The above command will return an output similar to the following: &#x20;

![](<../.gitbook/assets/Screenshot 2022-08-10 at 14.51.57.png>)

From the Accumulate manager main menu&#x20;

* Click `Accumulate - Create`&#x20;
* Click `Start new Node` &#x20;
* **Select the network you wish to join.**&#x20;

```
Testnet-Stable         
Testnet-Beta 
```

* **Select a BVN**&#x20;

We recommend you select \`Auto.\`&#x20;

```
Auto 
BVN0 
BVN1 
```

* **Select the network you wish to join.**&#x20;

```
v0-6-0              
v0-6-0-rc0            
v0-6-0-rc1            
v0-6-0-rc2  
```

Now, you have your Follower`Node` running. 🥳🥳🥳&#x20;

Also, if you want to create an `ssh` login account, it will take you directly to the Accumulate Manager menu:&#x20;

```
./accman createuser accman
```

This will create a login account `accman`. The private keys from \`/root/.ssh/authorized\_keys\` will be copied to `/home/accman/.ssh/authorized_keys`. Edit as necessary.&#x20;

### **Firewall & Rate Limiting**&#x20;

Locking down your server is essential. By default, Accumulate Manager will take care of this for you. To make manual changes, edit the `iptables.sh` file accordingly.&#x20;

Remember, it is still your responsibility to ensure your server is secure.&#x20;

### **SSL certificates**&#x20;

A self-certificate is generated automatically on start-up. If you have an existing certificate for a domain name, copy the `.crt` and `.key` files to the `./certs` directory. They will be read on start-up; the\`.pem\` files are also compatible. &#x20;

Also, rename them to `.crt` and `.key` files. Make sure the files are kept valid. For example, if you provide an e-mail address, Accumulate Manager will attempt to get a certificate from `LetsEncrypt` and keep it renewed.&#x20;





