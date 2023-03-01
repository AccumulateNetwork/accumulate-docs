---
description: >-
  Follow this guide to convert your Factoids (FCT) and wrapped Factoids (wFCT)
  on Factom to ACME on Accumulate.
---

# Converting FCT to ACME

The FCT conversion to ACME is automatic. At the point of conversion, the Factoid address will be converted into Accumulate Lite Token Account addresses. You will import all the Factoid addresses into accumulate as RCD1 Accumulate Lite Token account addresses at genesis. The Factoid address will map automatically to these new RCD1 Accumulate Lite Token accounts.

The Factoid balances will be automatically converted into ACME and deposited into the RCD1 ACME Lite Token account.&#x20;

To access ACME, users will need to import their **Factom private keys** into the Accumulate CLI wallet. The wallet will understand this mapping, and the users will have access at that point to their new ACME. Within the Accumulate Explorer, Factoid Addresses will point to ACME Lite Token Account Addresses.

### **Export and Import Steps for CLI**

**Step 1:**&#x20;

Locate Factoid Address and Factoid Secret Key

**Factoid Secret (ED25519 Private Key):**

```
Fs1ipNRjEXcWj8RUn1GRLMJYVoPFBL1yw9rn6sCxWGcxciC4HdPd 
```

**Factoid Address (Public Key RCD1 Hash):**

```
FA2PdKfzGP5XwoSbeW1k9QunCHwC8DY6d8xgEdfm57qfR31nTueb
```

#### **Step 2:**&#x20;

Import Factoid Secret to Accumulate CLI, Mobile Wallet, or Web Wallet

**Syntax**

```
accumulate key import factoid [factoid private address] Import a Factoid Secret Address 
```

**Command**

```
./accumulate key import factoid Fs1ipNRjEXcWj8RUn1GRLMJYVoPFBL1yw9rn6sCxWGcxciC4HdPd 
```

The above command will return an output similar to the following:

```
        name            :       FA2PdKfzGP5XwoSbeW1k9QunCHwC8DY6d8xgEdfm57qfR31nTueb 
        lite account    :       acc://37bd0f217ea091bb295f7c7c124b19dacaa13bab8fdafaa0/ACME 
        public key      :       3c1ff1dc8f60ad24155549fcbc21a48ce0e24a85d7af2dba98c6f2c227421520 
        key type        :       rcd1 
```

**Step 3:**&#x20;

Lite Token Account will hold ACME balance converted from Prior Factoid Balance

**Syntax**

```
./accumulate get [Account url]
```

**Command**

```
./accumulate get acc://37bd0f217ea091bb295f7c7c124b19dacaa13bab8fdafaa0/ACME   
```

The above command will return an output similar to the following:

```
        Account Url     :       acc://37bd0f217ea091bb295f7c7c124b19dacaa13bab8fdafaa0/ACME 
        Token Url       :       acc://ACME 
        Balance         :       2000000.00000000 ACME 
        CreditBalance   :       0.00 
        Last Used On    :       1969-12-31 19:00:00 -0500 EST 
```

### User Expectation

* **If a user has FCT in a Hot Wallet or on an Exchange:** Export FS Address (Factom Secret Key) from Factom Wallet. Import FS Address it into Accumulate Wallet (Mobile, Web, CLI). Reference Export and Import Steps.
* **If a user has FCT in a Ledger:** No action on the user’s part when the Ledger supports ACME to convert FCT to ACME. The user will need to install the ACME Ledger application.
* **If a user has WFCT:** WFCT holders can convert their WFCT to ACME using this [https://wfct-burn.netlify.app](https://wfct-burn.netlify.app)

### Exchange Expectation

* **If an exchange has FCT:** If the exchange supports FCT to ACME conversion. Nothing needs to be done by the Exchange, and If the exchange does not support the FCT to ACME conversion, the Exchange needs to tell users to withdraw their funds from the Exchange.

**Assumption:** Exchange may hold some FCT in Cold and Hot Storage

* **Current Exchanges that support FCT:** Bittrex.com and Qtrade.io

### Data Accounts

**Factom Data Chain to Lite Data Account**\
To Convert a Factom Data Chain to a Lite Data account, add acc:// before the Data Chain ID.
