## Vault

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Vault {
  bool public locked;
  bytes32 private password;

  constructor(bytes32 _password) {
    locked = true;
    password = _password;
  }

  function unlock(bytes32 _password) public {
    if (password == _password) {
      locked = false;
    }
  }
}
```

To unlock this vault we will read what is stored at the slot number 2

await web3.eth.getStorageAt("0xB178F1E1f76AE5D1D023f714f3F8a4B915173DB3", "1")