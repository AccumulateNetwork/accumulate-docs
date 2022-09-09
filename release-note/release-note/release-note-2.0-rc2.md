# Release Note 2.0 RC2

**Accumulate Release Candidate1 (RC1) Release Notes – 09/06/22**&#x20;

**🚀  New**  &#x20;

* Add height to /status&#x20;
* Integrate factom snapshot with accumulate genesis tool&#x20;
* Allow new Factom data entries&#x20;
* Variable fee schedule update&#x20;
* Limit delegation depth&#x20;
* Validate validator set at Genesis&#x20;
* Validate anchor and synthetic transaction keys against dn.acme/network instead of dn.acme/operators&#x20;
* Route when query-tx with txid&#x20;
* Send synthetic transactions as an RPC batch&#x20;

🔧 **Fixes** &#x20;

* ParseLiteAddress panics on small hex values&#x20;
* getVersion is exiting with check errors when it should be returning error&#x20;
* Do not allow adding a page as an authority&#x20;
* Various performance improvements&#x20;
* Correct configuration issue with routing transactions to DN&#x20;
* Limit URL length&#x20;
* Update Tendermint to 0.35.9&#x20;
* Pending synthetic transactions cause performance to suffer badly&#x20;
* Delegation allows replay&#x20;
* StateManager.AddAuthority checks the wrong URL&#x20;
* Able to Remove Delegate Entry (Only Entry) on Highest Priority Key Page &#x20;
* Able to add Duplicate Keys When Creating a New Key Page&#x20;
* UpdateKey doesn’t work with a delegated signature&#x20;

**✨** **Improvements**  &#x20;

* Add more logging to the sequence healing code&#x20;
* Eliminate remote transactions&#x20;
* Accumulated logs are a little too silent at startup&#x20;
* Decouple API v2 from ABCI&#x20;
* Query-tx API should accept the fully qualified tx ID (URL)&#x20;
* Replace block index with an account&#x20;
* Export the client&#x20;
* Move URL package to not internal&#x20;
* Remove deprecated terms&#x20;
