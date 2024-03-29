# CLI setup

The Accumulate CLI (Command Line Interface) installation and the binary installation are the fastest way to get Accumulate running locally. This guide will show you how to set up Accumulate locally.

## Two ways of CLI setup

* Binary installation
* From the source

### **1. Binary Installation** v0.6.3

**Step 1:** Choose one of the following:

{% tabs %}
{% tab title="Windows" %}
{% embed url="https://gitlab.com/accumulatenetwork/core/wallet/-/jobs/artifacts/v0.6.3/file/accumulate-windows-amd64.exe?job=binaries" %}
Intel/AMD
{% endembed %}

{% embed url="https://gitlab.com/accumulatenetwork/core/wallet/-/jobs/artifacts/v0.6.3/file/accumulate-windows-arm64.exe?job=binaries" %}
ARM
{% endembed %}

Rename the file to **accumulate.exe**
{% endtab %}

{% tab title="Mac OS" %}
{% embed url="https://gitlab.com/accumulatenetwork/core/wallet/-/jobs/artifacts/v0.6.3/file/accumulate-darwin-amd64?job=binaries" %}
Intel
{% endembed %}

{% embed url="https://gitlab.com/accumulatenetwork/core/wallet/-/jobs/artifacts/v0.6.3/file/accumulate-darwin-arm64?job=binaries" %}
Apple M1/M2
{% endembed %}

Rename the file to **accumulate**
{% endtab %}

{% tab title="Linux" %}
{% embed url="https://gitlab.com/accumulatenetwork/core/wallet/-/jobs/artifacts/v0.6.3/file/accumulate-linux-amd64?job=binaries" %}
Intel/AMD
{% endembed %}

{% embed url="https://gitlab.com/accumulatenetwork/core/wallet/-/jobs/artifacts/v0.6.3/file/accumulate-linux-arm64?job=binaries" %}
ARM
{% endembed %}

Rename the file to **accumulate**
{% endtab %}
{% endtabs %}

**Step 2:** Move **accumulate** to a folder of your choice.

Moving it to your **documents** folder is recommended, making it easier to locate on your terminal.

**Step 3:** In order to set the permissions so you can run this file, type in the following command: `chmod 744 <path_to_file>`. Pro tip: drag and drop the accumulate file onto the terminal to get the path.

**Step 4:**  Copy the binary file location and paste it into your terminal and press enter to bring up the usage guide. Pro-tip: after the first time you drag and drop, you can press the Up arrow key to repeat for every future command.

You can start using the [Accumulate CLI commands.](https://docs.accumulatenetwork.io/accumulate/cli/cli-reference)

**How to access Accumulate CLI from anywhere in the terminal.**

{% hint style="info" %}
&#x20;**This is an optional step**
{% endhint %}

This step makes it easier to run accumulate since you can call it anywhere in your terminal.

You can follow the instructions in this [link](https://zwbetz.com/how-to-add-a-binary-to-your-path-on-macos-linux-windows/#windows-cli)



### 2. From source

#### **Preparing the installation**

The CLI installation guide needs two requirements.

* GO language 1.18 version
* Terminal or any command line interface of your choice

#### **Step 1: Clone accumulate**

```
git clone https://gitlab.com/accumulatenetwork/core/wallet.git
```

#### **Step 2: Locate accumulate folder**

```
cd wallet
```

#### **Step 4: Build Accumulate**

This command works for Mac/Linux and Windows

```
go build ./cmd/accumulate
```

Once you run the command above, an **accumulate** binary file should appear in the root directory `accumulate`, which enables the CLI Commands.

#### **Step 5: Initialize your wallet**

This command will walk you through initializing your wallet:

```
./accumulate wallet init
```

If this is your first time using the Accumulate wallet, you will be prompted to
set some general configuration options.

```
? Automatically run the wallet daemon in the background when the CLI is used?:
  ▸ Yes (password(s) will be remembered for 10 minutes)
    No (enter your password(s) each time)
```

Running the daemon in the background is convenient because it lets the CLI
remember your passwords for up to 10 minutes after the last command, but it is
somewhat less secure. If an attacker gains direct control of your PC, they could
potentially abuse this feature to steal your keys.

You will be asked if you want to create a single- or multi-vault wallet. **Most
users should choose a single-vault wallet.** Advanced users may wish to choose a
multi-vault wallet as it allows multiple mnemonics and sets of keys to be used,
with (optionally) different encryption keys.

```
? Wallet mode:
  ▸ Single vault
    Multi vault
```

Next you will be asked if you want to encrypt your wallet. **Encrypting your
wallet is highly recommended.**

```
? Encrypt keys?:
  ▸ Yes
    No
```

If you chose to encrypt your wallet, you will be prompted to enter and confirm
the new encryption passphrase.

```
New password: ****
Confirm password: ****
```

If you are creating a multi-vault wallet, the command will now exit. See
[Managing
vaults](https://docs.accumulatenetwork.io/wallet/vaults/managing-vaults#create-a-new-vault)
for instructions on how to create vaults.

If you are creating a single-vault wallet, you will be asked if you wish to
generate a new mnemonic, import an existing one, or skip.

```
Use the arrow keys to navigate: ↓ ↑ → ←
? Mnemonic:
  ▸ Create
    Import
    Skip
```

If you chose to create a new mnemonic, you will be prompted to write down your
generated **mnemonic phrase** in the terminal and press enter.

{% hint style="info" %}
Please keep your **mnemonic phrase** safe, it will help you restore the wallet.
{% endhint %}

#### **Step 5: Start the CLI Tool**

To test that the Accumulate is installed correctly, run the below command without arguments.

**On Mac / Linux / Windows**

```
./accumulate
```
