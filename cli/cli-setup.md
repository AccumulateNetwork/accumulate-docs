# CLI Setup

The Accumulate CLI (Command Line Interface) installation is the fastest way to get Accumulate running locally. The following guide is the installation option most recommended by Accumulate.

### **Preparing the installation**

The CLI installation guide needs two requirements.

* GO language 1.18 version
* Terminal or any command line interface of your choice

### **Step 1: Clone accumulate**

```
git clone https://gitlab.com/AccumulateNetwork/accumulate.git
```

{% hint style="info" %}
The `accumulate`repository is also available on [Github](https://github.com/AccumulateNetwork/accumulate): `https://github.com/AccumulateNetwork/accumulate.git`
{% endhint %}

### **Step 2: Locate accumulate folder**

```
cd accumulate
```

### **Step 3: Checkout a branch (optional)**

Depending on the network you are connecting to, you may need to checkout a different branch. For best results, the CLI version must match the API version. Please see [networks.md](../getting-started/networks.md "mention") for the list of available networks and which branch to checkout.

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
