# Getting Started

The Command-Line Interface Tool allows for the following operations: token, identity, and key management. By default, the Command-Line Interface connects to a localhost Accumulate Node, but you can specify any remote server by using the flag `-s`.

## How to build the CLI tool

The first step is building the CLI executable. You will need to have the Go compiler installed on your machine before you can build the CLI. You can find the Go compiler [here](https://go.dev/dl/).

```bash
$ git clone https://github.com/AccumulateNetwork/accumulate.git
$ go build ./cmd/accumulate
```

Once you run these commands, an `accumulate` binary file should appear in the root directory `accumulate`.

## How to start the CLI tool

To test that the CLI built correctly, and to bring up a usage guide and list of available commands, run the `cli` command without any arguments.

#### On Windows

```bash
$ ./accumulate.exe
```

#### On Mac / Linux

```bash
$ ./accumulate
```

{% hint style="info" %}
_Note_: every operation must be prefixed with the `accumulate` command (either `./accumulate` or `./accumulate.exe` depending on your operating system).
{% endhint %}
