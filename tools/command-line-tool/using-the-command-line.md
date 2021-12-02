# Getting Started

The Command-Line Interface Tool allows for the following operations: token, identity, and key management. By default, the Command-Line Interface connects to a localhost Accumulate Node, but you can specify any remote server by using the flag `-s`.

## How to build the CLI tool

The first step is building the CLI executable.

```bash
$ git clone https://github.com/AccumulateNetwork/accumulate.git
$ go build ./cmd/cli
```

Once you run these commands, a `cli` binary file should appear in the root directory `accumulate`.

## How to start the CLI tool

To test that the CLI built correctly, and to bring up a usage guide and list of available commands, run the `cli` command without any arguments.

#### On Windows

```bash
$ ./cli.exe
```

#### On Mac / Linux

```bash
$ ./cli
```

{% hint style="info" %}
_Note_: you must prefix every operation with the `cli` command (either `./cli` or `./cli.exe` depending on your operating system).
{% endhint %}
