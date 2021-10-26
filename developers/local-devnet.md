# Local DevNet

This guide assumes you have successfully [compiled](contributing.md#compiling) `github.com/AccumulateNetwork/accumulated/cmd/accumulated` and installed the binary to your path. If the binary is not installed to your path, replace `accumulated ...` with `./accumulated ...`, assuming the binary is in the current directory.

### Configure

* [ ] Choose the directory to store configuration and state in, such as `.nodes`
* [ ] Choose the base IP address for the first node, such as `127.0.25.1`
* [ ] Choose the number of validators and followers to create
* [ ] Execute `accumulated init local-devnet [flags]`

{% hint style="warning" %}
Currently, the correct command is `accumulated testnet`. [This issue](https://github.com/AccumulateNetwork/accumulated/issues/162) on GitHub tracks the change.
{% endhint %}

```shell-session
$ accumulated init local-devnet --work-dir .nodes --ip 127.0.25.1 --followers 1 --validators 3
```

This will create configuration for four nodes, three validators and one follower, in `.nodes`, with IP addresses `127.0.25.1`, `127.0.25.2`, `127.0.25.3`, and `127.0.25.4`.

### Run

To run node 0 from directory `.nodes`, execute:

```shell-session
$ accumulated run -w .nodes -n 0
```

{% hint style="warning" %}
All validator nodes must be run together. For the example above, nodes 0, 1, and 2 must be run. Nodes will hang until all validators respond.
{% endhint %}
