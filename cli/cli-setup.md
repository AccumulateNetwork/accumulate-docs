# CLI setup

The Accumulate CLI (Command Line Interface) installation is the fastest way to get Accumulate running locally. The following guide is the installation option most recommended by Accumulate.

## Download

Latest release: [https://gitlab.com/accumulatenetwork/core/wallet/-/jobs/artifacts/v0.3.3/browse?job=build%20binaries](https://gitlab.com/accumulatenetwork/core/wallet/-/jobs/artifacts/v0.3.3/browse?job=build%20binaries)

Latest build: [https://gitlab.com/accumulatenetwork/core/wallet/-/jobs/artifacts/main/browse?job=build%20binaries](https://gitlab.com/accumulatenetwork/core/wallet/-/jobs/artifacts/main/browse?job=build%20binaries)

If you are running macOS on an Intel-based Mac, use accumulate-darwin-amd64. If you are running macOS on an Apple-silicon Mac, use accumulate-darwin-arm64.

## From source

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

#### **Step 5: Create a seeded wallet**

This command will create a mnemonic seed and wallet locally.

```
./accumulate wallet init create
```

After running the command above, you will be requested to write down your generated **mnemonic phrase** in the terminal and press enter.

{% hint style="info" %}
Please keep your **mnemonic phrase** safe, it will help you restore the wallet.
{% endhint %}

Also, if you have an existing Accumulate wallet, then you can `import` the wallet using the command below.

```
./accumulate wallet init import
```

Import a mnemonic seed via the command prompt or import a wallet backup file to create a wallet

To backup, your wallet

```
accumulate wallet export mywallet.json
```

To restore from the backup

```
accumulate wallet init import keystore mywallet.json
```

#### **Step 5: Start the CLI Tool**

To test that the Accumulate is installed correctly, run the below command without arguments.

**On Mac / Linux / Windows**

```
./accumulate
```
