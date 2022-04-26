# CLI Setup

The Accumulate CLI (Command Line Interface) installation is the fastest way to get Accumulate running locally. The following guide is the installation option most recommended by Accumulate.&#x20;

### **Preparing the installation**&#x20;

The CLI installation guide needs two requirements.&#x20;

* GO language 1.18 version&#x20;
* Terminal or any text editor of your choice&#x20;

&#x20;

### **Step 1: Clone accumulate from Github**&#x20;

```
git clone 
https://github.com/AccumulateNetwork/accumulate.git
```

### **Step 2: Change branch**&#x20;

In your terminal type the below command to switch to the develop branch. At the moment, the branch supports the Accumulate CLI.&#x20;

```
git checkout develop 
```

### **Step 3: Locate Accumulate folder**&#x20;

```
cd accumulate
```

### **Step 4: Build Accumulate** &#x20;

**Mac/Linux**

```
make accumulate 
```

#### Windows

```
go build ./cmd/accumulate
```

Once you run these commands, an accumulate binary file should appear in the root directory accumulate that enables the CLI Commands.&#x20;



### **Step 5: Start the CLI Tool**&#x20;

To test that the Accumulate is installed correctly, run the below command without arguments.&#x20;

&#x20;

**On Mac / Linux / Windows**

```
./accumulate
```

&#x20;

&#x20;
