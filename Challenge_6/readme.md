## Token

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

contract Token {

  mapping(address => uint) balances;
  uint public totalSupply;

  constructor(uint _initialSupply) public {
    balances[msg.sender] = totalSupply = _initialSupply;
  }

  function transfer(address _to, uint _value) public returns (bool) {
    require(balances[msg.sender] - _value >= 0);
    balances[msg.sender] -= _value;
    balances[_to] += _value;
    return true;
  }

  function balanceOf(address _owner) public view returns (uint balance) {
    return balances[_owner];
  }
}
```
This challenge requires an understanding of overflow and underflow. How do you define overflow and understand underflow?
Whenever uint (unsigned integer) reaches its byte limit, it overflows.
Underflow occurs when uint (unsigned integer) does not reach the minimum byte size



```solidity
  function transfer(address _to, uint _value) public returns (bool) {
    require(balances[msg.sender] - _value >= 0);
    balances[msg.sender] -= _value;
    balances[_to] += _value;
    return true;
  }
```

As a result of the transfer function, this challenge will be able to be crammed by overflow and overflow.

await contract.transfer('0x552cc9c97D7D107BF362eF8d50739bc5Ac4a11B5', '21')

When 21 tokens are transferred out, but the tokens in your wallet are 20, you will experience an underflow and your wallet will contain the maximum number of tokens that Unit256 can hold.