# Debugging node issues

### The node is not responding to API requests

1. Run `netstat -alpn | grep <port>` to check if Accumulate is or is not listening on the relevant port. A response like `tcp6 0 0 :::16695 :::* LISTEN 20355/accumulated` indicates that Accumulate **is** listening.
   * If Accumulate is listening, something is blocking or interfering with connections to the node. If you can connect to any port (including SSH or HTTPS), the issue is likely an incorrect firewall configuration.
   * Otherwise (if Accumulate is not listening),
2. Check if Tendermint is still catching up. Open `http://<your-node>:<tendermint-rpc>/status` in your browser, or make the equivalent RPC call.
   * If you get no response, use `netstat` to check if its listening. If it is listening, see above.
   * If it is not listening, wait for a minute to ensure the node has booted. If there's still no response, ask for help.
   * If you get a response and `catching_up` is `true`, wait for it to finish catching up.
   * If you get a response and `catching_up` is `false`, ask for help.

### Prometheus is not responding to requests

When running a DNN and BVNN in dual-mode, the BVNN's Prometheus exporer is disabled. Because of how Tendermint initializes Prometheus ([see here](https://github.com/tendermint/tendermint/issues/7076)), the Prometheus exporter cannot be enabled for both nodes. If neither the DNN's nor the BVNN's exporter are responding to requests, see [#the-node-is-not-responding-to-api-requests](debugging-node-issues.md#the-node-is-not-responding-to-api-requests "mention").

### Port numbers

The base port for the testnet and mainnet is 16591. All of the node ports have a fixed offset from the base port.

<table><thead><tr><th width="249">Service</th><th>DNN</th><th>BVNN</th></tr></thead><tbody><tr><td>Tendermint P2P</td><td>0</td><td>100</td></tr><tr><td>Tendermint RPC</td><td>1</td><td>101</td></tr><tr><td>Prometheus</td><td>3</td><td>103</td></tr><tr><td>Accumulate API</td><td>4</td><td>104</td></tr></tbody></table>
