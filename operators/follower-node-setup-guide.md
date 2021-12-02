# Follower Node Setup Guide

{% hint style="info" %}
This guide is for creating a Follower node on Accumulate, which only records transactions on the network. If you would like to set up a Validator node instead, which participates in consensus, please see the [node-setup-guide.md](node-setup-guide.md "mention")
{% endhint %}

#### Initializing the node

Run the following command to initialize the follower:

```d
./accumulate init follower --network "<NETWORK NAME>" --listen "tcp://0.0.0.0:26656"
```

This will generate the `~/.accumulate/Node0` directory with configs. &#x20;



#### Starting the node

Once the node is initialized, you can start the node with the following command:

```d
./accumulate run -n 0
```
