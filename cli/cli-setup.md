# CLI Setup

The Accumulate CLI (Command Line Interface) installation is the fastest way to get Accumulate running locally. The following guide is the installation option most recommended by Accumulate.

### **Preparing the installation**

The CLI installation guide needs two requirements.

* GO language 1.18 version
* Terminal or any command line interface of your choice

### **Step 1: Clone accumulate from Github**

```
git clone 
https://github.com/AccumulateNetwork/accumulate.git
```

### **Step 2: Locate Accumulate folder**

```
cd accumulate
```

### **Step 3: Checkout a branch (optional)**

Depending on the network you are connecting to, you may need to checkout a different branch. For best results, the CLI version must match the API version. As of 2022-5-26, these are the versions:

* Stable testnet (testnet.accumulatenetwork.io) runs v0.6, checkout `cli-v0.6`
* Beta testnet (beta.testnet.accumulatenetwork.io) runs v0.7-beta, checkout `cli-0.7.0-beta`
* Devnet (local or otherwise) runs the latest build, checkout `develop`

In your terminal type the below command to switch to a different branch.

```
git checkout ${branch_name}
```

### **Step 4: Build Accumulate**

**Mac/Linux**

```
make accumulate 
```

#### Windows

```
go build ./cmd/accumulate
```

Once you run these commands, an accumulate binary file should appear in the root directory accumulate that enables the CLI Commands.

### **Step 5: Start the CLI Tool**

To test that the Accumulate is installed correctly, run the below command without arguments.

**On Mac / Linux / Windows**

```
./accumulate
```
