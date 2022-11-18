# Import a Factom wallet

See [cli-setup.md](cli-setup.md "mention") for instructions on downloading the CLI binaries or building from source

## Import private keys

If you have not yet, initialize your wallet's mnemonic with `accumulate wallet init create`. This can be done at any time.

Run `accumulate key import factoid` and paste your private key into the prompt. Do this for each key.

## Import a mnemonic

Run `accumulate wallet init import mnemonic` and paste your mnemonic into the prompt. Enter and reender a password when prompted. This password encrypts your new wallet.

Run `accumulate key generate --sigtype rcd1 <nickname>` to regenerate a Factom key. `<nickname>` is an arbitrary nickname the CLI uses as a shorthand for the key. Run this command once for each key you generated from this mnemonic in your Factom wallet. If your Factom wallet had 5 keys generated with this mnemonic, run this command 5 times (with different nicknames).
