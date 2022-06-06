# Local DevNet Setup

The fastest way to experiment with the Accumulate CLI or API is to replace the Accumulate Testnet with a running local devnet.&#x20;

&#x20;A local devnet allows you to run accumulate Node locally on your computer and it's hosted on your company.&#x20;

&#x20;

**Requirements**&#x20;

* You should have Go 1.18 installed on your machine.&#x20;
* You should have a basic knowledge of CLI.&#x20;
* You should have the Accumulate CLI setup already.&#x20;

To set up the Accumulate CLI tool, go to [cli-setup.md](../cli/cli-setup.md "mention").&#x20;

You can run a local devnet with the Accumulate Github or Gitlab source code. &#x20;

{% hint style="info" %}
The CLI default network uses the Testnet devnet
{% endhint %}

## **Follow the steps below for Mac:**&#x20;

&#x20;

**Initialize the Devnet**&#x20;

Use this command below to initialize the local devnet&#x20;

```
go run ./cmd/accumulated init devnet -w .nodes -f 0 -v 1 -b 1 --no-empty-blocks --no-website --reset 
```

* init devnet: Initialize the configure files for the devnet &#x20;
* \--no-empty-blocks: A Tendermint command that will not allow empty blocks stored in the database&#x20;
* \--no-website: this will stop the creation of a website&#x20;
* \--reset: This flag will delete the previous configuration that you have or data&#x20;
* \-w.nodes: is the working directory that the data is stored&#x20;
* \-v 1: specifies how many validators that you are using&#x20;
* \-b 1: is the number of BVN that you are using&#x20;
* \-f 0: x is the number of followers&#x20;

{% hint style="info" %}
Before you run the code make sure you “git checkout” the branch for the network version you want for your local devnet. Please see Networks\[LINK] for a list of available versions.&#x20;
{% endhint %}

**Local network IP Address**&#x20;

```
export ACC_API=http://127.0.1.1:26660/v2 
```

The export ACC\_API makes this `http://127.0.1.1:26660/v2` address on your CLI to look for this IP on the local network&#x20;

**Add Loopback Alias**&#x20;

```
sudo ifconfig lo0 alias 127.0.1.1 
```

If you run the above command, it will prompt you to add your computer admin password. After that make sure to repeat this step till you get to 9.&#x20;

**Example**\


```
$ sudo ifconfig lo0 alias 127.0.1.1  
$ sudo ifconfig lo0 alias 127.0.1.2 
$ sudo ifconfig lo0 alias 127.0.1.3 
$ sudo ifconfig lo0 alias 127.0.1.4 
$ sudo ifconfig lo0 alias 127.0.1.5 
$ sudo ifconfig lo0 alias 127.0.1.6 
$ sudo ifconfig lo0 alias 127.0.1.7 
$ sudo ifconfig lo0 alias 127.0.1.8 
$ sudo ifconfig lo0 alias 127.0.1.9  
```

In Mac, you have to do this step from 127.0.1.1 - 127.0.1.9 because Mac requires a loopback alias.&#x20;

**Run the Devnet**&#x20;

```
go run ./cmd/accumulated run devnet -w .nodes 
```

To check that the devnet is running fine, open a new terminal and run the below command in the accumulate folder&#x20;

```
./scripts/ci/validate.sh 
```

The above command will return an output similar to the following:&#x20;

```

Setup 
Installing CLI 
 
 
Generate a Lite Token Account 
./scripts/ci/validate.sh: line 127: jq: command not found 
wisdomnwokocha@wisdoms-MBP accumulate % ./scripts/ci/validate.sh 
Setup 
Installing CLI 
 
 
Generate a Lite Token Account 
1f1bb66968df68f71b200135df74b127fcdc2dab8472d82c7825edf4c36121c7 
Waiting for 1f1bb66968df68f71b200135df74b127fcdc2dab8472d82c7825edf4c36121c7 
{"type":"acmeFaucet","data":{"type":"acmeFaucet", 
"url":"acc://02da9c2bdfcd54a2a56f4ad0dc315c0786b38df7656eb304/ACME"}, 
"origin":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME", 
"sponsor":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME", 
"transactionHash":"1f1bb66968df68f71b200135df74b127fcdc2dab8472d82c7825edf4c36121c7", 
"txid":"1f1bb66968df68f71b200135df74b127fcdc2dab8472d82c7825edf4c36121c7", 
"transaction":{"header":{"principal":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME", 
"origin":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","initiator":"dd4602c69be84ef506b30252fe6d149aef6b1c5890958b746cb96a4ee42aa886"}, 
"body":{"type":"acmeFaucet","url":"acc://02da9c2bdfcd54a2a56f4ad0dc315c0786b38df7656eb304/ACME"}}, 
"signatures":[{"type":"ed25519","publicKey":"d03c683332ed36add8d0eeb9eee9e2669b5565decec03acc43d762f3f79f49c2", 
"signature":"a05c49f63370cfe01878d4d9f596e5e890fe5408f562df92aecccbffc9e6ec35e798423b3ddfb3e3ce01d4f4646f0140c8938bc8e84a88f5f1e8dd6d44e9db00", 
"signer":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME", 
"signerVersion":1,"timestamp":1650645938374084900, 
"transactionHash":"1f1bb66968df68f71b200135df74b127fcdc2dab8472d82c7825edf4c36121c7"}], 
"status":{"delivered":true,"result":{"type":"unknown"}, 
"initiator":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME", 
"signers":[{"type":"liteTokenAccount", 
"url":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME", 
"tokenUrl":"acc://ACME","balance":"314159265358979323846264338327950288419716939937510582097494459", 
"lastUsedOn":1650645938374084900, 
"nonce":1650645938374084900}]}, 
"syntheticTxids":["6aec3ac62f099775f4daf9c2e3a67a4d77cb45c743d8bbf90fda9e88129fbd83"], 
"signatureBooks":[{"authority":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME", 
"pages":[{"signer":{"type":"liteTokenAccount","url":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME"},"signatures":[{"type":"ed25519","publicKey":"d03c683332ed36add8d0eeb9eee9e2669b5565decec03acc43d762f3f79f49c2","signature":"a05c49f63370cfe01878d4d9f596e5e890fe5408f562df92aecccbffc9e6ec35e798423b3ddfb3e3ce01d4f4646f0140c8938bc8e84a88f5f1e8dd6d44e9db00","signer":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","signerVersion":1,"timestamp":1650645938374084900,"transactionHash":"1f1bb66968df68f71b200135df74b127fcdc2dab8472d82c7825edf4c36121c7"}]}]}]} 
```

## **Follow the steps below for Windows:**&#x20;

&#x20;

### **Build accumulated (the node daemon)**&#x20;

Use this command below to build accumulate.&#x20;

```
go build ./cmd/accumulated 
```

### **Initialize the devnet**

Use this command below to initialize the local devnet.&#x20;

**Syntax**&#x20;

.\accumulated init devnet --bvns 1 --validators 1 --followers 0 --reset -w '\<location where you want data to be stored>'&#x20;

**Example**&#x20;

```
.\accumulated init devnet --bvns 1 --validators 1 --followers 0 --reset -w ' D:\.accumulate:\accumulate 
```

* init devnet: Initialize the configure files for the devnet &#x20;
* \--bvns 1: is the number of BVN that you are using&#x20;
* \--validators 1: specifies how many validators that you are using&#x20;
* \--followers 0: The number of followers you are using&#x20;
* \--log-levels 'error;executor=debug': (optional) to receive logs after running devnet&#x20;
* \--reset: This flag will delete the previous configuration that you have &#x20;
* \-w (optional) the working directory where you want data to be stored&#x20;

The above command will return an output similar to the following:&#x20;

```
Deleting D:\.accumulate/bvn0 
Deleting D:\.accumulate/dn  
```

**Run the Devnet**&#x20;

```
.\accumulated run devnet 
```

Add ‘-w’ if you included in the previous command 'D:\\.accumulate'&#x20;

{% hint style="info" %}
in order to point the CLI to your local devnet, you must add ‘-s local’ to each command.
{% endhint %}

To test if your devnet is working, checkout the [CLI guide](https://docs.accumulatenetwork.io/accumulate/cli/cli-reference).&#x20;
