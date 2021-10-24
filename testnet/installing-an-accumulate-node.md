# Installing an Accumulate Node

## Prerequisites

In order for Accumulate to run properly on your machine, you will need:

* Linux or Mac OS X operating system
* A **CPU** with at least **\_\_\_** cores
* **\_\_**GB of RAM
* **\_\_**GB of free disk space

## Installing with Docker

In order to install Accumulate using Docker, you need to have the following software installed and set up on your machine:

* Docker
* `bash`

## Installing from source

This guide will show you how to compile and install `accumulated` into your environment of choice directly from the source-code.

{% hint style="info" %}
**Note**: If you want to avoid compiling the binaries yourself, you can download and install the latest release binary of Accumulate from \_\_\_\_\_\_\_\_\_.
{% endhint %}

### Prerequisites for installing from source

In order to install `accumulated` from source, the following dependencies are required:

* **Go:** `accumulated` is written in the Golang programming language.

{% hint style="info" %}
**Note**: The minimum version of Go supported is Go 1.15. We recommend that users use the latest version of Go, which at the time of writing is 1.17
{% endhint %}

If you're not sure if your environment has Go, use this command to verify if you have Go installed and what version:

```d
$ go version
go version go1.17.x darwin/amd64
```

####

#### Installing Go on Mac OS X

Homebrew is the quickest and easiest way to install Go on Mac OS X. If you do not have Homebrew, install it by running this command:

```d
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

To install Go with Homebrew, run the following command:

```d
$ brew install go
```





#### Installing Go on Linux

First we need to find the link for the Go Linux binary by going to https://golang.org and then clicking on **Download Go**.

Copy the link for the Linux download (it will look something like `https://golang.org/dl/go1.17.2.linux-amd64.tar.gz`), and then run the `wget` command with the copied link to download.

```d
$ wget https://golang.org/dl/go1.17.2.linux-amd64.tar.gz
```

Next extract the tarball using the `tar` command to a directory of your choice.

```d
$ sudo tar -C /chosen/directory/ -xzf go1.17.2.linux-amd64.tar.gz
```

Next you must set the PATH for Go. To do so, open the .profile file in your home directory.

```d
$ sudo nano $HOME/.profile
```

Then append the following line to that file and save it:

```c
export PATH=$PATH:/usr/local/go/bin
```

Save the profile file and then run the following command apply the change:

```d
$ source .profile
```





### Installing accumulated from source

With the prerequisite steps completed, to install `accumulated` and all related dependencies run the following commands:

```d
$ git clone https://github.com/AccumulateNetwork/accumulated.git --branch develop
$ cd accumulated
$ go build ./cmd/accumulated
```

The command above will install the current _develop_ branch of `accumulated` and the necessary dependencies.

\
