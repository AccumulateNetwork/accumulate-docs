# Ledger Integration

This guide will help you connect your Ledger device to your Accumulate wallet (ACME) account. The Accumulate wallet enables you to send and receive ACME.

**Prerequisite**

* You need to have Docker installed on your system.
* You need to have Git installed.
* It works on a Linux Ubuntu OS only.
* The Accumulate CLI supports the following hardware device: Ledger Nano S plus and Ledger Nano X.

### Install the Accumulate Ledger (ACME) app on your Ledger device

**Step 1**&#x20;

Clone Ledger repo from GitHub

```
git clone https://github.com/LedgerHQ/ledger-app-builder.git
```

**Step 2**

Locate the builder folder.

```
cd ledger-app-builder
```

**Step 3**

Run the ledger builder.

```
sudo Docker build -t ledger-app-builder:latest .
```

**Step 4**

Compile the app.

```
sudo docker run --rm -ti -v "$(realpath .):/app" ledger-app-builder:latest
```

**Step 5**

Then exit the shell

```
exit
```

**Step 6**

Clone Accumulate repo from Gitlab in the ledger builder repo

```
git clone https://gitlab.com/accumulatenetwork/ledger/app-accumulate.git
```

**Step 7**

Locate the accumulate folder.

```
cd app-accumulate
```

**Step 8**

Run the below command to open the docker shell.

```
./docker-loader.sh
```

**Step 9**

Run the following command in the `app` folder.

{% hint style="info" %}
**Note:** You will need to connect the Nano s-plus to your laptop and ensure it's unlocked.
{% endhint %}

```
make
```

**Step 10**

Add the following to `ENV` by typing the following command.

```
BOLOS_SDK=/opt/nanosplus-secure-sdk make load
```

If it doesn't work, run `make clean` then rerun the **step 10** command.

**Step 11**

At this stage, your Ledger Nano will show you **Deny unsafe manager** and an arrow **>** to see other options like **Public key** and **Allow safe manager.**

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-07 at 11.00.18.png" alt=""><figcaption><p><strong>Deny unsafe manager</strong></p></figcaption></figure>

Press the right button to navigate to **Allow safe manager.** Then press both buttons to accept.

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-07 at 10.24.55.png" alt=""><figcaption><p><strong>Allow unsafe manager</strong></p></figcaption></figure>

**Step 12**

Install **app Accumulate** by pressing the right button until you see **Perform installation**

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-07 at 10.27.19.png" alt=""><figcaption><p>Install app accumulate</p></figcaption></figure>

Then, press both buttons to perform the installation.

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-07 at 10.27.03.png" alt=""><figcaption><p><strong>Perform installation</strong></p></figcaption></figure>

{% hint style="info" %}
Your Ledger device will prompt you to enter your pin again.
{% endhint %}

If the installation is complete, you will see the screen below.

<figure><img src="../../.gitbook/assets/Screenshot 2022-10-07 at 10.26.40.png" alt=""><figcaption></figcaption></figure>

You have successfully installed Accumulate on your Ledger device via CLI.
