---
description: >-
  This guide will run you through how to create a Validator Node to an
  Accumulate network.
---

# Validator Node Setup Guide

{% hint style="info" %}
This guide is for creating a Validator node on Accumulate, which participates in consensus. If you would like to set up a follower node instead, which only records transactions on the network, please see the [Follower Node Setup Guide](follower-node-setup-guide.md).
{% endhint %}

The first thing you must do is add your node's IP address to the `networks.go` file. Navigate to `accumulated/networks` then open up `networks.go` in your preferred code editor.

Within this file, you will see the available networks inside the `Networks` array. Each network is formatted as a `RouterNode` struct, which includes fields for the network's `Name` , the `Port` it listens on, and the `Ip`  addresses of all the nodes in this network.



#### Adding your node to an existing network

To add your node to an existing network, take a look at the networks that are available within the `Networks` array and choose which one you want to join. Within the `RouterNode` struct for your chosen network, create a new line in the `Ip` array, and add the public IP address of your node.

For example, let's say you wanted to join the `Arches` network:

```go
Networks = []RouterNode{
		RouterNode{
			Name: "Arches",
			Port: 33000,
		  //add your IP address to this array:
			Ip: []string{
				"127.0.0.1",
				"192.168.0.1",
				"<YOUR IP HERE>",
			},
		},
	}
```

####

#### Creating a new network

If you wanted to create a new network instead of joining an existing one, all you have to do is add the Network details as a `RouterNode` struct within the `Networks` array.

For example, let's say you wanted to create your own network between yourself and your friend called `TheBestiesNetwork` and open up port `8888`:

```d
Networks = []RouterNode{
		RouterNode{
			Name: "Arches",
			Port: 33000,
			Ip: []string{
				"127.0.0.1",
				"192.168.0.1",
				"<YOUR IP HERE>",
			},
		},
		//Add the following lines for your new network:
		RouterNode{
			Name: "TheBestiesNetwork",
			Port: 8888,
			Ip: []string{
				"<YOUR IP HERE>",
				"<YOUR FRIEND'S IP HERE",
			},
		},
	}
```

####

#### Initializing the node

Once you've modified `networks.go` and added your node's IP address, you then need to compile the code by running:

```d
$ go build ./cmd/accumulated
```

Once compiled, run the following command to initialize the network:

```d
./accumulated init -n "<NETWORK NAME>"
```

This will generate the `~/.accumulate` directory with configs. &#x20;

**Note: **Currently in order for the other nodes on this network to recognize your node, the contents of the `~/accumulate` folder must be copied over to the other nodes as well so they all have the same config.

Inside this directory you should find a directory for each node you included in the network, with the name following the convention of "Node" + the index for that node's IP address as it was entered in the `Ip` array in the RouterNode struct (e.g. `Node0`, `Node1`, etc).



#### Starting the node

Once the node is initialized, you can start the node with the following command:

```d
./accumulated run -n [node_number]
```

*   Where `[node_number]` is the index for the position of the node's entry in the `Ip` array in the network's RouterNode struct in `networks.go`.

    * Alternatively you can look for the `persistent peers` line in the node config file that shows all the addresses being used.



### Final step to joining the Testnet as a validator node

If you are interested in joining the Testnet as a participating member, please submit a Pull Request to the [Accumulate Repository](https://github.com/AccumulateNetwork/accumulated) with your updated `networks.go` file.&#x20;
