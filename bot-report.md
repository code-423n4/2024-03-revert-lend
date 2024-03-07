# Winning bot race submission
This is the top-ranked automated findings report, from Hound bot. All findings in this report will be considered known issues for the purposes of your C4 audit.

## Summary

| |Issue|Instances| Gas Savings
|-|:-|:-:|:-:|
| [[M-01](#m-01)] | Missing price checks for Chainlink oracle | 1| 0|
| [[M-02](#m-02)] | Missing L2 sequencer checks for Chainlink oracle | 1| 0|
| [[M-03](#m-03)] | Chainlink oracle will return the wrong price if the aggregator hits `minAnswer` | 1| 0|
| [[M-04](#m-04)] | Some `ERC20` can revert on a zero value `transfer` | 10| 0|
| [[L-01](#l-01)] | File allows a version of solidity that is susceptible to .selector-related optimizer bug | 4| 0|
| [[L-02](#l-02)] | Possible reentrancy with callback on transfer tokens | 4| 0|
| [[L-03](#l-03)] | Missing checks in constructor/initialize | 6| 0|
| [[L-04](#l-04)] | Missing checks for state variable assignments | 26| 0|
| [[L-05](#l-05)] | `payable` function does not transfer ETH | 2| 0|
| [[L-06](#l-06)] | Functions calling contracts with transfer hooks are missing reentrancy guards | 26| 0|
| [[L-07](#l-07)] | `decimals` is not part of the `ERC20` standard | 3| 0|
| [[L-08](#l-08)] | Large transfers may not work with some `ERC20` tokens | 17| 0|
| [[L-09](#l-09)] | Large approvals may not work with some `ERC20` tokens | 15| 0|
| [[L-10](#l-10)] | `approve` can revert if the current approval is not zero | 13| 0|
| [[L-11](#l-11)] | `safeApprove` is deprecated | 15| 0|
| [[L-12](#l-12)] | Unsafe downcast may overflow | 3| 0|
| [[L-13](#l-13)] | Unsafe `uint` to `int` conversion | 3| 0|
| [[L-14](#l-14)] | Use of `abi.encodeWithSignature`/`abi.encodeWithSelector` instead of `abi.encodeCall` | 2| 0|
| [[L-15](#l-15)] | Subtraction may underflow if multiplication is too large | 7| 0|
| [[L-16](#l-16)] | Possible division by 0 is not prevented | 5| 0|
| [[L-17](#l-17)] | Code does not follow the best practice of check-effects-interaction | 6| 0|
| [[L-18](#l-18)] | Missing limits when setting min/max amounts | 10| 0|
| [[L-19](#l-19)] | Owner can renounce ownership | 4| 0|
| [[L-20](#l-20)] | Missing contract-existence checks before low-level calls | 5| 0|
| [[L-21](#l-21)] | External calls in an unbounded loop can result in a DoS | 1| 0|
| [[L-22](#l-22)] | Solidity version `0.8.20` may not work on other chains due to `PUSH0` | 11| 0|
| [[L-23](#l-23)] | Lack of two-step update for updating protocol addresses | 8| 0|
| [[L-24](#l-24)] | Use of ownership with a single step rather than double | 4| 0|
| [[L-25](#l-25)] | Loss of precision on division | 66| 0|
| [[L-26](#l-26)] | Gas griefing/theft is possible on an unsafe external call | 3| 0|
| [[L-27](#l-27)] | Consider the case where `totalSupply` is zero | 9| 0|
| [[L-28](#l-28)] | Use `increaseAllowance/decreaseAllowance` instead of `approve/safeApprove` | 17| 0|
| [[L-29](#l-29)] | `onlyOwner` functions not accessible if `owner` renounces ownership | 14| 0|
| [[L-30](#l-30)] | Using a vulnerable dependency from some libraries | 21| 0|
| [[L-31](#l-31)] | Centralization issue caused by admin privileges | 15| 0|
| [[L-32](#l-32)] | Missing checks for `address(0)` in constructor/initializers | 12| 0|
| [[L-33](#l-33)] | Missing checks for `address(0)` when updating state variables | 16| 0|
| [[G-01](#g-01)] | Use `Array.unsafeAccess` to avoid repeated array length checks | 4| 8400|
| [[G-02](#g-02)] | State variables can be packed into fewer storage slots | 1| 20000|
| [[G-03](#g-03)] | Structs can be packed into fewer storage slots | 3| 80000|
| [[G-04](#g-04)] | Multiple `mapping`s that share an ID can be combined into a single `mapping` of ID / `struct` | 2| 40924|
| [[G-05](#g-05)] | Use of `memory` instead of `storage` for struct/array state variables | 3| 54600|
| [[G-06](#g-06)] | Cache state variables with stack variables | 9| 1900|
| [[G-07](#g-07)] | Avoid contract existence checks by using low level calls | 116| 11600|
| [[G-08](#g-08)] | Low level `call` can be optimized with assembly | 5| 1240|
| [[G-09](#g-09)] | Use at least Solidity version `0.8.19` to gain some gas boost | 11| 0|
| [[G-10](#g-10)] | Use of `memory` instead of `calldata` for immutable arguments | 8| 2096|
| [[G-11](#g-11)] | Avoid updating storage when the value hasn't changed | 16| 11200|
| [[G-12](#g-12)] | Use `uint256(1)/uint256(2)` instead of `true/false` to save gas for changes | 4| 68000|
| [[G-13](#g-13)] | Shortcircuit rules can be be used to optimize some gas usage | 2| 10500|
| [[G-14](#g-14)] | Cache multiple accesses of a mapping/array | 15| 966|
| [[G-15](#g-15)] | Using `private` for constants saves gas | 13| 109278|
| [[G-16](#g-16)] | require() or revert() statements that check input arguments should be at the top of the function | 1| 0|
| [[G-17](#g-17)] | Custom `error`s cost less than `require`/`assert` | 3| 87|
| [[G-18](#g-18)] | Consider activating `via-ir` for deploying | -| 0|
| [[G-19](#g-19)] | Functions that revert when called by normal users can be `payable` | 15| 315|
| [[G-20](#g-20)] | Add `unchecked` blocks for subtractions where the operands cannot underflow | 19| 1615|
| [[G-21](#g-21)] | Add `unchecked` blocks for divisions where the operands cannot overflow | 60| 9540|
| [[G-22](#g-22)] | Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead | 186| 1116|
| [[G-23](#g-23)] | `>=`/`<=` costs less gas than `>`/`<` | 127| 381|
| [[G-24](#g-24)] | `internal` functions only called once can be inlined to save gas | 18| 360|
| [[G-25](#g-25)] | Use multiple revert checks to save gas | 26| 52|
| [[G-26](#g-26)] | `abi.encode()` is less efficient than `abi.encodepacked()` for non-address arguments | 4| 20|
| [[G-27](#g-27)] | Unused named return variables without optimizer waste gas | 6| 15|
| [[G-28](#g-28)] | Consider pre-calculating the address of `address(this)` to save gas | 58| 0|
| [[G-29](#g-29)] | Consider using `solady`'s token contracts to save gas | 1| 0|
| [[G-30](#g-30)] | Consider using Solady's `FixedPointMathLib` | 55| 0|
| [[G-31](#g-31)] | Reduce deployment costs by tweaking contracts' metadata | 11| 0|
| [[G-32](#g-32)] | Emitting constants wastes gas | 3| 24|
| [[G-33](#g-33)] | Update OpenZeppelin dependency to save gas | 21| 0|
| [[G-34](#g-34)] | Function names can be optimized | 11| 242|
| [[G-35](#g-35)] | Using `delete` instead of setting mapping/struct to 0 saves gas | 5| 25|
| [[G-36](#g-36)] | Using `bool` for storage incurs overhead | 4| 400|
| [[G-37](#g-37)] | Multiplication/division by two should use bit shifting | 4| 80|
| [[G-38](#g-38)] | `x += y` is more expensive than `x = x + y` for state variables | 7| 140|
| [[G-39](#g-39)] | Use of `+=` is cheaper for mappings | 1| 40|
| [[G-40](#g-40)] | Mappings are cheaper to use than storage arrays | 1| 2100|
| [[G-41](#g-41)] | Use a more recent version of Solidity | 11| 0|
| [[G-42](#g-42)] | `SafeMath` usage with Solidity version >`0.8.0` | 1| 0|
| [[G-43](#g-43)] | Constructors can be marked `payable` | 11| 231|
| [[G-44](#g-44)] | Nesting `if` statements that use `&&` saves gas | 23| 690|
| [[G-45](#g-45)] | Counting down when iterating, saves gas | 2| 12|
| [[G-46](#g-46)] | `do-while` is cheaper than `for`-loops when the initial check can be skipped | 2| 0|
| [[G-47](#g-47)] | Lack of `unchecked` in loops | 2| 120|
| [[G-48](#g-48)] | `uint` comparison with zero can be cheaper | 56| 224|
| [[G-49](#g-49)] | Use assembly to check for `address(0)` | 14| 84|
| [[G-50](#g-50)] | Use scratch space for building calldata with assembly | 124| 27280|
| [[G-51](#g-51)] | Use assembly to validate `msg.sender` | 26| 312|
| [[G-52](#g-52)] | Use assembly to write `address` storage values | 13| 962|
| [[G-53](#g-53)] | Use assembly to emit an `event` | 49| 1862|
| [[N-01](#n-01)] | Fee-on-transfer/rebasing tokens will have problems when swapping | 1| 0|
| [[N-02](#n-02)] | `unchecked` blocks with subtractions may underflow | 10| 0|
| [[N-03](#n-03)] | Some functions do not work correctly with fee-on-transfer tokens | 6| 0|
| [[N-04](#n-04)] | Some functions do not work correctly with rebasing tokens | 4| 0|
| [[N-05](#n-05)] | Custom `error` should be used rather than `require`/`assert` | 3| 0|
| [[N-06](#n-06)] | High cyclomatic complexity | 12| 0|
| [[N-07](#n-07)] | Missing events in sensitive functions | 1| 0|
| [[N-08](#n-08)] | Missing events in initializers | 1| 0|
| [[N-09](#n-09)] | Consider emitting an event at the end of the constructor | 11| 0|
| [[N-10](#n-10)] | Setters should prevent re-setting the same value | 16| 0|
| [[N-11](#n-11)] | Using zero as a parameter | 32| 0|
| [[N-12](#n-12)] | Named imports of parent contracts are missing | 11| 0|
| [[N-13](#n-13)] | Unused named `return` | 5| 0|
| [[N-14](#n-14)] | OpenZeppelin libraries should be upgraded to a newer version | 21| 0|
| [[N-15](#n-15)] | Same `constant` is redefined elsewhere | 12| 0|
| [[N-16](#n-16)] | Enum values should be used in place of constant array indexes | 9| 0|
| [[N-17](#n-17)] | Variable initialization with zero value | 13| 0|
| [[N-18](#n-18)] | Consider adding emergency-stop functionality | 4| 0|
| [[N-19](#n-19)] | Duplicated `require/if` statements should be refactored | 5| 0|
| [[N-20](#n-20)] | Inconsistent usage of `require`/`error` | 2| 0|
| [[N-21](#n-21)] | Some functions contain the same exact logic | 4| 0|
| [[N-22](#n-22)] | Unbounded loop may run out of gas | 2| 0|
| [[N-23](#n-23)] | Public functions not called internally | 2| 0|
| [[N-24](#n-24)] | Large multiples of ten should use scientific notation | 3| 0|
| [[N-25](#n-25)] | Missing/malformed underscores for large numeric literals | 4| 0|
| [[N-26](#n-26)] | Avoid complex casting | 2| 0|
| [[N-27](#n-27)] | Consider using the `using-for` syntax | 167| 0|
| [[N-28](#n-28)] | Consider making contracts `Upgradeable` | 11| 0|
| [[N-29](#n-29)] | Missing timelock in critical functions | 1| 0|
| [[N-30](#n-30)] | Dependence on external protocols | 92| 0|
| [[N-31](#n-31)] | Use transfer libraries instead of low level calls | 3| 0|
| [[N-32](#n-32)] | `2**<n> - 1` should be re-written as `type(uint<n>).max` | 14| 0|
| [[N-33](#n-33)] | Use of non-named numeric constants | 11| 0|
| [[N-34](#n-34)] | Consider splitting complex checks into multiple steps | 32| 0|
| [[N-35](#n-35)] | Complex math should be split into multiple steps | 31| 0|
| [[N-36](#n-36)] | Time related variables should use time units instead of numbers | 2| 0|
| [[N-37](#n-37)] | Some functions don't have any logic | 5| 0|
| [[N-38](#n-38)] | Control structures do not comply with best practices | 9| 0|
| [[N-39](#n-39)] | Use a single file for system wide constants | 5| 0|
| [[N-40](#n-40)] | Event does not have proper `indexed` fields | 22| 0|
| [[N-41](#n-41)] | Old Solidity version | 11| 0|
| [[N-42](#n-42)] | Use of floating pragma | 11| 0|
| [[N-43](#n-43)] | Contract functions should use an `interface` | 37| 0|
| [[N-44](#n-44)] | `require`/`revert` without any message | 1| 0|
| [[N-45](#n-45)] | Some error strings are not descriptive | 1| 0|
| [[N-46](#n-46)] | `else` block is not required | 6| 0|
| [[N-47](#n-47)] | Multiple `address`/ID mappings can be combined into a single mapping of an `address`/ID to a `struct`, for readability | 2| 40924|
| [[N-48](#n-48)] | Lack of specific `import` identifier | 70| 0|
| [[N-49](#n-49)] | Imports should be organized more systematically | 9| 0|
| [[N-50](#n-50)] | Top-level declarations should be separated by at least two lines | 22| 0|
| [[N-51](#n-51)] | Use a struct to encapsulate multiple function parameters | 21| 0|
| [[N-52](#n-52)] | Returning a struct instead of returning many variables is better | 10| 0|
| [[N-53](#n-53)] | Event is missing `msg.sender` parameter | 41| 0|
| [[N-54](#n-54)] | Events should emit both new and old values | 19| 0|
| [[N-55](#n-55)] | Events may be emitted out of order due to reentrancy | 20| 0|
| [[N-56](#n-56)] | Use of polymorphism is discouraged for security audits | 3| 0|
| [[N-57](#n-57)] | Constants in comparisons should appear on the left side | 28| 0|
| [[N-58](#n-58)] | Consider using `delete` instead of assigning zero/false to clear values | 5| 0|
| [[N-59](#n-59)] | Use a ternary statement instead of `if`/`else` when appropriate | 3| 0|
| [[N-60](#n-60)] | Consider using named mappings | 16| 0|
| [[N-61](#n-61)] | Consider using named returns | 31| 0|
| [[N-62](#n-62)] | Layout order does not comply with best practices | 8| 0|
| [[N-63](#n-63)] | `mapping` definitions do not comply with best practices | 1| 0|
| [[N-64](#n-64)] | Function visibility order does not comply with best practices | 43| 0|
| [[N-65](#n-65)] | Long functions should be refactored into multiple functions | 12| 0|
| [[N-66](#n-66)] | Consider providing a ranged getter for array state variables | 1| 0|
| [[N-67](#n-67)] | Lines are too long | 36| 0|
| [[N-68](#n-68)] | Avoid the use of sensitive terms | 1| 0|
| [[N-69](#n-69)] | Consider adding a block/deny-list | 3| 0|
| [[N-70](#n-70)] | Use of `override` is unnecessary | 39| 0|
| [[N-71](#n-71)] | Missing variable names | 4| 0|
| [[N-72](#n-72)] | Typos in comments | 45| 0|
| [[N-73](#n-73)] | Contracts should have full test coverage | -| 0|
| [[N-74](#n-74)] | Large or complicated code bases should implement invariant tests | -| 0|
| [[N-75](#n-75)] | Codebase should implement formal verification testing | -| 0|
| [[N-76](#n-76)] | Inconsistent spacing in comments | 4| 0|
| [[N-77](#n-77)] | State variables should include comments | 27| 0|
| [[N-78](#n-78)] | Complex functions should have explicit comments | 5| 0|
| [[N-79](#n-79)] | Use `@inheritdoc` for overridden functions | 23| 0|
| [[N-80](#n-80)] | Variable names don't follow the Solidity naming convention | 7| 0|
| [[N-81](#n-81)] | `immutable` variable names should be uppercase | 18| 0|
| [[N-82](#n-82)] | Missing underscore prefix for non-external variables | 5| 0|
| [[N-83](#n-83)] | Invalid NatSpec comment style | 1| 0|
| [[N-84](#n-84)] | Missing NatSpec from contract declarations | 1| 0|
| [[N-85](#n-85)] | Missing NatSpec `@author` from contract declaration | 11| 0|
| [[N-86](#n-86)] | Missing NatSpec `@dev` from contract declaration | 11| 0|
| [[N-87](#n-87)] | Missing NatSpec `@notice` from contract declaration | 3| 0|
| [[N-88](#n-88)] | Missing NatSpec `@title` from contract declaration | 2| 0|
| [[N-89](#n-89)] | Missing NatSpec from event declaration | 39| 0|
| [[N-90](#n-90)] | Missing NatSpec `@dev` from event declaration | 39| 0|
| [[N-91](#n-91)] | Missing NatSpec `@notice` from event declaration | 39| 0|
| [[N-92](#n-92)] | Missing NatSpec `@param` from event declaration | 39| 0|
| [[N-93](#n-93)] | Missing NatSpec from function definitions | 65| 0|
| [[N-94](#n-94)] | Missing NatSpec `@dev` from function declaration | 114| 0|
| [[N-95](#n-95)] | Missing NatSpec `@notice` from function declaration | 66| 0|
| [[N-96](#n-96)] | Missing NatSpec `@param` from function declaration | 75| 0|
| [[N-97](#n-97)] | Incomplete NatSpec `@return` from function declaration | 46| 0|
| [[D-01](#d-01)] | Return values of `approve` not checked | 2| 0|
| [[D-02](#d-02)] | `approve` can revert if the current approval is not zero | 2| 0|
| [[D-03](#d-03)] | Some functions do not work correctly with fee-on-transfer tokens | 16| 0|
| [[D-04](#d-04)] | Enum values should be used in place of constant array indexes | 112| 0|
| [[D-05](#d-05)] | Time related variables should use time units instead of numbers | 15| 0|
| [[D-06](#d-06)] | Upgradeable contract is missing a constructor that disables initialization | 9| 0|
| [[D-07](#d-07)] | Upgradeable contract is missing a gap storage variable | 9| 0|
| [[D-08](#d-08)] | `selfbalance()` is cheaper than `address(this).balance` | 1| 97|
| [[D-09](#d-09)] | Some functions contain the same exact logic | 2| 0|
| [[D-10](#d-10)] | Modifier order does not comply with best practices | -| 0|
| [[D-11](#d-11)] | Visibility should be set explicitly rather than defaulting to internal | -| 0|

### Medium Risk Issues

### [M-01]<a name="m-01"></a> Missing price checks for Chainlink oracle

`latestRoundData` may return invalid data, and there aren't any checks to ensure that this doesn't happen.

This can be caused by any issues with Chainlink, such as oracle consensus problems or chain congestion, which may result in this contract relying on outdated data.

*There are 1 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit missing price check, which could be equal to 0
337: 		        (, int256 answer,, uint256 updatedAt,) = feedConfig.feed.latestRoundData();
```

*GitHub* : [337](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L337)

### [M-02]<a name="m-02"></a> Missing L2 sequencer checks for Chainlink oracle

Using Chainlink in L2 chains such as Arbitrum [requires](https://docs.chain.link/data-feeds/l2-sequencer-feeds) to check if the sequencer is down to avoid prices from looking like they are fresh although they are not.

The bug could be leveraged by malicious actors to take advantage of the sequencer downtime.

*There are 1 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit missing sequencer uptime, grace period checks
337: 		        (, int256 answer,, uint256 updatedAt,) = feedConfig.feed.latestRoundData();
```

*GitHub* : [337](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L337)

### [M-03]<a name="m-03"></a> Chainlink oracle will return the wrong price if the aggregator hits `minAnswer`

Chainlink aggregators have a built-in circuit breaker if the price of an asset goes outside of a predetermined price band.

The result is that if an asset experiences a huge drop in value (i.e. LUNA crash) the price of the oracle will continue to return the `minPrice` instead of the actual price of the asset.

This would allow users to continue borrowing with the asset but at the wrong price. This is exactly what happened to Venus on BSC when LUNA [crashed](https://rekt.news/venus-blizz-rekt/).

*There are 1 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit missing min/max price check
337: 		        (, int256 answer,, uint256 updatedAt,) = feedConfig.feed.latestRoundData();
```

*GitHub* : [337](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L337)

### [M-04]<a name="m-04"></a> Some `ERC20` can revert on a zero value `transfer`

Not all `ERC20` implementations are totally compliant, and some (e.g `LEND`) may fail while transfering a zero amount.

*There are 10 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

728: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), state.liquidatorCost);

946: 		        SafeERC20.safeTransfer(IERC20(asset), receiver, assets);
```

*GitHub* : [728](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L728), [946](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L946)

```solidity
File: src/automators/Automator.sol

226: 		            SafeERC20.safeTransfer(token, to, amount);
```

*GitHub* : [226](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L226)

```solidity
File: src/transformers/AutoCompound.sol

272: 		        SafeERC20.safeTransfer(IERC20(token), to, amount);
```

*GitHub* : [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L272)

```solidity
File: src/transformers/LeverageTransformer.sol

88: 		            SafeERC20.safeTransfer(IERC20(token0), params.recipient, amount0 - added0);

91: 		            SafeERC20.safeTransfer(IERC20(token1), params.recipient, amount1 - added1);
```

*GitHub* : [88](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L88), [91](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L91)

```solidity
File: src/transformers/V3Utils.sol

872: 		            SafeERC20.safeTransfer(token, to, amount);
```

*GitHub* : [872](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L872)

```solidity
File: src/utils/FlashloanLiquidator.sol

85: 		        SafeERC20.safeTransfer(data.asset, msg.sender, data.liquidationCost + (fee0 + fee1));
```

*GitHub* : [85](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L85)

```solidity
File: src/utils/Swapper.sol

98: 		                SafeERC20.safeTransfer(params.tokenIn, universalRouter, params.amountIn);

167: 		        SafeERC20.safeTransfer(IERC20(tokenIn), msg.sender, amountToPay);
```

*GitHub* : [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L98), [167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L167)

### Low Risk Issues

### [L-01]<a name="l-01"></a> File allows a version of solidity that is susceptible to .selector-related optimizer bug

In solidity versions prior to 0.8.21, there is a legacy code generation [bug](https://soliditylang.org/blog/2023/07/19/missing-side-effects-on-selector-access-bug/) where if `foo().selector` is called, `foo()` doesn't actually get evaluated. It is listed as low-severity, because projects usually use the contract name rather than a function call to look up the selector.

*There are 4 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

476: 		        return IERC721Receiver.onERC721Received.selector;
```

*GitHub* : [476](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L476)

```solidity
File: src/transformers/AutoCompound.sol

92: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoCompound.execute.selector, params)
```

*GitHub* : [92](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L92)

```solidity
File: src/transformers/AutoRange.sol

102: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoRange.execute.selector, params)
```

*GitHub* : [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L102)

```solidity
File: src/transformers/V3Utils.sol

378: 		        return IERC721Receiver.onERC721Received.selector;
```

*GitHub* : [378](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L378)

### [L-02]<a name="l-02"></a> Possible reentrancy with callback on transfer tokens

The following functions don't apply the CEI pattern. It's possible to reenter after the transfer if the token has some kind of callback functionality (e.g. ERC777/ERC1155).

*There are 4 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit state update on line 731
728: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), state.liquidatorCost);

// @audit state update on line 913
901: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

// @audit state update on line 949
946: 		        SafeERC20.safeTransfer(IERC20(asset), receiver, assets);

// @audit state update on line 992
986: 		                SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);
```

*GitHub* : [986](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L986), [728](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L728), [901](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L901), [946](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L946)

### [L-03]<a name="l-03"></a> Missing checks in constructor/initialize

There are some missing checks in these functions, and this could lead to unexpected scenarios. Consider always adding a sanity check for state variables.

*There are 6 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit baseRatePerYearX96, multiplierPerYearX96, jumpMultiplierPerYearX96, _kinkX96
33: 		    constructor(
34: 		        uint256 baseRatePerYearX96,
35: 		        uint256 multiplierPerYearX96,
36: 		        uint256 jumpMultiplierPerYearX96,
37: 		        uint256 _kinkX96
```

*GitHub* : [33-37](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L33-L37)

```solidity
File: src/V3Oracle.sol

// @audit tokenId
395: 		    function _initializeState(uint256 tokenId) internal view returns (PositionState memory state) {
```

*GitHub* : [395](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L395)

```solidity
File: src/automators/AutoExit.sol

// @audit _TWAPSeconds, _maxTWAPTickDifference
33: 		    constructor(
34: 		        INonfungiblePositionManager _npm,
35: 		        address _operator,
36: 		        address _withdrawer,
37: 		        uint32 _TWAPSeconds,
38: 		        uint16 _maxTWAPTickDifference,
39: 		        address _zeroxRouter,
40: 		        address _universalRouter
```

*GitHub* : [33-40](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L33-L40)

```solidity
File: src/automators/Automator.sol

// @audit _TWAPSeconds, _maxTWAPTickDifference
41: 		    constructor(
42: 		        INonfungiblePositionManager npm,
43: 		        address _operator,
44: 		        address _withdrawer,
45: 		        uint32 _TWAPSeconds,
46: 		        uint16 _maxTWAPTickDifference,
47: 		        address _zeroxRouter,
48: 		        address _universalRouter
```

*GitHub* : [41-48](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L41-L48)

```solidity
File: src/transformers/AutoCompound.sol

// @audit _TWAPSeconds, _maxTWAPTickDifference
37: 		    constructor(
38: 		        INonfungiblePositionManager _npm,
39: 		        address _operator,
40: 		        address _withdrawer,
41: 		        uint32 _TWAPSeconds,
42: 		        uint16 _maxTWAPTickDifference
```

*GitHub* : [37-42](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L37-L42)

```solidity
File: src/transformers/AutoRange.sol

// @audit _TWAPSeconds, _maxTWAPTickDifference
25: 		    constructor(
26: 		        INonfungiblePositionManager _npm,
27: 		        address _operator,
28: 		        address _withdrawer,
29: 		        uint32 _TWAPSeconds,
30: 		        uint16 _maxTWAPTickDifference,
31: 		        address _zeroxRouter,
32: 		        address _universalRouter
```

*GitHub* : [25-32](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L25-L32)

### [L-04]<a name="l-04"></a> Missing checks for state variable assignments

There are some missing checks in these functions, and this could lead to unexpected scenarios. Consider always adding a sanity check for state variables.

*There are 26 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

95: 		        baseRatePerSecondX96 = baseRatePerYearX96 / YEAR_SECS;

96: 		        multiplierPerSecondX96 = multiplierPerYearX96 / YEAR_SECS;

97: 		        jumpMultiplierPerSecondX96 = jumpMultiplierPerYearX96 / YEAR_SECS;

98: 		        kinkX96 = _kinkX96;
```

*GitHub* : [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L95), [96](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L96), [97](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L97), [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L98)

```solidity
File: src/V3Oracle.sol

240: 		        feedConfigs[token] = config;
```

*GitHub* : [240](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L240)

```solidity
File: src/V3Vault.sol

446: 		            loans[tokenId] = Loan(0);

461: 		                loans[tokenId] = Loan(loans[oldTokenId].debtShares);

487: 		        transformApprovals[msg.sender][tokenId][target] = isActive;

818: 		        minLoanSize = _minLoanSize;

819: 		        globalLendLimit = _globalLendLimit;

820: 		        globalDebtLimit = _globalDebtLimit;

821: 		        dailyLendIncreaseLimitMin = _dailyLendIncreaseLimitMin;

822: 		        dailyDebtIncreaseLimitMin = _dailyDebtIncreaseLimitMin;

838: 		        reserveFactorX32 = _reserveFactorX32;

1138: 		            lastLendExchangeRateX96 = newLendExchangeRateX96;

1252: 		            dailyLendIncreaseLimitLeft =
1253: 		                dailyLendIncreaseLimitMin > lendIncreaseLimit ? dailyLendIncreaseLimitMin : lendIncreaseLimit;

1264: 		            dailyDebtIncreaseLimitLeft =
1265: 		                dailyDebtIncreaseLimitMin > debtIncreaseLimit ? dailyDebtIncreaseLimitMin : debtIncreaseLimit;

1298: 		        ownedTokensIndex[tokenId] = ownedTokens[to].length;

1300: 		        tokenOwner[tokenId] = to;

1308: 		            ownedTokens[from][tokenIndex] = lastTokenId;

1309: 		            ownedTokensIndex[lastTokenId] = tokenIndex;
```

*GitHub* : [819](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L819), [820](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L820), [821](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L821), [822](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L822), [838](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L838), [1138](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1138), [1252-1253](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1252-L1253), [1264-1265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1264-L1265), [1298](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1298), [1300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1300), [1308](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1308), [1309](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1309), [446](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L446), [461](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L461), [487](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L487), [818](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L818)

```solidity
File: src/automators/AutoExit.sol

230: 		        positionConfigs[tokenId] = config;
```

*GitHub* : [230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L230)

```solidity
File: src/transformers/AutoCompound.sol

250: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] + amount;

257: 		            positionBalances[tokenId][token] = amount;

270: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] - amount;
```

*GitHub* : [270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L270), [250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L250), [257](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L257)

```solidity
File: src/transformers/AutoRange.sol

284: 		        positionConfigs[tokenId] = config;
```

*GitHub* : [284](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L284)

### [L-05]<a name="l-05"></a> `payable` function does not transfer ETH

The following functions can be called by any user, who may also send some funds by mistake. In that case, those funds will be lost (this also applies to delegatecalls, in case they don't use the transferred ETH).

*There are 2 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

251: 		    receive() external payable {
```

*GitHub* : [251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L251)

```solidity
File: src/transformers/V3Utils.sol

914: 		    receive() external payable {
```

*GitHub* : [914](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L914)

### [L-06]<a name="l-06"></a> Functions calling contracts with transfer hooks are missing reentrancy guards

Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks will open the users of this protocol up to read-only reentrancies with no way to protect against it, except by block-listing the whole protocol.

*There are 26 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

401: 		        nonfungiblePositionManager.safeTransferFrom(msg.sender, address(this), tokenId, abi.encode(recipient));

424: 		        nonfungiblePositionManager.safeTransferFrom(owner, address(this), tokenId, abi.encode(recipient));

599: 		        SafeERC20.safeTransfer(IERC20(asset), isTransformMode ? msg.sender : owner, assets);

728: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), state.liquidatorCost);

779: 		            SafeERC20.safeTransfer(IERC20(asset), receiver, amount);

901: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

946: 		        SafeERC20.safeTransfer(IERC20(asset), receiver, assets);

986: 		                SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

1083: 		        nonfungiblePositionManager.safeTransferFrom(address(this), owner, tokenId);
```

*GitHub* : [1083](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1083), [401](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L401), [424](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L424), [599](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L599), [728](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L728), [779](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L779), [901](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L901), [946](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L946), [986](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L986)

```solidity
File: src/automators/Automator.sol

226: 		            SafeERC20.safeTransfer(token, to, amount);
```

*GitHub* : [226](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L226)

```solidity
File: src/transformers/AutoCompound.sol

272: 		        SafeERC20.safeTransfer(IERC20(token), to, amount);
```

*GitHub* : [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L272)

```solidity
File: src/transformers/LeverageTransformer.sol

88: 		            SafeERC20.safeTransfer(IERC20(token0), params.recipient, amount0 - added0);

91: 		            SafeERC20.safeTransfer(IERC20(token1), params.recipient, amount1 - added1);

94: 		            SafeERC20.safeTransfer(IERC20(token), params.recipient, amount);

170: 		            SafeERC20.safeTransfer(IERC20(token0), params.recipient, amount0);

173: 		            SafeERC20.safeTransfer(IERC20(token1), params.recipient, amount1);
```

*GitHub* : [91](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L91), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L94), [170](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L170), [88](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L88), [173](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L173)

```solidity
File: src/transformers/V3Utils.sol

578: 		            SafeERC20.safeTransferFrom(token0, msg.sender, address(this), needed0);

581: 		            SafeERC20.safeTransferFrom(token1, msg.sender, address(this), needed1);

584: 		            SafeERC20.safeTransferFrom(otherToken, msg.sender, address(this), neededOther);

872: 		            SafeERC20.safeTransfer(token, to, amount);
```

*GitHub* : [584](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L584), [578](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L578), [581](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L581), [872](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L872)

```solidity
File: src/utils/FlashloanLiquidator.sol

85: 		        SafeERC20.safeTransfer(data.asset, msg.sender, data.liquidationCost + (fee0 + fee1));

91: 		                SafeERC20.safeTransfer(data.swap0.tokenIn, data.liquidator, balance);

97: 		                SafeERC20.safeTransfer(data.swap1.tokenIn, data.liquidator, balance);

106: 		                SafeERC20.safeTransfer(data.asset, data.liquidator, balance);
```

*GitHub* : [97](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L97), [85](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L85), [91](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L91), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L106)

```solidity
File: src/utils/Swapper.sol

98: 		                SafeERC20.safeTransfer(params.tokenIn, universalRouter, params.amountIn);

167: 		        SafeERC20.safeTransfer(IERC20(tokenIn), msg.sender, amountToPay);
```

*GitHub* : [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L98), [167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L167)

### [L-07]<a name="l-07"></a> `decimals` is not part of the `ERC20` standard

The `decimals` function is not part of the `ERC20` standard, and they may revert with some tokens if the don't also extend the `IERC20Metadata` interface.

*There are 3 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit IERC20Metadata(_referenceToken).decimals()
82: 		        referenceTokenDecimals = IERC20Metadata(_referenceToken).decimals();

// @audit IERC20Metadata(token).decimals()
216: 		        uint8 tokenDecimals = IERC20Metadata(token).decimals();
```

*GitHub* : [216](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L216), [82](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L82)

```solidity
File: src/V3Vault.sol

// @audit IERC20Metadata(_asset).decimals()
179: 		        assetDecimals = IERC20Metadata(_asset).decimals();
```

*GitHub* : [179](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L179)

### [L-08]<a name="l-08"></a> Large transfers may not work with some `ERC20` tokens

Some `IERC20` implementations (e.g `UNI`, `COMP`) may fail if the valued `transferred` is larger than `uint96`. [Source](https://github.com/d-xo/weird-erc20/blob/main/src/Uint96.sol).

*There are 17 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

599: 		        SafeERC20.safeTransfer(IERC20(asset), isTransformMode ? msg.sender : owner, assets);

779: 		            SafeERC20.safeTransfer(IERC20(asset), receiver, amount);

946: 		        SafeERC20.safeTransfer(IERC20(asset), receiver, assets);
```

*GitHub* : [779](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L779), [599](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L599), [946](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L946)

```solidity
File: src/automators/Automator.sol

226: 		            SafeERC20.safeTransfer(token, to, amount);
```

*GitHub* : [226](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L226)

```solidity
File: src/transformers/AutoCompound.sol

272: 		        SafeERC20.safeTransfer(IERC20(token), to, amount);
```

*GitHub* : [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L272)

```solidity
File: src/transformers/LeverageTransformer.sol

88: 		            SafeERC20.safeTransfer(IERC20(token0), params.recipient, amount0 - added0);

91: 		            SafeERC20.safeTransfer(IERC20(token1), params.recipient, amount1 - added1);

94: 		            SafeERC20.safeTransfer(IERC20(token), params.recipient, amount);

170: 		            SafeERC20.safeTransfer(IERC20(token0), params.recipient, amount0);

173: 		            SafeERC20.safeTransfer(IERC20(token1), params.recipient, amount1);
```

*GitHub* : [173](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L173), [88](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L88), [91](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L91), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L94), [170](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L170)

```solidity
File: src/transformers/V3Utils.sol

872: 		            SafeERC20.safeTransfer(token, to, amount);
```

*GitHub* : [872](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L872)

```solidity
File: src/utils/FlashloanLiquidator.sol

85: 		        SafeERC20.safeTransfer(data.asset, msg.sender, data.liquidationCost + (fee0 + fee1));

91: 		                SafeERC20.safeTransfer(data.swap0.tokenIn, data.liquidator, balance);

97: 		                SafeERC20.safeTransfer(data.swap1.tokenIn, data.liquidator, balance);

106: 		                SafeERC20.safeTransfer(data.asset, data.liquidator, balance);
```

*GitHub* : [85](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L85), [91](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L91), [97](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L97), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L106)

```solidity
File: src/utils/Swapper.sol

98: 		                SafeERC20.safeTransfer(params.tokenIn, universalRouter, params.amountIn);

167: 		        SafeERC20.safeTransfer(IERC20(tokenIn), msg.sender, amountToPay);
```

*GitHub* : [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L98), [167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L167)

### [L-09]<a name="l-09"></a> Large approvals may not work with some `ERC20` tokens

Not all `IERC20` implementations are totally compliant, and some (e.g `UNI`, `COMP`) may fail if the valued passed to `approve` is larger than `uint96`. If the approval amount is `type(uint256).max`, which may cause issues with systems that expect the value passed to approve to be reflected in the allowances mapping.

*There are 15 instance(s) of this issue:*

```solidity
File: src/transformers/AutoCompound.sol

280: 		            SafeERC20.safeApprove(IERC20(token0), address(nonfungiblePositionManager), type(uint256).max);

284: 		            SafeERC20.safeApprove(IERC20(token1), address(nonfungiblePositionManager), type(uint256).max);
```

*GitHub* : [284](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L284), [280](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L280)

```solidity
File: src/transformers/AutoRange.sol

213: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), state.maxAddAmount0);

214: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), state.maxAddAmount1);

220: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), 0);

221: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), 0);
```

*GitHub* : [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L221), [213](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L213), [214](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L214), [220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L220)

```solidity
File: src/transformers/LeverageTransformer.sol

165: 		        SafeERC20.safeApprove(IERC20(token), msg.sender, amount);
```

*GitHub* : [165](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L165)

```solidity
File: src/transformers/V3Utils.sol

831: 		            SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), 0);

832: 		            SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), total0);

835: 		            SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), 0);

836: 		            SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), total1);
```

*GitHub* : [835](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L835), [831](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L831), [832](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L832), [836](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L836)

```solidity
File: src/utils/FlashloanLiquidator.sol

72: 		        SafeERC20.safeApprove(data.asset, address(data.vault), data.liquidationCost);

78: 		        SafeERC20.safeApprove(data.asset, address(data.vault), 0);
```

*GitHub* : [72](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L72), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L78)

```solidity
File: src/utils/Swapper.sol

87: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, params.amountIn);

94: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, 0);
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L87), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L94)

### [L-10]<a name="l-10"></a> `approve` can revert if the current approval is not zero

Some tokens like USDT check for the current approval, and they revert if it's not zero. While Tether is known to do this, it applies to other tokens as well, which are trying to protect against [this](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit) attack vector.

*There are 13 instance(s) of this issue:*

```solidity
File: src/transformers/AutoRange.sol

213: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), state.maxAddAmount0);

214: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), state.maxAddAmount1);

220: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), 0);

221: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), 0);
```

*GitHub* : [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L221), [213](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L213), [214](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L214), [220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L220)

```solidity
File: src/transformers/LeverageTransformer.sol

165: 		        SafeERC20.safeApprove(IERC20(token), msg.sender, amount);
```

*GitHub* : [165](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L165)

```solidity
File: src/transformers/V3Utils.sol

831: 		            SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), 0);

832: 		            SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), total0);

835: 		            SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), 0);

836: 		            SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), total1);
```

*GitHub* : [835](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L835), [831](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L831), [832](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L832), [836](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L836)

```solidity
File: src/utils/FlashloanLiquidator.sol

72: 		        SafeERC20.safeApprove(data.asset, address(data.vault), data.liquidationCost);

78: 		        SafeERC20.safeApprove(data.asset, address(data.vault), 0);
```

*GitHub* : [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L78), [72](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L72)

```solidity
File: src/utils/Swapper.sol

87: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, params.amountIn);

94: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, 0);
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L87), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L94)

### [L-11]<a name="l-11"></a> `safeApprove` is deprecated

The usage of deprecated library functions should be discouraged, as `safeApprove` is also potentially [dangerous](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/2219).

*There are 15 instance(s) of this issue:*

```solidity
File: src/transformers/AutoCompound.sol

280: 		            SafeERC20.safeApprove(IERC20(token0), address(nonfungiblePositionManager), type(uint256).max);

284: 		            SafeERC20.safeApprove(IERC20(token1), address(nonfungiblePositionManager), type(uint256).max);
```

*GitHub* : [284](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L284), [280](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L280)

```solidity
File: src/transformers/AutoRange.sol

213: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), state.maxAddAmount0);

214: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), state.maxAddAmount1);

220: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), 0);

221: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), 0);
```

*GitHub* : [213](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L213), [214](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L214), [220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L220), [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L221)

```solidity
File: src/transformers/LeverageTransformer.sol

165: 		        SafeERC20.safeApprove(IERC20(token), msg.sender, amount);
```

*GitHub* : [165](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L165)

```solidity
File: src/transformers/V3Utils.sol

831: 		            SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), 0);

832: 		            SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), total0);

835: 		            SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), 0);

836: 		            SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), total1);
```

*GitHub* : [835](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L835), [831](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L831), [832](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L832), [836](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L836)

```solidity
File: src/utils/FlashloanLiquidator.sol

72: 		        SafeERC20.safeApprove(data.asset, address(data.vault), data.liquidationCost);

78: 		        SafeERC20.safeApprove(data.asset, address(data.vault), 0);
```

*GitHub* : [72](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L72), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L78)

```solidity
File: src/utils/Swapper.sol

87: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, params.amountIn);

94: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, 0);
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L87), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L94)

### [L-12]<a name="l-12"></a> Unsafe downcast may overflow

When a type is downcast to a smaller type, the higher order bits are discarded, resulting in the application of a modulo operation to the original value.

If the downcasted value is large enough, this may result in an overflow that will not revert.

*There are 3 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit uint256 liquidationValue * fees0 / feeValue downcasted to uint128
1054: 		                fees0 = uint128(liquidationValue * fees0 / feeValue);

// @audit uint256 liquidationValue * fees1 / feeValue downcasted to uint128
1055: 		                fees1 = uint128(liquidationValue * fees1 / feeValue);

// @audit uint256 (liquidationValue - feeValue) * liquidity / (fullValue - feeValue) downcasted to uint128
1060: 		                liquidity = uint128((liquidationValue - feeValue) * liquidity / (fullValue - feeValue));
```

*GitHub* : [1055](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1055), [1054](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1054), [1060](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1060)

### [L-13]<a name="l-13"></a> Unsafe `uint` to `int` conversion

The `int` type in Solidity uses the [two's complement system](https://en.wikipedia.org/wiki/Two%27s_complement), so it is possible to accidentally overflow a very large `uint` to an `int`, even if they share the same number of bytes (e.g. a `uint256 number > type(uint128).max` will overflow a `int256` cast).

Consider using the [SafeCast](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/math/SafeCast.sol) library to prevent any overflows.

*There are 3 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

// @audit uint16 maxDifference downcasted to int16
173: 		            return twapTick - currentTick >= -int16(maxDifference) && twapTick - currentTick <= int16(maxDifference);

// @audit uint16 maxDifference downcasted to int16
173: 		            return twapTick - currentTick >= -int16(maxDifference) && twapTick - currentTick <= int16(maxDifference);
```

*GitHub* : [173](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L173), [173](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L173)

```solidity
File: src/utils/Swapper.sol

// @audit uint256 params.amountIn downcasted to int256
137: 		                int256(params.amountIn),
```

*GitHub* : [137](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L137)

### [L-14]<a name="l-14"></a> Use of `abi.encodeWithSignature`/`abi.encodeWithSelector` instead of `abi.encodeCall`

Consider refactoring the code by using `abi.encodeCall` instead of `abi.encodeWithSignature`/`abi.encodeWithSelector`, as the former keeps the code [typo/type safe](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/3693).

*There are 2 instance(s) of this issue:*

```solidity
File: src/transformers/AutoCompound.sol

92: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoCompound.execute.selector, params)
```

*GitHub* : [92](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L92)

```solidity
File: src/transformers/AutoRange.sol

102: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoRange.execute.selector, params)
```

*GitHub* : [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L102)

### [L-15]<a name="l-15"></a> Subtraction may underflow if multiplication is too large

The following expressions may underflow, as the subtrahend could be greater than the minuend in case the former is multiplied by a large number.

*There are 7 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

1107: 		                (Q96 - ((fullValue - maxPenaltyValue) * Q96 / (startLiquidationValue - maxPenaltyValue)));
```

*GitHub* : [1107](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1107)

```solidity
File: src/automators/AutoExit.sol

155: 		                state.amount0 -= state.feeAmount0 * params.rewardX64 / Q64;

156: 		                state.amount1 -= state.feeAmount1 * params.rewardX64 / Q64;

187: 		                    state.amount0 -= state.amount0 * params.rewardX64 / Q64;

189: 		                    state.amount1 -= state.amount1 * params.rewardX64 / Q64;

194: 		            state.amount0 -= (config.onlyFees ? state.feeAmount0 : state.amount0) * params.rewardX64 / Q64;

195: 		            state.amount1 -= (config.onlyFees ? state.feeAmount1 : state.amount1) * params.rewardX64 / Q64;
```

*GitHub* : [194](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L194), [155](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L155), [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L156), [187](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L187), [189](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L189), [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L195)

### [L-16]<a name="l-16"></a> Possible division by 0 is not prevented

These functions can be called with 0 value in the input and this value is not checked for being bigger than 0, that means in some scenarios this can potentially trigger a division by zero.

*There are 5 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit priceX96
144: 		            ? (priceX96 - verifyPriceX96) * 10000 / priceX96

// @audit verifyPriceX96
145: 		            : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;
```

*GitHub* : [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L144), [145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L145)

```solidity
File: src/V3Vault.sol

// @audit feeValue
1054: 		                fees0 = uint128(liquidationValue * fees0 / feeValue);

// @audit feeValue
1055: 		                fees1 = uint128(liquidationValue * fees1 / feeValue);

// @audit collateralValue
1105: 		            uint256 startLiquidationValue = debt * fullValue / collateralValue;
```

*GitHub* : [1055](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1055), [1054](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1054), [1105](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1105)

### [L-17]<a name="l-17"></a> Code does not follow the best practice of check-effects-interaction

Code should follow the best-practice of [CEI](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.

*There are 6 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit nonfungiblePositionManager.approve(transformer, tokenId) called on line 520
542: 		        transformedTokenId = 0;

// @audit permit2.permitTransferFrom(
                permit,
                ISignatureTransfer.SignatureTransferDetails(address(this), state.liquidatorCost),
                msg.sender,
                signature
            ) called on line 720
731: 		        debtSharesTotal -= debtShares;

// @audit permit2.permitTransferFrom(
                permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature
            ) called on line 896
913: 		            dailyLendIncreaseLimitLeft -= assets;

// @audit permit2.permitTransferFrom(
                    permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature
                ) called on line 981
992: 		        debtSharesTotal -= shares;

// @audit permit2.permitTransferFrom(
                    permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature
                ) called on line 981
995: 		        dailyDebtIncreaseLimitLeft += assets;
```

*GitHub* : [913](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L913), [542](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L542), [731](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L731), [992](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L992), [995](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L995)

```solidity
File: src/transformers/AutoRange.sol

// @audit nonfungiblePositionManager.positions(params.tokenId) called on line 131
251: 		            positionConfigs[state.newTokenId] = config;
```

*GitHub* : [251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L251)

### [L-18]<a name="l-18"></a> Missing limits when setting min/max amounts

There are some missing limits in these functions, and this could lead to unexpected scenarios. Consider adding a min/max limit for the following values, when appropriate.

*There are 10 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit missing both checks -> baseRatePerYearX96, multiplierPerYearX96, jumpMultiplierPerYearX96, _kinkX96
82: 		    function setValues(
83: 		        uint256 baseRatePerYearX96,
84: 		        uint256 multiplierPerYearX96,
85: 		        uint256 jumpMultiplierPerYearX96,
86: 		        uint256 _kinkX96
```

*GitHub* : [82-86](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L82-L86)

```solidity
File: src/V3Oracle.sol

// @audit missing max check -> 
185: 		    function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

// @audit missing both checks -> maxFeedAge, twapSeconds
// @audit missing max check -> 
201: 		    function setTokenConfig(
202: 		        address token,
203: 		        AggregatorV3Interface feed,
204: 		        uint32 maxFeedAge,
205: 		        IUniswapV3Pool pool,
206: 		        uint32 twapSeconds,
207: 		        Mode mode,
208: 		        uint16 maxDifference
```

*GitHub* : [185](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L185), [201-208](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L201-L208)

```solidity
File: src/V3Vault.sol

// @audit missing both checks -> _minLoanSize, _globalLendLimit, _globalDebtLimit, _dailyLendIncreaseLimitMin, _dailyDebtIncreaseLimitMin
807: 		    function setLimits(
808: 		        uint256 _minLoanSize,
809: 		        uint256 _globalLendLimit,
810: 		        uint256 _globalDebtLimit,
811: 		        uint256 _dailyLendIncreaseLimitMin,
812: 		        uint256 _dailyDebtIncreaseLimitMin

// @audit missing both checks -> _reserveFactorX32
837: 		    function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

// @audit missing max check -> 
844: 		    function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

// @audit missing both checks -> collateralValueLimitFactorX32
// @audit missing min check -> collateralFactorX32
856: 		    function setTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32)

// @audit missing both checks -> debtExchangeRateX96, lendExchangeRateX96, newShares
// @audit missing min check -> oldShares
1205: 		    function _updateAndCheckCollateral(
1206: 		        uint256 tokenId,
1207: 		        uint256 debtExchangeRateX96,
1208: 		        uint256 lendExchangeRateX96,
1209: 		        uint256 oldShares,
1210: 		        uint256 newShares
```

*GitHub* : [856](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L856), [807-812](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L807-L812), [837](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L837), [844](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L844), [1205-1210](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1205-L1210)

```solidity
File: src/automators/Automator.sol

// @audit missing min check -> _maxTWAPTickDifference
// @audit missing max check -> _maxTWAPTickDifference
87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87)

```solidity
File: src/transformers/AutoCompound.sol

// @audit missing min check -> _totalRewardX64
243: 		    function setReward(uint64 _totalRewardX64) external onlyOwner {
```

*GitHub* : [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L243)

### [L-19]<a name="l-19"></a> Owner can renounce ownership

Each of the following contracts implements or inherits the `renounceOwnership` function. This can represent a certain risk if the ownership is renounced for any other reason than by design. Renouncing ownership will leave the contract without an owner, thereby removing any functionality that is only available to the owner.

*There are 4 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

11: 		contract InterestRateModel is Ownable, IInterestRateModel, IErrors {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L11)

```solidity
File: src/V3Oracle.sol

24: 		contract V3Oracle is IV3Oracle, Ownable, IErrors {
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L24)

```solidity
File: src/V3Vault.sol

30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

```solidity
File: src/automators/Automator.sol

19: 		abstract contract Automator is Swapper, Ownable {
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L19)

### [L-20]<a name="l-20"></a> Missing contract-existence checks before low-level calls

Low-level calls return success if there is no code present at the specified address, and this could lead to unexpected scenarios.

Ensure that the code is initialized by checking `<address>.code.length > 0`.

*There are 5 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

522: 		        (bool success,) = transformer.call(data);
```

*GitHub* : [522](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L522)

```solidity
File: src/automators/Automator.sol

130: 		            (bool sent,) = to.call{value: balance}("");

221: 		            (bool sent,) = to.call{value: amount}("");
```

*GitHub* : [130](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L130), [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L221)

```solidity
File: src/transformers/V3Utils.sol

867: 		            (bool sent,) = to.call{value: amount}("");
```

*GitHub* : [867](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L867)

```solidity
File: src/utils/Swapper.sol

89: 		                (bool success,) = zeroxRouter.call(data.data);
```

*GitHub* : [89](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L89)

### [L-21]<a name="l-21"></a> External calls in an unbounded loop can result in a DoS

Consider limiting the number of iterations in loops that make external calls, as just a single one of them failing will result in a revert.

*There are 1 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

// @audit balanceOf (112)
111: 		        for (; i < count; ++i) {
```

*GitHub* : [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L111)

### [L-22]<a name="l-22"></a> Solidity version `0.8.20` may not work on other chains due to `PUSH0`

In Solidity `0.8.20`'s compiler, the default target EVM version has been changed to Shanghai. This version introduces a new op code called `PUSH0`.

However, not all Layer 2 solutions have implemented this op code yet, leading to deployment failures on these chains. To overcome this problem, it is recommended to utilize an earlier EVM version.

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L2)

```solidity
File: src/V3Oracle.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L2)

```solidity
File: src/V3Vault.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L2)

```solidity
File: src/automators/AutoExit.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L2)

```solidity
File: src/automators/Automator.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L2)

```solidity
File: src/transformers/AutoCompound.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L2)

```solidity
File: src/transformers/AutoRange.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L2)

```solidity
File: src/transformers/LeverageTransformer.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L2)

```solidity
File: src/transformers/V3Utils.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L2)

```solidity
File: src/utils/FlashloanLiquidator.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L2)

```solidity
File: src/utils/Swapper.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L2)

### [L-23]<a name="l-23"></a> Lack of two-step update for updating protocol addresses

Add a two-step process for any critical address changes.

*There are 8 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

201: 		    function setTokenConfig(
202: 		        address token,
203: 		        AggregatorV3Interface feed,
204: 		        uint32 maxFeedAge,
205: 		        IUniswapV3Pool pool,
206: 		        uint32 twapSeconds,
207: 		        Mode mode,
208: 		        uint16 maxDifference
209: 		    ) external onlyOwner {
210: 		        // can not be unset
211: 		        if (mode == Mode.NOT_SET) {
212: 		            revert InvalidConfig();
213: 		        }
214: 		
215: 		        uint8 feedDecimals = feed.decimals();
216: 		        uint8 tokenDecimals = IERC20Metadata(token).decimals();
217: 		
218: 		        TokenConfig memory config;
219: 		
220: 		        if (token != referenceToken) {
221: 		            if (maxDifference < MIN_PRICE_DIFFERENCE) {
222: 		                revert InvalidConfig();
223: 		            }
224: 		
225: 		            address token0 = pool.token0();
226: 		            address token1 = pool.token1();
227: 		            if (!(token0 == token && token1 == referenceToken || token0 == referenceToken && token1 == token)) {
228: 		                revert InvalidPool();
229: 		            }
230: 		            bool isToken0 = token0 == token;
231: 		            config = TokenConfig(
232: 		                feed, maxFeedAge, feedDecimals, tokenDecimals, pool, isToken0, twapSeconds, mode, maxDifference
233: 		            );
234: 		        } else {
235: 		            config = TokenConfig(
236: 		                feed, maxFeedAge, feedDecimals, tokenDecimals, IUniswapV3Pool(address(0)), false, 0, Mode.CHAINLINK, 0
237: 		            );
238: 		        }
239: 		
240: 		        feedConfigs[token] = config;
241: 		
242: 		        emit TokenConfigUpdated(token, config);
243: 		        emit OracleModeUpdated(token, mode);
244: 		    }

265: 		    function setEmergencyAdmin(address admin) external onlyOwner {
266: 		        emergencyAdmin = admin;
267: 		        emit SetEmergencyAdmin(admin);
268: 		    }
```

*GitHub* : [201-244](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L201-L244), [265-268](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L265-L268)

```solidity
File: src/V3Vault.sol

788: 		    function setTransformer(address transformer, bool active) external onlyOwner {
789: 		        // protects protocol from owner trying to set dangerous transformer
790: 		        if (
791: 		            transformer == address(0) || transformer == address(this) || transformer == asset
792: 		                || transformer == address(nonfungiblePositionManager)
793: 		        ) {
794: 		            revert InvalidConfig();
795: 		        }
796: 		
797: 		        transformerAllowList[transformer] = active;
798: 		        emit SetTransformer(transformer, active);
799: 		    }

856: 		    function setTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32)
857: 		        external
858: 		        onlyOwner
859: 		    {
860: 		        if (collateralFactorX32 > MAX_COLLATERAL_FACTOR_X32) {
861: 		            revert CollateralFactorExceedsMax();
862: 		        }
863: 		        tokenConfigs[token].collateralFactorX32 = collateralFactorX32;
864: 		        tokenConfigs[token].collateralValueLimitFactorX32 = collateralValueLimitFactorX32;
865: 		        emit SetTokenConfig(token, collateralFactorX32, collateralValueLimitFactorX32);
866: 		    }

870: 		    function setEmergencyAdmin(address admin) external onlyOwner {
871: 		        emergencyAdmin = admin;
872: 		        emit SetEmergencyAdmin(admin);
873: 		    }
```

*GitHub* : [788-799](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L788-L799), [856-866](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L856-L866), [870-873](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L870-L873)

```solidity
File: src/automators/Automator.sol

59: 		    function setWithdrawer(address _withdrawer) public onlyOwner {
60: 		        emit WithdrawerChanged(_withdrawer);
61: 		        withdrawer = _withdrawer;
62: 		    }

69: 		    function setOperator(address _operator, bool _active) public onlyOwner {
70: 		        emit OperatorChanged(_operator, _active);
71: 		        operators[_operator] = _active;
72: 		    }

79: 		    function setVault(address _vault, bool _active) public onlyOwner {
80: 		        emit VaultChanged(_vault, _active);
81: 		        vaults[_vault] = _active;
82: 		    }
```

*GitHub* : [59-62](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L59-L62), [69-72](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L69-L72), [79-82](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L79-L82)

### [L-24]<a name="l-24"></a> Use of ownership with a single step rather than double

A single step ownership change is risky due to the fact that the new owner address could be wrong.

Instead, consider using a contract like [Ownable2Step](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable2Step.sol), which provides a two-step ownership.

*There are 4 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L4)

```solidity
File: src/V3Oracle.sol

15: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L15)

```solidity
File: src/V3Vault.sol

16: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L16)

```solidity
File: src/automators/Automator.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L4)

### [L-25]<a name="l-25"></a> Loss of precision on division

Solidity doesn't support fractions, so divisions by large numbers could result in the quotient being zero.

To avoid this, it's recommended to require a minimum numerator amount to ensure that it is always greater than the denominator.

*There are 66 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

50: 		        return debt * Q96 / (cash + debt);

67: 		            borrowRateX96 = (utilizationRateX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

69: 		            uint256 normalRateX96 = (kinkX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

71: 		            borrowRateX96 = (excessUtilX96 * jumpMultiplierPerSecondX96 / Q96) + normalRateX96;

74: 		        supplyRateX96 = utilizationRateX96 * borrowRateX96 / Q96;

95: 		        baseRatePerSecondX96 = baseRatePerYearX96 / YEAR_SECS;

96: 		        multiplierPerSecondX96 = multiplierPerYearX96 / YEAR_SECS;

97: 		        jumpMultiplierPerSecondX96 = jumpMultiplierPerYearX96 / YEAR_SECS;
```

*GitHub* : [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L50), [67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L67), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L69), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L71), [74](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L74), [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L95), [96](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L96), [97](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L97)

```solidity
File: src/V3Oracle.sol

120: 		        value = (price0X96 * (amount0 + fees0) / Q96 + price1X96 * (amount1 + fees1) / Q96) * Q96 / priceTokenX96;

120: 		        value = (price0X96 * (amount0 + fees0) / Q96 + price1X96 * (amount1 + fees1) / Q96) * Q96 / priceTokenX96;

120: 		        value = (price0X96 * (amount0 + fees0) / Q96 + price1X96 * (amount1 + fees1) / Q96) * Q96 / priceTokenX96;

121: 		        feeValue = (price0X96 * fees0 / Q96 + price1X96 * fees1 / Q96) * Q96 / priceTokenX96;

121: 		        feeValue = (price0X96 * fees0 / Q96 + price1X96 * fees1 / Q96) * Q96 / priceTokenX96;

121: 		        feeValue = (price0X96 * fees0 / Q96 + price1X96 * fees1 / Q96) * Q96 / priceTokenX96;

122: 		        price0X96 = price0X96 * Q96 / priceTokenX96;

123: 		        price1X96 = price1X96 * Q96 / priceTokenX96;

129: 		        uint256 derivedPoolPriceX96 = price0X96 * Q96 / price1X96;

144: 		            ? (priceX96 - verifyPriceX96) * 10000 / priceX96

145: 		            : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;

304: 		            chainlinkPriceX96 = (10 ** referenceTokenDecimals) * chainlinkPriceX96 * Q96 / chainlinkReferencePriceX96
305: 		                / (10 ** feedConfig.tokenDecimals);

304: 		            chainlinkPriceX96 = (10 ** referenceTokenDecimals) * chainlinkPriceX96 * Q96 / chainlinkReferencePriceX96

342: 		        return uint256(answer) * Q96 / (10 ** feedConfig.feedDecimals);

353: 		            poolTWAPPriceX96 = Q96 * Q96 / priceX96;

369: 		            int24 tick = int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapSeconds)));
```

*GitHub* : [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L120), [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L120), [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L120), [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L121), [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L121), [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L121), [122](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L122), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L123), [129](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L129), [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L144), [145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L145), [304-305](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L304-L305), [304](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L304), [342](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L342), [353](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L353), [369](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L369)

```solidity
File: src/V3Vault.sol

36: 		    uint32 public constant MAX_COLLATERAL_FACTOR_X32 = uint32(Q32 * 90 / 100); // 90%

36: 		    uint32 public constant MAX_COLLATERAL_FACTOR_X32 = uint32(Q32 * 90 / 100); // 90%

38: 		    uint32 public constant MIN_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 2 / 100); // 2%

38: 		    uint32 public constant MIN_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 2 / 100); // 2%

39: 		    uint32 public constant MAX_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 10 / 100); // 10%

39: 		    uint32 public constant MAX_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 10 / 100); // 10%

41: 		    uint32 public constant MIN_RESERVE_PROTECTION_FACTOR_X32 = uint32(Q32 / 100); //1%

41: 		    uint32 public constant MIN_RESERVE_PROTECTION_FACTOR_X32 = uint32(Q32 / 100); //1%

769: 		            _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up) * reserveProtectionFactorX32 / Q32;

1054: 		                fees0 = uint128(liquidationValue * fees0 / feeValue);

1055: 		                fees1 = uint128(liquidationValue * fees1 / feeValue);

1060: 		                liquidity = uint128((liquidationValue - feeValue) * liquidity / (fullValue - feeValue));

1100: 		        uint256 maxPenaltyValue = debt * (Q32 + MAX_LIQUIDATION_PENALTY_X32) / Q32;

1105: 		            uint256 startLiquidationValue = debt * fullValue / collateralValue;

1107: 		                (Q96 - ((fullValue - maxPenaltyValue) * Q96 / (startLiquidationValue - maxPenaltyValue)));

1109: 		                + (MAX_LIQUIDATION_PENALTY_X32 - MIN_LIQUIDATION_PENALTY_X32) * penaltyFractionX96 / Q96;

1111: 		            liquidationValue = debt * (Q32 + penaltyX32) / Q32;

1116: 		            uint256 penaltyValue = fullValue * (Q32 - MAX_LIQUIDATION_PENALTY_X32) / Q32;

1137: 		            newLendExchangeRateX96 = (totalLent - missing) * newLendExchangeRateX96 / totalLent;

1188: 		                + oldDebtExchangeRateX96 * (block.timestamp - lastRateUpdate) * borrowRateX96 / Q96;

1190: 		                + oldLendExchangeRateX96 * (block.timestamp - lastRateUpdate) * supplyRateX96 / Q96;

1230: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1238: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1250: 		            uint256 lendIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)
1251: 		                * (Q32 + MAX_DAILY_LEND_INCREASE_X32) / Q32;

1262: 		            uint256 debtIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)
1263: 		                * (Q32 + MAX_DAILY_DEBT_INCREASE_X32) / Q32;
```

*GitHub* : [36](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L36), [36](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L36), [38](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L38), [38](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L38), [39](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L39), [39](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L39), [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L41), [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L41), [769](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L769), [1054](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1054), [1055](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1055), [1060](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1060), [1100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1100), [1105](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1105), [1107](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1107), [1109](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1109), [1111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1111), [1116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1116), [1137](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1137), [1188](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1188), [1190](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1190), [1230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1230), [1238](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1238), [1250-1251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1250-L1251), [1262-1263](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1262-L1263)

```solidity
File: src/automators/AutoExit.sol

155: 		                state.amount0 -= state.feeAmount0 * params.rewardX64 / Q64;

156: 		                state.amount1 -= state.feeAmount1 * params.rewardX64 / Q64;

187: 		                    state.amount0 -= state.amount0 * params.rewardX64 / Q64;

189: 		                    state.amount1 -= state.amount1 * params.rewardX64 / Q64;

194: 		            state.amount0 -= (config.onlyFees ? state.feeAmount0 : state.amount0) * params.rewardX64 / Q64;

195: 		            state.amount1 -= (config.onlyFees ? state.feeAmount1 : state.amount1) * params.rewardX64 / Q64;
```

*GitHub* : [187](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L187), [155](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L155), [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L156), [189](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L189), [194](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L194), [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L195)

```solidity
File: src/automators/Automator.sol

187: 		            return (int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapPeriod))), true);
```

*GitHub* : [187](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L187)

```solidity
File: src/transformers/AutoCompound.sol

156: 		            state.maxAddAmount0 = state.amount0 * Q64 / (rewardX64 + Q64);

157: 		            state.maxAddAmount1 = state.amount1 * Q64 / (rewardX64 + Q64);

170: 		                state.amount0Fees = state.compounded0 * rewardX64 / Q64;

171: 		                state.amount1Fees = state.compounded1 * rewardX64 / Q64;
```

*GitHub* : [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L157), [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L156), [170](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L170), [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L171)

```solidity
File: src/transformers/AutoRange.sol

143: 		            state.protocolReward0 = state.feeAmount0 * params.rewardX64 / Q64;

144: 		            state.protocolReward1 = state.feeAmount1 * params.rewardX64 / Q64;

195: 		            state.maxAddAmount0 = config.onlyFees ? state.amount0 : state.amount0 * Q64 / (params.rewardX64 + Q64);

196: 		            state.maxAddAmount1 = config.onlyFees ? state.amount1 : state.amount1 * Q64 / (params.rewardX64 + Q64);

236: 		                state.protocolReward0 = state.amountAdded0 * params.rewardX64 / Q64;

237: 		                state.protocolReward1 = state.amountAdded1 * params.rewardX64 / Q64;
```

*GitHub* : [143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L143), [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L144), [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L195), [196](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L196), [236](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L236), [237](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L237)

### [L-26]<a name="l-26"></a> Gas griefing/theft is possible on an unsafe external call

A low-level call will copy any amount of bytes to local memory. When bytes are copied from returndata to memory, the memory expansion cost is paid.

This means that when using a standard solidity call, the callee can 'returnbomb' the caller, imposing an arbitrary gas cost.

Because this gas is paid by the caller and in the caller's context, it can cause the caller to run out of gas and halt execution.

Consider replacing all unsafe `call` with `excessivelySafeCall` from this [repository](https://github.com/nomad-xyz/ExcessivelySafeCall).

*There are 3 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

130: 		            (bool sent,) = to.call{value: balance}("");

221: 		            (bool sent,) = to.call{value: amount}("");
```

*GitHub* : [130](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L130), [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L221)

```solidity
File: src/transformers/V3Utils.sol

867: 		            (bool sent,) = to.call{value: amount}("");
```

*GitHub* : [867](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L867)

### [L-27]<a name="l-27"></a> Consider the case where `totalSupply` is zero

The following functions should handle the edge case where the totalSupply is zero, for example to avoid division by zero errors, as such errors may negatively impact the logic of these functions.

*There are 9 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

303: 		        uint256 value = _convertToAssets(totalSupply(), lendExchangeRateX96, Math.Rounding.Up);

314: 		        uint256 value = _convertToAssets(totalSupply(), lendExchangeRateX96, Math.Rounding.Up);

769: 		            _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up) * reserveProtectionFactorX32 / Q32;

906: 		        if (totalSupply() > globalLendLimit) {

1025: 		        uint256 lent = _convertToAssets(totalSupply(), lendExchangeRateX96, Math.Rounding.Down);

1134: 		            uint256 totalLent = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up);

1225: 		                uint256 lentAssets = _convertToAssets(totalSupply(), lendExchangeRateX96, Math.Rounding.Up);

1250: 		            uint256 lendIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)

1262: 		            uint256 debtIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)
```

*GitHub* : [769](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L769), [303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L303), [314](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L314), [906](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L906), [1025](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1025), [1134](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1134), [1225](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1225), [1250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1250), [1262](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1262)

### [L-28]<a name="l-28"></a> Use `increaseAllowance/decreaseAllowance` instead of `approve/safeApprove`

Changing an allowance with `approve` brings the risk that someone may use both the old and the new allowance by unfortunate transaction ordering. Refer to [ERC20 API: An Attack Vector on the Approve/TransferFrom Methods](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit).

It is recommended to use the `increaseAllowance/decreaseAllowance` to avoid ths problem.

*There are 17 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

520: 		        nonfungiblePositionManager.approve(transformer, tokenId);

537: 		        nonfungiblePositionManager.approve(address(0), tokenId);
```

*GitHub* : [520](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L520), [537](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L537)

```solidity
File: src/transformers/AutoCompound.sol

280: 		            SafeERC20.safeApprove(IERC20(token0), address(nonfungiblePositionManager), type(uint256).max);

284: 		            SafeERC20.safeApprove(IERC20(token1), address(nonfungiblePositionManager), type(uint256).max);
```

*GitHub* : [280](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L280), [284](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L284)

```solidity
File: src/transformers/AutoRange.sol

213: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), state.maxAddAmount0);

214: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), state.maxAddAmount1);

220: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), 0);

221: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), 0);
```

*GitHub* : [213](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L213), [214](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L214), [220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L220), [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L221)

```solidity
File: src/transformers/LeverageTransformer.sol

165: 		        SafeERC20.safeApprove(IERC20(token), msg.sender, amount);
```

*GitHub* : [165](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L165)

```solidity
File: src/transformers/V3Utils.sol

831: 		            SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), 0);

832: 		            SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), total0);

835: 		            SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), 0);

836: 		            SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), total1);
```

*GitHub* : [831](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L831), [832](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L832), [835](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L835), [836](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L836)

```solidity
File: src/utils/FlashloanLiquidator.sol

72: 		        SafeERC20.safeApprove(data.asset, address(data.vault), data.liquidationCost);

78: 		        SafeERC20.safeApprove(data.asset, address(data.vault), 0);
```

*GitHub* : [72](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L72), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L78)

```solidity
File: src/utils/Swapper.sol

87: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, params.amountIn);

94: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, 0);
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L87), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L94)

### [L-29]<a name="l-29"></a> `onlyOwner` functions not accessible if `owner` renounces ownership

The `owner` is able to perform certain privileged activities, but it's possible to set the owner to `address(0)`. This can represent a certain risk if the ownership is renounced for any other reason than by design.

Renouncing ownership will leave the contract without an `owner`, therefore limiting any functionality that needs authority.

*There are 14 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

87: 		    ) public onlyOwner {
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L87)

```solidity
File: src/V3Oracle.sol

185: 		    function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

209: 		    ) external onlyOwner {

265: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [185](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L185), [209](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L209), [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L265)

```solidity
File: src/V3Vault.sol

765: 		    function withdrawReserves(uint256 amount, address receiver) external onlyOwner {

788: 		    function setTransformer(address transformer, bool active) external onlyOwner {

837: 		    function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

844: 		    function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

858: 		        onlyOwner

870: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [765](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L765), [788](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L788), [837](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L837), [844](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L844), [858](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L858), [870](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L870)

```solidity
File: src/automators/Automator.sol

59: 		    function setWithdrawer(address _withdrawer) public onlyOwner {

69: 		    function setOperator(address _operator, bool _active) public onlyOwner {

79: 		    function setVault(address _vault, bool _active) public onlyOwner {

87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {
```

*GitHub* : [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L59), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L69), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L79), [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87)

### [L-30]<a name="l-30"></a> Using a vulnerable dependency from some libraries

This project is using a vulnerable version of some libraries, which have the following issues:



Current `@openzeppelin/contracts` version: 4.6.0

|Risk|Title|Min Version|Max Version|
|------|-------|-------------|-------------|
|LOW|[Denial of Service (DoS)](https://security.snyk.io/vuln/SNYK-JS-OPENZEPPELINCONTRACTS-5425827)|>=3.2.0|<4.8.3|
|MEDIUM|[Improper Input Validation](https://security.snyk.io/vuln/SNYK-JS-OPENZEPPELINCONTRACTS-5425051)|>=3.3.0|<4.9.2|
|MEDIUM|[Improper Encoding or Escaping of Output](https://security.snyk.io/vuln/SNYK-JS-OPENZEPPELINCONTRACTS-5838352)|>=4.0.0|<4.9.3|
|HIGH|[Improper Verification of Cryptographic Signature](https://security.snyk.io/vuln/SNYK-JS-OPENZEPPELINCONTRACTS-2980279)|>=0.0.0|<4.7.3|
|MEDIUM|[Denial of Service (DoS)](https://security.snyk.io/vuln/SNYK-JS-OPENZEPPELINCONTRACTS-2965798)|>=2.3.0|<4.7.2|
|LOW|[Incorrect Resource Transfer Between Spheres](https://security.snyk.io/vuln/SNYK-JS-OPENZEPPELINCONTRACTS-2965580)|>=4.6.0|<4.7.2|
|HIGH|[Incorrect Calculation](https://security.snyk.io/vuln/SNYK-JS-OPENZEPPELINCONTRACTS-2964946)|>=4.3.0|<4.7.2|
|HIGH|[Information Exposure](https://security.snyk.io/vuln/SNYK-JS-OPENZEPPELINCONTRACTS-2958050)|>=4.1.0|<4.7.1|
|HIGH|[Information Exposure](https://security.snyk.io/vuln/SNYK-JS-OPENZEPPELINCONTRACTS-2958047)|>=4.0.0|<4.7.1|
|LOW|[Missing Authorization](https://security.snyk.io/vuln/SNYK-JS-OPENZEPPELINCONTRACTS-5672116)|>=4.3.0|<4.9.1|

*There are 21 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L4)

```solidity
File: src/V3Oracle.sol

14: 		import "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

15: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [14](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L14), [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L15)

```solidity
File: src/V3Vault.sol

12: 		import "@openzeppelin/contracts/utils/math/Math.sol";

13: 		import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

14: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

15: 		import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

16: 		import "@openzeppelin/contracts/access/Ownable.sol";

17: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

18: 		import "@openzeppelin/contracts/utils/Multicall.sol";
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L12), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L13), [14](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L14), [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L15), [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L16), [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L17), [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L18)

```solidity
File: src/automators/Automator.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";

5: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

6: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L5), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L6)

```solidity
File: src/transformers/AutoCompound.sol

4: 		import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

5: 		import "@openzeppelin/contracts/utils/Multicall.sol";

6: 		import "@openzeppelin/contracts/utils/math/SafeMath.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L5), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L6)

```solidity
File: src/transformers/LeverageTransformer.sol

4: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

5: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L5)

```solidity
File: src/transformers/V3Utils.sol

4: 		import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

5: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L5)

```solidity
File: src/utils/Swapper.sol

4: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L4)

### [L-31]<a name="l-31"></a> Centralization issue caused by admin privileges

There are priviliged roles that are a single point of failure, who can use critical functions, posing a centralization issue.

*There are 15 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

82: 		    function setValues(
```

*GitHub* : [82](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L82)

```solidity
File: src/V3Oracle.sol

185: 		    function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

201: 		    function setTokenConfig(

265: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [185](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L185), [201](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L201), [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L265)

```solidity
File: src/V3Vault.sol

765: 		    function withdrawReserves(uint256 amount, address receiver) external onlyOwner {

788: 		    function setTransformer(address transformer, bool active) external onlyOwner {

837: 		    function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

844: 		    function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

856: 		    function setTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32)

870: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [765](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L765), [788](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L788), [837](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L837), [844](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L844), [856](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L856), [870](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L870)

```solidity
File: src/automators/Automator.sol

59: 		    function setWithdrawer(address _withdrawer) public onlyOwner {

69: 		    function setOperator(address _operator, bool _active) public onlyOwner {

79: 		    function setVault(address _vault, bool _active) public onlyOwner {

87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {
```

*GitHub* : [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L59), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L69), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L79), [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87)

```solidity
File: src/transformers/AutoCompound.sol

243: 		    function setReward(uint64 _totalRewardX64) external onlyOwner {
```

*GitHub* : [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L243)

### [L-32]<a name="l-32"></a> Missing checks for `address(0)` in constructor/initializers

Check for zero-address to avoid the risk of setting `address(0)` for state variables when deploying.

*There are 12 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit _nonfungiblePositionManager
79: 		        nonfungiblePositionManager = _nonfungiblePositionManager;

// @audit _referenceToken
81: 		        referenceToken = _referenceToken;

// @audit _chainlinkReferenceToken
83: 		        chainlinkReferenceToken = _chainlinkReferenceToken;
```

*GitHub* : [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L79), [81](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L81), [83](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L83)

```solidity
File: src/V3Vault.sol

// @audit _asset
178: 		        asset = _asset;

// @audit _nonfungiblePositionManager
180: 		        nonfungiblePositionManager = _nonfungiblePositionManager;

// @audit _interestRateModel
182: 		        interestRateModel = _interestRateModel;

// @audit _oracle
183: 		        oracle = _oracle;

// @audit _permit2
184: 		        permit2 = _permit2;
```

*GitHub* : [178](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L178), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L180), [182](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L182), [183](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L183), [184](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L184)

```solidity
File: src/transformers/V3Utils.sol

// @audit _permit2
37: 		        permit2 = IPermit2(_permit2);
```

*GitHub* : [37](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L37)

```solidity
File: src/utils/Swapper.sol

// @audit _nonfungiblePositionManager
42: 		        weth = IWETH9(_nonfungiblePositionManager.WETH9());

// @audit _zeroxRouter
45: 		        zeroxRouter = _zeroxRouter;

// @audit _universalRouter
46: 		        universalRouter = _universalRouter;
```

*GitHub* : [42](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L42), [45](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L45), [46](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L46)

### [L-33]<a name="l-33"></a> Missing checks for `address(0)` when updating state variables

Check for zero-address to avoid the risk of setting `address(0)` for state variables after an update.

*There are 16 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit token
240: 		        feedConfigs[token] = config;

// @audit feed
240: 		        feedConfigs[token] = config;

// @audit admin
266: 		        emergencyAdmin = admin;
```

*GitHub* : [240](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L240), [240](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L240), [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L266)

```solidity
File: src/V3Vault.sol

// @audit target
487: 		        transformApprovals[msg.sender][tokenId][target] = isActive;

// @audit admin
871: 		        emergencyAdmin = admin;

// @audit to
1298: 		        ownedTokensIndex[tokenId] = ownedTokens[to].length;

// @audit from
1308: 		            ownedTokens[from][tokenIndex] = lastTokenId;
```

*GitHub* : [487](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L487), [871](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L871), [1298](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1298), [1308](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1308)

```solidity
File: src/automators/AutoExit.sol

// @audit config
230: 		        positionConfigs[tokenId] = config;
```

*GitHub* : [230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L230)

```solidity
File: src/automators/Automator.sol

// @audit _withdrawer
61: 		        withdrawer = _withdrawer;

// @audit _operator
71: 		        operators[_operator] = _active;

// @audit _vault
81: 		        vaults[_vault] = _active;
```

*GitHub* : [61](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L61), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L71), [81](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L81)

```solidity
File: src/transformers/AutoCompound.sol

// @audit token
250: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] + amount;

// @audit token
257: 		            positionBalances[tokenId][token] = amount;

// @audit token
270: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] - amount;

// @audit to
270: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] - amount;
```

*GitHub* : [250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L250), [257](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L257), [270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L270), [270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L270)

```solidity
File: src/transformers/AutoRange.sol

// @audit config
284: 		        positionConfigs[tokenId] = config;
```

*GitHub* : [284](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L284)

### Gas Risk Issues

### [G-01]<a name="g-01"></a> Use `Array.unsafeAccess` to avoid repeated array length checks

When using storage arrays, solidity adds an internal lookup of the array's length (a **Gcoldsload 2100 gas**) to ensure it doesn't read past the array's end.

It's possible to avoid this lookup by using `Array.unsafeAccess` in cases where the length has already been checked.

*There are 4 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

112: 		            uint256 balance = IERC20(tokens[i]).balanceOf(address(this));

114: 		                _transferToken(to, IERC20(tokens[i]), balance, true);
```

*GitHub* : [112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L112), [114](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L114)

```solidity
File: src/transformers/AutoCompound.sol

234: 		            uint256 balance = positionBalances[0][tokens[i]];

235: 		            _withdrawBalanceInternal(0, tokens[i], to, balance, balance);
```

*GitHub* : [234](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L234), [235](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L235)

### [G-02]<a name="g-02"></a> State variables can be packed into fewer storage slots

Each slot saved can avoid an extra Gsset (**20000 gas**). Reads and writes (if two variables that occupy the same slot are written by the same function) will have a cheaper gas consumption.

*There are 1 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit Can save 1 storage slot (from 23 to 22) 
// @audit Consider using the following order:
/*
  *	mapping(address => TokenConfig) tokenConfigs (32)
  *	uint256 debtSharesTotal (32)
  *	uint256 lastExchangeRateUpdate (32)
  *	uint256 lastDebtExchangeRateX96 (32)
  *	uint256 lastLendExchangeRateX96 (32)
  *	uint256 globalDebtLimit (32)
  *	uint256 globalLendLimit (32)
  *	uint256 minLoanSize (32)
  *	uint256 dailyLendIncreaseLimitMin (32)
  *	uint256 dailyLendIncreaseLimitLeft (32)
  *	uint256 dailyLendIncreaseLimitLastReset (32)
  *	uint256 dailyDebtIncreaseLimitMin (32)
  *	uint256 dailyDebtIncreaseLimitLeft (32)
  *	uint256 dailyDebtIncreaseLimitLastReset (32)
  *	mapping(uint256 => Loan) loans (32)
  *	mapping(address => uint256[]) ownedTokens (32)
  *	mapping(uint256 => uint256) ownedTokensIndex (32)
  *	mapping(uint256 => address) tokenOwner (32)
  *	uint256 transformedTokenId (32)
  *	mapping(address => bool) transformerAllowList (32)
  *	mapping(address => mapping(uint256 => mapping(address => bool))) transformApprovals (32)
  *	address emergencyAdmin (20)
  *	uint32 reserveFactorX32 (4)
  *	uint32 reserveProtectionFactorX32 (4)
*/
30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

### [G-03]<a name="g-03"></a> Structs can be packed into fewer storage slots

Each slot saved can avoid an extra Gsset (**20000 gas**) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings.

*There are 3 instance(s) of this issue:*

```solidity
File: src/automators/AutoExit.sol

// @audit Can save 1 storage slot (from 7 to 6) 
// @audit Consider using the following order:
/*
  *	uint256 tokenId (32)
  *	bytes swapData (32)
  *	uint256 amountRemoveMin0 (32)
  *	uint256 amountRemoveMin1 (32)
  *	uint256 deadline (32)
  *	uint128 liquidity (16)
  *	uint64 rewardX64 (8)
*/
63: 		    struct ExecuteParams {
64: 		        uint256 tokenId; // tokenid to process
65: 		        bytes swapData; // if its a swap order - must include swap data
66: 		        uint128 liquidity; // liquidity the calculations are based on
67: 		        uint256 amountRemoveMin0; // min amount to be removed from liquidity
68: 		        uint256 amountRemoveMin1; // min amount to be removed from liquidity
69: 		        uint256 deadline; // for uniswap operations - operator promises fair value
70: 		        uint64 rewardX64; // which reward will be used for protocol, can be max configured amount (considering onlyFees)
71: 		    }
```

*GitHub* : [63-71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L63-L71)

```solidity
File: src/transformers/AutoRange.sol

// @audit Can save 2 storage slots (from 9 to 7) 
// @audit Consider using the following order:
/*
  *	uint256 tokenId (32)
  *	uint256 amountIn (32)
  *	bytes swapData (32)
  *	uint256 amountRemoveMin0 (32)
  *	uint256 amountRemoveMin1 (32)
  *	uint256 deadline (32)
  *	uint128 liquidity (16)
  *	uint64 rewardX64 (8)
  *	bool swap0To1 (1)
*/
53: 		    struct ExecuteParams {
54: 		        uint256 tokenId;
55: 		        bool swap0To1;
56: 		        uint256 amountIn; // if this is set to 0 no swap happens
57: 		        bytes swapData;
58: 		        uint128 liquidity; // liquidity the calculations are based on
59: 		        uint256 amountRemoveMin0; // min amount to be removed from liquidity
60: 		        uint256 amountRemoveMin1; // min amount to be removed from liquidity
61: 		        uint256 deadline; // for uniswap operations - operator promises fair value
62: 		        uint64 rewardX64; // which reward will be used for protocol, can be max configured amount (considering onlyFees)
63: 		    }
```

*GitHub* : [53-63](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L53-L63)

```solidity
File: src/transformers/V3Utils.sol

// @audit Can save 1 storage slot (from 8 to 7) 
// @audit Consider using the following order:
/*
  *	uint256 amountIn (32)
  *	uint256 minAmountOut (32)
  *	bytes swapData (32)
  *	bytes permitData (32)
  *	IERC20 tokenIn (20)
  *	bool unwrap (1)
  *	IERC20 tokenOut (20)
  *	address recipient (20)
*/
382: 		    struct SwapParams {
383: 		        IERC20 tokenIn;
384: 		        IERC20 tokenOut;
385: 		        uint256 amountIn;
386: 		        uint256 minAmountOut;
387: 		        address recipient; // recipient of tokenOut and leftover tokenIn (if any leftover)
388: 		        bytes swapData;
389: 		        bool unwrap; // if tokenIn or tokenOut is WETH - unwrap
390: 		        bytes permitData; // if permit2 signatures are used - set this
391: 		    }
```

*GitHub* : [382-391](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L382-L391)

### [G-04]<a name="g-04"></a> Multiple `mapping`s that share an ID can be combined into a single `mapping` of ID / `struct`

This can avoid a Gsset (**20000 Gas**) per mapping combined. Reads and writes will also be cheaper when a function requires both values as they both can fit in the same storage slot.

Finally, if both fields are accessed in the same function, this can save **~42 gas** per access due to not having to recalculate the key's `keccak256` hash (Gkeccak256 - **30 Gas**) and that calculation's associated stack operations.

*There are 2 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit consider merging ownedTokensIndex, tokenOwner
158: 		    mapping(uint256 => uint256) private ownedTokensIndex; // Mapping from token ID to index of the owner tokens list (for removal without loop)
159: 		    mapping(uint256 => address) private tokenOwner; // Mapping from token ID to owner

// @audit consider merging transformerAllowList, transformApprovals
163: 		    mapping(address => bool) public transformerAllowList; // contracts allowed to transform positions (selected audited contracts e.g. V3Utils)
164: 		    mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)
```

*GitHub* : [163](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L163), [158](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L158)

### [G-05]<a name="g-05"></a> Use of `memory` instead of `storage` for struct/array state variables

When fetching data from `storage`, using the `memory` keyword to assign it to a variable reads all fields of the struct/array and incurs a Gcoldsload (**2100 gas**) for each field.

This can be avoided by declaring the variable with the `storage` keyword and caching the necessary fields in stack variables.

The `memory` keyword should only be used if the entire struct/array is being returned or passed to a function that requires `memory`, or if it is being read from another `memory` array/struct.

*There are 3 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

334: 		        TokenConfig memory feedConfig = feedConfigs[token];
```

*GitHub* : [334](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L334)

```solidity
File: src/automators/AutoExit.sol

106: 		        PositionConfig memory config = positionConfigs[params.tokenId];
```

*GitHub* : [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L106)

```solidity
File: src/transformers/AutoRange.sol

116: 		        PositionConfig memory config = positionConfigs[params.tokenId];
```

*GitHub* : [116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L116)

### [G-06]<a name="g-06"></a> Cache state variables with stack variables

Caching of a state variable replaces each Gwarmaccess (**100 gas**) with a cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses.

*There are 9 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit kinkX96 on lines 66, 69
70: 		            uint256 excessUtilX96 = utilizationRateX96 - kinkX96;

// @audit baseRatePerSecondX96 on line 67
69: 		            uint256 normalRateX96 = (kinkX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

// @audit multiplierPerSecondX96 on line 67
69: 		            uint256 normalRateX96 = (kinkX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;
```

*GitHub* : [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L70), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L69), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L69)

```solidity
File: src/V3Vault.sol

// @audit globalLendLimit on line 304
307: 		            return globalLendLimit - value;

// @audit globalLendLimit on line 315
318: 		            return _convertToShares(globalLendLimit - value, lendExchangeRateX96, Math.Rounding.Down);

// @audit transformedTokenId on line 505
528: 		        tokenId = transformedTokenId;

// @audit debtSharesTotal on line 569
571: 		        if (debtSharesTotal > _convertToShares(globalDebtLimit, newDebtExchangeRateX96, Math.Rounding.Down)) {

// @audit dailyDebtIncreaseLimitLeft on line 574
577: 		            dailyDebtIncreaseLimitLeft -= assets;

// @audit dailyLendIncreaseLimitLeft on line 910
913: 		            dailyLendIncreaseLimitLeft -= assets;
```

*GitHub* : [318](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L318), [307](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L307), [528](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L528), [571](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L571), [577](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L577), [913](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L913)

### [G-07]<a name="g-07"></a> Avoid contract existence checks by using low level calls

Prior to Solidity 0.8.10 the compiler inserted extra code, including EXTCODESIZE (**100 gas**), to check for contract existence for external function calls.

In more recent solidity versions, the compiler will not insert these checks if the external call has a return value.

A similar behavior can be achieved in earlier versions by using low - level calls, since low level calls never check for contract existence.

*There are 116 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

82: 		        referenceTokenDecimals = IERC20Metadata(_referenceToken).decimals();

215: 		        uint8 feedDecimals = feed.decimals();

216: 		        uint8 tokenDecimals = IERC20Metadata(token).decimals();

225: 		            address token0 = pool.token0();

226: 		            address token1 = pool.token1();

363: 		            (sqrtPriceX96,,,,,,) = pool.slot0();

368: 		            (int56[] memory tickCumulatives,) = pool.observe(secondsAgos); // pool observe may fail when there is not enough history available (only use pool with enough history!)

409: 		        ) = nonfungiblePositionManager.positions(tokenId);

480: 		        (,, uint256 lowerFeeGrowthOutside0X128, uint256 lowerFeeGrowthOutside1X128,,,,) = pool.ticks(tickLower);

481: 		        (,, uint256 upperFeeGrowthOutside0X128, uint256 upperFeeGrowthOutside1X128,,,,) = pool.ticks(tickUpper);
```

*GitHub* : [82](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L82), [215](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L215), [368](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L368), [216](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L216), [480](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L480), [481](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L481), [409](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L409), [363](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L363), [226](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L226), [225](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L225)

```solidity
File: src/V3Vault.sol

179: 		        assetDecimals = IERC20Metadata(_asset).decimals();

285: 		        return IERC20(asset).balanceOf(address(this));

401: 		        nonfungiblePositionManager.safeTransferFrom(msg.sender, address(this), tokenId, abi.encode(recipient));

423: 		        nonfungiblePositionManager.permit(address(this), tokenId, deadline, v, r, s);

424: 		        nonfungiblePositionManager.safeTransferFrom(owner, address(this), tokenId, abi.encode(recipient));

444: 		                owner = abi.decode(data, (address));

520: 		        nonfungiblePositionManager.approve(transformer, tokenId);

522: 		        (bool success,) = transformer.call(data);

531: 		        address owner = nonfungiblePositionManager.ownerOf(tokenId);

537: 		        nonfungiblePositionManager.approve(address(0), tokenId);

627: 		        (amount0, amount1) = nonfungiblePositionManager.decreaseLiquidity(
628: 		            INonfungiblePositionManager.DecreaseLiquidityParams(
629: 		                params.tokenId, params.liquidity, params.amount0Min, params.amount1Min, params.deadline
630: 		            )
631: 		        );

640: 		        (amount0, amount1) = nonfungiblePositionManager.collect(collectParams);

719: 		                abi.decode(params.permitData, (ISignatureTransfer.PermitTransferFrom, bytes));

720: 		            permit2.permitTransferFrom(
721: 		                permit,
722: 		                ISignatureTransfer.SignatureTransferDetails(address(this), state.liquidatorCost),
723: 		                msg.sender,
724: 		                signature
725: 		            );

895: 		                abi.decode(permitData, (ISignatureTransfer.PermitTransferFrom, bytes));

896: 		            permit2.permitTransferFrom(
897: 		                permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature
898: 		            );

980: 		                    abi.decode(permitData, (ISignatureTransfer.PermitTransferFrom, bytes));

981: 		                permit2.permitTransferFrom(
982: 		                    permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature
983: 		                );

1045: 		            (,,,,,,, liquidity,,,,) = nonfungiblePositionManager.positions(tokenId);

1049: 		            (,,, liquidity,,, fees0, fees1) = oracle.getPositionBreakdown(tokenId);

1065: 		            nonfungiblePositionManager.decreaseLiquidity(
1066: 		                INonfungiblePositionManager.DecreaseLiquidityParams(tokenId, liquidity, 0, 0, block.timestamp)
1067: 		            );

1070: 		        (amount0, amount1) = nonfungiblePositionManager.collect(
1071: 		            INonfungiblePositionManager.CollectParams(tokenId, recipient, fees0, fees1)
1072: 		        );

1083: 		        nonfungiblePositionManager.safeTransferFrom(address(this), owner, tokenId);

1144: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(tokenId);

1179: 		        (uint256 borrowRateX96, uint256 supplyRateX96) = interestRateModel.getRatesPerSecondX96(available, debt);

1213: 		            (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(tokenId);

1275: 		        (fullValue, feeValue,,) = oracle.getValue(tokenId, address(asset));

1299: 		        ownedTokens[to].push(tokenId);

1311: 		        ownedTokens[from].pop();
```

*GitHub* : [537](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L537), [627-631](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L627-L631), [640](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L640), [719](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L719), [720-725](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L720-L725), [895](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L895), [896-898](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L896-L898), [980](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L980), [981-983](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L981-L983), [1045](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1045), [1049](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1049), [1065-1067](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1065-L1067), [1070-1072](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1070-L1072), [1083](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1083), [1144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1144), [1213](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1213), [1275](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1275), [1299](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1299), [1311](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1311), [1179](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1179), [179](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L179), [285](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L285), [401](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L401), [423](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L423), [424](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L424), [444](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L444), [520](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L520), [522](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L522), [531](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L531)

```solidity
File: src/automators/AutoExit.sol

121: 		            nonfungiblePositionManager.positions(params.tokenId);

198: 		        state.owner = nonfungiblePositionManager.ownerOf(params.tokenId);

219: 		        address owner = nonfungiblePositionManager.ownerOf(tokenId);
```

*GitHub* : [219](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L219), [198](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L198), [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L121)

```solidity
File: src/automators/Automator.sol

112: 		            uint256 balance = IERC20(tokens[i]).balanceOf(address(this));

148: 		        (sqrtPriceX96, currentTick,,,,,) = pool.slot0();

186: 		        try pool.observe(secondsAgos) returns (int56[] memory tickCumulatives, uint160[] memory) {

202: 		            (feeAmount0, feeAmount1) = nonfungiblePositionManager.decreaseLiquidity(
203: 		                INonfungiblePositionManager.DecreaseLiquidityParams(
204: 		                    tokenId, liquidity, amountRemoveMin0, amountRemoveMin1, deadline
205: 		                )
206: 		            );

208: 		        (amount0, amount1) = nonfungiblePositionManager.collect(
209: 		            INonfungiblePositionManager.CollectParams(tokenId, address(this), type(uint128).max, type(uint128).max)
210: 		        );

220: 		            weth.withdraw(amount);

240: 		            owner = IVault(vault).ownerOf(tokenId);

242: 		            owner = nonfungiblePositionManager.ownerOf(tokenId);
```

*GitHub* : [112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L112), [148](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L148), [186](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L186), [202-206](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L202-L206), [208-210](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L208-L210), [220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L220), [240](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L240), [242](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L242)

```solidity
File: src/transformers/AutoCompound.sol

91: 		        IVault(vault).transform(
92: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoCompound.execute.selector, params)
93: 		        );

92: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoCompound.execute.selector, params)

108: 		        (state.amount0, state.amount1) = nonfungiblePositionManager.collect(
109: 		            INonfungiblePositionManager.CollectParams(
110: 		                params.tokenId, address(this), type(uint128).max, type(uint128).max
111: 		            )
112: 		        );

116: 		            nonfungiblePositionManager.positions(params.tokenId);

129: 		                (state.sqrtPriceX96, state.tick,,,,,) = pool.slot0();

163: 		                (, state.compounded0, state.compounded1) = nonfungiblePositionManager.increaseLiquidity(
164: 		                    INonfungiblePositionManager.IncreaseLiquidityParams(
165: 		                        params.tokenId, state.maxAddAmount0, state.maxAddAmount1, 0, 0, block.timestamp
166: 		                    )
167: 		                );

201: 		        address owner = nonfungiblePositionManager.ownerOf(tokenId);

203: 		            owner = IVault(owner).ownerOf(tokenId);

209: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(tokenId);

278: 		        uint256 allowance0 = IERC20(token0).allowance(address(this), address(nonfungiblePositionManager));

282: 		        uint256 allowance1 = IERC20(token1).allowance(address(this), address(nonfungiblePositionManager));
```

*GitHub* : [116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L116), [129](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L129), [163-167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L163-L167), [201](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L201), [203](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L203), [209](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L209), [278](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L278), [282](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L282), [108-112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L108-L112), [92](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L92), [91-93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L91-L93)

```solidity
File: src/transformers/AutoRange.sol

101: 		        IVault(vault).transform(
102: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoRange.execute.selector, params)
103: 		        );

102: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoRange.execute.selector, params)

131: 		            nonfungiblePositionManager.positions(params.tokenId);

217: 		            (state.newTokenId,, state.amountAdded0, state.amountAdded1) = nonfungiblePositionManager.mint(mintParams);

223: 		            state.owner = nonfungiblePositionManager.ownerOf(params.tokenId);

228: 		                state.realOwner = IVault(state.owner).ownerOf(params.tokenId);

232: 		            nonfungiblePositionManager.safeTransferFrom(address(this), state.owner, state.newTokenId);

308: 		            int24 spacing = IUniswapV3Factory(factory).feeAmountTickSpacing(fee);
```

*GitHub* : [217](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L217), [223](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L223), [228](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L228), [232](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L232), [308](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L308), [101-103](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L101-L103), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L102), [131](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L131)

```solidity
File: src/transformers/LeverageTransformer.sol

43: 		        address token = IVault(msg.sender).asset();

45: 		        IVault(msg.sender).borrow(params.tokenId, amount);

47: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(params.tokenId);

84: 		        (, uint256 added0, uint256 added1) = nonfungiblePositionManager.increaseLiquidity(increaseLiquidityParams);

124: 		        address token = IVault(msg.sender).asset();

125: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(params.tokenId);

134: 		        (amount0, amount1) = nonfungiblePositionManager.decreaseLiquidity(decreaseLiquidityParams);

142: 		        (amount0, amount1) = nonfungiblePositionManager.collect(collectParams);

166: 		        IVault(msg.sender).repay(params.tokenId, amount, false);
```

*GitHub* : [84](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L84), [124](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L124), [125](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L125), [134](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L134), [142](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L142), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L166), [43](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L43), [45](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L45), [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L47)

```solidity
File: src/transformers/V3Utils.sol

102: 		        if (nonfungiblePositionManager.ownerOf(tokenId) != msg.sender) {

106: 		        nonfungiblePositionManager.permit(address(this), tokenId, instructions.deadline, v, r, s);

116: 		        (,, address token0, address token1,,,, uint128 liquidity,,,,) = nonfungiblePositionManager.positions(tokenId);

371: 		        Instructions memory instructions = abi.decode(data, (Instructions));

376: 		        nonfungiblePositionManager.safeTransferFrom(address(this), from, tokenId, instructions.returnData);

404: 		                abi.decode(params.permitData, (ISignatureTransfer.PermitBatchTransferFrom, bytes));

478: 		                abi.decode(params.permitData, (ISignatureTransfer.PermitBatchTransferFrom, bytes));

537: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(params.tokenId);

541: 		                abi.decode(params.permitData, (ISignatureTransfer.PermitBatchTransferFrom, bytes));

618: 		            state.balanceBefore0 = token0.balanceOf(address(this));

622: 		            state.balanceBefore1 = token1.balanceOf(address(this));

626: 		            state.balanceBeforeOther = otherToken.balanceOf(address(this));

631: 		        permit2.permitTransferFrom(permit, transferDetails, msg.sender, signature);

635: 		            if (token0.balanceOf(address(this)) - state.balanceBefore0 != state.needed0) {

640: 		            if (token1.balanceOf(address(this)) - state.balanceBefore1 != state.needed1) {

645: 		            if (otherToken.balanceOf(address(this)) - state.balanceBeforeOther != state.neededOther) {

726: 		        (tokenId, liquidity, added0, added1) = nonfungiblePositionManager.mint(mintParams);

727: 		        nonfungiblePositionManager.safeTransferFrom(address(this), params.recipientNFT, tokenId, params.returnData);

771: 		        (liquidity, added0, added1) = nonfungiblePositionManager.increaseLiquidity(increaseLiquidityParams);

866: 		            weth.withdraw(amount);

885: 		            (amount0, amount1) = nonfungiblePositionManager.decreaseLiquidity(
886: 		                INonfungiblePositionManager.DecreaseLiquidityParams(tokenId, liquidity, token0Min, token1Min, deadline)
887: 		            );

896: 		        uint256 balanceBefore0 = token0.balanceOf(address(this));

897: 		        uint256 balanceBefore1 = token1.balanceOf(address(this));

898: 		        (amount0, amount1) = nonfungiblePositionManager.collect(
899: 		            INonfungiblePositionManager.CollectParams(tokenId, address(this), collectAmount0, collectAmount1)
900: 		        );

901: 		        uint256 balanceAfter0 = token0.balanceOf(address(this));

902: 		        uint256 balanceAfter1 = token1.balanceOf(address(this));
```

*GitHub* : [376](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L376), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L102), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L106), [116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L116), [371](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L371), [404](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L404), [478](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L478), [537](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L537), [541](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L541), [618](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L618), [622](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L622), [626](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L626), [631](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L631), [635](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L635), [640](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L640), [645](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L645), [726](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L726), [727](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L727), [771](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L771), [866](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L866), [885-887](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L885-L887), [896](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L896), [897](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L897), [898-900](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L898-L900), [901](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L901), [902](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L902)

```solidity
File: src/utils/FlashloanLiquidator.sol

47: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(params.tokenId);

51: 		        bytes memory data = abi.encode(
52: 		            FlashCallbackData(
53: 		                params.tokenId,
54: 		                params.debtShares,
55: 		                liquidationCost,
56: 		                params.vault,
57: 		                IERC20(asset),
58: 		                RouterSwapParams(IERC20(token0), IERC20(asset), params.amount0In, 0, params.swapData0),
59: 		                RouterSwapParams(IERC20(token1), IERC20(asset), params.amount1In, 0, params.swapData1),
60: 		                msg.sender,
61: 		                params.minReward
62: 		            )
63: 		        );

70: 		        FlashCallbackData memory data = abi.decode(callbackData, (FlashCallbackData));

89: 		            uint256 balance = data.swap0.tokenIn.balanceOf(address(this));

95: 		            uint256 balance = data.swap1.tokenIn.balanceOf(address(this));
```

*GitHub* : [89](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L89), [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L70), [51-63](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L51-L63), [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L95), [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L47)

```solidity
File: src/utils/Swapper.sol

82: 		            (address router, bytes memory routerData) = abi.decode(params.swapData, (address, bytes));

85: 		                ZeroxRouterData memory data = abi.decode(routerData, (ZeroxRouterData));

89: 		                (bool success,) = zeroxRouter.call(data.data);

96: 		                UniversalRouterData memory data = abi.decode(routerData, (UniversalRouterData));

99: 		                IUniversalRouter(universalRouter).execute(data.commands, data.inputs, data.deadline);

139: 		                abi.encode(
140: 		                    params.swap0For1 ? params.token0 : params.token1,
141: 		                    params.swap0For1 ? params.token1 : params.token0,
142: 		                    params.fee
143: 		                )

160: 		        (address tokenIn, address tokenOut, uint24 fee) = abi.decode(data, (address, address, uint24));
```

*GitHub* : [96](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L96), [82](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L82), [99](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L99), [139-143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L139-L143), [160](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L160), [89](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L89), [85](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L85)

### [G-08]<a name="g-08"></a> Low level `call` can be optimized with assembly

`returnData` is copied to memory even if the variable is not utilized: the proper way to handle this is through a low level assembly call.

```solidity
// before
(bool success,) = payable(receiver).call{gas: gas, value: value}("");

//after
bool success;
assembly {
    success := call(gas, receiver, value, 0, 0, 0, 0)
}
```

*There are 5 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

522: 		        (bool success,) = transformer.call(data);
```

*GitHub* : [522](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L522)

```solidity
File: src/automators/Automator.sol

130: 		            (bool sent,) = to.call{value: balance}("");

221: 		            (bool sent,) = to.call{value: amount}("");
```

*GitHub* : [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L221), [130](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L130)

```solidity
File: src/transformers/V3Utils.sol

867: 		            (bool sent,) = to.call{value: amount}("");
```

*GitHub* : [867](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L867)

```solidity
File: src/utils/Swapper.sol

89: 		                (bool success,) = zeroxRouter.call(data.data);
```

*GitHub* : [89](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L89)

### [G-09]<a name="g-09"></a> Use at least Solidity version `0.8.19` to gain some gas boost

Upgrade to at least solidity version 0.8.19 to get additional gas savings. Check the [documentation](https://blog.soliditylang.org/2023/02/22/solidity-0.8.19-release-announcement/) for reference.

Some additional details:
> In earlier releases and in the default legacy code generation, when an internal library function or a free function accessed via a module was called only during contract creation, e.g. only in the constructor, a copy of the function still also occurred in the contract’s runtime bytecode.
>
>So a function pointer in creation code also refers to the offset of the function in runtime code, which requires the function to actually be present in runtime code.
>
>For direct calls to internal contract functions the full encoding of the function expression is bypassed by the compiler. However, this bypassing did not happen for internal library functions and for free functions called via modules, causing the undesirable behaviour that is now fixed in this release.

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L2)

```solidity
File: src/V3Oracle.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L2)

```solidity
File: src/V3Vault.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L2)

```solidity
File: src/automators/AutoExit.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L2)

```solidity
File: src/automators/Automator.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L2)

```solidity
File: src/transformers/AutoCompound.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L2)

```solidity
File: src/transformers/AutoRange.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L2)

```solidity
File: src/transformers/LeverageTransformer.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L2)

```solidity
File: src/transformers/V3Utils.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L2)

```solidity
File: src/utils/FlashloanLiquidator.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L2)

```solidity
File: src/utils/Swapper.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L2)

### [G-10]<a name="g-10"></a> Use of `memory` instead of `calldata` for immutable arguments

Consider refactoring the function arguments from `memory` to `calldata` when they are immutable, as `calldata` is cheaper.

*There are 8 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit feedConfig
346: 		    function _getTWAPPriceX96(TokenConfig memory feedConfig) internal view returns (uint256 poolTWAPPriceX96) {

// @audit position
445: 		    function _getUncollectedFees(PositionState memory position, int24 tick)
```

*GitHub* : [445](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L445), [346](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L346)

```solidity
File: src/V3Vault.sol

// @audit permitData
877: 		    function _deposit(address receiver, uint256 amount, bool isShare, bytes memory permitData)

// @audit permitData
954: 		    function _repay(uint256 tokenId, uint256 amount, bool isShare, bytes memory permitData) internal {
```

*GitHub* : [954](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L954), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L877)

```solidity
File: src/transformers/V3Utils.sol

// @audit instructions
115: 		    function execute(uint256 tokenId, Instructions memory instructions) public returns (uint256 newTokenId) {

// @audit signature
598: 		    function _prepareAddPermit2(
599: 		        IERC20 token0,
600: 		        IERC20 token1,
601: 		        IERC20 otherToken,
602: 		        uint256 amount0,
603: 		        uint256 amount1,
604: 		        uint256 amountOther,
605: 		        IPermit2.PermitBatchTransferFrom memory permit,
606: 		        bytes memory signature

// @audit params
735: 		    function _swapAndIncrease(SwapAndIncreaseLiquidityParams memory params, IERC20 token0, IERC20 token1, bool unwrap)

// @audit params
779: 		    function _swapAndPrepareAmounts(SwapAndMintParams memory params, bool unwrap)
```

*GitHub* : [779](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L779), [115](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L115), [598-606](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L598-L606), [735](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L735)

### [G-11]<a name="g-11"></a> Avoid updating storage when the value hasn't changed

If the old value is equal to the new value, not re-storing the value will avoid a Gsreset (**2900 gas**), potentially at the expense of a Gcoldsload (**2100 gas**) or a Gwarmaccess (**100 gas**)

*There are 16 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit baseRatePerSecondX96, multiplierPerSecondX96, jumpMultiplierPerSecondX96, kinkX96
82: 		    function setValues(
```

*GitHub* : [82](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L82)

```solidity
File: src/V3Oracle.sol

// @audit maxPoolPriceDifference
185: 		    function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

// @audit feedConfigs
201: 		    function setTokenConfig(

// @audit emergencyAdmin
265: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L265), [185](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L185), [201](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L201)

```solidity
File: src/V3Vault.sol

// @audit transformerAllowList
788: 		    function setTransformer(address transformer, bool active) external onlyOwner {

// @audit minLoanSize, globalLendLimit, globalDebtLimit, dailyLendIncreaseLimitMin, dailyDebtIncreaseLimitMin
807: 		    function setLimits(

// @audit reserveFactorX32
837: 		    function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

// @audit reserveProtectionFactorX32
844: 		    function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

// @audit emergencyAdmin
870: 		    function setEmergencyAdmin(address admin) external onlyOwner {

// @audit lastDebtExchangeRateX96, lastLendExchangeRateX96, lastExchangeRateUpdate
1150: 		    function _updateGlobalInterest()
```

*GitHub* : [807](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L807), [788](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L788), [837](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L837), [844](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L844), [870](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L870), [1150](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1150)

```solidity
File: src/automators/Automator.sol

// @audit withdrawer
59: 		    function setWithdrawer(address _withdrawer) public onlyOwner {

// @audit operators
69: 		    function setOperator(address _operator, bool _active) public onlyOwner {

// @audit vaults
79: 		    function setVault(address _vault, bool _active) public onlyOwner {

// @audit TWAPSeconds, maxTWAPTickDifference
87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L79), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L69), [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L59)

```solidity
File: src/transformers/AutoCompound.sol

// @audit totalRewardX64
243: 		    function setReward(uint64 _totalRewardX64) external onlyOwner {

// @audit positionBalances
254: 		    function _setBalance(uint256 tokenId, address token, uint256 amount) internal {
```

*GitHub* : [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L243), [254](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L254)

### [G-12]<a name="g-12"></a> Use `uint256(1)/uint256(2)` instead of `true/false` to save gas for changes

Use `uint256(1)` and `uint256(2)` for `true`/`false` to avoid a Gsset (20000 gas) when changing from `false` to `true`, after having been `true` in the past. See [source](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27).

*There are 4 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

163: 		    mapping(address => bool) public transformerAllowList; // contracts allowed to transform positions (selected audited contracts e.g. V3Utils)

164: 		    mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)
```

*GitHub* : [164](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L164), [163](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L163)

```solidity
File: src/automators/Automator.sol

34: 		    mapping(address => bool) public operators;

35: 		    mapping(address => bool) public vaults;
```

*GitHub* : [35](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L35), [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L34)

### [G-13]<a name="g-13"></a> Shortcircuit rules can be be used to optimize some gas usage

Some conditions may be reordered to save an `SLOAD` (**2100 gas**), as we avoid reading state variables when the first part of the condition fails (with `&&`), or succeeds (with `||`).

*There are 2 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit switch with this condition
// from == address(this) || msg.sender != address(nonfungiblePositionManager)
435: 		        if (msg.sender != address(nonfungiblePositionManager) || from == address(this)) {

// @audit switch with this condition
// address(this) != msg.sender && !isTransformMode && tokenOwner[tokenId] != msg.sender
561: 		        if (!isTransformMode && tokenOwner[tokenId] != msg.sender && address(this) != msg.sender) {
```

*GitHub* : [561](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L561), [435](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L435)

### [G-14]<a name="g-14"></a> Cache multiple accesses of a mapping/array

Consider using a local `storage` or `calldata` variable when accessing a mapping/array value multiple times.

This can be useful to avoid recalculating the mapping hash and/or the array offsets.

*There are 15 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit transformApprovals[loanOwner] on line 515
515: 		        if (loanOwner != msg.sender && !transformApprovals[loanOwner][tokenId][msg.sender]) {

// @audit tokenConfigs on line 863
864: 		        tokenConfigs[token].collateralValueLimitFactorX32 = collateralValueLimitFactorX32;

// @audit loans on line 1081
1082: 		        delete loans[tokenId];

// @audit tokenConfigs on line 1145
1146: 		        uint32 factor1X32 = tokenConfigs[token1].collateralFactorX32;

// @audit tokenConfigs on lines 1217, 1218, 1220, 1221, 1226, 1229, 1234
1237: 		                        && _convertToAssets(tokenConfigs[token1].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)

// @audit ownedTokens on line 1298
1299: 		        ownedTokens[to].push(tokenId);

// @audit ownedTokens on lines 1304, 1307, 1308
1311: 		        ownedTokens[from].pop();
```

*GitHub* : [1146](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1146), [1237](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1237), [1299](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1299), [1311](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1311), [864](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L864), [515](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L515), [1082](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1082)

```solidity
File: src/automators/AutoExit.sol

// @audit positionConfigs on line 106
207: 		        delete positionConfigs[params.tokenId];
```

*GitHub* : [207](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L207)

```solidity
File: src/automators/Automator.sol

// @audit vaults on line 232
237: 		            if (!vaults[vault]) {
```

*GitHub* : [237](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L237)

```solidity
File: src/transformers/AutoCompound.sol

// @audit positionBalances[params.tokenId] on line 119
120: 		        state.amount1 = state.amount1 + positionBalances[params.tokenId][state.token1];

// @audit positionBalances[tokenId] on line 211
215: 		        uint256 balance1 = positionBalances[tokenId][token1];

// @audit positionBalances on line 250
250: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] + amount;

// @audit positionBalances on line 255
257: 		            positionBalances[tokenId][token] = amount;

// @audit positionBalances on line 270
270: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] - amount;
```

*GitHub* : [257](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L257), [270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L270), [215](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L215), [250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L250), [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L120)

```solidity
File: src/transformers/AutoRange.sol

// @audit positionConfigs on line 116
265: 		            delete positionConfigs[params.tokenId];
```

*GitHub* : [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L265)

### [G-15]<a name="g-15"></a> Using `private` for constants saves gas

Saves deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table.

*There are 13 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

13: 		    uint256 public constant YEAR_SECS = 31557600; // taking into account leap years

15: 		    uint256 public constant MAX_BASE_RATE_X96 = Q96 / 10; // 10%

16: 		    uint256 public constant MAX_MULTIPLIER_X96 = Q96 * 2; // 200%
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L16), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L13), [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L15)

```solidity
File: src/V3Oracle.sol

25: 		    uint16 public constant MIN_PRICE_DIFFERENCE = 200; //2%
```

*GitHub* : [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L25)

```solidity
File: src/V3Vault.sol

36: 		    uint32 public constant MAX_COLLATERAL_FACTOR_X32 = uint32(Q32 * 90 / 100); // 90%

38: 		    uint32 public constant MIN_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 2 / 100); // 2%

39: 		    uint32 public constant MAX_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 10 / 100); // 10%

41: 		    uint32 public constant MIN_RESERVE_PROTECTION_FACTOR_X32 = uint32(Q32 / 100); //1%

43: 		    uint32 public constant MAX_DAILY_LEND_INCREASE_X32 = uint32(Q32 / 10); //10%

44: 		    uint32 public constant MAX_DAILY_DEBT_INCREASE_X32 = uint32(Q32 / 10); //10%
```

*GitHub* : [36](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L36), [38](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L38), [39](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L39), [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L41), [43](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L43), [44](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L44)

```solidity
File: src/automators/Automator.sol

23: 		    uint32 public constant MIN_TWAP_SECONDS = 60; // 1 minute

24: 		    uint32 public constant MAX_TWAP_TICK_DIFFERENCE = 200; // 2%
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L24), [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L23)

```solidity
File: src/transformers/AutoCompound.sol

47: 		    uint64 public constant MAX_REWARD_X64 = uint64(Q64 / 50); // 2%
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L47)

### [G-16]<a name="g-16"></a> require() or revert() statements that check input arguments should be at the top of the function

Checks that can be performed earlier should come before checks that involve state variables, function calls, and calculations. By doing these checks first, the function is able to revert before wasting a Gcoldsload (*2100 gas*) in a function that may ultimately revert.

*There are 1 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

// @audit expensive op on line 233, 232
236: 		        if (vault != address(0)) {
```

*GitHub* : [236](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L236)

### [G-17]<a name="g-17"></a> Custom `error`s cost less than `require`/`assert`

Consider the use of a custom `error`, as it leads to a cheaper deploy cost and run time cost. The run time cost is only relevant when the revert condition is met.

*There are 3 instance(s) of this issue:*

```solidity
File: src/transformers/AutoCompound.sol

244: 		        require(_totalRewardX64 <= totalRewardX64, ">totalRewardX64");

269: 		        require(amount <= balance, "amount>balance");
```

*GitHub* : [269](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L269), [244](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L244)

```solidity
File: src/utils/Swapper.sol

157: 		        require(amount0Delta > 0 || amount1Delta > 0); // swaps entirely within 0-liquidity regions are not supported
```

*GitHub* : [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L157)

### [G-18]<a name="g-18"></a> Consider activating `via-ir` for deploying

The IR-based code generator was developed to make code generation more performant by enabling optimization passes that can be applied across functions.

It is possible to activate the IR-based code generator through the command line by using the flag `--via-ir` or by including the option `{"viaIR": true}`.

Keep in mind that compiling with this option may take longer. However, you can simply test it before deploying your code. If you find that it provides better performance, you can add the `--via-ir` flag to your deploy command.

*There are 0 instance(s) of this issue:*

```solidity
File: All in-scope files
```

### [G-19]<a name="g-19"></a> Functions that revert when called by normal users can be `payable`

If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function.

Marking the function as `payable` will lower the gas for legitimate callers, as the compiler will not include checks for whether a payment was provided.

The extra opcodes avoided are:

`CALLVALUE(2), DUP1(3), ISZERO(3), PUSH2(3), JUMPI(10), PUSH1(3), DUP1(3), REVERT(0), JUMPDEST(1), POP(2)`

which cost an average of about 21 gas per call to the function, in addition to the extra deployment cost.

*There are 15 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

82: 		    function setValues(
83: 		        uint256 baseRatePerYearX96,
84: 		        uint256 multiplierPerYearX96,
85: 		        uint256 jumpMultiplierPerYearX96,
86: 		        uint256 _kinkX96
87: 		    ) public onlyOwner {
```

*GitHub* : [82-87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L82-L87)

```solidity
File: src/V3Oracle.sol

185: 		    function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

201: 		    function setTokenConfig(
202: 		        address token,
203: 		        AggregatorV3Interface feed,
204: 		        uint32 maxFeedAge,
205: 		        IUniswapV3Pool pool,
206: 		        uint32 twapSeconds,
207: 		        Mode mode,
208: 		        uint16 maxDifference
209: 		    ) external onlyOwner {

265: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [185](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L185), [201-209](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L201-L209), [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L265)

```solidity
File: src/V3Vault.sol

765: 		    function withdrawReserves(uint256 amount, address receiver) external onlyOwner {

788: 		    function setTransformer(address transformer, bool active) external onlyOwner {

837: 		    function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

844: 		    function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

856: 		    function setTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32)
857: 		        external
858: 		        onlyOwner

870: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [856-858](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L856-L858), [870](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L870), [788](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L788), [837](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L837), [844](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L844), [765](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L765)

```solidity
File: src/automators/Automator.sol

59: 		    function setWithdrawer(address _withdrawer) public onlyOwner {

69: 		    function setOperator(address _operator, bool _active) public onlyOwner {

79: 		    function setVault(address _vault, bool _active) public onlyOwner {

87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {
```

*GitHub* : [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L59), [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L69), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L79)

```solidity
File: src/transformers/AutoCompound.sol

243: 		    function setReward(uint64 _totalRewardX64) external onlyOwner {
```

*GitHub* : [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L243)

### [G-20]<a name="g-20"></a> Add `unchecked` blocks for subtractions where the operands cannot underflow

There are some checks to avoid an underflow, so it's safe to use `unchecked` to have some gas savings.

*There are 19 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit check on line 66
70: 		            uint256 excessUtilX96 = utilizationRateX96 - kinkX96;
```

*GitHub* : [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L70)

```solidity
File: src/V3Vault.sol

// @audit check on line 304
307: 		            return globalLendLimit - value;

// @audit check on line 315
318: 		            return _convertToShares(globalLendLimit - value, lendExchangeRateX96, Math.Rounding.Down);

// @audit check on line 1052
1060: 		                liquidity = uint128((liquidationValue - feeValue) * liquidity / (fullValue - feeValue));

// @audit check on line 1103
1107: 		                (Q96 - ((fullValue - maxPenaltyValue) * Q96 / (startLiquidationValue - maxPenaltyValue)));

// @audit check on line 1131
1132: 		            missing = reserveCost - reserves;

// @audit check on line 1216
1217: 		                tokenConfigs[token0].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);

// @audit check on line 1216
1218: 		                tokenConfigs[token1].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);

// @audit check on line 1216
1220: 		                tokenConfigs[token0].totalDebtShares += SafeCast.toUint192(newShares - oldShares);

// @audit check on line 1216
1221: 		                tokenConfigs[token1].totalDebtShares += SafeCast.toUint192(newShares - oldShares);
```

*GitHub* : [1132](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1132), [1217](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1217), [1218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1218), [1220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1220), [1221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1221), [1107](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1107), [1060](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1060), [318](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L318), [307](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L307)

```solidity
File: src/transformers/AutoCompound.sol

// @audit check on line 258
259: 		                emit BalanceAdded(tokenId, token, amount - currentBalance);

// @audit check on line 258
261: 		                emit BalanceRemoved(tokenId, token, currentBalance - amount);
```

*GitHub* : [259](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L259), [261](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L261)

```solidity
File: src/transformers/LeverageTransformer.sol

// @audit check on line 87
88: 		            SafeERC20.safeTransfer(IERC20(token0), params.recipient, amount0 - added0);

// @audit check on line 90
91: 		            SafeERC20.safeTransfer(IERC20(token1), params.recipient, amount1 - added1);
```

*GitHub* : [88](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L88), [91](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L91)

```solidity
File: src/transformers/V3Utils.sol

// @audit check on line 316
317: 		                    _transferToken(instructions.recipient, IERC20(token0), amount0 - amountInDelta, instructions.unwrap);

// @audit check on line 333
334: 		                    _transferToken(instructions.recipient, IERC20(token1), amount1 - amountInDelta, instructions.unwrap);

// @audit check on line 671
691: 		            needed0 = amount0 - amountAdded0;

// @audit check on line 676
694: 		            needed1 = amount1 - amountAdded1;

// @audit check on line 681
700: 		            neededOther = amountOther - amountAddedOther;
```

*GitHub* : [317](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L317), [334](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L334), [691](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L691), [694](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L694), [700](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L700)

### [G-21]<a name="g-21"></a> Add `unchecked` blocks for divisions where the operands cannot overflow

`uint` divisions can't overflow, while `int` divisions can overflow only in [one specific case](https://docs.soliditylang.org/en/latest/types.html#division).

Consider adding an `unchecked` block to have some [gas savings](https://gist.github.com/DadeKuma/3bc597338ae774b8b3bd43280d55271f).

*There are 60 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

50: 		        return debt * Q96 / (cash + debt);

67: 		            borrowRateX96 = (utilizationRateX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

69: 		            uint256 normalRateX96 = (kinkX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

71: 		            borrowRateX96 = (excessUtilX96 * jumpMultiplierPerSecondX96 / Q96) + normalRateX96;

74: 		        supplyRateX96 = utilizationRateX96 * borrowRateX96 / Q96;

95: 		        baseRatePerSecondX96 = baseRatePerYearX96 / YEAR_SECS;

96: 		        multiplierPerSecondX96 = multiplierPerYearX96 / YEAR_SECS;

97: 		        jumpMultiplierPerSecondX96 = jumpMultiplierPerYearX96 / YEAR_SECS;
```

*GitHub* : [74](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L74), [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L95), [96](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L96), [97](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L97), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L71), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L69), [67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L67), [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L50)

```solidity
File: src/V3Oracle.sol

120: 		        value = (price0X96 * (amount0 + fees0) / Q96 + price1X96 * (amount1 + fees1) / Q96) * Q96 / priceTokenX96;

120: 		        value = (price0X96 * (amount0 + fees0) / Q96 + price1X96 * (amount1 + fees1) / Q96) * Q96 / priceTokenX96;

120: 		        value = (price0X96 * (amount0 + fees0) / Q96 + price1X96 * (amount1 + fees1) / Q96) * Q96 / priceTokenX96;

121: 		        feeValue = (price0X96 * fees0 / Q96 + price1X96 * fees1 / Q96) * Q96 / priceTokenX96;

121: 		        feeValue = (price0X96 * fees0 / Q96 + price1X96 * fees1 / Q96) * Q96 / priceTokenX96;

121: 		        feeValue = (price0X96 * fees0 / Q96 + price1X96 * fees1 / Q96) * Q96 / priceTokenX96;

122: 		        price0X96 = price0X96 * Q96 / priceTokenX96;

123: 		        price1X96 = price1X96 * Q96 / priceTokenX96;

129: 		        uint256 derivedPoolPriceX96 = price0X96 * Q96 / price1X96;

144: 		            ? (priceX96 - verifyPriceX96) * 10000 / priceX96

145: 		            : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;

304: 		            chainlinkPriceX96 = (10 ** referenceTokenDecimals) * chainlinkPriceX96 * Q96 / chainlinkReferencePriceX96
305: 		                / (10 ** feedConfig.tokenDecimals);

304: 		            chainlinkPriceX96 = (10 ** referenceTokenDecimals) * chainlinkPriceX96 * Q96 / chainlinkReferencePriceX96

342: 		        return uint256(answer) * Q96 / (10 ** feedConfig.feedDecimals);

353: 		            poolTWAPPriceX96 = Q96 * Q96 / priceX96;

369: 		            int24 tick = int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapSeconds)));
```

*GitHub* : [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L121), [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L121), [122](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L122), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L123), [129](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L129), [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L144), [145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L145), [304-305](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L304-L305), [304](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L304), [342](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L342), [353](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L353), [369](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L369), [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L120), [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L120), [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L120), [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L121)

```solidity
File: src/V3Vault.sol

769: 		            _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up) * reserveProtectionFactorX32 / Q32;

1054: 		                fees0 = uint128(liquidationValue * fees0 / feeValue);

1055: 		                fees1 = uint128(liquidationValue * fees1 / feeValue);

1060: 		                liquidity = uint128((liquidationValue - feeValue) * liquidity / (fullValue - feeValue));

1100: 		        uint256 maxPenaltyValue = debt * (Q32 + MAX_LIQUIDATION_PENALTY_X32) / Q32;

1105: 		            uint256 startLiquidationValue = debt * fullValue / collateralValue;

1107: 		                (Q96 - ((fullValue - maxPenaltyValue) * Q96 / (startLiquidationValue - maxPenaltyValue)));

1109: 		                + (MAX_LIQUIDATION_PENALTY_X32 - MIN_LIQUIDATION_PENALTY_X32) * penaltyFractionX96 / Q96;

1111: 		            liquidationValue = debt * (Q32 + penaltyX32) / Q32;

1116: 		            uint256 penaltyValue = fullValue * (Q32 - MAX_LIQUIDATION_PENALTY_X32) / Q32;

1137: 		            newLendExchangeRateX96 = (totalLent - missing) * newLendExchangeRateX96 / totalLent;

1188: 		                + oldDebtExchangeRateX96 * (block.timestamp - lastRateUpdate) * borrowRateX96 / Q96;

1190: 		                + oldLendExchangeRateX96 * (block.timestamp - lastRateUpdate) * supplyRateX96 / Q96;

1230: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1238: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1248: 		        uint256 time = block.timestamp / 1 days;

1250: 		            uint256 lendIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)
1251: 		                * (Q32 + MAX_DAILY_LEND_INCREASE_X32) / Q32;

1260: 		        uint256 time = block.timestamp / 1 days;

1262: 		            uint256 debtIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)
1263: 		                * (Q32 + MAX_DAILY_DEBT_INCREASE_X32) / Q32;
```

*GitHub* : [1248](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1248), [769](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L769), [1054](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1054), [1055](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1055), [1060](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1060), [1100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1100), [1105](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1105), [1107](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1107), [1109](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1109), [1111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1111), [1116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1116), [1137](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1137), [1188](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1188), [1190](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1190), [1230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1230), [1238](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1238), [1250-1251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1250-L1251), [1260](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1260), [1262-1263](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1262-L1263)

```solidity
File: src/automators/AutoExit.sol

155: 		                state.amount0 -= state.feeAmount0 * params.rewardX64 / Q64;

156: 		                state.amount1 -= state.feeAmount1 * params.rewardX64 / Q64;

187: 		                    state.amount0 -= state.amount0 * params.rewardX64 / Q64;

189: 		                    state.amount1 -= state.amount1 * params.rewardX64 / Q64;

194: 		            state.amount0 -= (config.onlyFees ? state.feeAmount0 : state.amount0) * params.rewardX64 / Q64;

195: 		            state.amount1 -= (config.onlyFees ? state.feeAmount1 : state.amount1) * params.rewardX64 / Q64;
```

*GitHub* : [187](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L187), [189](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L189), [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L195), [194](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L194), [155](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L155), [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L156)

```solidity
File: src/automators/Automator.sol

187: 		            return (int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapPeriod))), true);
```

*GitHub* : [187](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L187)

```solidity
File: src/transformers/AutoCompound.sol

156: 		            state.maxAddAmount0 = state.amount0 * Q64 / (rewardX64 + Q64);

157: 		            state.maxAddAmount1 = state.amount1 * Q64 / (rewardX64 + Q64);

170: 		                state.amount0Fees = state.compounded0 * rewardX64 / Q64;

171: 		                state.amount1Fees = state.compounded1 * rewardX64 / Q64;
```

*GitHub* : [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L157), [170](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L170), [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L171), [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L156)

```solidity
File: src/transformers/AutoRange.sol

143: 		            state.protocolReward0 = state.feeAmount0 * params.rewardX64 / Q64;

144: 		            state.protocolReward1 = state.feeAmount1 * params.rewardX64 / Q64;

195: 		            state.maxAddAmount0 = config.onlyFees ? state.amount0 : state.amount0 * Q64 / (params.rewardX64 + Q64);

196: 		            state.maxAddAmount1 = config.onlyFees ? state.amount1 : state.amount1 * Q64 / (params.rewardX64 + Q64);

236: 		                state.protocolReward0 = state.amountAdded0 * params.rewardX64 / Q64;

237: 		                state.protocolReward1 = state.amountAdded1 * params.rewardX64 / Q64;
```

*GitHub* : [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L144), [196](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L196), [236](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L236), [237](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L237), [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L195), [143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L143)

### [G-22]<a name="g-22"></a> Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead

Citing the [documentation](https://docs.soliditylang.org/en/latest/internals/layout_in_storage.html):

> When using elements that are smaller than 32 bytes, your contract’s gas usage may be higher.This is because the EVM operates on 32 bytes at a time.Therefore, if the element is smaller than that, the EVM must use more operations in order to reduce the size of the element from 32 bytes to the desired size.

For example, each operation involving a `uint8` costs an extra ** 22 - 28 gas ** (depending on whether the other operand is also a variable of type `uint8`) as compared to ones involving`uint256`, due to the compiler having to clear the higher bits of the memory word before operating on the`uint8`, as well as the associated stack operations of doing so.

Note that it might be beneficial to use reduced-size types when dealing with storage values because the compiler will pack multiple elements into one storage slot, but if not, it will have the opposite effect.

*There are 186 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

25: 		    uint16 public constant MIN_PRICE_DIFFERENCE = 200; //2%

32: 		    event SetMaxPoolPriceDifference(uint16 maxPoolPriceDifference);

45: 		        uint32 maxFeedAge;

46: 		        uint8 feedDecimals;

47: 		        uint8 tokenDecimals;

50: 		        uint32 twapSeconds;

52: 		        uint16 maxDifference; // max price difference x10000

63: 		    uint8 public immutable referenceTokenDecimals;

65: 		    uint16 public maxPoolPriceDifference = MIN_PRICE_DIFFERENCE; // max price difference between oracle derived price and pool price x10000

101: 		        (address token0, address token1, uint24 fee,, uint256 amount0, uint256 amount1, uint256 fees0, uint256 fees1) =

133: 		    function _checkPoolPrice(address token0, address token1, uint24 fee, uint256 derivedPoolPriceX96) internal view {

169: 		            uint24 fee,

170: 		            uint128 liquidity,

173: 		            uint128 fees0,

174: 		            uint128 fees1

185: 		    function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

204: 		        uint32 maxFeedAge,

206: 		        uint32 twapSeconds,

208: 		        uint16 maxDifference

215: 		        uint8 feedDecimals = feed.decimals();

216: 		        uint8 tokenDecimals = IERC20Metadata(token).decimals();

359: 		    function _getReferencePoolPriceX96(IUniswapV3Pool pool, uint32 twapSeconds) internal view returns (uint256) {

360: 		        uint160 sqrtPriceX96;

369: 		            int24 tick = int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapSeconds)));

380: 		        uint24 fee;

381: 		        int24 tickLower;

382: 		        int24 tickUpper;

383: 		        uint128 liquidity;

386: 		        uint128 tokensOwed0;

387: 		        uint128 tokensOwed1;

389: 		        uint160 sqrtPriceX96;

390: 		        int24 tick;

391: 		        uint160 sqrtPriceX96Lower;

392: 		        uint160 sqrtPriceX96Upper;

401: 		            uint24 fee,

402: 		            int24 tickLower,

403: 		            int24 tickUpper,

404: 		            uint128 liquidity,

407: 		            uint128 tokensOwed0,

408: 		            uint128 tokensOwed1

429: 		        returns (uint256 amount0, uint256 amount1, uint128 fees0, uint128 fees1)

429: 		        returns (uint256 amount0, uint256 amount1, uint128 fees0, uint128 fees1)

445: 		    function _getUncollectedFees(PositionState memory position, int24 tick)

448: 		        returns (uint128 fees0, uint128 fees1)

448: 		        returns (uint128 fees0, uint128 fees1)

474: 		        int24 tickLower,

475: 		        int24 tickUpper,

476: 		        int24 tickCurrent,

499: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [204](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L204), [206](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L206), [208](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L208), [215](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L215), [216](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L216), [359](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L359), [360](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L360), [369](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L369), [380](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L380), [381](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L381), [382](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L382), [383](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L383), [386](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L386), [387](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L387), [389](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L389), [390](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L390), [391](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L391), [392](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L392), [401](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L401), [402](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L402), [403](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L403), [404](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L404), [407](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L407), [408](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L408), [429](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L429), [429](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L429), [445](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L445), [448](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L448), [474](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L474), [475](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L475), [476](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L476), [499](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L499), [448](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L448), [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L25), [32](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L32), [45](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L45), [46](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L46), [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L47), [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L50), [52](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L52), [63](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L63), [65](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L65), [101](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L101), [133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L133), [169](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L169), [170](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L170), [173](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L173), [174](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L174), [185](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L185)

```solidity
File: src/V3Vault.sol

36: 		    uint32 public constant MAX_COLLATERAL_FACTOR_X32 = uint32(Q32 * 90 / 100); // 90%

38: 		    uint32 public constant MIN_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 2 / 100); // 2%

39: 		    uint32 public constant MAX_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 10 / 100); // 10%

41: 		    uint32 public constant MIN_RESERVE_PROTECTION_FACTOR_X32 = uint32(Q32 / 100); //1%

43: 		    uint32 public constant MAX_DAILY_LEND_INCREASE_X32 = uint32(Q32 / 10); //10%

44: 		    uint32 public constant MAX_DAILY_DEBT_INCREASE_X32 = uint32(Q32 / 10); //10%

65: 		    uint8 private immutable assetDecimals;

76: 		        uint256 indexed tokenId, address owner, address recipient, uint128 liquidity, uint256 amount0, uint256 amount1

102: 		    event SetReserveFactor(uint32 reserveFactorX32);

103: 		    event SetReserveProtectionFactor(uint32 reserveProtectionFactorX32);

104: 		    event SetTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32);

104: 		    event SetTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32);

110: 		        uint32 collateralFactorX32; // how much this token is valued as collateral

111: 		        uint32 collateralValueLimitFactorX32; // how much asset equivalent may be lent out given this collateral

112: 		        uint192 totalDebtShares; // how much debt shares are theoretically backed by this collateral

118: 		    uint32 public reserveFactorX32 = 0;

121: 		    uint32 public reserveProtectionFactorX32 = MIN_RESERVE_PROTECTION_FACTOR_X32;

277: 		    function decimals() public view override(IERC20Metadata, ERC20) returns (uint8) {

415: 		        uint8 v,

837: 		    function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

844: 		    function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

856: 		    function setTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32)

856: 		    function setTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32)

1039: 		        uint128 liquidity;

1040: 		        uint128 fees0;

1041: 		        uint128 fees1;

1143: 		    function _calculateTokenCollateralFactorX32(uint256 tokenId) internal view returns (uint32) {

1145: 		        uint32 factor0X32 = tokenConfigs[token0].collateralFactorX32;

1146: 		        uint32 factor1X32 = tokenConfigs[token1].collateralFactorX32;
```

*GitHub* : [44](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L44), [36](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L36), [38](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L38), [39](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L39), [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L41), [43](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L43), [65](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L65), [76](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L76), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L102), [103](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L103), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L104), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L104), [110](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L110), [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L111), [112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L112), [118](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L118), [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L121), [277](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L277), [415](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L415), [837](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L837), [844](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L844), [856](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L856), [856](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L856), [1039](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1039), [1040](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1040), [1041](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1041), [1143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1143), [1145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1145), [1146](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1146)

```solidity
File: src/automators/AutoExit.sol

25: 		        int24 token0TriggerTick,

26: 		        int24 token1TriggerTick,

27: 		        uint64 token0SlippageX64,

28: 		        uint64 token1SlippageX64,

30: 		        uint64 maxRewardX64

37: 		        uint32 _TWAPSeconds,

38: 		        uint16 _maxTWAPTickDifference,

50: 		        int24 token0TriggerTick; // when tick is below this one

51: 		        int24 token1TriggerTick; // when tick is equal or above this one

53: 		        uint64 token0SlippageX64; // when token 0 is swapped to token 1

54: 		        uint64 token1SlippageX64; // when token 1 is swapped to token 0

56: 		        uint64 maxRewardX64; // max allowed reward percentage of fees or full position

66: 		        uint128 liquidity; // liquidity the calculations are based on

70: 		        uint64 rewardX64; // which reward will be used for protocol, can be max configured amount (considering onlyFees)

76: 		        uint24 fee;

77: 		        int24 tickLower;

78: 		        int24 tickUpper;

79: 		        uint128 liquidity;

89: 		        int24 tick;
```

*GitHub* : [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L25), [26](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L26), [27](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L27), [28](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L28), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L78), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L79), [89](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L89), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L30), [54](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L54), [56](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L56), [66](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L66), [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L70), [76](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L76), [53](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L53), [77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L77), [37](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L37), [38](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L38), [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L50), [51](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L51)

```solidity
File: src/automators/Automator.sol

23: 		    uint32 public constant MIN_TWAP_SECONDS = 60; // 1 minute

24: 		    uint32 public constant MAX_TWAP_TICK_DIFFERENCE = 200; // 2%

31: 		    event TWAPConfigChanged(uint32 TWAPSeconds, uint16 maxTWAPTickDifference);

31: 		    event TWAPConfigChanged(uint32 TWAPSeconds, uint16 maxTWAPTickDifference);

38: 		    uint32 public TWAPSeconds;

39: 		    uint16 public maxTWAPTickDifference;

45: 		        uint32 _TWAPSeconds,

46: 		        uint16 _maxTWAPTickDifference,

87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {

87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {

143: 		        uint32 twapPeriod,

144: 		        uint16 maxTickDifference,

145: 		        uint64 maxPriceDifferenceX64

146: 		    ) internal view returns (uint256 amountOutMin, int24 currentTick, uint160 sqrtPriceX96, uint256 priceX96) {

146: 		    ) internal view returns (uint256 amountOutMin, int24 currentTick, uint160 sqrtPriceX96, uint256 priceX96) {

166: 		    function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

166: 		    function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

166: 		    function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

171: 		        (int24 twapTick, bool twapOk) = _getTWAPTick(pool, twapPeriod);

180: 		    function _getTWAPTick(IUniswapV3Pool pool, uint32 twapPeriod) internal view returns (int24, bool) {

180: 		    function _getTWAPTick(IUniswapV3Pool pool, uint32 twapPeriod) internal view returns (int24, bool) {

195: 		        uint128 liquidity,
```

*GitHub* : [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L171), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L180), [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L195), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L180), [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L23), [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L24), [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L31), [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L31), [38](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L38), [39](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L39), [45](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L45), [46](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L46), [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87), [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87), [143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L143), [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L144), [145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L145), [146](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L146), [146](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L146), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L166), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L166), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L166)

```solidity
File: src/transformers/AutoCompound.sol

30: 		    event RewardUpdated(address account, uint64 totalRewardX64);

41: 		        uint32 _TWAPSeconds,

42: 		        uint16 _maxTWAPTickDifference

47: 		    uint64 public constant MAX_REWARD_X64 = uint64(Q64 / 50); // 2%

48: 		    uint64 public totalRewardX64 = MAX_REWARD_X64; // 2%

71: 		        uint24 fee;

72: 		        int24 tickLower;

73: 		        int24 tickUpper;

76: 		        int24 tick;

77: 		        uint160 sqrtPriceX96;

132: 		                uint32 tSecs = TWAPSeconds;

243: 		    function setReward(uint64 _totalRewardX64) external onlyOwner {
```

*GitHub* : [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L71), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L30), [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L41), [42](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L42), [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L47), [48](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L48), [72](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L72), [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L73), [76](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L76), [77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L77), [132](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L132), [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L243)

```solidity
File: src/transformers/AutoRange.sol

15: 		        int32 lowerTickLimit,

16: 		        int32 upperTickLimit,

17: 		        int32 lowerTickDelta,

18: 		        int32 upperTickDelta,

19: 		        uint64 token0SlippageX64,

20: 		        uint64 token1SlippageX64,

22: 		        uint64 maxRewardX64

29: 		        uint32 _TWAPSeconds,

30: 		        uint16 _maxTWAPTickDifference,

39: 		        int32 lowerTickLimit; // if negative also in-range positions may be adjusted / if 0 out of range positions may be adjusted

40: 		        int32 upperTickLimit; // if negative also in-range positions may be adjusted / if 0 out of range positions may be adjusted

41: 		        int32 lowerTickDelta; // this amount is added to current tick (floored to tickspacing) to define lowerTick of new position

42: 		        int32 upperTickDelta; // this amount is added to current tick (floored to tickspacing) to define upperTick of new position

43: 		        uint64 token0SlippageX64; // max price difference from current pool price for swap / Q64 for token0

44: 		        uint64 token1SlippageX64; // max price difference from current pool price for swap / Q64 for token1

46: 		        uint64 maxRewardX64; // max allowed reward percentage of fees or full position

58: 		        uint128 liquidity; // liquidity the calculations are based on

62: 		        uint64 rewardX64; // which reward will be used for protocol, can be max configured amount (considering onlyFees)

71: 		        uint24 fee;

72: 		        int24 tickLower;

73: 		        int24 tickUpper;

74: 		        int24 currentTick;

83: 		        uint128 liquidity;

170: 		            int24 tickSpacing = _getTickSpacing(state.fee);

171: 		            int24 baseTick = state.currentTick - (((state.currentTick % tickSpacing) + tickSpacing) % tickSpacing);

300: 		    function _getTickSpacing(uint24 fee) internal view returns (int24) {

300: 		    function _getTickSpacing(uint24 fee) internal view returns (int24) {

308: 		            int24 spacing = IUniswapV3Factory(factory).feeAmountTickSpacing(fee);
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L15), [20](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L20), [22](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L22), [29](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L29), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L30), [39](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L39), [40](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L40), [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L41), [42](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L42), [43](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L43), [44](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L44), [46](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L46), [58](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L58), [62](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L62), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L71), [72](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L72), [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L73), [74](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L74), [83](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L83), [170](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L170), [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L171), [300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L300), [300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L300), [308](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L308), [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L17), [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L16), [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L19), [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L18)

```solidity
File: src/transformers/LeverageTransformer.sol

102: 		        uint128 liquidity;

106: 		        uint128 feeAmount0;

107: 		        uint128 feeAmount1;
```

*GitHub* : [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L102), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L106), [107](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L107)

```solidity
File: src/transformers/V3Utils.sol

22: 		    event CompoundFees(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

25: 		    event SwapAndMint(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

26: 		    event SwapAndIncreaseLiquidity(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

67: 		        uint128 feeAmount0;

68: 		        uint128 feeAmount1;

70: 		        uint24 fee;

71: 		        int24 tickLower;

72: 		        int24 tickUpper;

74: 		        uint128 liquidity;

98: 		    function executeWithPermit(uint256 tokenId, Instructions memory instructions, uint8 v, bytes32 r, bytes32 s)

116: 		        (,, address token0, address token1,,,, uint128 liquidity,,,,) = nonfungiblePositionManager.positions(tokenId);

435: 		        uint24 fee;

436: 		        int24 tickLower;

437: 		        int24 tickUpper;

470: 		        returns (uint256 tokenId, uint128 liquidity, uint256 amount0, uint256 amount1)

535: 		        returns (uint128 liquidity, uint256 amount0, uint256 amount1)

707: 		        returns (uint256 tokenId, uint128 liquidity, uint256 added0, uint256 added1)

737: 		        returns (uint128 liquidity, uint256 added0, uint256 added1)

879: 		        uint128 liquidity,

892: 		    function _collectFees(uint256 tokenId, IERC20 token0, IERC20 token1, uint128 collectAmount0, uint128 collectAmount1)

892: 		    function _collectFees(uint256 tokenId, IERC20 token0, IERC20 token1, uint128 collectAmount0, uint128 collectAmount1)
```

*GitHub* : [22](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L22), [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L25), [26](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L26), [67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L67), [68](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L68), [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L70), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L71), [72](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L72), [74](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L74), [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L98), [116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L116), [435](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L435), [436](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L436), [437](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L437), [470](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L470), [535](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L535), [707](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L707), [737](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L737), [879](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L879), [892](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L892), [892](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L892)

```solidity
File: src/utils/Swapper.sol

124: 		        uint24 fee;

160: 		        (address tokenIn, address tokenOut, uint24 fee) = abi.decode(data, (address, address, uint24));

171: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [124](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L124), [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L171), [160](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L160)

### [G-23]<a name="g-23"></a> `>=`/`<=` costs less gas than `>`/`<`

The compiler uses opcodes `GT` and `ISZERO` for code that uses `>`, but only requires `LT` for `>=`. A similar behaviour applies for `>`, which uses opcodes `LT` and `ISZERO`, but only requires `GT` for `<=`.

*There are 127 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

89: 		            baseRatePerYearX96 > MAX_BASE_RATE_X96 || multiplierPerYearX96 > MAX_MULTIPLIER_X96

89: 		            baseRatePerYearX96 > MAX_BASE_RATE_X96 || multiplierPerYearX96 > MAX_MULTIPLIER_X96

90: 		                || jumpMultiplierPerYearX96 > MAX_MULTIPLIER_X96
```

*GitHub* : [89](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L89), [90](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L90), [89](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L89)

```solidity
File: src/V3Oracle.sol

143: 		        uint256 differenceX10000 = priceX96 > verifyPriceX96

186: 		        if (_maxPoolPriceDifference < MIN_PRICE_DIFFERENCE) {

221: 		            if (maxDifference < MIN_PRICE_DIFFERENCE) {

338: 		        if (updatedAt + feedConfig.maxFeedAge < block.timestamp || answer < 0) {

338: 		        if (updatedAt + feedConfig.maxFeedAge < block.timestamp || answer < 0) {

431: 		        if (state.liquidity > 0) {

485: 		            if (tickCurrent < tickLower) {

488: 		            } else if (tickCurrent < tickUpper) {
```

*GitHub* : [431](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L431), [338](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L338), [488](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L488), [485](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L485), [186](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L186), [143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L143), [338](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L338), [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L221)

```solidity
File: src/V3Vault.sol

443: 		            if (data.length > 0) {

505: 		        if (transformedTokenId > 0) {

552: 		            transformedTokenId > 0 && transformedTokenId == tokenId && transformerAllowList[msg.sender];

571: 		        if (debtSharesTotal > _convertToShares(globalDebtLimit, newDebtExchangeRateX96, Math.Rounding.Down)) {

574: 		        if (assets > dailyDebtIncreaseLimitLeft) {

586: 		        if (debt < minLoanSize) {

615: 		        if (transformedTokenId > 0) {

687: 		        if (transformedTokenId > 0) {

712: 		        if (state.reserveCost > 0) {

717: 		        if (params.permitData.length > 0) {

737: 		        if (amount0 < params.amount0Min || amount1 < params.amount1Min) {

737: 		        if (amount0 < params.amount0Min || amount1 < params.amount1Min) {

771: 		        uint256 unprotected = reserves > protected ? reserves - protected : 0;

772: 		        uint256 available = balance > unprotected ? unprotected : balance;

774: 		        if (amount > available) {

778: 		        if (amount > 0) {

845: 		        if (_reserveProtectionFactorX32 < MIN_RESERVE_PROTECTION_FACTOR_X32) {

860: 		        if (collateralFactorX32 > MAX_COLLATERAL_FACTOR_X32) {

893: 		        if (permitData.length > 0) {

906: 		        if (totalSupply() > globalLendLimit) {

910: 		        if (assets > dailyLendIncreaseLimitLeft) {

940: 		        if (available < assets) {

973: 		        if (shares > currentShares) {

977: 		        if (assets > 0) {

978: 		            if (permitData.length > 0) {

1008: 		            if (_convertToAssets(loanDebtShares, newDebtExchangeRateX96, Math.Rounding.Up) < minLoanSize) {

1027: 		        reserves = balance + debt > lent ? balance + debt - lent : 0;

1028: 		        available = balance > reserves ? balance - reserves : 0;

1052: 		            if (liquidationValue < feeValue) {

1064: 		        if (liquidity > 0) {

1131: 		        if (reserveCost > reserves) {

1147: 		        return factor0X32 > factor1X32 ? factor1X32 : factor0X32;

1155: 		        if (block.timestamp > lastExchangeRateUpdate) {

1186: 		        if (lastRateUpdate > 0) {

1216: 		            if (oldShares > newShares) {

1228: 		                    collateralValueLimitFactorX32 < type(uint32).max

1229: 		                        && _convertToAssets(tokenConfigs[token0].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1230: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1236: 		                    collateralValueLimitFactorX32 < type(uint32).max

1237: 		                        && _convertToAssets(tokenConfigs[token1].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1238: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1249: 		        if (force || time > dailyLendIncreaseLimitLastReset) {

1253: 		                dailyLendIncreaseLimitMin > lendIncreaseLimit ? dailyLendIncreaseLimitMin : lendIncreaseLimit;

1261: 		        if (force || time > dailyDebtIncreaseLimitLastReset) {

1265: 		                dailyDebtIncreaseLimitMin > debtIncreaseLimit ? dailyDebtIncreaseLimitMin : debtIncreaseLimit;
```

*GitHub* : [772](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L772), [774](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L774), [778](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L778), [845](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L845), [860](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L860), [893](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L893), [906](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L906), [910](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L910), [940](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L940), [973](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L973), [977](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L977), [978](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L978), [1008](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1008), [1027](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1027), [1028](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1028), [1052](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1052), [1064](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1064), [1131](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1131), [1147](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1147), [1155](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1155), [1186](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1186), [1216](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1216), [1228](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1228), [1229-1230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1229-L1230), [1236](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1236), [1249](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1249), [1253](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1253), [1261](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1261), [1265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1265), [1237-1238](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1237-L1238), [443](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L443), [505](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L505), [552](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L552), [571](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L571), [574](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L574), [586](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L586), [615](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L615), [687](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L687), [712](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L712), [717](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L717), [737](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L737), [737](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L737), [771](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L771)

```solidity
File: src/automators/AutoExit.sol

113: 		            config.onlyFees && params.rewardX64 > config.maxRewardX64

114: 		                || !config.onlyFees && params.rewardX64 > config.maxRewardX64

135: 		        if (config.token0TriggerTick <= state.tick && state.tick < config.token1TriggerTick) {

199: 		        if (state.amount0 > 0) {

202: 		        if (state.amount1 > 0) {
```

*GitHub* : [202](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L202), [199](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L199), [135](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L135), [114](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L114), [113](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L113)

```solidity
File: src/automators/Automator.sol

88: 		        if (_TWAPSeconds < MIN_TWAP_SECONDS) {

91: 		        if (_maxTWAPTickDifference > MAX_TWAP_TICK_DIFFERENCE) {

111: 		        for (; i < count; ++i) {

113: 		            if (balance > 0) {

129: 		        if (balance > 0) {

200: 		        if (liquidity > 0) {
```

*GitHub* : [129](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L129), [200](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L200), [88](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L88), [91](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L91), [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L111), [113](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L113)

```solidity
File: src/transformers/AutoCompound.sol

123: 		        if (state.amount0 > 0 || state.amount1 > 0) {

123: 		        if (state.amount0 > 0 || state.amount1 > 0) {

127: 		            if (amountIn > 0) {

133: 		                if (tSecs > 0) {

140: 		                if (amountIn > 0) {

160: 		            if (state.maxAddAmount0 > 0 || state.maxAddAmount1 > 0) {

160: 		            if (state.maxAddAmount0 > 0 || state.maxAddAmount1 > 0) {

212: 		        if (balance0 > 0) {

216: 		        if (balance1 > 0) {

233: 		        for (; i < count; ++i) {

258: 		            if (amount > currentBalance) {
```

*GitHub* : [140](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L140), [160](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L160), [160](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L160), [212](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L212), [216](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L216), [233](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L233), [258](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L258), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L123), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L123), [127](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L127), [133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L133)

```solidity
File: src/transformers/AutoRange.sol

123: 		            config.onlyFees && params.rewardX64 > config.maxRewardX64

124: 		                || !config.onlyFees && params.rewardX64 > config.maxRewardX64

149: 		        if (params.swap0To1 && params.amountIn > state.amount0 || !params.swap0To1 && params.amountIn > state.amount1) {

149: 		        if (params.swap0To1 && params.amountIn > state.amount0 || !params.swap0To1 && params.amountIn > state.amount1) {

167: 		            state.currentTick < state.tickLower - config.lowerTickLimit

243: 		            if (state.amount0 - state.amountAdded0 > 0) {

246: 		            if (state.amount1 - state.amountAdded1 > 0) {

280: 		        if (config.lowerTickDelta > config.upperTickDelta) {
```

*GitHub* : [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L123), [124](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L124), [149](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L149), [149](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L149), [167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L167), [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L243), [246](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L246), [280](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L280)

```solidity
File: src/transformers/LeverageTransformer.sol

52: 		        if (params.amountIn0 > 0) {

64: 		        if (params.amountIn1 > 0) {

87: 		        if (amount0 > added0) {

90: 		        if (amount1 > added1) {

93: 		        if (token != token0 && token != token1 && amount > 0) {

146: 		        if (params.amountIn0 > 0 && token != token0) {

155: 		        if (params.amountIn1 > 0 && token != token1) {

169: 		        if (amount0 > 0 && token != token0) {

172: 		        if (amount1 > 0 && token != token1) {
```

*GitHub* : [52](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L52), [64](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L64), [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L87), [90](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L90), [172](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L172), [146](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L146), [155](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L155), [169](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L169), [93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L93)

```solidity
File: src/transformers/V3Utils.sol

142: 		        if (amount0 < instructions.amountIn0 || amount1 < instructions.amountIn1) {

142: 		        if (amount0 < instructions.amountIn0 || amount1 < instructions.amountIn1) {

316: 		                if (amountInDelta < amount0) {

333: 		                if (amountInDelta < amount1) {

402: 		        if (params.permitData.length > 0) {

476: 		        if (params.permitData.length > 0) {

539: 		        if (params.permitData.length > 0) {

577: 		        if (needed0 > 0) {

580: 		        if (needed1 > 0) {

583: 		        if (neededOther > 0) {

617: 		        if (state.needed0 > 0) {

621: 		        if (state.needed1 > 0) {

625: 		        if (state.neededOther > 0) {

634: 		        if (state.needed0 > 0) {

639: 		        if (state.needed1 > 0) {

644: 		        if (state.neededOther > 0) {

671: 		                if (amountAdded0 > amount0) {

676: 		                if (amountAdded1 > amount1) {

681: 		                if (amountAddedOther > amountOther) {

690: 		        if (amount0 > amountAdded0) {

693: 		        if (amount1 > amountAdded1) {

697: 		            amountOther > amountAddedOther && address(otherToken) != address(0) && token0 != otherToken

784: 		            if (params.amount0 < params.amountIn1) {

795: 		            if (params.amount1 < params.amountIn0) {
```

*GitHub* : [402](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L402), [476](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L476), [539](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L539), [577](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L577), [580](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L580), [583](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L583), [617](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L617), [621](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L621), [625](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L625), [634](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L634), [639](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L639), [644](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L644), [671](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L671), [676](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L676), [681](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L681), [690](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L690), [693](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L693), [697](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L697), [784](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L784), [795](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L795), [142](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L142), [142](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L142), [316](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L316), [333](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L333)

```solidity
File: src/utils/FlashloanLiquidator.sol

90: 		            if (balance > 0) {

96: 		            if (balance > 0) {

102: 		            if (balance < data.minReward) {

105: 		            if (balance > 0) {
```

*GitHub* : [105](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L105), [90](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L90), [96](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L96), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L102)

```solidity
File: src/utils/Swapper.sol

111: 		            if (amountOutDelta < params.amountOutMin) {

133: 		        if (params.amountIn > 0) {

149: 		            if (amountOutDelta < params.amountOutMin) {

157: 		        require(amount0Delta > 0 || amount1Delta > 0); // swaps entirely within 0-liquidity regions are not supported

157: 		        require(amount0Delta > 0 || amount1Delta > 0); // swaps entirely within 0-liquidity regions are not supported

166: 		        uint256 amountToPay = amount0Delta > 0 ? uint256(amount0Delta) : uint256(amount1Delta);
```

*GitHub* : [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L157), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L166), [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L157), [149](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L149), [133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L133), [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L111)

### [G-24]<a name="g-24"></a> `internal` functions only called once can be inlined to save gas

Consider removing the following internal functions, and put the logic directly where they are called, as they are called only once.

*There are 18 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

133: 		    function _checkPoolPrice(address token0, address token1, uint24 fee, uint256 derivedPoolPriceX96) internal view {

346: 		    function _getTWAPPriceX96(TokenConfig memory feedConfig) internal view returns (uint256 poolTWAPPriceX96) {

395: 		    function _initializeState(uint256 tokenId) internal view returns (PositionState memory state) {

426: 		    function _getAmounts(PositionState memory state)

445: 		    function _getUncollectedFees(PositionState memory position, int24 tick)

472: 		    function _getFeeGrowthInside(
```

*GitHub* : [445](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L445), [472](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L472), [133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L133), [346](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L346), [395](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L395), [426](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L426)

```solidity
File: src/V3Vault.sol

1032: 		    function _sendPositionValue(

1123: 		    function _handleReserveLiquidation(

1143: 		    function _calculateTokenCollateralFactorX32(uint256 tokenId) internal view returns (uint32) {

1303: 		    function _removeTokenFromOwner(address from, uint256 tokenId) internal {
```

*GitHub* : [1143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1143), [1123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1123), [1032](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1032), [1303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1303)

```solidity
File: src/automators/Automator.sol

166: 		    function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

180: 		    function _getTWAPTick(IUniswapV3Pool pool, uint32 twapPeriod) internal view returns (int24, bool) {

218: 		    function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {
```

*GitHub* : [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L166), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L180), [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L218)

```solidity
File: src/transformers/AutoCompound.sol

276: 		    function _checkApprovals(address token0, address token1) internal {
```

*GitHub* : [276](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L276)

```solidity
File: src/transformers/AutoRange.sol

300: 		    function _getTickSpacing(uint24 fee) internal view returns (int24) {
```

*GitHub* : [300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L300)

```solidity
File: src/transformers/V3Utils.sol

877: 		    function _decreaseLiquidity(

892: 		    function _collectFees(uint256 tokenId, IERC20 token0, IERC20 token1, uint128 collectAmount0, uint128 collectAmount1)
```

*GitHub* : [892](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L892), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L877)

```solidity
File: src/utils/Swapper.sol

171: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L171)

### [G-25]<a name="g-25"></a> Use multiple revert checks to save gas

Splitting the conditions into two separate checks [saves](https://gist.github.com/IllIllI000/7e25b0fca6bd9d57d9b9bcb9d2018959) 2 gas per split.

*There are 26 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

88: 		        if (
89: 		            baseRatePerYearX96 > MAX_BASE_RATE_X96 || multiplierPerYearX96 > MAX_MULTIPLIER_X96
90: 		                || jumpMultiplierPerYearX96 > MAX_MULTIPLIER_X96
91: 		        ) {
92: 		            revert InvalidConfig();
93: 		        }
```

*GitHub* : [88-93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L88-L93)

```solidity
File: src/V3Oracle.sol

250: 		        if (msg.sender != emergencyAdmin && msg.sender != owner()) {
251: 		            revert Unauthorized();
252: 		        }

338: 		        if (updatedAt + feedConfig.maxFeedAge < block.timestamp || answer < 0) {
339: 		            revert ChainlinkPriceError();
340: 		        }
```

*GitHub* : [250-252](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L250-L252), [338-340](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L338-L340)

```solidity
File: src/V3Vault.sol

435: 		        if (msg.sender != address(nonfungiblePositionManager) || from == address(this)) {
436: 		            revert WrongContract();
437: 		        }

502: 		        if (tokenId == 0 || !transformerAllowList[transformer]) {
503: 		            revert TransformNotAllowed();
504: 		        }

515: 		        if (loanOwner != msg.sender && !transformApprovals[loanOwner][tokenId][msg.sender]) {
516: 		            revert Unauthorized();
517: 		        }

561: 		        if (!isTransformMode && tokenOwner[tokenId] != msg.sender && address(this) != msg.sender) {
562: 		            revert Unauthorized();
563: 		        }

737: 		        if (amount0 < params.amount0Min || amount1 < params.amount1Min) {
738: 		            revert SlippageError();
739: 		        }

790: 		        if (
791: 		            transformer == address(0) || transformer == address(this) || transformer == asset
792: 		                || transformer == address(nonfungiblePositionManager)
793: 		        ) {
794: 		            revert InvalidConfig();
795: 		        }

814: 		        if (msg.sender != emergencyAdmin && msg.sender != owner()) {
815: 		            revert Unauthorized();
816: 		        }

1227: 		                if (
1228: 		                    collateralValueLimitFactorX32 < type(uint32).max
1229: 		                        && _convertToAssets(tokenConfigs[token0].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1230: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32
1231: 		                ) {
1232: 		                    revert CollateralValueLimit();
1233: 		                }

1235: 		                if (
1236: 		                    collateralValueLimitFactorX32 < type(uint32).max
1237: 		                        && _convertToAssets(tokenConfigs[token1].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1238: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32
1239: 		                ) {
1240: 		                    revert CollateralValueLimit();
1241: 		                }
```

*GitHub* : [790-795](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L790-L795), [435-437](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L435-L437), [502-504](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L502-L504), [515-517](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L515-L517), [561-563](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L561-L563), [737-739](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L737-L739), [814-816](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L814-L816), [1227-1233](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1227-L1233), [1235-1241](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1235-L1241)

```solidity
File: src/automators/AutoExit.sol

112: 		        if (
113: 		            config.onlyFees && params.rewardX64 > config.maxRewardX64
114: 		                || !config.onlyFees && params.rewardX64 > config.maxRewardX64
115: 		        ) {
116: 		            revert ExceedsMaxReward();
117: 		        }

135: 		        if (config.token0TriggerTick <= state.tick && state.tick < config.token1TriggerTick) {
136: 		            revert NotReady();
137: 		        }
```

*GitHub* : [135-137](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L135-L137), [112-117](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L112-L117)

```solidity
File: src/automators/Automator.sol

219: 		        if (address(weth) == address(token) && unwrap) {
220: 		            weth.withdraw(amount);
221: 		            (bool sent,) = to.call{value: amount}("");
222: 		            if (!sent) {
223: 		                revert EtherSendFailed();
224: 		            }
225: 		        } else {
226: 		            SafeERC20.safeTransfer(token, to, amount);
227: 		        }
```

*GitHub* : [219-227](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L219-L227)

```solidity
File: src/transformers/AutoCompound.sol

88: 		        if (!operators[msg.sender] || !vaults[vault]) {
89: 		            revert Unauthorized();
90: 		        }

102: 		        if (!operators[msg.sender] && !vaults[msg.sender]) {
103: 		            revert Unauthorized();
104: 		        }
```

*GitHub* : [102-104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L102-L104), [88-90](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L88-L90)

```solidity
File: src/transformers/AutoRange.sol

98: 		        if (!operators[msg.sender] || !vaults[vault]) {
99: 		            revert Unauthorized();
100: 		        }

112: 		        if (!operators[msg.sender] && !vaults[msg.sender]) {
113: 		            revert Unauthorized();
114: 		        }

122: 		        if (
123: 		            config.onlyFees && params.rewardX64 > config.maxRewardX64
124: 		                || !config.onlyFees && params.rewardX64 > config.maxRewardX64
125: 		        ) {
126: 		            revert ExceedsMaxReward();
127: 		        }

149: 		        if (params.swap0To1 && params.amountIn > state.amount0 || !params.swap0To1 && params.amountIn > state.amount1) {
150: 		            revert SwapAmountTooLarge();
151: 		        }

166: 		        if (
167: 		            state.currentTick < state.tickLower - config.lowerTickLimit
168: 		                || state.currentTick >= state.tickUpper + config.upperTickLimit
169: 		        ) {
170: 		            int24 tickSpacing = _getTickSpacing(state.fee);
171: 		            int24 baseTick = state.currentTick - (((state.currentTick % tickSpacing) + tickSpacing) % tickSpacing);
172: 		
173: 		            // check if new range same as old range
174: 		            if (
175: 		                baseTick + config.lowerTickDelta == state.tickLower
176: 		                    && baseTick + config.upperTickDelta == state.tickUpper
177: 		            ) {
178: 		                revert SameRange();
179: 		            }
180: 		
181: 		            (state.amountInDelta, state.amountOutDelta) = _routerSwap(
182: 		                Swapper.RouterSwapParams(
183: 		                    params.swap0To1 ? IERC20(state.token0) : IERC20(state.token1),
184: 		                    params.swap0To1 ? IERC20(state.token1) : IERC20(state.token0),
185: 		                    params.amountIn,
186: 		                    state.amountOutMin,
187: 		                    params.swapData
188: 		                )
189: 		            );
190: 		
191: 		            state.amount0 = params.swap0To1 ? state.amount0 - state.amountInDelta : state.amount0 + state.amountOutDelta;
192: 		            state.amount1 = params.swap0To1 ? state.amount1 + state.amountOutDelta : state.amount1 - state.amountInDelta;
193: 		
194: 		            // max amount to add - removing max potential fees (if config.onlyFees - the have been removed already)
195: 		            state.maxAddAmount0 = config.onlyFees ? state.amount0 : state.amount0 * Q64 / (params.rewardX64 + Q64);
196: 		            state.maxAddAmount1 = config.onlyFees ? state.amount1 : state.amount1 * Q64 / (params.rewardX64 + Q64);
197: 		
198: 		            INonfungiblePositionManager.MintParams memory mintParams = INonfungiblePositionManager.MintParams(
199: 		                address(state.token0),
200: 		                address(state.token1),
201: 		                state.fee,
202: 		                SafeCast.toInt24(baseTick + config.lowerTickDelta), // reverts if out of valid range
203: 		                SafeCast.toInt24(baseTick + config.upperTickDelta), // reverts if out of valid range
204: 		                state.maxAddAmount0,
205: 		                state.maxAddAmount1,
206: 		                0,
207: 		                0,
208: 		                address(this), // is sent to real recipient aftwards
209: 		                params.deadline
210: 		            );
211: 		
212: 		            // approve npm
213: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), state.maxAddAmount0);
214: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), state.maxAddAmount1);
215: 		
216: 		            // mint is done to address(this) first - its not a safemint
217: 		            (state.newTokenId,, state.amountAdded0, state.amountAdded1) = nonfungiblePositionManager.mint(mintParams);
218: 		
219: 		            // remove remaining approval
220: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), 0);
221: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), 0);
222: 		
223: 		            state.owner = nonfungiblePositionManager.ownerOf(params.tokenId);
224: 		
225: 		            // get the real owner - if owner is vault - for sending leftover tokens
226: 		            state.realOwner = state.owner;
227: 		            if (vaults[state.owner]) {
228: 		                state.realOwner = IVault(state.owner).ownerOf(params.tokenId);
229: 		            }
230: 		
231: 		            // send the new nft to the owner / vault
232: 		            nonfungiblePositionManager.safeTransferFrom(address(this), state.owner, state.newTokenId);
233: 		
234: 		            // protocol reward is calculated based on added amount (to incentivize optimal swap done by operator)
235: 		            if (!config.onlyFees) {
236: 		                state.protocolReward0 = state.amountAdded0 * params.rewardX64 / Q64;
237: 		                state.protocolReward1 = state.amountAdded1 * params.rewardX64 / Q64;
238: 		                state.amount0 -= state.protocolReward0;
239: 		                state.amount1 -= state.protocolReward1;
240: 		            }
241: 		
242: 		            // send leftover to real owner
243: 		            if (state.amount0 - state.amountAdded0 > 0) {
244: 		                _transferToken(state.realOwner, IERC20(state.token0), state.amount0 - state.amountAdded0, true);
245: 		            }
246: 		            if (state.amount1 - state.amountAdded1 > 0) {
247: 		                _transferToken(state.realOwner, IERC20(state.token1), state.amount1 - state.amountAdded1, true);
248: 		            }
249: 		
250: 		            // copy token config for new token
251: 		            positionConfigs[state.newTokenId] = config;
252: 		            emit PositionConfigured(
253: 		                state.newTokenId,
254: 		                config.lowerTickLimit,
255: 		                config.upperTickLimit,
256: 		                config.lowerTickDelta,
257: 		                config.upperTickDelta,
258: 		                config.token0SlippageX64,
259: 		                config.token1SlippageX64,
260: 		                config.onlyFees,
261: 		                config.maxRewardX64
262: 		            );
263: 		
264: 		            // delete config for old position
265: 		            delete positionConfigs[params.tokenId];
266: 		            emit PositionConfigured(params.tokenId, 0, 0, 0, 0, 0, 0, false, 0);
267: 		
268: 		            emit RangeChanged(params.tokenId, state.newTokenId);
269: 		        } else {
270: 		            revert NotReady();
271: 		        }

174: 		            if (
175: 		                baseTick + config.lowerTickDelta == state.tickLower
176: 		                    && baseTick + config.upperTickDelta == state.tickUpper
177: 		            ) {
178: 		                revert SameRange();
179: 		            }
```

*GitHub* : [149-151](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L149-L151), [166-271](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L166-L271), [98-100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L98-L100), [174-179](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L174-L179), [112-114](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L112-L114), [122-127](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L122-L127)

```solidity
File: src/transformers/V3Utils.sol

142: 		        if (amount0 < instructions.amountIn0 || amount1 < instructions.amountIn1) {
143: 		            revert AmountError();
144: 		        }

865: 		        if (address(weth) == address(token) && unwrap) {
866: 		            weth.withdraw(amount);
867: 		            (bool sent,) = to.call{value: amount}("");
868: 		            if (!sent) {
869: 		                revert EtherSendFailed();
870: 		            }
871: 		        } else {
872: 		            SafeERC20.safeTransfer(token, to, amount);
873: 		        }
```

*GitHub* : [142-144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L142-L144), [865-873](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L865-L873)

```solidity
File: src/utils/Swapper.sol

77: 		        if (params.amountIn != 0 && params.swapData.length != 0 && address(params.tokenOut) != address(0)) {
78: 		            uint256 balanceInBefore = params.tokenIn.balanceOf(address(this));
79: 		            uint256 balanceOutBefore = params.tokenOut.balanceOf(address(this));
80: 		
81: 		            // get router specific swap data
82: 		            (address router, bytes memory routerData) = abi.decode(params.swapData, (address, bytes));
83: 		
84: 		            if (router == zeroxRouter) {
85: 		                ZeroxRouterData memory data = abi.decode(routerData, (ZeroxRouterData));
86: 		                // approve needed amount
87: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, params.amountIn);
88: 		                // execute swap
89: 		                (bool success,) = zeroxRouter.call(data.data);
90: 		                if (!success) {
91: 		                    revert SwapFailed();
92: 		                }
93: 		                // reset approval
94: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, 0);
95: 		            } else if (router == universalRouter) {
96: 		                UniversalRouterData memory data = abi.decode(routerData, (UniversalRouterData));
97: 		                // tokens are transfered to Universalrouter directly (data.commands must include sweep action!)
98: 		                SafeERC20.safeTransfer(params.tokenIn, universalRouter, params.amountIn);
99: 		                IUniversalRouter(universalRouter).execute(data.commands, data.inputs, data.deadline);
100: 		            } else {
101: 		                revert WrongContract();
102: 		            }
103: 		
104: 		            uint256 balanceInAfter = params.tokenIn.balanceOf(address(this));
105: 		            uint256 balanceOutAfter = params.tokenOut.balanceOf(address(this));
106: 		
107: 		            amountInDelta = balanceInBefore - balanceInAfter;
108: 		            amountOutDelta = balanceOutAfter - balanceOutBefore;
109: 		
110: 		            // amountMin slippage check
111: 		            if (amountOutDelta < params.amountOutMin) {
112: 		                revert SlippageError();
113: 		            }
114: 		
115: 		            // event for any swap with exact swapped value
116: 		            emit Swap(address(params.tokenIn), address(params.tokenOut), amountInDelta, amountOutDelta);
117: 		        }
```

*GitHub* : [77-117](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L77-L117)

### [G-26]<a name="g-26"></a> `abi.encode()` is less efficient than `abi.encodepacked()` for non-address arguments

Consider refactoring the code by using `abi.encodepacked` instead of `abi.encode`, as the former is cheaper when used with non-address arguments.

*There are 4 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

401: 		        nonfungiblePositionManager.safeTransferFrom(msg.sender, address(this), tokenId, abi.encode(recipient));

424: 		        nonfungiblePositionManager.safeTransferFrom(owner, address(this), tokenId, abi.encode(recipient));
```

*GitHub* : [401](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L401), [424](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L424)

```solidity
File: src/utils/FlashloanLiquidator.sol

51: 		        bytes memory data = abi.encode(
52: 		            FlashCallbackData(
53: 		                params.tokenId,
54: 		                params.debtShares,
55: 		                liquidationCost,
56: 		                params.vault,
57: 		                IERC20(asset),
58: 		                RouterSwapParams(IERC20(token0), IERC20(asset), params.amount0In, 0, params.swapData0),
59: 		                RouterSwapParams(IERC20(token1), IERC20(asset), params.amount1In, 0, params.swapData1),
60: 		                msg.sender,
61: 		                params.minReward
62: 		            )
63: 		        );
```

*GitHub* : [51-63](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L51-L63)

```solidity
File: src/utils/Swapper.sol

139: 		                abi.encode(
140: 		                    params.swap0For1 ? params.token0 : params.token1,
141: 		                    params.swap0For1 ? params.token1 : params.token0,
142: 		                    params.fee
143: 		                )
```

*GitHub* : [139-143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L139-L143)

### [G-27]<a name="g-27"></a> Unused named return variables without optimizer waste gas

Consider changing the variable to be an unnamed one, since the variable is never assigned, nor is it returned by name. If the optimizer is not turned on, leaving the code as it is will also waste gas for the stack variable.

*There are 6 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit 
275: 		        returns (uint256 priceX96, uint256 chainlinkReferencePriceX96)
```

*GitHub* : [275](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L275)

```solidity
File: src/V3Vault.sol

// @audit address owner
258: 		    function ownerOf(uint256 tokenId) external view override returns (address owner) {

// @audit uint256 shares
289: 		    function convertToShares(uint256 assets) external view override returns (uint256 shares) {

// @audit uint256 assets
295: 		    function convertToAssets(uint256 shares) external view override returns (uint256 assets) {

// @audit uint256 newTokenId
500: 		        returns (uint256 newTokenId)
```

*GitHub* : [258](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L258), [289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L289), [295](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L295), [500](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L500)

```solidity
File: src/transformers/V3Utils.sol

// @audit uint256 newTokenId
100: 		        returns (uint256 newTokenId)
```

*GitHub* : [100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L100)

### [G-28]<a name="g-28"></a> Consider pre-calculating the address of `address(this)` to save gas

Use Foundry's [`script.sol`](https://book.getfoundry.sh/reference/forge-std/compute-create-address) or Solady's [`LibRlp.sol`](https://github.com/Vectorized/solady/blob/main/src/utils/LibRLP.sol) to save the value in a constant, which will avoid having to spend gas to push the value on the stack every time it's used.

*There are 58 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

285: 		        return IERC20(asset).balanceOf(address(this));

401: 		        nonfungiblePositionManager.safeTransferFrom(msg.sender, address(this), tokenId, abi.encode(recipient));

423: 		        nonfungiblePositionManager.permit(address(this), tokenId, deadline, v, r, s);

424: 		        nonfungiblePositionManager.safeTransferFrom(owner, address(this), tokenId, abi.encode(recipient));

435: 		        if (msg.sender != address(nonfungiblePositionManager) || from == address(this)) {

532: 		        if (owner != address(this)) {

561: 		        if (!isTransformMode && tokenOwner[tokenId] != msg.sender && address(this) != msg.sender) {

722: 		                ISignatureTransfer.SignatureTransferDetails(address(this), state.liquidatorCost),

728: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), state.liquidatorCost);

791: 		            transformer == address(0) || transformer == address(this) || transformer == asset

897: 		                permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature

901: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

982: 		                    permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature

986: 		                SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

1083: 		        nonfungiblePositionManager.safeTransferFrom(address(this), owner, tokenId);
```

*GitHub* : [728](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L728), [285](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L285), [401](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L401), [423](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L423), [424](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L424), [435](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L435), [532](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L532), [561](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L561), [722](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L722), [791](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L791), [897](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L897), [901](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L901), [982](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L982), [986](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L986), [1083](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1083)

```solidity
File: src/automators/Automator.sol

112: 		            uint256 balance = IERC20(tokens[i]).balanceOf(address(this));

128: 		        uint256 balance = address(this).balance;

209: 		            INonfungiblePositionManager.CollectParams(tokenId, address(this), type(uint128).max, type(uint128).max)
```

*GitHub* : [209](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L209), [128](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L128), [112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L112)

```solidity
File: src/transformers/AutoCompound.sol

92: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoCompound.execute.selector, params)

110: 		                params.tokenId, address(this), type(uint128).max, type(uint128).max

278: 		        uint256 allowance0 = IERC20(token0).allowance(address(this), address(nonfungiblePositionManager));

282: 		        uint256 allowance1 = IERC20(token1).allowance(address(this), address(nonfungiblePositionManager));
```

*GitHub* : [110](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L110), [92](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L92), [278](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L278), [282](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L282)

```solidity
File: src/transformers/AutoRange.sol

102: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoRange.execute.selector, params)

208: 		                address(this), // is sent to real recipient aftwards

232: 		            nonfungiblePositionManager.safeTransferFrom(address(this), state.owner, state.newTokenId);
```

*GitHub* : [232](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L232), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L102), [208](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L208)

```solidity
File: src/transformers/LeverageTransformer.sol

138: 		            address(this),
```

*GitHub* : [138](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L138)

```solidity
File: src/transformers/V3Utils.sol

106: 		        nonfungiblePositionManager.permit(address(this), tokenId, instructions.deadline, v, r, s);

367: 		        if (from == address(this)) {

376: 		        nonfungiblePositionManager.safeTransferFrom(address(this), from, tokenId, instructions.returnData);

578: 		            SafeERC20.safeTransferFrom(token0, msg.sender, address(this), needed0);

581: 		            SafeERC20.safeTransferFrom(token1, msg.sender, address(this), needed1);

584: 		            SafeERC20.safeTransferFrom(otherToken, msg.sender, address(this), neededOther);

618: 		            state.balanceBefore0 = token0.balanceOf(address(this));

619: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed0);

622: 		            state.balanceBefore1 = token1.balanceOf(address(this));

623: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed1);

626: 		            state.balanceBeforeOther = otherToken.balanceOf(address(this));

627: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.neededOther);

635: 		            if (token0.balanceOf(address(this)) - state.balanceBefore0 != state.needed0) {

640: 		            if (token1.balanceOf(address(this)) - state.balanceBefore1 != state.needed1) {

645: 		            if (otherToken.balanceOf(address(this)) - state.balanceBeforeOther != state.neededOther) {

721: 		            address(this), // is sent to real recipient aftwards

727: 		        nonfungiblePositionManager.safeTransferFrom(address(this), params.recipientNFT, tokenId, params.returnData);

896: 		        uint256 balanceBefore0 = token0.balanceOf(address(this));

897: 		        uint256 balanceBefore1 = token1.balanceOf(address(this));

899: 		            INonfungiblePositionManager.CollectParams(tokenId, address(this), collectAmount0, collectAmount1)

901: 		        uint256 balanceAfter0 = token0.balanceOf(address(this));

902: 		        uint256 balanceAfter1 = token1.balanceOf(address(this));
```

*GitHub* : [581](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L581), [584](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L584), [618](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L618), [619](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L619), [622](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L622), [623](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L623), [626](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L626), [627](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L627), [635](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L635), [640](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L640), [645](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L645), [721](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L721), [727](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L727), [896](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L896), [897](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L897), [899](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L899), [901](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L901), [902](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L902), [578](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L578), [376](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L376), [367](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L367), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L106)

```solidity
File: src/utils/FlashloanLiquidator.sol

64: 		        params.flashLoanPool.flash(address(this), isAsset0 ? liquidationCost : 0, !isAsset0 ? liquidationCost : 0, data);

75: 		                data.tokenId, data.debtShares, data.swap0.amountIn, data.swap1.amountIn, address(this), ""

89: 		            uint256 balance = data.swap0.tokenIn.balanceOf(address(this));

95: 		            uint256 balance = data.swap1.tokenIn.balanceOf(address(this));

101: 		            uint256 balance = data.asset.balanceOf(address(this));
```

*GitHub* : [101](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L101), [64](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L64), [75](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L75), [89](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L89), [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L95)

```solidity
File: src/utils/Swapper.sol

78: 		            uint256 balanceInBefore = params.tokenIn.balanceOf(address(this));

79: 		            uint256 balanceOutBefore = params.tokenOut.balanceOf(address(this));

104: 		            uint256 balanceInAfter = params.tokenIn.balanceOf(address(this));

105: 		            uint256 balanceOutAfter = params.tokenOut.balanceOf(address(this));

135: 		                address(this),
```

*GitHub* : [135](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L135), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L78), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L79), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L104), [105](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L105)

### [G-29]<a name="g-29"></a> Consider using `solady`'s token contracts to save gas

They're written using heavily-optimized assembly, and gas usage will be cheaper than other solutions.

*There are 1 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit ERC20
30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

### [G-30]<a name="g-30"></a> Consider using Solady's `FixedPointMathLib`

Saves gas, and works to avoid unnecessary [overflows](https://github.com/Vectorized/solady/blob/6cce088e69d6e46671f2f622318102bd5db77a65/src/utils/FixedPointMathLib.sol#L267).

*There are 55 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

50: 		        return debt * Q96 / (cash + debt);

67: 		            borrowRateX96 = (utilizationRateX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

69: 		            uint256 normalRateX96 = (kinkX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

71: 		            borrowRateX96 = (excessUtilX96 * jumpMultiplierPerSecondX96 / Q96) + normalRateX96;

74: 		        supplyRateX96 = utilizationRateX96 * borrowRateX96 / Q96;
```

*GitHub* : [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L71), [74](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L74), [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L50), [67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L67), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L69)

```solidity
File: src/V3Oracle.sol

120: 		        value = (price0X96 * (amount0 + fees0) / Q96 + price1X96 * (amount1 + fees1) / Q96) * Q96 / priceTokenX96;

121: 		        feeValue = (price0X96 * fees0 / Q96 + price1X96 * fees1 / Q96) * Q96 / priceTokenX96;

122: 		        price0X96 = price0X96 * Q96 / priceTokenX96;

123: 		        price1X96 = price1X96 * Q96 / priceTokenX96;

129: 		        uint256 derivedPoolPriceX96 = price0X96 * Q96 / price1X96;

144: 		            ? (priceX96 - verifyPriceX96) * 10000 / priceX96

145: 		            : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;

304: 		            chainlinkPriceX96 = (10 ** referenceTokenDecimals) * chainlinkPriceX96 * Q96 / chainlinkReferencePriceX96
305: 		                / (10 ** feedConfig.tokenDecimals);

342: 		        return uint256(answer) * Q96 / (10 ** feedConfig.feedDecimals);

353: 		            poolTWAPPriceX96 = Q96 * Q96 / priceX96;
```

*GitHub* : [129](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L129), [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L120), [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L121), [122](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L122), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L123), [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L144), [145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L145), [304-305](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L304-L305), [342](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L342), [353](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L353)

```solidity
File: src/V3Vault.sol

769: 		            _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up) * reserveProtectionFactorX32 / Q32;

1054: 		                fees0 = uint128(liquidationValue * fees0 / feeValue);

1055: 		                fees1 = uint128(liquidationValue * fees1 / feeValue);

1060: 		                liquidity = uint128((liquidationValue - feeValue) * liquidity / (fullValue - feeValue));

1100: 		        uint256 maxPenaltyValue = debt * (Q32 + MAX_LIQUIDATION_PENALTY_X32) / Q32;

1105: 		            uint256 startLiquidationValue = debt * fullValue / collateralValue;

1107: 		                (Q96 - ((fullValue - maxPenaltyValue) * Q96 / (startLiquidationValue - maxPenaltyValue)));

1108: 		            uint256 penaltyX32 = MIN_LIQUIDATION_PENALTY_X32
1109: 		                + (MAX_LIQUIDATION_PENALTY_X32 - MIN_LIQUIDATION_PENALTY_X32) * penaltyFractionX96 / Q96;

1109: 		                + (MAX_LIQUIDATION_PENALTY_X32 - MIN_LIQUIDATION_PENALTY_X32) * penaltyFractionX96 / Q96;

1111: 		            liquidationValue = debt * (Q32 + penaltyX32) / Q32;

1116: 		            uint256 penaltyValue = fullValue * (Q32 - MAX_LIQUIDATION_PENALTY_X32) / Q32;

1137: 		            newLendExchangeRateX96 = (totalLent - missing) * newLendExchangeRateX96 / totalLent;

1187: 		            newDebtExchangeRateX96 = oldDebtExchangeRateX96
1188: 		                + oldDebtExchangeRateX96 * (block.timestamp - lastRateUpdate) * borrowRateX96 / Q96;

1188: 		                + oldDebtExchangeRateX96 * (block.timestamp - lastRateUpdate) * borrowRateX96 / Q96;

1189: 		            newLendExchangeRateX96 = oldLendExchangeRateX96
1190: 		                + oldLendExchangeRateX96 * (block.timestamp - lastRateUpdate) * supplyRateX96 / Q96;

1190: 		                + oldLendExchangeRateX96 * (block.timestamp - lastRateUpdate) * supplyRateX96 / Q96;

1228: 		                    collateralValueLimitFactorX32 < type(uint32).max
1229: 		                        && _convertToAssets(tokenConfigs[token0].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1230: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1229: 		                        && _convertToAssets(tokenConfigs[token0].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1230: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1230: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1236: 		                    collateralValueLimitFactorX32 < type(uint32).max
1237: 		                        && _convertToAssets(tokenConfigs[token1].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1238: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1237: 		                        && _convertToAssets(tokenConfigs[token1].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1238: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1238: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1250: 		            uint256 lendIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)
1251: 		                * (Q32 + MAX_DAILY_LEND_INCREASE_X32) / Q32;

1262: 		            uint256 debtIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)
1263: 		                * (Q32 + MAX_DAILY_DEBT_INCREASE_X32) / Q32;
```

*GitHub* : [1109](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1109), [1111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1111), [1055](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1055), [1054](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1054), [769](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L769), [1100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1100), [1116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1116), [1137](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1137), [1187-1188](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1187-L1188), [1188](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1188), [1189-1190](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1189-L1190), [1190](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1190), [1228-1230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1228-L1230), [1229-1230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1229-L1230), [1230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1230), [1236-1238](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1236-L1238), [1237-1238](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1237-L1238), [1238](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1238), [1250-1251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1250-L1251), [1262-1263](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1262-L1263), [1105](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1105), [1060](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1060), [1107](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1107), [1108-1109](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1108-L1109)

```solidity
File: src/automators/AutoExit.sol

155: 		                state.amount0 -= state.feeAmount0 * params.rewardX64 / Q64;

156: 		                state.amount1 -= state.feeAmount1 * params.rewardX64 / Q64;

187: 		                    state.amount0 -= state.amount0 * params.rewardX64 / Q64;

189: 		                    state.amount1 -= state.amount1 * params.rewardX64 / Q64;

194: 		            state.amount0 -= (config.onlyFees ? state.feeAmount0 : state.amount0) * params.rewardX64 / Q64;

195: 		            state.amount1 -= (config.onlyFees ? state.feeAmount1 : state.amount1) * params.rewardX64 / Q64;
```

*GitHub* : [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L156), [155](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L155), [187](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L187), [189](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L189), [194](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L194), [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L195)

```solidity
File: src/transformers/AutoCompound.sol

156: 		            state.maxAddAmount0 = state.amount0 * Q64 / (rewardX64 + Q64);

157: 		            state.maxAddAmount1 = state.amount1 * Q64 / (rewardX64 + Q64);

170: 		                state.amount0Fees = state.compounded0 * rewardX64 / Q64;

171: 		                state.amount1Fees = state.compounded1 * rewardX64 / Q64;
```

*GitHub* : [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L156), [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L157), [170](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L170), [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L171)

```solidity
File: src/transformers/AutoRange.sol

143: 		            state.protocolReward0 = state.feeAmount0 * params.rewardX64 / Q64;

144: 		            state.protocolReward1 = state.feeAmount1 * params.rewardX64 / Q64;

195: 		            state.maxAddAmount0 = config.onlyFees ? state.amount0 : state.amount0 * Q64 / (params.rewardX64 + Q64);

196: 		            state.maxAddAmount1 = config.onlyFees ? state.amount1 : state.amount1 * Q64 / (params.rewardX64 + Q64);

236: 		                state.protocolReward0 = state.amountAdded0 * params.rewardX64 / Q64;

237: 		                state.protocolReward1 = state.amountAdded1 * params.rewardX64 / Q64;
```

*GitHub* : [236](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L236), [237](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L237), [143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L143), [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L144), [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L195), [196](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L196)

### [G-31]<a name="g-31"></a> Reduce deployment costs by tweaking contracts' metadata

When solidity generates the bytecode for the smart contract to be deployed, it appends metadata about the compilation at the end of the bytecode.

By default, the solidity compiler appends metadata at the end of the “actual” initcode, which gets stored to the blockchain when the constructor finishes executing.

Consider tweaking the metadata to avoid this unnecessary allocation. A full guide can be found [here](https://www.rareskills.io/post/solidity-metadata).

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

11: 		contract InterestRateModel is Ownable, IInterestRateModel, IErrors {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L11)

```solidity
File: src/V3Oracle.sol

24: 		contract V3Oracle is IV3Oracle, Ownable, IErrors {
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L24)

```solidity
File: src/V3Vault.sol

30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

```solidity
File: src/automators/AutoExit.sol

10: 		contract AutoExit is Automator {
```

*GitHub* : [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L10)

```solidity
File: src/automators/Automator.sol

19: 		abstract contract Automator is Swapper, Ownable {
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L19)

```solidity
File: src/transformers/AutoCompound.sol

16: 		contract AutoCompound is Automator, Multicall, ReentrancyGuard {
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L16)

```solidity
File: src/transformers/AutoRange.sol

11: 		contract AutoRange is Automator {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L11)

```solidity
File: src/transformers/LeverageTransformer.sol

12: 		contract LeverageTransformer is Swapper {
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L12)

```solidity
File: src/transformers/V3Utils.sol

15: 		contract V3Utils is Swapper, IERC721Receiver {
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L15)

```solidity
File: src/utils/FlashloanLiquidator.sol

11: 		contract FlashloanLiquidator is Swapper, IUniswapV3FlashCallback {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L11)

```solidity
File: src/utils/Swapper.sol

17: 		abstract contract Swapper is IUniswapV3SwapCallback, IErrors {
```

*GitHub* : [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L17)

### [G-32]<a name="g-32"></a> Emitting constants wastes gas

Every event parameter costs `Glogdata` (**8 gas**) per byte. You can avoid this extra cost, in cases where you're emitting a constant, by creating a second version of the event, which doesn't have the parameter (and have users look to the contract's variables for its value instead), and using the new event in the cases shown below.

*There are 3 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit 0
449: 		            emit Add(tokenId, owner, 0);
```

*GitHub* : [449](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L449)

```solidity
File: src/automators/AutoExit.sol

// @audit false, false, false, 0, 0, 0, 0, false, 0
208: 		        emit PositionConfigured(params.tokenId, false, false, false, 0, 0, 0, 0, false, 0);
```

*GitHub* : [208](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L208)

```solidity
File: src/transformers/AutoRange.sol

// @audit 0, 0, 0, 0, 0, 0, false, 0
266: 		            emit PositionConfigured(params.tokenId, 0, 0, 0, 0, 0, 0, false, 0);
```

*GitHub* : [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L266)

### [G-33]<a name="g-33"></a> Update OpenZeppelin dependency to save gas

Every release contains new gas optimizations, use the latest version to take advantage of this.

*There are 21 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L4)

```solidity
File: src/V3Oracle.sol

14: 		import "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

15: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [14](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L14), [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L15)

```solidity
File: src/V3Vault.sol

12: 		import "@openzeppelin/contracts/utils/math/Math.sol";

13: 		import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

14: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

15: 		import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

16: 		import "@openzeppelin/contracts/access/Ownable.sol";

17: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

18: 		import "@openzeppelin/contracts/utils/Multicall.sol";
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L16), [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L17), [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L18), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L13), [14](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L14), [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L15), [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L12)

```solidity
File: src/automators/Automator.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";

5: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

6: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

*GitHub* : [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L6), [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L5)

```solidity
File: src/transformers/AutoCompound.sol

4: 		import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

5: 		import "@openzeppelin/contracts/utils/Multicall.sol";

6: 		import "@openzeppelin/contracts/utils/math/SafeMath.sol";
```

*GitHub* : [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L5), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L6), [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L4)

```solidity
File: src/transformers/LeverageTransformer.sol

4: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

5: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L5)

```solidity
File: src/transformers/V3Utils.sol

4: 		import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

5: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L5)

```solidity
File: src/utils/Swapper.sol

4: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L4)

### [G-34]<a name="g-34"></a> Function names can be optimized

Function that are `public`/`external` and `public` state variable names can be optimized to save gas.

Method IDs that have two leading zero bytes can save **128 gas** each during deployment, and renaming functions to have lower method IDs will save **22 gas** per call, per sorted position shifted. [Reference](https://blog.emn178.cc/en/post/solidity-gas-optimization-function-name/)

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

11: 		contract InterestRateModel is Ownable, IInterestRateModel, IErrors {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L11)

```solidity
File: src/V3Oracle.sol

24: 		contract V3Oracle is IV3Oracle, Ownable, IErrors {
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L24)

```solidity
File: src/V3Vault.sol

30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

```solidity
File: src/automators/AutoExit.sol

10: 		contract AutoExit is Automator {
```

*GitHub* : [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L10)

```solidity
File: src/automators/Automator.sol

19: 		abstract contract Automator is Swapper, Ownable {
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L19)

```solidity
File: src/transformers/AutoCompound.sol

16: 		contract AutoCompound is Automator, Multicall, ReentrancyGuard {
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L16)

```solidity
File: src/transformers/AutoRange.sol

11: 		contract AutoRange is Automator {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L11)

```solidity
File: src/transformers/LeverageTransformer.sol

12: 		contract LeverageTransformer is Swapper {
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L12)

```solidity
File: src/transformers/V3Utils.sol

15: 		contract V3Utils is Swapper, IERC721Receiver {
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L15)

```solidity
File: src/utils/FlashloanLiquidator.sol

11: 		contract FlashloanLiquidator is Swapper, IUniswapV3FlashCallback {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L11)

```solidity
File: src/utils/Swapper.sol

17: 		abstract contract Swapper is IUniswapV3SwapCallback, IErrors {
```

*GitHub* : [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L17)

### [G-35]<a name="g-35"></a> Using `delete` instead of setting mapping/struct to 0 saves gas

Avoid an assignment by deleting the value instead of setting it to zero, as it's [cheaper](https://gist.github.com/DadeKuma/ea874815202fc77e9d81f81a047c1e5e).

*There are 5 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

366: 		            secondsAgos[0] = 0; // from (before)
```

*GitHub* : [366](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L366)

```solidity
File: src/V3Vault.sol

542: 		        transformedTokenId = 0;

1053: 		                liquidity = 0;
```

*GitHub* : [542](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L542), [1053](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1053)

```solidity
File: src/automators/Automator.sol

182: 		        secondsAgos[0] = 0; // from (before)
```

*GitHub* : [182](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L182)

```solidity
File: src/transformers/AutoCompound.sol

136: 		                        amountIn = 0;
```

*GitHub* : [136](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L136)

### [G-36]<a name="g-36"></a> Using `bool` for storage incurs overhead

Booleans are more expensive than `uint256` or any type that takes up a full word because each write operation emits an extra SLOAD to first read the slot's contents, replace the bits taken up by the boolean, and then write back.

This is the compiler's defense against contract upgrades and pointer aliasing, and it cannot be disabled. Use `uint256(0) and uint256(1)` for `true/false` to avoid a Gwarmaccess (**100 gas**) for the extra `SLOAD`.

*There are 4 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

163: 		    mapping(address => bool) public transformerAllowList; // contracts allowed to transform positions (selected audited contracts e.g. V3Utils)

164: 		    mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)
```

*GitHub* : [164](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L164), [163](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L163)

```solidity
File: src/automators/Automator.sol

34: 		    mapping(address => bool) public operators;

35: 		    mapping(address => bool) public vaults;
```

*GitHub* : [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L34), [35](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L35)

### [G-37]<a name="g-37"></a> Multiplication/division by two should use bit shifting

`X * 2` is equivalent to `X << 1` and `X / 2` is the same as `X >> 1`.

The `MUL` and `DIV` opcodes cost 5 gas, whereas `SHL` and `SHR` only cost 3 gas.

*There are 4 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

16: 		    uint256 public constant MAX_MULTIPLIER_X96 = Q96 * 2; // 200%

16: 		    uint256 public constant MAX_MULTIPLIER_X96 = Q96 * 2; // 200%
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L16), [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L16)

```solidity
File: src/V3Vault.sol

38: 		    uint32 public constant MIN_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 2 / 100); // 2%

38: 		    uint32 public constant MIN_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 2 / 100); // 2%
```

*GitHub* : [38](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L38), [38](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L38)

### [G-38]<a name="g-38"></a> `x += y` is more expensive than `x = x + y` for state variables

Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.

*There are 7 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

569: 		        debtSharesTotal += shares;

577: 		            dailyDebtIncreaseLimitLeft -= assets;

731: 		        debtSharesTotal -= debtShares;

913: 		            dailyLendIncreaseLimitLeft -= assets;

949: 		        dailyLendIncreaseLimitLeft += assets;

992: 		        debtSharesTotal -= shares;

995: 		        dailyDebtIncreaseLimitLeft += assets;
```

*GitHub* : [949](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L949), [992](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L992), [731](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L731), [577](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L577), [569](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L569), [995](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L995), [913](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L913)

### [G-39]<a name="g-39"></a> Use of `+=` is cheaper for mappings

Using `+=` for mappings saves 40 gas due to not having to recalculate the mapping's value's hash.

*There are 1 instance(s) of this issue:*

```solidity
File: src/transformers/AutoCompound.sol

250: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] + amount;
```

*GitHub* : [250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L250)

### [G-40]<a name="g-40"></a> Mappings are cheaper to use than storage arrays

When using storage arrays, solidity adds an internal lookup of the array's length (a **Gcoldsload 2100 gas**) to ensure you don't read past the array's end.

You can avoid this lookup by using a mapping and storing the number of entries in a separate storage variable. In cases where you have sentinel values (e.g. 'zero' means invalid), you can avoid length checks.

*There are 1 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

157: 		    mapping(address => uint256[]) private ownedTokens; // Mapping from owner address to list of owned token IDs
```

*GitHub* : [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L157)

### [G-41]<a name="g-41"></a> Use a more recent version of Solidity

v0.8.2 has a simple compiler automatic inlining

v0.8.3 has a better struct packing and cheaper multiple storage reads

v0.8.4 has custom errors, which are cheaper at deployment than revert/require strings

v0.8.10 has external calls skip contract existence checks if the external call has a return value

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L2)

```solidity
File: src/V3Oracle.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L2)

```solidity
File: src/V3Vault.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L2)

```solidity
File: src/automators/AutoExit.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L2)

```solidity
File: src/automators/Automator.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L2)

```solidity
File: src/transformers/AutoCompound.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L2)

```solidity
File: src/transformers/AutoRange.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L2)

```solidity
File: src/transformers/LeverageTransformer.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L2)

```solidity
File: src/transformers/V3Utils.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L2)

```solidity
File: src/utils/FlashloanLiquidator.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L2)

```solidity
File: src/utils/Swapper.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L2)

### [G-42]<a name="g-42"></a> `SafeMath` usage with Solidity version >`0.8.0`

Version `0.8.0` introduces internal overflow checks, so using `SafeMath` is redundant and adds overhead.

*There are 1 instance(s) of this issue:*

```solidity
File: src/transformers/AutoCompound.sol

6: 		import "@openzeppelin/contracts/utils/math/SafeMath.sol";
```

*GitHub* : [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L6)

### [G-43]<a name="g-43"></a> Constructors can be marked `payable`

`payable` functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided.

A `constructor` can safely be marked as `payable`, since only the deployer would be able to pass funds, and the project itself would not pass any funds.

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

33: 		    constructor(
```

*GitHub* : [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L33)

```solidity
File: src/V3Oracle.sol

74: 		    constructor(
```

*GitHub* : [74](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L74)

```solidity
File: src/V3Vault.sol

169: 		    constructor(
```

*GitHub* : [169](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L169)

```solidity
File: src/automators/AutoExit.sol

33: 		    constructor(
```

*GitHub* : [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L33)

```solidity
File: src/automators/Automator.sol

41: 		    constructor(
```

*GitHub* : [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L41)

```solidity
File: src/transformers/AutoCompound.sol

37: 		    constructor(
```

*GitHub* : [37](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L37)

```solidity
File: src/transformers/AutoRange.sol

25: 		    constructor(
```

*GitHub* : [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L25)

```solidity
File: src/transformers/LeverageTransformer.sol

13: 		    constructor(INonfungiblePositionManager _nonfungiblePositionManager, address _zeroxRouter, address _universalRouter)
```

*GitHub* : [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L13)

```solidity
File: src/transformers/V3Utils.sol

31: 		    constructor(
```

*GitHub* : [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L31)

```solidity
File: src/utils/FlashloanLiquidator.sol

24: 		    constructor(INonfungiblePositionManager _nonfungiblePositionManager, address _zeroxRouter, address _universalRouter)
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L24)

```solidity
File: src/utils/Swapper.sol

37: 		    constructor(
```

*GitHub* : [37](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L37)

### [G-44]<a name="g-44"></a> Nesting `if` statements that use `&&` saves gas

Using the `&&` operator on a single `if` [costs more gas](https://gist.github.com/DadeKuma/931ce6794a050201ec6544dbcc31316c) than using two nested `if`.

*There are 23 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

250: 		        if (msg.sender != emergencyAdmin && msg.sender != owner()) {
```

*GitHub* : [250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L250)

```solidity
File: src/V3Vault.sol

515: 		        if (loanOwner != msg.sender && !transformApprovals[loanOwner][tokenId][msg.sender]) {

561: 		        if (!isTransformMode && tokenOwner[tokenId] != msg.sender && address(this) != msg.sender) {

814: 		        if (msg.sender != emergencyAdmin && msg.sender != owner()) {

1228: 		                    collateralValueLimitFactorX32 < type(uint32).max
1229: 		                        && _convertToAssets(tokenConfigs[token0].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1230: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32

1236: 		                    collateralValueLimitFactorX32 < type(uint32).max
1237: 		                        && _convertToAssets(tokenConfigs[token1].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1238: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32
```

*GitHub* : [1236-1238](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1236-L1238), [814](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L814), [1228-1230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1228-L1230), [561](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L561), [515](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L515)

```solidity
File: src/automators/AutoExit.sol

113: 		            config.onlyFees && params.rewardX64 > config.maxRewardX64
114: 		                || !config.onlyFees && params.rewardX64 > config.maxRewardX64

135: 		        if (config.token0TriggerTick <= state.tick && state.tick < config.token1TriggerTick) {
```

*GitHub* : [113-114](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L113-L114), [135](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L135)

```solidity
File: src/automators/Automator.sol

219: 		        if (address(weth) == address(token) && unwrap) {
```

*GitHub* : [219](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L219)

```solidity
File: src/transformers/AutoCompound.sol

102: 		        if (!operators[msg.sender] && !vaults[msg.sender]) {
```

*GitHub* : [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L102)

```solidity
File: src/transformers/AutoRange.sol

112: 		        if (!operators[msg.sender] && !vaults[msg.sender]) {

123: 		            config.onlyFees && params.rewardX64 > config.maxRewardX64
124: 		                || !config.onlyFees && params.rewardX64 > config.maxRewardX64

149: 		        if (params.swap0To1 && params.amountIn > state.amount0 || !params.swap0To1 && params.amountIn > state.amount1) {

175: 		                baseTick + config.lowerTickDelta == state.tickLower
176: 		                    && baseTick + config.upperTickDelta == state.tickUpper
```

*GitHub* : [112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L112), [123-124](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L123-L124), [149](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L149), [175-176](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L175-L176)

```solidity
File: src/transformers/LeverageTransformer.sol

93: 		        if (token != token0 && token != token1 && amount > 0) {

146: 		        if (params.amountIn0 > 0 && token != token0) {

155: 		        if (params.amountIn1 > 0 && token != token1) {

169: 		        if (amount0 > 0 && token != token0) {

172: 		        if (amount1 > 0 && token != token1) {
```

*GitHub* : [172](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L172), [169](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L169), [155](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L155), [146](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L146), [93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L93)

```solidity
File: src/transformers/V3Utils.sol

342: 		            if (targetAmount != 0 && instructions.targetToken != address(0)) {

697: 		            amountOther > amountAddedOther && address(otherToken) != address(0) && token0 != otherToken
698: 		                && token1 != otherToken

865: 		        if (address(weth) == address(token) && unwrap) {
```

*GitHub* : [342](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L342), [865](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L865), [697-698](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L697-L698)

```solidity
File: src/utils/Swapper.sol

77: 		        if (params.amountIn != 0 && params.swapData.length != 0 && address(params.tokenOut) != address(0)) {
```

*GitHub* : [77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L77)

### [G-45]<a name="g-45"></a> Counting down when iterating, saves gas

Counting down saves **6 gas** per loop, since checks for zero are more efficient than checks against any other value.

*There are 2 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

111: 		        for (; i < count; ++i) {
```

*GitHub* : [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L111)

```solidity
File: src/transformers/AutoCompound.sol

233: 		        for (; i < count; ++i) {
```

*GitHub* : [233](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L233)

### [G-46]<a name="g-46"></a> `do-while` is cheaper than `for`-loops when the initial check can be skipped

Example:

```solidity
for (uint256 i; i < len; ++i){ ... } -> do { ...; ++i } while (i < len);
```

*There are 2 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

111: 		        for (; i < count; ++i) {
```

*GitHub* : [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L111)

```solidity
File: src/transformers/AutoCompound.sol

233: 		        for (; i < count; ++i) {
```

*GitHub* : [233](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L233)

### [G-47]<a name="g-47"></a> Lack of `unchecked` in loops

Use `unchecked` to increment the loop variable as it can save gas:

```solidity
for(uint256 i; i < length;) {
	unchecked{
		++i;
	}
}
```

*There are 2 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

111: 		        for (; i < count; ++i) {
```

*GitHub* : [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L111)

```solidity
File: src/transformers/AutoCompound.sol

233: 		        for (; i < count; ++i) {
```

*GitHub* : [233](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L233)

### [G-48]<a name="g-48"></a> `uint` comparison with zero can be cheaper

Checking for `!= 0` is cheaper than `> 0` for unsigned integers.

*There are 56 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

431: 		        if (state.liquidity > 0) {
```

*GitHub* : [431](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L431)

```solidity
File: src/V3Vault.sol

443: 		            if (data.length > 0) {

505: 		        if (transformedTokenId > 0) {

552: 		            transformedTokenId > 0 && transformedTokenId == tokenId && transformerAllowList[msg.sender];

615: 		        if (transformedTokenId > 0) {

687: 		        if (transformedTokenId > 0) {

712: 		        if (state.reserveCost > 0) {

717: 		        if (params.permitData.length > 0) {

778: 		        if (amount > 0) {

893: 		        if (permitData.length > 0) {

977: 		        if (assets > 0) {

978: 		            if (permitData.length > 0) {

1064: 		        if (liquidity > 0) {

1186: 		        if (lastRateUpdate > 0) {
```

*GitHub* : [778](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L778), [443](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L443), [505](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L505), [552](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L552), [615](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L615), [687](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L687), [712](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L712), [717](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L717), [893](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L893), [977](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L977), [978](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L978), [1064](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1064), [1186](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1186)

```solidity
File: src/automators/AutoExit.sol

199: 		        if (state.amount0 > 0) {

202: 		        if (state.amount1 > 0) {
```

*GitHub* : [202](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L202), [199](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L199)

```solidity
File: src/automators/Automator.sol

113: 		            if (balance > 0) {

129: 		        if (balance > 0) {

200: 		        if (liquidity > 0) {
```

*GitHub* : [129](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L129), [200](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L200), [113](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L113)

```solidity
File: src/transformers/AutoCompound.sol

123: 		        if (state.amount0 > 0 || state.amount1 > 0) {

123: 		        if (state.amount0 > 0 || state.amount1 > 0) {

127: 		            if (amountIn > 0) {

133: 		                if (tSecs > 0) {

140: 		                if (amountIn > 0) {

160: 		            if (state.maxAddAmount0 > 0 || state.maxAddAmount1 > 0) {

160: 		            if (state.maxAddAmount0 > 0 || state.maxAddAmount1 > 0) {

212: 		        if (balance0 > 0) {

216: 		        if (balance1 > 0) {
```

*GitHub* : [140](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L140), [160](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L160), [160](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L160), [212](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L212), [216](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L216), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L123), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L123), [127](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L127), [133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L133)

```solidity
File: src/transformers/AutoRange.sol

243: 		            if (state.amount0 - state.amountAdded0 > 0) {

246: 		            if (state.amount1 - state.amountAdded1 > 0) {
```

*GitHub* : [246](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L246), [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L243)

```solidity
File: src/transformers/LeverageTransformer.sol

52: 		        if (params.amountIn0 > 0) {

64: 		        if (params.amountIn1 > 0) {

93: 		        if (token != token0 && token != token1 && amount > 0) {

146: 		        if (params.amountIn0 > 0 && token != token0) {

155: 		        if (params.amountIn1 > 0 && token != token1) {

169: 		        if (amount0 > 0 && token != token0) {

172: 		        if (amount1 > 0 && token != token1) {
```

*GitHub* : [155](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L155), [169](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L169), [172](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L172), [93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L93), [146](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L146), [52](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L52), [64](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L64)

```solidity
File: src/transformers/V3Utils.sol

402: 		        if (params.permitData.length > 0) {

476: 		        if (params.permitData.length > 0) {

539: 		        if (params.permitData.length > 0) {

577: 		        if (needed0 > 0) {

580: 		        if (needed1 > 0) {

583: 		        if (neededOther > 0) {

617: 		        if (state.needed0 > 0) {

621: 		        if (state.needed1 > 0) {

625: 		        if (state.neededOther > 0) {

634: 		        if (state.needed0 > 0) {

639: 		        if (state.needed1 > 0) {

644: 		        if (state.neededOther > 0) {
```

*GitHub* : [577](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L577), [583](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L583), [617](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L617), [621](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L621), [625](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L625), [634](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L634), [639](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L639), [644](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L644), [402](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L402), [539](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L539), [580](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L580), [476](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L476)

```solidity
File: src/utils/FlashloanLiquidator.sol

90: 		            if (balance > 0) {

96: 		            if (balance > 0) {

105: 		            if (balance > 0) {
```

*GitHub* : [90](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L90), [96](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L96), [105](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L105)

```solidity
File: src/utils/Swapper.sol

133: 		        if (params.amountIn > 0) {

157: 		        require(amount0Delta > 0 || amount1Delta > 0); // swaps entirely within 0-liquidity regions are not supported

157: 		        require(amount0Delta > 0 || amount1Delta > 0); // swaps entirely within 0-liquidity regions are not supported

166: 		        uint256 amountToPay = amount0Delta > 0 ? uint256(amount0Delta) : uint256(amount1Delta);
```

*GitHub* : [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L166), [133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L133), [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L157), [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L157)

### [G-49]<a name="g-49"></a> Use assembly to check for `address(0)`

[A simple zero address check](https://medium.com/@kalexotsu/solidity-assembly-checking-if-an-address-is-0-efficiently-d2bfe071331) can be written in assembly to save some gas.

*There are 14 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

791: 		            transformer == address(0) || transformer == address(this) || transformer == asset
792: 		                || transformer == address(nonfungiblePositionManager)

791: 		            transformer == address(0) || transformer == address(this) || transformer == asset

791: 		            transformer == address(0) || transformer == address(this) || transformer == asset

791: 		            transformer == address(0) || transformer == address(this) || transformer == asset
```

*GitHub* : [791](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L791), [791-792](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L791-L792), [791](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L791), [791](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L791)

```solidity
File: src/automators/Automator.sol

236: 		        if (vault != address(0)) {
```

*GitHub* : [236](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L236)

```solidity
File: src/transformers/V3Utils.sol

342: 		            if (targetAmount != 0 && instructions.targetToken != address(0)) {

342: 		            if (targetAmount != 0 && instructions.targetToken != address(0)) {

697: 		            amountOther > amountAddedOther && address(otherToken) != address(0) && token0 != otherToken
698: 		                && token1 != otherToken

697: 		            amountOther > amountAddedOther && address(otherToken) != address(0) && token0 != otherToken

697: 		            amountOther > amountAddedOther && address(otherToken) != address(0) && token0 != otherToken

697: 		            amountOther > amountAddedOther && address(otherToken) != address(0) && token0 != otherToken

805: 		        } else if (address(params.swapSourceToken) != address(0)) {
```

*GitHub* : [697](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L697), [697](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L697), [805](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L805), [697](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L697), [697-698](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L697-L698), [342](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L342), [342](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L342)

```solidity
File: src/utils/Swapper.sol

77: 		        if (params.amountIn != 0 && params.swapData.length != 0 && address(params.tokenOut) != address(0)) {

77: 		        if (params.amountIn != 0 && params.swapData.length != 0 && address(params.tokenOut) != address(0)) {
```

*GitHub* : [77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L77), [77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L77)

### [G-50]<a name="g-50"></a> Use scratch space for building calldata with assembly

If an external call's calldata can fit into two or fewer words, use the scratch space to build the calldata, rather than allowing Solidity to do a memory expansion.

*There are 124 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

80: 		        factory = _nonfungiblePositionManager.factory();

82: 		        referenceTokenDecimals = IERC20Metadata(_referenceToken).decimals();

215: 		        uint8 feedDecimals = feed.decimals();

216: 		        uint8 tokenDecimals = IERC20Metadata(token).decimals();

225: 		            address token0 = pool.token0();

226: 		            address token1 = pool.token1();

337: 		        (, int256 answer,, uint256 updatedAt,) = feedConfig.feed.latestRoundData();

363: 		            (sqrtPriceX96,,,,,,) = pool.slot0();

368: 		            (int56[] memory tickCumulatives,) = pool.observe(secondsAgos); // pool observe may fail when there is not enough history available (only use pool with enough history!)

370: 		            sqrtPriceX96 = TickMath.getSqrtRatioAtTick(tick);

409: 		        ) = nonfungiblePositionManager.positions(tokenId);

422: 		        (state.sqrtPriceX96, state.tick,,,,,) = state.pool.slot0();

432: 		            state.sqrtPriceX96Lower = TickMath.getSqrtRatioAtTick(state.tickLower);

433: 		            state.sqrtPriceX96Upper = TickMath.getSqrtRatioAtTick(state.tickUpper);

455: 		            position.pool.feeGrowthGlobal0X128(),

456: 		            position.pool.feeGrowthGlobal1X128()

480: 		        (,, uint256 lowerFeeGrowthOutside0X128, uint256 lowerFeeGrowthOutside1X128,,,,) = pool.ticks(tickLower);

481: 		        (,, uint256 upperFeeGrowthOutside0X128, uint256 upperFeeGrowthOutside1X128,,,,) = pool.ticks(tickUpper);

500: 		        return IUniswapV3Pool(PoolAddress.computeAddress(factory, PoolAddress.getPoolKey(tokenA, tokenB, fee)));
```

*GitHub* : [225](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L225), [226](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L226), [337](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L337), [363](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L363), [368](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L368), [370](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L370), [409](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L409), [422](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L422), [432](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L432), [433](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L433), [455](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L455), [456](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L456), [480](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L480), [481](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L481), [500](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L500), [80](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L80), [215](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L215), [82](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L82), [216](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L216)

```solidity
File: src/V3Vault.sol

179: 		        assetDecimals = IERC20Metadata(_asset).decimals();

181: 		        factory = IUniswapV3Factory(_nonfungiblePositionManager.factory());

285: 		        return IERC20(asset).balanceOf(address(this));

520: 		        nonfungiblePositionManager.approve(transformer, tokenId);

522: 		        (bool success,) = transformer.call(data);

531: 		        address owner = nonfungiblePositionManager.ownerOf(tokenId);

537: 		        nonfungiblePositionManager.approve(address(0), tokenId);

627: 		        (amount0, amount1) = nonfungiblePositionManager.decreaseLiquidity(
628: 		            INonfungiblePositionManager.DecreaseLiquidityParams(
629: 		                params.tokenId, params.liquidity, params.amount0Min, params.amount1Min, params.deadline
630: 		            )
631: 		        );

636: 		            params.feeAmount0 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount0 + params.feeAmount0),

637: 		            params.feeAmount1 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount1 + params.feeAmount1)

640: 		        (amount0, amount1) = nonfungiblePositionManager.collect(collectParams);

722: 		                ISignatureTransfer.SignatureTransferDetails(address(this), state.liquidatorCost),

897: 		                permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature

982: 		                    permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature

1045: 		            (,,,,,,, liquidity,,,,) = nonfungiblePositionManager.positions(tokenId);

1049: 		            (,,, liquidity,,, fees0, fees1) = oracle.getPositionBreakdown(tokenId);

1065: 		            nonfungiblePositionManager.decreaseLiquidity(
1066: 		                INonfungiblePositionManager.DecreaseLiquidityParams(tokenId, liquidity, 0, 0, block.timestamp)
1067: 		            );

1070: 		        (amount0, amount1) = nonfungiblePositionManager.collect(
1071: 		            INonfungiblePositionManager.CollectParams(tokenId, recipient, fees0, fees1)
1072: 		        );

1144: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(tokenId);

1179: 		        (uint256 borrowRateX96, uint256 supplyRateX96) = interestRateModel.getRatesPerSecondX96(available, debt);

1181: 		        supplyRateX96 = supplyRateX96.mulDiv(Q32 - reserveFactorX32, Q32);

1213: 		            (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(tokenId);

1217: 		                tokenConfigs[token0].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);

1218: 		                tokenConfigs[token1].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);

1220: 		                tokenConfigs[token0].totalDebtShares += SafeCast.toUint192(newShares - oldShares);

1221: 		                tokenConfigs[token1].totalDebtShares += SafeCast.toUint192(newShares - oldShares);

1275: 		        (fullValue, feeValue,,) = oracle.getValue(tokenId, address(asset));

1277: 		        collateralValue = fullValue.mulDiv(collateralFactorX32, Q32);
```

*GitHub* : [897](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L897), [179](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L179), [181](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L181), [285](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L285), [520](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L520), [522](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L522), [531](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L531), [537](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L537), [627-631](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L627-L631), [636](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L636), [637](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L637), [640](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L640), [722](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L722), [982](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L982), [1045](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1045), [1049](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1049), [1065-1067](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1065-L1067), [1070-1072](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1070-L1072), [1144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1144), [1179](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1179), [1181](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1181), [1213](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1213), [1217](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1217), [1218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1218), [1220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1220), [1221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1221), [1275](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1275), [1277](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1277)

```solidity
File: src/automators/AutoExit.sol

121: 		            nonfungiblePositionManager.positions(params.tokenId);

132: 		        (, state.tick,,,,,) = state.pool.slot0();

198: 		        state.owner = nonfungiblePositionManager.ownerOf(params.tokenId);

219: 		        address owner = nonfungiblePositionManager.ownerOf(tokenId);
```

*GitHub* : [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L121), [132](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L132), [198](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L198), [219](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L219)

```solidity
File: src/automators/Automator.sol

112: 		            uint256 balance = IERC20(tokens[i]).balanceOf(address(this));

148: 		        (sqrtPriceX96, currentTick,,,,,) = pool.slot0();

186: 		        try pool.observe(secondsAgos) returns (int56[] memory tickCumulatives, uint160[] memory) {

202: 		            (feeAmount0, feeAmount1) = nonfungiblePositionManager.decreaseLiquidity(
203: 		                INonfungiblePositionManager.DecreaseLiquidityParams(
204: 		                    tokenId, liquidity, amountRemoveMin0, amountRemoveMin1, deadline
205: 		                )
206: 		            );

208: 		        (amount0, amount1) = nonfungiblePositionManager.collect(
209: 		            INonfungiblePositionManager.CollectParams(tokenId, address(this), type(uint128).max, type(uint128).max)
210: 		        );

220: 		            weth.withdraw(amount);

240: 		            owner = IVault(vault).ownerOf(tokenId);

242: 		            owner = nonfungiblePositionManager.ownerOf(tokenId);
```

*GitHub* : [148](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L148), [242](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L242), [240](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L240), [220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L220), [208-210](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L208-L210), [202-206](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L202-L206), [112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L112), [186](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L186)

```solidity
File: src/transformers/AutoCompound.sol

108: 		        (state.amount0, state.amount1) = nonfungiblePositionManager.collect(
109: 		            INonfungiblePositionManager.CollectParams(
110: 		                params.tokenId, address(this), type(uint128).max, type(uint128).max
111: 		            )
112: 		        );

116: 		            nonfungiblePositionManager.positions(params.tokenId);

129: 		                (state.sqrtPriceX96, state.tick,,,,,) = pool.slot0();

163: 		                (, state.compounded0, state.compounded1) = nonfungiblePositionManager.increaseLiquidity(
164: 		                    INonfungiblePositionManager.IncreaseLiquidityParams(
165: 		                        params.tokenId, state.maxAddAmount0, state.maxAddAmount1, 0, 0, block.timestamp
166: 		                    )
167: 		                );

201: 		        address owner = nonfungiblePositionManager.ownerOf(tokenId);

203: 		            owner = IVault(owner).ownerOf(tokenId);

209: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(tokenId);

278: 		        uint256 allowance0 = IERC20(token0).allowance(address(this), address(nonfungiblePositionManager));

282: 		        uint256 allowance1 = IERC20(token1).allowance(address(this), address(nonfungiblePositionManager));
```

*GitHub* : [209](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L209), [116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L116), [108-112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L108-L112), [203](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L203), [201](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L201), [163-167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L163-L167), [129](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L129), [282](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L282), [278](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L278)

```solidity
File: src/transformers/AutoRange.sol

131: 		            nonfungiblePositionManager.positions(params.tokenId);

202: 		                SafeCast.toInt24(baseTick + config.lowerTickDelta), // reverts if out of valid range

203: 		                SafeCast.toInt24(baseTick + config.upperTickDelta), // reverts if out of valid range

217: 		            (state.newTokenId,, state.amountAdded0, state.amountAdded1) = nonfungiblePositionManager.mint(mintParams);

223: 		            state.owner = nonfungiblePositionManager.ownerOf(params.tokenId);

228: 		                state.realOwner = IVault(state.owner).ownerOf(params.tokenId);

308: 		            int24 spacing = IUniswapV3Factory(factory).feeAmountTickSpacing(fee);
```

*GitHub* : [131](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L131), [202](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L202), [203](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L203), [217](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L217), [223](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L223), [228](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L228), [308](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L308)

```solidity
File: src/transformers/LeverageTransformer.sol

43: 		        address token = IVault(msg.sender).asset();

45: 		        IVault(msg.sender).borrow(params.tokenId, amount);

47: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(params.tokenId);

84: 		        (, uint256 added0, uint256 added1) = nonfungiblePositionManager.increaseLiquidity(increaseLiquidityParams);

124: 		        address token = IVault(msg.sender).asset();

125: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(params.tokenId);

134: 		        (amount0, amount1) = nonfungiblePositionManager.decreaseLiquidity(decreaseLiquidityParams);

139: 		            params.feeAmount0 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount0 + params.feeAmount0),

140: 		            params.feeAmount1 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount1 + params.feeAmount1)

142: 		        (amount0, amount1) = nonfungiblePositionManager.collect(collectParams);
```

*GitHub* : [124](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L124), [125](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L125), [134](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L134), [84](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L84), [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L47), [45](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L45), [43](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L43), [142](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L142), [140](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L140), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L139)

```solidity
File: src/transformers/V3Utils.sol

102: 		        if (nonfungiblePositionManager.ownerOf(tokenId) != msg.sender) {

116: 		        (,, address token0, address token1,,,, uint128 liquidity,,,,) = nonfungiblePositionManager.positions(tokenId);

135: 		                : (amount0 + instructions.feeAmount0).toUint128(),

138: 		                : (amount1 + instructions.feeAmount1).toUint128()

537: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(params.tokenId);

618: 		            state.balanceBefore0 = token0.balanceOf(address(this));

619: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed0);

622: 		            state.balanceBefore1 = token1.balanceOf(address(this));

623: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed1);

626: 		            state.balanceBeforeOther = otherToken.balanceOf(address(this));

627: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.neededOther);

635: 		            if (token0.balanceOf(address(this)) - state.balanceBefore0 != state.needed0) {

640: 		            if (token1.balanceOf(address(this)) - state.balanceBefore1 != state.needed1) {

645: 		            if (otherToken.balanceOf(address(this)) - state.balanceBeforeOther != state.neededOther) {

726: 		        (tokenId, liquidity, added0, added1) = nonfungiblePositionManager.mint(mintParams);

771: 		        (liquidity, added0, added1) = nonfungiblePositionManager.increaseLiquidity(increaseLiquidityParams);

866: 		            weth.withdraw(amount);

885: 		            (amount0, amount1) = nonfungiblePositionManager.decreaseLiquidity(
886: 		                INonfungiblePositionManager.DecreaseLiquidityParams(tokenId, liquidity, token0Min, token1Min, deadline)
887: 		            );

896: 		        uint256 balanceBefore0 = token0.balanceOf(address(this));

897: 		        uint256 balanceBefore1 = token1.balanceOf(address(this));

898: 		        (amount0, amount1) = nonfungiblePositionManager.collect(
899: 		            INonfungiblePositionManager.CollectParams(tokenId, address(this), collectAmount0, collectAmount1)
900: 		        );

901: 		        uint256 balanceAfter0 = token0.balanceOf(address(this));

902: 		        uint256 balanceAfter1 = token1.balanceOf(address(this));
```

*GitHub* : [901](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L901), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L102), [116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L116), [135](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L135), [138](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L138), [537](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L537), [618](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L618), [619](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L619), [622](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L622), [623](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L623), [626](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L626), [627](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L627), [635](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L635), [640](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L640), [645](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L645), [726](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L726), [771](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L771), [866](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L866), [885-887](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L885-L887), [896](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L896), [897](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L897), [898-900](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L898-L900), [902](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L902)

```solidity
File: src/utils/FlashloanLiquidator.sol

42: 		        (,,, uint256 liquidationCost,) = params.vault.loanInfo(params.tokenId);

47: 		        (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(params.tokenId);

48: 		        address asset = params.vault.asset();

50: 		        bool isAsset0 = params.flashLoanPool.token0() == asset;

73: 		        data.vault.liquidate(
74: 		            IVault.LiquidateParams(
75: 		                data.tokenId, data.debtShares, data.swap0.amountIn, data.swap1.amountIn, address(this), ""
76: 		            )
77: 		        );

89: 		            uint256 balance = data.swap0.tokenIn.balanceOf(address(this));

95: 		            uint256 balance = data.swap1.tokenIn.balanceOf(address(this));

101: 		            uint256 balance = data.asset.balanceOf(address(this));
```

*GitHub* : [73-77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L73-L77), [89](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L89), [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L95), [101](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L101), [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L50), [48](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L48), [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L47), [42](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L42)

```solidity
File: src/utils/Swapper.sol

42: 		        weth = IWETH9(_nonfungiblePositionManager.WETH9());

43: 		        factory = _nonfungiblePositionManager.factory();

78: 		            uint256 balanceInBefore = params.tokenIn.balanceOf(address(this));

79: 		            uint256 balanceOutBefore = params.tokenOut.balanceOf(address(this));

89: 		                (bool success,) = zeroxRouter.call(data.data);

104: 		            uint256 balanceInAfter = params.tokenIn.balanceOf(address(this));

105: 		            uint256 balanceOutAfter = params.tokenOut.balanceOf(address(this));

172: 		        return IUniswapV3Pool(PoolAddress.computeAddress(address(factory), PoolAddress.getPoolKey(tokenA, tokenB, fee)));
```

*GitHub* : [89](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L89), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L104), [105](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L105), [172](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L172), [42](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L42), [43](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L43), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L78), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L79)

### [G-51]<a name="g-51"></a> Use assembly to validate `msg.sender`

It is possible to use assembly to efficiently validate `msg.sender` with the least amount of opcodes. For more details check the [following report](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender).

*There are 26 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

250: 		        if (msg.sender != emergencyAdmin && msg.sender != owner()) {
```

*GitHub* : [250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L250)

```solidity
File: src/V3Vault.sol

419: 		        if (msg.sender != owner) {

435: 		        if (msg.sender != address(nonfungiblePositionManager) || from == address(this)) {

484: 		        if (tokenOwner[tokenId] != msg.sender) {

515: 		        if (loanOwner != msg.sender && !transformApprovals[loanOwner][tokenId][msg.sender]) {

561: 		        if (!isTransformMode && tokenOwner[tokenId] != msg.sender && address(this) != msg.sender) {

621: 		        if (owner != msg.sender) {

814: 		        if (msg.sender != emergencyAdmin && msg.sender != owner()) {

935: 		        if (msg.sender != owner) {
```

*GitHub* : [561](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L561), [621](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L621), [814](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L814), [935](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L935), [515](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L515), [435](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L435), [484](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L484), [419](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L419)

```solidity
File: src/automators/AutoExit.sol

101: 		        if (!operators[msg.sender]) {

220: 		        if (owner != msg.sender) {
```

*GitHub* : [220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L220), [101](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L101)

```solidity
File: src/automators/Automator.sol

105: 		        if (msg.sender != withdrawer) {

124: 		        if (msg.sender != withdrawer) {

232: 		        if (vaults[msg.sender]) {

245: 		        if (owner != msg.sender) {

252: 		        if (msg.sender != address(weth)) {
```

*GitHub* : [105](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L105), [124](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L124), [232](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L232), [245](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L245), [252](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L252)

```solidity
File: src/transformers/AutoCompound.sol

88: 		        if (!operators[msg.sender] || !vaults[vault]) {

102: 		        if (!operators[msg.sender] && !vaults[msg.sender]) {

205: 		        if (owner != msg.sender) {

228: 		        if (msg.sender != withdrawer) {
```

*GitHub* : [88](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L88), [228](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L228), [205](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L205), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L102)

```solidity
File: src/transformers/AutoRange.sol

98: 		        if (!operators[msg.sender] || !vaults[vault]) {

112: 		        if (!operators[msg.sender] && !vaults[msg.sender]) {
```

*GitHub* : [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L98), [112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L112)

```solidity
File: src/transformers/V3Utils.sol

102: 		        if (nonfungiblePositionManager.ownerOf(tokenId) != msg.sender) {

362: 		        if (msg.sender != address(nonfungiblePositionManager)) {

915: 		        if (msg.sender != address(weth)) {
```

*GitHub* : [915](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L915), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L102), [362](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L362)

```solidity
File: src/utils/Swapper.sol

161: 		        if (address(_getPool(tokenIn, tokenOut, fee)) != msg.sender) {
```

*GitHub* : [161](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L161)

### [G-52]<a name="g-52"></a> Use assembly to write `address` storage values

Using assembly `{ sstore(state.slot, addr)` instead of `state = addr` can save gas.

*There are 13 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

80: 		        factory = _nonfungiblePositionManager.factory();

81: 		        referenceToken = _referenceToken;

83: 		        chainlinkReferenceToken = _chainlinkReferenceToken;

266: 		        emergencyAdmin = admin;
```

*GitHub* : [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L266), [80](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L80), [81](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L81), [83](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L83)

```solidity
File: src/V3Vault.sol

178: 		        asset = _asset;

181: 		        factory = IUniswapV3Factory(_nonfungiblePositionManager.factory());

871: 		        emergencyAdmin = admin;
```

*GitHub* : [181](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L181), [871](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L871), [178](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L178)

```solidity
File: src/automators/Automator.sol

61: 		        withdrawer = _withdrawer;
```

*GitHub* : [61](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L61)

```solidity
File: src/transformers/V3Utils.sol

37: 		        permit2 = IPermit2(_permit2);
```

*GitHub* : [37](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L37)

```solidity
File: src/utils/Swapper.sol

42: 		        weth = IWETH9(_nonfungiblePositionManager.WETH9());

43: 		        factory = _nonfungiblePositionManager.factory();

45: 		        zeroxRouter = _zeroxRouter;

46: 		        universalRouter = _universalRouter;
```

*GitHub* : [46](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L46), [45](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L45), [43](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L43), [42](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L42)

### [G-53]<a name="g-53"></a> Use assembly to emit an `event`

To efficiently emit events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.

However, it's important to note that in order to safely optimize this process, it is preferable to cache and restore the free memory pointer.

A good example of such practice can be seen in [Solady's](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167) codebase.

*There are 49 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

100: 		        emit SetValues(baseRatePerYearX96, multiplierPerYearX96, jumpMultiplierPerYearX96, _kinkX96);
```

*GitHub* : [100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L100)

```solidity
File: src/V3Oracle.sol

190: 		        emit SetMaxPoolPriceDifference(_maxPoolPriceDifference);

242: 		        emit TokenConfigUpdated(token, config);

243: 		        emit OracleModeUpdated(token, mode);

260: 		        emit OracleModeUpdated(token, mode);

267: 		        emit SetEmergencyAdmin(admin);
```

*GitHub* : [260](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L260), [267](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L267), [190](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L190), [242](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L242), [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L243)

```solidity
File: src/V3Vault.sol

449: 		            emit Add(tokenId, owner, 0);

464: 		                emit Add(tokenId, owner, oldTokenId);

489: 		        emit ApprovedTransform(tokenId, msg.sender, target, isActive);

601: 		        emit Borrow(tokenId, owner, assets, shares);

645: 		        emit WithdrawCollateral(params.tokenId, owner, params.recipient, params.liquidity, amount0, amount1);

746: 		        emit Liquidate(
747: 		            params.tokenId,
748: 		            msg.sender,
749: 		            owner,
750: 		            state.fullValue,
751: 		            state.liquidatorCost,
752: 		            amount0,
753: 		            amount1,
754: 		            state.reserveCost,
755: 		            state.missing
756: 		        );

782: 		        emit WithdrawReserves(amount, receiver);

798: 		        emit SetTransformer(transformer, active);

830: 		        emit SetLimits(
831: 		            _minLoanSize, _globalLendLimit, _globalDebtLimit, _dailyLendIncreaseLimitMin, _dailyDebtIncreaseLimitMin
832: 		        );

839: 		        emit SetReserveFactor(_reserveFactorX32);

849: 		        emit SetReserveProtectionFactor(_reserveProtectionFactorX32);

865: 		        emit SetTokenConfig(token, collateralFactorX32, collateralValueLimitFactorX32);

872: 		        emit SetEmergencyAdmin(admin);

916: 		        emit Deposit(msg.sender, receiver, assets, shares);

951: 		        emit Withdraw(msg.sender, receiver, owner, assets, shares);

1013: 		        emit Repay(tokenId, msg.sender, owner, assets, shares);

1084: 		        emit Remove(tokenId, owner);

1139: 		            emit ExchangeRateUpdate(newDebtExchangeRateX96, newLendExchangeRateX96);

1160: 		            emit ExchangeRateUpdate(newDebtExchangeRateX96, newLendExchangeRateX96);
```

*GitHub* : [645](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L645), [449](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L449), [464](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L464), [489](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L489), [601](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L601), [746-756](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L746-L756), [782](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L782), [798](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L798), [830-832](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L830-L832), [839](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L839), [849](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L849), [865](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L865), [872](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L872), [916](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L916), [951](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L951), [1013](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1013), [1084](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1084), [1139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1139), [1160](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1160)

```solidity
File: src/automators/AutoExit.sol

208: 		        emit PositionConfigured(params.tokenId, false, false, false, 0, 0, 0, 0, false, 0);

211: 		        emit Executed(
212: 		            params.tokenId, msg.sender, state.isSwap, state.amount0, state.amount1, state.token0, state.token1
213: 		        );

232: 		        emit PositionConfigured(
233: 		            tokenId,
234: 		            config.isActive,
235: 		            config.token0Swap,
236: 		            config.token1Swap,
237: 		            config.token0TriggerTick,
238: 		            config.token1TriggerTick,
239: 		            config.token0SlippageX64,
240: 		            config.token1SlippageX64,
241: 		            config.onlyFees,
242: 		            config.maxRewardX64
243: 		        );
```

*GitHub* : [208](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L208), [211-213](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L211-L213), [232-243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L232-L243)

```solidity
File: src/automators/Automator.sol

60: 		        emit WithdrawerChanged(_withdrawer);

70: 		        emit OperatorChanged(_operator, _active);

80: 		        emit VaultChanged(_vault, _active);

94: 		        emit TWAPConfigChanged(_TWAPSeconds, _maxTWAPTickDifference);
```

*GitHub* : [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L70), [80](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L80), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L94), [60](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L60)

```solidity
File: src/transformers/AutoCompound.sol

183: 		        emit AutoCompounded(
184: 		            msg.sender,
185: 		            params.tokenId,
186: 		            state.compounded0,
187: 		            state.compounded1,
188: 		            state.amount0Fees,
189: 		            state.amount1Fees,
190: 		            state.token0,
191: 		            state.token1
192: 		        );

246: 		        emit RewardUpdated(msg.sender, _totalRewardX64);

251: 		        emit BalanceAdded(tokenId, token, amount);

259: 		                emit BalanceAdded(tokenId, token, amount - currentBalance);

261: 		                emit BalanceRemoved(tokenId, token, currentBalance - amount);

271: 		        emit BalanceRemoved(tokenId, token, amount);

273: 		        emit BalanceWithdrawn(tokenId, token, to, amount);
```

*GitHub* : [261](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L261), [271](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L271), [273](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L273), [183-192](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L183-L192), [251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L251), [246](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L246), [259](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L259)

```solidity
File: src/transformers/AutoRange.sol

252: 		            emit PositionConfigured(
253: 		                state.newTokenId,
254: 		                config.lowerTickLimit,
255: 		                config.upperTickLimit,
256: 		                config.lowerTickDelta,
257: 		                config.upperTickDelta,
258: 		                config.token0SlippageX64,
259: 		                config.token1SlippageX64,
260: 		                config.onlyFees,
261: 		                config.maxRewardX64
262: 		            );

266: 		            emit PositionConfigured(params.tokenId, 0, 0, 0, 0, 0, 0, false, 0);

268: 		            emit RangeChanged(params.tokenId, state.newTokenId);

286: 		        emit PositionConfigured(
287: 		            tokenId,
288: 		            config.lowerTickLimit,
289: 		            config.upperTickLimit,
290: 		            config.lowerTickDelta,
291: 		            config.upperTickDelta,
292: 		            config.token0SlippageX64,
293: 		            config.token1SlippageX64,
294: 		            config.onlyFees,
295: 		            config.maxRewardX64
296: 		        );
```

*GitHub* : [286-296](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L286-L296), [268](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L268), [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L266), [252-262](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L252-L262)

```solidity
File: src/transformers/V3Utils.sol

218: 		            emit CompoundFees(tokenId, liquidity, amount0, amount1);

303: 		            emit ChangeRange(tokenId, newTokenId);

348: 		            emit WithdrawAndCollectAndSwap(tokenId, instructions.targetToken, targetAmount);

729: 		        emit SwapAndMint(tokenId, liquidity, added0, added1);

773: 		        emit SwapAndIncreaseLiquidity(params.tokenId, liquidity, added0, added1);
```

*GitHub* : [773](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L773), [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L218), [303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L303), [348](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L348), [729](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L729)

```solidity
File: src/utils/Swapper.sol

116: 		            emit Swap(address(params.tokenIn), address(params.tokenOut), amountInDelta, amountOutDelta);
```

*GitHub* : [116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L116)

### NonCritical Risk Issues

### [N-01]<a name="n-01"></a> Fee-on-transfer/rebasing tokens will have problems when swapping

The Uniswap v3 protocol does not provide support for rebasing or fee-on-transfer tokens. Consequently, attempting to utilize such tokens with Uniswap v3 may lead to failed transfers after a swap due to insufficient tokens or result in the contract having a remaining balance following the transfer.

*There are 1 instance(s) of this issue:*

```solidity
File: src/utils/Swapper.sol

134: 		            (int256 amount0Delta, int256 amount1Delta) = params.pool.swap(
135: 		                address(this),
136: 		                params.swap0For1,
137: 		                int256(params.amountIn),
138: 		                (params.swap0For1 ? TickMath.MIN_SQRT_RATIO + 1 : TickMath.MAX_SQRT_RATIO - 1),
139: 		                abi.encode(
140: 		                    params.swap0For1 ? params.token0 : params.token1,
141: 		                    params.swap0For1 ? params.token1 : params.token0,
142: 		                    params.fee
143: 		                )
144: 		            );
```

*GitHub* : [134-144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L134-L144)

### [N-02]<a name="n-02"></a> `unchecked` blocks with subtractions may underflow

There aren't any checks to avoid an underflow which can happen inside an `unchecked` block, so the following subtractions may underflow silently.

*There are 10 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit feeGrowthInside0LastX128 - position.feeGrowthInside0LastX128
463: 		            feeGrowth0 = feeGrowthInside0LastX128 - position.feeGrowthInside0LastX128;

// @audit feeGrowthInside1LastX128 - position.feeGrowthInside1LastX128
464: 		            feeGrowth1 = feeGrowthInside1LastX128 - position.feeGrowthInside1LastX128;

// @audit lowerFeeGrowthOutside0X128 - upperFeeGrowthOutside0X128
486: 		                feeGrowthInside0X128 = lowerFeeGrowthOutside0X128 - upperFeeGrowthOutside0X128;

// @audit lowerFeeGrowthOutside1X128 - upperFeeGrowthOutside1X128
487: 		                feeGrowthInside1X128 = lowerFeeGrowthOutside1X128 - upperFeeGrowthOutside1X128;

// @audit feeGrowthGlobal0X128 - lowerFeeGrowthOutside0X128 - upperFeeGrowthOutside0X128
489: 		                feeGrowthInside0X128 = feeGrowthGlobal0X128 - lowerFeeGrowthOutside0X128 - upperFeeGrowthOutside0X128;

// @audit feeGrowthGlobal0X128 - lowerFeeGrowthOutside0X128
489: 		                feeGrowthInside0X128 = feeGrowthGlobal0X128 - lowerFeeGrowthOutside0X128 - upperFeeGrowthOutside0X128;

// @audit feeGrowthGlobal1X128 - lowerFeeGrowthOutside1X128 - upperFeeGrowthOutside1X128
490: 		                feeGrowthInside1X128 = feeGrowthGlobal1X128 - lowerFeeGrowthOutside1X128 - upperFeeGrowthOutside1X128;

// @audit feeGrowthGlobal1X128 - lowerFeeGrowthOutside1X128
490: 		                feeGrowthInside1X128 = feeGrowthGlobal1X128 - lowerFeeGrowthOutside1X128 - upperFeeGrowthOutside1X128;

// @audit upperFeeGrowthOutside0X128 - lowerFeeGrowthOutside0X128
492: 		                feeGrowthInside0X128 = upperFeeGrowthOutside0X128 - lowerFeeGrowthOutside0X128;

// @audit upperFeeGrowthOutside1X128 - lowerFeeGrowthOutside1X128
493: 		                feeGrowthInside1X128 = upperFeeGrowthOutside1X128 - lowerFeeGrowthOutside1X128;
```

*GitHub* : [463](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L463), [464](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L464), [486](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L486), [487](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L487), [489](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L489), [489](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L489), [490](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L490), [490](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L490), [492](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L492), [493](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L493)

### [N-03]<a name="n-03"></a> Some functions do not work correctly with fee-on-transfer tokens

Some tokens take a transfer fee (e.g. `STA`, `PAXG`), some do not currently charge a fee but may do so in the future (e.g. `USDT`, `USDC`).

Should a fee-on-transfer token be added as an asset and deposited, it could be abused, as the accounting is wrong. In the current implementation the following function calls do not work well with fee-on-transfer tokens as the amount variable is the pre-fee amount, including the fee, whereas the final balance do not include the fee anymore.

*There are 6 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

728: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), state.liquidatorCost);

901: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

986: 		                SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);
```

*GitHub* : [901](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L901), [728](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L728), [986](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L986)

```solidity
File: src/transformers/V3Utils.sol

578: 		            SafeERC20.safeTransferFrom(token0, msg.sender, address(this), needed0);

581: 		            SafeERC20.safeTransferFrom(token1, msg.sender, address(this), needed1);

584: 		            SafeERC20.safeTransferFrom(otherToken, msg.sender, address(this), neededOther);
```

*GitHub* : [578](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L578), [581](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L581), [584](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L584)

### [N-04]<a name="n-04"></a> Some functions do not work correctly with rebasing tokens

A rebasing token is an asset whose supply is algorithmically adjusted to control its price. Examples of such tokens include YAM, RMPL, and BASED.

If any of these tokens are used in the following contracts, the rewards will accumulate within the contract holding the tokens, making them inaccessible for withdrawal by the original depositor.

*There are 4 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

685: 		    function liquidate(LiquidateParams calldata params) external override returns (uint256 amount0, uint256 amount1) {
686: 		        // liquidation is not allowed during transformer mode
687: 		        if (transformedTokenId > 0) {
688: 		            revert TransformNotAllowed();
689: 		        }
690: 		
691: 		        LiquidateState memory state;
692: 		
693: 		        (state.newDebtExchangeRateX96, state.newLendExchangeRateX96) = _updateGlobalInterest();
694: 		
695: 		        uint256 debtShares = loans[params.tokenId].debtShares;
696: 		        if (debtShares != params.debtShares) {
697: 		            revert DebtChanged();
698: 		        }
699: 		
700: 		        state.debt = _convertToAssets(debtShares, state.newDebtExchangeRateX96, Math.Rounding.Up);
701: 		
702: 		        (state.isHealthy, state.fullValue, state.collateralValue, state.feeValue) =
703: 		            _checkLoanIsHealthy(params.tokenId, state.debt);
704: 		        if (state.isHealthy) {
705: 		            revert NotLiquidatable();
706: 		        }
707: 		
708: 		        (state.liquidationValue, state.liquidatorCost, state.reserveCost) =
709: 		            _calculateLiquidation(state.debt, state.fullValue, state.collateralValue);
710: 		
711: 		        // calculate reserve (before transfering liquidation money - otherwise calculation is off)
712: 		        if (state.reserveCost > 0) {
713: 		            state.missing =
714: 		                _handleReserveLiquidation(state.reserveCost, state.newDebtExchangeRateX96, state.newLendExchangeRateX96);
715: 		        }
716: 		
717: 		        if (params.permitData.length > 0) {
718: 		            (ISignatureTransfer.PermitTransferFrom memory permit, bytes memory signature) =
719: 		                abi.decode(params.permitData, (ISignatureTransfer.PermitTransferFrom, bytes));
720: 		            permit2.permitTransferFrom(
721: 		                permit,
722: 		                ISignatureTransfer.SignatureTransferDetails(address(this), state.liquidatorCost),
723: 		                msg.sender,
724: 		                signature
725: 		            );
726: 		        } else {
727: 		            // take value from liquidator
728: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), state.liquidatorCost);
729: 		        }
730: 		
731: 		        debtSharesTotal -= debtShares;
732: 		
733: 		        // send promised collateral tokens to liquidator
734: 		        (amount0, amount1) =
735: 		            _sendPositionValue(params.tokenId, state.liquidationValue, state.fullValue, state.feeValue, msg.sender);
736: 		
737: 		        if (amount0 < params.amount0Min || amount1 < params.amount1Min) {
738: 		            revert SlippageError();
739: 		        }
740: 		
741: 		        address owner = tokenOwner[params.tokenId];
742: 		
743: 		        // disarm loan and send remaining position to owner
744: 		        _cleanupLoan(params.tokenId, state.newDebtExchangeRateX96, state.newLendExchangeRateX96, owner);
745: 		
746: 		        emit Liquidate(
747: 		            params.tokenId,
748: 		            msg.sender,
749: 		            owner,
750: 		            state.fullValue,
751: 		            state.liquidatorCost,
752: 		            amount0,
753: 		            amount1,
754: 		            state.reserveCost,
755: 		            state.missing
756: 		        );
757: 		    }

877: 		    function _deposit(address receiver, uint256 amount, bool isShare, bytes memory permitData)
878: 		        internal
879: 		        returns (uint256 assets, uint256 shares)
880: 		    {
881: 		        (, uint256 newLendExchangeRateX96) = _updateGlobalInterest();
882: 		
883: 		        _resetDailyLendIncreaseLimit(newLendExchangeRateX96, false);
884: 		
885: 		        if (isShare) {
886: 		            shares = amount;
887: 		            assets = _convertToAssets(shares, newLendExchangeRateX96, Math.Rounding.Up);
888: 		        } else {
889: 		            assets = amount;
890: 		            shares = _convertToShares(assets, newLendExchangeRateX96, Math.Rounding.Down);
891: 		        }
892: 		
893: 		        if (permitData.length > 0) {
894: 		            (ISignatureTransfer.PermitTransferFrom memory permit, bytes memory signature) =
895: 		                abi.decode(permitData, (ISignatureTransfer.PermitTransferFrom, bytes));
896: 		            permit2.permitTransferFrom(
897: 		                permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature
898: 		            );
899: 		        } else {
900: 		            // fails if not enough token approved
901: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);
902: 		        }
903: 		
904: 		        _mint(receiver, shares);
905: 		
906: 		        if (totalSupply() > globalLendLimit) {
907: 		            revert GlobalLendLimit();
908: 		        }
909: 		
910: 		        if (assets > dailyLendIncreaseLimitLeft) {
911: 		            revert DailyLendIncreaseLimit();
912: 		        } else {
913: 		            dailyLendIncreaseLimitLeft -= assets;
914: 		        }
915: 		
916: 		        emit Deposit(msg.sender, receiver, assets, shares);
917: 		    }

954: 		    function _repay(uint256 tokenId, uint256 amount, bool isShare, bytes memory permitData) internal {
955: 		        (uint256 newDebtExchangeRateX96, uint256 newLendExchangeRateX96) = _updateGlobalInterest();
956: 		
957: 		        Loan storage loan = loans[tokenId];
958: 		
959: 		        uint256 currentShares = loan.debtShares;
960: 		
961: 		        uint256 shares;
962: 		        uint256 assets;
963: 		
964: 		        if (isShare) {
965: 		            shares = amount;
966: 		            assets = _convertToAssets(amount, newDebtExchangeRateX96, Math.Rounding.Up);
967: 		        } else {
968: 		            assets = amount;
969: 		            shares = _convertToShares(amount, newDebtExchangeRateX96, Math.Rounding.Down);
970: 		        }
971: 		
972: 		        // fails if too much repayed
973: 		        if (shares > currentShares) {
974: 		            revert RepayExceedsDebt();
975: 		        }
976: 		
977: 		        if (assets > 0) {
978: 		            if (permitData.length > 0) {
979: 		                (ISignatureTransfer.PermitTransferFrom memory permit, bytes memory signature) =
980: 		                    abi.decode(permitData, (ISignatureTransfer.PermitTransferFrom, bytes));
981: 		                permit2.permitTransferFrom(
982: 		                    permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature
983: 		                );
984: 		            } else {
985: 		                // fails if not enough token approved
986: 		                SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);
987: 		            }
988: 		        }
989: 		
990: 		        uint256 loanDebtShares = loan.debtShares - shares;
991: 		        loan.debtShares = loanDebtShares;
992: 		        debtSharesTotal -= shares;
993: 		
994: 		        // when amounts are repayed - they maybe borrowed again
995: 		        dailyDebtIncreaseLimitLeft += assets;
996: 		
997: 		        _updateAndCheckCollateral(
998: 		            tokenId, newDebtExchangeRateX96, newLendExchangeRateX96, loanDebtShares + shares, loanDebtShares
999: 		        );
1000: 		
1001: 		        address owner = tokenOwner[tokenId];
1002: 		
1003: 		        // if fully repayed
1004: 		        if (currentShares == shares) {
1005: 		            _cleanupLoan(tokenId, newDebtExchangeRateX96, newLendExchangeRateX96, owner);
1006: 		        } else {
1007: 		            // if resulting loan is too small - revert
1008: 		            if (_convertToAssets(loanDebtShares, newDebtExchangeRateX96, Math.Rounding.Up) < minLoanSize) {
1009: 		                revert MinLoanSize();
1010: 		            }
1011: 		        }
1012: 		
1013: 		        emit Repay(tokenId, msg.sender, owner, assets, shares);
1014: 		    }
```

*GitHub* : [685-757](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L685-L757), [877-917](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L877-L917), [954-1014](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L954-L1014)

```solidity
File: src/transformers/V3Utils.sol

566: 		    function _prepareAddApproved(
567: 		        IERC20 token0,
568: 		        IERC20 token1,
569: 		        IERC20 otherToken,
570: 		        uint256 amount0,
571: 		        uint256 amount1,
572: 		        uint256 amountOther
573: 		    ) internal {
574: 		        (uint256 needed0, uint256 needed1, uint256 neededOther) =
575: 		            _prepareAdd(token0, token1, otherToken, amount0, amount1, amountOther);
576: 		
577: 		        if (needed0 > 0) {
578: 		            SafeERC20.safeTransferFrom(token0, msg.sender, address(this), needed0);
579: 		        }
580: 		        if (needed1 > 0) {
581: 		            SafeERC20.safeTransferFrom(token1, msg.sender, address(this), needed1);
582: 		        }
583: 		        if (neededOther > 0) {
584: 		            SafeERC20.safeTransferFrom(otherToken, msg.sender, address(this), neededOther);
585: 		        }
586: 		    }
```

*GitHub* : [566-586](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L566-L586)

### [N-05]<a name="n-05"></a> Custom `error` should be used rather than `require`/`assert`

Custom errors are available from solidity version 0.8.4. Custom errors are more easily processed in try-catch blocks, and are easier to re-use and maintain.

*There are 3 instance(s) of this issue:*

```solidity
File: src/transformers/AutoCompound.sol

244: 		        require(_totalRewardX64 <= totalRewardX64, ">totalRewardX64");

269: 		        require(amount <= balance, "amount>balance");
```

*GitHub* : [244](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L244), [269](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L269)

```solidity
File: src/utils/Swapper.sol

157: 		        require(amount0Delta > 0 || amount1Delta > 0); // swaps entirely within 0-liquidity regions are not supported
```

*GitHub* : [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L157)

### [N-06]<a name="n-06"></a> High cyclomatic complexity

Consider breaking down these blocks into more manageable units, by splitting things into utility functions, by reducing nesting, and by using early returns.

*There are 12 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

272: 		    function _getReferenceTokenPriceX96(address token, uint256 cachedChainlinkReferencePriceX96)
```

*GitHub* : [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L272)

```solidity
File: src/V3Vault.sol

550: 		    function borrow(uint256 tokenId, uint256 assets) external override {

685: 		    function liquidate(LiquidateParams calldata params) external override returns (uint256 amount0, uint256 amount1) {

954: 		    function _repay(uint256 tokenId, uint256 amount, bool isShare, bytes memory permitData) internal {
```

*GitHub* : [550](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L550), [685](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L685), [954](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L954)

```solidity
File: src/automators/AutoExit.sol

100: 		    function execute(ExecuteParams calldata params) external {
```

*GitHub* : [100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L100)

```solidity
File: src/transformers/AutoCompound.sol

101: 		    function execute(ExecuteParams calldata params) external nonReentrant {
```

*GitHub* : [101](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L101)

```solidity
File: src/transformers/AutoRange.sol

111: 		    function execute(ExecuteParams calldata params) external {
```

*GitHub* : [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L111)

```solidity
File: src/transformers/LeverageTransformer.sol

40: 		    function leverageUp(LeverageUpParams calldata params) external {

123: 		    function leverageDown(LeverageDownParams calldata params) external {
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L40), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L123)

```solidity
File: src/transformers/V3Utils.sol

115: 		    function execute(uint256 tokenId, Instructions memory instructions) public returns (uint256 newTokenId) {

598: 		    function _prepareAddPermit2(

779: 		    function _swapAndPrepareAmounts(SwapAndMintParams memory params, bool unwrap)
```

*GitHub* : [115](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L115), [598](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L598), [779](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L779)

### [N-07]<a name="n-07"></a> Missing events in sensitive functions

Events should be emitted when sensitive changes are made to the contracts, but some functions lack them.

*There are 1 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

1205: 		    function _updateAndCheckCollateral(
1206: 		        uint256 tokenId,
1207: 		        uint256 debtExchangeRateX96,
1208: 		        uint256 lendExchangeRateX96,
1209: 		        uint256 oldShares,
1210: 		        uint256 newShares
1211: 		    ) internal {
1212: 		        if (oldShares != newShares) {
1213: 		            (,, address token0, address token1,,,,,,,,) = nonfungiblePositionManager.positions(tokenId);
1214: 		
1215: 		            // remove previous collateral - add new collateral
1216: 		            if (oldShares > newShares) {
1217: 		                tokenConfigs[token0].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);
1218: 		                tokenConfigs[token1].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);
1219: 		            } else {
1220: 		                tokenConfigs[token0].totalDebtShares += SafeCast.toUint192(newShares - oldShares);
1221: 		                tokenConfigs[token1].totalDebtShares += SafeCast.toUint192(newShares - oldShares);
1222: 		
1223: 		                // check if current value of used collateral is more than allowed limit
1224: 		                // if collateral is decreased - never revert
1225: 		                uint256 lentAssets = _convertToAssets(totalSupply(), lendExchangeRateX96, Math.Rounding.Up);
1226: 		                uint256 collateralValueLimitFactorX32 = tokenConfigs[token0].collateralValueLimitFactorX32;
1227: 		                if (
1228: 		                    collateralValueLimitFactorX32 < type(uint32).max
1229: 		                        && _convertToAssets(tokenConfigs[token0].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1230: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32
1231: 		                ) {
1232: 		                    revert CollateralValueLimit();
1233: 		                }
1234: 		                collateralValueLimitFactorX32 = tokenConfigs[token1].collateralValueLimitFactorX32;
1235: 		                if (
1236: 		                    collateralValueLimitFactorX32 < type(uint32).max
1237: 		                        && _convertToAssets(tokenConfigs[token1].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)
1238: 		                            > lentAssets * collateralValueLimitFactorX32 / Q32
1239: 		                ) {
1240: 		                    revert CollateralValueLimit();
1241: 		                }
1242: 		            }
1243: 		        }
1244: 		    }
```

*GitHub* : [1205-1244](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1205-L1244)

### [N-08]<a name="n-08"></a> Missing events in initializers

As a best practice, consider emitting an event when the contract is initialized. In this way, it's easy for the user to track the exact point in time when the contract was initialized, by filtering the emitted events.

*There are 1 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

395: 		    function _initializeState(uint256 tokenId) internal view returns (PositionState memory state) {
```

*GitHub* : [395](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L395)

### [N-09]<a name="n-09"></a> Consider emitting an event at the end of the constructor

This will allow users to easily exactly pinpoint when and by whom a contract was constructed.

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

33: 		    constructor(
```

*GitHub* : [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L33)

```solidity
File: src/V3Oracle.sol

74: 		    constructor(
```

*GitHub* : [74](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L74)

```solidity
File: src/V3Vault.sol

169: 		    constructor(
```

*GitHub* : [169](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L169)

```solidity
File: src/automators/AutoExit.sol

33: 		    constructor(
```

*GitHub* : [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L33)

```solidity
File: src/automators/Automator.sol

41: 		    constructor(
```

*GitHub* : [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L41)

```solidity
File: src/transformers/AutoCompound.sol

37: 		    constructor(
```

*GitHub* : [37](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L37)

```solidity
File: src/transformers/AutoRange.sol

25: 		    constructor(
```

*GitHub* : [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L25)

```solidity
File: src/transformers/LeverageTransformer.sol

13: 		    constructor(INonfungiblePositionManager _nonfungiblePositionManager, address _zeroxRouter, address _universalRouter)
```

*GitHub* : [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L13)

```solidity
File: src/transformers/V3Utils.sol

31: 		    constructor(
```

*GitHub* : [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L31)

```solidity
File: src/utils/FlashloanLiquidator.sol

24: 		    constructor(INonfungiblePositionManager _nonfungiblePositionManager, address _zeroxRouter, address _universalRouter)
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L24)

```solidity
File: src/utils/Swapper.sol

37: 		    constructor(
```

*GitHub* : [37](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L37)

### [N-10]<a name="n-10"></a> Setters should prevent re-setting the same value

Not only is wasteful in terms of gas, but this is especially problematic when an event is emitted and the old and new values set are the same, as listeners might not expect this kind of scenario.

*There are 16 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit baseRatePerSecondX96, multiplierPerSecondX96, jumpMultiplierPerSecondX96, kinkX96
82: 		    function setValues(
```

*GitHub* : [82](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L82)

```solidity
File: src/V3Oracle.sol

// @audit maxPoolPriceDifference
185: 		    function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

// @audit feedConfigs
201: 		    function setTokenConfig(

// @audit emergencyAdmin
265: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [185](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L185), [201](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L201), [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L265)

```solidity
File: src/V3Vault.sol

// @audit transformerAllowList
788: 		    function setTransformer(address transformer, bool active) external onlyOwner {

// @audit minLoanSize, globalLendLimit, globalDebtLimit, dailyLendIncreaseLimitMin, dailyDebtIncreaseLimitMin
807: 		    function setLimits(

// @audit reserveFactorX32
837: 		    function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

// @audit reserveProtectionFactorX32
844: 		    function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

// @audit emergencyAdmin
870: 		    function setEmergencyAdmin(address admin) external onlyOwner {

// @audit lastDebtExchangeRateX96, lastLendExchangeRateX96, lastExchangeRateUpdate
1150: 		    function _updateGlobalInterest()
```

*GitHub* : [788](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L788), [807](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L807), [837](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L837), [844](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L844), [870](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L870), [1150](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1150)

```solidity
File: src/automators/Automator.sol

// @audit withdrawer
59: 		    function setWithdrawer(address _withdrawer) public onlyOwner {

// @audit operators
69: 		    function setOperator(address _operator, bool _active) public onlyOwner {

// @audit vaults
79: 		    function setVault(address _vault, bool _active) public onlyOwner {

// @audit TWAPSeconds, maxTWAPTickDifference
87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {
```

*GitHub* : [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L59), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L69), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L79), [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87)

```solidity
File: src/transformers/AutoCompound.sol

// @audit totalRewardX64
243: 		    function setReward(uint64 _totalRewardX64) external onlyOwner {

// @audit positionBalances
254: 		    function _setBalance(uint256 tokenId, address token, uint256 amount) internal {
```

*GitHub* : [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L243), [254](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L254)

### [N-11]<a name="n-11"></a> Using zero as a parameter

Taking zero as a valid argument without checks can lead to severe security issues in some cases.

If using a zero argument is mandatory, consider using descriptive constants or an enum instead of passing zero directly on function calls, as that might be error-prone, to fully describe the caller's intention.

*There are 32 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

135: 		        uint256 priceX96 = _getReferencePoolPriceX96(pool, 0);

235: 		            config = TokenConfig(
236: 		                feed, maxFeedAge, feedDecimals, tokenDecimals, IUniswapV3Pool(address(0)), false, 0, Mode.CHAINLINK, 0
237: 		            );
```

*GitHub* : [135](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L135), [235-237](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L235-L237)

```solidity
File: src/V3Vault.sol

446: 		            loans[tokenId] = Loan(0);

449: 		            emit Add(tokenId, owner, 0);

470: 		                _updateAndCheckCollateral(
471: 		                    tokenId, debtExchangeRateX96, lendExchangeRateX96, 0, loans[tokenId].debtShares
472: 		                );

1066: 		                INonfungiblePositionManager.DecreaseLiquidityParams(tokenId, liquidity, 0, 0, block.timestamp)

1081: 		        _updateAndCheckCollateral(tokenId, debtExchangeRateX96, lendExchangeRateX96, loans[tokenId].debtShares, 0);
```

*GitHub* : [446](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L446), [449](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L449), [470-472](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L470-L472), [1066](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1066), [1081](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1081)

```solidity
File: src/automators/AutoExit.sol

208: 		        emit PositionConfigured(params.tokenId, false, false, false, 0, 0, 0, 0, false, 0);
```

*GitHub* : [208](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L208)

```solidity
File: src/transformers/AutoCompound.sol

143: 		                        Swapper.PoolSwapParams(
144: 		                            pool, IERC20(state.token0), IERC20(state.token1), state.fee, params.swap0To1, amountIn, 0
145: 		                        )

164: 		                    INonfungiblePositionManager.IncreaseLiquidityParams(
165: 		                        params.tokenId, state.maxAddAmount0, state.maxAddAmount1, 0, 0, block.timestamp
166: 		                    )

179: 		            _increaseBalance(0, state.token0, state.amount0Fees);

180: 		            _increaseBalance(0, state.token1, state.amount1Fees);

235: 		            _withdrawBalanceInternal(0, tokens[i], to, balance, balance);
```

*GitHub* : [235](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L235), [143-145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L143-L145), [164-166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L164-L166), [179](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L179), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L180)

```solidity
File: src/transformers/AutoRange.sol

198: 		            INonfungiblePositionManager.MintParams memory mintParams = INonfungiblePositionManager.MintParams(
199: 		                address(state.token0),
200: 		                address(state.token1),
201: 		                state.fee,
202: 		                SafeCast.toInt24(baseTick + config.lowerTickDelta), // reverts if out of valid range
203: 		                SafeCast.toInt24(baseTick + config.upperTickDelta), // reverts if out of valid range
204: 		                state.maxAddAmount0,
205: 		                state.maxAddAmount1,
206: 		                0,
207: 		                0,
208: 		                address(this), // is sent to real recipient aftwards
209: 		                params.deadline
210: 		            );

220: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), 0);

221: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), 0);

266: 		            emit PositionConfigured(params.tokenId, 0, 0, 0, 0, 0, 0, false, 0);
```

*GitHub* : [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L221), [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L266), [198-210](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L198-L210), [220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L220)

```solidity
File: src/transformers/V3Utils.sol

149: 		                    SwapAndIncreaseLiquidityParams(
150: 		                        tokenId,
151: 		                        amount0,
152: 		                        amount1,
153: 		                        instructions.recipient,
154: 		                        instructions.deadline,
155: 		                        IERC20(token1),
156: 		                        instructions.amountIn1,
157: 		                        instructions.amountOut1Min,
158: 		                        instructions.swapData1,
159: 		                        0,
160: 		                        0,
161: 		                        "",
162: 		                        instructions.amountAddMin0,
163: 		                        instructions.amountAddMin1,
164: 		                        ""
165: 		                    ),

172: 		                    SwapAndIncreaseLiquidityParams(
173: 		                        tokenId,
174: 		                        amount0,
175: 		                        amount1,
176: 		                        instructions.recipient,
177: 		                        instructions.deadline,
178: 		                        IERC20(token0),
179: 		                        0,
180: 		                        0,
181: 		                        "",
182: 		                        instructions.amountIn0,
183: 		                        instructions.amountOut0Min,
184: 		                        instructions.swapData0,
185: 		                        instructions.amountAddMin0,
186: 		                        instructions.amountAddMin1,
187: 		                        ""
188: 		                    ),

196: 		                    SwapAndIncreaseLiquidityParams(
197: 		                        tokenId,
198: 		                        amount0,
199: 		                        amount1,
200: 		                        instructions.recipient,
201: 		                        instructions.deadline,
202: 		                        IERC20(address(0)),
203: 		                        0,
204: 		                        0,
205: 		                        "",
206: 		                        0,
207: 		                        0,
208: 		                        "",
209: 		                        instructions.amountAddMin0,
210: 		                        instructions.amountAddMin1,
211: 		                        ""
212: 		                    ),

222: 		                    SwapAndMintParams(
223: 		                        IERC20(token0),
224: 		                        IERC20(token1),
225: 		                        instructions.fee,
226: 		                        instructions.tickLower,
227: 		                        instructions.tickUpper,
228: 		                        amount0,
229: 		                        amount1,
230: 		                        instructions.recipient,
231: 		                        instructions.recipientNFT,
232: 		                        instructions.deadline,
233: 		                        IERC20(token1),
234: 		                        instructions.amountIn1,
235: 		                        instructions.amountOut1Min,
236: 		                        instructions.swapData1,
237: 		                        0,
238: 		                        0,
239: 		                        "",
240: 		                        instructions.amountAddMin0,
241: 		                        instructions.amountAddMin1,
242: 		                        instructions.swapAndMintReturnData,
243: 		                        ""
244: 		                    ),

249: 		                    SwapAndMintParams(
250: 		                        IERC20(token0),
251: 		                        IERC20(token1),
252: 		                        instructions.fee,
253: 		                        instructions.tickLower,
254: 		                        instructions.tickUpper,
255: 		                        amount0,
256: 		                        amount1,
257: 		                        instructions.recipient,
258: 		                        instructions.recipientNFT,
259: 		                        instructions.deadline,
260: 		                        IERC20(token0),
261: 		                        0,
262: 		                        0,
263: 		                        "",
264: 		                        instructions.amountIn0,
265: 		                        instructions.amountOut0Min,
266: 		                        instructions.swapData0,
267: 		                        instructions.amountAddMin0,
268: 		                        instructions.amountAddMin1,
269: 		                        instructions.swapAndMintReturnData,
270: 		                        ""
271: 		                    ),

277: 		                    SwapAndMintParams(
278: 		                        IERC20(token0),
279: 		                        IERC20(token1),
280: 		                        instructions.fee,
281: 		                        instructions.tickLower,
282: 		                        instructions.tickUpper,
283: 		                        amount0,
284: 		                        amount1,
285: 		                        instructions.recipient,
286: 		                        instructions.recipientNFT,
287: 		                        instructions.deadline,
288: 		                        IERC20(address(0)),
289: 		                        0,
290: 		                        0,
291: 		                        "",
292: 		                        0,
293: 		                        0,
294: 		                        "",
295: 		                        instructions.amountAddMin0,
296: 		                        instructions.amountAddMin1,
297: 		                        instructions.swapAndMintReturnData,
298: 		                        ""
299: 		                    ),

405: 		            _prepareAddPermit2(
406: 		                params.tokenIn, IERC20(address(0)), IERC20(address(0)), params.amountIn, 0, 0, pbtf, signature
407: 		            );

409: 		            _prepareAddApproved(params.tokenIn, IERC20(address(0)), IERC20(address(0)), params.amountIn, 0, 0);

740: 		            SwapAndMintParams(
741: 		                token0,
742: 		                token1,
743: 		                0,
744: 		                0,
745: 		                0,
746: 		                params.amount0,
747: 		                params.amount1,
748: 		                params.recipient,
749: 		                params.recipient,
750: 		                params.deadline,
751: 		                params.swapSourceToken,
752: 		                params.amountIn0,
753: 		                params.amountOut0Min,
754: 		                params.swapData0,
755: 		                params.amountIn1,
756: 		                params.amountOut1Min,
757: 		                params.swapData1,
758: 		                params.amountAddMin0,
759: 		                params.amountAddMin1,
760: 		                "",
761: 		                params.permitData
762: 		            ),

831: 		            SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), 0);

835: 		            SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), 0);
```

*GitHub* : [222-244](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L222-L244), [249-271](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L249-L271), [277-299](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L277-L299), [405-407](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L405-L407), [409](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L409), [740-762](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L740-L762), [835](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L835), [831](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L831), [149-165](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L149-L165), [172-188](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L172-L188), [196-212](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L196-L212)

```solidity
File: src/utils/FlashloanLiquidator.sol

58: 		                RouterSwapParams(IERC20(token0), IERC20(asset), params.amount0In, 0, params.swapData0),

59: 		                RouterSwapParams(IERC20(token1), IERC20(asset), params.amount1In, 0, params.swapData1),

78: 		        SafeERC20.safeApprove(data.asset, address(data.vault), 0);
```

*GitHub* : [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L59), [58](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L58), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L78)

```solidity
File: src/utils/Swapper.sol

94: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, 0);
```

*GitHub* : [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L94)

### [N-12]<a name="n-12"></a> Named imports of parent contracts are missing

Parent contracts should use [named imports](https://docs.soliditylang.org/en/latest/layout-of-source-files.html#syntax-and-semantics) to improve the code readability.

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit Ownable, IInterestRateModel, IErrors
11: 		contract InterestRateModel is Ownable, IInterestRateModel, IErrors {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L11)

```solidity
File: src/V3Oracle.sol

// @audit IV3Oracle, Ownable, IErrors
24: 		contract V3Oracle is IV3Oracle, Ownable, IErrors {
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L24)

```solidity
File: src/V3Vault.sol

// @audit ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors
30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

```solidity
File: src/automators/AutoExit.sol

// @audit Automator
10: 		contract AutoExit is Automator {
```

*GitHub* : [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L10)

```solidity
File: src/automators/Automator.sol

// @audit Swapper, Ownable
19: 		abstract contract Automator is Swapper, Ownable {
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L19)

```solidity
File: src/transformers/AutoCompound.sol

// @audit Automator, Multicall, ReentrancyGuard
16: 		contract AutoCompound is Automator, Multicall, ReentrancyGuard {
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L16)

```solidity
File: src/transformers/AutoRange.sol

// @audit Automator
11: 		contract AutoRange is Automator {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L11)

```solidity
File: src/transformers/LeverageTransformer.sol

// @audit Swapper
12: 		contract LeverageTransformer is Swapper {
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L12)

```solidity
File: src/transformers/V3Utils.sol

// @audit Swapper, IERC721Receiver
15: 		contract V3Utils is Swapper, IERC721Receiver {
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L15)

```solidity
File: src/utils/FlashloanLiquidator.sol

// @audit Swapper, IUniswapV3FlashCallback
11: 		contract FlashloanLiquidator is Swapper, IUniswapV3FlashCallback {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L11)

```solidity
File: src/utils/Swapper.sol

// @audit IUniswapV3SwapCallback, IErrors
17: 		abstract contract Swapper is IUniswapV3SwapCallback, IErrors {
```

*GitHub* : [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L17)

### [N-13]<a name="n-13"></a> Unused named `return`

Declaring named returns, but not using them, is confusing to the reader. Consider either completely removing them (by declaring just the type without a name), or remove the return statement and do a variable assignment.

This would improve the readability of the code, and it may also help reduce regressions during future code refactors.

*There are 5 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

258: 		    function ownerOf(uint256 tokenId) external view override returns (address owner) {
259: 		        return tokenOwner[tokenId];

289: 		    function convertToShares(uint256 assets) external view override returns (uint256 shares) {

291: 		        return _convertToShares(assets, lendExchangeRateX96, Math.Rounding.Down);

295: 		    function convertToAssets(uint256 shares) external view override returns (uint256 assets) {

297: 		        return _convertToAssets(shares, lendExchangeRateX96, Math.Rounding.Down);

500: 		        returns (uint256 newTokenId)

544: 		        return tokenId;
```

*GitHub* : [289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L289), [258](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L258), [295](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L295), [500](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L500)

```solidity
File: src/transformers/V3Utils.sol

100: 		        returns (uint256 newTokenId)

107: 		        return execute(tokenId, instructions);
```

*GitHub* : [100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L100)

### [N-14]<a name="n-14"></a> OpenZeppelin libraries should be upgraded to a newer version

These contracts import some OpenZeppelin libraries, but they are using an old version.

*There are 21 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L4)

```solidity
File: src/V3Oracle.sol

14: 		import "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

15: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L15), [14](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L14)

```solidity
File: src/V3Vault.sol

12: 		import "@openzeppelin/contracts/utils/math/Math.sol";

13: 		import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

14: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

15: 		import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

16: 		import "@openzeppelin/contracts/access/Ownable.sol";

17: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

18: 		import "@openzeppelin/contracts/utils/Multicall.sol";
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L15), [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L16), [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L17), [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L18), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L13), [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L12), [14](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L14)

```solidity
File: src/automators/Automator.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";

5: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

6: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

*GitHub* : [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L6), [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L5)

```solidity
File: src/transformers/AutoCompound.sol

4: 		import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

5: 		import "@openzeppelin/contracts/utils/Multicall.sol";

6: 		import "@openzeppelin/contracts/utils/math/SafeMath.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L5), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L6)

```solidity
File: src/transformers/LeverageTransformer.sol

4: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

5: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L5)

```solidity
File: src/transformers/V3Utils.sol

4: 		import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

5: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L5)

```solidity
File: src/utils/Swapper.sol

4: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L4)

### [N-15]<a name="n-15"></a> Same `constant` is redefined elsewhere

Keeping the same constants in different files may cause some problems, as the values could become out of sync when only one location is updated; reading constants from a single file is preferable. This should also be preferred for gas optimizations.

*There are 12 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit seen in src/V3Oracle.sol, src/V3Vault.sol, src/automators/Automator.sol
12: 		    uint256 private constant Q96 = 2 ** 96;
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L12)

```solidity
File: src/V3Oracle.sol

// @audit seen in src/InterestRateModel.sol, src/V3Vault.sol, src/automators/Automator.sol
27: 		    uint256 private constant Q96 = 2 ** 96;

// @audit seen in src/V3Vault.sol, src/utils/Swapper.sol
58: 		    address public immutable factory;

// @audit seen in src/V3Vault.sol, src/utils/Swapper.sol
59: 		    INonfungiblePositionManager public immutable nonfungiblePositionManager;
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L27), [58](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L58), [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L59)

```solidity
File: src/V3Vault.sol

// @audit seen in src/InterestRateModel.sol, src/V3Oracle.sol, src/automators/Automator.sol
34: 		    uint256 private constant Q96 = 2 ** 96;

// @audit seen in src/V3Oracle.sol, src/utils/Swapper.sol
50: 		    IUniswapV3Factory public immutable factory;

// @audit seen in src/V3Oracle.sol, src/utils/Swapper.sol
47: 		    INonfungiblePositionManager public immutable nonfungiblePositionManager;

// @audit seen in src/transformers/V3Utils.sol
59: 		    IPermit2 public immutable permit2;
```

*GitHub* : [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L59), [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L34), [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L50), [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L47)

```solidity
File: src/automators/Automator.sol

// @audit seen in src/InterestRateModel.sol, src/V3Oracle.sol, src/V3Vault.sol
21: 		    uint256 internal constant Q96 = 2 ** 96;
```

*GitHub* : [21](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L21)

```solidity
File: src/transformers/V3Utils.sol

// @audit seen in src/V3Vault.sol
19: 		    IPermit2 public immutable permit2;
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L19)

```solidity
File: src/utils/Swapper.sol

// @audit seen in src/V3Oracle.sol, src/V3Vault.sol
23: 		    address public immutable factory;

// @audit seen in src/V3Oracle.sol, src/V3Vault.sol
26: 		    INonfungiblePositionManager public immutable nonfungiblePositionManager;
```

*GitHub* : [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L23), [26](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L26)

### [N-16]<a name="n-16"></a> Enum values should be used in place of constant array indexes

Consider using an enum instead of hardcoding an index access to make the code easier to understand.

*There are 9 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

366: 		            secondsAgos[0] = 0; // from (before)

367: 		            secondsAgos[1] = twapSeconds; // from (before)

369: 		            int24 tick = int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapSeconds)));

369: 		            int24 tick = int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapSeconds)));
```

*GitHub* : [366](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L366), [367](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L367), [369](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L369), [369](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L369)

```solidity
File: src/automators/Automator.sol

182: 		        secondsAgos[0] = 0; // from (before)

183: 		        secondsAgos[1] = twapPeriod; // from (before)

187: 		            return (int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapPeriod))), true);

187: 		            return (int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapPeriod))), true);
```

*GitHub* : [182](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L182), [183](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L183), [187](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L187), [187](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L187)

```solidity
File: src/transformers/AutoCompound.sol

234: 		            uint256 balance = positionBalances[0][tokens[i]];
```

*GitHub* : [234](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L234)

### [N-17]<a name="n-17"></a> Variable initialization with zero value

It's not necessary to initialize a variable with a zero value, as it's the default behaviour, and it's actually worse in gas terms as it adds an overhead.

*There are 13 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

118: 		    uint32 public reserveFactorX32 = 0;

124: 		    uint256 public debtSharesTotal = 0;

127: 		    uint256 public lastExchangeRateUpdate = 0;

131: 		    uint256 public globalDebtLimit = 0;

132: 		    uint256 public globalLendLimit = 0;

135: 		    uint256 public minLoanSize = 0;

138: 		    uint256 public dailyLendIncreaseLimitMin = 0;

139: 		    uint256 public dailyLendIncreaseLimitLeft = 0;

140: 		    uint256 public dailyLendIncreaseLimitLastReset = 0;

143: 		    uint256 public dailyDebtIncreaseLimitMin = 0;

144: 		    uint256 public dailyDebtIncreaseLimitLeft = 0;

145: 		    uint256 public dailyDebtIncreaseLimitLastReset = 0;

161: 		    uint256 private transformedTokenId = 0; // transient storage (when available in dencun)
```

*GitHub* : [118](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L118), [124](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L124), [127](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L127), [131](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L131), [132](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L132), [135](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L135), [138](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L138), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L139), [140](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L140), [143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L143), [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L144), [145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L145), [161](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L161)

### [N-18]<a name="n-18"></a> Consider adding emergency-stop functionality

Consider adding `pausable` to the following contracts so it's possible to stop them in case of an emergency.

*There are 4 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

11: 		contract InterestRateModel is Ownable, IInterestRateModel, IErrors {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L11)

```solidity
File: src/V3Oracle.sol

24: 		contract V3Oracle is IV3Oracle, Ownable, IErrors {
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L24)

```solidity
File: src/V3Vault.sol

30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

```solidity
File: src/automators/Automator.sol

19: 		abstract contract Automator is Swapper, Ownable {
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L19)

### [N-19]<a name="n-19"></a> Duplicated `require/if` statements should be refactored

These statements should be refactored to a separate function, as there are multiple parts of the codebase that use the same logic, to improve the code readability and reduce code duplication.

*There are 5 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit this if condition is duplicated on line 255
211: 		        if (mode == Mode.NOT_SET) {
212: 		            revert InvalidConfig();
213: 		        }
```

*GitHub* : [211-213](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L211-L213)

```solidity
File: src/V3Vault.sol

// @audit this if condition is duplicated on line 687
615: 		        if (transformedTokenId > 0) {
616: 		            revert TransformNotAllowed();
617: 		        }
```

*GitHub* : [615-617](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L615-L617)

```solidity
File: src/automators/Automator.sol

// @audit this if condition is duplicated on line 124
105: 		        if (msg.sender != withdrawer) {
106: 		            revert Unauthorized();
107: 		        }

// @audit this if condition is duplicated on line 222
131: 		            if (!sent) {
132: 		                revert EtherSendFailed();
133: 		            }
```

*GitHub* : [105-107](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L105-L107), [131-133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L131-L133)

```solidity
File: src/utils/Swapper.sol

// @audit this if condition is duplicated on line 149
111: 		            if (amountOutDelta < params.amountOutMin) {
112: 		                revert SlippageError();
113: 		            }
```

*GitHub* : [111-113](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L111-L113)

### [N-20]<a name="n-20"></a> Inconsistent usage of `require`/`error`

Some parts of the codebase use `require` statements, while others use custom `error`s. Consider refactoring the code to use the same approach: the following findings represent the minority of `require` vs `error`, and they show the first occurance in each file, for brevity.

*There are 2 instance(s) of this issue:*

```solidity
File: src/transformers/AutoCompound.sol

244: 		        require(_totalRewardX64 <= totalRewardX64, ">totalRewardX64");
```

*GitHub* : [244](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L244)

```solidity
File: src/utils/Swapper.sol

157: 		        require(amount0Delta > 0 || amount1Delta > 0); // swaps entirely within 0-liquidity regions are not supported
```

*GitHub* : [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L157)

### [N-21]<a name="n-21"></a> Some functions contain the same exact logic

These functions might be a problem if the logic changes before the contract is deployed, as the developer must remember to syncronize the logic between all the function instances.

Consider using a single function instead of duplicating the code, for example by using a `library`, or through inheritance.

*There are 4 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit duplicated logic in src/V3Oracle.sol -> setEmergencyAdmin, src/V3Vault.sol -> setEmergencyAdmin
265: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L265)

```solidity
File: src/V3Vault.sol

// @audit duplicated logic in src/V3Oracle.sol -> setEmergencyAdmin, src/V3Vault.sol -> setEmergencyAdmin
870: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [870](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L870)

```solidity
File: src/automators/Automator.sol

// @audit duplicated logic in src/automators/Automator.sol -> _transferToken, src/transformers/V3Utils.sol -> _transferToken
218: 		    function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {
```

*GitHub* : [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L218)

```solidity
File: src/transformers/V3Utils.sol

// @audit duplicated logic in src/automators/Automator.sol -> _transferToken, src/transformers/V3Utils.sol -> _transferToken
864: 		    function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {
```

*GitHub* : [864](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L864)

### [N-22]<a name="n-22"></a> Unbounded loop may run out of gas

Consider limiting the number of iterations in loops with an explicit revert reason to avoid iterating an array that is too large.

The function would eventually revert if out of gas anyway, but by limiting it the user avoids wasting too much gas, as the loop doesn't execute if an excessive value is provided.

*There are 2 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

111: 		        for (; i < count; ++i) {
112: 		            uint256 balance = IERC20(tokens[i]).balanceOf(address(this));
113: 		            if (balance > 0) {
114: 		                _transferToken(to, IERC20(tokens[i]), balance, true);
115: 		            }
116: 		        }
```

*GitHub* : [111-116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L111-L116)

```solidity
File: src/transformers/AutoCompound.sol

233: 		        for (; i < count; ++i) {
234: 		            uint256 balance = positionBalances[0][tokens[i]];
235: 		            _withdrawBalanceInternal(0, tokens[i], to, balance, balance);
236: 		        }
```

*GitHub* : [233-236](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L233-L236)

### [N-23]<a name="n-23"></a> Public functions not called internally

Those functions should be declared as `external` instead of `public`, as they are never called internally by the contract.

Contracts are allowed to override their parents' functions and change the visibility from external to public.

*There are 2 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

79: 		    function setVault(address _vault, bool _active) public onlyOwner {
```

*GitHub* : [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L79)

```solidity
File: src/transformers/V3Utils.sol

98: 		    function executeWithPermit(uint256 tokenId, Instructions memory instructions, uint8 v, bytes32 r, bytes32 s)
```

*GitHub* : [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L98)

### [N-24]<a name="n-24"></a> Large multiples of ten should use scientific notation

Use a scientific notation rather than decimal literals (e.g. `1e6` instead of `1000000`), for better code readability.

*There are 3 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit 10000 -> 1e4
144: 		            ? (priceX96 - verifyPriceX96) * 10000 / priceX96

// @audit 10000 -> 1e4
145: 		            : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;
```

*GitHub* : [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L144), [145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L145)

```solidity
File: src/transformers/AutoRange.sol

// @audit 10000 -> 1e4
301: 		        if (fee == 10000) {
```

*GitHub* : [301](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L301)

### [N-25]<a name="n-25"></a> Missing/malformed underscores for large numeric literals

Large hardcoded numbers in code can be difficult to read. Consider using underscores for number literals to improve readability (e.g `1234567` -> `1_234_567`). Consider using an underscore for every third digit from the right.

*There are 4 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

13: 		    uint256 public constant YEAR_SECS = 31557600; // taking into account leap years
```

*GitHub* : [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L13)

```solidity
File: src/V3Oracle.sol

144: 		            ? (priceX96 - verifyPriceX96) * 10000 / priceX96

145: 		            : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;
```

*GitHub* : [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L144), [145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L145)

```solidity
File: src/transformers/AutoRange.sol

301: 		        if (fee == 10000) {
```

*GitHub* : [301](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L301)

### [N-26]<a name="n-26"></a> Avoid complex casting

Consider refactoring the following code, as double casting is confusing, and, in some scenarios, it may introduce unexpected truncations or rounding issues.

Furthermore, double type casting can make the code less readable and harder to maintain, increasing the likelihood of errors and misunderstandings during development and debugging.

*There are 2 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit int56(uint56)
369: 		            int24 tick = int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapSeconds)));
```

*GitHub* : [369](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L369)

```solidity
File: src/automators/Automator.sol

// @audit int56(uint56)
187: 		            return (int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapPeriod))), true);
```

*GitHub* : [187](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L187)

### [N-27]<a name="n-27"></a> Consider using the `using-for` syntax

The `using-for` [syntax](https://docs.soliditylang.org/en/latest/contracts.html#using-for) is the more common way of calling library functions.

*There are 167 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

211: 		        if (mode == Mode.NOT_SET) {

236: 		                feed, maxFeedAge, feedDecimals, tokenDecimals, IUniswapV3Pool(address(0)), false, 0, Mode.CHAINLINK, 0

255: 		        if (mode == Mode.NOT_SET) {

283: 		        if (feedConfig.mode == Mode.NOT_SET) {

290: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY

290: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY

291: 		                || feedConfig.mode == Mode.CHAINLINK

294: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY

294: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY

295: 		                || feedConfig.mode == Mode.TWAP

307: 		            if (feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY) {

316: 		            if (feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY) {

323: 		        if (feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY) {

323: 		        if (feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY) {

370: 		            sqrtPriceX96 = TickMath.getSqrtRatioAtTick(tick);

373: 		        return FullMath.mulDiv(sqrtPriceX96, sqrtPriceX96, Q96);

432: 		            state.sqrtPriceX96Lower = TickMath.getSqrtRatioAtTick(state.tickLower);

433: 		            state.sqrtPriceX96Upper = TickMath.getSqrtRatioAtTick(state.tickUpper);

434: 		            (amount0, amount1) = LiquidityAmounts.getAmountsForLiquidity(

467: 		        fees0 = uint128(FullMath.mulDiv(feeGrowth0, position.liquidity, Q128));

468: 		        fees1 = uint128(FullMath.mulDiv(feeGrowth1, position.liquidity, Q128));

500: 		        return IUniswapV3Pool(PoolAddress.computeAddress(factory, PoolAddress.getPoolKey(tokenA, tokenB, fee)));

500: 		        return IUniswapV3Pool(PoolAddress.computeAddress(factory, PoolAddress.getPoolKey(tokenA, tokenB, fee)));
```

*GitHub* : [211](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L211), [236](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L236), [255](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L255), [283](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L283), [290](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L290), [290](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L290), [291](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L291), [294](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L294), [294](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L294), [295](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L295), [307](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L307), [316](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L316), [323](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L323), [323](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L323), [370](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L370), [373](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L373), [432](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L432), [433](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L433), [434](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L434), [467](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L467), [468](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L468), [500](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L500), [500](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L500)

```solidity
File: src/V3Vault.sol

212: 		        debt = _convertToAssets(debtSharesTotal, debtExchangeRateX96, Math.Rounding.Up);

213: 		        lent = _convertToAssets(totalSupply(), lendExchangeRateX96, Math.Rounding.Up);

221: 		        amount = _convertToAssets(balanceOf(account), newLendExchangeRateX96, Math.Rounding.Down);

245: 		        debt = _convertToAssets(loans[tokenId].debtShares, newDebtExchangeRateX96, Math.Rounding.Up);

291: 		        return _convertToShares(assets, lendExchangeRateX96, Math.Rounding.Down);

297: 		        return _convertToAssets(shares, lendExchangeRateX96, Math.Rounding.Down);

303: 		        uint256 value = _convertToAssets(totalSupply(), lendExchangeRateX96, Math.Rounding.Up);

314: 		        uint256 value = _convertToAssets(totalSupply(), lendExchangeRateX96, Math.Rounding.Up);

318: 		            return _convertToShares(globalLendLimit - value, lendExchangeRateX96, Math.Rounding.Down);

325: 		        return _convertToAssets(balanceOf(owner), lendExchangeRateX96, Math.Rounding.Down);

336: 		        return _convertToShares(assets, lendExchangeRateX96, Math.Rounding.Down);

342: 		        return _convertToAssets(shares, lendExchangeRateX96, Math.Rounding.Up);

348: 		        return _convertToShares(assets, lendExchangeRateX96, Math.Rounding.Up);

354: 		        return _convertToAssets(shares, lendExchangeRateX96, Math.Rounding.Down);

476: 		        return IERC721Receiver.onERC721Received.selector;

539: 		        uint256 debt = _convertToAssets(loans[tokenId].debtShares, newDebtExchangeRateX96, Math.Rounding.Up);

565: 		        uint256 shares = _convertToShares(assets, newDebtExchangeRateX96, Math.Rounding.Up);

571: 		        if (debtSharesTotal > _convertToShares(globalDebtLimit, newDebtExchangeRateX96, Math.Rounding.Down)) {

584: 		        uint256 debt = _convertToAssets(loanDebtShares, newDebtExchangeRateX96, Math.Rounding.Up);

599: 		        SafeERC20.safeTransfer(IERC20(asset), isTransformMode ? msg.sender : owner, assets);

628: 		            INonfungiblePositionManager.DecreaseLiquidityParams(

633: 		        INonfungiblePositionManager.CollectParams memory collectParams = INonfungiblePositionManager.CollectParams(

636: 		            params.feeAmount0 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount0 + params.feeAmount0),

637: 		            params.feeAmount1 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount1 + params.feeAmount1)

642: 		        uint256 debt = _convertToAssets(loans[params.tokenId].debtShares, newDebtExchangeRateX96, Math.Rounding.Up);

700: 		        state.debt = _convertToAssets(debtShares, state.newDebtExchangeRateX96, Math.Rounding.Up);

719: 		                abi.decode(params.permitData, (ISignatureTransfer.PermitTransferFrom, bytes));

722: 		                ISignatureTransfer.SignatureTransferDetails(address(this), state.liquidatorCost),

728: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), state.liquidatorCost);

769: 		            _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up) * reserveProtectionFactorX32 / Q32;

779: 		            SafeERC20.safeTransfer(IERC20(asset), receiver, amount);

887: 		            assets = _convertToAssets(shares, newLendExchangeRateX96, Math.Rounding.Up);

890: 		            shares = _convertToShares(assets, newLendExchangeRateX96, Math.Rounding.Down);

895: 		                abi.decode(permitData, (ISignatureTransfer.PermitTransferFrom, bytes));

897: 		                permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature

901: 		            SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

928: 		            assets = _convertToAssets(amount, newLendExchangeRateX96, Math.Rounding.Down);

931: 		            shares = _convertToShares(amount, newLendExchangeRateX96, Math.Rounding.Up);

946: 		        SafeERC20.safeTransfer(IERC20(asset), receiver, assets);

966: 		            assets = _convertToAssets(amount, newDebtExchangeRateX96, Math.Rounding.Up);

969: 		            shares = _convertToShares(amount, newDebtExchangeRateX96, Math.Rounding.Down);

980: 		                    abi.decode(permitData, (ISignatureTransfer.PermitTransferFrom, bytes));

982: 		                    permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature

986: 		                SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

1008: 		            if (_convertToAssets(loanDebtShares, newDebtExchangeRateX96, Math.Rounding.Up) < minLoanSize) {

1024: 		        uint256 debt = _convertToAssets(debtSharesTotal, debtExchangeRateX96, Math.Rounding.Up);

1025: 		        uint256 lent = _convertToAssets(totalSupply(), lendExchangeRateX96, Math.Rounding.Down);

1066: 		                INonfungiblePositionManager.DecreaseLiquidityParams(tokenId, liquidity, 0, 0, block.timestamp)

1071: 		            INonfungiblePositionManager.CollectParams(tokenId, recipient, fees0, fees1)

1134: 		            uint256 totalLent = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up);

1177: 		        uint256 debt = _convertToAssets(debtSharesTotal, oldDebtExchangeRateX96, Math.Rounding.Up);

1217: 		                tokenConfigs[token0].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);

1218: 		                tokenConfigs[token1].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);

1220: 		                tokenConfigs[token0].totalDebtShares += SafeCast.toUint192(newShares - oldShares);

1221: 		                tokenConfigs[token1].totalDebtShares += SafeCast.toUint192(newShares - oldShares);

1225: 		                uint256 lentAssets = _convertToAssets(totalSupply(), lendExchangeRateX96, Math.Rounding.Up);

1229: 		                        && _convertToAssets(tokenConfigs[token0].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)

1237: 		                        && _convertToAssets(tokenConfigs[token1].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)

1250: 		            uint256 lendIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)

1262: 		            uint256 debtIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)
```

*GitHub* : [212](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L212), [213](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L213), [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L221), [245](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L245), [291](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L291), [297](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L297), [303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L303), [314](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L314), [318](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L318), [325](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L325), [336](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L336), [342](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L342), [348](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L348), [354](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L354), [476](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L476), [539](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L539), [565](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L565), [571](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L571), [584](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L584), [599](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L599), [628](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L628), [633](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L633), [636](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L636), [637](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L637), [642](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L642), [700](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L700), [719](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L719), [722](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L722), [728](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L728), [769](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L769), [779](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L779), [887](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L887), [890](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L890), [895](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L895), [897](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L897), [901](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L901), [928](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L928), [931](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L931), [946](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L946), [966](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L966), [969](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L969), [980](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L980), [982](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L982), [986](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L986), [1008](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1008), [1024](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1024), [1025](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1025), [1066](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1066), [1071](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1071), [1134](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1134), [1177](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1177), [1217](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1217), [1218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1218), [1220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1220), [1221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1221), [1225](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1225), [1229](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1229), [1237](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1237), [1250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1250), [1262](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1262)

```solidity
File: src/automators/AutoExit.sol

172: 		                Swapper.RouterSwapParams(
```

*GitHub* : [172](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L172)

```solidity
File: src/automators/Automator.sol

156: 		        priceX96 = FullMath.mulDiv(sqrtPriceX96, sqrtPriceX96, Q96);

158: 		            amountOutMin = FullMath.mulDiv(amountIn * (Q64 - maxPriceDifferenceX64), priceX96, Q96 * Q64);

160: 		            amountOutMin = FullMath.mulDiv(amountIn * (Q64 - maxPriceDifferenceX64), Q96, priceX96 * Q64);

203: 		                INonfungiblePositionManager.DecreaseLiquidityParams(

209: 		            INonfungiblePositionManager.CollectParams(tokenId, address(this), type(uint128).max, type(uint128).max)

226: 		            SafeERC20.safeTransfer(token, to, amount);
```

*GitHub* : [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L156), [158](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L158), [160](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L160), [203](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L203), [209](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L209), [226](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L226)

```solidity
File: src/transformers/AutoCompound.sol

92: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoCompound.execute.selector, params)

109: 		            INonfungiblePositionManager.CollectParams(

143: 		                        Swapper.PoolSwapParams(

164: 		                    INonfungiblePositionManager.IncreaseLiquidityParams(

272: 		        SafeERC20.safeTransfer(IERC20(token), to, amount);

280: 		            SafeERC20.safeApprove(IERC20(token0), address(nonfungiblePositionManager), type(uint256).max);

284: 		            SafeERC20.safeApprove(IERC20(token1), address(nonfungiblePositionManager), type(uint256).max);
```

*GitHub* : [92](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L92), [109](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L109), [143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L143), [164](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L164), [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L272), [280](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L280), [284](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L284)

```solidity
File: src/transformers/AutoRange.sol

102: 		            params.tokenId, address(this), abi.encodeWithSelector(AutoRange.execute.selector, params)

182: 		                Swapper.RouterSwapParams(

198: 		            INonfungiblePositionManager.MintParams memory mintParams = INonfungiblePositionManager.MintParams(

202: 		                SafeCast.toInt24(baseTick + config.lowerTickDelta), // reverts if out of valid range

203: 		                SafeCast.toInt24(baseTick + config.upperTickDelta), // reverts if out of valid range

213: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), state.maxAddAmount0);

214: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), state.maxAddAmount1);

220: 		            SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), 0);

221: 		            SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), 0);
```

*GitHub* : [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L102), [182](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L182), [198](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L198), [202](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L202), [203](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L203), [213](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L213), [214](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L214), [220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L220), [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L221)

```solidity
File: src/transformers/LeverageTransformer.sol

54: 		                Swapper.RouterSwapParams(

66: 		                Swapper.RouterSwapParams(

77: 		        SafeERC20.safeIncreaseAllowance(IERC20(token0), address(nonfungiblePositionManager), amount0);

78: 		        SafeERC20.safeIncreaseAllowance(IERC20(token1), address(nonfungiblePositionManager), amount1);

80: 		        INonfungiblePositionManager.IncreaseLiquidityParams memory increaseLiquidityParams = INonfungiblePositionManager

88: 		            SafeERC20.safeTransfer(IERC20(token0), params.recipient, amount0 - added0);

91: 		            SafeERC20.safeTransfer(IERC20(token1), params.recipient, amount1 - added1);

94: 		            SafeERC20.safeTransfer(IERC20(token), params.recipient, amount);

130: 		        INonfungiblePositionManager.DecreaseLiquidityParams memory decreaseLiquidityParams = INonfungiblePositionManager

136: 		        INonfungiblePositionManager.CollectParams memory collectParams = INonfungiblePositionManager.CollectParams(

139: 		            params.feeAmount0 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount0 + params.feeAmount0),

140: 		            params.feeAmount1 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount1 + params.feeAmount1)

148: 		                Swapper.RouterSwapParams(

157: 		                Swapper.RouterSwapParams(

165: 		        SafeERC20.safeApprove(IERC20(token), msg.sender, amount);

170: 		            SafeERC20.safeTransfer(IERC20(token0), params.recipient, amount0);

173: 		            SafeERC20.safeTransfer(IERC20(token1), params.recipient, amount1);
```

*GitHub* : [54](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L54), [66](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L66), [77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L77), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L78), [80](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L80), [88](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L88), [91](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L91), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L94), [130](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L130), [136](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L136), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L139), [140](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L140), [148](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L148), [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L157), [165](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L165), [170](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L170), [173](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L173)

```solidity
File: src/transformers/V3Utils.sol

146: 		        if (instructions.whatToDo == WhatToDo.COMPOUND_FEES) {

219: 		        } else if (instructions.whatToDo == WhatToDo.CHANGE_RANGE) {

304: 		        } else if (instructions.whatToDo == WhatToDo.WITHDRAW_AND_COLLECT_AND_SWAP) {

308: 		                    Swapper.RouterSwapParams(

325: 		                    Swapper.RouterSwapParams(

378: 		        return IERC721Receiver.onERC721Received.selector;

404: 		                abi.decode(params.permitData, (ISignatureTransfer.PermitBatchTransferFrom, bytes));

414: 		            Swapper.RouterSwapParams(

478: 		                abi.decode(params.permitData, (ISignatureTransfer.PermitBatchTransferFrom, bytes));

541: 		                abi.decode(params.permitData, (ISignatureTransfer.PermitBatchTransferFrom, bytes));

578: 		            SafeERC20.safeTransferFrom(token0, msg.sender, address(this), needed0);

581: 		            SafeERC20.safeTransferFrom(token1, msg.sender, address(this), needed1);

584: 		            SafeERC20.safeTransferFrom(otherToken, msg.sender, address(this), neededOther);

619: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed0);

623: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed1);

627: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.neededOther);

711: 		        INonfungiblePositionManager.MintParams memory mintParams = INonfungiblePositionManager.MintParams(

766: 		        INonfungiblePositionManager.IncreaseLiquidityParams memory increaseLiquidityParams = INonfungiblePositionManager

788: 		                Swapper.RouterSwapParams(

799: 		                Swapper.RouterSwapParams(

807: 		                Swapper.RouterSwapParams(

812: 		                Swapper.RouterSwapParams(

831: 		            SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), 0);

832: 		            SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), total0);

835: 		            SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), 0);

836: 		            SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), total1);

872: 		            SafeERC20.safeTransfer(token, to, amount);

886: 		                INonfungiblePositionManager.DecreaseLiquidityParams(tokenId, liquidity, token0Min, token1Min, deadline)

899: 		            INonfungiblePositionManager.CollectParams(tokenId, address(this), collectAmount0, collectAmount1)
```

*GitHub* : [146](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L146), [219](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L219), [304](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L304), [308](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L308), [325](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L325), [378](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L378), [404](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L404), [414](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L414), [478](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L478), [541](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L541), [578](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L578), [581](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L581), [584](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L584), [619](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L619), [623](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L623), [627](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L627), [711](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L711), [766](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L766), [788](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L788), [799](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L799), [807](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L807), [812](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L812), [831](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L831), [832](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L832), [835](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L835), [836](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L836), [872](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L872), [886](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L886), [899](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L899)

```solidity
File: src/utils/FlashloanLiquidator.sol

72: 		        SafeERC20.safeApprove(data.asset, address(data.vault), data.liquidationCost);

74: 		            IVault.LiquidateParams(

78: 		        SafeERC20.safeApprove(data.asset, address(data.vault), 0);

85: 		        SafeERC20.safeTransfer(data.asset, msg.sender, data.liquidationCost + (fee0 + fee1));

91: 		                SafeERC20.safeTransfer(data.swap0.tokenIn, data.liquidator, balance);

97: 		                SafeERC20.safeTransfer(data.swap1.tokenIn, data.liquidator, balance);

106: 		                SafeERC20.safeTransfer(data.asset, data.liquidator, balance);
```

*GitHub* : [72](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L72), [74](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L74), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L78), [85](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L85), [91](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L91), [97](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L97), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L106)

```solidity
File: src/utils/Swapper.sol

87: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, params.amountIn);

94: 		                SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, 0);

98: 		                SafeERC20.safeTransfer(params.tokenIn, universalRouter, params.amountIn);

138: 		                (params.swap0For1 ? TickMath.MIN_SQRT_RATIO + 1 : TickMath.MAX_SQRT_RATIO - 1),

138: 		                (params.swap0For1 ? TickMath.MIN_SQRT_RATIO + 1 : TickMath.MAX_SQRT_RATIO - 1),

167: 		        SafeERC20.safeTransfer(IERC20(tokenIn), msg.sender, amountToPay);

172: 		        return IUniswapV3Pool(PoolAddress.computeAddress(address(factory), PoolAddress.getPoolKey(tokenA, tokenB, fee)));

172: 		        return IUniswapV3Pool(PoolAddress.computeAddress(address(factory), PoolAddress.getPoolKey(tokenA, tokenB, fee)));
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L87), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L94), [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L98), [138](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L138), [138](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L138), [167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L167), [172](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L172), [172](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L172)

### [N-28]<a name="n-28"></a> Consider making contracts `Upgradeable`

This allows for bugs to be fixed in production, at the expense of **significantly** increasing centralization.

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

11: 		contract InterestRateModel is Ownable, IInterestRateModel, IErrors {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L11)

```solidity
File: src/V3Oracle.sol

24: 		contract V3Oracle is IV3Oracle, Ownable, IErrors {
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L24)

```solidity
File: src/V3Vault.sol

30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

```solidity
File: src/automators/AutoExit.sol

10: 		contract AutoExit is Automator {
```

*GitHub* : [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L10)

```solidity
File: src/automators/Automator.sol

19: 		abstract contract Automator is Swapper, Ownable {
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L19)

```solidity
File: src/transformers/AutoCompound.sol

16: 		contract AutoCompound is Automator, Multicall, ReentrancyGuard {
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L16)

```solidity
File: src/transformers/AutoRange.sol

11: 		contract AutoRange is Automator {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L11)

```solidity
File: src/transformers/LeverageTransformer.sol

12: 		contract LeverageTransformer is Swapper {
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L12)

```solidity
File: src/transformers/V3Utils.sol

15: 		contract V3Utils is Swapper, IERC721Receiver {
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L15)

```solidity
File: src/utils/FlashloanLiquidator.sol

11: 		contract FlashloanLiquidator is Swapper, IUniswapV3FlashCallback {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L11)

```solidity
File: src/utils/Swapper.sol

17: 		abstract contract Swapper is IUniswapV3SwapCallback, IErrors {
```

*GitHub* : [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L17)

### [N-29]<a name="n-29"></a> Missing timelock in critical functions

It is a good practice to give time for users to react and adjust to critical changes. A timelock provides more guarantees and reduces the level of trust required, thus decreasing risk for users. It also indicates that the project is legitimate (less risk of a malicious owner making a sandwich attack on a user). Consider adding a timelock to the following functions:

*There are 1 instance(s) of this issue:*

```solidity
File: src/transformers/AutoCompound.sol

243: 		    function setReward(uint64 _totalRewardX64) external onlyOwner {
```

*GitHub* : [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L243)

### [N-30]<a name="n-30"></a> Dependence on external protocols

External protocols should be monitored as such dependencies may introduce vulnerabilities if a vulnerability is found in the external protocol.

*There are 92 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L4)

```solidity
File: src/V3Oracle.sol

4: 		import "v3-core/interfaces/IUniswapV3Factory.sol";

5: 		import "v3-core/interfaces/IUniswapV3Pool.sol";

14: 		import "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

15: 		import "@openzeppelin/contracts/access/Ownable.sol";

37: 		        CHAINLINK_TWAP_VERIFY, // using chainlink for price and TWAP to verify

38: 		        TWAP_CHAINLINK_VERIFY, // using TWAP for price and chainlink to verify

39: 		        CHAINLINK, // using only chainlink directly

48: 		        IUniswapV3Pool pool; // reference pool

68: 		    address public immutable chainlinkReferenceToken;

77: 		        address _chainlinkReferenceToken

83: 		        chainlinkReferenceToken = _chainlinkReferenceToken;

104: 		        uint256 cachedChainlinkReferencePriceX96;

106: 		        (price0X96, cachedChainlinkReferencePriceX96) =

107: 		            _getReferenceTokenPriceX96(token0, cachedChainlinkReferencePriceX96);

108: 		        (price1X96, cachedChainlinkReferencePriceX96) =

109: 		            _getReferenceTokenPriceX96(token1, cachedChainlinkReferencePriceX96);

117: 		            (priceTokenX96,) = _getReferenceTokenPriceX96(token, cachedChainlinkReferencePriceX96);

134: 		        IUniswapV3Pool pool = _getPool(token0, token1, fee);

205: 		        IUniswapV3Pool pool,

236: 		                feed, maxFeedAge, feedDecimals, tokenDecimals, IUniswapV3Pool(address(0)), false, 0, Mode.CHAINLINK, 0

272: 		    function _getReferenceTokenPriceX96(address token, uint256 cachedChainlinkReferencePriceX96)

275: 		        returns (uint256 priceX96, uint256 chainlinkReferencePriceX96)

278: 		            return (Q96, chainlinkReferencePriceX96);

289: 		        bool usesChainlink = (

290: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY

291: 		                || feedConfig.mode == Mode.CHAINLINK

294: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY

298: 		        if (usesChainlink) {

299: 		            uint256 chainlinkPriceX96 = _getChainlinkPriceX96(token);

300: 		            chainlinkReferencePriceX96 = cachedChainlinkReferencePriceX96 == 0

301: 		                ? _getChainlinkPriceX96(referenceToken)

302: 		                : cachedChainlinkReferencePriceX96;

304: 		            chainlinkPriceX96 = (10 ** referenceTokenDecimals) * chainlinkPriceX96 * Q96 / chainlinkReferencePriceX96

307: 		            if (feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY) {

308: 		                verifyPriceX96 = chainlinkPriceX96;

310: 		                priceX96 = chainlinkPriceX96;

316: 		            if (feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY) {

323: 		        if (feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY) {

329: 		    function _getChainlinkPriceX96(address token) internal view returns (uint256) {

330: 		        if (token == chainlinkReferenceToken) {

339: 		            revert ChainlinkPriceError();

359: 		    function _getReferencePoolPriceX96(IUniswapV3Pool pool, uint32 twapSeconds) internal view returns (uint256) {

388: 		        IUniswapV3Pool pool;

473: 		        IUniswapV3Pool pool,

499: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {

500: 		        return IUniswapV3Pool(PoolAddress.computeAddress(factory, PoolAddress.getPoolKey(tokenA, tokenB, fee)));
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L5), [14](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L14), [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L15), [37](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L37), [38](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L38), [39](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L39), [48](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L48), [68](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L68), [77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L77), [83](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L83), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L104), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L106), [107](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L107), [108](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L108), [109](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L109), [117](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L117), [134](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L134), [205](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L205), [236](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L236), [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L272), [275](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L275), [278](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L278), [289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L289), [290](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L290), [291](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L291), [294](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L294), [298](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L298), [299](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L299), [300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L300), [301](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L301), [302](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L302), [304](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L304), [307](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L307), [308](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L308), [310](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L310), [316](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L316), [323](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L323), [329](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L329), [330](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L330), [339](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L339), [359](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L359), [388](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L388), [473](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L473), [499](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L499), [500](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L500)

```solidity
File: src/V3Vault.sol

4: 		import "v3-core/interfaces/IUniswapV3Factory.sol";

5: 		import "v3-core/interfaces/IUniswapV3Pool.sol";

12: 		import "@openzeppelin/contracts/utils/math/Math.sol";

13: 		import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

14: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

15: 		import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

16: 		import "@openzeppelin/contracts/access/Ownable.sol";

17: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

18: 		import "@openzeppelin/contracts/utils/Multicall.sol";

50: 		    IUniswapV3Factory public immutable factory;

181: 		        factory = IUniswapV3Factory(_nonfungiblePositionManager.factory());

434: 		        // only Uniswap v3 NFTs allowed - sent from other contract
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L5), [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L12), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L13), [14](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L14), [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L15), [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L16), [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L17), [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L18), [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L50), [181](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L181), [434](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L434)

```solidity
File: src/automators/AutoExit.sol

87: 		        IUniswapV3Pool pool;
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L87)

```solidity
File: src/automators/Automator.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";

5: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

6: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

8: 		import "v3-core/interfaces/IUniswapV3Factory.sol";

9: 		import "v3-core/interfaces/IUniswapV3Pool.sol";

142: 		        IUniswapV3Pool pool,

166: 		    function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

180: 		    function _getTWAPTick(IUniswapV3Pool pool, uint32 twapPeriod) internal view returns (int24, bool) {
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L5), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L6), [8](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L8), [9](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L9), [142](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L142), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L166), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L180)

```solidity
File: src/transformers/AutoCompound.sol

4: 		import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

5: 		import "@openzeppelin/contracts/utils/Multicall.sol";

6: 		import "@openzeppelin/contracts/utils/math/SafeMath.sol";

128: 		                IUniswapV3Pool pool = _getPool(state.token0, state.token1, state.fee);
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L5), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L6), [128](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L128)

```solidity
File: src/transformers/AutoRange.sol

68: 		        IUniswapV3Pool pool;

308: 		            int24 spacing = IUniswapV3Factory(factory).feeAmountTickSpacing(fee);
```

*GitHub* : [68](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L68), [308](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L308)

```solidity
File: src/transformers/LeverageTransformer.sol

4: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

5: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L5)

```solidity
File: src/transformers/V3Utils.sol

4: 		import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

5: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

361: 		        // only Uniswap v3 NFTs allowed
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L5), [361](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L361)

```solidity
File: src/utils/FlashloanLiquidator.sol

4: 		import "v3-core/interfaces/IUniswapV3Pool.sol";

5: 		import "v3-core/interfaces/callback/IUniswapV3FlashCallback.sol";

11: 		contract FlashloanLiquidator is Swapper, IUniswapV3FlashCallback {

32: 		        IUniswapV3Pool flashLoanPool; // pool which is used for flashloan - may not be used in the swaps below

67: 		    function uniswapV3FlashCallback(uint256 fee0, uint256 fee1, bytes calldata callbackData) external {
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L5), [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L11), [32](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L32), [67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L67)

```solidity
File: src/utils/Swapper.sol

4: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

6: 		import "v3-core/interfaces/callback/IUniswapV3SwapCallback.sol";

7: 		import "v3-core/interfaces/IUniswapV3Pool.sol";

17: 		abstract contract Swapper is IUniswapV3SwapCallback, IErrors {

121: 		        IUniswapV3Pool pool;

156: 		    function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external override {

171: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {

172: 		        return IUniswapV3Pool(PoolAddress.computeAddress(address(factory), PoolAddress.getPoolKey(tokenA, tokenB, fee)));
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L4), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L6), [7](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L7), [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L17), [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L121), [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L156), [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L171), [172](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L172)

### [N-31]<a name="n-31"></a> Use transfer libraries instead of low level calls

Consider using `SafeTransferLib.safeTransferETH` or `Address.sendValue` for clearer semantic meaning instead of using a low level `call`.

*There are 3 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

130: 		            (bool sent,) = to.call{value: balance}("");

221: 		            (bool sent,) = to.call{value: amount}("");
```

*GitHub* : [130](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L130), [221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L221)

```solidity
File: src/transformers/V3Utils.sol

867: 		            (bool sent,) = to.call{value: amount}("");
```

*GitHub* : [867](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L867)

### [N-32]<a name="n-32"></a> `2**<n> - 1` should be re-written as `type(uint<n>).max`

Earlier versions of solidity can use `uint<n>(-1)` instead. Expressions not including the `- 1` can often be re-written to accomodate the change (e.g. by using a `>` rather than a `>=`, which will also save some gas).

*There are 14 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

12: 		    uint256 private constant Q96 = 2 ** 96;

12: 		    uint256 private constant Q96 = 2 ** 96;
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L12), [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L12)

```solidity
File: src/V3Oracle.sol

27: 		    uint256 private constant Q96 = 2 ** 96;

27: 		    uint256 private constant Q96 = 2 ** 96;

28: 		    uint256 private constant Q128 = 2 ** 128;

28: 		    uint256 private constant Q128 = 2 ** 128;
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L27), [27](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L27), [28](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L28), [28](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L28)

```solidity
File: src/V3Vault.sol

33: 		    uint256 private constant Q32 = 2 ** 32;

33: 		    uint256 private constant Q32 = 2 ** 32;

34: 		    uint256 private constant Q96 = 2 ** 96;

34: 		    uint256 private constant Q96 = 2 ** 96;
```

*GitHub* : [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L33), [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L33), [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L34), [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L34)

```solidity
File: src/automators/Automator.sol

20: 		    uint256 internal constant Q64 = 2 ** 64;

20: 		    uint256 internal constant Q64 = 2 ** 64;

21: 		    uint256 internal constant Q96 = 2 ** 96;

21: 		    uint256 internal constant Q96 = 2 ** 96;
```

*GitHub* : [20](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L20), [20](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L20), [21](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L21), [21](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L21)

### [N-33]<a name="n-33"></a> Use of non-named numeric constants

Constants should be defined instead of using magic numbers.

*There are 11 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit 10000
144: 		            ? (priceX96 - verifyPriceX96) * 10000 / priceX96

// @audit 10000
145: 		            : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;

// @audit 10
304: 		            chainlinkPriceX96 = (10 ** referenceTokenDecimals) * chainlinkPriceX96 * Q96 / chainlinkReferencePriceX96

// @audit 10
305: 		                / (10 ** feedConfig.tokenDecimals);

// @audit 10
342: 		        return uint256(answer) * Q96 / (10 ** feedConfig.feedDecimals);
```

*GitHub* : [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L144), [145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L145), [304](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L304), [305](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L305), [342](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L342)

```solidity
File: src/transformers/AutoRange.sol

// @audit 10000
301: 		        if (fee == 10000) {

// @audit 200
302: 		            return 200;

// @audit 3000
303: 		        } else if (fee == 3000) {

// @audit 60
304: 		            return 60;

// @audit 500
305: 		        } else if (fee == 500) {

// @audit 10
306: 		            return 10;
```

*GitHub* : [301](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L301), [302](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L302), [303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L303), [304](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L304), [305](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L305), [306](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L306)

### [N-34]<a name="n-34"></a> Consider splitting complex checks into multiple steps

Assign the expression's parts to intermediate local variables, and check against those instead.

*There are 32 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

227: 		            if (!(token0 == token && token1 == referenceToken || token0 == referenceToken && token1 == token)) {

227: 		            if (!(token0 == token && token1 == referenceToken || token0 == referenceToken && token1 == token)) {

227: 		            if (!(token0 == token && token1 == referenceToken || token0 == referenceToken && token1 == token)) {

250: 		        if (msg.sender != emergencyAdmin && msg.sender != owner()) {

289: 		        bool usesChainlink = (
290: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY
291: 		                || feedConfig.mode == Mode.CHAINLINK
292: 		        );

293: 		        bool usesTWAP = (
294: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY
295: 		                || feedConfig.mode == Mode.TWAP
296: 		        );

290: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY
291: 		                || feedConfig.mode == Mode.CHAINLINK

290: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY

294: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY
295: 		                || feedConfig.mode == Mode.TWAP

294: 		            feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY

323: 		        if (feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY) {
```

*GitHub* : [227](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L227), [227](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L227), [227](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L227), [250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L250), [289-292](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L289-L292), [293-296](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L293-L296), [290-291](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L290-L291), [290](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L290), [294-295](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L294-L295), [294](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L294), [323](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L323)

```solidity
File: src/V3Vault.sol

435: 		        if (msg.sender != address(nonfungiblePositionManager) || from == address(this)) {

551: 		        bool isTransformMode =
552: 		            transformedTokenId > 0 && transformedTokenId == tokenId && transformerAllowList[msg.sender];

552: 		            transformedTokenId > 0 && transformedTokenId == tokenId && transformerAllowList[msg.sender];

561: 		        if (!isTransformMode && tokenOwner[tokenId] != msg.sender && address(this) != msg.sender) {

791: 		            transformer == address(0) || transformer == address(this) || transformer == asset
792: 		                || transformer == address(nonfungiblePositionManager)

791: 		            transformer == address(0) || transformer == address(this) || transformer == asset

791: 		            transformer == address(0) || transformer == address(this) || transformer == asset

814: 		        if (msg.sender != emergencyAdmin && msg.sender != owner()) {
```

*GitHub* : [435](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L435), [551-552](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L551-L552), [552](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L552), [561](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L561), [791-792](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L791-L792), [791](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L791), [791](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L791), [814](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L814)

```solidity
File: src/automators/AutoExit.sol

113: 		            config.onlyFees && params.rewardX64 > config.maxRewardX64
114: 		                || !config.onlyFees && params.rewardX64 > config.maxRewardX64

140: 		        state.isSwap = !state.isAbove && config.token0Swap || state.isAbove && config.token1Swap;

140: 		        state.isSwap = !state.isAbove && config.token0Swap || state.isAbove && config.token1Swap;
```

*GitHub* : [113-114](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L113-L114), [140](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L140), [140](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L140)

```solidity
File: src/transformers/AutoRange.sol

123: 		            config.onlyFees && params.rewardX64 > config.maxRewardX64
124: 		                || !config.onlyFees && params.rewardX64 > config.maxRewardX64

149: 		        if (params.swap0To1 && params.amountIn > state.amount0 || !params.swap0To1 && params.amountIn > state.amount1) {

175: 		                baseTick + config.lowerTickDelta == state.tickLower
176: 		                    && baseTick + config.upperTickDelta == state.tickUpper
```

*GitHub* : [123-124](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L123-L124), [149](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L149), [175-176](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L175-L176)

```solidity
File: src/transformers/LeverageTransformer.sol

93: 		        if (token != token0 && token != token1 && amount > 0) {

93: 		        if (token != token0 && token != token1 && amount > 0) {
```

*GitHub* : [93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L93), [93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L93)

```solidity
File: src/transformers/V3Utils.sol

342: 		            if (targetAmount != 0 && instructions.targetToken != address(0)) {

697: 		            amountOther > amountAddedOther && address(otherToken) != address(0) && token0 != otherToken
698: 		                && token1 != otherToken

697: 		            amountOther > amountAddedOther && address(otherToken) != address(0) && token0 != otherToken
```

*GitHub* : [342](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L342), [697-698](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L697-L698), [697](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L697)

```solidity
File: src/utils/Swapper.sol

77: 		        if (params.amountIn != 0 && params.swapData.length != 0 && address(params.tokenOut) != address(0)) {

77: 		        if (params.amountIn != 0 && params.swapData.length != 0 && address(params.tokenOut) != address(0)) {
```

*GitHub* : [77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L77), [77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L77)

### [N-35]<a name="n-35"></a> Complex math should be split into multiple steps

Consider splitting long arithmetic calculations into multiple steps to improve the code readability.

*There are 31 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

50: 		        return debt * Q96 / (cash + debt);

69: 		            uint256 normalRateX96 = (kinkX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

67: 		            borrowRateX96 = (utilizationRateX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

71: 		            borrowRateX96 = (excessUtilX96 * jumpMultiplierPerSecondX96 / Q96) + normalRateX96;
```

*GitHub* : [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L50), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L69), [67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L67), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L71)

```solidity
File: src/V3Oracle.sol

120: 		        value = (price0X96 * (amount0 + fees0) / Q96 + price1X96 * (amount1 + fees1) / Q96) * Q96 / priceTokenX96;

121: 		        feeValue = (price0X96 * fees0 / Q96 + price1X96 * fees1 / Q96) * Q96 / priceTokenX96;

304: 		            chainlinkPriceX96 = (10 ** referenceTokenDecimals) * chainlinkPriceX96 * Q96 / chainlinkReferencePriceX96
305: 		                / (10 ** feedConfig.tokenDecimals);

342: 		        return uint256(answer) * Q96 / (10 ** feedConfig.feedDecimals);
```

*GitHub* : [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L120), [121](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L121), [304-305](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L304-L305), [342](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L342)

```solidity
File: src/V3Vault.sol

1060: 		                liquidity = uint128((liquidationValue - feeValue) * liquidity / (fullValue - feeValue));

1100: 		        uint256 maxPenaltyValue = debt * (Q32 + MAX_LIQUIDATION_PENALTY_X32) / Q32;

1106: 		            uint256 penaltyFractionX96 =
1107: 		                (Q96 - ((fullValue - maxPenaltyValue) * Q96 / (startLiquidationValue - maxPenaltyValue)));

1108: 		            uint256 penaltyX32 = MIN_LIQUIDATION_PENALTY_X32
1109: 		                + (MAX_LIQUIDATION_PENALTY_X32 - MIN_LIQUIDATION_PENALTY_X32) * penaltyFractionX96 / Q96;

1116: 		            uint256 penaltyValue = fullValue * (Q32 - MAX_LIQUIDATION_PENALTY_X32) / Q32;

1111: 		            liquidationValue = debt * (Q32 + penaltyX32) / Q32;

1137: 		            newLendExchangeRateX96 = (totalLent - missing) * newLendExchangeRateX96 / totalLent;

1187: 		            newDebtExchangeRateX96 = oldDebtExchangeRateX96
1188: 		                + oldDebtExchangeRateX96 * (block.timestamp - lastRateUpdate) * borrowRateX96 / Q96;

1189: 		            newLendExchangeRateX96 = oldLendExchangeRateX96
1190: 		                + oldLendExchangeRateX96 * (block.timestamp - lastRateUpdate) * supplyRateX96 / Q96;

1250: 		            uint256 lendIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)
1251: 		                * (Q32 + MAX_DAILY_LEND_INCREASE_X32) / Q32;

1262: 		            uint256 debtIncreaseLimit = _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up)
1263: 		                * (Q32 + MAX_DAILY_DEBT_INCREASE_X32) / Q32;
```

*GitHub* : [1060](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1060), [1100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1100), [1106-1107](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1106-L1107), [1108-1109](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1108-L1109), [1116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1116), [1111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1111), [1137](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1137), [1187-1188](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1187-L1188), [1189-1190](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1189-L1190), [1250-1251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1250-L1251), [1262-1263](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1262-L1263)

```solidity
File: src/automators/AutoExit.sol

155: 		                state.amount0 -= state.feeAmount0 * params.rewardX64 / Q64;

156: 		                state.amount1 -= state.feeAmount1 * params.rewardX64 / Q64;

187: 		                    state.amount0 -= state.amount0 * params.rewardX64 / Q64;

189: 		                    state.amount1 -= state.amount1 * params.rewardX64 / Q64;

194: 		            state.amount0 -= (config.onlyFees ? state.feeAmount0 : state.amount0) * params.rewardX64 / Q64;

195: 		            state.amount1 -= (config.onlyFees ? state.feeAmount1 : state.amount1) * params.rewardX64 / Q64;
```

*GitHub* : [155](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L155), [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L156), [187](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L187), [189](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L189), [194](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L194), [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L195)

```solidity
File: src/automators/Automator.sol

158: 		            amountOutMin = FullMath.mulDiv(amountIn * (Q64 - maxPriceDifferenceX64), priceX96, Q96 * Q64);

160: 		            amountOutMin = FullMath.mulDiv(amountIn * (Q64 - maxPriceDifferenceX64), Q96, priceX96 * Q64);
```

*GitHub* : [158](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L158), [160](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L160)

```solidity
File: src/transformers/AutoCompound.sol

156: 		            state.maxAddAmount0 = state.amount0 * Q64 / (rewardX64 + Q64);

157: 		            state.maxAddAmount1 = state.amount1 * Q64 / (rewardX64 + Q64);
```

*GitHub* : [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L156), [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L157)

```solidity
File: src/transformers/AutoRange.sol

171: 		            int24 baseTick = state.currentTick - (((state.currentTick % tickSpacing) + tickSpacing) % tickSpacing);
```

*GitHub* : [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L171)

```solidity
File: src/transformers/V3Utils.sol

820: 		            uint256 leftOver = params.amountIn0 + params.amountIn1 - amountInDelta0 - amountInDelta1;
```

*GitHub* : [820](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L820)

### [N-36]<a name="n-36"></a> Time related variables should use time units instead of numbers

There are [units](https://docs.soliditylang.org/en/latest/units-and-global-variables.html#time-units) for seconds, minutes, hours, days, and weeks, and since they're defined, they should be used

*There are 2 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

13: 		    uint256 public constant YEAR_SECS = 31557600; // taking into account leap years
```

*GitHub* : [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L13)

```solidity
File: src/automators/Automator.sol

23: 		    uint32 public constant MIN_TWAP_SECONDS = 60; // 1 minute
```

*GitHub* : [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L23)

### [N-37]<a name="n-37"></a> Some functions don't have any logic

Some functions don't have a body, consider commenting why, or refactor the code and remove these functions.

*There are 5 instance(s) of this issue:*

```solidity
File: src/automators/AutoExit.sol

33: 		    constructor(
34: 		        INonfungiblePositionManager _npm,
35: 		        address _operator,
36: 		        address _withdrawer,
37: 		        uint32 _TWAPSeconds,
38: 		        uint16 _maxTWAPTickDifference,
39: 		        address _zeroxRouter,
40: 		        address _universalRouter
41: 		    ) Automator(_npm, _operator, _withdrawer, _TWAPSeconds, _maxTWAPTickDifference, _zeroxRouter, _universalRouter) {}
```

*GitHub* : [33-41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L33-L41)

```solidity
File: src/transformers/AutoCompound.sol

37: 		    constructor(
38: 		        INonfungiblePositionManager _npm,
39: 		        address _operator,
40: 		        address _withdrawer,
41: 		        uint32 _TWAPSeconds,
42: 		        uint16 _maxTWAPTickDifference
43: 		    ) Automator(_npm, _operator, _withdrawer, _TWAPSeconds, _maxTWAPTickDifference, address(0), address(0)) {}
```

*GitHub* : [37-43](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L37-L43)

```solidity
File: src/transformers/AutoRange.sol

25: 		    constructor(
26: 		        INonfungiblePositionManager _npm,
27: 		        address _operator,
28: 		        address _withdrawer,
29: 		        uint32 _TWAPSeconds,
30: 		        uint16 _maxTWAPTickDifference,
31: 		        address _zeroxRouter,
32: 		        address _universalRouter
33: 		    ) Automator(_npm, _operator, _withdrawer, _TWAPSeconds, _maxTWAPTickDifference, _zeroxRouter, _universalRouter) {}
```

*GitHub* : [25-33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L25-L33)

```solidity
File: src/transformers/LeverageTransformer.sol

13: 		    constructor(INonfungiblePositionManager _nonfungiblePositionManager, address _zeroxRouter, address _universalRouter)
14: 		        Swapper(_nonfungiblePositionManager, _zeroxRouter, _universalRouter)
15: 		    {}
```

*GitHub* : [13-15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L13-L15)

```solidity
File: src/utils/FlashloanLiquidator.sol

24: 		    constructor(INonfungiblePositionManager _nonfungiblePositionManager, address _zeroxRouter, address _universalRouter)
25: 		        Swapper(_nonfungiblePositionManager, _zeroxRouter, _universalRouter)
26: 		    {}
```

*GitHub* : [24-26](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L24-L26)

### [N-38]<a name="n-38"></a> Control structures do not comply with best practices

This is a [best practice](https://docs.soliditylang.org/en/latest/style-guide.html#control-structures) that should be followed. 

*There are 9 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

88: 		        if (
```

*GitHub* : [88](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L88)

```solidity
File: src/V3Vault.sol

790: 		        if (

1227: 		                if (

1235: 		                if (
```

*GitHub* : [790](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L790), [1227](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1227), [1235](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1235)

```solidity
File: src/automators/AutoExit.sol

112: 		        if (
```

*GitHub* : [112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L112)

```solidity
File: src/transformers/AutoRange.sol

122: 		        if (

166: 		        if (

174: 		            if (
```

*GitHub* : [122](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L122), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L166), [174](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L174)

```solidity
File: src/transformers/V3Utils.sol

696: 		        if (
```

*GitHub* : [696](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L696)

### [N-39]<a name="n-39"></a> Use a single file for system wide constants

Consider grouping all the system constants under a single file. This finding shows only the first constant for each file, for brevity.

*There are 5 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

12: 		    uint256 private constant Q96 = 2 ** 96;
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L12)

```solidity
File: src/V3Oracle.sol

25: 		    uint16 public constant MIN_PRICE_DIFFERENCE = 200; //2%
```

*GitHub* : [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L25)

```solidity
File: src/V3Vault.sol

33: 		    uint256 private constant Q32 = 2 ** 32;
```

*GitHub* : [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L33)

```solidity
File: src/automators/Automator.sol

20: 		    uint256 internal constant Q64 = 2 ** 64;
```

*GitHub* : [20](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L20)

```solidity
File: src/transformers/AutoCompound.sol

47: 		    uint64 public constant MAX_REWARD_X64 = uint64(Q64 / 50); // 2%
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L47)

### [N-40]<a name="n-40"></a> Event does not have proper `indexed` fields

Index event fields make the field more quickly accessible to off-chain tools that parse events. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields).

Each event should use three `indexed` fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three fields, all of the fields should be indexed.

*There are 22 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit emergencyAdmin
33: 		    event SetEmergencyAdmin(address emergencyAdmin);
```

*GitHub* : [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L33)

```solidity
File: src/V3Vault.sol

// @audit owner, target
68: 		    event ApprovedTransform(uint256 indexed tokenId, address owner, address target, bool isActive);

// @audit owner
70: 		    event Add(uint256 indexed tokenId, address owner, uint256 oldTokenId); // when a token is added replacing another token - oldTokenId > 0

// @audit recipient
71: 		    event Remove(uint256 indexed tokenId, address recipient);

// @audit owner, recipient
75: 		    event WithdrawCollateral(
76: 		        uint256 indexed tokenId, address owner, address recipient, uint128 liquidity, uint256 amount0, uint256 amount1
77: 		    );

// @audit owner
78: 		    event Borrow(uint256 indexed tokenId, address owner, uint256 assets, uint256 shares);

// @audit repayer, owner
79: 		    event Repay(uint256 indexed tokenId, address repayer, address owner, uint256 assets, uint256 shares);

// @audit liquidator, owner
80: 		    event Liquidate(
81: 		        uint256 indexed tokenId,
82: 		        address liquidator,
83: 		        address owner,
84: 		        uint256 value,
85: 		        uint256 cost,
86: 		        uint256 amount0,
87: 		        uint256 amount1,
88: 		        uint256 reserve,
89: 		        uint256 missing
90: 		    ); // shows exactly how liquidation amounts were divided

// @audit receiver
93: 		    event WithdrawReserves(uint256 amount, address receiver);

// @audit transformer
94: 		    event SetTransformer(address transformer, bool active);

// @audit token
104: 		    event SetTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32);

// @audit emergencyAdmin
106: 		    event SetEmergencyAdmin(address emergencyAdmin);
```

*GitHub* : [68](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L68), [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L70), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L71), [75-77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L75-L77), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L78), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L79), [80-90](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L80-L90), [93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L93), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L94), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L104), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L106)

```solidity
File: src/automators/AutoExit.sol

// @audit account, token0, token1
11: 		    event Executed(
12: 		        uint256 indexed tokenId,
13: 		        address account,
14: 		        bool isSwap,
15: 		        uint256 amountReturned0,
16: 		        uint256 amountReturned1,
17: 		        address token0,
18: 		        address token1
19: 		    );
```

*GitHub* : [11-19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L11-L19)

```solidity
File: src/automators/Automator.sol

// @audit newOperator
27: 		    event OperatorChanged(address newOperator, bool active);

// @audit newVault
28: 		    event VaultChanged(address newVault, bool active);

// @audit newWithdrawer
30: 		    event WithdrawerChanged(address newWithdrawer);
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L27), [28](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L28), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L30)

```solidity
File: src/transformers/AutoCompound.sol

// @audit account, token0, token1
18: 		    event AutoCompounded(
19: 		        address account,
20: 		        uint256 tokenId,
21: 		        uint256 amountAdded0,
22: 		        uint256 amountAdded1,
23: 		        uint256 reward0,
24: 		        uint256 reward1,
25: 		        address token0,
26: 		        address token1
27: 		    );

// @audit account
30: 		    event RewardUpdated(address account, uint64 totalRewardX64);

// @audit token
33: 		    event BalanceAdded(uint256 tokenId, address token, uint256 amount);

// @audit token
34: 		    event BalanceRemoved(uint256 tokenId, address token, uint256 amount);

// @audit token, to
35: 		    event BalanceWithdrawn(uint256 tokenId, address token, address to, uint256 amount);
```

*GitHub* : [18-27](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L18-L27), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L30), [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L33), [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L34), [35](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L35)

```solidity
File: src/transformers/V3Utils.sol

// @audit token
24: 		    event WithdrawAndCollectAndSwap(uint256 indexed tokenId, address token, uint256 amount);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L24)

### [N-41]<a name="n-41"></a> Old Solidity version

Use a more recent version of Solidity: the latest version is 0.8.24, but it's safer to use at least the version 0.8.19 to get the latest bugfixes and features when deploying on L2.

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L2)

```solidity
File: src/V3Oracle.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L2)

```solidity
File: src/V3Vault.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L2)

```solidity
File: src/automators/AutoExit.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L2)

```solidity
File: src/automators/Automator.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L2)

```solidity
File: src/transformers/AutoCompound.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L2)

```solidity
File: src/transformers/AutoRange.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L2)

```solidity
File: src/transformers/LeverageTransformer.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L2)

```solidity
File: src/transformers/V3Utils.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L2)

```solidity
File: src/utils/FlashloanLiquidator.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L2)

```solidity
File: src/utils/Swapper.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L2)

### [N-42]<a name="n-42"></a> Use of floating pragma

Locking the pragma helps avoid accidental deploys with an outdated compiler version that may introduce bugs and unexpected vulnerabilities.

Floating pragma is meant to be used for libraries and contracts that have external users and need backward compatibility.

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L2)

```solidity
File: src/V3Oracle.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L2)

```solidity
File: src/V3Vault.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L2)

```solidity
File: src/automators/AutoExit.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L2)

```solidity
File: src/automators/Automator.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L2)

```solidity
File: src/transformers/AutoCompound.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L2)

```solidity
File: src/transformers/AutoRange.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L2)

```solidity
File: src/transformers/LeverageTransformer.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L2)

```solidity
File: src/transformers/V3Utils.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L2)

```solidity
File: src/utils/FlashloanLiquidator.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L2)

```solidity
File: src/utils/Swapper.sol

2: 		pragma solidity ^0.8.0;
```

*GitHub* : [2](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L2)

### [N-43]<a name="n-43"></a> Contract functions should use an `interface`

All `external`/`public` functions should override an `interface`. This is useful to make sure that the whole API is extracted.

*There are 37 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

46: 		    function getUtilizationRateX96(uint256 cash, uint256 debt) public pure returns (uint256) {

82: 		    function setValues(
```

*GitHub* : [46](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L46), [82](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L82)

```solidity
File: src/V3Oracle.sol

185: 		    function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

201: 		    function setTokenConfig(

249: 		    function setOracleMode(address token, Mode mode) external {

265: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [185](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L185), [201](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L201), [249](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L249), [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L265)

```solidity
File: src/V3Vault.sol

765: 		    function withdrawReserves(uint256 amount, address receiver) external onlyOwner {

788: 		    function setTransformer(address transformer, bool active) external onlyOwner {

807: 		    function setLimits(

837: 		    function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

844: 		    function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

856: 		    function setTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32)

870: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [765](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L765), [788](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L788), [807](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L807), [837](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L837), [844](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L844), [856](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L856), [870](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L870)

```solidity
File: src/automators/AutoExit.sol

100: 		    function execute(ExecuteParams calldata params) external {

218: 		    function configToken(uint256 tokenId, PositionConfig calldata config) external {
```

*GitHub* : [100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L100), [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L218)

```solidity
File: src/automators/Automator.sol

59: 		    function setWithdrawer(address _withdrawer) public onlyOwner {

69: 		    function setOperator(address _operator, bool _active) public onlyOwner {

79: 		    function setVault(address _vault, bool _active) public onlyOwner {

87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {

104: 		    function withdrawBalances(address[] calldata tokens, address to) external virtual {

123: 		    function withdrawETH(address to) external {
```

*GitHub* : [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L59), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L69), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L79), [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L104), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L123)

```solidity
File: src/transformers/AutoCompound.sol

87: 		    function executeWithVault(ExecuteParams calldata params, address vault) external {

101: 		    function execute(ExecuteParams calldata params) external nonReentrant {

200: 		    function withdrawLeftoverBalances(uint256 tokenId, address to) external nonReentrant {

243: 		    function setReward(uint64 _totalRewardX64) external onlyOwner {
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L87), [101](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L101), [200](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L200), [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L243)

```solidity
File: src/transformers/AutoRange.sol

97: 		    function executeWithVault(ExecuteParams calldata params, address vault) external {

111: 		    function execute(ExecuteParams calldata params) external {

276: 		    function configToken(uint256 tokenId, address vault, PositionConfig calldata config) external {
```

*GitHub* : [97](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L97), [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L111), [276](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L276)

```solidity
File: src/transformers/LeverageTransformer.sol

40: 		    function leverageUp(LeverageUpParams calldata params) external {

123: 		    function leverageDown(LeverageDownParams calldata params) external {
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L40), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L123)

```solidity
File: src/transformers/V3Utils.sol

98: 		    function executeWithPermit(uint256 tokenId, Instructions memory instructions, uint8 v, bytes32 r, bytes32 s)

115: 		    function execute(uint256 tokenId, Instructions memory instructions) public returns (uint256 newTokenId) {

397: 		    function swap(SwapParams calldata params) external payable returns (uint256 amountOut) {

467: 		    function swapAndMint(SwapAndMintParams calldata params)

532: 		    function swapAndIncreaseLiquidity(SwapAndIncreaseLiquidityParams calldata params)
```

*GitHub* : [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L98), [115](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L115), [397](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L397), [467](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L467), [532](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L532)

```solidity
File: src/utils/FlashloanLiquidator.sol

41: 		    function liquidate(LiquidateParams calldata params) external {

67: 		    function uniswapV3FlashCallback(uint256 fee0, uint256 fee1, bytes calldata callbackData) external {
```

*GitHub* : [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L41), [67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L67)

### [N-44]<a name="n-44"></a> `require`/`revert` without any message

If a transaction reverts, it can be confusing to debug if there aren't any messages. Add a descriptive message to all `require`/`revert` statements.

*There are 1 instance(s) of this issue:*

```solidity
File: src/utils/Swapper.sol

157: 		        require(amount0Delta > 0 || amount1Delta > 0); // swaps entirely within 0-liquidity regions are not supported
```

*GitHub* : [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L157)

### [N-45]<a name="n-45"></a> Some error strings are not descriptive

Consider adding more detail to the following error messages. It is recommended to keep the message size under 32 chars to avoid adding a gas overhead.

*There are 1 instance(s) of this issue:*

```solidity
File: src/transformers/AutoCompound.sol

244: 		        require(_totalRewardX64 <= totalRewardX64, ">totalRewardX64");
```

*GitHub* : [244](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L244)

### [N-46]<a name="n-46"></a> `else` block is not required

Consider moving the logic outside the `else` block, and then removing it (it's not required, as the function is returning a value). There will be one less level of nesting, which will improve the quality of the codebase.

*There are 6 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

306: 		        } else {
307: 		            return globalLendLimit - value;
308: 		        }

317: 		        } else {
318: 		            return _convertToShares(globalLendLimit - value, lendExchangeRateX96, Math.Rounding.Down);
319: 		        }
```

*GitHub* : [306-308](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L306-L308), [317-319](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L317-L319)

```solidity
File: src/automators/Automator.sol

174: 		        } else {
175: 		            return false;
176: 		        }
```

*GitHub* : [174-176](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L174-L176)

```solidity
File: src/transformers/AutoRange.sol

269: 		        } else {
270: 		            revert NotReady();
271: 		        }
```

*GitHub* : [269-271](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L269-L271)

```solidity
File: src/transformers/V3Utils.sol

349: 		        } else {
350: 		            revert NotSupportedWhatToDo();
351: 		        }
```

*GitHub* : [349-351](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L349-L351)

```solidity
File: src/utils/Swapper.sol

100: 		            } else {
101: 		                revert WrongContract();
102: 		            }
```

*GitHub* : [100-102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L100-L102)

### [N-47]<a name="n-47"></a> Multiple `address`/ID mappings can be combined into a single mapping of an `address`/ID to a `struct`, for readability

Well-organized data structures make code reviews easier, which may lead to fewer bugs. Consider combining related mappings into mappings to structs, so it's clear what data is related.

*There are 2 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit consider merging ownedTokensIndex, tokenOwner
158: 		    mapping(uint256 => uint256) private ownedTokensIndex; // Mapping from token ID to index of the owner tokens list (for removal without loop)
159: 		    mapping(uint256 => address) private tokenOwner; // Mapping from token ID to owner

// @audit consider merging transformerAllowList, transformApprovals
163: 		    mapping(address => bool) public transformerAllowList; // contracts allowed to transform positions (selected audited contracts e.g. V3Utils)
164: 		    mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)
```

*GitHub* : [158](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L158), [163](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L163)

### [N-48]<a name="n-48"></a> Lack of specific `import` identifier

It is better to use `import {<identifier>} from "<file.sol>"` instead of `import "<file.sol>"` to improve readability and speed up the compilation time.

*There are 70 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";

6: 		import "./interfaces/IInterestRateModel.sol";

7: 		import "./interfaces/IErrors.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L4), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L6), [7](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L7)

```solidity
File: src/V3Oracle.sol

4: 		import "v3-core/interfaces/IUniswapV3Factory.sol";

5: 		import "v3-core/interfaces/IUniswapV3Pool.sol";

7: 		import "v3-core/libraries/TickMath.sol";

9: 		import "v3-periphery/libraries/PoolAddress.sol";

10: 		import "v3-periphery/libraries/LiquidityAmounts.sol";

12: 		import "v3-periphery/interfaces/INonfungiblePositionManager.sol";

14: 		import "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

15: 		import "@openzeppelin/contracts/access/Ownable.sol";

17: 		import "../lib/AggregatorV3Interface.sol";

19: 		import "./interfaces/IV3Oracle.sol";

20: 		import "./interfaces/IErrors.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L5), [7](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L7), [9](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L9), [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L10), [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L12), [14](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L14), [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L15), [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L17), [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L19), [20](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L20)

```solidity
File: src/V3Vault.sol

4: 		import "v3-core/interfaces/IUniswapV3Factory.sol";

5: 		import "v3-core/interfaces/IUniswapV3Pool.sol";

6: 		import "v3-core/libraries/TickMath.sol";

7: 		import "v3-core/libraries/FixedPoint128.sol";

9: 		import "v3-periphery/libraries/LiquidityAmounts.sol";

10: 		import "v3-periphery/interfaces/INonfungiblePositionManager.sol";

12: 		import "@openzeppelin/contracts/utils/math/Math.sol";

13: 		import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

14: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

15: 		import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

16: 		import "@openzeppelin/contracts/access/Ownable.sol";

17: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

18: 		import "@openzeppelin/contracts/utils/Multicall.sol";

20: 		import "permit2/interfaces/IPermit2.sol";

22: 		import "./interfaces/IVault.sol";

23: 		import "./interfaces/IV3Oracle.sol";

24: 		import "./interfaces/IInterestRateModel.sol";

25: 		import "./interfaces/IErrors.sol";
```

*GitHub* : [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L5), [7](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L7), [9](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L9), [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L10), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L6), [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L12), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L13), [14](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L14), [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L4), [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L15), [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L16), [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L17), [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L18), [20](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L20), [22](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L22), [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L23), [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L24), [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L25)

```solidity
File: src/automators/AutoExit.sol

4: 		import "./Automator.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L4)

```solidity
File: src/automators/Automator.sol

4: 		import "@openzeppelin/contracts/access/Ownable.sol";

5: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

6: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

8: 		import "v3-core/interfaces/IUniswapV3Factory.sol";

9: 		import "v3-core/interfaces/IUniswapV3Pool.sol";

10: 		import "v3-core/libraries/TickMath.sol";

11: 		import "v3-core/libraries/FullMath.sol";

13: 		import "v3-periphery/interfaces/INonfungiblePositionManager.sol";

15: 		import "../../lib/IWETH9.sol";

16: 		import "../utils/Swapper.sol";

17: 		import "../interfaces/IVault.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L5), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L6), [8](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L8), [9](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L9), [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L10), [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L11), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L13), [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L15), [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L16), [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L17)

```solidity
File: src/transformers/AutoCompound.sol

4: 		import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

5: 		import "@openzeppelin/contracts/utils/Multicall.sol";

6: 		import "@openzeppelin/contracts/utils/math/SafeMath.sol";

8: 		import "v3-periphery/interfaces/INonfungiblePositionManager.sol";

10: 		import "../automators/Automator.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L5), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L6), [8](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L8), [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L10)

```solidity
File: src/transformers/AutoRange.sol

4: 		import "../automators/Automator.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L4)

```solidity
File: src/transformers/LeverageTransformer.sol

4: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

5: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

7: 		import "../utils/Swapper.sol";

8: 		import "../interfaces/IVault.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L5), [7](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L7), [8](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L8)

```solidity
File: src/transformers/V3Utils.sol

4: 		import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

5: 		import "@openzeppelin/contracts/utils/math/SafeCast.sol";

7: 		import "permit2/interfaces/IPermit2.sol";

9: 		import "../utils/Swapper.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L5), [7](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L7), [9](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L9)

```solidity
File: src/utils/FlashloanLiquidator.sol

4: 		import "v3-core/interfaces/IUniswapV3Pool.sol";

5: 		import "v3-core/interfaces/callback/IUniswapV3FlashCallback.sol";

7: 		import "../interfaces/IVault.sol";

8: 		import "./Swapper.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L4), [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L5), [7](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L7), [8](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L8)

```solidity
File: src/utils/Swapper.sol

4: 		import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

6: 		import "v3-core/interfaces/callback/IUniswapV3SwapCallback.sol";

7: 		import "v3-core/interfaces/IUniswapV3Pool.sol";

8: 		import "v3-core/libraries/TickMath.sol";

10: 		import "v3-periphery/interfaces/INonfungiblePositionManager.sol";

12: 		import "../../lib/IWETH9.sol";

13: 		import "../../lib/IUniversalRouter.sol";

14: 		import "../interfaces/IErrors.sol";
```

*GitHub* : [4](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L4), [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L6), [7](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L7), [8](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L8), [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L10), [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L12), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L13), [14](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L14)

### [N-49]<a name="n-49"></a> Imports should be organized more systematically

The contract's interface should be imported first, followed by each of the interfaces it uses, followed by all other files. The examples below do not follow this layout.

*There are 9 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

6: 		import "./interfaces/IInterestRateModel.sol";
```

*GitHub* : [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L6)

```solidity
File: src/V3Oracle.sol

15: 		import "@openzeppelin/contracts/access/Ownable.sol";
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L15)

```solidity
File: src/V3Vault.sol

13: 		import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
```

*GitHub* : [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L13)

```solidity
File: src/automators/Automator.sol

16: 		import "../utils/Swapper.sol";
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L16)

```solidity
File: src/transformers/AutoCompound.sol

10: 		import "../automators/Automator.sol";
```

*GitHub* : [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L10)

```solidity
File: src/transformers/LeverageTransformer.sol

7: 		import "../utils/Swapper.sol";
```

*GitHub* : [7](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L7)

```solidity
File: src/transformers/V3Utils.sol

9: 		import "../utils/Swapper.sol";
```

*GitHub* : [9](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L9)

```solidity
File: src/utils/FlashloanLiquidator.sol

5: 		import "v3-core/interfaces/callback/IUniswapV3FlashCallback.sol";
```

*GitHub* : [5](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L5)

```solidity
File: src/utils/Swapper.sol

6: 		import "v3-core/interfaces/callback/IUniswapV3SwapCallback.sol";
```

*GitHub* : [6](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L6)

### [N-50]<a name="n-50"></a> Top-level declarations should be separated by at least two lines

Surround top level declarations in Solidity source with two blank lines. [Documentation](https://docs.soliditylang.org/en/latest/style-guide.html#blank-lines)

*There are 22 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

131: 		    }
132: 		
133: 		    function _checkPoolPrice(address token0, address token1, uint24 fee, uint256 derivedPoolPriceX96) internal view {

137: 		    }
138: 		
139: 		    function _requireMaxDifference(uint256 priceX96, uint256 verifyPriceX96, uint256 maxDifferenceX10000)
```

*GitHub* : [131-133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L131-L133), [137-139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L137-L139)

```solidity
File: src/V3Vault.sol

952: 		    }
953: 		
954: 		    function _repay(uint256 tokenId, uint256 amount, bool isShare, bytes memory permitData) internal {

1141: 		    }
1142: 		
1143: 		    function _calculateTokenCollateralFactorX32(uint256 tokenId) internal view returns (uint32) {

1148: 		    }
1149: 		
1150: 		    function _updateGlobalInterest()

1165: 		    }
1166: 		
1167: 		    function _calculateGlobalInterest()

1195: 		    }
1196: 		
1197: 		    function _requireLoanIsHealthy(uint256 tokenId, uint256 debt) internal view {

1244: 		    }
1245: 		
1246: 		    function _resetDailyLendIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

1256: 		    }
1257: 		
1258: 		    function _resetDailyDebtIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

1268: 		    }
1269: 		
1270: 		    function _checkLoanIsHealthy(uint256 tokenId, uint256 debt)

1279: 		    }
1280: 		
1281: 		    function _convertToShares(uint256 amount, uint256 exchangeRateX96, Math.Rounding rounding)

1287: 		    }
1288: 		
1289: 		    function _convertToAssets(uint256 shares, uint256 exchangeRateX96, Math.Rounding rounding)

1295: 		    }
1296: 		
1297: 		    function _addTokenToOwner(address to, uint256 tokenId) internal {

1301: 		    }
1302: 		
1303: 		    function _removeTokenFromOwner(address from, uint256 tokenId) internal {
```

*GitHub* : [952-954](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L952-L954), [1141-1143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1141-L1143), [1148-1150](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1148-L1150), [1165-1167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1165-L1167), [1195-1197](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1195-L1197), [1244-1246](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1244-L1246), [1256-1258](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1256-L1258), [1268-1270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1268-L1270), [1279-1281](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1279-L1281), [1287-1289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1287-L1289), [1295-1297](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1295-L1297), [1301-1303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1301-L1303)

```solidity
File: src/automators/Automator.sol

191: 		    }
192: 		
193: 		    function _decreaseFullLiquidityAndCollect(

228: 		    }
229: 		
230: 		    function _validateOwner(uint256 tokenId, address vault) internal returns (address owner) {
```

*GitHub* : [191-193](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L191-L193), [228-230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L228-L230)

```solidity
File: src/transformers/AutoCompound.sol

247: 		    }
248: 		
249: 		    function _increaseBalance(uint256 tokenId, address token, uint256 amount) internal {

252: 		    }
253: 		
254: 		    function _setBalance(uint256 tokenId, address token, uint256 amount) internal {

264: 		    }
265: 		
266: 		    function _withdrawBalanceInternal(uint256 tokenId, address token, address to, uint256 balance, uint256 amount)

274: 		    }
275: 		
276: 		    function _checkApprovals(address token0, address token1) internal {
```

*GitHub* : [247-249](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L247-L249), [252-254](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L252-L254), [264-266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L264-L266), [274-276](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L274-L276)

```solidity
File: src/transformers/V3Utils.sol

564: 		    }
565: 		
566: 		    function _prepareAddApproved(
```

*GitHub* : [564-566](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L564-L566)

```solidity
File: src/utils/FlashloanLiquidator.sol

65: 		    }
66: 		
67: 		    function uniswapV3FlashCallback(uint256 fee0, uint256 fee1, bytes calldata callbackData) external {
```

*GitHub* : [65-67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L65-L67)

### [N-51]<a name="n-51"></a> Use a struct to encapsulate multiple function parameters

If a function has too many parameters, replacing them with a struct can improve code readability and maintainability, increase reusability, and reduce the likelihood of errors when passing the parameters.

*There are 21 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

201: 		    function setTokenConfig(
202: 		        address token,
203: 		        AggregatorV3Interface feed,
204: 		        uint32 maxFeedAge,
205: 		        IUniswapV3Pool pool,
206: 		        uint32 twapSeconds,
207: 		        Mode mode,
208: 		        uint16 maxDifference

472: 		    function _getFeeGrowthInside(
473: 		        IUniswapV3Pool pool,
474: 		        int24 tickLower,
475: 		        int24 tickUpper,
476: 		        int24 tickCurrent,
477: 		        uint256 feeGrowthGlobal0X128,
478: 		        uint256 feeGrowthGlobal1X128
```

*GitHub* : [201-208](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L201-L208), [472-478](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L472-L478)

```solidity
File: src/V3Vault.sol

169: 		    constructor(
170: 		        string memory name,
171: 		        string memory symbol,
172: 		        address _asset,
173: 		        INonfungiblePositionManager _nonfungiblePositionManager,
174: 		        IInterestRateModel _interestRateModel,
175: 		        IV3Oracle _oracle,
176: 		        IPermit2 _permit2

410: 		    function createWithPermit(
411: 		        uint256 tokenId,
412: 		        address owner,
413: 		        address recipient,
414: 		        uint256 deadline,
415: 		        uint8 v,
416: 		        bytes32 r,
417: 		        bytes32 s

807: 		    function setLimits(
808: 		        uint256 _minLoanSize,
809: 		        uint256 _globalLendLimit,
810: 		        uint256 _globalDebtLimit,
811: 		        uint256 _dailyLendIncreaseLimitMin,
812: 		        uint256 _dailyDebtIncreaseLimitMin

1032: 		    function _sendPositionValue(
1033: 		        uint256 tokenId,
1034: 		        uint256 liquidationValue,
1035: 		        uint256 fullValue,
1036: 		        uint256 feeValue,
1037: 		        address recipient

1205: 		    function _updateAndCheckCollateral(
1206: 		        uint256 tokenId,
1207: 		        uint256 debtExchangeRateX96,
1208: 		        uint256 lendExchangeRateX96,
1209: 		        uint256 oldShares,
1210: 		        uint256 newShares
```

*GitHub* : [169-176](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L169-L176), [410-417](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L410-L417), [807-812](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L807-L812), [1032-1037](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1032-L1037), [1205-1210](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1205-L1210)

```solidity
File: src/automators/AutoExit.sol

33: 		    constructor(
34: 		        INonfungiblePositionManager _npm,
35: 		        address _operator,
36: 		        address _withdrawer,
37: 		        uint32 _TWAPSeconds,
38: 		        uint16 _maxTWAPTickDifference,
39: 		        address _zeroxRouter,
40: 		        address _universalRouter
```

*GitHub* : [33-40](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L33-L40)

```solidity
File: src/automators/Automator.sol

41: 		    constructor(
42: 		        INonfungiblePositionManager npm,
43: 		        address _operator,
44: 		        address _withdrawer,
45: 		        uint32 _TWAPSeconds,
46: 		        uint16 _maxTWAPTickDifference,
47: 		        address _zeroxRouter,
48: 		        address _universalRouter

139: 		    function _validateSwap(
140: 		        bool swap0For1,
141: 		        uint256 amountIn,
142: 		        IUniswapV3Pool pool,
143: 		        uint32 twapPeriod,
144: 		        uint16 maxTickDifference,
145: 		        uint64 maxPriceDifferenceX64

193: 		    function _decreaseFullLiquidityAndCollect(
194: 		        uint256 tokenId,
195: 		        uint128 liquidity,
196: 		        uint256 amountRemoveMin0,
197: 		        uint256 amountRemoveMin1,
198: 		        uint256 deadline
```

*GitHub* : [41-48](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L41-L48), [139-145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L139-L145), [193-198](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L193-L198)

```solidity
File: src/transformers/AutoCompound.sol

37: 		    constructor(
38: 		        INonfungiblePositionManager _npm,
39: 		        address _operator,
40: 		        address _withdrawer,
41: 		        uint32 _TWAPSeconds,
42: 		        uint16 _maxTWAPTickDifference

266: 		    function _withdrawBalanceInternal(uint256 tokenId, address token, address to, uint256 balance, uint256 amount)
```

*GitHub* : [37-42](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L37-L42), [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L266)

```solidity
File: src/transformers/AutoRange.sol

25: 		    constructor(
26: 		        INonfungiblePositionManager _npm,
27: 		        address _operator,
28: 		        address _withdrawer,
29: 		        uint32 _TWAPSeconds,
30: 		        uint16 _maxTWAPTickDifference,
31: 		        address _zeroxRouter,
32: 		        address _universalRouter
```

*GitHub* : [25-32](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L25-L32)

```solidity
File: src/transformers/V3Utils.sol

98: 		    function executeWithPermit(uint256 tokenId, Instructions memory instructions, uint8 v, bytes32 r, bytes32 s)

566: 		    function _prepareAddApproved(
567: 		        IERC20 token0,
568: 		        IERC20 token1,
569: 		        IERC20 otherToken,
570: 		        uint256 amount0,
571: 		        uint256 amount1,
572: 		        uint256 amountOther

598: 		    function _prepareAddPermit2(
599: 		        IERC20 token0,
600: 		        IERC20 token1,
601: 		        IERC20 otherToken,
602: 		        uint256 amount0,
603: 		        uint256 amount1,
604: 		        uint256 amountOther,
605: 		        IPermit2.PermitBatchTransferFrom memory permit,
606: 		        bytes memory signature

653: 		    function _prepareAdd(
654: 		        IERC20 token0,
655: 		        IERC20 token1,
656: 		        IERC20 otherToken,
657: 		        uint256 amount0,
658: 		        uint256 amount1,
659: 		        uint256 amountOther

841: 		    function _returnLeftoverTokens(
842: 		        address to,
843: 		        IERC20 token0,
844: 		        IERC20 token1,
845: 		        uint256 total0,
846: 		        uint256 total1,
847: 		        uint256 added0,
848: 		        uint256 added1,
849: 		        bool unwrap

877: 		    function _decreaseLiquidity(
878: 		        uint256 tokenId,
879: 		        uint128 liquidity,
880: 		        uint256 deadline,
881: 		        uint256 token0Min,
882: 		        uint256 token1Min

892: 		    function _collectFees(uint256 tokenId, IERC20 token0, IERC20 token1, uint128 collectAmount0, uint128 collectAmount1)
```

*GitHub* : [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L98), [566-572](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L566-L572), [598-606](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L598-L606), [653-659](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L653-L659), [841-849](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L841-L849), [877-882](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L877-L882), [892](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L892)

### [N-52]<a name="n-52"></a> Returning a struct instead of returning many variables is better

If a function returns [too many variables](https://docs.soliditylang.org/en/latest/contracts.html#returning-multiple-values), replacing them with a struct can improve code readability, maintainability and reusability.

*There are 10 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

95: 		    function getValue(uint256 tokenId, address token)
96: 		        external
97: 		        view
98: 		        override
99: 		        returns (uint256 value, uint256 feeValue, uint256 price0X96, uint256 price1X96)

162: 		    function getPositionBreakdown(uint256 tokenId)
163: 		        public
164: 		        view
165: 		        override
166: 		        returns (
167: 		            address token0,
168: 		            address token1,
169: 		            uint24 fee,
170: 		            uint128 liquidity,
171: 		            uint256 amount0,
172: 		            uint256 amount1,
173: 		            uint128 fees0,
174: 		            uint128 fees1

426: 		    function _getAmounts(PositionState memory state)
427: 		        internal
428: 		        view
429: 		        returns (uint256 amount0, uint256 amount1, uint128 fees0, uint128 fees1)
```

*GitHub* : [95-99](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L95-L99), [162-174](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L162-L174), [426-429](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L426-L429)

```solidity
File: src/V3Vault.sol

195: 		    function vaultInfo()
196: 		        external
197: 		        view
198: 		        override
199: 		        returns (
200: 		            uint256 debt,
201: 		            uint256 lent,
202: 		            uint256 balance,
203: 		            uint256 available,
204: 		            uint256 reserves,
205: 		            uint256 debtExchangeRateX96,
206: 		            uint256 lendExchangeRateX96

231: 		    function loanInfo(uint256 tokenId)
232: 		        external
233: 		        view
234: 		        override
235: 		        returns (
236: 		            uint256 debt,
237: 		            uint256 fullValue,
238: 		            uint256 collateralValue,
239: 		            uint256 liquidationCost,
240: 		            uint256 liquidationValue

1270: 		    function _checkLoanIsHealthy(uint256 tokenId, uint256 debt)
1271: 		        internal
1272: 		        view
1273: 		        returns (bool isHealthy, uint256 fullValue, uint256 collateralValue, uint256 feeValue)
```

*GitHub* : [195-206](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L195-L206), [231-240](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L231-L240), [1270-1273](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1270-L1273)

```solidity
File: src/automators/Automator.sol

139: 		    function _validateSwap(
140: 		        bool swap0For1,
141: 		        uint256 amountIn,
142: 		        IUniswapV3Pool pool,
143: 		        uint32 twapPeriod,
144: 		        uint16 maxTickDifference,
145: 		        uint64 maxPriceDifferenceX64
146: 		    ) internal view returns (uint256 amountOutMin, int24 currentTick, uint160 sqrtPriceX96, uint256 priceX96) {

193: 		    function _decreaseFullLiquidityAndCollect(
194: 		        uint256 tokenId,
195: 		        uint128 liquidity,
196: 		        uint256 amountRemoveMin0,
197: 		        uint256 amountRemoveMin1,
198: 		        uint256 deadline
199: 		    ) internal returns (uint256 amount0, uint256 amount1, uint256 feeAmount0, uint256 feeAmount1) {
```

*GitHub* : [139-146](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L139-L146), [193-199](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L193-L199)

```solidity
File: src/transformers/V3Utils.sol

467: 		    function swapAndMint(SwapAndMintParams calldata params)
468: 		        external
469: 		        payable
470: 		        returns (uint256 tokenId, uint128 liquidity, uint256 amount0, uint256 amount1)

705: 		    function _swapAndMint(SwapAndMintParams memory params, bool unwrap)
706: 		        internal
707: 		        returns (uint256 tokenId, uint128 liquidity, uint256 added0, uint256 added1)
```

*GitHub* : [467-470](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L467-L470), [705-707](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L705-L707)

### [N-53]<a name="n-53"></a> Event is missing `msg.sender` parameter

The following functions are missing some parameters when emitting an event: when dealing with a source address which uses the value of `msg.sender`, the `msg.sender` value should be specified in every event.

Otherwise, a contract or web page listening to events cannot react to connected users: basically, those events cannot be used properly.

*There are 41 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

100: 		        emit SetValues(baseRatePerYearX96, multiplierPerYearX96, jumpMultiplierPerYearX96, _kinkX96);
```

*GitHub* : [100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L100)

```solidity
File: src/V3Oracle.sol

190: 		        emit SetMaxPoolPriceDifference(_maxPoolPriceDifference);

242: 		        emit TokenConfigUpdated(token, config);

243: 		        emit OracleModeUpdated(token, mode);

260: 		        emit OracleModeUpdated(token, mode);

267: 		        emit SetEmergencyAdmin(admin);
```

*GitHub* : [190](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L190), [242](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L242), [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L243), [260](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L260), [267](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L267)

```solidity
File: src/V3Vault.sol

449: 		            emit Add(tokenId, owner, 0);

464: 		                emit Add(tokenId, owner, oldTokenId);

601: 		        emit Borrow(tokenId, owner, assets, shares);

645: 		        emit WithdrawCollateral(params.tokenId, owner, params.recipient, params.liquidity, amount0, amount1);

782: 		        emit WithdrawReserves(amount, receiver);

798: 		        emit SetTransformer(transformer, active);

830: 		        emit SetLimits(
831: 		            _minLoanSize, _globalLendLimit, _globalDebtLimit, _dailyLendIncreaseLimitMin, _dailyDebtIncreaseLimitMin
832: 		        );

839: 		        emit SetReserveFactor(_reserveFactorX32);

849: 		        emit SetReserveProtectionFactor(_reserveProtectionFactorX32);

865: 		        emit SetTokenConfig(token, collateralFactorX32, collateralValueLimitFactorX32);

872: 		        emit SetEmergencyAdmin(admin);

1084: 		        emit Remove(tokenId, owner);

1139: 		            emit ExchangeRateUpdate(newDebtExchangeRateX96, newLendExchangeRateX96);

1160: 		            emit ExchangeRateUpdate(newDebtExchangeRateX96, newLendExchangeRateX96);
```

*GitHub* : [782](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L782), [449](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L449), [464](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L464), [601](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L601), [645](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L645), [798](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L798), [830-832](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L830-L832), [839](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L839), [849](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L849), [865](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L865), [872](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L872), [1084](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1084), [1139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1139), [1160](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1160)

```solidity
File: src/automators/AutoExit.sol

208: 		        emit PositionConfigured(params.tokenId, false, false, false, 0, 0, 0, 0, false, 0);

232: 		        emit PositionConfigured(
233: 		            tokenId,
234: 		            config.isActive,
235: 		            config.token0Swap,
236: 		            config.token1Swap,
237: 		            config.token0TriggerTick,
238: 		            config.token1TriggerTick,
239: 		            config.token0SlippageX64,
240: 		            config.token1SlippageX64,
241: 		            config.onlyFees,
242: 		            config.maxRewardX64
243: 		        );
```

*GitHub* : [208](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L208), [232-243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L232-L243)

```solidity
File: src/automators/Automator.sol

60: 		        emit WithdrawerChanged(_withdrawer);

70: 		        emit OperatorChanged(_operator, _active);

80: 		        emit VaultChanged(_vault, _active);

94: 		        emit TWAPConfigChanged(_TWAPSeconds, _maxTWAPTickDifference);
```

*GitHub* : [60](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L60), [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L70), [80](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L80), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L94)

```solidity
File: src/transformers/AutoCompound.sol

251: 		        emit BalanceAdded(tokenId, token, amount);

259: 		                emit BalanceAdded(tokenId, token, amount - currentBalance);

261: 		                emit BalanceRemoved(tokenId, token, currentBalance - amount);

271: 		        emit BalanceRemoved(tokenId, token, amount);

273: 		        emit BalanceWithdrawn(tokenId, token, to, amount);
```

*GitHub* : [251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L251), [259](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L259), [261](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L261), [271](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L271), [273](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L273)

```solidity
File: src/transformers/AutoRange.sol

252: 		            emit PositionConfigured(
253: 		                state.newTokenId,
254: 		                config.lowerTickLimit,
255: 		                config.upperTickLimit,
256: 		                config.lowerTickDelta,
257: 		                config.upperTickDelta,
258: 		                config.token0SlippageX64,
259: 		                config.token1SlippageX64,
260: 		                config.onlyFees,
261: 		                config.maxRewardX64
262: 		            );

266: 		            emit PositionConfigured(params.tokenId, 0, 0, 0, 0, 0, 0, false, 0);

268: 		            emit RangeChanged(params.tokenId, state.newTokenId);

286: 		        emit PositionConfigured(
287: 		            tokenId,
288: 		            config.lowerTickLimit,
289: 		            config.upperTickLimit,
290: 		            config.lowerTickDelta,
291: 		            config.upperTickDelta,
292: 		            config.token0SlippageX64,
293: 		            config.token1SlippageX64,
294: 		            config.onlyFees,
295: 		            config.maxRewardX64
296: 		        );
```

*GitHub* : [252-262](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L252-L262), [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L266), [268](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L268), [286-296](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L286-L296)

```solidity
File: src/transformers/V3Utils.sol

218: 		            emit CompoundFees(tokenId, liquidity, amount0, amount1);

303: 		            emit ChangeRange(tokenId, newTokenId);

348: 		            emit WithdrawAndCollectAndSwap(tokenId, instructions.targetToken, targetAmount);

729: 		        emit SwapAndMint(tokenId, liquidity, added0, added1);

773: 		        emit SwapAndIncreaseLiquidity(params.tokenId, liquidity, added0, added1);
```

*GitHub* : [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L218), [303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L303), [348](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L348), [729](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L729), [773](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L773)

```solidity
File: src/utils/Swapper.sol

116: 		            emit Swap(address(params.tokenIn), address(params.tokenOut), amountInDelta, amountOutDelta);
```

*GitHub* : [116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L116)

### [N-54]<a name="n-54"></a> Events should emit both new and old values

Events are generally emitted when sensitive changes are made to the contracts.

However, some are missing important parameters, as they should include both the new value and old value where possible.

*There are 19 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

100: 		        emit SetValues(baseRatePerYearX96, multiplierPerYearX96, jumpMultiplierPerYearX96, _kinkX96);
```

*GitHub* : [100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L100)

```solidity
File: src/V3Oracle.sol

190: 		        emit SetMaxPoolPriceDifference(_maxPoolPriceDifference);

242: 		        emit TokenConfigUpdated(token, config);

243: 		        emit OracleModeUpdated(token, mode);

260: 		        emit OracleModeUpdated(token, mode);

267: 		        emit SetEmergencyAdmin(admin);
```

*GitHub* : [190](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L190), [242](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L242), [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L243), [260](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L260), [267](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L267)

```solidity
File: src/V3Vault.sol

798: 		        emit SetTransformer(transformer, active);

830: 		        emit SetLimits(
831: 		            _minLoanSize, _globalLendLimit, _globalDebtLimit, _dailyLendIncreaseLimitMin, _dailyDebtIncreaseLimitMin
832: 		        );

839: 		        emit SetReserveFactor(_reserveFactorX32);

849: 		        emit SetReserveProtectionFactor(_reserveProtectionFactorX32);

865: 		        emit SetTokenConfig(token, collateralFactorX32, collateralValueLimitFactorX32);

872: 		        emit SetEmergencyAdmin(admin);
```

*GitHub* : [798](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L798), [830-832](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L830-L832), [839](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L839), [849](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L849), [865](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L865), [872](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L872)

```solidity
File: src/automators/Automator.sol

60: 		        emit WithdrawerChanged(_withdrawer);

70: 		        emit OperatorChanged(_operator, _active);

80: 		        emit VaultChanged(_vault, _active);

94: 		        emit TWAPConfigChanged(_TWAPSeconds, _maxTWAPTickDifference);
```

*GitHub* : [60](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L60), [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L70), [80](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L80), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L94)

```solidity
File: src/transformers/AutoCompound.sol

246: 		        emit RewardUpdated(msg.sender, _totalRewardX64);

259: 		                emit BalanceAdded(tokenId, token, amount - currentBalance);

261: 		                emit BalanceRemoved(tokenId, token, currentBalance - amount);
```

*GitHub* : [246](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L246), [259](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L259), [261](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L261)

### [N-55]<a name="n-55"></a> Events may be emitted out of order due to reentrancy

If a reentrancy occurs, some events may be emitted in an unexpected order, and this may be a problem if a third party expects a specific order for these events. Ensure that events follow the best practice of CEI.

*There are 20 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit feed.decimals()
242: 		        emit TokenConfigUpdated(token, config);

// @audit feed.decimals()
243: 		        emit OracleModeUpdated(token, mode);
```

*GitHub* : [242](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L242), [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L243)

```solidity
File: src/V3Vault.sol

// @audit nonfungiblePositionManager.decreaseLiquidity(
            INonfungiblePositionManager.DecreaseLiquidityParams(
                params.tokenId, params.liquidity, params.amount0Min, params.amount1Min, params.deadline
            )
        )
645: 		        emit WithdrawCollateral(params.tokenId, owner, params.recipient, params.liquidity, amount0, amount1);

// @audit permit2.permitTransferFrom(
                permit,
                ISignatureTransfer.SignatureTransferDetails(address(this), state.liquidatorCost),
                msg.sender,
                signature
            )
746: 		        emit Liquidate(
747: 		            params.tokenId,
748: 		            msg.sender,
749: 		            owner,
750: 		            state.fullValue,
751: 		            state.liquidatorCost,
752: 		            amount0,
753: 		            amount1,
754: 		            state.reserveCost,
755: 		            state.missing
756: 		        );

// @audit permit2.permitTransferFrom(
                permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature
            )
916: 		        emit Deposit(msg.sender, receiver, assets, shares);

// @audit permit2.permitTransferFrom(
                    permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature
                )
1013: 		        emit Repay(tokenId, msg.sender, owner, assets, shares);

// @audit nonfungiblePositionManager.safeTransferFrom(address(this), owner, tokenId)
1084: 		        emit Remove(tokenId, owner);
```

*GitHub* : [645](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L645), [746-756](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L746-L756), [916](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L916), [1013](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1013), [1084](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1084)

```solidity
File: src/automators/AutoExit.sol

// @audit nonfungiblePositionManager.positions(params.tokenId)
208: 		        emit PositionConfigured(params.tokenId, false, false, false, 0, 0, 0, 0, false, 0);

// @audit nonfungiblePositionManager.positions(params.tokenId)
211: 		        emit Executed(
212: 		            params.tokenId, msg.sender, state.isSwap, state.amount0, state.amount1, state.token0, state.token1
213: 		        );

// @audit nonfungiblePositionManager.ownerOf(tokenId)
232: 		        emit PositionConfigured(
233: 		            tokenId,
234: 		            config.isActive,
235: 		            config.token0Swap,
236: 		            config.token1Swap,
237: 		            config.token0TriggerTick,
238: 		            config.token1TriggerTick,
239: 		            config.token0SlippageX64,
240: 		            config.token1SlippageX64,
241: 		            config.onlyFees,
242: 		            config.maxRewardX64
243: 		        );
```

*GitHub* : [208](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L208), [211-213](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L211-L213), [232-243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L232-L243)

```solidity
File: src/transformers/AutoCompound.sol

// @audit nonfungiblePositionManager.collect(
            INonfungiblePositionManager.CollectParams(
                params.tokenId, address(this), type(uint128).max, type(uint128).max
            )
        )
183: 		        emit AutoCompounded(
184: 		            msg.sender,
185: 		            params.tokenId,
186: 		            state.compounded0,
187: 		            state.compounded1,
188: 		            state.amount0Fees,
189: 		            state.amount1Fees,
190: 		            state.token0,
191: 		            state.token1
192: 		        );
```

*GitHub* : [183-192](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L183-L192)

```solidity
File: src/transformers/AutoRange.sol

// @audit nonfungiblePositionManager.positions(params.tokenId)
252: 		            emit PositionConfigured(
253: 		                state.newTokenId,
254: 		                config.lowerTickLimit,
255: 		                config.upperTickLimit,
256: 		                config.lowerTickDelta,
257: 		                config.upperTickDelta,
258: 		                config.token0SlippageX64,
259: 		                config.token1SlippageX64,
260: 		                config.onlyFees,
261: 		                config.maxRewardX64
262: 		            );

// @audit nonfungiblePositionManager.positions(params.tokenId)
266: 		            emit PositionConfigured(params.tokenId, 0, 0, 0, 0, 0, 0, false, 0);

// @audit nonfungiblePositionManager.positions(params.tokenId)
268: 		            emit RangeChanged(params.tokenId, state.newTokenId);
```

*GitHub* : [252-262](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L252-L262), [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L266), [268](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L268)

```solidity
File: src/transformers/V3Utils.sol

// @audit nonfungiblePositionManager.positions(tokenId)
218: 		            emit CompoundFees(tokenId, liquidity, amount0, amount1);

// @audit nonfungiblePositionManager.positions(tokenId)
303: 		            emit ChangeRange(tokenId, newTokenId);

// @audit nonfungiblePositionManager.positions(tokenId)
348: 		            emit WithdrawAndCollectAndSwap(tokenId, instructions.targetToken, targetAmount);

// @audit nonfungiblePositionManager.mint(mintParams)
729: 		        emit SwapAndMint(tokenId, liquidity, added0, added1);

// @audit nonfungiblePositionManager.increaseLiquidity(increaseLiquidityParams)
773: 		        emit SwapAndIncreaseLiquidity(params.tokenId, liquidity, added0, added1);
```

*GitHub* : [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L218), [303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L303), [348](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L348), [729](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L729), [773](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L773)

```solidity
File: src/utils/Swapper.sol

// @audit params.tokenIn.balanceOf(address(this))
116: 		            emit Swap(address(params.tokenIn), address(params.tokenOut), amountInDelta, amountOutDelta);
```

*GitHub* : [116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L116)

### [N-56]<a name="n-56"></a> Use of polymorphism is discouraged for security audits

A duplicated function name in the same contract might have problems with automated auditing tools, so it should be avoided. Consider always using a different name for functions to improve the readability of the code.

*There are 3 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit found also on line 360
384: 		    function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

// @audit found also on line 366
390: 		    function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

// @audit found also on line 652
661: 		    function repay(uint256 tokenId, uint256 amount, bool isShare, bytes calldata permitData) external override {
```

*GitHub* : [390](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L390), [384](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L384), [661](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L661)

### [N-57]<a name="n-57"></a> Constants in comparisons should appear on the left side

This is useful to avoid doing some [typo bugs](https://www.moserware.com/2008/01/constants-on-left-are-better-but-this.html).

*There are 28 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

47: 		        if (debt == 0) {
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L47)

```solidity
File: src/V3Oracle.sol

300: 		            chainlinkReferencePriceX96 = cachedChainlinkReferencePriceX96 == 0

362: 		        if (twapSeconds == 0) {
```

*GitHub* : [300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L300), [362](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L362)

```solidity
File: src/V3Vault.sol

441: 		        if (transformedTokenId == 0) {

502: 		        if (tokenId == 0 || !transformerAllowList[transformer]) {
```

*GitHub* : [441](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L441), [502](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L502)

```solidity
File: src/automators/AutoExit.sol

124: 		        if (state.liquidity == 0) {

149: 		            if (params.swapData.length == 0) {
```

*GitHub* : [124](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L124), [149](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L149)

```solidity
File: src/transformers/AutoCompound.sol

279: 		        if (allowance0 == 0) {

283: 		        if (allowance1 == 0) {
```

*GitHub* : [279](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L279), [283](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L283)

```solidity
File: src/transformers/AutoRange.sol

301: 		        if (fee == 10000) {

303: 		        } else if (fee == 3000) {

305: 		        } else if (fee == 500) {
```

*GitHub* : [303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L303), [301](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L301), [305](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L305)

```solidity
File: src/transformers/V3Utils.sol

120: 		        if (instructions.liquidity != 0) {

342: 		            if (targetAmount != 0 && instructions.targetToken != address(0)) {

420: 		        if (amountOut != 0) {

426: 		        if (leftOver != 0) {

500: 		        (tokenId, liquidity, amount0, amount1) = _swapAndMint(params, msg.value != 0);

563: 		        (liquidity, amount0, amount1) = _swapAndIncrease(params, IERC20(token0), IERC20(token1), msg.value != 0);

666: 		        if (msg.value != 0) {

822: 		            if (leftOver != 0) {

830: 		        if (total0 != 0) {

834: 		        if (total1 != 0) {

855: 		        if (left0 != 0) {

858: 		        if (left1 != 0) {

884: 		        if (liquidity != 0) {
```

*GitHub* : [858](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L858), [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L120), [342](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L342), [420](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L420), [426](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L426), [500](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L500), [563](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L563), [666](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L666), [822](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L822), [830](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L830), [834](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L834), [855](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L855), [884](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L884)

```solidity
File: src/utils/FlashloanLiquidator.sol

43: 		        if (liquidationCost == 0) {
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L43)

```solidity
File: src/utils/Swapper.sol

77: 		        if (params.amountIn != 0 && params.swapData.length != 0 && address(params.tokenOut) != address(0)) {

77: 		        if (params.amountIn != 0 && params.swapData.length != 0 && address(params.tokenOut) != address(0)) {
```

*GitHub* : [77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L77), [77](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L77)

### [N-58]<a name="n-58"></a> Consider using `delete` instead of assigning zero/false to clear values

The `delete` keyword more closely matches the semantics of what is being done, and draws more attention to the changing of state, which may lead to a more thorough audit of its associated logic.

*There are 5 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

366: 		            secondsAgos[0] = 0; // from (before)
```

*GitHub* : [366](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L366)

```solidity
File: src/V3Vault.sol

542: 		        transformedTokenId = 0;

1053: 		                liquidity = 0;
```

*GitHub* : [542](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L542), [1053](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1053)

```solidity
File: src/automators/Automator.sol

182: 		        secondsAgos[0] = 0; // from (before)
```

*GitHub* : [182](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L182)

```solidity
File: src/transformers/AutoCompound.sol

136: 		                        amountIn = 0;
```

*GitHub* : [136](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L136)

### [N-59]<a name="n-59"></a> Use a ternary statement instead of `if`/`else` when appropriate

The `if`/`else` statement can be written in a shorthand way using the ternary operator, as it increases readability and reduces the number of lines of code.

*There are 3 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

315: 		        if (value >= globalLendLimit) {
316: 		            return 0;
317: 		        } else {
318: 		            return _convertToShares(globalLendLimit - value, lendExchangeRateX96, Math.Rounding.Down);
319: 		        }
```

*GitHub* : [315-319](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L315-L319)

```solidity
File: src/automators/Automator.sol

157: 		        if (swap0For1) {
158: 		            amountOutMin = FullMath.mulDiv(amountIn * (Q64 - maxPriceDifferenceX64), priceX96, Q96 * Q64);
159: 		        } else {
160: 		            amountOutMin = FullMath.mulDiv(amountIn * (Q64 - maxPriceDifferenceX64), Q96, priceX96 * Q64);
161: 		        }

172: 		        if (twapOk) {
173: 		            return twapTick - currentTick >= -int16(maxDifference) && twapTick - currentTick <= int16(maxDifference);
174: 		        } else {
175: 		            return false;
176: 		        }
```

*GitHub* : [172-176](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L172-L176), [157-161](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L157-L161)

### [N-60]<a name="n-60"></a> Consider using named mappings

Named mappings improve the readability of the code, even if they are optional, as it's possible to infer the usage of both key and value, instead of looking just at the type.

*There are 16 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

56: 		    mapping(address => TokenConfig) public feedConfigs;
```

*GitHub* : [56](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L56)

```solidity
File: src/V3Vault.sol

115: 		    mapping(address => TokenConfig) public tokenConfigs;

154: 		    mapping(uint256 => Loan) public loans; // tokenID -> loan mapping

157: 		    mapping(address => uint256[]) private ownedTokens; // Mapping from owner address to list of owned token IDs

158: 		    mapping(uint256 => uint256) private ownedTokensIndex; // Mapping from token ID to index of the owner tokens list (for removal without loop)

159: 		    mapping(uint256 => address) private tokenOwner; // Mapping from token ID to owner

163: 		    mapping(address => bool) public transformerAllowList; // contracts allowed to transform positions (selected audited contracts e.g. V3Utils)

164: 		    mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)

164: 		    mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)

164: 		    mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)
```

*GitHub* : [164](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L164), [115](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L115), [154](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L154), [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L157), [158](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L158), [159](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L159), [163](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L163), [164](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L164), [164](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L164)

```solidity
File: src/automators/AutoExit.sol

60: 		    mapping(uint256 => PositionConfig) public positionConfigs;
```

*GitHub* : [60](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L60)

```solidity
File: src/automators/Automator.sol

34: 		    mapping(address => bool) public operators;

35: 		    mapping(address => bool) public vaults;
```

*GitHub* : [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L34), [35](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L35)

```solidity
File: src/transformers/AutoCompound.sol

45: 		    mapping(uint256 => mapping(address => uint256)) public positionBalances;

45: 		    mapping(uint256 => mapping(address => uint256)) public positionBalances;
```

*GitHub* : [45](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L45), [45](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L45)

```solidity
File: src/transformers/AutoRange.sol

50: 		    mapping(uint256 => PositionConfig) public positionConfigs;
```

*GitHub* : [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L50)

### [N-61]<a name="n-61"></a> Consider using named returns

Using named returns makes the code more self-documenting, makes it easier to fill out NatSpec, and in some cases can save gas. The cases below are where there currently is at most one return statement, which is ideal for named returns.

*There are 31 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

46: 		    function getUtilizationRateX96(uint256 cash, uint256 debt) public pure returns (uint256) {
```

*GitHub* : [46](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L46)

```solidity
File: src/V3Oracle.sol

329: 		    function _getChainlinkPriceX96(address token) internal view returns (uint256) {

359: 		    function _getReferencePoolPriceX96(IUniswapV3Pool pool, uint32 twapSeconds) internal view returns (uint256) {

499: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [359](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L359), [329](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L329), [499](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L499)

```solidity
File: src/V3Vault.sol

264: 		    function loanCount(address owner) external view override returns (uint256) {

271: 		    function loanAtIndex(address owner, uint256 index) external view override returns (uint256) {

277: 		    function decimals() public view override(IERC20Metadata, ERC20) returns (uint8) {

284: 		    function totalAssets() public view override returns (uint256) {

301: 		    function maxDeposit(address) external view override returns (uint256) {

312: 		    function maxMint(address) external view override returns (uint256) {

323: 		    function maxWithdraw(address owner) external view override returns (uint256) {

329: 		    function maxRedeem(address owner) external view override returns (uint256) {

334: 		    function previewDeposit(uint256 assets) public view override returns (uint256) {

340: 		    function previewMint(uint256 shares) public view override returns (uint256) {

346: 		    function previewWithdraw(uint256 assets) public view override returns (uint256) {

352: 		    function previewRedeem(uint256 shares) public view override returns (uint256) {

360: 		    function deposit(uint256 assets, address receiver) external override returns (uint256) {

366: 		    function mint(uint256 shares, address receiver) external override returns (uint256) {

372: 		    function withdraw(uint256 assets, address receiver, address owner) external override returns (uint256) {

378: 		    function redeem(uint256 shares, address receiver, address owner) external override returns (uint256) {

384: 		    function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

390: 		    function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

429: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)
430: 		        external
431: 		        override
432: 		        returns (bytes4)

1143: 		    function _calculateTokenCollateralFactorX32(uint256 tokenId) internal view returns (uint32) {

1281: 		    function _convertToShares(uint256 amount, uint256 exchangeRateX96, Math.Rounding rounding)
1282: 		        internal
1283: 		        pure
1284: 		        returns (uint256)

1289: 		    function _convertToAssets(uint256 shares, uint256 exchangeRateX96, Math.Rounding rounding)
1290: 		        internal
1291: 		        pure
1292: 		        returns (uint256)
```

*GitHub* : [271](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L271), [264](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L264), [277](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L277), [284](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L284), [301](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L301), [312](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L312), [323](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L323), [329](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L329), [334](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L334), [340](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L340), [346](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L346), [352](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L352), [360](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L360), [366](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L366), [372](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L372), [378](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L378), [384](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L384), [390](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L390), [429-432](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L429-L432), [1143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1143), [1281-1284](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1281-L1284), [1289-1292](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1289-L1292)

```solidity
File: src/automators/Automator.sol

166: 		    function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)
167: 		        internal
168: 		        view
169: 		        returns (bool)

180: 		    function _getTWAPTick(IUniswapV3Pool pool, uint32 twapPeriod) internal view returns (int24, bool) {
```

*GitHub* : [166-169](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L166-L169), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L180)

```solidity
File: src/transformers/AutoRange.sol

300: 		    function _getTickSpacing(uint24 fee) internal view returns (int24) {
```

*GitHub* : [300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L300)

```solidity
File: src/transformers/V3Utils.sol

356: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)
357: 		        external
358: 		        override
359: 		        returns (bytes4)
```

*GitHub* : [356-359](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L356-L359)

```solidity
File: src/utils/Swapper.sol

171: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L171)

### [N-62]<a name="n-62"></a> Layout order does not comply with best practices

This is a [best practice](https://docs.soliditylang.org/en/latest/style-guide.html#order-of-layout) that should be followed.

Inside each contract, library or interface, use the following order:

1. Type declarations
2. State variables
3. Events
4. Errors
5. Modifiers
6. Functions

*There are 8 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit event SetValues found on line 18
23: 		    uint256 public multiplierPerSecondX96;
```

*GitHub* : [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L23)

```solidity
File: src/V3Oracle.sol

// @audit event SetEmergencyAdmin found on line 33
56: 		    mapping(address => TokenConfig) public feedConfigs;
```

*GitHub* : [56](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L56)

```solidity
File: src/V3Vault.sol

// @audit event SetEmergencyAdmin found on line 106
115: 		    mapping(address => TokenConfig) public tokenConfigs;
```

*GitHub* : [115](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L115)

```solidity
File: src/automators/AutoExit.sol

// @audit function constructor found on line 33
60: 		    mapping(uint256 => PositionConfig) public positionConfigs;
```

*GitHub* : [60](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L60)

```solidity
File: src/automators/Automator.sol

// @audit event TWAPConfigChanged found on line 31
34: 		    mapping(address => bool) public operators;
```

*GitHub* : [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L34)

```solidity
File: src/transformers/AutoCompound.sol

// @audit function constructor found on line 37
45: 		    mapping(uint256 => mapping(address => uint256)) public positionBalances;
```

*GitHub* : [45](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L45)

```solidity
File: src/transformers/AutoRange.sol

// @audit function constructor found on line 25
50: 		    mapping(uint256 => PositionConfig) public positionConfigs;
```

*GitHub* : [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L50)

```solidity
File: src/utils/Swapper.sol

// @audit event Swap found on line 18
21: 		    IWETH9 public immutable weth;
```

*GitHub* : [21](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L21)

### [N-63]<a name="n-63"></a> `mapping` definitions do not comply with best practices

This is a [best practice](https://docs.soliditylang.org/en/latest/style-guide.html#mappings) that should be followed. In variable declarations, do not separate the keyword mapping from its type by a space. Do not separate any nested mapping keyword from its type by whitespace.

*There are 1 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

154: 		    mapping(uint256 => Loan) public loans; // tokenID -> loan mapping
```

*GitHub* : [154](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L154)

### [N-64]<a name="n-64"></a> Function visibility order does not comply with best practices

This is a [best practice](https://docs.soliditylang.org/en/latest/style-guide.html#order-of-functions) that should be followed.

Functions should be grouped according to their visibility and ordered:

1. constructor
2. receive function (if exists)
3. fallback function (if exists)
4. external
5. public
6. internal
7. private

Within a grouping, place the view and pure functions last.

*There are 43 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit _requireMaxDifference on line 139, which is internal
162: 		    function getPositionBreakdown(uint256 tokenId)

// @audit _requireMaxDifference on line 139, which is internal
185: 		    function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

// @audit _requireMaxDifference on line 139, which is internal
201: 		    function setTokenConfig(

// @audit _requireMaxDifference on line 139, which is internal
249: 		    function setOracleMode(address token, Mode mode) external {

// @audit _requireMaxDifference on line 139, which is internal
265: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [162](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L162), [185](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L185), [201](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L201), [249](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L249), [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L265)

```solidity
File: src/V3Vault.sol

// @audit totalAssets on line 284, which is public
289: 		    function convertToShares(uint256 assets) external view override returns (uint256 shares) {

// @audit totalAssets on line 284, which is public
295: 		    function convertToAssets(uint256 shares) external view override returns (uint256 assets) {

// @audit totalAssets on line 284, which is public
301: 		    function maxDeposit(address) external view override returns (uint256) {

// @audit totalAssets on line 284, which is public
312: 		    function maxMint(address) external view override returns (uint256) {

// @audit totalAssets on line 284, which is public
323: 		    function maxWithdraw(address owner) external view override returns (uint256) {

// @audit totalAssets on line 284, which is public
329: 		    function maxRedeem(address owner) external view override returns (uint256) {

// @audit previewRedeem on line 352, which is public
360: 		    function deposit(uint256 assets, address receiver) external override returns (uint256) {

// @audit previewRedeem on line 352, which is public
366: 		    function mint(uint256 shares, address receiver) external override returns (uint256) {

// @audit previewRedeem on line 352, which is public
372: 		    function withdraw(uint256 assets, address receiver, address owner) external override returns (uint256) {

// @audit previewRedeem on line 352, which is public
378: 		    function redeem(uint256 shares, address receiver, address owner) external override returns (uint256) {

// @audit previewRedeem on line 352, which is public
384: 		    function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

// @audit previewRedeem on line 352, which is public
390: 		    function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

// @audit previewRedeem on line 352, which is public
400: 		    function create(uint256 tokenId, address recipient) external override {

// @audit previewRedeem on line 352, which is public
410: 		    function createWithPermit(

// @audit previewRedeem on line 352, which is public
429: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)

// @audit previewRedeem on line 352, which is public
483: 		    function approveTransform(uint256 tokenId, address target, bool isActive) external override {

// @audit previewRedeem on line 352, which is public
497: 		    function transform(uint256 tokenId, address transformer, bytes calldata data)

// @audit previewRedeem on line 352, which is public
550: 		    function borrow(uint256 tokenId, uint256 assets) external override {

// @audit previewRedeem on line 352, which is public
609: 		    function decreaseLiquidityAndCollect(DecreaseLiquidityAndCollectParams calldata params)

// @audit previewRedeem on line 352, which is public
652: 		    function repay(uint256 tokenId, uint256 amount, bool isShare) external override {

// @audit previewRedeem on line 352, which is public
661: 		    function repay(uint256 tokenId, uint256 amount, bool isShare, bytes calldata permitData) external override {

// @audit previewRedeem on line 352, which is public
685: 		    function liquidate(LiquidateParams calldata params) external override returns (uint256 amount0, uint256 amount1) {

// @audit previewRedeem on line 352, which is public
765: 		    function withdrawReserves(uint256 amount, address receiver) external onlyOwner {

// @audit previewRedeem on line 352, which is public
788: 		    function setTransformer(address transformer, bool active) external onlyOwner {

// @audit previewRedeem on line 352, which is public
807: 		    function setLimits(

// @audit previewRedeem on line 352, which is public
837: 		    function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

// @audit previewRedeem on line 352, which is public
844: 		    function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

// @audit previewRedeem on line 352, which is public
856: 		    function setTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32)

// @audit previewRedeem on line 352, which is public
870: 		    function setEmergencyAdmin(address admin) external onlyOwner {
```

*GitHub* : [289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L289), [295](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L295), [301](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L301), [312](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L312), [323](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L323), [329](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L329), [360](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L360), [366](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L366), [372](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L372), [378](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L378), [384](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L384), [390](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L390), [400](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L400), [410](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L410), [429](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L429), [483](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L483), [497](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L497), [550](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L550), [609](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L609), [652](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L652), [661](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L661), [685](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L685), [765](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L765), [788](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L788), [807](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L807), [837](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L837), [844](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L844), [856](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L856), [870](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L870)

```solidity
File: src/automators/Automator.sol

// @audit setTWAPConfig on line 87, which is public
104: 		    function withdrawBalances(address[] calldata tokens, address to) external virtual {

// @audit setTWAPConfig on line 87, which is public
123: 		    function withdrawETH(address to) external {

// @audit _validateOwner on line 230, which is internal
251: 		    receive() external payable {
```

*GitHub* : [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L104), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L123), [251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L251)

```solidity
File: src/transformers/V3Utils.sol

// @audit execute on line 115, which is public
356: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)

// @audit execute on line 115, which is public
397: 		    function swap(SwapParams calldata params) external payable returns (uint256 amountOut) {

// @audit execute on line 115, which is public
467: 		    function swapAndMint(SwapAndMintParams calldata params)

// @audit execute on line 115, which is public
532: 		    function swapAndIncreaseLiquidity(SwapAndIncreaseLiquidityParams calldata params)

// @audit _collectFees on line 892, which is internal
914: 		    receive() external payable {
```

*GitHub* : [356](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L356), [397](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L397), [467](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L467), [532](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L532), [914](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L914)

```solidity
File: src/utils/Swapper.sol

// @audit _poolSwap on line 132, which is internal
156: 		    function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external override {
```

*GitHub* : [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L156)

### [N-65]<a name="n-65"></a> Long functions should be refactored into multiple functions

Consider splitting long functions into multiple, smaller functions to improve the code readability.

*There are 12 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

272: 		    function _getReferenceTokenPriceX96(address token, uint256 cachedChainlinkReferencePriceX96)
```

*GitHub* : [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L272)

```solidity
File: src/V3Vault.sol

550: 		    function borrow(uint256 tokenId, uint256 assets) external override {

685: 		    function liquidate(LiquidateParams calldata params) external override returns (uint256 amount0, uint256 amount1) {

954: 		    function _repay(uint256 tokenId, uint256 amount, bool isShare, bytes memory permitData) internal {
```

*GitHub* : [550](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L550), [685](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L685), [954](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L954)

```solidity
File: src/automators/AutoExit.sol

100: 		    function execute(ExecuteParams calldata params) external {
```

*GitHub* : [100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L100)

```solidity
File: src/transformers/AutoCompound.sol

101: 		    function execute(ExecuteParams calldata params) external nonReentrant {
```

*GitHub* : [101](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L101)

```solidity
File: src/transformers/AutoRange.sol

111: 		    function execute(ExecuteParams calldata params) external {
```

*GitHub* : [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L111)

```solidity
File: src/transformers/LeverageTransformer.sol

40: 		    function leverageUp(LeverageUpParams calldata params) external {

123: 		    function leverageDown(LeverageDownParams calldata params) external {
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L40), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L123)

```solidity
File: src/transformers/V3Utils.sol

115: 		    function execute(uint256 tokenId, Instructions memory instructions) public returns (uint256 newTokenId) {

598: 		    function _prepareAddPermit2(

779: 		    function _swapAndPrepareAmounts(SwapAndMintParams memory params, bool unwrap)
```

*GitHub* : [115](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L115), [598](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L598), [779](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L779)

### [N-66]<a name="n-66"></a> Consider providing a ranged getter for array state variables

While the compiler automatically provides a getter for accessing single elements within a public state variable array, it doesn't provide a way to fetch the whole array, or subsets thereof.

Consider adding a function to allow the fetching of slices of the array, especially if the contract doesn't already have multicall functionality.

*There are 1 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

157: 		    mapping(address => uint256[]) private ownedTokens; // Mapping from owner address to list of owned token IDs
```

*GitHub* : [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L157)

### [N-67]<a name="n-67"></a> Lines are too long

Maximum suggested line length is 120 characters according to the [documentation](https://docs.soliditylang.org/en/latest/style-guide.html#maximum-line-length).

*There are 36 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

65: 		    uint16 public maxPoolPriceDifference = MIN_PRICE_DIFFERENCE; // max price difference between oracle derived price and pool price x10000

152: 		    /// @notice Gets breakdown of a uniswap v3 position (tokens and fee tier, liquidity, current liquidity amounts, uncollected fees)

368: 		            (int56[] memory tickCumulatives,) = pool.observe(secondsAgos); // pool observe may fail when there is not enough history available (only use pool with enough history!)
```

*GitHub* : [65](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L65), [152](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L152), [368](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L368)

```solidity
File: src/V3Vault.sol

28: 		/// @notice The vault manages ONE ERC20 (eg. USDC) asset for lending / borrowing, but collateral positions can be composed of any 2 tokens configured each with a collateralFactor > 0

70: 		    event Add(uint256 indexed tokenId, address owner, uint256 oldTokenId); // when a token is added replacing another token - oldTokenId > 0

158: 		    mapping(uint256 => uint256) private ownedTokensIndex; // Mapping from token ID to index of the owner tokens list (for removal without loop)

163: 		    mapping(address => bool) public transformerAllowList; // contracts allowed to transform positions (selected audited contracts e.g. V3Utils)

164: 		    mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)

230: 		    /// @return liquidationValue If position is liquidatable - the value of the (partial) position which the liquidator recieves - otherwise 0

427: 		    /// @notice Whenever a token is recieved it either creates a new loan, or modifies an existing one when in transform mode.

496: 		    /// @return newTokenId Final token ID (may be different than input token ID when the position was replaced by transformation)

605: 		    /// This function is not allowed during transformation (if a transformer wants to decreaseLiquidity he can call the methods directly on the NonfungiblePositionManager)

606: 		    /// @param params Struct containing various parameters for the operation. Includes tokenId, liquidity amount, minimum asset amounts, and deadline.

842: 		    /// @notice sets reserve protection factor - percentage of globalLendAmount which can't be withdrawn by owner (onlyOwner)

855: 		    /// @param collateralValueLimitFactorX32 how much of it maybe used as collateral measured as percentage of total lent assets mutiplied by Q32

1089: 		    //  if position is not valuable enough - missing part is covered by reserves - if not enough reserves - collectively by other borrowers

1096: 		        // if position has less than enough value - liquidation cost maybe less - rest is payed by protocol or lenders collectively

1204: 		    // updates collateral token configs - and check if limit is not surpassed (check is only done on increasing debt shares)
```

*GitHub* : [28](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L28), [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L70), [158](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L158), [163](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L163), [164](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L164), [230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L230), [427](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L427), [496](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L496), [605](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L605), [606](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L606), [842](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L842), [855](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L855), [1089](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1089), [1096](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1096), [1204](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1204)

```solidity
File: src/automators/AutoExit.sol

7: 		/// @notice Lets a v3 position to be automatically removed (limit order) or swapped to the opposite token (stop loss order) when it reaches a certain tick.

9: 		/// Positions need to be approved (approve or setApprovalForAll) for the contract and configured with configToken method

184: 		            // when swap and !onlyFees - protocol reward is removed only from target token (to incentivize optimal swap done by operator)
```

*GitHub* : [7](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L7), [9](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L9), [184](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L184)

```solidity
File: src/transformers/AutoRange.sol

39: 		        int32 lowerTickLimit; // if negative also in-range positions may be adjusted / if 0 out of range positions may be adjusted

40: 		        int32 upperTickLimit; // if negative also in-range positions may be adjusted / if 0 out of range positions may be adjusted

41: 		        int32 lowerTickDelta; // this amount is added to current tick (floored to tickspacing) to define lowerTick of new position

42: 		        int32 upperTickDelta; // this amount is added to current tick (floored to tickspacing) to define upperTick of new position
```

*GitHub* : [39](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L39), [40](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L40), [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L41), [42](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L42)

```solidity
File: src/transformers/V3Utils.sol

47: 		    /// @notice Complete description of what should be executed on provided NFT - different fields are used depending on specified WhatToDo

73: 		        // remove liquidity amount for COMPOUND_FEES (in this case should be probably 0) / CHANGE_RANGE / WITHDRAW_AND_COLLECT_AND_SWAP

109: 		        // NOTE: previous operator can not be reset as operator set by permit can not change operator - so this operator will stay until reset

354: 		    /// @notice ERC721 callback function. Called on safeTransferFrom and does manipulation as configured in encoded Instructions parameter.

355: 		    /// At the end the NFT (and any newly minted NFT) is returned to sender. The leftover tokens are sent to instructions.recipient.

395: 		    /// If tokenIn is wrapped native token - both the token or the wrapped token can be sent (the sum of both must be equal to amountIn)

445: 		        // if swapSourceToken is another token than token0 or token1 -> amountIn0 + amountIn1 of swapSourceToken are expected to be available

464: 		    /// @notice Does 1 or 2 swaps from swapSourceToken to token0 and token1 and adds as much as possible liquidity to a newly minted position.

512: 		        // if swapSourceToken is another token than token0 or token1 -> amountIn0 + amountIn1 of swapSourceToken are expected to be available

529: 		    /// @notice Does 1 or 2 swaps from swapSourceToken to token0 and token1 and adds as much as possible liquidity to any existing position (no need to be position owner).
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L47), [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L73), [109](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L109), [354](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L354), [355](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L355), [395](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L395), [445](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L445), [464](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L464), [512](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L512), [529](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L529)

```solidity
File: src/utils/FlashloanLiquidator.sol

68: 		        // no origin check is needed - because the contract doesn't hold any funds - there is no benefit in calling uniswapV3FlashCallback() from another context
```

*GitHub* : [68](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L68)

### [N-68]<a name="n-68"></a> Avoid the use of sensitive terms

Use [alternative variants](https://www.zdnet.com/article/mysql-drops-master-slave-and-blacklist-whitelist-terminology/), e.g. allowlist/denylist instead of whitelist/blacklist.

*There are 1 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

494: 		    /// @param transformer The address of a whitelisted transformer contract
```

*GitHub* : [494](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L494)

### [N-69]<a name="n-69"></a> Consider adding a block/deny-list

This can help to prevent hackers from using stolen tokens, but as a side effect it will increase the project centralization.

*There are 3 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

11: 		contract InterestRateModel is Ownable, IInterestRateModel, IErrors {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L11)

```solidity
File: src/V3Oracle.sol

24: 		contract V3Oracle is IV3Oracle, Ownable, IErrors {
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L24)

```solidity
File: src/V3Vault.sol

30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

### [N-70]<a name="n-70"></a> Use of `override` is unnecessary

Starting with Solidity version [0.8.8](https://docs.soliditylang.org/en/latest/contracts.html#function-overriding), using the override keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.

*There are 39 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

58: 		    function getRatesPerSecondX96(uint256 cash, uint256 debt)
```

*GitHub* : [58](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L58)

```solidity
File: src/V3Oracle.sol

95: 		    function getValue(uint256 tokenId, address token)

162: 		    function getPositionBreakdown(uint256 tokenId)
```

*GitHub* : [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L95), [162](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L162)

```solidity
File: src/V3Vault.sol

195: 		    function vaultInfo()

219: 		    function lendInfo(address account) external view override returns (uint256 amount) {

231: 		    function loanInfo(uint256 tokenId)

258: 		    function ownerOf(uint256 tokenId) external view override returns (address owner) {

264: 		    function loanCount(address owner) external view override returns (uint256) {

271: 		    function loanAtIndex(address owner, uint256 index) external view override returns (uint256) {

284: 		    function totalAssets() public view override returns (uint256) {

289: 		    function convertToShares(uint256 assets) external view override returns (uint256 shares) {

295: 		    function convertToAssets(uint256 shares) external view override returns (uint256 assets) {

301: 		    function maxDeposit(address) external view override returns (uint256) {

312: 		    function maxMint(address) external view override returns (uint256) {

323: 		    function maxWithdraw(address owner) external view override returns (uint256) {

329: 		    function maxRedeem(address owner) external view override returns (uint256) {

334: 		    function previewDeposit(uint256 assets) public view override returns (uint256) {

340: 		    function previewMint(uint256 shares) public view override returns (uint256) {

346: 		    function previewWithdraw(uint256 assets) public view override returns (uint256) {

352: 		    function previewRedeem(uint256 shares) public view override returns (uint256) {

360: 		    function deposit(uint256 assets, address receiver) external override returns (uint256) {

366: 		    function mint(uint256 shares, address receiver) external override returns (uint256) {

372: 		    function withdraw(uint256 assets, address receiver, address owner) external override returns (uint256) {

378: 		    function redeem(uint256 shares, address receiver, address owner) external override returns (uint256) {

384: 		    function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

390: 		    function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

400: 		    function create(uint256 tokenId, address recipient) external override {

410: 		    function createWithPermit(

429: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)

483: 		    function approveTransform(uint256 tokenId, address target, bool isActive) external override {

497: 		    function transform(uint256 tokenId, address transformer, bytes calldata data)

550: 		    function borrow(uint256 tokenId, uint256 assets) external override {

609: 		    function decreaseLiquidityAndCollect(DecreaseLiquidityAndCollectParams calldata params)

652: 		    function repay(uint256 tokenId, uint256 amount, bool isShare) external override {

661: 		    function repay(uint256 tokenId, uint256 amount, bool isShare, bytes calldata permitData) external override {

685: 		    function liquidate(LiquidateParams calldata params) external override returns (uint256 amount0, uint256 amount1) {
```

*GitHub* : [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L195), [219](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L219), [231](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L231), [258](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L258), [264](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L264), [271](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L271), [284](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L284), [289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L289), [295](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L295), [301](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L301), [312](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L312), [323](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L323), [329](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L329), [334](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L334), [340](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L340), [346](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L346), [352](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L352), [360](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L360), [366](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L366), [372](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L372), [378](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L378), [384](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L384), [390](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L390), [400](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L400), [410](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L410), [429](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L429), [483](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L483), [497](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L497), [550](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L550), [609](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L609), [652](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L652), [661](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L661), [685](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L685)

```solidity
File: src/transformers/AutoCompound.sol

227: 		    function withdrawBalances(address[] calldata tokens, address to) external override nonReentrant {
```

*GitHub* : [227](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L227)

```solidity
File: src/transformers/V3Utils.sol

356: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)
```

*GitHub* : [356](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L356)

```solidity
File: src/utils/Swapper.sol

156: 		    function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external override {
```

*GitHub* : [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L156)

### [N-71]<a name="n-71"></a> Missing variable names

Consider adding a comment with the variable name even if it's not used, to improve the code readability.

*There are 4 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

301: 		    function maxDeposit(address) external view override returns (uint256) {

312: 		    function maxMint(address) external view override returns (uint256) {

429: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)
```

*GitHub* : [301](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L301), [312](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L312), [429](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L429)

```solidity
File: src/transformers/V3Utils.sol

356: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)
```

*GitHub* : [356](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L356)

### [N-72]<a name="n-72"></a> Typos in comments

Avoid typos, and proper nouns should be capitalized.

*There are 45 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit verfies
87: 		    /// @dev uses configured oracles and verfies price on second oracle - if fails - reverts

// @audit arbitrageurs
127: 		        // when a pool is in this state, liquidations will be disabled - but arbitrageurs (or liquidator himself)

// @audit twap
361: 		        // if twap seconds set to 0 just use pool price
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L87), [127](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L127), [361](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L361)

```solidity
File: src/V3Vault.sol

// @audit dencun
161: 		    uint256 private transformedTokenId = 0; // transient storage (when available in dencun)

// @audit recieves
230: 		    /// @return liquidationValue If position is liquidatable - the value of the (partial) position which the liquidator recieves - otherwise 0

// @audit tokenid
268: 		    /// @notice Retrieves tokenid of loan at given index for owner (for enumerating owners loans)

// @audit recieve
399: 		    /// @param recipient Address to recieve the position in the vault

// @audit recieve
407: 		    /// @param recipient Address to recieve the position in the vault

// @audit recieved
427: 		    /// @notice Whenever a token is recieved it either creates a new loan, or modifies an existing one when in transform mode.

// @audit nftmanager
614: 		        // this method is not allowed during transform - can be called directly on nftmanager if needed from transform contract

// @audit transfering
711: 		        // calculate reserve (before transfering liquidation money - otherwise calculation is off)

// @audit mutiplied
854: 		    /// @param collateralFactorX32 collateral factor for this token mutiplied by Q32

// @audit mutiplied
855: 		    /// @param collateralValueLimitFactorX32 how much of it maybe used as collateral measured as percentage of total lent assets mutiplied by Q32

// @audit liquididated
1088: 		    //  if position is too valuable - not all of the position is liquididated - only needed amount

// @audit liquidaton
1122: 		    // calculates if there are enough reserves to cover liquidaton - if not its shared between lenders
```

*GitHub* : [161](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L161), [230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L230), [268](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L268), [399](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L399), [407](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L407), [427](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L427), [614](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L614), [711](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L711), [854](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L854), [855](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L855), [1088](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1088), [1122](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1122)

```solidity
File: src/automators/AutoExit.sol

// @audit stoploss
43: 		    // define how stoploss / limit should be handled

// @audit tokenid
64: 		        uint256 tokenId; // tokenid to process

// @audit incentivize
184: 		            // when swap and !onlyFees - protocol reward is removed only from target token (to incentivize optimal swap done by operator)
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L43), [64](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L64), [184](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L184)

```solidity
File: src/automators/Automator.sol

// @audit twap
179: 		    // gets twap tick from pool history if enough history available

// @audit temporarely
201: 		            // store in temporarely "misnamed" variables - see comment below
```

*GitHub* : [179](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L179), [201](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L201)

```solidity
File: src/transformers/AutoCompound.sol

// @audit autocompound
17: 		    // autocompound event

// @audit tokenid, autocompound
52: 		        // tokenid to autocompound

// @audit autocompound
60: 		    // state used during autocompound execution

// @audit autocompounding
122: 		        // only if there are balances to work with - start autocompounding process

// @audit incentivize
169: 		                // fees are always calculated based on added amount (to incentivize optimal swap)

// @audit overriden, automator
223: 		     * @dev The method is overriden, because it differs from standard automator fee handling
```

*GitHub* : [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L17), [52](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L52), [60](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L60), [122](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L122), [169](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L169), [223](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L223)

```solidity
File: src/transformers/AutoRange.sol

// @audit tickspacing
41: 		        int32 lowerTickDelta; // this amount is added to current tick (floored to tickspacing) to define lowerTick of new position

// @audit tickspacing
42: 		        int32 upperTickDelta; // this amount is added to current tick (floored to tickspacing) to define upperTick of new position

// @audit npm
212: 		            // approve npm

// @audit safemint
216: 		            // mint is done to address(this) first - its not a safemint

// @audit incentivize
234: 		            // protocol reward is calculated based on added amount (to incentivize optimal swap done by operator)
```

*GitHub* : [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L41), [42](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L42), [212](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L212), [216](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L216), [234](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L234)

```solidity
File: src/transformers/LeverageTransformer.sol

// @audit deleverage
11: 		/// @notice Functionality to leverage / deleverage positions direcly in one tx

// @audit api
25: 		        bytes swapData0; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

// @audit api
29: 		        bytes swapData1; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

// @audit deadlineable
35: 		        // for all uniswap deadlineable functions

// @audit api
111: 		        bytes swapData0; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

// @audit api
115: 		        bytes swapData1; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

// @audit deadlineable
118: 		        // for all uniswap deadlineable functions
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L11), [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L25), [29](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L29), [35](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L35), [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L111), [115](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L115), [118](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L118)

```solidity
File: src/transformers/V3Utils.sol

// @audit api
60: 		        bytes swapData0; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

// @audit api
65: 		        bytes swapData1; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

// @audit deadlineable
78: 		        // for all uniswap deadlineable functions

// @audit transfered
458: 		        // data to be sent along newly created NFT when transfered to recipientNFT (sent to IERC721Receiver callback)

// @audit recieved
633: 		        // check if recieved correct amount of tokens

// @audit safemint
725: 		        // mint is done to address(this) because it is not a safemint and safeTransferFrom needs to be done manually afterwards
```

*GitHub* : [60](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L60), [65](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L65), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L78), [458](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L458), [633](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L633), [725](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L725)

```solidity
File: src/utils/Swapper.sol

// @audit transfered
97: 		                // tokens are transfered to Universalrouter directly (data.commands must include sweep action!)
```

*GitHub* : [97](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L97)

### [N-73]<a name="n-73"></a> Contracts should have full test coverage

A 100% test coverage is not foolproof, but it helps immensely in reducing the amount of bugs that may occur.

*There are 0 instance(s) of this issue:*

```solidity
File: All in-scope files
```

### [N-74]<a name="n-74"></a> Large or complicated code bases should implement invariant tests

This includes: large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts.

Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold.

Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers may help significantly.

*There are 0 instance(s) of this issue:*

```solidity
File: All in-scope files
```

### [N-75]<a name="n-75"></a> Codebase should implement formal verification testing

Formal verification is the act of proving or disproving the correctness of intended algorithms underlying a system with respect to a certain formal specification/property/invariant, using formal methods of mathematics.

Some tools that are currently available to perform these tests on smart contracts are [SMTChecker](https://docs.soliditylang.org/en/latest/smtchecker.html) and [Certora Prover](https://www.certora.com/).

*There are 0 instance(s) of this issue:*

```solidity
File: All in-scope files
```

### [N-76]<a name="n-76"></a> Inconsistent spacing in comments

Some lines use `// x` and some use `//x`. The instances below point out the usages that don't follow the majority, within each file.

*There are 4 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

25: 		    uint16 public constant MIN_PRICE_DIFFERENCE = 200; //2%
```

*GitHub* : [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L25)

```solidity
File: src/V3Vault.sol

41: 		    uint32 public constant MIN_RESERVE_PROTECTION_FACTOR_X32 = uint32(Q32 / 100); //1%

43: 		    uint32 public constant MAX_DAILY_LEND_INCREASE_X32 = uint32(Q32 / 10); //10%

44: 		    uint32 public constant MAX_DAILY_DEBT_INCREASE_X32 = uint32(Q32 / 10); //10%
```

*GitHub* : [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L41), [43](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L43), [44](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L44)

### [N-77]<a name="n-77"></a> State variables should include comments

Consider adding some comments on critical state variables to explain what they are supposed to do: this will help for future code reviews.

*There are 27 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

24: 		    uint256 public baseRatePerSecondX96;

25: 		    uint256 public jumpMultiplierPerSecondX96;

26: 		    uint256 public kinkX96;
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L24), [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L25), [26](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L26)

```solidity
File: src/V3Oracle.sol

27: 		    uint256 private constant Q96 = 2 ** 96;

28: 		    uint256 private constant Q128 = 2 ** 128;

58: 		    address public immutable factory;

59: 		    INonfungiblePositionManager public immutable nonfungiblePositionManager;

63: 		    uint8 public immutable referenceTokenDecimals;
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L27), [28](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L28), [58](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L58), [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L59), [63](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L63)

```solidity
File: src/V3Vault.sol

33: 		    uint256 private constant Q32 = 2 ** 32;

34: 		    uint256 private constant Q96 = 2 ** 96;

115: 		    mapping(address => TokenConfig) public tokenConfigs;

128: 		    uint256 public lastDebtExchangeRateX96 = Q96;

129: 		    uint256 public lastLendExchangeRateX96 = Q96;

131: 		    uint256 public globalDebtLimit = 0;

132: 		    uint256 public globalLendLimit = 0;

139: 		    uint256 public dailyLendIncreaseLimitLeft = 0;

140: 		    uint256 public dailyLendIncreaseLimitLastReset = 0;

144: 		    uint256 public dailyDebtIncreaseLimitLeft = 0;

145: 		    uint256 public dailyDebtIncreaseLimitLastReset = 0;
```

*GitHub* : [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L33), [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L34), [115](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L115), [128](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L128), [129](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L129), [131](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L131), [132](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L132), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L139), [140](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L140), [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L144), [145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L145)

```solidity
File: src/automators/Automator.sol

20: 		    uint256 internal constant Q64 = 2 ** 64;

21: 		    uint256 internal constant Q96 = 2 ** 96;

35: 		    mapping(address => bool) public vaults;

37: 		    address public withdrawer;

38: 		    uint32 public TWAPSeconds;

39: 		    uint16 public maxTWAPTickDifference;
```

*GitHub* : [20](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L20), [21](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L21), [35](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L35), [37](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L37), [38](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L38), [39](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L39)

```solidity
File: src/transformers/AutoCompound.sol

45: 		    mapping(uint256 => mapping(address => uint256)) public positionBalances;
```

*GitHub* : [45](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L45)

```solidity
File: src/utils/Swapper.sol

23: 		    address public immutable factory;
```

*GitHub* : [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L23)

### [N-78]<a name="n-78"></a> Complex functions should have explicit comments

Large and/or complex functions should have more comments to better explain the purpose of each logic step.

*There are 5 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

685: 		    function liquidate(LiquidateParams calldata params) external override returns (uint256 amount0, uint256 amount1) {
```

*GitHub* : [685](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L685)

```solidity
File: src/automators/AutoExit.sol

100: 		    function execute(ExecuteParams calldata params) external {
```

*GitHub* : [100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L100)

```solidity
File: src/transformers/AutoCompound.sol

101: 		    function execute(ExecuteParams calldata params) external nonReentrant {
```

*GitHub* : [101](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L101)

```solidity
File: src/transformers/AutoRange.sol

111: 		    function execute(ExecuteParams calldata params) external {
```

*GitHub* : [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L111)

```solidity
File: src/transformers/V3Utils.sol

115: 		    function execute(uint256 tokenId, Instructions memory instructions) public returns (uint256 newTokenId) {
```

*GitHub* : [115](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L115)

### [N-79]<a name="n-79"></a> Use `@inheritdoc` for overridden functions

`@inheritdoc` Copies all missing tags from the base function. [Documentation](https://docs.soliditylang.org/en/latest/natspec-format.html#tags)

*There are 23 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

58: 		    function getRatesPerSecondX96(uint256 cash, uint256 debt)
```

*GitHub* : [58](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L58)

```solidity
File: src/V3Oracle.sol

95: 		    function getValue(uint256 tokenId, address token)

162: 		    function getPositionBreakdown(uint256 tokenId)
```

*GitHub* : [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L95), [162](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L162)

```solidity
File: src/V3Vault.sol

195: 		    function vaultInfo()

219: 		    function lendInfo(address account) external view override returns (uint256 amount) {

231: 		    function loanInfo(uint256 tokenId)

258: 		    function ownerOf(uint256 tokenId) external view override returns (address owner) {

264: 		    function loanCount(address owner) external view override returns (uint256) {

271: 		    function loanAtIndex(address owner, uint256 index) external view override returns (uint256) {

384: 		    function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

390: 		    function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

400: 		    function create(uint256 tokenId, address recipient) external override {

410: 		    function createWithPermit(

483: 		    function approveTransform(uint256 tokenId, address target, bool isActive) external override {

497: 		    function transform(uint256 tokenId, address transformer, bytes calldata data)

550: 		    function borrow(uint256 tokenId, uint256 assets) external override {

609: 		    function decreaseLiquidityAndCollect(DecreaseLiquidityAndCollectParams calldata params)

652: 		    function repay(uint256 tokenId, uint256 amount, bool isShare) external override {

661: 		    function repay(uint256 tokenId, uint256 amount, bool isShare, bytes calldata permitData) external override {

685: 		    function liquidate(LiquidateParams calldata params) external override returns (uint256 amount0, uint256 amount1) {
```

*GitHub* : [400](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L400), [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L195), [219](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L219), [231](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L231), [258](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L258), [264](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L264), [271](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L271), [384](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L384), [390](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L390), [410](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L410), [483](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L483), [497](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L497), [550](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L550), [609](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L609), [652](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L652), [661](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L661), [685](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L685)

```solidity
File: src/transformers/AutoCompound.sol

227: 		    function withdrawBalances(address[] calldata tokens, address to) external override nonReentrant {
```

*GitHub* : [227](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L227)

```solidity
File: src/transformers/V3Utils.sol

356: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)
```

*GitHub* : [356](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L356)

```solidity
File: src/utils/Swapper.sol

156: 		    function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external override {
```

*GitHub* : [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L156)

### [N-80]<a name="n-80"></a> Variable names don't follow the Solidity naming convention

Use `mixedCase` for local and state variables that are not constants, and add a trailing underscore for non-external variables. [Documentation](https://docs.soliditylang.org/en/latest/style-guide.html#local-and-state-variable-names)

*There are 7 instance(s) of this issue:*

```solidity
File: src/automators/AutoExit.sol

// @audit _TWAPSeconds
37: 		        uint32 _TWAPSeconds,
```

*GitHub* : [37](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L37)

```solidity
File: src/automators/Automator.sol

// @audit TWAPSeconds
31: 		    event TWAPConfigChanged(uint32 TWAPSeconds, uint16 maxTWAPTickDifference);

// @audit TWAPSeconds
38: 		    uint32 public TWAPSeconds;

// @audit _TWAPSeconds
45: 		        uint32 _TWAPSeconds,

// @audit _TWAPSeconds
87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {
```

*GitHub* : [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L31), [38](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L38), [45](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L45), [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87)

```solidity
File: src/transformers/AutoCompound.sol

// @audit _TWAPSeconds
41: 		        uint32 _TWAPSeconds,
```

*GitHub* : [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L41)

```solidity
File: src/transformers/AutoRange.sol

// @audit _TWAPSeconds
29: 		        uint32 _TWAPSeconds,
```

*GitHub* : [29](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L29)

### [N-81]<a name="n-81"></a> `immutable` variable names should be uppercase

`immutable` variables should be named with all capital letters with underscores separating words. Examples: `TOKEN_ADDRESS`, `ROOT`. [Documentation](https://docs.soliditylang.org/en/latest/style-guide.html#constants)

*There are 18 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

58: 		    address public immutable factory;

59: 		    INonfungiblePositionManager public immutable nonfungiblePositionManager;

62: 		    address public immutable referenceToken;

63: 		    uint8 public immutable referenceTokenDecimals;

68: 		    address public immutable chainlinkReferenceToken;
```

*GitHub* : [58](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L58), [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L59), [62](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L62), [63](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L63), [68](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L68)

```solidity
File: src/V3Vault.sol

47: 		    INonfungiblePositionManager public immutable nonfungiblePositionManager;

50: 		    IUniswapV3Factory public immutable factory;

53: 		    IInterestRateModel public immutable interestRateModel;

56: 		    IV3Oracle public immutable oracle;

59: 		    IPermit2 public immutable permit2;

62: 		    address public immutable override asset;

65: 		    uint8 private immutable assetDecimals;
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L47), [50](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L50), [53](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L53), [56](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L56), [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L59), [62](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L62), [65](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L65)

```solidity
File: src/transformers/V3Utils.sol

19: 		    IPermit2 public immutable permit2;
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L19)

```solidity
File: src/utils/Swapper.sol

21: 		    IWETH9 public immutable weth;

23: 		    address public immutable factory;

26: 		    INonfungiblePositionManager public immutable nonfungiblePositionManager;

29: 		    address public immutable zeroxRouter;

32: 		    address public immutable universalRouter;
```

*GitHub* : [21](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L21), [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L23), [26](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L26), [29](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L29), [32](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L32)

### [N-82]<a name="n-82"></a> Missing underscore prefix for non-external variables

This convention is suggested for non-external state variables (private or internal). [Documentation](https://docs.soliditylang.org/en/latest/style-guide.html#underscore-prefix-for-non-external-functions-and-variables)

*There are 5 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

65: 		    uint8 private immutable assetDecimals;

157: 		    mapping(address => uint256[]) private ownedTokens; // Mapping from owner address to list of owned token IDs

158: 		    mapping(uint256 => uint256) private ownedTokensIndex; // Mapping from token ID to index of the owner tokens list (for removal without loop)

159: 		    mapping(uint256 => address) private tokenOwner; // Mapping from token ID to owner

161: 		    uint256 private transformedTokenId = 0; // transient storage (when available in dencun)
```

*GitHub* : [65](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L65), [157](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L157), [158](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L158), [159](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L159), [161](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L161)

### [N-83]<a name="n-83"></a> Invalid NatSpec comment style

NatSpec [must](https://docs.soliditylang.org/en/latest/natspec-format.html#documentation-example) begin with `///`, or use the `/* ... */` syntax.

*There are 1 instance(s) of this issue:*

```solidity
File: src/transformers/V3Utils.sol

18: 		    // @notice Permit2 contract
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L18)

### [N-84]<a name="n-84"></a> Missing NatSpec from contract declarations

Some contracts miss a `@dev/@notice` NatSpec, which should be a [best practice](https://docs.soliditylang.org/en/latest/natspec-format.html) to add as a documentation.

*There are 1 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

19: 		abstract contract Automator is Swapper, Ownable {
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L19)

### [N-85]<a name="n-85"></a> Missing NatSpec `@author` from contract declaration

Some contract definitions have an incomplete NatSpec: add a `@author` notation to improve the code documentation.

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

11: 		contract InterestRateModel is Ownable, IInterestRateModel, IErrors {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L11)

```solidity
File: src/V3Oracle.sol

24: 		contract V3Oracle is IV3Oracle, Ownable, IErrors {
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L24)

```solidity
File: src/V3Vault.sol

30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

```solidity
File: src/automators/AutoExit.sol

10: 		contract AutoExit is Automator {
```

*GitHub* : [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L10)

```solidity
File: src/automators/Automator.sol

19: 		abstract contract Automator is Swapper, Ownable {
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L19)

```solidity
File: src/transformers/AutoCompound.sol

16: 		contract AutoCompound is Automator, Multicall, ReentrancyGuard {
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L16)

```solidity
File: src/transformers/AutoRange.sol

11: 		contract AutoRange is Automator {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L11)

```solidity
File: src/transformers/LeverageTransformer.sol

12: 		contract LeverageTransformer is Swapper {
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L12)

```solidity
File: src/transformers/V3Utils.sol

15: 		contract V3Utils is Swapper, IERC721Receiver {
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L15)

```solidity
File: src/utils/FlashloanLiquidator.sol

11: 		contract FlashloanLiquidator is Swapper, IUniswapV3FlashCallback {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L11)

```solidity
File: src/utils/Swapper.sol

17: 		abstract contract Swapper is IUniswapV3SwapCallback, IErrors {
```

*GitHub* : [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L17)

### [N-86]<a name="n-86"></a> Missing NatSpec `@dev` from contract declaration

Some contract definitions have an incomplete NatSpec: add a `@dev` notation to describe the contract to improve the code documentation.

*There are 11 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

11: 		contract InterestRateModel is Ownable, IInterestRateModel, IErrors {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L11)

```solidity
File: src/V3Oracle.sol

24: 		contract V3Oracle is IV3Oracle, Ownable, IErrors {
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L24)

```solidity
File: src/V3Vault.sol

30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

```solidity
File: src/automators/AutoExit.sol

10: 		contract AutoExit is Automator {
```

*GitHub* : [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L10)

```solidity
File: src/automators/Automator.sol

19: 		abstract contract Automator is Swapper, Ownable {
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L19)

```solidity
File: src/transformers/AutoCompound.sol

16: 		contract AutoCompound is Automator, Multicall, ReentrancyGuard {
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L16)

```solidity
File: src/transformers/AutoRange.sol

11: 		contract AutoRange is Automator {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L11)

```solidity
File: src/transformers/LeverageTransformer.sol

12: 		contract LeverageTransformer is Swapper {
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L12)

```solidity
File: src/transformers/V3Utils.sol

15: 		contract V3Utils is Swapper, IERC721Receiver {
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L15)

```solidity
File: src/utils/FlashloanLiquidator.sol

11: 		contract FlashloanLiquidator is Swapper, IUniswapV3FlashCallback {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L11)

```solidity
File: src/utils/Swapper.sol

17: 		abstract contract Swapper is IUniswapV3SwapCallback, IErrors {
```

*GitHub* : [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L17)

### [N-87]<a name="n-87"></a> Missing NatSpec `@notice` from contract declaration

Some contract definitions have an incomplete NatSpec: add a `@notice` notation to describe the contract to improve the code documentation.

*There are 3 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

19: 		abstract contract Automator is Swapper, Ownable {
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L19)

```solidity
File: src/utils/FlashloanLiquidator.sol

11: 		contract FlashloanLiquidator is Swapper, IUniswapV3FlashCallback {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L11)

```solidity
File: src/utils/Swapper.sol

17: 		abstract contract Swapper is IUniswapV3SwapCallback, IErrors {
```

*GitHub* : [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L17)

### [N-88]<a name="n-88"></a> Missing NatSpec `@title` from contract declaration

Some contract definitions have an incomplete NatSpec: add a `@title` notation to describe the contract to improve the code documentation.

*There are 2 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

19: 		abstract contract Automator is Swapper, Ownable {
```

*GitHub* : [19](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L19)

```solidity
File: src/utils/Swapper.sol

17: 		abstract contract Swapper is IUniswapV3SwapCallback, IErrors {
```

*GitHub* : [17](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L17)

### [N-89]<a name="n-89"></a> Missing NatSpec from event declaration

Consider adding some comments on event declarations to explain what they are supposed to do: this will help for future code reviews.

*There are 39 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

18: 		    event SetValues(
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L18)

```solidity
File: src/V3Oracle.sol

30: 		    event TokenConfigUpdated(address indexed token, TokenConfig config);

31: 		    event OracleModeUpdated(address indexed token, Mode mode);

32: 		    event SetMaxPoolPriceDifference(uint16 maxPoolPriceDifference);

33: 		    event SetEmergencyAdmin(address emergencyAdmin);
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L30), [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L31), [32](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L32), [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L33)

```solidity
File: src/V3Vault.sol

68: 		    event ApprovedTransform(uint256 indexed tokenId, address owner, address target, bool isActive);

70: 		    event Add(uint256 indexed tokenId, address owner, uint256 oldTokenId); // when a token is added replacing another token - oldTokenId > 0

71: 		    event Remove(uint256 indexed tokenId, address recipient);

73: 		    event ExchangeRateUpdate(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96);

75: 		    event WithdrawCollateral(

78: 		    event Borrow(uint256 indexed tokenId, address owner, uint256 assets, uint256 shares);

79: 		    event Repay(uint256 indexed tokenId, address repayer, address owner, uint256 assets, uint256 shares);

80: 		    event Liquidate(

93: 		    event WithdrawReserves(uint256 amount, address receiver);

94: 		    event SetTransformer(address transformer, bool active);

95: 		    event SetLimits(

102: 		    event SetReserveFactor(uint32 reserveFactorX32);

103: 		    event SetReserveProtectionFactor(uint32 reserveProtectionFactorX32);

104: 		    event SetTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32);

106: 		    event SetEmergencyAdmin(address emergencyAdmin);
```

*GitHub* : [68](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L68), [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L70), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L71), [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L73), [75](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L75), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L78), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L79), [80](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L80), [93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L93), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L94), [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L95), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L102), [103](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L103), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L104), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L106)

```solidity
File: src/automators/AutoExit.sol

11: 		    event Executed(

20: 		    event PositionConfigured(
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L11), [20](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L20)

```solidity
File: src/automators/Automator.sol

27: 		    event OperatorChanged(address newOperator, bool active);

28: 		    event VaultChanged(address newVault, bool active);

30: 		    event WithdrawerChanged(address newWithdrawer);

31: 		    event TWAPConfigChanged(uint32 TWAPSeconds, uint16 maxTWAPTickDifference);
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L27), [28](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L28), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L30), [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L31)

```solidity
File: src/transformers/AutoCompound.sol

18: 		    event AutoCompounded(

30: 		    event RewardUpdated(address account, uint64 totalRewardX64);

33: 		    event BalanceAdded(uint256 tokenId, address token, uint256 amount);

34: 		    event BalanceRemoved(uint256 tokenId, address token, uint256 amount);

35: 		    event BalanceWithdrawn(uint256 tokenId, address token, address to, uint256 amount);
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L18), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L30), [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L33), [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L34), [35](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L35)

```solidity
File: src/transformers/AutoRange.sol

12: 		    event RangeChanged(uint256 indexed oldTokenId, uint256 indexed newTokenId);

13: 		    event PositionConfigured(
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L12), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L13)

```solidity
File: src/transformers/V3Utils.sol

22: 		    event CompoundFees(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

23: 		    event ChangeRange(uint256 indexed tokenId, uint256 newTokenId);

24: 		    event WithdrawAndCollectAndSwap(uint256 indexed tokenId, address token, uint256 amount);

25: 		    event SwapAndMint(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

26: 		    event SwapAndIncreaseLiquidity(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);
```

*GitHub* : [22](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L22), [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L23), [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L24), [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L25), [26](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L26)

```solidity
File: src/utils/Swapper.sol

18: 		    event Swap(address indexed tokenIn, address indexed tokenOut, uint256 amountIn, uint256 amountOut);
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L18)

### [N-90]<a name="n-90"></a> Missing NatSpec `@dev` from event declaration

Some events have an incomplete NatSpec: add a `@dev` notation to describe the event to improve the code documentation.

*There are 39 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

18: 		    event SetValues(
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L18)

```solidity
File: src/V3Oracle.sol

30: 		    event TokenConfigUpdated(address indexed token, TokenConfig config);

31: 		    event OracleModeUpdated(address indexed token, Mode mode);

32: 		    event SetMaxPoolPriceDifference(uint16 maxPoolPriceDifference);

33: 		    event SetEmergencyAdmin(address emergencyAdmin);
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L30), [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L31), [32](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L32), [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L33)

```solidity
File: src/V3Vault.sol

68: 		    event ApprovedTransform(uint256 indexed tokenId, address owner, address target, bool isActive);

70: 		    event Add(uint256 indexed tokenId, address owner, uint256 oldTokenId); // when a token is added replacing another token - oldTokenId > 0

71: 		    event Remove(uint256 indexed tokenId, address recipient);

73: 		    event ExchangeRateUpdate(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96);

75: 		    event WithdrawCollateral(

78: 		    event Borrow(uint256 indexed tokenId, address owner, uint256 assets, uint256 shares);

79: 		    event Repay(uint256 indexed tokenId, address repayer, address owner, uint256 assets, uint256 shares);

80: 		    event Liquidate(

93: 		    event WithdrawReserves(uint256 amount, address receiver);

94: 		    event SetTransformer(address transformer, bool active);

95: 		    event SetLimits(

102: 		    event SetReserveFactor(uint32 reserveFactorX32);

103: 		    event SetReserveProtectionFactor(uint32 reserveProtectionFactorX32);

104: 		    event SetTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32);

106: 		    event SetEmergencyAdmin(address emergencyAdmin);
```

*GitHub* : [68](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L68), [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L70), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L71), [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L73), [75](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L75), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L78), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L79), [80](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L80), [93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L93), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L94), [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L95), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L102), [103](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L103), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L104), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L106)

```solidity
File: src/automators/AutoExit.sol

11: 		    event Executed(

20: 		    event PositionConfigured(
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L11), [20](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L20)

```solidity
File: src/automators/Automator.sol

27: 		    event OperatorChanged(address newOperator, bool active);

28: 		    event VaultChanged(address newVault, bool active);

30: 		    event WithdrawerChanged(address newWithdrawer);

31: 		    event TWAPConfigChanged(uint32 TWAPSeconds, uint16 maxTWAPTickDifference);
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L27), [28](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L28), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L30), [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L31)

```solidity
File: src/transformers/AutoCompound.sol

18: 		    event AutoCompounded(

30: 		    event RewardUpdated(address account, uint64 totalRewardX64);

33: 		    event BalanceAdded(uint256 tokenId, address token, uint256 amount);

34: 		    event BalanceRemoved(uint256 tokenId, address token, uint256 amount);

35: 		    event BalanceWithdrawn(uint256 tokenId, address token, address to, uint256 amount);
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L18), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L30), [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L33), [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L34), [35](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L35)

```solidity
File: src/transformers/AutoRange.sol

12: 		    event RangeChanged(uint256 indexed oldTokenId, uint256 indexed newTokenId);

13: 		    event PositionConfigured(
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L12), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L13)

```solidity
File: src/transformers/V3Utils.sol

22: 		    event CompoundFees(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

23: 		    event ChangeRange(uint256 indexed tokenId, uint256 newTokenId);

24: 		    event WithdrawAndCollectAndSwap(uint256 indexed tokenId, address token, uint256 amount);

25: 		    event SwapAndMint(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

26: 		    event SwapAndIncreaseLiquidity(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);
```

*GitHub* : [22](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L22), [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L23), [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L24), [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L25), [26](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L26)

```solidity
File: src/utils/Swapper.sol

18: 		    event Swap(address indexed tokenIn, address indexed tokenOut, uint256 amountIn, uint256 amountOut);
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L18)

### [N-91]<a name="n-91"></a> Missing NatSpec `@notice` from event declaration

Some events have an incomplete NatSpec: add a `@notice` notation to describe the event to improve the code documentation.

*There are 39 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

18: 		    event SetValues(
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L18)

```solidity
File: src/V3Oracle.sol

30: 		    event TokenConfigUpdated(address indexed token, TokenConfig config);

31: 		    event OracleModeUpdated(address indexed token, Mode mode);

32: 		    event SetMaxPoolPriceDifference(uint16 maxPoolPriceDifference);

33: 		    event SetEmergencyAdmin(address emergencyAdmin);
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L30), [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L31), [32](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L32), [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L33)

```solidity
File: src/V3Vault.sol

68: 		    event ApprovedTransform(uint256 indexed tokenId, address owner, address target, bool isActive);

70: 		    event Add(uint256 indexed tokenId, address owner, uint256 oldTokenId); // when a token is added replacing another token - oldTokenId > 0

71: 		    event Remove(uint256 indexed tokenId, address recipient);

73: 		    event ExchangeRateUpdate(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96);

75: 		    event WithdrawCollateral(

78: 		    event Borrow(uint256 indexed tokenId, address owner, uint256 assets, uint256 shares);

79: 		    event Repay(uint256 indexed tokenId, address repayer, address owner, uint256 assets, uint256 shares);

80: 		    event Liquidate(

93: 		    event WithdrawReserves(uint256 amount, address receiver);

94: 		    event SetTransformer(address transformer, bool active);

95: 		    event SetLimits(

102: 		    event SetReserveFactor(uint32 reserveFactorX32);

103: 		    event SetReserveProtectionFactor(uint32 reserveProtectionFactorX32);

104: 		    event SetTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32);

106: 		    event SetEmergencyAdmin(address emergencyAdmin);
```

*GitHub* : [68](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L68), [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L70), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L71), [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L73), [75](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L75), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L78), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L79), [80](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L80), [93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L93), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L94), [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L95), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L102), [103](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L103), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L104), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L106)

```solidity
File: src/automators/AutoExit.sol

11: 		    event Executed(

20: 		    event PositionConfigured(
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L11), [20](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L20)

```solidity
File: src/automators/Automator.sol

27: 		    event OperatorChanged(address newOperator, bool active);

28: 		    event VaultChanged(address newVault, bool active);

30: 		    event WithdrawerChanged(address newWithdrawer);

31: 		    event TWAPConfigChanged(uint32 TWAPSeconds, uint16 maxTWAPTickDifference);
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L27), [28](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L28), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L30), [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L31)

```solidity
File: src/transformers/AutoCompound.sol

18: 		    event AutoCompounded(

30: 		    event RewardUpdated(address account, uint64 totalRewardX64);

33: 		    event BalanceAdded(uint256 tokenId, address token, uint256 amount);

34: 		    event BalanceRemoved(uint256 tokenId, address token, uint256 amount);

35: 		    event BalanceWithdrawn(uint256 tokenId, address token, address to, uint256 amount);
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L18), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L30), [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L33), [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L34), [35](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L35)

```solidity
File: src/transformers/AutoRange.sol

12: 		    event RangeChanged(uint256 indexed oldTokenId, uint256 indexed newTokenId);

13: 		    event PositionConfigured(
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L12), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L13)

```solidity
File: src/transformers/V3Utils.sol

22: 		    event CompoundFees(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

23: 		    event ChangeRange(uint256 indexed tokenId, uint256 newTokenId);

24: 		    event WithdrawAndCollectAndSwap(uint256 indexed tokenId, address token, uint256 amount);

25: 		    event SwapAndMint(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

26: 		    event SwapAndIncreaseLiquidity(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);
```

*GitHub* : [22](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L22), [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L23), [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L24), [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L25), [26](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L26)

```solidity
File: src/utils/Swapper.sol

18: 		    event Swap(address indexed tokenIn, address indexed tokenOut, uint256 amountIn, uint256 amountOut);
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L18)

### [N-92]<a name="n-92"></a> Missing NatSpec `@param` from event declaration

Some events have an incomplete NatSpec: add a `@param` notation to describe the event to improve the code documentation.

*There are 39 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit missing baseRatePerYearX96, multiplierPerYearX96, jumpMultiplierPerYearX96, kinkX96
18: 		    event SetValues(
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L18)

```solidity
File: src/V3Oracle.sol

// @audit missing token, config
30: 		    event TokenConfigUpdated(address indexed token, TokenConfig config);

// @audit missing token, mode
31: 		    event OracleModeUpdated(address indexed token, Mode mode);

// @audit missing maxPoolPriceDifference
32: 		    event SetMaxPoolPriceDifference(uint16 maxPoolPriceDifference);

// @audit missing emergencyAdmin
33: 		    event SetEmergencyAdmin(address emergencyAdmin);
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L30), [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L31), [32](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L32), [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L33)

```solidity
File: src/V3Vault.sol

// @audit missing tokenId, owner, target, isActive
68: 		    event ApprovedTransform(uint256 indexed tokenId, address owner, address target, bool isActive);

// @audit missing tokenId, owner, oldTokenId
70: 		    event Add(uint256 indexed tokenId, address owner, uint256 oldTokenId); // when a token is added replacing another token - oldTokenId > 0

// @audit missing tokenId, recipient
71: 		    event Remove(uint256 indexed tokenId, address recipient);

// @audit missing debtExchangeRateX96, lendExchangeRateX96
73: 		    event ExchangeRateUpdate(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96);

// @audit missing tokenId, owner, recipient, liquidity, amount0, amount1
75: 		    event WithdrawCollateral(

// @audit missing tokenId, owner, assets, shares
78: 		    event Borrow(uint256 indexed tokenId, address owner, uint256 assets, uint256 shares);

// @audit missing tokenId, repayer, owner, assets, shares
79: 		    event Repay(uint256 indexed tokenId, address repayer, address owner, uint256 assets, uint256 shares);

// @audit missing tokenId, liquidator, owner, value, cost, amount0, amount1, reserve, missing
80: 		    event Liquidate(

// @audit missing amount, receiver
93: 		    event WithdrawReserves(uint256 amount, address receiver);

// @audit missing transformer, active
94: 		    event SetTransformer(address transformer, bool active);

// @audit missing minLoanSize, globalLendLimit, globalDebtLimit, dailyLendIncreaseLimitMin, dailyDebtIncreaseLimitMin
95: 		    event SetLimits(

// @audit missing reserveFactorX32
102: 		    event SetReserveFactor(uint32 reserveFactorX32);

// @audit missing reserveProtectionFactorX32
103: 		    event SetReserveProtectionFactor(uint32 reserveProtectionFactorX32);

// @audit missing token, collateralFactorX32, collateralValueLimitFactorX32
104: 		    event SetTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32);

// @audit missing emergencyAdmin
106: 		    event SetEmergencyAdmin(address emergencyAdmin);
```

*GitHub* : [68](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L68), [70](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L70), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L71), [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L73), [75](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L75), [78](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L78), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L79), [80](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L80), [93](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L93), [94](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L94), [95](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L95), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L102), [103](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L103), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L104), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L106)

```solidity
File: src/automators/AutoExit.sol

// @audit missing tokenId, account, isSwap, amountReturned0, amountReturned1, token0, token1
11: 		    event Executed(

// @audit missing tokenId, isActive, token0Swap, token1Swap, token0TriggerTick, token1TriggerTick, token0SlippageX64, token1SlippageX64, onlyFees, maxRewardX64
20: 		    event PositionConfigured(
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L11), [20](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L20)

```solidity
File: src/automators/Automator.sol

// @audit missing newOperator, active
27: 		    event OperatorChanged(address newOperator, bool active);

// @audit missing newVault, active
28: 		    event VaultChanged(address newVault, bool active);

// @audit missing newWithdrawer
30: 		    event WithdrawerChanged(address newWithdrawer);

// @audit missing TWAPSeconds, maxTWAPTickDifference
31: 		    event TWAPConfigChanged(uint32 TWAPSeconds, uint16 maxTWAPTickDifference);
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L27), [28](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L28), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L30), [31](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L31)

```solidity
File: src/transformers/AutoCompound.sol

// @audit missing account, tokenId, amountAdded0, amountAdded1, reward0, reward1, token0, token1
18: 		    event AutoCompounded(

// @audit missing account, totalRewardX64
30: 		    event RewardUpdated(address account, uint64 totalRewardX64);

// @audit missing tokenId, token, amount
33: 		    event BalanceAdded(uint256 tokenId, address token, uint256 amount);

// @audit missing tokenId, token, amount
34: 		    event BalanceRemoved(uint256 tokenId, address token, uint256 amount);

// @audit missing tokenId, token, to, amount
35: 		    event BalanceWithdrawn(uint256 tokenId, address token, address to, uint256 amount);
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L18), [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L30), [33](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L33), [34](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L34), [35](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L35)

```solidity
File: src/transformers/AutoRange.sol

// @audit missing oldTokenId, newTokenId
12: 		    event RangeChanged(uint256 indexed oldTokenId, uint256 indexed newTokenId);

// @audit missing tokenId, lowerTickLimit, upperTickLimit, lowerTickDelta, upperTickDelta, token0SlippageX64, token1SlippageX64, onlyFees, maxRewardX64
13: 		    event PositionConfigured(
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L12), [13](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L13)

```solidity
File: src/transformers/V3Utils.sol

// @audit missing tokenId, liquidity, amount0, amount1
22: 		    event CompoundFees(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

// @audit missing tokenId, newTokenId
23: 		    event ChangeRange(uint256 indexed tokenId, uint256 newTokenId);

// @audit missing tokenId, token, amount
24: 		    event WithdrawAndCollectAndSwap(uint256 indexed tokenId, address token, uint256 amount);

// @audit missing tokenId, liquidity, amount0, amount1
25: 		    event SwapAndMint(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

// @audit missing tokenId, liquidity, amount0, amount1
26: 		    event SwapAndIncreaseLiquidity(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);
```

*GitHub* : [22](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L22), [23](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L23), [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L24), [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L25), [26](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L26)

```solidity
File: src/utils/Swapper.sol

// @audit missing tokenIn, tokenOut, amountIn, amountOut
18: 		    event Swap(address indexed tokenIn, address indexed tokenOut, uint256 amountIn, uint256 amountOut);
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L18)

### [N-93]<a name="n-93"></a> Missing NatSpec from function definitions

Some functions miss a NatSpec, which should be a [best practice](https://docs.soliditylang.org/en/latest/natspec-format.html) to add as a documentation.

Even if Natspec for internal and private function is not parsed (but this may change in the future, according to the official docs), it still helps while reviewing the codebase.

*There are 65 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

133: 		    function _checkPoolPrice(address token0, address token1, uint24 fee, uint256 derivedPoolPriceX96) internal view {

139: 		    function _requireMaxDifference(uint256 priceX96, uint256 verifyPriceX96, uint256 maxDifferenceX10000)

272: 		    function _getReferenceTokenPriceX96(address token, uint256 cachedChainlinkReferencePriceX96)

329: 		    function _getChainlinkPriceX96(address token) internal view returns (uint256) {

346: 		    function _getTWAPPriceX96(TokenConfig memory feedConfig) internal view returns (uint256 poolTWAPPriceX96) {

359: 		    function _getReferencePoolPriceX96(IUniswapV3Pool pool, uint32 twapSeconds) internal view returns (uint256) {

395: 		    function _initializeState(uint256 tokenId) internal view returns (PositionState memory state) {

426: 		    function _getAmounts(PositionState memory state)

445: 		    function _getUncollectedFees(PositionState memory position, int24 tick)

472: 		    function _getFeeGrowthInside(

499: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L133), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L139), [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L272), [329](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L329), [346](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L346), [359](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L359), [395](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L395), [426](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L426), [445](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L445), [472](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L472), [499](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L499)

```solidity
File: src/V3Vault.sol

384: 		    function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

390: 		    function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

877: 		    function _deposit(address receiver, uint256 amount, bool isShare, bytes memory permitData)

920: 		    function _withdraw(address receiver, address owner, uint256 amount, bool isShare)

954: 		    function _repay(uint256 tokenId, uint256 amount, bool isShare, bytes memory permitData) internal {

1017: 		    function _getAvailableBalance(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96)

1032: 		    function _sendPositionValue(

1077: 		    function _cleanupLoan(uint256 tokenId, uint256 debtExchangeRateX96, uint256 lendExchangeRateX96, address owner)

1090: 		    function _calculateLiquidation(uint256 debt, uint256 fullValue, uint256 collateralValue)

1123: 		    function _handleReserveLiquidation(

1143: 		    function _calculateTokenCollateralFactorX32(uint256 tokenId) internal view returns (uint32) {

1150: 		    function _updateGlobalInterest()

1167: 		    function _calculateGlobalInterest()

1197: 		    function _requireLoanIsHealthy(uint256 tokenId, uint256 debt) internal view {

1205: 		    function _updateAndCheckCollateral(

1246: 		    function _resetDailyLendIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

1258: 		    function _resetDailyDebtIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

1270: 		    function _checkLoanIsHealthy(uint256 tokenId, uint256 debt)

1281: 		    function _convertToShares(uint256 amount, uint256 exchangeRateX96, Math.Rounding rounding)

1289: 		    function _convertToAssets(uint256 shares, uint256 exchangeRateX96, Math.Rounding rounding)

1297: 		    function _addTokenToOwner(address to, uint256 tokenId) internal {

1303: 		    function _removeTokenFromOwner(address from, uint256 tokenId) internal {
```

*GitHub* : [384](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L384), [390](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L390), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L877), [920](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L920), [954](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L954), [1017](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1017), [1032](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1032), [1077](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1077), [1090](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1090), [1123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1123), [1143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1143), [1150](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1150), [1167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1167), [1197](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1197), [1205](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1205), [1246](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1246), [1258](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1258), [1270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1270), [1281](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1281), [1289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1289), [1297](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1297), [1303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1303)

```solidity
File: src/automators/AutoExit.sol

218: 		    function configToken(uint256 tokenId, PositionConfig calldata config) external {
```

*GitHub* : [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L218)

```solidity
File: src/automators/Automator.sol

139: 		    function _validateSwap(

166: 		    function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

180: 		    function _getTWAPTick(IUniswapV3Pool pool, uint32 twapPeriod) internal view returns (int24, bool) {

193: 		    function _decreaseFullLiquidityAndCollect(

218: 		    function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {

230: 		    function _validateOwner(uint256 tokenId, address vault) internal returns (address owner) {

251: 		    receive() external payable {
```

*GitHub* : [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L139), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L166), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L180), [193](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L193), [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L218), [230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L230), [251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L251)

```solidity
File: src/transformers/AutoCompound.sol

249: 		    function _increaseBalance(uint256 tokenId, address token, uint256 amount) internal {

254: 		    function _setBalance(uint256 tokenId, address token, uint256 amount) internal {

266: 		    function _withdrawBalanceInternal(uint256 tokenId, address token, address to, uint256 balance, uint256 amount)

276: 		    function _checkApprovals(address token0, address token1) internal {
```

*GitHub* : [249](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L249), [254](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L254), [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L266), [276](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L276)

```solidity
File: src/transformers/AutoRange.sol

276: 		    function configToken(uint256 tokenId, address vault, PositionConfig calldata config) external {

300: 		    function _getTickSpacing(uint24 fee) internal view returns (int24) {
```

*GitHub* : [276](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L276), [300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L300)

```solidity
File: src/transformers/LeverageTransformer.sol

40: 		    function leverageUp(LeverageUpParams calldata params) external {

123: 		    function leverageDown(LeverageDownParams calldata params) external {
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L40), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L123)

```solidity
File: src/transformers/V3Utils.sol

566: 		    function _prepareAddApproved(

598: 		    function _prepareAddPermit2(

653: 		    function _prepareAdd(

705: 		    function _swapAndMint(SwapAndMintParams memory params, bool unwrap)

735: 		    function _swapAndIncrease(SwapAndIncreaseLiquidityParams memory params, IERC20 token0, IERC20 token1, bool unwrap)

779: 		    function _swapAndPrepareAmounts(SwapAndMintParams memory params, bool unwrap)

841: 		    function _returnLeftoverTokens(

864: 		    function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {

877: 		    function _decreaseLiquidity(

892: 		    function _collectFees(uint256 tokenId, IERC20 token0, IERC20 token1, uint128 collectAmount0, uint128 collectAmount1)

914: 		    receive() external payable {
```

*GitHub* : [566](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L566), [598](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L598), [653](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L653), [705](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L705), [735](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L735), [779](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L779), [841](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L841), [864](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L864), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L877), [892](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L892), [914](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L914)

```solidity
File: src/utils/FlashloanLiquidator.sol

67: 		    function uniswapV3FlashCallback(uint256 fee0, uint256 fee1, bytes calldata callbackData) external {
```

*GitHub* : [67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L67)

```solidity
File: src/utils/Swapper.sol

73: 		    function _routerSwap(RouterSwapParams memory params)

132: 		    function _poolSwap(PoolSwapParams memory params) internal returns (uint256 amountInDelta, uint256 amountOutDelta) {

156: 		    function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external override {

171: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L73), [132](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L132), [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L156), [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L171)

### [N-94]<a name="n-94"></a> Missing NatSpec `@dev` from function declaration

Some functions have an incomplete NatSpec: add a `@dev` notation to describe the function to improve the code documentation.

*There are 114 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

46: 		    function getUtilizationRateX96(uint256 cash, uint256 debt) public pure returns (uint256) {

58: 		    function getRatesPerSecondX96(uint256 cash, uint256 debt)

82: 		    function setValues(
```

*GitHub* : [46](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L46), [58](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L58), [82](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L82)

```solidity
File: src/V3Oracle.sol

133: 		    function _checkPoolPrice(address token0, address token1, uint24 fee, uint256 derivedPoolPriceX96) internal view {

139: 		    function _requireMaxDifference(uint256 priceX96, uint256 verifyPriceX96, uint256 maxDifferenceX10000)

162: 		    function getPositionBreakdown(uint256 tokenId)

185: 		    function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

201: 		    function setTokenConfig(

249: 		    function setOracleMode(address token, Mode mode) external {

265: 		    function setEmergencyAdmin(address admin) external onlyOwner {

272: 		    function _getReferenceTokenPriceX96(address token, uint256 cachedChainlinkReferencePriceX96)

329: 		    function _getChainlinkPriceX96(address token) internal view returns (uint256) {

346: 		    function _getTWAPPriceX96(TokenConfig memory feedConfig) internal view returns (uint256 poolTWAPPriceX96) {

359: 		    function _getReferencePoolPriceX96(IUniswapV3Pool pool, uint32 twapSeconds) internal view returns (uint256) {

395: 		    function _initializeState(uint256 tokenId) internal view returns (PositionState memory state) {

426: 		    function _getAmounts(PositionState memory state)

445: 		    function _getUncollectedFees(PositionState memory position, int24 tick)

472: 		    function _getFeeGrowthInside(

499: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L133), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L139), [162](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L162), [185](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L185), [201](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L201), [249](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L249), [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L265), [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L272), [329](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L329), [346](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L346), [359](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L359), [395](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L395), [426](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L426), [445](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L445), [472](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L472), [499](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L499)

```solidity
File: src/V3Vault.sol

195: 		    function vaultInfo()

219: 		    function lendInfo(address account) external view override returns (uint256 amount) {

231: 		    function loanInfo(uint256 tokenId)

258: 		    function ownerOf(uint256 tokenId) external view override returns (address owner) {

264: 		    function loanCount(address owner) external view override returns (uint256) {

271: 		    function loanAtIndex(address owner, uint256 index) external view override returns (uint256) {

384: 		    function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

390: 		    function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

400: 		    function create(uint256 tokenId, address recipient) external override {

410: 		    function createWithPermit(

483: 		    function approveTransform(uint256 tokenId, address target, bool isActive) external override {

497: 		    function transform(uint256 tokenId, address transformer, bytes calldata data)

550: 		    function borrow(uint256 tokenId, uint256 assets) external override {

652: 		    function repay(uint256 tokenId, uint256 amount, bool isShare) external override {

661: 		    function repay(uint256 tokenId, uint256 amount, bool isShare, bytes calldata permitData) external override {

685: 		    function liquidate(LiquidateParams calldata params) external override returns (uint256 amount0, uint256 amount1) {

765: 		    function withdrawReserves(uint256 amount, address receiver) external onlyOwner {

788: 		    function setTransformer(address transformer, bool active) external onlyOwner {

807: 		    function setLimits(

837: 		    function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

844: 		    function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

856: 		    function setTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32)

870: 		    function setEmergencyAdmin(address admin) external onlyOwner {

877: 		    function _deposit(address receiver, uint256 amount, bool isShare, bytes memory permitData)

920: 		    function _withdraw(address receiver, address owner, uint256 amount, bool isShare)

954: 		    function _repay(uint256 tokenId, uint256 amount, bool isShare, bytes memory permitData) internal {

1017: 		    function _getAvailableBalance(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96)

1032: 		    function _sendPositionValue(

1077: 		    function _cleanupLoan(uint256 tokenId, uint256 debtExchangeRateX96, uint256 lendExchangeRateX96, address owner)

1090: 		    function _calculateLiquidation(uint256 debt, uint256 fullValue, uint256 collateralValue)

1123: 		    function _handleReserveLiquidation(

1143: 		    function _calculateTokenCollateralFactorX32(uint256 tokenId) internal view returns (uint32) {

1150: 		    function _updateGlobalInterest()

1167: 		    function _calculateGlobalInterest()

1197: 		    function _requireLoanIsHealthy(uint256 tokenId, uint256 debt) internal view {

1205: 		    function _updateAndCheckCollateral(

1246: 		    function _resetDailyLendIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

1258: 		    function _resetDailyDebtIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

1270: 		    function _checkLoanIsHealthy(uint256 tokenId, uint256 debt)

1281: 		    function _convertToShares(uint256 amount, uint256 exchangeRateX96, Math.Rounding rounding)

1289: 		    function _convertToAssets(uint256 shares, uint256 exchangeRateX96, Math.Rounding rounding)

1297: 		    function _addTokenToOwner(address to, uint256 tokenId) internal {

1303: 		    function _removeTokenFromOwner(address from, uint256 tokenId) internal {
```

*GitHub* : [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L195), [219](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L219), [231](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L231), [258](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L258), [264](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L264), [271](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L271), [384](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L384), [390](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L390), [400](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L400), [410](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L410), [483](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L483), [497](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L497), [550](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L550), [652](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L652), [661](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L661), [685](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L685), [765](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L765), [788](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L788), [807](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L807), [837](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L837), [844](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L844), [856](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L856), [870](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L870), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L877), [920](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L920), [954](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L954), [1017](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1017), [1032](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1032), [1077](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1077), [1090](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1090), [1123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1123), [1143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1143), [1150](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1150), [1167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1167), [1197](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1197), [1205](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1205), [1246](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1246), [1258](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1258), [1270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1270), [1281](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1281), [1289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1289), [1297](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1297), [1303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1303)

```solidity
File: src/automators/AutoExit.sol

100: 		    function execute(ExecuteParams calldata params) external {

218: 		    function configToken(uint256 tokenId, PositionConfig calldata config) external {
```

*GitHub* : [100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L100), [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L218)

```solidity
File: src/automators/Automator.sol

59: 		    function setWithdrawer(address _withdrawer) public onlyOwner {

69: 		    function setOperator(address _operator, bool _active) public onlyOwner {

79: 		    function setVault(address _vault, bool _active) public onlyOwner {

87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {

104: 		    function withdrawBalances(address[] calldata tokens, address to) external virtual {

123: 		    function withdrawETH(address to) external {

139: 		    function _validateSwap(

166: 		    function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

180: 		    function _getTWAPTick(IUniswapV3Pool pool, uint32 twapPeriod) internal view returns (int24, bool) {

193: 		    function _decreaseFullLiquidityAndCollect(

218: 		    function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {

230: 		    function _validateOwner(uint256 tokenId, address vault) internal returns (address owner) {

251: 		    receive() external payable {
```

*GitHub* : [59](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L59), [69](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L69), [79](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L79), [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87), [104](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L104), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L123), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L139), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L166), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L180), [193](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L193), [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L218), [230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L230), [251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L251)

```solidity
File: src/transformers/AutoCompound.sol

87: 		    function executeWithVault(ExecuteParams calldata params, address vault) external {

101: 		    function execute(ExecuteParams calldata params) external nonReentrant {

200: 		    function withdrawLeftoverBalances(uint256 tokenId, address to) external nonReentrant {

243: 		    function setReward(uint64 _totalRewardX64) external onlyOwner {

249: 		    function _increaseBalance(uint256 tokenId, address token, uint256 amount) internal {

254: 		    function _setBalance(uint256 tokenId, address token, uint256 amount) internal {

266: 		    function _withdrawBalanceInternal(uint256 tokenId, address token, address to, uint256 balance, uint256 amount)

276: 		    function _checkApprovals(address token0, address token1) internal {
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L87), [101](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L101), [200](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L200), [243](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L243), [249](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L249), [254](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L254), [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L266), [276](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L276)

```solidity
File: src/transformers/AutoRange.sol

97: 		    function executeWithVault(ExecuteParams calldata params, address vault) external {

111: 		    function execute(ExecuteParams calldata params) external {

276: 		    function configToken(uint256 tokenId, address vault, PositionConfig calldata config) external {

300: 		    function _getTickSpacing(uint24 fee) internal view returns (int24) {
```

*GitHub* : [97](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L97), [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L111), [276](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L276), [300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L300)

```solidity
File: src/transformers/LeverageTransformer.sol

40: 		    function leverageUp(LeverageUpParams calldata params) external {

123: 		    function leverageDown(LeverageDownParams calldata params) external {
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L40), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L123)

```solidity
File: src/transformers/V3Utils.sol

98: 		    function executeWithPermit(uint256 tokenId, Instructions memory instructions, uint8 v, bytes32 r, bytes32 s)

115: 		    function execute(uint256 tokenId, Instructions memory instructions) public returns (uint256 newTokenId) {

356: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)

397: 		    function swap(SwapParams calldata params) external payable returns (uint256 amountOut) {

467: 		    function swapAndMint(SwapAndMintParams calldata params)

532: 		    function swapAndIncreaseLiquidity(SwapAndIncreaseLiquidityParams calldata params)

566: 		    function _prepareAddApproved(

598: 		    function _prepareAddPermit2(

653: 		    function _prepareAdd(

705: 		    function _swapAndMint(SwapAndMintParams memory params, bool unwrap)

735: 		    function _swapAndIncrease(SwapAndIncreaseLiquidityParams memory params, IERC20 token0, IERC20 token1, bool unwrap)

779: 		    function _swapAndPrepareAmounts(SwapAndMintParams memory params, bool unwrap)

841: 		    function _returnLeftoverTokens(

864: 		    function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {

877: 		    function _decreaseLiquidity(

892: 		    function _collectFees(uint256 tokenId, IERC20 token0, IERC20 token1, uint128 collectAmount0, uint128 collectAmount1)

914: 		    receive() external payable {
```

*GitHub* : [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L98), [115](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L115), [356](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L356), [397](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L397), [467](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L467), [532](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L532), [566](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L566), [598](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L598), [653](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L653), [705](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L705), [735](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L735), [779](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L779), [841](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L841), [864](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L864), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L877), [892](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L892), [914](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L914)

```solidity
File: src/utils/FlashloanLiquidator.sol

41: 		    function liquidate(LiquidateParams calldata params) external {

67: 		    function uniswapV3FlashCallback(uint256 fee0, uint256 fee1, bytes calldata callbackData) external {
```

*GitHub* : [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L41), [67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L67)

```solidity
File: src/utils/Swapper.sol

73: 		    function _routerSwap(RouterSwapParams memory params)

132: 		    function _poolSwap(PoolSwapParams memory params) internal returns (uint256 amountInDelta, uint256 amountOutDelta) {

156: 		    function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external override {

171: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L73), [132](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L132), [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L156), [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L171)

### [N-95]<a name="n-95"></a> Missing NatSpec `@notice` from function declaration

Some functions have an incomplete NatSpec: add a `@notice` notation to describe the function to improve the code documentation.

*There are 66 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

133: 		    function _checkPoolPrice(address token0, address token1, uint24 fee, uint256 derivedPoolPriceX96) internal view {

139: 		    function _requireMaxDifference(uint256 priceX96, uint256 verifyPriceX96, uint256 maxDifferenceX10000)

272: 		    function _getReferenceTokenPriceX96(address token, uint256 cachedChainlinkReferencePriceX96)

329: 		    function _getChainlinkPriceX96(address token) internal view returns (uint256) {

346: 		    function _getTWAPPriceX96(TokenConfig memory feedConfig) internal view returns (uint256 poolTWAPPriceX96) {

359: 		    function _getReferencePoolPriceX96(IUniswapV3Pool pool, uint32 twapSeconds) internal view returns (uint256) {

395: 		    function _initializeState(uint256 tokenId) internal view returns (PositionState memory state) {

426: 		    function _getAmounts(PositionState memory state)

445: 		    function _getUncollectedFees(PositionState memory position, int24 tick)

472: 		    function _getFeeGrowthInside(

499: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L133), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L139), [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L272), [329](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L329), [346](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L346), [359](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L359), [395](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L395), [426](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L426), [445](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L445), [472](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L472), [499](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L499)

```solidity
File: src/V3Vault.sol

384: 		    function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

390: 		    function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

609: 		    function decreaseLiquidityAndCollect(DecreaseLiquidityAndCollectParams calldata params)

877: 		    function _deposit(address receiver, uint256 amount, bool isShare, bytes memory permitData)

920: 		    function _withdraw(address receiver, address owner, uint256 amount, bool isShare)

954: 		    function _repay(uint256 tokenId, uint256 amount, bool isShare, bytes memory permitData) internal {

1017: 		    function _getAvailableBalance(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96)

1032: 		    function _sendPositionValue(

1077: 		    function _cleanupLoan(uint256 tokenId, uint256 debtExchangeRateX96, uint256 lendExchangeRateX96, address owner)

1090: 		    function _calculateLiquidation(uint256 debt, uint256 fullValue, uint256 collateralValue)

1123: 		    function _handleReserveLiquidation(

1143: 		    function _calculateTokenCollateralFactorX32(uint256 tokenId) internal view returns (uint32) {

1150: 		    function _updateGlobalInterest()

1167: 		    function _calculateGlobalInterest()

1197: 		    function _requireLoanIsHealthy(uint256 tokenId, uint256 debt) internal view {

1205: 		    function _updateAndCheckCollateral(

1246: 		    function _resetDailyLendIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

1258: 		    function _resetDailyDebtIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

1270: 		    function _checkLoanIsHealthy(uint256 tokenId, uint256 debt)

1281: 		    function _convertToShares(uint256 amount, uint256 exchangeRateX96, Math.Rounding rounding)

1289: 		    function _convertToAssets(uint256 shares, uint256 exchangeRateX96, Math.Rounding rounding)

1297: 		    function _addTokenToOwner(address to, uint256 tokenId) internal {

1303: 		    function _removeTokenFromOwner(address from, uint256 tokenId) internal {
```

*GitHub* : [384](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L384), [390](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L390), [609](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L609), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L877), [920](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L920), [954](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L954), [1017](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1017), [1032](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1032), [1077](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1077), [1090](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1090), [1123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1123), [1143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1143), [1150](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1150), [1167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1167), [1197](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1197), [1205](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1205), [1246](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1246), [1258](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1258), [1270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1270), [1281](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1281), [1289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1289), [1297](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1297), [1303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1303)

```solidity
File: src/automators/AutoExit.sol

218: 		    function configToken(uint256 tokenId, PositionConfig calldata config) external {
```

*GitHub* : [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L218)

```solidity
File: src/automators/Automator.sol

139: 		    function _validateSwap(

166: 		    function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

180: 		    function _getTWAPTick(IUniswapV3Pool pool, uint32 twapPeriod) internal view returns (int24, bool) {

193: 		    function _decreaseFullLiquidityAndCollect(

218: 		    function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {

230: 		    function _validateOwner(uint256 tokenId, address vault) internal returns (address owner) {

251: 		    receive() external payable {
```

*GitHub* : [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L139), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L166), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L180), [193](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L193), [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L218), [230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L230), [251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L251)

```solidity
File: src/transformers/AutoCompound.sol

249: 		    function _increaseBalance(uint256 tokenId, address token, uint256 amount) internal {

254: 		    function _setBalance(uint256 tokenId, address token, uint256 amount) internal {

266: 		    function _withdrawBalanceInternal(uint256 tokenId, address token, address to, uint256 balance, uint256 amount)

276: 		    function _checkApprovals(address token0, address token1) internal {
```

*GitHub* : [249](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L249), [254](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L254), [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L266), [276](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L276)

```solidity
File: src/transformers/AutoRange.sol

276: 		    function configToken(uint256 tokenId, address vault, PositionConfig calldata config) external {

300: 		    function _getTickSpacing(uint24 fee) internal view returns (int24) {
```

*GitHub* : [276](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L276), [300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L300)

```solidity
File: src/transformers/LeverageTransformer.sol

40: 		    function leverageUp(LeverageUpParams calldata params) external {

123: 		    function leverageDown(LeverageDownParams calldata params) external {
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L40), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L123)

```solidity
File: src/transformers/V3Utils.sol

566: 		    function _prepareAddApproved(

598: 		    function _prepareAddPermit2(

653: 		    function _prepareAdd(

705: 		    function _swapAndMint(SwapAndMintParams memory params, bool unwrap)

735: 		    function _swapAndIncrease(SwapAndIncreaseLiquidityParams memory params, IERC20 token0, IERC20 token1, bool unwrap)

779: 		    function _swapAndPrepareAmounts(SwapAndMintParams memory params, bool unwrap)

841: 		    function _returnLeftoverTokens(

864: 		    function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {

877: 		    function _decreaseLiquidity(

892: 		    function _collectFees(uint256 tokenId, IERC20 token0, IERC20 token1, uint128 collectAmount0, uint128 collectAmount1)

914: 		    receive() external payable {
```

*GitHub* : [566](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L566), [598](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L598), [653](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L653), [705](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L705), [735](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L735), [779](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L779), [841](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L841), [864](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L864), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L877), [892](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L892), [914](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L914)

```solidity
File: src/utils/FlashloanLiquidator.sol

67: 		    function uniswapV3FlashCallback(uint256 fee0, uint256 fee1, bytes calldata callbackData) external {
```

*GitHub* : [67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L67)

```solidity
File: src/utils/Swapper.sol

73: 		    function _routerSwap(RouterSwapParams memory params)

132: 		    function _poolSwap(PoolSwapParams memory params) internal returns (uint256 amountInDelta, uint256 amountOutDelta) {

156: 		    function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external override {

171: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L73), [132](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L132), [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L156), [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L171)

### [N-96]<a name="n-96"></a> Missing NatSpec `@param` from function declaration

Some functions have an incomplete NatSpec: add a `@param` notation to describe the function parameters to improve the code documentation.

*There are 75 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

// @audit missing token0, token1, fee, derivedPoolPriceX96
133: 		    function _checkPoolPrice(address token0, address token1, uint24 fee, uint256 derivedPoolPriceX96) internal view {

// @audit missing priceX96, verifyPriceX96, maxDifferenceX10000
139: 		    function _requireMaxDifference(uint256 priceX96, uint256 verifyPriceX96, uint256 maxDifferenceX10000)

// @audit missing token, cachedChainlinkReferencePriceX96
272: 		    function _getReferenceTokenPriceX96(address token, uint256 cachedChainlinkReferencePriceX96)

// @audit missing token
329: 		    function _getChainlinkPriceX96(address token) internal view returns (uint256) {

// @audit missing feedConfig
346: 		    function _getTWAPPriceX96(TokenConfig memory feedConfig) internal view returns (uint256 poolTWAPPriceX96) {

// @audit missing pool, twapSeconds
359: 		    function _getReferencePoolPriceX96(IUniswapV3Pool pool, uint32 twapSeconds) internal view returns (uint256) {

// @audit missing tokenId
395: 		    function _initializeState(uint256 tokenId) internal view returns (PositionState memory state) {

// @audit missing state
426: 		    function _getAmounts(PositionState memory state)

// @audit missing position, tick
445: 		    function _getUncollectedFees(PositionState memory position, int24 tick)

// @audit missing pool, tickLower, tickUpper, tickCurrent, feeGrowthGlobal0X128, feeGrowthGlobal1X128
472: 		    function _getFeeGrowthInside(

// @audit missing tokenA, tokenB, fee
499: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [133](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L133), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L139), [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L272), [329](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L329), [346](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L346), [359](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L359), [395](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L395), [426](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L426), [445](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L445), [472](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L472), [499](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L499)

```solidity
File: src/V3Vault.sol

195: 		    function vaultInfo()

// @audit missing assets, receiver, permitData
384: 		    function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

// @audit missing shares, receiver, permitData
390: 		    function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

// @audit missing r, s
410: 		    function createWithPermit(

// @audit missing receiver, amount, isShare, permitData
877: 		    function _deposit(address receiver, uint256 amount, bool isShare, bytes memory permitData)

// @audit missing receiver, owner, amount, isShare
920: 		    function _withdraw(address receiver, address owner, uint256 amount, bool isShare)

// @audit missing tokenId, amount, isShare, permitData
954: 		    function _repay(uint256 tokenId, uint256 amount, bool isShare, bytes memory permitData) internal {

// @audit missing debtExchangeRateX96, lendExchangeRateX96
1017: 		    function _getAvailableBalance(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96)

// @audit missing tokenId, liquidationValue, fullValue, feeValue, recipient
1032: 		    function _sendPositionValue(

// @audit missing tokenId, debtExchangeRateX96, lendExchangeRateX96, owner
1077: 		    function _cleanupLoan(uint256 tokenId, uint256 debtExchangeRateX96, uint256 lendExchangeRateX96, address owner)

// @audit missing debt, fullValue, collateralValue
1090: 		    function _calculateLiquidation(uint256 debt, uint256 fullValue, uint256 collateralValue)

// @audit missing reserveCost, newDebtExchangeRateX96, newLendExchangeRateX96
1123: 		    function _handleReserveLiquidation(

// @audit missing tokenId
1143: 		    function _calculateTokenCollateralFactorX32(uint256 tokenId) internal view returns (uint32) {

1150: 		    function _updateGlobalInterest()

1167: 		    function _calculateGlobalInterest()

// @audit missing tokenId, debt
1197: 		    function _requireLoanIsHealthy(uint256 tokenId, uint256 debt) internal view {

// @audit missing tokenId, debtExchangeRateX96, lendExchangeRateX96, oldShares, newShares
1205: 		    function _updateAndCheckCollateral(

// @audit missing newLendExchangeRateX96, force
1246: 		    function _resetDailyLendIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

// @audit missing newLendExchangeRateX96, force
1258: 		    function _resetDailyDebtIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

// @audit missing tokenId, debt
1270: 		    function _checkLoanIsHealthy(uint256 tokenId, uint256 debt)

// @audit missing amount, exchangeRateX96, rounding
1281: 		    function _convertToShares(uint256 amount, uint256 exchangeRateX96, Math.Rounding rounding)

// @audit missing shares, exchangeRateX96, rounding
1289: 		    function _convertToAssets(uint256 shares, uint256 exchangeRateX96, Math.Rounding rounding)

// @audit missing to, tokenId
1297: 		    function _addTokenToOwner(address to, uint256 tokenId) internal {

// @audit missing from, tokenId
1303: 		    function _removeTokenFromOwner(address from, uint256 tokenId) internal {
```

*GitHub* : [195](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L195), [384](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L384), [390](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L390), [410](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L410), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L877), [920](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L920), [954](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L954), [1017](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1017), [1032](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1032), [1077](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1077), [1090](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1090), [1123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1123), [1143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1143), [1150](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1150), [1167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1167), [1197](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1197), [1205](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1205), [1246](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1246), [1258](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1258), [1270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1270), [1281](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1281), [1289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1289), [1297](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1297), [1303](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1303)

```solidity
File: src/automators/AutoExit.sol

// @audit missing params
100: 		    function execute(ExecuteParams calldata params) external {

// @audit missing tokenId, config
218: 		    function configToken(uint256 tokenId, PositionConfig calldata config) external {
```

*GitHub* : [100](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L100), [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L218)

```solidity
File: src/automators/Automator.sol

// @audit missing _maxTWAPTickDifference, _TWAPSeconds
87: 		    function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {

// @audit missing swap0For1, amountIn, pool, twapPeriod, maxTickDifference, maxPriceDifferenceX64
139: 		    function _validateSwap(

// @audit missing pool, twapPeriod, currentTick, maxDifference
166: 		    function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

// @audit missing pool, twapPeriod
180: 		    function _getTWAPTick(IUniswapV3Pool pool, uint32 twapPeriod) internal view returns (int24, bool) {

// @audit missing tokenId, liquidity, amountRemoveMin0, amountRemoveMin1, deadline
193: 		    function _decreaseFullLiquidityAndCollect(

// @audit missing to, token, amount, unwrap
218: 		    function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {

// @audit missing tokenId, vault
230: 		    function _validateOwner(uint256 tokenId, address vault) internal returns (address owner) {

251: 		    receive() external payable {
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L87), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L139), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L166), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L180), [193](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L193), [218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L218), [230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L230), [251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L251)

```solidity
File: src/transformers/AutoCompound.sol

// @audit missing params, vault
87: 		    function executeWithVault(ExecuteParams calldata params, address vault) external {

// @audit missing params
101: 		    function execute(ExecuteParams calldata params) external nonReentrant {

// @audit missing tokenId, token, amount
249: 		    function _increaseBalance(uint256 tokenId, address token, uint256 amount) internal {

// @audit missing tokenId, token, amount
254: 		    function _setBalance(uint256 tokenId, address token, uint256 amount) internal {

// @audit missing tokenId, token, to, balance, amount
266: 		    function _withdrawBalanceInternal(uint256 tokenId, address token, address to, uint256 balance, uint256 amount)

// @audit missing token0, token1
276: 		    function _checkApprovals(address token0, address token1) internal {
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L87), [101](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L101), [249](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L249), [254](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L254), [266](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L266), [276](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L276)

```solidity
File: src/transformers/AutoRange.sol

// @audit missing params, vault
97: 		    function executeWithVault(ExecuteParams calldata params, address vault) external {

// @audit missing params
111: 		    function execute(ExecuteParams calldata params) external {

// @audit missing tokenId, vault, config
276: 		    function configToken(uint256 tokenId, address vault, PositionConfig calldata config) external {

// @audit missing fee
300: 		    function _getTickSpacing(uint24 fee) internal view returns (int24) {
```

*GitHub* : [97](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L97), [276](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L276), [300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L300), [111](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L111)

```solidity
File: src/transformers/LeverageTransformer.sol

// @audit missing params
40: 		    function leverageUp(LeverageUpParams calldata params) external {

// @audit missing params
123: 		    function leverageDown(LeverageDownParams calldata params) external {
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L40), [123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L123)

```solidity
File: src/transformers/V3Utils.sol

// @audit missing from, tokenId, data
356: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)

// @audit missing token0, token1, otherToken, amount0, amount1, amountOther
566: 		    function _prepareAddApproved(

// @audit missing token0, token1, otherToken, amount0, amount1, amountOther, permit, signature
598: 		    function _prepareAddPermit2(

// @audit missing token0, token1, otherToken, amount0, amount1, amountOther
653: 		    function _prepareAdd(

// @audit missing params, unwrap
705: 		    function _swapAndMint(SwapAndMintParams memory params, bool unwrap)

// @audit missing params, token0, token1, unwrap
735: 		    function _swapAndIncrease(SwapAndIncreaseLiquidityParams memory params, IERC20 token0, IERC20 token1, bool unwrap)

// @audit missing params, unwrap
779: 		    function _swapAndPrepareAmounts(SwapAndMintParams memory params, bool unwrap)

// @audit missing to, token0, token1, total0, total1, added0, added1, unwrap
841: 		    function _returnLeftoverTokens(

// @audit missing to, token, amount, unwrap
864: 		    function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {

// @audit missing tokenId, liquidity, deadline, token0Min, token1Min
877: 		    function _decreaseLiquidity(

// @audit missing tokenId, token0, token1, collectAmount0, collectAmount1
892: 		    function _collectFees(uint256 tokenId, IERC20 token0, IERC20 token1, uint128 collectAmount0, uint128 collectAmount1)

914: 		    receive() external payable {
```

*GitHub* : [864](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L864), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L877), [892](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L892), [356](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L356), [914](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L914), [735](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L735), [705](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L705), [653](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L653), [598](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L598), [566](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L566), [841](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L841), [779](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L779)

```solidity
File: src/utils/FlashloanLiquidator.sol

// @audit missing params
41: 		    function liquidate(LiquidateParams calldata params) external {

// @audit missing fee0, fee1, callbackData
67: 		    function uniswapV3FlashCallback(uint256 fee0, uint256 fee1, bytes calldata callbackData) external {
```

*GitHub* : [67](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L67), [41](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L41)

```solidity
File: src/utils/Swapper.sol

// @audit missing params
73: 		    function _routerSwap(RouterSwapParams memory params)

// @audit missing params
132: 		    function _poolSwap(PoolSwapParams memory params) internal returns (uint256 amountInDelta, uint256 amountOutDelta) {

// @audit missing amount0Delta, amount1Delta, data
156: 		    function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external override {

// @audit missing tokenA, tokenB, fee
171: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L73), [132](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L132), [156](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L156), [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L171)

### [N-97]<a name="n-97"></a> Incomplete NatSpec `@return` from function declaration

Some functions have an incomplete NatSpec: add a `@return` notation to describe the function return value to improve the code documentation.

*There are 46 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

272: 		    function _getReferenceTokenPriceX96(address token, uint256 cachedChainlinkReferencePriceX96)

329: 		    function _getChainlinkPriceX96(address token) internal view returns (uint256) {

346: 		    function _getTWAPPriceX96(TokenConfig memory feedConfig) internal view returns (uint256 poolTWAPPriceX96) {

359: 		    function _getReferencePoolPriceX96(IUniswapV3Pool pool, uint32 twapSeconds) internal view returns (uint256) {

395: 		    function _initializeState(uint256 tokenId) internal view returns (PositionState memory state) {

426: 		    function _getAmounts(PositionState memory state)

445: 		    function _getUncollectedFees(PositionState memory position, int24 tick)

472: 		    function _getFeeGrowthInside(

499: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [426](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L426), [445](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L445), [472](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L472), [395](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L395), [329](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L329), [346](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L346), [499](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L499), [359](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L359), [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L272)

```solidity
File: src/V3Vault.sol

264: 		    function loanCount(address owner) external view override returns (uint256) {

271: 		    function loanAtIndex(address owner, uint256 index) external view override returns (uint256) {

384: 		    function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

390: 		    function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

877: 		    function _deposit(address receiver, uint256 amount, bool isShare, bytes memory permitData)

920: 		    function _withdraw(address receiver, address owner, uint256 amount, bool isShare)

1017: 		    function _getAvailableBalance(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96)

1032: 		    function _sendPositionValue(

1090: 		    function _calculateLiquidation(uint256 debt, uint256 fullValue, uint256 collateralValue)

1123: 		    function _handleReserveLiquidation(

1143: 		    function _calculateTokenCollateralFactorX32(uint256 tokenId) internal view returns (uint32) {

1150: 		    function _updateGlobalInterest()

1167: 		    function _calculateGlobalInterest()

1270: 		    function _checkLoanIsHealthy(uint256 tokenId, uint256 debt)

1281: 		    function _convertToShares(uint256 amount, uint256 exchangeRateX96, Math.Rounding rounding)

1289: 		    function _convertToAssets(uint256 shares, uint256 exchangeRateX96, Math.Rounding rounding)
```

*GitHub* : [271](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L271), [264](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L264), [384](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L384), [390](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L390), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L877), [920](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L920), [1017](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1017), [1032](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1032), [1090](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1090), [1123](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1123), [1143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1143), [1150](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1150), [1167](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1167), [1270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1270), [1281](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1281), [1289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1289)

```solidity
File: src/automators/Automator.sol

139: 		    function _validateSwap(

166: 		    function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

180: 		    function _getTWAPTick(IUniswapV3Pool pool, uint32 twapPeriod) internal view returns (int24, bool) {

193: 		    function _decreaseFullLiquidityAndCollect(

230: 		    function _validateOwner(uint256 tokenId, address vault) internal returns (address owner) {
```

*GitHub* : [193](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L193), [230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L230), [180](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L180), [166](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L166), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L139)

```solidity
File: src/transformers/AutoRange.sol

300: 		    function _getTickSpacing(uint24 fee) internal view returns (int24) {
```

*GitHub* : [300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L300)

```solidity
File: src/transformers/V3Utils.sol

98: 		    function executeWithPermit(uint256 tokenId, Instructions memory instructions, uint8 v, bytes32 r, bytes32 s)

115: 		    function execute(uint256 tokenId, Instructions memory instructions) public returns (uint256 newTokenId) {

356: 		    function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)

397: 		    function swap(SwapParams calldata params) external payable returns (uint256 amountOut) {

467: 		    function swapAndMint(SwapAndMintParams calldata params)

532: 		    function swapAndIncreaseLiquidity(SwapAndIncreaseLiquidityParams calldata params)

653: 		    function _prepareAdd(

705: 		    function _swapAndMint(SwapAndMintParams memory params, bool unwrap)

735: 		    function _swapAndIncrease(SwapAndIncreaseLiquidityParams memory params, IERC20 token0, IERC20 token1, bool unwrap)

779: 		    function _swapAndPrepareAmounts(SwapAndMintParams memory params, bool unwrap)

877: 		    function _decreaseLiquidity(

892: 		    function _collectFees(uint256 tokenId, IERC20 token0, IERC20 token1, uint128 collectAmount0, uint128 collectAmount1)
```

*GitHub* : [397](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L397), [467](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L467), [532](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L532), [653](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L653), [705](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L705), [735](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L735), [779](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L779), [877](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L877), [892](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L892), [356](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L356), [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L98), [115](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L115)

```solidity
File: src/utils/Swapper.sol

73: 		    function _routerSwap(RouterSwapParams memory params)

132: 		    function _poolSwap(PoolSwapParams memory params) internal returns (uint256 amountInDelta, uint256 amountOutDelta) {

171: 		    function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {
```

*GitHub* : [132](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L132), [73](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L73), [171](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/Swapper.sol#L171)

### Disputed Risk Issues

### [D-01]<a name="d-01"></a> Return values of `approve` not checked

The rule is valid for some ERC20, but these instances contain either non-ERC20 or ERC20 that do not have this issue.

*There are 2 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit not an ERC-20
520: 		        nonfungiblePositionManager.approve(transformer, tokenId);

// @audit not an ERC-20
537: 		        nonfungiblePositionManager.approve(address(0), tokenId);
```

*GitHub* : [537](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L537), [520](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L520)

### [D-02]<a name="d-02"></a> `approve` can revert if the current approval is not zero

The rule is valid for some ERC20, but these instances contain either non-ERC20 or ERC20 that do not have this issue.

*There are 2 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit not an ERC-20
520: 		        nonfungiblePositionManager.approve(transformer, tokenId);

// @audit not an ERC-20
537: 		        nonfungiblePositionManager.approve(address(0), tokenId);
```

*GitHub* : [537](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L537), [520](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L520)

### [D-03]<a name="d-03"></a> Some functions do not work correctly with fee-on-transfer tokens

The rule is valid for some ERC20, but these instances contain either non-ERC20 or ERC20 that do not have this issue.

*There are 16 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit not an ERC-20
401: 		        nonfungiblePositionManager.safeTransferFrom(msg.sender, address(this), tokenId, abi.encode(recipient));

// @audit not an ERC-20
424: 		        nonfungiblePositionManager.safeTransferFrom(owner, address(this), tokenId, abi.encode(recipient));

// @audit not an ERC-20
720: 		            permit2.permitTransferFrom(
721: 		                permit,
722: 		                ISignatureTransfer.SignatureTransferDetails(address(this), state.liquidatorCost),
723: 		                msg.sender,
724: 		                signature
725: 		            );

// @audit not an ERC-20
722: 		                ISignatureTransfer.SignatureTransferDetails(address(this), state.liquidatorCost),

// @audit not an ERC-20
896: 		            permit2.permitTransferFrom(
897: 		                permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature
898: 		            );

// @audit not an ERC-20
897: 		                permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature

// @audit not an ERC-20
981: 		                permit2.permitTransferFrom(
982: 		                    permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature
983: 		                );

// @audit not an ERC-20
982: 		                    permit, ISignatureTransfer.SignatureTransferDetails(address(this), assets), msg.sender, signature

// @audit not an ERC-20
1083: 		        nonfungiblePositionManager.safeTransferFrom(address(this), owner, tokenId);
```

*GitHub* : [720-725](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L720-L725), [401](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L401), [424](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L424), [722](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L722), [896-898](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L896-L898), [897](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L897), [981-983](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L981-L983), [982](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L982), [1083](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1083)

```solidity
File: src/transformers/AutoRange.sol

// @audit not an ERC-20
232: 		            nonfungiblePositionManager.safeTransferFrom(address(this), state.owner, state.newTokenId);
```

*GitHub* : [232](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L232)

```solidity
File: src/transformers/V3Utils.sol

// @audit not an ERC-20
376: 		        nonfungiblePositionManager.safeTransferFrom(address(this), from, tokenId, instructions.returnData);

// @audit not an ERC-20
619: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed0);

// @audit not an ERC-20
623: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed1);

// @audit not an ERC-20
627: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.neededOther);

// @audit not an ERC-20
631: 		        permit2.permitTransferFrom(permit, transferDetails, msg.sender, signature);

// @audit not an ERC-20
727: 		        nonfungiblePositionManager.safeTransferFrom(address(this), params.recipientNFT, tokenId, params.returnData);
```

*GitHub* : [631](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L631), [619](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L619), [623](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L623), [727](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L727), [627](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L627), [376](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L376)

### [D-04]<a name="d-04"></a> Enum values should be used in place of constant array indexes

The following instances are not numbers and thus they are invalid.

*There are 112 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

240: 		        feedConfigs[token] = config;

259: 		        feedConfigs[token].mode = mode;

281: 		        TokenConfig memory feedConfig = feedConfigs[token];

334: 		        TokenConfig memory feedConfig = feedConfigs[token];
```

*GitHub* : [281](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L281), [334](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L334), [240](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L240), [259](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L259)

```solidity
File: src/V3Vault.sol

245: 		        debt = _convertToAssets(loans[tokenId].debtShares, newDebtExchangeRateX96, Math.Rounding.Up);

259: 		        return tokenOwner[tokenId];

265: 		        return ownedTokens[owner].length;

272: 		        return ownedTokens[owner][index];

272: 		        return ownedTokens[owner][index];

446: 		            loans[tokenId] = Loan(0);

455: 		                address owner = tokenOwner[oldTokenId];

461: 		                loans[tokenId] = Loan(loans[oldTokenId].debtShares);

461: 		                loans[tokenId] = Loan(loans[oldTokenId].debtShares);

471: 		                    tokenId, debtExchangeRateX96, lendExchangeRateX96, 0, loans[tokenId].debtShares

484: 		        if (tokenOwner[tokenId] != msg.sender) {

487: 		        transformApprovals[msg.sender][tokenId][target] = isActive;

487: 		        transformApprovals[msg.sender][tokenId][target] = isActive;

487: 		        transformApprovals[msg.sender][tokenId][target] = isActive;

502: 		        if (tokenId == 0 || !transformerAllowList[transformer]) {

512: 		        address loanOwner = tokenOwner[tokenId];

515: 		        if (loanOwner != msg.sender && !transformApprovals[loanOwner][tokenId][msg.sender]) {

515: 		        if (loanOwner != msg.sender && !transformApprovals[loanOwner][tokenId][msg.sender]) {

515: 		        if (loanOwner != msg.sender && !transformApprovals[loanOwner][tokenId][msg.sender]) {

539: 		        uint256 debt = _convertToAssets(loans[tokenId].debtShares, newDebtExchangeRateX96, Math.Rounding.Up);

552: 		            transformedTokenId > 0 && transformedTokenId == tokenId && transformerAllowList[msg.sender];

558: 		        Loan storage loan = loans[tokenId];

561: 		        if (!isTransformMode && tokenOwner[tokenId] != msg.sender && address(this) != msg.sender) {

595: 		        address owner = tokenOwner[tokenId];

619: 		        address owner = tokenOwner[params.tokenId];

642: 		        uint256 debt = _convertToAssets(loans[params.tokenId].debtShares, newDebtExchangeRateX96, Math.Rounding.Up);

695: 		        uint256 debtShares = loans[params.tokenId].debtShares;

741: 		        address owner = tokenOwner[params.tokenId];

797: 		        transformerAllowList[transformer] = active;

863: 		        tokenConfigs[token].collateralFactorX32 = collateralFactorX32;

864: 		        tokenConfigs[token].collateralValueLimitFactorX32 = collateralValueLimitFactorX32;

957: 		        Loan storage loan = loans[tokenId];

1001: 		        address owner = tokenOwner[tokenId];

1081: 		        _updateAndCheckCollateral(tokenId, debtExchangeRateX96, lendExchangeRateX96, loans[tokenId].debtShares, 0);

1082: 		        delete loans[tokenId];

1145: 		        uint32 factor0X32 = tokenConfigs[token0].collateralFactorX32;

1146: 		        uint32 factor1X32 = tokenConfigs[token1].collateralFactorX32;

1217: 		                tokenConfigs[token0].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);

1218: 		                tokenConfigs[token1].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);

1220: 		                tokenConfigs[token0].totalDebtShares += SafeCast.toUint192(newShares - oldShares);

1221: 		                tokenConfigs[token1].totalDebtShares += SafeCast.toUint192(newShares - oldShares);

1226: 		                uint256 collateralValueLimitFactorX32 = tokenConfigs[token0].collateralValueLimitFactorX32;

1229: 		                        && _convertToAssets(tokenConfigs[token0].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)

1234: 		                collateralValueLimitFactorX32 = tokenConfigs[token1].collateralValueLimitFactorX32;

1237: 		                        && _convertToAssets(tokenConfigs[token1].totalDebtShares, debtExchangeRateX96, Math.Rounding.Up)

1298: 		        ownedTokensIndex[tokenId] = ownedTokens[to].length;

1298: 		        ownedTokensIndex[tokenId] = ownedTokens[to].length;

1299: 		        ownedTokens[to].push(tokenId);

1300: 		        tokenOwner[tokenId] = to;

1304: 		        uint256 lastTokenIndex = ownedTokens[from].length - 1;

1305: 		        uint256 tokenIndex = ownedTokensIndex[tokenId];

1307: 		            uint256 lastTokenId = ownedTokens[from][lastTokenIndex];

1307: 		            uint256 lastTokenId = ownedTokens[from][lastTokenIndex];

1308: 		            ownedTokens[from][tokenIndex] = lastTokenId;

1308: 		            ownedTokens[from][tokenIndex] = lastTokenId;

1309: 		            ownedTokensIndex[lastTokenId] = tokenIndex;

1311: 		        ownedTokens[from].pop();

1313: 		        delete tokenOwner[tokenId]; // Remove the token from the token owner mapping
```

*GitHub* : [484](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L484), [487](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L487), [487](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L487), [487](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L487), [502](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L502), [512](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L512), [515](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L515), [515](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L515), [515](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L515), [539](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L539), [552](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L552), [558](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L558), [561](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L561), [595](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L595), [619](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L619), [642](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L642), [695](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L695), [741](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L741), [797](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L797), [863](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L863), [864](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L864), [957](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L957), [1001](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1001), [1081](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1081), [1082](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1082), [1145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1145), [1146](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1146), [1217](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1217), [1218](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1218), [1220](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1220), [1221](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1221), [1226](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1226), [1229](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1229), [1234](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1234), [1237](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1237), [1298](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1298), [1298](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1298), [1299](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1299), [1300](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1300), [1304](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1304), [1305](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1305), [1307](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1307), [1307](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1307), [1308](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1308), [1309](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1309), [1311](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1311), [1313](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1313), [1308](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L1308), [245](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L245), [259](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L259), [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L265), [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L272), [272](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L272), [446](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L446), [455](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L455), [461](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L461), [461](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L461), [471](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L471)

```solidity
File: src/automators/AutoExit.sol

101: 		        if (!operators[msg.sender]) {

106: 		        PositionConfig memory config = positionConfigs[params.tokenId];

207: 		        delete positionConfigs[params.tokenId];

230: 		        positionConfigs[tokenId] = config;
```

*GitHub* : [230](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L230), [207](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L207), [106](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L106), [101](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L101)

```solidity
File: src/automators/Automator.sol

71: 		        operators[_operator] = _active;

81: 		        vaults[_vault] = _active;

112: 		            uint256 balance = IERC20(tokens[i]).balanceOf(address(this));

114: 		                _transferToken(to, IERC20(tokens[i]), balance, true);

232: 		        if (vaults[msg.sender]) {

237: 		            if (!vaults[vault]) {
```

*GitHub* : [232](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L232), [71](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L71), [237](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L237), [81](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L81), [112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L112), [114](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L114)

```solidity
File: src/transformers/AutoCompound.sol

88: 		        if (!operators[msg.sender] || !vaults[vault]) {

88: 		        if (!operators[msg.sender] || !vaults[vault]) {

102: 		        if (!operators[msg.sender] && !vaults[msg.sender]) {

102: 		        if (!operators[msg.sender] && !vaults[msg.sender]) {

119: 		        state.amount0 = state.amount0 + positionBalances[params.tokenId][state.token0];

119: 		        state.amount0 = state.amount0 + positionBalances[params.tokenId][state.token0];

120: 		        state.amount1 = state.amount1 + positionBalances[params.tokenId][state.token1];

120: 		        state.amount1 = state.amount1 + positionBalances[params.tokenId][state.token1];

202: 		        if (vaults[owner]) {

211: 		        uint256 balance0 = positionBalances[tokenId][token0];

211: 		        uint256 balance0 = positionBalances[tokenId][token0];

215: 		        uint256 balance1 = positionBalances[tokenId][token1];

215: 		        uint256 balance1 = positionBalances[tokenId][token1];

234: 		            uint256 balance = positionBalances[0][tokens[i]];

234: 		            uint256 balance = positionBalances[0][tokens[i]];

235: 		            _withdrawBalanceInternal(0, tokens[i], to, balance, balance);

250: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] + amount;

250: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] + amount;

250: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] + amount;

250: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] + amount;

255: 		        uint256 currentBalance = positionBalances[tokenId][token];

255: 		        uint256 currentBalance = positionBalances[tokenId][token];

257: 		            positionBalances[tokenId][token] = amount;

257: 		            positionBalances[tokenId][token] = amount;

270: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] - amount;

270: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] - amount;

270: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] - amount;

270: 		        positionBalances[tokenId][token] = positionBalances[tokenId][token] - amount;
```

*GitHub* : [257](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L257), [88](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L88), [88](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L88), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L102), [102](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L102), [119](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L119), [119](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L119), [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L120), [120](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L120), [202](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L202), [211](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L211), [211](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L211), [215](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L215), [215](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L215), [234](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L234), [234](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L234), [235](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L235), [250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L250), [250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L250), [250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L250), [250](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L250), [255](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L255), [255](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L255), [257](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L257), [270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L270), [270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L270), [270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L270), [270](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L270)

```solidity
File: src/transformers/AutoRange.sol

98: 		        if (!operators[msg.sender] || !vaults[vault]) {

98: 		        if (!operators[msg.sender] || !vaults[vault]) {

112: 		        if (!operators[msg.sender] && !vaults[msg.sender]) {

112: 		        if (!operators[msg.sender] && !vaults[msg.sender]) {

116: 		        PositionConfig memory config = positionConfigs[params.tokenId];

227: 		            if (vaults[state.owner]) {

251: 		            positionConfigs[state.newTokenId] = config;

265: 		            delete positionConfigs[params.tokenId];

284: 		        positionConfigs[tokenId] = config;
```

*GitHub* : [112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L112), [227](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L227), [251](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L251), [265](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L265), [284](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L284), [116](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L116), [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L98), [98](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L98), [112](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L112)

```solidity
File: src/transformers/V3Utils.sol

619: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed0);

623: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed1);

627: 		            transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.neededOther);
```

*GitHub* : [627](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L627), [623](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L623), [619](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L619)

### [D-05]<a name="d-05"></a> Time related variables should use time units instead of numbers

The following instances do not indicate time, or they already use time units, and thus they are invalid.

*There are 15 instance(s) of this issue:*

```solidity
File: src/V3Oracle.sol

25: 		    uint16 public constant MIN_PRICE_DIFFERENCE = 200; //2%
```

*GitHub* : [25](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L25)

```solidity
File: src/V3Vault.sol

118: 		    uint32 public reserveFactorX32 = 0;

124: 		    uint256 public debtSharesTotal = 0;

127: 		    uint256 public lastExchangeRateUpdate = 0;

131: 		    uint256 public globalDebtLimit = 0;

132: 		    uint256 public globalLendLimit = 0;

135: 		    uint256 public minLoanSize = 0;

138: 		    uint256 public dailyLendIncreaseLimitMin = 0;

139: 		    uint256 public dailyLendIncreaseLimitLeft = 0;

140: 		    uint256 public dailyLendIncreaseLimitLastReset = 0;

143: 		    uint256 public dailyDebtIncreaseLimitMin = 0;

144: 		    uint256 public dailyDebtIncreaseLimitLeft = 0;

145: 		    uint256 public dailyDebtIncreaseLimitLastReset = 0;

161: 		    uint256 private transformedTokenId = 0; // transient storage (when available in dencun)
```

*GitHub* : [132](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L132), [135](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L135), [138](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L138), [139](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L139), [140](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L140), [143](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L143), [118](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L118), [145](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L145), [161](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L161), [144](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L144), [124](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L124), [127](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L127), [131](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L131)

```solidity
File: src/automators/Automator.sol

24: 		    uint32 public constant MAX_TWAP_TICK_DIFFERENCE = 200; // 2%
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L24)

### [D-06]<a name="d-06"></a> Upgradeable contract is missing a constructor that disables initialization

The general rule is true, but the following instances are invalid.

*There are 9 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit not upgreadable
11: 		contract InterestRateModel is Ownable, IInterestRateModel, IErrors {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L11)

```solidity
File: src/V3Oracle.sol

// @audit not upgreadable
24: 		contract V3Oracle is IV3Oracle, Ownable, IErrors {
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L24)

```solidity
File: src/V3Vault.sol

// @audit not upgreadable
30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

```solidity
File: src/automators/AutoExit.sol

// @audit not upgreadable
10: 		contract AutoExit is Automator {
```

*GitHub* : [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L10)

```solidity
File: src/transformers/AutoCompound.sol

// @audit not upgreadable
16: 		contract AutoCompound is Automator, Multicall, ReentrancyGuard {
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L16)

```solidity
File: src/transformers/AutoRange.sol

// @audit not upgreadable
11: 		contract AutoRange is Automator {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L11)

```solidity
File: src/transformers/LeverageTransformer.sol

// @audit not upgreadable
12: 		contract LeverageTransformer is Swapper {
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L12)

```solidity
File: src/transformers/V3Utils.sol

// @audit not upgreadable
15: 		contract V3Utils is Swapper, IERC721Receiver {
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L15)

```solidity
File: src/utils/FlashloanLiquidator.sol

// @audit not upgreadable
11: 		contract FlashloanLiquidator is Swapper, IUniswapV3FlashCallback {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L11)

### [D-07]<a name="d-07"></a> Upgradeable contract is missing a gap storage variable

The general rule is true, but the following instances are invalid.

*There are 9 instance(s) of this issue:*

```solidity
File: src/InterestRateModel.sol

// @audit not upgreadable
11: 		contract InterestRateModel is Ownable, IInterestRateModel, IErrors {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/InterestRateModel.sol#L11)

```solidity
File: src/V3Oracle.sol

// @audit not upgreadable
24: 		contract V3Oracle is IV3Oracle, Ownable, IErrors {
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Oracle.sol#L24)

```solidity
File: src/V3Vault.sol

// @audit not upgreadable
30: 		contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {
```

*GitHub* : [30](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L30)

```solidity
File: src/automators/AutoExit.sol

// @audit not upgreadable
10: 		contract AutoExit is Automator {
```

*GitHub* : [10](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/AutoExit.sol#L10)

```solidity
File: src/transformers/AutoCompound.sol

// @audit not upgreadable
16: 		contract AutoCompound is Automator, Multicall, ReentrancyGuard {
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoCompound.sol#L16)

```solidity
File: src/transformers/AutoRange.sol

// @audit not upgreadable
11: 		contract AutoRange is Automator {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/AutoRange.sol#L11)

```solidity
File: src/transformers/LeverageTransformer.sol

// @audit not upgreadable
12: 		contract LeverageTransformer is Swapper {
```

*GitHub* : [12](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/LeverageTransformer.sol#L12)

```solidity
File: src/transformers/V3Utils.sol

// @audit not upgreadable
15: 		contract V3Utils is Swapper, IERC721Receiver {
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/transformers/V3Utils.sol#L15)

```solidity
File: src/utils/FlashloanLiquidator.sol

// @audit not upgreadable
11: 		contract FlashloanLiquidator is Swapper, IUniswapV3FlashCallback {
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/utils/FlashloanLiquidator.sol#L11)

### [D-08]<a name="d-08"></a> `selfbalance()` is cheaper than `address(this).balance`

This issue is not valid, it's actually worse in gas usage. [Proof](https://gist.github.com/DadeKuma/dbe25aafceb14291294449e31b0973c5)

*There are 1 instance(s) of this issue:*

```solidity
File: src/automators/Automator.sol

128: 		        uint256 balance = address(this).balance;
```

*GitHub* : [128](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/automators/Automator.sol#L128)

### [D-09]<a name="d-09"></a> Some functions contain the same exact logic

The general rule is true, but the following instances are invalid.

*There are 2 instance(s) of this issue:*

```solidity
File: src/V3Vault.sol

// @audit overrides an interface
289: 		    function convertToShares(uint256 assets) external view override returns (uint256 shares) {

// @audit overrides an interface
295: 		    function convertToAssets(uint256 shares) external view override returns (uint256 assets) {
```

*GitHub* : [295](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L295), [289](https://github.com/code-423n4/2024-03-revert-lend/blob/ac520c5fedf4e1654c597a46efaf5a7c27295de1/src/V3Vault.sol#L289)

### [D-10]<a name="d-10"></a> Modifier order does not comply with best practices

The general rule is true, but every in-scope function follows the recommended order:

1. Visibility
2. Mutability
3. Virtual
4. Override
5. Custom modifiers

*There are 0 instance(s) of this issue:*

```solidity
File: All in-scope files
```

### [D-11]<a name="d-11"></a> Visibility should be set explicitly rather than defaulting to internal

The general rule is true, but there aren't any variables that use the default visibility.

*There are 0 instance(s) of this issue:*

```solidity
File: All in-scope files
```