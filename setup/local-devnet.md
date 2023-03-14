# Local DevNet Setup

The fastest way to experiment with the Accumulate CLI or API is to replace the Accumulate Testnet with a running local devnet.

A local devnet allows you to run accumulate Node locally on your computer, and it's hosted on your company.

**Requirements**

* You should have Go 1.18 installed on your machine.
* You should have a basic knowledge of CLI.
* You should have the Accumulate CLI setup already.

To set up the Accumulate CLI tool, go to [cli-setup.md](../cli/cli-setup.md "mention").

You can run a local devnet with the Accumulate Github or Gitlab source code.

{% hint style="info" %}
When using the CLI tool with your local devnet, you must specify the CLI to point to localhost by appending`-s local` with every command.
{% endhint %}

## **Follow the steps:**&#x20;

## **1. Mac:**

**Initialize the Devnet**

{% hint style="danger" %}
WARNING: Be extremely careful with the `--reset` flag, as it permanently deletes files on your computer. If you set a custom location for your configuration with the `-w` flag, it will delete whatever you specify in the directory. If you need to use `-w` , specify an empty directory, so no files are at risk.
{% endhint %}

{% hint style="info" %}
Before you run the code, make sure you “git checkout” the branch for the network version you want for your local devnet. Please see [networks.md](../getting-started/networks.md "mention") for the list of available versions.
{% endhint %}

Use this command below to initialize the local devnet

```
go run ./cmd/accumulated init devnet -w .nodes -f 0 -v 1 -b 1 --no-empty-blocks --no-website --reset 
```

* init devnet: Initialize the configure files for the devnet
* \--no-empty-blocks: A Tendermint command that will not allow empty blocks stored in the database
* \--no-website: this will stop the creation of a website
* \--reset: This flag will delete the previous configuration that you have or the data
* \-w .nodes: is the working directory where the data is stored (you can also specify a custom location).
* \-v 1: specifies how many validators that you are using
* \-b 1: is the number of BVN that you are using
* \-f 0: x is the number of followers

**Local network IP Address**

```
export ACC_API=http://127.0.1.1:26660/v2 
```

The export `ACC\_API` the command sets the CLI to look for this IP address when executing commands.

**Add Loopback Alias**

```
sudo ifconfig lo0 alias 127.0.1.1 
```

If you run the above command, it will prompt you to add your computer admin password. After that, repeat this step until you get to 9.

**Example**

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

In Mac, you have to do this step from 127.0.1.1 - 127.0.1.9 because Mac requires a loopback alias.

**Run the Devnet**

```
go run ./cmd/accumulated run devnet -w .nodes 
```

To check that the devnet is running fine, open a new terminal and run the below command in the accumulate folder

```
./scripts/ci/validate.sh 
```

The above command will return an output similar to the following:

```
Setup 
Installing CLI 
 
 
Generate a Lite Token Account 
./scripts/ci/validate.sh 
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

## **2. Windows:**

### **Build accumulated (the node daemon)**

Use this command below to build accumulate.

```
go build ./cmd/accumulated 
```

### **Initialize the devnet**

Use this command below to initialize the local devnet.

**Syntax**

```
.\accumulated init devnet --bvns 1 --validators 1 --followers 0 --reset -w '<location where you want data to be stored (optional)>'
```

{% hint style="warning" %}
WARNING: Be extremely careful with the `--reset` flag, as it permanently deletes files on your computer. If you set a custom location for your configuration with the `-w` flag, it will delete whatever is in the directory you specify. If you need to use `-w`, specify an empty directory, so no files are at risk.
{% endhint %}

* \--bvns 1: is the number of BVN that you are using
* \--validators 1: specifies how many validators that you are using
* \--followers 0: The number of followers you are using
* \--log-levels 'error;executor=debug': (optional) to receive logs after running devnet
* \--reset: This flag will delete the previous configuration that you have
* \-w (optional) the working directory where you want data stored. If omitted, a working directory will be added in the default location.

The above command will return an output similar to the following:

```
Deleting D:\.accumulate/bvn0 
Deleting D:\.accumulate/dn  
```

**Run the Devnet**

```
.\accumulated run devnet 
```

Add ‘-w’ if you included in the previous command 'D:\\.accumulate'

{% hint style="info" %}
To point the CLI to your local devnet, add ‘-s local’ to each command.
{% endhint %}

To test if your devnet is working, check out the [CLI guide](https://docs.accumulatenetwork.io/accumulate/cli/cli-reference).
