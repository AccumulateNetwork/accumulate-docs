# Follower Node Setup Guide

#### Initializing the node

Run the following command to initialize the follower:

```d
./accumulated init follower --network "<NETWORK NAME>" --listen "tcp://0.0.0.0:26656"
```

This will generate the `~/.accumulate/Node0` directory with configs.  



#### Starting the node

Once the node is initialized, you can start the node with the following command:

```d
./accumulated run -n 0
```

