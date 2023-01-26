## Fallback

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Fallback {

  mapping(address => uint) public contributions;
  address public owner;

  constructor() {
    owner = msg.sender;
    contributions[msg.sender] = 1000 * (1 ether);
  }

  modifier onlyOwner {
        require(
            msg.sender == owner,
            "caller is not the owner"
        );
        _;
    }

  function contribute() public payable {
    require(msg.value < 0.001 ether);
    contributions[msg.sender] += msg.value;
    if(contributions[msg.sender] > contributions[owner]) {
      owner = msg.sender;
    }
  }

  function getContribution() public view returns (uint) {
    return contributions[msg.sender];
  }

  function withdraw() public onlyOwner {
    payable(owner).transfer(address(this).balance);
  }

  receive() external payable {
    require(msg.value > 0 && contributions[msg.sender] > 0);
    owner = msg.sender;
  }
}
```

The Fallback challenge introduces you into fallback functions .
### What is a fallback function?

Fallback function is a special function available to a contract. It has following features −

It is called when a non-existent function is called on the contract.

It is required to be marked external.

It has no name.

It has no arguments

It can not return anything.

It can be defined per contract.


It also introduces you to web3js and etherjs a way of communicating with the contract ABI.

### Steps in cracking the challenge

1. Try reading the contract code and understand what the contract is doing.
2. Use the help() method to see the methods that are available.
3. First Send your contributions to the contract should be less than 0.001, using contract.contribute({value: 4}) 4 here means 4 wei
4. Second Ether directly into the contract using, contract.sendTransaction({value:4}).
5. Third Withdraw the funds from the contract using contract.withdraw().

### Vulnerabilities 
The fallback function is vulnerable because its allows anyone you also made contributions to be became the owner when called again.
The Contribute function also allows anyone whose contribution is greater than the present owner to became owner 
So, who ever is the owner can withdraw ALL the funds from the contract

