# Ledger CLI Reference

**Key list**

To show the list of keys, use the below command.

```
./accumulate key list
```

The above command will return an output similar to the following:

```
Public Key                                                              Key name
7abd943bacf33397d2c63a92e6bbb6f5bcaf46469dfec5e2020b535be2abe227        a7ea6fb829b21262e7b1256823e71452a685fc6d14764c5b
44915cdf9c299c8dbaef2e44e371be4b862f984258666a26db88f4b3fde62ff7        e9a8fb30ab448a5c3fb9b67ec8c1d155b04db3eb144568bd
e9b288de4f55dc3c2e3403589c6aca9781af89d77ea584cc6a349797d5b3be73        key
ae335c01ce48de127eac73d4837752b0b6d14c96c24326943b8b83282084e241        key1234
6eb9dfa41b3400d4ea226a52a0c93484ae61e3cd02ccee27c5373a8d2049d732        wise
```

**Account list**

```
accumulate account list
```

The above command will return an output similar to the following:

```
        key name        :       wise
        lite account    :       acc://1336bbe9ab0de46cbf2cbe539697ed0f654a0fddfefe8455/ACME
        public key      :       6eb9dfa41b3400d4ea226a52a0c93484ae61e3cd02ccee27c5373a8d2049d732
        key type        :       ed25519
        derivation      :       m/44'/281'/0'/0'/0'

        key name        :       wise4
        lite account    :       acc://505f114bdc1285ce98adb374725824cfd2bbdef7dddf9104/ACME
        public key      :       44bb5f8f4412c66b3dbd1541a417d87a65a5c414f278eef1172f82b2ffb3153e
        key type        :       ed25519
        derivation      :       m/44'/281'/0'/0'/1'
```

The wallet ID (shown in Accumulate ledger info) should remain the same. You can create new keys, it should create new lite accounts and the derivation path should count up like

```
  m/44'/281'/0'/0'/0'
  m/44'/281'/0'/0'/1'
  m/44'/281'/0'/0'/2'
```

Only when you delete your local wallet database it starts counting at 0 again
