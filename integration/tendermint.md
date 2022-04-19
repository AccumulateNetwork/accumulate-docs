# Tendermint

Accumulate uses the Tendermint API and config files to set up networks. The Tendermint consensus will be run for the Block Validator Network (BVN) and Directory Network (DN) in the Accumulate network so that adding BVNs adds capacity linearly with 1,000 to 10,000 transactions per second per BVN.

Tendermint Core is Byzantine Fault Tolerant (BFT) middleware that takes a state transition machine - written in any programming language - and securely replicates it on many machines. Tendermint Core is written in the Golang programming language.

For more information on Tendermint, visit their [docs](https://docs.tendermint.com).
