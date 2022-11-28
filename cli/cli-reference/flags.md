# Flags

Flags modify the operation of a command and are sometimes called options. A flag is set off by spaces or tabs and usually starts with a dash (-).

When a command uses flags, they come directly after the command name. Single-character flags in a command can be combined with one dash.

**Flags:**

```
--authority strings        Additional authorities to add when creating an account 
--database string          Directory the database is stored in (default 
-d,--debug                 Print accumulated API calls 
--delegator strings        Specifies the delegator when creating a delegated signature 
--entropy uint             Specifies the size of the mnemonic entropy. (default 128) 
-h,--help                  help for accumulate 
--ignore-pending           Ignore pending transactions. Combined with --wait, this waits for transactions to be delivered. 
-j,--json                  print outputs as json 
-m,--memo string           Memo
-a,--metadata string       Transaction Metadata 
--no-wait                  Don't wait for the transaction to complete 
--no-wallet-version-check  Bypass the check to prevent updating the wallet to the format supported by the cli 
-n,--pretend               Enables check-only mode for transactions 
--prove                    Request a receipt proving the transaction or account 
-s,--server string         Accumulated server (default "https://testnet.accumulatenetwork.io/v2") 
--sign-with strings        Specifies additional keys to sign the transaction with 
--signer-version uint      Specify the signer version. Overrides the default behavior of fetching the signer version. 
-t,--timeout duration      Timeout for all API requests (i.e. 10s, 1m) (default 5s) 
--use-unencrypted-wallet   Use unencrypted wallet (strongly discouraged) stored at ~/.accumulate/wallet.db 
-w,--wait duration         Wait for the transaction to complete
```
