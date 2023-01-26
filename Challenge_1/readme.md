## Hello Ehernaut

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Instance {

  string public password;
  uint8 public infoNum = 42;
  string public theMethodName = 'The method name is method7123949.';
  bool private cleared = false;

  // constructor
  constructor(string memory _password) {
    password = _password;
  }

  function info() public pure returns (string memory) {
    return 'You will find what you need in info1().';
  }

  function info1() public pure returns (string memory) {
    return 'Try info2(), but with "hello" as a parameter.';
  }

  function info2(string memory param) public pure returns (string memory) {
    if(keccak256(abi.encodePacked(param)) == keccak256(abi.encodePacked('hello'))) {
      return 'The property infoNum holds the number of the next info method to call.';
    }
    return 'Wrong parameter.';
  }

  function info42() public pure returns (string memory) {
    return 'theMethodName is the name of the next method.';
  }

  function method7123949() public pure returns (string memory) {
    return 'If you know the password, submit it to authenticate().';
  }

  function authenticate(string memory passkey) public {
    if(keccak256(abi.encodePacked(passkey)) == keccak256(abi.encodePacked(password))) {
      cleared = true;
    }
  }

  function getCleared() public view returns (bool) {
    return cleared;
  }
}
```

The Ethernaut challenge "hello" is a beginner-level exercise in smart contract security. 
To crake this level first you call the await contract.info(); and it gives the instructions on how to go through the level

#### Vulnerabilities in the Contract
```solidity
pragma solidity ^0.8.0;
```
Is a floating version of solidity and its not adviceable to use it ^. Its better you use a specific version of solidity to compile your code to avoid errors.
```solidity
pragma solidity 0.8.0;
```
Is better.
```solidity
string public password;
```
password is a public variable and its meant to be secured, if the password was stored in a public variable the contract will not be prone to attack. 
Always store important Data offchain or in a public variable.