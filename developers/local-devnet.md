# Local DevNet

This guide assumes you have successfully [compiled](contributing.md#compiling) `github.com/AccumulateNetwork/accumulate/cmd/accumulated` and installed the binary to your path. If the binary is not installed to your path, replace `accumulate ...` with `./accumulate ...`, assuming the binary is in the current directory.

### Configure

* [ ] Choose the directory to store configuration and state in, such as `.nodes`
* [ ] Choose the base IP address for the first node, such as `127.0.25.1`
* [ ] Choose the number of validators and followers to create
* [ ] Execute `accumulate init local-devnet [flags]`

{% hint style="danger" %}
On macOS, you need to create loopback aliases before you will be able to listen on `127.x.y.z` (except `127.0.0.1`). To create an alias for `127.0.25.1`, execute `sudo ifconfig lo0 alias 127.0.`25`.1.`
{% endhint %}

```shell-session
$ accumulate init local-devnet --work-dir .nodes --ip 127.0.25.1 --followers 1 --validators 3
```

This will create configuration for four nodes, three validators and one follower, in `.nodes`, with IP addresses `127.0.25.1`, `127.0.25.2`, `127.0.25.3`, and `127.0.25.4`.

### Run

To run node 0 from directory `.nodes`, execute:

```shell-session
$ accumulate run -w .nodes -n 0
```

{% hint style="warning" %}
All validator nodes must be run together. For the example above, nodes 0, 1, and 2 must be run. Nodes will hang until all validators respond.
{% endhint %}
