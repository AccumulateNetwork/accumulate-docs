---
description: >-
  This guide will run you through how to create a Validator Node to an
  Accumulate network.
---

# Validator Node Setup

{% hint style="info" %}
This guide is for creating a Validator node on Accumulate, which participates in consensus. If you would like to set up a follower node instead, which only records transactions on the network, please see the [Broken link](broken-reference "mention").
{% endhint %}

{% hint style="warning" %}
Accumulate is not currently set up in a way that allows operators outside of the core team to join the network as validators. This guide is not useful without access to DeFi Dev's cloud infrastructure.
{% endhint %}

## BVN

{% hint style="info" %}
`<network>` must be the name of BVN network and `<all networks>` must be a comma-separated list of all BVN networks. See [Broken link](broken-reference "mention") for a list of BVN network names.
{% endhint %}

1. Execute the following command to configure a BVN network: `accumulate init --work-dir .nodes --network "<network>" --relay-to "<all networks>"`
2. Copy `.nodes` to each server
3. On each server, execute `accumulate run --work-dir .nodes -n <node number>`. `<node number>` must be the index of the node's IP address in the network's `Nodes` array (in `networks.go`).
