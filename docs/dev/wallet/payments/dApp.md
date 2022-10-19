---
tags:
  - JavaScript
  - dApp Development
---

# dApp Connector

The Yoroi's dapp connector [example code](https://github.com/Emurgo/yoroi-frontend/tree/develop/packages/yoroi-ergo-connector/example-ergo) is the best staring point for now, Nautilus and SAFEW implements the same API as Yoroi ([EIP-12](https://github.com/ergoplatform/eips/pull/23/files#diff-cb3f835ea389f22c2f074a6acd820d178e44c82df8898e8ff36aea7f762b6710))


Specifically with Nautilus, to avoid conflicts, you can call `ergoConnector.nautilus.connect()` in place of `window.ergo_request_read_access()` and `ergoConnector.nautilus.isConnected()` in place of `window.ergo_check_read_access()`


## ergo-dapp-connector

- [NightOwl dApp Connector](https://github.com/nightowlcasino/dApp-connector-react-package) React package and [video tutorial](https://twitter.com/NightOwlCasino/status/1529452399475179520)
- [Message signing and user authentication with Nautilus wallet and sigma-rust](https://www.dappstep.com/docs/tutorial-dapp-connector/message-signing-authentication)
