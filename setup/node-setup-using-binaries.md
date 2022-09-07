# Running an Accumulate Node directly from the binary

For some types of deployment it may be preferable to run an Accumulate Node directly from the binary, rather than using Accman or Docker.
This guide will detail the specific steps necessary to successfully run an Accumulate Node in this way but it is not intended as a general guide on Linux system administration. 

**Prerequisites**&#x20;

* Experience using the command line.&#x20;
* Basic knowledge about Accumulate.&#x20;
* Creation of an `accumulate` user account (it is NOT recommended to run as `root`!).&#x20;
* Knowledge of how to manage the specific firewall implemenation running on your machine.&#x20;
* A copy of the `accumulated` binary, preferably built from source.&#x20;

N.B. If you are intending to run a production mainnet validator it is not advisable to install compilers and build the binary on the same system. 
Please see here ***[TO_DO] Document detailing how to build from source***



Follow the steps below to set up an Accumulate Node on your machine:&#x20;

&#x20;**Install the accumulated binary**&#x20;

Copy the `accumulated` binary to your machine. `/usr/local/bin` is a sensible place to store this file.

&#x20;**Ensure the correct firewall ports are open to the world**&#x20;

Please see here for the list of ports an Accumulate Node uses and ensure your firewall is configured for the appropriate ones to be publicly accessible. 
***[TO DO] Reference document listing all ports, their protocol and whether they are to be publicly or privately accessible***
Please note, it is your responsibility to ensure that your firewall is configured proprely to adequately secure your server.

&#x20;**Create a working directory for the configuration files**&#x20;
the
You should switch to the `accumulate` user account and create a directory to contain the required configuration files. Here we opt to create a directory called `node` in the `accumulate` user's home directory:

```
su - accumulate
```
```
mkdir node 
```

&#x20;**Identify a BVN to run and initialize configuration files**&#x20;

The next step is identify which BVN you wish this machine to run and the corresponding seed url.
For testnet we have either:
```
tcp://bvn0-seed.testnet.accumulatenetwork.io:16691
tcp://bvn1-seed.testnet.accumulatenetwork.io:16691
```
***[TO DO] Create a reference file that lists all the different networks, the minimum viable and recommended software versions for each type of node (eg. RPC, validator), along with a list of their seed nodes.***

Once we have chosen our BVN we need to initialize it with the following command:
```
accumulated init dual <bvn_seed_url> -w <working_directory> --public <public_ip_address>
```
e.g.
```
accumulated init dual tcp://bvn0-seed.testnet.accumulatenetwork.io:16691 -w /home/accumulate/node --public x.x.x.x
```

If successful this will contact the sever behind the seed url and pull down all the necessary config files. You should find that your working directory has been populated with `bvnn` and `dnn` subdirectories containing these files.

&#x20;**Run the node**&#x20;

The node can then be started by the `accumulate` user with the following command:
```
accumulated run-dual <working_directory>/dnn <working_directory>/bvnn -w <working_directory>
```
e.g.
```
accumulated run-dual /home/accumulate/node/dnn /home/accumulate/node/bvnn -w /home/accumulate/node
```

However, if you are running a validator node it is advisable to use a proper process manager to ensure it remains online and will automatically restart on failure. Systemd is an excellent choice and an example unit file is:
```
[Unit]
Description=Accumulate Validator Node
After=network-online.target

[Service]
User=accumulate
Group=accumulate
Restart=always
WorkingDirectory=/home/accumulate/node
ExecStart=/usr/local/bin/accumulated run-dual /home/accumulate/node/dnn /home/accumulate/node/bvnn -w /home/accumulate/node
LimitNOFILE=1048576


[Install]
WantedBy=multi-user.target
```
Switch to your usual user account with `sudo` privileges and place a file containing the above in `/etc/systemd/system/accumulate.service`.

You then need to run the following to start this service:
```
sudo systemctl daemon-reload
```
```
sudo systemctl start accumulate.service
```

Log output can be viewed via journalctl, e.g.:
```
sudo journalctl -f -u accumulate.service
```

Please note, on quiet networks, for example newly initalized testnets, the logs will not be particular chatty, producing output only for snapshots/major blocks and failed transactions.
To confirm a node is functioning correctly please see the recommended strategies in 
***[TO DO] Create a doc with details on assessing whether a node is healthy***
