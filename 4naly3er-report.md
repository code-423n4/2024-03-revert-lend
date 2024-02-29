# Report

## Gas Optimizations

| |Issue|Instances|
|-|:-|:-:|
| [GAS-1](#GAS-1) | `a = a + b` is more gas effective than `a += b` for state variables (excluding arrays and mappings) | 15 |
| [GAS-2](#GAS-2) | Use assembly to check for `address(0)` | 6 |
| [GAS-3](#GAS-3) | `array[index] += amount` is cheaper than `array[index] = array[index] + amount` (or related variants) | 2 |
| [GAS-4](#GAS-4) | Using bools for storage incurs overhead | 4 |
| [GAS-5](#GAS-5) | State variables should be cached in stack variables rather than re-reading them from storage | 1 |
| [GAS-6](#GAS-6) | Use calldata instead of memory for function arguments that do not get mutated | 2 |
| [GAS-7](#GAS-7) | For Operations that will not overflow, you could use unchecked | 352 |
| [GAS-8](#GAS-8) | Use Custom Errors instead of Revert Strings to save Gas | 2 |
| [GAS-9](#GAS-9) | Avoid contract existence checks by using low level calls | 19 |
| [GAS-10](#GAS-10) | State variables only set in the constructor should be declared `immutable` | 18 |
| [GAS-11](#GAS-11) | Functions guaranteed to revert when called by normal users can be marked `payable` | 12 |
| [GAS-12](#GAS-12) | Using `private` rather than `public` for constants, saves gas | 13 |
| [GAS-13](#GAS-13) | Use shift right/left instead of division/multiplication if possible | 2 |
| [GAS-14](#GAS-14) | Increments/decrements can be unchecked in for-loops | 2 |
| [GAS-15](#GAS-15) | Use != 0 instead of > 0 for unsigned integer comparison | 57 |
| [GAS-16](#GAS-16) | WETH address definition can be use directly | 1 |

### <a name="GAS-1"></a>[GAS-1] `a = a + b` is more gas effective than `a += b` for state variables (excluding arrays and mappings)

This saves **16 gas per instance.**

*Instances (15)*:

```solidity
File: src/V3Oracle.sol

440:         fees0 += state.tokensOwed0;

441:         fees1 += state.tokensOwed1;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

569:         debtSharesTotal += shares;

949:         dailyLendIncreaseLimitLeft += assets;

995:         dailyDebtIncreaseLimitLeft += assets;

1220:                 tokenConfigs[token0].totalDebtShares += SafeCast.toUint192(newShares - oldShares);

1221:                 tokenConfigs[token1].totalDebtShares += SafeCast.toUint192(newShares - oldShares);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

62:             amount0 += amountOut;

74:             amount1 += amountOut;

153:             amount += amountOut;

162:             amount += amountOut;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/transformers/V3Utils.sol

319:                 targetAmount += amountOutDelta;

321:                 targetAmount += amount0;

336:                 targetAmount += amountOutDelta;

338:                 targetAmount += amount1;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

### <a name="GAS-2"></a>[GAS-2] Use assembly to check for `address(0)`

*Saves 6 gas per instance*

*Instances (6)*:

```solidity
File: src/V3Vault.sol

791:             transformer == address(0) || transformer == address(this) || transformer == asset

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

236:         if (vault != address(0)) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/V3Utils.sol

342:             if (targetAmount != 0 && instructions.targetToken != address(0)) {

697:             amountOther > amountAddedOther && address(otherToken) != address(0) && token0 != otherToken

805:         } else if (address(params.swapSourceToken) != address(0)) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/Swapper.sol

77:         if (params.amountIn != 0 && params.swapData.length != 0 && address(params.tokenOut) != address(0)) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="GAS-3"></a>[GAS-3] `array[index] += amount` is cheaper than `array[index] = array[index] + amount` (or related variants)

When updating a value in an array with arithmetic, using `array[index] += amount` is cheaper than `array[index] = array[index] + amount`.

This is because you avoid an additional `mload` when the array is stored in memory, and an `sload` when the array is stored in storage.

This can be applied for any arithmetic operation including `+=`, `-=`,`/=`,`*=`,`^=`,`&=`, `%=`, `<<=`,`>>=`, and `>>>=`.

This optimization can be particularly significant if the pattern occurs during a loop.

*Saves 28 gas for a storage array, 38 for a memory array*

*Instances (2)*:

```solidity
File: src/transformers/AutoCompound.sol

250:         positionBalances[tokenId][token] = positionBalances[tokenId][token] + amount;

270:         positionBalances[tokenId][token] = positionBalances[tokenId][token] - amount;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

### <a name="GAS-4"></a>[GAS-4] Using bools for storage incurs overhead

Use uint256(1) and uint256(2) for true/false to avoid a Gwarmaccess (100 gas), and to avoid Gsset (20000 gas) when changing from ‘false’ to ‘true’, after having been ‘true’ in the past. See [source](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27).

*Instances (4)*:

```solidity
File: src/V3Vault.sol

163:     mapping(address => bool) public transformerAllowList; // contracts allowed to transform positions (selected audited contracts e.g. V3Utils)

164:     mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

34:     mapping(address => bool) public operators;

35:     mapping(address => bool) public vaults;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

### <a name="GAS-5"></a>[GAS-5] State variables should be cached in stack variables rather than re-reading them from storage

The instances below point to the second+ access of a state variable within a function. Caching of a state variable replaces each Gwarmaccess (100 gas) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses.

*Saves 100 gas per instance*

*Instances (1)*:

```solidity
File: src/utils/Swapper.sol

99:                 IUniversalRouter(universalRouter).execute(data.commands, data.inputs, data.deadline);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="GAS-6"></a>[GAS-6] Use calldata instead of memory for function arguments that do not get mutated

When a function with a `memory` array is called externally, the `abi.decode()` step has to use a for-loop to copy each index of the `calldata` to the `memory` index. Each iteration of this for-loop costs at least 60 gas (i.e. `60 * <mem_array>.length`). Using `calldata` directly bypasses this loop.

If the array is passed to an `internal` function which passes the array to another internal function where the array is modified and therefore `memory` is used in the `external` call, it's still more gas-efficient to use `calldata` when the `external` function uses modifiers, since the modifiers may prevent the internal functions from being called. Structs have the same overhead as an array of length one.

 *Saves 60 gas per instance*

*Instances (2)*:

```solidity
File: src/transformers/V3Utils.sol

98:     function executeWithPermit(uint256 tokenId, Instructions memory instructions, uint8 v, bytes32 r, bytes32 s)

115:     function execute(uint256 tokenId, Instructions memory instructions) public returns (uint256 newTokenId) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

### <a name="GAS-7"></a>[GAS-7] For Operations that will not overflow, you could use unchecked

*Instances (352)*:

```solidity
File: src/InterestRateModel.sol

4: import "@openzeppelin/contracts/access/Ownable.sol";

6: import "./interfaces/IInterestRateModel.sol";

7: import "./interfaces/IErrors.sol";

12:     uint256 private constant Q96 = 2 ** 96;

13:     uint256 public constant YEAR_SECS = 31557600; // taking into account leap years

15:     uint256 public constant MAX_BASE_RATE_X96 = Q96 / 10; // 10%

16:     uint256 public constant MAX_MULTIPLIER_X96 = Q96 * 2; // 200%

50:         return debt * Q96 / (cash + debt);

67:             borrowRateX96 = (utilizationRateX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

69:             uint256 normalRateX96 = (kinkX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

70:             uint256 excessUtilX96 = utilizationRateX96 - kinkX96;

71:             borrowRateX96 = (excessUtilX96 * jumpMultiplierPerSecondX96 / Q96) + normalRateX96;

74:         supplyRateX96 = utilizationRateX96 * borrowRateX96 / Q96;

95:         baseRatePerSecondX96 = baseRatePerYearX96 / YEAR_SECS;

96:         multiplierPerSecondX96 = multiplierPerYearX96 / YEAR_SECS;

97:         jumpMultiplierPerSecondX96 = jumpMultiplierPerYearX96 / YEAR_SECS;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

4: import "v3-core/interfaces/IUniswapV3Factory.sol";

5: import "v3-core/interfaces/IUniswapV3Pool.sol";

7: import "v3-core/libraries/TickMath.sol";

9: import "v3-periphery/libraries/PoolAddress.sol";

10: import "v3-periphery/libraries/LiquidityAmounts.sol";

12: import "v3-periphery/interfaces/INonfungiblePositionManager.sol";

14: import "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

15: import "@openzeppelin/contracts/access/Ownable.sol";

17: import "../lib/AggregatorV3Interface.sol";

19: import "./interfaces/IV3Oracle.sol";

20: import "./interfaces/IErrors.sol";

25:     uint16 public constant MIN_PRICE_DIFFERENCE = 200; //2%

27:     uint256 private constant Q96 = 2 ** 96;

28:     uint256 private constant Q128 = 2 ** 128;

37:         CHAINLINK_TWAP_VERIFY, // using chainlink for price and TWAP to verify

38:         TWAP_CHAINLINK_VERIFY, // using TWAP for price and chainlink to verify

39:         CHAINLINK, // using only chainlink directly

40:         TWAP // using TWAP directly

44:         AggregatorV3Interface feed; // chainlink feed

48:         IUniswapV3Pool pool; // reference pool

52:         uint16 maxDifference; // max price difference x10000

65:     uint16 public maxPoolPriceDifference = MIN_PRICE_DIFFERENCE; // max price difference between oracle derived price and pool price x10000

120:         value = (price0X96 * (amount0 + fees0) / Q96 + price1X96 * (amount1 + fees1) / Q96) * Q96 / priceTokenX96;

121:         feeValue = (price0X96 * fees0 / Q96 + price1X96 * fees1 / Q96) * Q96 / priceTokenX96;

122:         price0X96 = price0X96 * Q96 / priceTokenX96;

123:         price1X96 = price1X96 * Q96 / priceTokenX96;

129:         uint256 derivedPoolPriceX96 = price0X96 * Q96 / price1X96;

144:             ? (priceX96 - verifyPriceX96) * 10000 / priceX96

145:             : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;

304:             chainlinkPriceX96 = (10 ** referenceTokenDecimals) * chainlinkPriceX96 * Q96 / chainlinkReferencePriceX96

305:                 / (10 ** feedConfig.tokenDecimals);

338:         if (updatedAt + feedConfig.maxFeedAge < block.timestamp || answer < 0) {

342:         return uint256(answer) * Q96 / (10 ** feedConfig.feedDecimals);

353:             poolTWAPPriceX96 = Q96 * Q96 / priceX96;

366:             secondsAgos[0] = 0; // from (before)

367:             secondsAgos[1] = twapSeconds; // from (before)

368:             (int56[] memory tickCumulatives,) = pool.observe(secondsAgos); // pool observe may fail when there is not enough history available (only use pool with enough history!)

369:             int24 tick = int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapSeconds)));

440:         fees0 += state.tokensOwed0;

441:         fees1 += state.tokensOwed1;

463:             feeGrowth0 = feeGrowthInside0LastX128 - position.feeGrowthInside0LastX128;

464:             feeGrowth1 = feeGrowthInside1LastX128 - position.feeGrowthInside1LastX128;

486:                 feeGrowthInside0X128 = lowerFeeGrowthOutside0X128 - upperFeeGrowthOutside0X128;

487:                 feeGrowthInside1X128 = lowerFeeGrowthOutside1X128 - upperFeeGrowthOutside1X128;

489:                 feeGrowthInside0X128 = feeGrowthGlobal0X128 - lowerFeeGrowthOutside0X128 - upperFeeGrowthOutside0X128;

490:                 feeGrowthInside1X128 = feeGrowthGlobal1X128 - lowerFeeGrowthOutside1X128 - upperFeeGrowthOutside1X128;

492:                 feeGrowthInside0X128 = upperFeeGrowthOutside0X128 - lowerFeeGrowthOutside0X128;

493:                 feeGrowthInside1X128 = upperFeeGrowthOutside1X128 - lowerFeeGrowthOutside1X128;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

4: import "v3-core/interfaces/IUniswapV3Factory.sol";

5: import "v3-core/interfaces/IUniswapV3Pool.sol";

6: import "v3-core/libraries/TickMath.sol";

7: import "v3-core/libraries/FixedPoint128.sol";

9: import "v3-periphery/libraries/LiquidityAmounts.sol";

10: import "v3-periphery/interfaces/INonfungiblePositionManager.sol";

12: import "@openzeppelin/contracts/utils/math/Math.sol";

13: import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

14: import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

15: import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

16: import "@openzeppelin/contracts/access/Ownable.sol";

17: import "@openzeppelin/contracts/utils/math/SafeCast.sol";

18: import "@openzeppelin/contracts/utils/Multicall.sol";

20: import "permit2/interfaces/IPermit2.sol";

22: import "./interfaces/IVault.sol";

23: import "./interfaces/IV3Oracle.sol";

24: import "./interfaces/IInterestRateModel.sol";

25: import "./interfaces/IErrors.sol";

33:     uint256 private constant Q32 = 2 ** 32;

34:     uint256 private constant Q96 = 2 ** 96;

36:     uint32 public constant MAX_COLLATERAL_FACTOR_X32 = uint32(Q32 * 90 / 100); // 90%

38:     uint32 public constant MIN_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 2 / 100); // 2%

39:     uint32 public constant MAX_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 10 / 100); // 10%

41:     uint32 public constant MIN_RESERVE_PROTECTION_FACTOR_X32 = uint32(Q32 / 100); //1%

43:     uint32 public constant MAX_DAILY_LEND_INCREASE_X32 = uint32(Q32 / 10); //10%

44:     uint32 public constant MAX_DAILY_DEBT_INCREASE_X32 = uint32(Q32 / 10); //10%

70:     event Add(uint256 indexed tokenId, address owner, uint256 oldTokenId); // when a token is added replacing another token - oldTokenId > 0

90:     ); // shows exactly how liquidation amounts were divided

110:         uint32 collateralFactorX32; // how much this token is valued as collateral

111:         uint32 collateralValueLimitFactorX32; // how much asset equivalent may be lent out given this collateral

112:         uint192 totalDebtShares; // how much debt shares are theoretically backed by this collateral

154:     mapping(uint256 => Loan) public loans; // tokenID -> loan mapping

157:     mapping(address => uint256[]) private ownedTokens; // Mapping from owner address to list of owned token IDs

158:     mapping(uint256 => uint256) private ownedTokensIndex; // Mapping from token ID to index of the owner tokens list (for removal without loop)

159:     mapping(uint256 => address) private tokenOwner; // Mapping from token ID to owner

161:     uint256 private transformedTokenId = 0; // transient storage (when available in dencun)

163:     mapping(address => bool) public transformerAllowList; // contracts allowed to transform positions (selected audited contracts e.g. V3Utils)

164:     mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)

307:             return globalLendLimit - value;

318:             return _convertToShares(globalLendLimit - value, lendExchangeRateX96, Math.Rounding.Down);

567:         uint256 loanDebtShares = loan.debtShares + shares;

569:         debtSharesTotal += shares;

577:             dailyDebtIncreaseLimitLeft -= assets;

581:             tokenId, newDebtExchangeRateX96, newLendExchangeRateX96, loanDebtShares - shares, loanDebtShares

636:             params.feeAmount0 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount0 + params.feeAmount0),

637:             params.feeAmount1 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount1 + params.feeAmount1)

731:         debtSharesTotal -= debtShares;

769:             _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up) * reserveProtectionFactorX32 / Q32;

771:         uint256 unprotected = reserves > protected ? reserves - protected : 0;

913:             dailyLendIncreaseLimitLeft -= assets;

949:         dailyLendIncreaseLimitLeft += assets;

990:         uint256 loanDebtShares = loan.debtShares - shares;

992:         debtSharesTotal -= shares;

995:         dailyDebtIncreaseLimitLeft += assets;

998:             tokenId, newDebtExchangeRateX96, newLendExchangeRateX96, loanDebtShares + shares, loanDebtShares

1027:         reserves = balance + debt > lent ? balance + debt - lent : 0;

1028:         available = balance > reserves ? balance - reserves : 0;

1054:                 fees0 = uint128(liquidationValue * fees0 / feeValue);

1055:                 fees1 = uint128(liquidationValue * fees1 / feeValue);

1060:                 liquidity = uint128((liquidationValue - feeValue) * liquidity / (fullValue - feeValue));

1100:         uint256 maxPenaltyValue = debt * (Q32 + MAX_LIQUIDATION_PENALTY_X32) / Q32;

1105:             uint256 startLiquidationValue = debt * fullValue / collateralValue;

1107:                 (Q96 - ((fullValue - maxPenaltyValue) * Q96 / (startLiquidationValue - maxPenaltyValue)));

1109:                 + (MAX_LIQUIDATION_PENALTY_X32 - MIN_LIQUIDATION_PENALTY_X32) * penaltyFractionX96 / Q96;

1111:             liquidationValue = debt * (Q32 + penaltyX32) / Q32;

1116:             uint256 penaltyValue = fullValue * (Q32 - MAX_LIQUIDATION_PENALTY_X32) / Q32;

1118:             reserveCost = debt - penaltyValue;

1132:             missing = reserveCost - reserves;

1137:             newLendExchangeRateX96 = (totalLent - missing) * newLendExchangeRateX96 / totalLent;

1181:         supplyRateX96 = supplyRateX96.mulDiv(Q32 - reserveFactorX32, Q32);

1188:                 + oldDebtExchangeRateX96 * (block.timestamp - lastRateUpdate) * borrowRateX96 / Q96;

1190:                 + oldLendExchangeRateX96 * (block.timestamp - lastRateUpdate) * supplyRateX96 / Q96;

1217:                 tokenConfigs[token0].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);

1218:                 tokenConfigs[token1].totalDebtShares -= SafeCast.toUint192(oldShares - newShares);

1220:                 tokenConfigs[token0].totalDebtShares += SafeCast.toUint192(newShares - oldShares);

1221:                 tokenConfigs[token1].totalDebtShares += SafeCast.toUint192(newShares - oldShares);

1230:                             > lentAssets * collateralValueLimitFactorX32 / Q32

1238:                             > lentAssets * collateralValueLimitFactorX32 / Q32

1248:         uint256 time = block.timestamp / 1 days;

1260:         uint256 time = block.timestamp / 1 days;

1304:         uint256 lastTokenIndex = ownedTokens[from].length - 1;

1313:         delete tokenOwner[tokenId]; // Remove the token from the token owner mapping

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

4: import "./Automator.sol";

45:         bool isActive; // if position is active

50:         int24 token0TriggerTick; // when tick is below this one

51:         int24 token1TriggerTick; // when tick is equal or above this one

53:         uint64 token0SlippageX64; // when token 0 is swapped to token 1

54:         uint64 token1SlippageX64; // when token 1 is swapped to token 0

55:         bool onlyFees; // if only fees maybe used for protocol reward

56:         uint64 maxRewardX64; // max allowed reward percentage of fees or full position

64:         uint256 tokenId; // tokenid to process

65:         bytes swapData; // if its a swap order - must include swap data

66:         uint128 liquidity; // liquidity the calculations are based on

67:         uint256 amountRemoveMin0; // min amount to be removed from liquidity

68:         uint256 amountRemoveMin1; // min amount to be removed from liquidity

69:         uint256 deadline; // for uniswap operations - operator promises fair value

70:         uint64 rewardX64; // which reward will be used for protocol, can be max configured amount (considering onlyFees)

155:                 state.amount0 -= state.feeAmount0 * params.rewardX64 / Q64;

156:                 state.amount1 -= state.feeAmount1 * params.rewardX64 / Q64;

181:             state.amount0 = state.isAbove ? state.amount0 + state.amountOutDelta : state.amount0 - state.amountInDelta;

182:             state.amount1 = state.isAbove ? state.amount1 - state.amountInDelta : state.amount1 + state.amountOutDelta;

187:                     state.amount0 -= state.amount0 * params.rewardX64 / Q64;

189:                     state.amount1 -= state.amount1 * params.rewardX64 / Q64;

194:             state.amount0 -= (config.onlyFees ? state.feeAmount0 : state.amount0) * params.rewardX64 / Q64;

195:             state.amount1 -= (config.onlyFees ? state.feeAmount1 : state.amount1) * params.rewardX64 / Q64;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/automators/Automator.sol

4: import "@openzeppelin/contracts/access/Ownable.sol";

5: import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

6: import "@openzeppelin/contracts/utils/math/SafeCast.sol";

8: import "v3-core/interfaces/IUniswapV3Factory.sol";

9: import "v3-core/interfaces/IUniswapV3Pool.sol";

10: import "v3-core/libraries/TickMath.sol";

11: import "v3-core/libraries/FullMath.sol";

13: import "v3-periphery/interfaces/INonfungiblePositionManager.sol";

14: import "v3-periphery/interfaces/external/IWETH9.sol";

16: import "../utils/Swapper.sol";

17: import "../interfaces/IVault.sol";

20:     uint256 internal constant Q64 = 2 ** 64;

21:     uint256 internal constant Q96 = 2 ** 96;

23:     uint32 public constant MIN_TWAP_SECONDS = 60; // 1 minute

24:     uint32 public constant MAX_TWAP_TICK_DIFFERENCE = 200; // 2%

111:         for (; i < count; ++i) {

158:             amountOutMin = FullMath.mulDiv(amountIn * (Q64 - maxPriceDifferenceX64), priceX96, Q96 * Q64);

160:             amountOutMin = FullMath.mulDiv(amountIn * (Q64 - maxPriceDifferenceX64), Q96, priceX96 * Q64);

173:             return twapTick - currentTick >= -int16(maxDifference) && twapTick - currentTick <= int16(maxDifference);

182:         secondsAgos[0] = 0; // from (before)

183:         secondsAgos[1] = twapPeriod; // from (before)

187:             return (int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapPeriod))), true);

213:         feeAmount0 = amount0 - feeAmount0;

214:         feeAmount1 = amount1 - feeAmount1;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

4: import "@openzeppelin/contracts/security/ReentrancyGuard.sol";

5: import "@openzeppelin/contracts/utils/Multicall.sol";

6: import "@openzeppelin/contracts/utils/math/SafeMath.sol";

8: import "v3-periphery/interfaces/INonfungiblePositionManager.sol";

10: import "../automators/Automator.sol";

47:     uint64 public constant MAX_REWARD_X64 = uint64(Q64 / 50); // 2%

48:     uint64 public totalRewardX64 = MAX_REWARD_X64; // 2%

119:         state.amount0 = state.amount0 + positionBalances[params.tokenId][state.token0];

120:         state.amount1 = state.amount1 + positionBalances[params.tokenId][state.token1];

148:                         params.swap0To1 ? state.amount0 - state.amountInDelta : state.amount0 + state.amountOutDelta;

150:                         params.swap0To1 ? state.amount1 + state.amountOutDelta : state.amount1 - state.amountInDelta;

156:             state.maxAddAmount0 = state.amount0 * Q64 / (rewardX64 + Q64);

157:             state.maxAddAmount1 = state.amount1 * Q64 / (rewardX64 + Q64);

170:                 state.amount0Fees = state.compounded0 * rewardX64 / Q64;

171:                 state.amount1Fees = state.compounded1 * rewardX64 / Q64;

175:             _setBalance(params.tokenId, state.token0, state.amount0 - state.compounded0 - state.amount0Fees);

176:             _setBalance(params.tokenId, state.token1, state.amount1 - state.compounded1 - state.amount1Fees);

233:         for (; i < count; ++i) {

250:         positionBalances[tokenId][token] = positionBalances[tokenId][token] + amount;

259:                 emit BalanceAdded(tokenId, token, amount - currentBalance);

261:                 emit BalanceRemoved(tokenId, token, currentBalance - amount);

270:         positionBalances[tokenId][token] = positionBalances[tokenId][token] - amount;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

4: import "../automators/Automator.sol";

39:         int32 lowerTickLimit; // if negative also in-range positions may be adjusted / if 0 out of range positions may be adjusted

40:         int32 upperTickLimit; // if negative also in-range positions may be adjusted / if 0 out of range positions may be adjusted

41:         int32 lowerTickDelta; // this amount is added to current tick (floored to tickspacing) to define lowerTick of new position

42:         int32 upperTickDelta; // this amount is added to current tick (floored to tickspacing) to define upperTick of new position

43:         uint64 token0SlippageX64; // max price difference from current pool price for swap / Q64 for token0

44:         uint64 token1SlippageX64; // max price difference from current pool price for swap / Q64 for token1

45:         bool onlyFees; // if only fees maybe used for protocol reward

46:         uint64 maxRewardX64; // max allowed reward percentage of fees or full position

56:         uint256 amountIn; // if this is set to 0 no swap happens

58:         uint128 liquidity; // liquidity the calculations are based on

59:         uint256 amountRemoveMin0; // min amount to be removed from liquidity

60:         uint256 amountRemoveMin1; // min amount to be removed from liquidity

61:         uint256 deadline; // for uniswap operations - operator promises fair value

62:         uint64 rewardX64; // which reward will be used for protocol, can be max configured amount (considering onlyFees)

143:             state.protocolReward0 = state.feeAmount0 * params.rewardX64 / Q64;

144:             state.protocolReward1 = state.feeAmount1 * params.rewardX64 / Q64;

145:             state.amount0 -= state.protocolReward0;

146:             state.amount1 -= state.protocolReward1;

167:             state.currentTick < state.tickLower - config.lowerTickLimit

168:                 || state.currentTick >= state.tickUpper + config.upperTickLimit

171:             int24 baseTick = state.currentTick - (((state.currentTick % tickSpacing) + tickSpacing) % tickSpacing);

175:                 baseTick + config.lowerTickDelta == state.tickLower

176:                     && baseTick + config.upperTickDelta == state.tickUpper

191:             state.amount0 = params.swap0To1 ? state.amount0 - state.amountInDelta : state.amount0 + state.amountOutDelta;

192:             state.amount1 = params.swap0To1 ? state.amount1 + state.amountOutDelta : state.amount1 - state.amountInDelta;

195:             state.maxAddAmount0 = config.onlyFees ? state.amount0 : state.amount0 * Q64 / (params.rewardX64 + Q64);

196:             state.maxAddAmount1 = config.onlyFees ? state.amount1 : state.amount1 * Q64 / (params.rewardX64 + Q64);

202:                 SafeCast.toInt24(baseTick + config.lowerTickDelta), // reverts if out of valid range

203:                 SafeCast.toInt24(baseTick + config.upperTickDelta), // reverts if out of valid range

208:                 address(this), // is sent to real recipient aftwards

236:                 state.protocolReward0 = state.amountAdded0 * params.rewardX64 / Q64;

237:                 state.protocolReward1 = state.amountAdded1 * params.rewardX64 / Q64;

238:                 state.amount0 -= state.protocolReward0;

239:                 state.amount1 -= state.protocolReward1;

243:             if (state.amount0 - state.amountAdded0 > 0) {

244:                 _transferToken(state.realOwner, IERC20(state.token0), state.amount0 - state.amountAdded0, true);

246:             if (state.amount1 - state.amountAdded1 > 0) {

247:                 _transferToken(state.realOwner, IERC20(state.token1), state.amount1 - state.amountAdded1, true);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

4: import "@openzeppelin/contracts/utils/math/SafeCast.sol";

5: import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

7: import "../utils/Swapper.sol";

8: import "../interfaces/IVault.sol";

25:         bytes swapData0; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

29:         bytes swapData1; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

59:                 amount1 -= amountIn;

61:             amount -= amountIn;

62:             amount0 += amountOut;

71:                 amount0 -= amountIn;

73:             amount -= amountIn;

74:             amount1 += amountOut;

88:             SafeERC20.safeTransfer(IERC20(token0), params.recipient, amount0 - added0);

91:             SafeERC20.safeTransfer(IERC20(token1), params.recipient, amount1 - added1);

111:         bytes swapData0; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

115:         bytes swapData1; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

139:             params.feeAmount0 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount0 + params.feeAmount0),

140:             params.feeAmount1 == type(uint128).max ? type(uint128).max : SafeCast.toUint128(amount1 + params.feeAmount1)

152:             amount0 -= amountIn;

153:             amount += amountOut;

161:             amount1 -= amountIn;

162:             amount += amountOut;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/transformers/V3Utils.sol

4: import "@openzeppelin/contracts/token/ERC721/IERC721Receiver.sol";

5: import "@openzeppelin/contracts/utils/math/SafeCast.sol";

7: import "permit2/interfaces/IPermit2.sol";

9: import "../utils/Swapper.sol";

60:         bytes swapData0; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

65:         bytes swapData1; // encoded data from 0x api call (address,bytes) - allowanceTarget,data

135:                 : (amount0 + instructions.feeAmount0).toUint128(),

138:                 : (amount1 + instructions.feeAmount1).toUint128()

317:                     _transferToken(instructions.recipient, IERC20(token0), amount0 - amountInDelta, instructions.unwrap);

319:                 targetAmount += amountOutDelta;

321:                 targetAmount += amount0;

334:                     _transferToken(instructions.recipient, IERC20(token1), amount1 - amountInDelta, instructions.unwrap);

336:                 targetAmount += amountOutDelta;

338:                 targetAmount += amount1;

387:         address recipient; // recipient of tokenOut and leftover tokenIn (if any leftover)

389:         bool unwrap; // if tokenIn or tokenOut is WETH - unwrap

390:         bytes permitData; // if permit2 signatures are used - set this

425:         uint256 leftOver = params.amountIn - amountInDelta;

441:         address recipient; // recipient of leftover tokens

442:         address recipientNFT; // recipient of nft

485:                 params.amountIn0 + params.amountIn1,

496:                 params.amountIn0 + params.amountIn1

509:         address recipient; // recipient of leftover tokens

548:                 params.amountIn0 + params.amountIn1,

559:                 params.amountIn0 + params.amountIn1

619:             transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed0);

623:             transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.needed1);

627:             transferDetails[state.i++] = ISignatureTransfer.SignatureTransferDetails(address(this), state.neededOther);

635:             if (token0.balanceOf(address(this)) - state.balanceBefore0 != state.needed0) {

636:                 revert TransferError(); // reverts for fee-on-transfer tokens

640:             if (token1.balanceOf(address(this)) - state.balanceBefore1 != state.needed1) {

641:                 revert TransferError(); // reverts for fee-on-transfer tokens

645:             if (otherToken.balanceOf(address(this)) - state.balanceBeforeOther != state.neededOther) {

646:                 revert TransferError(); // reverts for fee-on-transfer tokens

691:             needed0 = amount0 - amountAdded0;

694:             needed1 = amount1 - amountAdded1;

700:             neededOther = amountOther - amountAddedOther;

721:             address(this), // is sent to real recipient aftwards

792:             total0 = params.amount0 - amountInDelta;

793:             total1 = params.amount1 + amountOutDelta;

803:             total1 = params.amount1 - amountInDelta;

804:             total0 = params.amount0 + amountOutDelta;

816:             total0 = params.amount0 + amountOutDelta0;

817:             total1 = params.amount1 + amountOutDelta1;

820:             uint256 leftOver = params.amountIn0 + params.amountIn1 - amountInDelta0 - amountInDelta1;

851:         uint256 left0 = total0 - added0;

852:         uint256 left1 = total1 - added1;

905:         if (balanceAfter0 - balanceBefore0 != amount0) {

908:         if (balanceAfter1 - balanceBefore1 != amount1) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

4: import "v3-core/interfaces/IUniswapV3Pool.sol";

5: import "v3-core/interfaces/callback/IUniswapV3FlashCallback.sol";

7: import "../interfaces/IVault.sol";

8: import "./Swapper.sol";

29:         uint256 tokenId; // loan to liquidate

30:         uint256 debtShares; // debt shares calculation is based on

31:         IVault vault; // vault where the loan is

32:         IUniswapV3Pool flashLoanPool; // pool which is used for flashloan - may not be used in the swaps below

33:         uint256 amount0In; // how much of token0 to swap to asset (0 if no swap should be done)

34:         bytes swapData0; // swap data for token0 swap

35:         uint256 amount1In; // how much of token1 to swap to asset (0 if no swap should be done)

36:         bytes swapData1; // swap data for token1 swap

37:         uint256 minReward; // min reward amount (works as a global slippage control for complete operation)

85:         SafeERC20.safeTransfer(data.asset, msg.sender, data.liquidationCost + (fee0 + fee1));

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

```solidity
File: src/utils/Swapper.sol

4: import "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";

6: import "v3-core/interfaces/callback/IUniswapV3SwapCallback.sol";

7: import "v3-core/interfaces/IUniswapV3Pool.sol";

8: import "v3-core/libraries/TickMath.sol";

10: import "v3-periphery/interfaces/INonfungiblePositionManager.sol";

11: import "v3-periphery/interfaces/external/IWETH9.sol";

13: import "../../lib/IUniversalRouter.sol";

14: import "../interfaces/IErrors.sol";

107:             amountInDelta = balanceInBefore - balanceInAfter;

108:             amountOutDelta = balanceOutAfter - balanceOutBefore;

138:                 (params.swap0For1 ? TickMath.MIN_SQRT_RATIO + 1 : TickMath.MAX_SQRT_RATIO - 1),

146:             amountOutDelta = params.swap0For1 ? uint256(-amount1Delta) : uint256(-amount0Delta);

157:         require(amount0Delta > 0 || amount1Delta > 0); // swaps entirely within 0-liquidity regions are not supported

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="GAS-8"></a>[GAS-8] Use Custom Errors instead of Revert Strings to save Gas

Custom errors are available from solidity version 0.8.4. Custom errors save [**~50 gas**](https://gist.github.com/IllIllI000/ad1bd0d29a0101b25e57c293b4b0c746) each time they're hit by [avoiding having to allocate and store the revert string](https://blog.soliditylang.org/2021/04/21/custom-errors/#errors-in-depth). Not defining the strings also save deployment gas

Additionally, custom errors can be used inside and outside of contracts (including interfaces and libraries).

Source: <https://blog.soliditylang.org/2021/04/21/custom-errors/>:

> Starting from [Solidity v0.8.4](https://github.com/ethereum/solidity/releases/tag/v0.8.4), there is a convenient and gas-efficient way to explain to users why an operation failed through the use of custom errors. Until now, you could already use strings to give more information about failures (e.g., `revert("Insufficient funds.");`), but they are rather expensive, especially when it comes to deploy cost, and it is difficult to use dynamic information in them.

Consider replacing **all revert strings** with custom errors in the solution, and particularly those that have multiple occurrences:

*Instances (2)*:

```solidity
File: src/transformers/AutoCompound.sol

244:         require(_totalRewardX64 <= totalRewardX64, ">totalRewardX64");

269:         require(amount <= balance, "amount>balance");

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

### <a name="GAS-9"></a>[GAS-9] Avoid contract existence checks by using low level calls

Prior to 0.8.10 the compiler inserted extra code, including `EXTCODESIZE` (**100 gas**), to check for contract existence for external function calls. In more recent solidity versions, the compiler will not insert these checks if the external call has a return value. Similar behavior can be achieved in earlier versions by using low-level calls, since low level calls never check for contract existence

*Instances (19)*:

```solidity
File: src/V3Vault.sol

285:         return IERC20(asset).balanceOf(address(this));

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

112:             uint256 balance = IERC20(tokens[i]).balanceOf(address(this));

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/V3Utils.sol

618:             state.balanceBefore0 = token0.balanceOf(address(this));

622:             state.balanceBefore1 = token1.balanceOf(address(this));

626:             state.balanceBeforeOther = otherToken.balanceOf(address(this));

635:             if (token0.balanceOf(address(this)) - state.balanceBefore0 != state.needed0) {

640:             if (token1.balanceOf(address(this)) - state.balanceBefore1 != state.needed1) {

645:             if (otherToken.balanceOf(address(this)) - state.balanceBeforeOther != state.neededOther) {

896:         uint256 balanceBefore0 = token0.balanceOf(address(this));

897:         uint256 balanceBefore1 = token1.balanceOf(address(this));

901:         uint256 balanceAfter0 = token0.balanceOf(address(this));

902:         uint256 balanceAfter1 = token1.balanceOf(address(this));

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

89:             uint256 balance = data.swap0.tokenIn.balanceOf(address(this));

95:             uint256 balance = data.swap1.tokenIn.balanceOf(address(this));

101:             uint256 balance = data.asset.balanceOf(address(this));

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

```solidity
File: src/utils/Swapper.sol

78:             uint256 balanceInBefore = params.tokenIn.balanceOf(address(this));

79:             uint256 balanceOutBefore = params.tokenOut.balanceOf(address(this));

104:             uint256 balanceInAfter = params.tokenIn.balanceOf(address(this));

105:             uint256 balanceOutAfter = params.tokenOut.balanceOf(address(this));

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="GAS-10"></a>[GAS-10] State variables only set in the constructor should be declared `immutable`

Variables only set in the constructor and never edited afterwards should be marked as immutable, as it would avoid the expensive storage-writing operation in the constructor (around **20 000 gas** per variable) and replace the expensive storage-reading operations (around **2100 gas** per reading) to a less expensive value reading (**3 gas**)

*Instances (18)*:

```solidity
File: src/V3Oracle.sol

79:         nonfungiblePositionManager = _nonfungiblePositionManager;

80:         factory = _nonfungiblePositionManager.factory();

81:         referenceToken = _referenceToken;

82:         referenceTokenDecimals = IERC20Metadata(_referenceToken).decimals();

83:         chainlinkReferenceToken = _chainlinkReferenceToken;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

178:         asset = _asset;

179:         assetDecimals = IERC20Metadata(_asset).decimals();

180:         nonfungiblePositionManager = _nonfungiblePositionManager;

181:         factory = IUniswapV3Factory(_nonfungiblePositionManager.factory());

182:         interestRateModel = _interestRateModel;

183:         oracle = _oracle;

184:         permit2 = _permit2;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/transformers/V3Utils.sol

37:         permit2 = IPermit2(_permit2);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/Swapper.sol

42:         weth = IWETH9(_nonfungiblePositionManager.WETH9());

43:         factory = _nonfungiblePositionManager.factory();

44:         nonfungiblePositionManager = _nonfungiblePositionManager;

45:         zeroxRouter = _zeroxRouter;

46:         universalRouter = _universalRouter;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="GAS-11"></a>[GAS-11] Functions guaranteed to revert when called by normal users can be marked `payable`

If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function. Marking the function as `payable` will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided.

*Instances (12)*:

```solidity
File: src/V3Oracle.sol

185:     function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

265:     function setEmergencyAdmin(address admin) external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

765:     function withdrawReserves(uint256 amount, address receiver) external onlyOwner {

788:     function setTransformer(address transformer, bool active) external onlyOwner {

837:     function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

844:     function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

870:     function setEmergencyAdmin(address admin) external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

59:     function setWithdrawer(address _withdrawer) public onlyOwner {

69:     function setOperator(address _operator, bool _active) public onlyOwner {

79:     function setVault(address _vault, bool _active) public onlyOwner {

87:     function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

243:     function setReward(uint64 _totalRewardX64) external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

### <a name="GAS-12"></a>[GAS-12] Using `private` rather than `public` for constants, saves gas

If needed, the values can be read from the verified contract source code, or if there are multiple values there can be a single getter function that [returns a tuple](https://github.com/code-423n4/2022-08-frax/blob/90f55a9ce4e25bceed3a74290b854341d8de6afa/src/contracts/FraxlendPair.sol#L156-L178) of the values of all currently-public constants. Saves **3406-3606 gas** in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table

*Instances (13)*:

```solidity
File: src/InterestRateModel.sol

13:     uint256 public constant YEAR_SECS = 31557600; // taking into account leap years

15:     uint256 public constant MAX_BASE_RATE_X96 = Q96 / 10; // 10%

16:     uint256 public constant MAX_MULTIPLIER_X96 = Q96 * 2; // 200%

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

25:     uint16 public constant MIN_PRICE_DIFFERENCE = 200; //2%

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

36:     uint32 public constant MAX_COLLATERAL_FACTOR_X32 = uint32(Q32 * 90 / 100); // 90%

38:     uint32 public constant MIN_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 2 / 100); // 2%

39:     uint32 public constant MAX_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 10 / 100); // 10%

41:     uint32 public constant MIN_RESERVE_PROTECTION_FACTOR_X32 = uint32(Q32 / 100); //1%

43:     uint32 public constant MAX_DAILY_LEND_INCREASE_X32 = uint32(Q32 / 10); //10%

44:     uint32 public constant MAX_DAILY_DEBT_INCREASE_X32 = uint32(Q32 / 10); //10%

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

23:     uint32 public constant MIN_TWAP_SECONDS = 60; // 1 minute

24:     uint32 public constant MAX_TWAP_TICK_DIFFERENCE = 200; // 2%

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

47:     uint64 public constant MAX_REWARD_X64 = uint64(Q64 / 50); // 2%

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

### <a name="GAS-13"></a>[GAS-13] Use shift right/left instead of division/multiplication if possible

While the `DIV` / `MUL` opcode uses 5 gas, the `SHR` / `SHL` opcode only uses 3 gas. Furthermore, beware that Solidity's division operation also includes a division-by-0 prevention which is bypassed using shifting. Eventually, overflow checks are never performed for shift operations as they are done for arithmetic operations. Instead, the result is always truncated, so the calculation can be unchecked in Solidity version `0.8+`

- Use `>> 1` instead of `/ 2`
- Use `>> 2` instead of `/ 4`
- Use `<< 3` instead of `* 8`
- ...
- Use `>> 5` instead of `/ 2^5 == / 32`
- Use `<< 6` instead of `* 2^6 == * 64`

TL;DR:

- Shifting left by N is like multiplying by 2^N (Each bits to the left is an increased power of 2)
- Shifting right by N is like dividing by 2^N (Each bits to the right is a decreased power of 2)

*Saves around 2 gas + 20 for unchecked per instance*

*Instances (2)*:

```solidity
File: src/InterestRateModel.sol

16:     uint256 public constant MAX_MULTIPLIER_X96 = Q96 * 2; // 200%

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Vault.sol

38:     uint32 public constant MIN_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 2 / 100); // 2%

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

### <a name="GAS-14"></a>[GAS-14] Increments/decrements can be unchecked in for-loops

In Solidity 0.8+, there's a default overflow check on unsigned integers. It's possible to uncheck this in for-loops and save some gas at each iteration, but at the cost of some code readability, as this uncheck cannot be made inline.

[ethereum/solidity#10695](https://github.com/ethereum/solidity/issues/10695)

The change would be:

```diff
- for (uint256 i; i < numIterations; i++) {
+ for (uint256 i; i < numIterations;) {
 // ...  
+   unchecked { ++i; }
}  
```

These save around **25 gas saved** per instance.

The same can be applied with decrements (which should use `break` when `i == 0`).

The risk of overflow is non-existent for `uint256`.

*Instances (2)*:

```solidity
File: src/automators/Automator.sol

111:         for (; i < count; ++i) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

233:         for (; i < count; ++i) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

### <a name="GAS-15"></a>[GAS-15] Use != 0 instead of > 0 for unsigned integer comparison

*Instances (57)*:

```solidity
File: src/V3Oracle.sol

431:         if (state.liquidity > 0) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

70:     event Add(uint256 indexed tokenId, address owner, uint256 oldTokenId); // when a token is added replacing another token - oldTokenId > 0

443:             if (data.length > 0) {

505:         if (transformedTokenId > 0) {

552:             transformedTokenId > 0 && transformedTokenId == tokenId && transformerAllowList[msg.sender];

615:         if (transformedTokenId > 0) {

687:         if (transformedTokenId > 0) {

712:         if (state.reserveCost > 0) {

717:         if (params.permitData.length > 0) {

737:         if (amount0 < params.amount0Min || amount1 < params.amount1Min) {

778:         if (amount > 0) {

893:         if (permitData.length > 0) {

977:         if (assets > 0) {

978:             if (permitData.length > 0) {

1064:         if (liquidity > 0) {

1186:         if (lastRateUpdate > 0) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

199:         if (state.amount0 > 0) {

202:         if (state.amount1 > 0) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/automators/Automator.sol

113:             if (balance > 0) {

129:         if (balance > 0) {

200:         if (liquidity > 0) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

123:         if (state.amount0 > 0 || state.amount1 > 0) {

127:             if (amountIn > 0) {

133:                 if (tSecs > 0) {

140:                 if (amountIn > 0) {

160:             if (state.maxAddAmount0 > 0 || state.maxAddAmount1 > 0) {

212:         if (balance0 > 0) {

216:         if (balance1 > 0) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

243:             if (state.amount0 - state.amountAdded0 > 0) {

246:             if (state.amount1 - state.amountAdded1 > 0) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

52:         if (params.amountIn0 > 0) {

64:         if (params.amountIn1 > 0) {

93:         if (token != token0 && token != token1 && amount > 0) {

146:         if (params.amountIn0 > 0 && token != token0) {

155:         if (params.amountIn1 > 0 && token != token1) {

169:         if (amount0 > 0 && token != token0) {

172:         if (amount1 > 0 && token != token1) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/transformers/V3Utils.sol

142:         if (amount0 < instructions.amountIn0 || amount1 < instructions.amountIn1) {

402:         if (params.permitData.length > 0) {

476:         if (params.permitData.length > 0) {

539:         if (params.permitData.length > 0) {

577:         if (needed0 > 0) {

580:         if (needed1 > 0) {

583:         if (neededOther > 0) {

617:         if (state.needed0 > 0) {

621:         if (state.needed1 > 0) {

625:         if (state.neededOther > 0) {

634:         if (state.needed0 > 0) {

639:         if (state.needed1 > 0) {

644:         if (state.neededOther > 0) {

784:             if (params.amount0 < params.amountIn1) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

90:             if (balance > 0) {

96:             if (balance > 0) {

105:             if (balance > 0) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

```solidity
File: src/utils/Swapper.sol

133:         if (params.amountIn > 0) {

157:         require(amount0Delta > 0 || amount1Delta > 0); // swaps entirely within 0-liquidity regions are not supported

166:         uint256 amountToPay = amount0Delta > 0 ? uint256(amount0Delta) : uint256(amount1Delta);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="GAS-16"></a>[GAS-16] WETH address definition can be use directly

WETH is a wrap Ether contract with a specific address in the Ethereum network, giving the option to define it may cause false recognition, it is healthier to define it directly.

    Advantages of defining a specific contract directly:
    
    It saves gas,
    Prevents incorrect argument definition,
    Prevents execution on a different chain and re-signature issues,
    WETH Address : 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2

*Instances (1)*:

```solidity
File: src/utils/Swapper.sol

21:     IWETH9 public immutable weth;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

## Non Critical Issues

| |Issue|Instances|
|-|:-|:-:|
| [NC-1](#NC-1) | Replace `abi.encodeWithSignature` and `abi.encodeWithSelector` with `abi.encodeCall` which keeps the code typo/type safe | 2 |
| [NC-2](#NC-2) | Missing checks for `address(0)` when assigning values to address state variables | 6 |
| [NC-3](#NC-3) | Array indices should be referenced via `enum`s rather than via numeric literals | 7 |
| [NC-4](#NC-4) | `constant`s should be defined rather than using magic numbers | 8 |
| [NC-5](#NC-5) | Control structures do not follow the Solidity Style Guide | 65 |
| [NC-6](#NC-6) | Critical Changes Should Use Two-step Procedure | 2 |
| [NC-7](#NC-7) | Consider disabling `renounceOwnership()` | 4 |
| [NC-8](#NC-8) | Event missing indexed field | 20 |
| [NC-9](#NC-9) | Events that mark critical parameter changes should contain both the old and the new value | 17 |
| [NC-10](#NC-10) | Function ordering does not follow the Solidity style guide | 5 |
| [NC-11](#NC-11) | Functions should not be longer than 50 lines | 109 |
| [NC-12](#NC-12) | Lack of checks in setters | 6 |
| [NC-13](#NC-13) | Lines are too long | 2 |
| [NC-14](#NC-14) | NatSpec is completely non-existent on functions that should have them | 8 |
| [NC-15](#NC-15) | Incomplete NatSpec: `@param` is missing on actually documented functions | 9 |
| [NC-16](#NC-16) | Incomplete NatSpec: `@return` is missing on actually documented functions | 6 |
| [NC-17](#NC-17) | Use a `modifier` instead of a `require/if` statement for a special `msg.sender` actor | 26 |
| [NC-18](#NC-18) | Constant state variables defined more than once | 4 |
| [NC-19](#NC-19) | Consider using named mappings | 13 |
| [NC-20](#NC-20) | Adding a `return` statement when the function defines a named return variable, is redundant | 6 |
| [NC-21](#NC-21) | `require()` / `revert()` statements should have descriptive reason strings | 1 |
| [NC-22](#NC-22) | Take advantage of Custom Error's return value property | 102 |
| [NC-23](#NC-23) | Deprecated library used for Solidity `>= 0.8` : SafeMath | 1 |
| [NC-24](#NC-24) | Contract does not follow the Solidity style guide's suggested layout ordering | 11 |
| [NC-25](#NC-25) | Use Underscores for Number Literals (add an underscore every 3 digits) | 5 |
| [NC-26](#NC-26) | Internal and private variables and functions names should begin with an underscore | 4 |
| [NC-27](#NC-27) | Event is missing `indexed` fields | 38 |
| [NC-28](#NC-28) | `public` functions not called by the contract should be declared `external` instead | 2 |
| [NC-29](#NC-29) | Variables need not be initialized to zero | 13 |

### <a name="NC-1"></a>[NC-1] Replace `abi.encodeWithSignature` and `abi.encodeWithSelector` with `abi.encodeCall` which keeps the code typo/type safe

When using `abi.encodeWithSignature`, it is possible to include a typo for the correct function signature.
When using `abi.encodeWithSignature` or `abi.encodeWithSelector`, it is also possible to provide parameters that are not of the correct type for the function.

To avoid these pitfalls, it would be best to use [`abi.encodeCall`](https://solidity-by-example.org/abi-encode/) instead.

*Instances (2)*:

```solidity
File: src/transformers/AutoCompound.sol

92:             params.tokenId, address(this), abi.encodeWithSelector(AutoCompound.execute.selector, params)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

102:             params.tokenId, address(this), abi.encodeWithSelector(AutoRange.execute.selector, params)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

### <a name="NC-2"></a>[NC-2] Missing checks for `address(0)` when assigning values to address state variables

*Instances (6)*:

```solidity
File: src/V3Oracle.sol

81:         referenceToken = _referenceToken;

83:         chainlinkReferenceToken = _chainlinkReferenceToken;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

178:         asset = _asset;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

61:         withdrawer = _withdrawer;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/utils/Swapper.sol

45:         zeroxRouter = _zeroxRouter;

46:         universalRouter = _universalRouter;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="NC-3"></a>[NC-3] Array indices should be referenced via `enum`s rather than via numeric literals

*Instances (7)*:

```solidity
File: src/V3Oracle.sol

366:             secondsAgos[0] = 0; // from (before)

367:             secondsAgos[1] = twapSeconds; // from (before)

369:             int24 tick = int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapSeconds)));

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/automators/Automator.sol

182:         secondsAgos[0] = 0; // from (before)

183:         secondsAgos[1] = twapPeriod; // from (before)

187:             return (int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapPeriod))), true);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

234:             uint256 balance = positionBalances[0][tokens[i]];

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

### <a name="NC-4"></a>[NC-4] `constant`s should be defined rather than using magic numbers

Even [assembly](https://github.com/code-423n4/2022-05-opensea-seaport/blob/9d7ce4d08bf3c3010304a0476a785c70c0e90ae7/contracts/lib/TokenTransferrer.sol#L35-L39) can benefit from using readable constants instead of hex/numeric literals

*Instances (8)*:

```solidity
File: src/V3Oracle.sol

144:             ? (priceX96 - verifyPriceX96) * 10000 / priceX96

145:             : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/transformers/AutoRange.sol

301:         if (fee == 10000) {

302:             return 200;

303:         } else if (fee == 3000) {

304:             return 60;

305:         } else if (fee == 500) {

306:             return 10;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

### <a name="NC-5"></a>[NC-5] Control structures do not follow the Solidity Style Guide

See the [control structures](https://docs.soliditylang.org/en/latest/style-guide.html#control-structures) section of the Solidity Style Guide

*Instances (65)*:

```solidity
File: src/InterestRateModel.sol

88:         if (

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

25:     uint16 public constant MIN_PRICE_DIFFERENCE = 200; //2%

32:     event SetMaxPoolPriceDifference(uint16 maxPoolPriceDifference);

37:         CHAINLINK_TWAP_VERIFY, // using chainlink for price and TWAP to verify

38:         TWAP_CHAINLINK_VERIFY, // using TWAP for price and chainlink to verify

52:         uint16 maxDifference; // max price difference x10000

65:     uint16 public maxPoolPriceDifference = MIN_PRICE_DIFFERENCE; // max price difference between oracle derived price and pool price x10000

136:         _requireMaxDifference(priceX96, derivedPoolPriceX96, maxPoolPriceDifference);

139:     function _requireMaxDifference(uint256 priceX96, uint256 verifyPriceX96, uint256 maxDifferenceX10000)

143:         uint256 differenceX10000 = priceX96 > verifyPriceX96

144:             ? (priceX96 - verifyPriceX96) * 10000 / priceX96

145:             : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;

148:             revert PriceDifferenceExceeded();

189:         maxPoolPriceDifference = _maxPoolPriceDifference;

190:         emit SetMaxPoolPriceDifference(_maxPoolPriceDifference);

208:         uint16 maxDifference

232:                 feed, maxFeedAge, feedDecimals, tokenDecimals, pool, isToken0, twapSeconds, mode, maxDifference

287:         uint256 verifyPriceX96;

290:             feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY

294:             feedConfig.mode == Mode.CHAINLINK_TWAP_VERIFY || feedConfig.mode == Mode.TWAP_CHAINLINK_VERIFY

308:                 verifyPriceX96 = chainlinkPriceX96;

317:                 verifyPriceX96 = twapPriceX96;

324:             _requireMaxDifference(priceX96, verifyPriceX96, feedConfig.maxDifference);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

790:         if (

1227:                 if (

1235:                 if (

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

38:         uint16 _maxTWAPTickDifference,

45:         bool isActive; // if position is active

55:         bool onlyFees; // if only fees maybe used for protocol reward

65:         bytes swapData; // if its a swap order - must include swap data

112:         if (

167:                 maxTWAPTickDifference,

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/automators/Automator.sol

24:     uint32 public constant MAX_TWAP_TICK_DIFFERENCE = 200; // 2%

31:     event TWAPConfigChanged(uint32 TWAPSeconds, uint16 maxTWAPTickDifference);

39:     uint16 public maxTWAPTickDifference;

46:         uint16 _maxTWAPTickDifference,

52:         setTWAPConfig(_maxTWAPTickDifference, _TWAPSeconds);

94:         emit TWAPConfigChanged(_TWAPSeconds, _maxTWAPTickDifference);

96:         maxTWAPTickDifference = _maxTWAPTickDifference;

144:         uint16 maxTickDifference,

145:         uint64 maxPriceDifferenceX64

158:             amountOutMin = FullMath.mulDiv(amountIn * (Q64 - maxPriceDifferenceX64), priceX96, Q96 * Q64);

160:             amountOutMin = FullMath.mulDiv(amountIn * (Q64 - maxPriceDifferenceX64), Q96, priceX96 * Q64);

166:     function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

173:             return twapTick - currentTick >= -int16(maxDifference) && twapTick - currentTick <= int16(maxDifference);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

42:         uint16 _maxTWAPTickDifference

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

30:         uint16 _maxTWAPTickDifference,

39:         int32 lowerTickLimit; // if negative also in-range positions may be adjusted / if 0 out of range positions may be adjusted

40:         int32 upperTickLimit; // if negative also in-range positions may be adjusted / if 0 out of range positions may be adjusted

43:         uint64 token0SlippageX64; // max price difference from current pool price for swap / Q64 for token0

44:         uint64 token1SlippageX64; // max price difference from current pool price for swap / Q64 for token1

45:         bool onlyFees; // if only fees maybe used for protocol reward

56:         uint256 amountIn; // if this is set to 0 no swap happens

122:         if (

162:             maxTWAPTickDifference,

166:         if (

174:             if (

202:                 SafeCast.toInt24(baseTick + config.lowerTickDelta), // reverts if out of valid range

203:                 SafeCast.toInt24(baseTick + config.upperTickDelta), // reverts if out of valid range

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/V3Utils.sol

387:         address recipient; // recipient of tokenOut and leftover tokenIn (if any leftover)

389:         bool unwrap; // if tokenIn or tokenOut is WETH - unwrap

390:         bytes permitData; // if permit2 signatures are used - set this

696:         if (

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

33:         uint256 amount0In; // how much of token0 to swap to asset (0 if no swap should be done)

35:         uint256 amount1In; // how much of token1 to swap to asset (0 if no swap should be done)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

### <a name="NC-6"></a>[NC-6] Critical Changes Should Use Two-step Procedure

The critical procedures should be two step process.

See similar findings in previous Code4rena contests for reference: <https://code4rena.com/reports/2022-06-illuminate/#2-critical-changes-should-use-two-step-procedure>

**Recommended Mitigation Steps**

Lack of two-step procedure for critical operations leaves them error-prone. Consider adding two step procedure on the critical functions.

*Instances (2)*:

```solidity
File: src/V3Oracle.sol

265:     function setEmergencyAdmin(address admin) external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

870:     function setEmergencyAdmin(address admin) external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

### <a name="NC-7"></a>[NC-7] Consider disabling `renounceOwnership()`

If the plan for your project does not include eventually giving up all ownership control, consider overwriting OpenZeppelin's `Ownable`'s `renounceOwnership()` function in order to disable it.

*Instances (4)*:

```solidity
File: src/InterestRateModel.sol

11: contract InterestRateModel is Ownable, IInterestRateModel, IErrors {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

24: contract V3Oracle is IV3Oracle, Ownable, IErrors {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

30: contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

19: abstract contract Automator is Swapper, Ownable {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

### <a name="NC-8"></a>[NC-8] Event missing indexed field

Index event fields make the field more quickly accessible [to off-chain tools](https://ethereum.stackexchange.com/questions/40396/can-somebody-please-explain-the-concept-of-event-indexing) that parse events. This is especially useful when it comes to filtering based on an address. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Where applicable, each `event` should use three `indexed` fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three applicable fields, all of the applicable fields should be indexed.

*Instances (20)*:

```solidity
File: src/InterestRateModel.sol

18:     event SetValues(

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

32:     event SetMaxPoolPriceDifference(uint16 maxPoolPriceDifference);

33:     event SetEmergencyAdmin(address emergencyAdmin);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

73:     event ExchangeRateUpdate(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96);

93:     event WithdrawReserves(uint256 amount, address receiver);

94:     event SetTransformer(address transformer, bool active);

95:     event SetLimits(

102:     event SetReserveFactor(uint32 reserveFactorX32);

103:     event SetReserveProtectionFactor(uint32 reserveProtectionFactorX32);

104:     event SetTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32);

106:     event SetEmergencyAdmin(address emergencyAdmin);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

27:     event OperatorChanged(address newOperator, bool active);

28:     event VaultChanged(address newVault, bool active);

30:     event WithdrawerChanged(address newWithdrawer);

31:     event TWAPConfigChanged(uint32 TWAPSeconds, uint16 maxTWAPTickDifference);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

18:     event AutoCompounded(

30:     event RewardUpdated(address account, uint64 totalRewardX64);

33:     event BalanceAdded(uint256 tokenId, address token, uint256 amount);

34:     event BalanceRemoved(uint256 tokenId, address token, uint256 amount);

35:     event BalanceWithdrawn(uint256 tokenId, address token, address to, uint256 amount);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

### <a name="NC-9"></a>[NC-9] Events that mark critical parameter changes should contain both the old and the new value

This should especially be done if the new value is not required to be different from the old value

*Instances (17)*:

```solidity
File: src/InterestRateModel.sol

82:     function setValues(
            uint256 baseRatePerYearX96,
            uint256 multiplierPerYearX96,
            uint256 jumpMultiplierPerYearX96,
            uint256 _kinkX96
        ) public onlyOwner {
            if (
                baseRatePerYearX96 > MAX_BASE_RATE_X96 || multiplierPerYearX96 > MAX_MULTIPLIER_X96
                    || jumpMultiplierPerYearX96 > MAX_MULTIPLIER_X96
            ) {
                revert InvalidConfig();
            }
    
            baseRatePerSecondX96 = baseRatePerYearX96 / YEAR_SECS;
            multiplierPerSecondX96 = multiplierPerYearX96 / YEAR_SECS;
            jumpMultiplierPerSecondX96 = jumpMultiplierPerYearX96 / YEAR_SECS;
            kinkX96 = _kinkX96;
    
            emit SetValues(baseRatePerYearX96, multiplierPerYearX96, jumpMultiplierPerYearX96, _kinkX96);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

185:     function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {
             if (_maxPoolPriceDifference < MIN_PRICE_DIFFERENCE) {
                 revert InvalidConfig();
             }
             maxPoolPriceDifference = _maxPoolPriceDifference;
             emit SetMaxPoolPriceDifference(_maxPoolPriceDifference);

201:     function setTokenConfig(
             address token,
             AggregatorV3Interface feed,
             uint32 maxFeedAge,
             IUniswapV3Pool pool,
             uint32 twapSeconds,
             Mode mode,
             uint16 maxDifference
         ) external onlyOwner {
             // can not be unset
             if (mode == Mode.NOT_SET) {
                 revert InvalidConfig();
             }
     
             uint8 feedDecimals = feed.decimals();
             uint8 tokenDecimals = IERC20Metadata(token).decimals();
     
             TokenConfig memory config;
     
             if (token != referenceToken) {
                 if (maxDifference < MIN_PRICE_DIFFERENCE) {
                     revert InvalidConfig();
                 }
     
                 address token0 = pool.token0();
                 address token1 = pool.token1();
                 if (!(token0 == token && token1 == referenceToken || token0 == referenceToken && token1 == token)) {
                     revert InvalidPool();
                 }
                 bool isToken0 = token0 == token;
                 config = TokenConfig(
                     feed, maxFeedAge, feedDecimals, tokenDecimals, pool, isToken0, twapSeconds, mode, maxDifference
                 );
             } else {
                 config = TokenConfig(
                     feed, maxFeedAge, feedDecimals, tokenDecimals, IUniswapV3Pool(address(0)), false, 0, Mode.CHAINLINK, 0
                 );
             }
     
             feedConfigs[token] = config;
     
             emit TokenConfigUpdated(token, config);

201:     function setTokenConfig(
             address token,
             AggregatorV3Interface feed,
             uint32 maxFeedAge,
             IUniswapV3Pool pool,
             uint32 twapSeconds,
             Mode mode,
             uint16 maxDifference
         ) external onlyOwner {
             // can not be unset
             if (mode == Mode.NOT_SET) {
                 revert InvalidConfig();
             }
     
             uint8 feedDecimals = feed.decimals();
             uint8 tokenDecimals = IERC20Metadata(token).decimals();
     
             TokenConfig memory config;
     
             if (token != referenceToken) {
                 if (maxDifference < MIN_PRICE_DIFFERENCE) {
                     revert InvalidConfig();
                 }
     
                 address token0 = pool.token0();
                 address token1 = pool.token1();
                 if (!(token0 == token && token1 == referenceToken || token0 == referenceToken && token1 == token)) {
                     revert InvalidPool();
                 }
                 bool isToken0 = token0 == token;
                 config = TokenConfig(
                     feed, maxFeedAge, feedDecimals, tokenDecimals, pool, isToken0, twapSeconds, mode, maxDifference
                 );
             } else {
                 config = TokenConfig(
                     feed, maxFeedAge, feedDecimals, tokenDecimals, IUniswapV3Pool(address(0)), false, 0, Mode.CHAINLINK, 0
                 );
             }
     
             feedConfigs[token] = config;
     
             emit TokenConfigUpdated(token, config);
             emit OracleModeUpdated(token, mode);

249:     function setOracleMode(address token, Mode mode) external {
             if (msg.sender != emergencyAdmin && msg.sender != owner()) {
                 revert Unauthorized();
             }
     
             // can not be unset
             if (mode == Mode.NOT_SET) {
                 revert InvalidConfig();
             }
     
             feedConfigs[token].mode = mode;
             emit OracleModeUpdated(token, mode);

265:     function setEmergencyAdmin(address admin) external onlyOwner {
             emergencyAdmin = admin;
             emit SetEmergencyAdmin(admin);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

788:     function setTransformer(address transformer, bool active) external onlyOwner {
             // protects protocol from owner trying to set dangerous transformer
             if (
                 transformer == address(0) || transformer == address(this) || transformer == asset
                     || transformer == address(nonfungiblePositionManager)
             ) {
                 revert InvalidConfig();
             }
     
             transformerAllowList[transformer] = active;
             emit SetTransformer(transformer, active);

807:     function setLimits(
             uint256 _minLoanSize,
             uint256 _globalLendLimit,
             uint256 _globalDebtLimit,
             uint256 _dailyLendIncreaseLimitMin,
             uint256 _dailyDebtIncreaseLimitMin
         ) external {
             if (msg.sender != emergencyAdmin && msg.sender != owner()) {
                 revert Unauthorized();
             }
     
             minLoanSize = _minLoanSize;
             globalLendLimit = _globalLendLimit;
             globalDebtLimit = _globalDebtLimit;
             dailyLendIncreaseLimitMin = _dailyLendIncreaseLimitMin;
             dailyDebtIncreaseLimitMin = _dailyDebtIncreaseLimitMin;
     
             (, uint256 newLendExchangeRateX96) = _updateGlobalInterest();
     
             // force reset daily limits with new values
             _resetDailyLendIncreaseLimit(newLendExchangeRateX96, true);
             _resetDailyDebtIncreaseLimit(newLendExchangeRateX96, true);
     
             emit SetLimits(

837:     function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {
             reserveFactorX32 = _reserveFactorX32;
             emit SetReserveFactor(_reserveFactorX32);

844:     function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {
             if (_reserveProtectionFactorX32 < MIN_RESERVE_PROTECTION_FACTOR_X32) {
                 revert InvalidConfig();
             }
             reserveProtectionFactorX32 = _reserveProtectionFactorX32;
             emit SetReserveProtectionFactor(_reserveProtectionFactorX32);

856:     function setTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32)
             external
             onlyOwner
         {
             if (collateralFactorX32 > MAX_COLLATERAL_FACTOR_X32) {
                 revert CollateralFactorExceedsMax();
             }
             tokenConfigs[token].collateralFactorX32 = collateralFactorX32;
             tokenConfigs[token].collateralValueLimitFactorX32 = collateralValueLimitFactorX32;
             emit SetTokenConfig(token, collateralFactorX32, collateralValueLimitFactorX32);

870:     function setEmergencyAdmin(address admin) external onlyOwner {
             emergencyAdmin = admin;
             emit SetEmergencyAdmin(admin);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

59:     function setWithdrawer(address _withdrawer) public onlyOwner {
            emit WithdrawerChanged(_withdrawer);

69:     function setOperator(address _operator, bool _active) public onlyOwner {
            emit OperatorChanged(_operator, _active);

79:     function setVault(address _vault, bool _active) public onlyOwner {
            emit VaultChanged(_vault, _active);

87:     function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {
            if (_TWAPSeconds < MIN_TWAP_SECONDS) {
                revert InvalidConfig();
            }
            if (_maxTWAPTickDifference > MAX_TWAP_TICK_DIFFERENCE) {
                revert InvalidConfig();
            }
            emit TWAPConfigChanged(_TWAPSeconds, _maxTWAPTickDifference);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

243:     function setReward(uint64 _totalRewardX64) external onlyOwner {
             require(_totalRewardX64 <= totalRewardX64, ">totalRewardX64");
             totalRewardX64 = _totalRewardX64;
             emit RewardUpdated(msg.sender, _totalRewardX64);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

### <a name="NC-10"></a>[NC-10] Function ordering does not follow the Solidity style guide

According to the [Solidity style guide](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#order-of-functions), functions should be laid out in the following order :`constructor()`, `receive()`, `fallback()`, `external`, `public`, `internal`, `private`, but the cases below do not follow this pattern

*Instances (5)*:

```solidity
File: src/V3Oracle.sol

1: 
   Current order:
   external getValue
   internal _checkPoolPrice
   internal _requireMaxDifference
   public getPositionBreakdown
   external setMaxPoolPriceDifference
   external setTokenConfig
   external setOracleMode
   external setEmergencyAdmin
   internal _getReferenceTokenPriceX96
   internal _getChainlinkPriceX96
   internal _getTWAPPriceX96
   internal _getReferencePoolPriceX96
   internal _initializeState
   internal _getAmounts
   internal _getUncollectedFees
   internal _getFeeGrowthInside
   internal _getPool
   
   Suggested order:
   external getValue
   external setMaxPoolPriceDifference
   external setTokenConfig
   external setOracleMode
   external setEmergencyAdmin
   public getPositionBreakdown
   internal _checkPoolPrice
   internal _requireMaxDifference
   internal _getReferenceTokenPriceX96
   internal _getChainlinkPriceX96
   internal _getTWAPPriceX96
   internal _getReferencePoolPriceX96
   internal _initializeState
   internal _getAmounts
   internal _getUncollectedFees
   internal _getFeeGrowthInside
   internal _getPool

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

1: 
   Current order:
   external vaultInfo
   external lendInfo
   external loanInfo
   external ownerOf
   external loanCount
   external loanAtIndex
   public decimals
   public totalAssets
   external convertToShares
   external convertToAssets
   external maxDeposit
   external maxMint
   external maxWithdraw
   external maxRedeem
   public previewDeposit
   public previewMint
   public previewWithdraw
   public previewRedeem
   external deposit
   external mint
   external withdraw
   external redeem
   external deposit
   external mint
   external create
   external createWithPermit
   external onERC721Received
   external approveTransform
   external transform
   external borrow
   external decreaseLiquidityAndCollect
   external repay
   external repay
   external liquidate
   external withdrawReserves
   external setTransformer
   external setLimits
   external setReserveFactor
   external setReserveProtectionFactor
   external setTokenConfig
   external setEmergencyAdmin
   internal _deposit
   internal _withdraw
   internal _repay
   internal _getAvailableBalance
   internal _sendPositionValue
   internal _cleanupLoan
   internal _calculateLiquidation
   internal _handleReserveLiquidation
   internal _calculateTokenCollateralFactorX32
   internal _updateGlobalInterest
   internal _calculateGlobalInterest
   internal _requireLoanIsHealthy
   internal _updateAndCheckCollateral
   internal _resetDailyLendIncreaseLimit
   internal _resetDailyDebtIncreaseLimit
   internal _checkLoanIsHealthy
   internal _convertToShares
   internal _convertToAssets
   internal _addTokenToOwner
   internal _removeTokenFromOwner
   
   Suggested order:
   external vaultInfo
   external lendInfo
   external loanInfo
   external ownerOf
   external loanCount
   external loanAtIndex
   external convertToShares
   external convertToAssets
   external maxDeposit
   external maxMint
   external maxWithdraw
   external maxRedeem
   external deposit
   external mint
   external withdraw
   external redeem
   external deposit
   external mint
   external create
   external createWithPermit
   external onERC721Received
   external approveTransform
   external transform
   external borrow
   external decreaseLiquidityAndCollect
   external repay
   external repay
   external liquidate
   external withdrawReserves
   external setTransformer
   external setLimits
   external setReserveFactor
   external setReserveProtectionFactor
   external setTokenConfig
   external setEmergencyAdmin
   public decimals
   public totalAssets
   public previewDeposit
   public previewMint
   public previewWithdraw
   public previewRedeem
   internal _deposit
   internal _withdraw
   internal _repay
   internal _getAvailableBalance
   internal _sendPositionValue
   internal _cleanupLoan
   internal _calculateLiquidation
   internal _handleReserveLiquidation
   internal _calculateTokenCollateralFactorX32
   internal _updateGlobalInterest
   internal _calculateGlobalInterest
   internal _requireLoanIsHealthy
   internal _updateAndCheckCollateral
   internal _resetDailyLendIncreaseLimit
   internal _resetDailyDebtIncreaseLimit
   internal _checkLoanIsHealthy
   internal _convertToShares
   internal _convertToAssets
   internal _addTokenToOwner
   internal _removeTokenFromOwner

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

1: 
   Current order:
   public setWithdrawer
   public setOperator
   public setVault
   public setTWAPConfig
   external withdrawBalances
   external withdrawETH
   internal _validateSwap
   internal _hasMaxTWAPTickDifference
   internal _getTWAPTick
   internal _decreaseFullLiquidityAndCollect
   internal _transferToken
   internal _validateOwner
   
   Suggested order:
   external withdrawBalances
   external withdrawETH
   public setWithdrawer
   public setOperator
   public setVault
   public setTWAPConfig
   internal _validateSwap
   internal _hasMaxTWAPTickDifference
   internal _getTWAPTick
   internal _decreaseFullLiquidityAndCollect
   internal _transferToken
   internal _validateOwner

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/V3Utils.sol

1: 
   Current order:
   public executeWithPermit
   public execute
   external onERC721Received
   external swap
   external swapAndMint
   external swapAndIncreaseLiquidity
   internal _prepareAddApproved
   internal _prepareAddPermit2
   internal _prepareAdd
   internal _swapAndMint
   internal _swapAndIncrease
   internal _swapAndPrepareAmounts
   internal _returnLeftoverTokens
   internal _transferToken
   internal _decreaseLiquidity
   internal _collectFees
   
   Suggested order:
   external onERC721Received
   external swap
   external swapAndMint
   external swapAndIncreaseLiquidity
   public executeWithPermit
   public execute
   internal _prepareAddApproved
   internal _prepareAddPermit2
   internal _prepareAdd
   internal _swapAndMint
   internal _swapAndIncrease
   internal _swapAndPrepareAmounts
   internal _returnLeftoverTokens
   internal _transferToken
   internal _decreaseLiquidity
   internal _collectFees

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/Swapper.sol

1: 
   Current order:
   internal _routerSwap
   internal _poolSwap
   external uniswapV3SwapCallback
   internal _getPool
   
   Suggested order:
   external uniswapV3SwapCallback
   internal _routerSwap
   internal _poolSwap
   internal _getPool

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="NC-11"></a>[NC-11] Functions should not be longer than 50 lines

Overly complex code can make understanding functionality more difficult, try to further modularize your code to ensure readability

*Instances (109)*:

```solidity
File: src/InterestRateModel.sol

46:     function getUtilizationRateX96(uint256 cash, uint256 debt) public pure returns (uint256) {

58:     function getRatesPerSecondX96(uint256 cash, uint256 debt)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

133:     function _checkPoolPrice(address token0, address token1, uint24 fee, uint256 derivedPoolPriceX96) internal view {

139:     function _requireMaxDifference(uint256 priceX96, uint256 verifyPriceX96, uint256 maxDifferenceX10000)

185:     function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

249:     function setOracleMode(address token, Mode mode) external {

265:     function setEmergencyAdmin(address admin) external onlyOwner {

272:     function _getReferenceTokenPriceX96(address token, uint256 cachedChainlinkReferencePriceX96)

329:     function _getChainlinkPriceX96(address token) internal view returns (uint256) {

346:     function _getTWAPPriceX96(TokenConfig memory feedConfig) internal view returns (uint256 poolTWAPPriceX96) {

359:     function _getReferencePoolPriceX96(IUniswapV3Pool pool, uint32 twapSeconds) internal view returns (uint256) {

395:     function _initializeState(uint256 tokenId) internal view returns (PositionState memory state) {

445:     function _getUncollectedFees(PositionState memory position, int24 tick)

499:     function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

219:     function lendInfo(address account) external view override returns (uint256 amount) {

258:     function ownerOf(uint256 tokenId) external view override returns (address owner) {

264:     function loanCount(address owner) external view override returns (uint256) {

271:     function loanAtIndex(address owner, uint256 index) external view override returns (uint256) {

277:     function decimals() public view override(IERC20Metadata, ERC20) returns (uint8) {

284:     function totalAssets() public view override returns (uint256) {

289:     function convertToShares(uint256 assets) external view override returns (uint256 shares) {

295:     function convertToAssets(uint256 shares) external view override returns (uint256 assets) {

301:     function maxDeposit(address) external view override returns (uint256) {

312:     function maxMint(address) external view override returns (uint256) {

323:     function maxWithdraw(address owner) external view override returns (uint256) {

329:     function maxRedeem(address owner) external view override returns (uint256) {

334:     function previewDeposit(uint256 assets) public view override returns (uint256) {

340:     function previewMint(uint256 shares) public view override returns (uint256) {

346:     function previewWithdraw(uint256 assets) public view override returns (uint256) {

352:     function previewRedeem(uint256 shares) public view override returns (uint256) {

360:     function deposit(uint256 assets, address receiver) external override returns (uint256) {

366:     function mint(uint256 shares, address receiver) external override returns (uint256) {

372:     function withdraw(uint256 assets, address receiver, address owner) external override returns (uint256) {

378:     function redeem(uint256 shares, address receiver, address owner) external override returns (uint256) {

384:     function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

390:     function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

400:     function create(uint256 tokenId, address recipient) external override {

429:     function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)

483:     function approveTransform(uint256 tokenId, address target, bool isActive) external override {

497:     function transform(uint256 tokenId, address transformer, bytes calldata data)

550:     function borrow(uint256 tokenId, uint256 assets) external override {

609:     function decreaseLiquidityAndCollect(DecreaseLiquidityAndCollectParams calldata params)

652:     function repay(uint256 tokenId, uint256 amount, bool isShare) external override {

661:     function repay(uint256 tokenId, uint256 amount, bool isShare, bytes calldata permitData) external override {

685:     function liquidate(LiquidateParams calldata params) external override returns (uint256 amount0, uint256 amount1) {

765:     function withdrawReserves(uint256 amount, address receiver) external onlyOwner {

788:     function setTransformer(address transformer, bool active) external onlyOwner {

837:     function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

844:     function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

856:     function setTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32)

870:     function setEmergencyAdmin(address admin) external onlyOwner {

877:     function _deposit(address receiver, uint256 amount, bool isShare, bytes memory permitData)

920:     function _withdraw(address receiver, address owner, uint256 amount, bool isShare)

954:     function _repay(uint256 tokenId, uint256 amount, bool isShare, bytes memory permitData) internal {

1017:     function _getAvailableBalance(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96)

1077:     function _cleanupLoan(uint256 tokenId, uint256 debtExchangeRateX96, uint256 lendExchangeRateX96, address owner)

1090:     function _calculateLiquidation(uint256 debt, uint256 fullValue, uint256 collateralValue)

1143:     function _calculateTokenCollateralFactorX32(uint256 tokenId) internal view returns (uint32) {

1197:     function _requireLoanIsHealthy(uint256 tokenId, uint256 debt) internal view {

1246:     function _resetDailyLendIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

1258:     function _resetDailyDebtIncreaseLimit(uint256 newLendExchangeRateX96, bool force) internal {

1270:     function _checkLoanIsHealthy(uint256 tokenId, uint256 debt)

1281:     function _convertToShares(uint256 amount, uint256 exchangeRateX96, Math.Rounding rounding)

1289:     function _convertToAssets(uint256 shares, uint256 exchangeRateX96, Math.Rounding rounding)

1297:     function _addTokenToOwner(address to, uint256 tokenId) internal {

1303:     function _removeTokenFromOwner(address from, uint256 tokenId) internal {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

100:     function execute(ExecuteParams calldata params) external {

218:     function configToken(uint256 tokenId, PositionConfig calldata config) external {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/automators/Automator.sol

59:     function setWithdrawer(address _withdrawer) public onlyOwner {

69:     function setOperator(address _operator, bool _active) public onlyOwner {

79:     function setVault(address _vault, bool _active) public onlyOwner {

87:     function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {

104:     function withdrawBalances(address[] calldata tokens, address to) external virtual {

166:     function _hasMaxTWAPTickDifference(IUniswapV3Pool pool, uint32 twapPeriod, int24 currentTick, uint16 maxDifference)

180:     function _getTWAPTick(IUniswapV3Pool pool, uint32 twapPeriod) internal view returns (int24, bool) {

218:     function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {

230:     function _validateOwner(uint256 tokenId, address vault) internal returns (address owner) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

87:     function executeWithVault(ExecuteParams calldata params, address vault) external {

101:     function execute(ExecuteParams calldata params) external nonReentrant {

200:     function withdrawLeftoverBalances(uint256 tokenId, address to) external nonReentrant {

227:     function withdrawBalances(address[] calldata tokens, address to) external override nonReentrant {

243:     function setReward(uint64 _totalRewardX64) external onlyOwner {

249:     function _increaseBalance(uint256 tokenId, address token, uint256 amount) internal {

254:     function _setBalance(uint256 tokenId, address token, uint256 amount) internal {

266:     function _withdrawBalanceInternal(uint256 tokenId, address token, address to, uint256 balance, uint256 amount)

276:     function _checkApprovals(address token0, address token1) internal {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

97:     function executeWithVault(ExecuteParams calldata params, address vault) external {

111:     function execute(ExecuteParams calldata params) external {

276:     function configToken(uint256 tokenId, address vault, PositionConfig calldata config) external {

300:     function _getTickSpacing(uint24 fee) internal view returns (int24) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

40:     function leverageUp(LeverageUpParams calldata params) external {

123:     function leverageDown(LeverageDownParams calldata params) external {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/transformers/V3Utils.sol

98:     function executeWithPermit(uint256 tokenId, Instructions memory instructions, uint8 v, bytes32 r, bytes32 s)

115:     function execute(uint256 tokenId, Instructions memory instructions) public returns (uint256 newTokenId) {

356:     function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)

397:     function swap(SwapParams calldata params) external payable returns (uint256 amountOut) {

467:     function swapAndMint(SwapAndMintParams calldata params)

532:     function swapAndIncreaseLiquidity(SwapAndIncreaseLiquidityParams calldata params)

705:     function _swapAndMint(SwapAndMintParams memory params, bool unwrap)

735:     function _swapAndIncrease(SwapAndIncreaseLiquidityParams memory params, IERC20 token0, IERC20 token1, bool unwrap)

779:     function _swapAndPrepareAmounts(SwapAndMintParams memory params, bool unwrap)

864:     function _transferToken(address to, IERC20 token, uint256 amount, bool unwrap) internal {

892:     function _collectFees(uint256 tokenId, IERC20 token0, IERC20 token1, uint128 collectAmount0, uint128 collectAmount1)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

41:     function liquidate(LiquidateParams calldata params) external {

67:     function uniswapV3FlashCallback(uint256 fee0, uint256 fee1, bytes calldata callbackData) external {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

```solidity
File: src/utils/Swapper.sol

73:     function _routerSwap(RouterSwapParams memory params)

132:     function _poolSwap(PoolSwapParams memory params) internal returns (uint256 amountInDelta, uint256 amountOutDelta) {

156:     function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external override {

171:     function _getPool(address tokenA, address tokenB, uint24 fee) internal view returns (IUniswapV3Pool) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="NC-12"></a>[NC-12] Lack of checks in setters

Be it sanity checks (like checks against `0`-values) or initial setting checks: it's best for Setter functions to have them

*Instances (6)*:

```solidity
File: src/V3Oracle.sol

265:     function setEmergencyAdmin(address admin) external onlyOwner {
             emergencyAdmin = admin;
             emit SetEmergencyAdmin(admin);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

837:     function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {
             reserveFactorX32 = _reserveFactorX32;
             emit SetReserveFactor(_reserveFactorX32);

870:     function setEmergencyAdmin(address admin) external onlyOwner {
             emergencyAdmin = admin;
             emit SetEmergencyAdmin(admin);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

59:     function setWithdrawer(address _withdrawer) public onlyOwner {
            emit WithdrawerChanged(_withdrawer);
            withdrawer = _withdrawer;

69:     function setOperator(address _operator, bool _active) public onlyOwner {
            emit OperatorChanged(_operator, _active);
            operators[_operator] = _active;

79:     function setVault(address _vault, bool _active) public onlyOwner {
            emit VaultChanged(_vault, _active);
            vaults[_vault] = _active;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

### <a name="NC-13"></a>[NC-13] Lines are too long

Usually lines in source code are limited to [80](https://softwareengineering.stackexchange.com/questions/148677/why-is-80-characters-the-standard-limit-for-code-width) characters. Today's screens are much larger so it's reasonable to stretch this in some cases. Since the files will most likely reside in GitHub, and GitHub starts using a scroll bar in all cases when the length is over [164](https://github.com/aizatto/character-length) characters, the lines below should be split when they reach that length

*Instances (2)*:

```solidity
File: src/V3Oracle.sol

368:             (int56[] memory tickCumulatives,) = pool.observe(secondsAgos); // pool observe may fail when there is not enough history available (only use pool with enough history!)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

164:     mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

### <a name="NC-14"></a>[NC-14] NatSpec is completely non-existent on functions that should have them

Public and external functions that aren't view or pure should have NatSpec comments

*Instances (8)*:

```solidity
File: src/V3Vault.sol

384:     function deposit(uint256 assets, address receiver, bytes calldata permitData) external override returns (uint256) {

390:     function mint(uint256 shares, address receiver, bytes calldata permitData) external override returns (uint256) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

218:     function configToken(uint256 tokenId, PositionConfig calldata config) external {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/transformers/AutoRange.sol

276:     function configToken(uint256 tokenId, address vault, PositionConfig calldata config) external {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

40:     function leverageUp(LeverageUpParams calldata params) external {

123:     function leverageDown(LeverageDownParams calldata params) external {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

67:     function uniswapV3FlashCallback(uint256 fee0, uint256 fee1, bytes calldata callbackData) external {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

```solidity
File: src/utils/Swapper.sol

156:     function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external override {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="NC-15"></a>[NC-15] Incomplete NatSpec: `@param` is missing on actually documented functions

The following functions are missing `@param` NatSpec comments.

*Instances (9)*:

```solidity
File: src/V3Vault.sol

404:     /// @notice Creates a new collateralized position with a permit for token spending (transfer position with permit)
         /// @param tokenId The token ID associated with the new position.
         /// @param owner Current owner of the position (signature owner)
         /// @param recipient Address to recieve the position in the vault
         /// @param deadline Timestamp until which the permit is valid.
         /// @param v, r, s Components of the signature for the permit.
         function createWithPermit(
             uint256 tokenId,
             address owner,
             address recipient,
             uint256 deadline,
             uint8 v,
             bytes32 r,
             bytes32 s

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

95:     /**
         * @notice Handle token (must be in correct state)
         * Can only be called only from configured operator account
         * Swap needs to be done with max price difference from current pool price - otherwise reverts
         */
        function execute(ExecuteParams calldata params) external {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/automators/Automator.sol

84:     /**
         * @notice Owner controlled function to increase TWAPSeconds / decrease maxTWAPTickDifference
         */
        function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

82:     /**
         * @notice Adjust token (which is in a Vault) - via transform method
         * Can only be called from configured operator account - vault must be configured as well
         * Swap needs to be done with max price difference from current pool price - otherwise reverts
         */
        function executeWithVault(ExecuteParams calldata params, address vault) external {

96:     /**
         * @notice Adjust token directly (must be in correct state)
         * Can only be called only from configured operator account, or vault via transform
         * Swap needs to be done with max price difference from current pool price - otherwise reverts
         */
        function execute(ExecuteParams calldata params) external nonReentrant {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

92:     /**
         * @notice Adjust token (which is in a Vault) - via transform method
         * Can only be called from configured operator account - vault must be configured as well
         * Swap needs to be done with max price difference from current pool price - otherwise reverts
         */
        function executeWithVault(ExecuteParams calldata params, address vault) external {

106:     /**
          * @notice Adjust token directly (must be in correct state)
          * Can only be called only from configured operator account, or vault via transform
          * Swap needs to be done with max price difference from current pool price - otherwise reverts
          */
         function execute(ExecuteParams calldata params) external {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/V3Utils.sol

354:     /// @notice ERC721 callback function. Called on safeTransferFrom and does manipulation as configured in encoded Instructions parameter.
         /// At the end the NFT (and any newly minted NFT) is returned to sender. The leftover tokens are sent to instructions.recipient.
         function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

40:     /// @notice Liquidates a loan, using a Uniswap Flashloan
        function liquidate(LiquidateParams calldata params) external {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

### <a name="NC-16"></a>[NC-16] Incomplete NatSpec: `@return` is missing on actually documented functions

The following functions are missing `@return` NatSpec comments.

*Instances (6)*:

```solidity
File: src/transformers/V3Utils.sol

92:     /// @notice Execute instruction with EIP712 permit
        /// @param tokenId Token to process
        /// @param instructions Instructions to execute
        /// @param v Signature values for EIP712 permit
        /// @param r Signature values for EIP712 permit
        /// @param s Signature values for EIP712 permit
        function executeWithPermit(uint256 tokenId, Instructions memory instructions, uint8 v, bytes32 r, bytes32 s)
            public
            returns (uint256 newTokenId)

112:     /// @notice Execute instruction by pulling approved NFT instead of direct safeTransferFrom call from owner
         /// @param tokenId Token to process
         /// @param instructions Instructions to execute
         function execute(uint256 tokenId, Instructions memory instructions) public returns (uint256 newTokenId) {

354:     /// @notice ERC721 callback function. Called on safeTransferFrom and does manipulation as configured in encoded Instructions parameter.
         /// At the end the NFT (and any newly minted NFT) is returned to sender. The leftover tokens are sent to instructions.recipient.
         function onERC721Received(address, address from, uint256 tokenId, bytes calldata data)
             external
             override
             returns (bytes4)

393:     /// @notice Swaps amountIn of tokenIn for tokenOut - returning at least minAmountOut
         /// @param params Swap configuration
         /// If tokenIn is wrapped native token - both the token or the wrapped token can be sent (the sum of both must be equal to amountIn)
         /// Optionally unwraps any wrapped native token and returns native token instead
         function swap(SwapParams calldata params) external payable returns (uint256 amountOut) {

464:     /// @notice Does 1 or 2 swaps from swapSourceToken to token0 and token1 and adds as much as possible liquidity to a newly minted position.
         /// @param params Swap and mint configuration
         /// Newly minted NFT and leftover tokens are returned to recipient
         function swapAndMint(SwapAndMintParams calldata params)
             external
             payable
             returns (uint256 tokenId, uint128 liquidity, uint256 amount0, uint256 amount1)

529:     /// @notice Does 1 or 2 swaps from swapSourceToken to token0 and token1 and adds as much as possible liquidity to any existing position (no need to be position owner).
         /// @param params Swap and increase liquidity configuration
         // Sends any leftover tokens to recipient.
         function swapAndIncreaseLiquidity(SwapAndIncreaseLiquidityParams calldata params)
             external
             payable
             returns (uint128 liquidity, uint256 amount0, uint256 amount1)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

### <a name="NC-17"></a>[NC-17] Use a `modifier` instead of a `require/if` statement for a special `msg.sender` actor

If a function is supposed to be access-controlled, a `modifier` should be used instead of a `require/if` statement for more readability.

*Instances (26)*:

```solidity
File: src/V3Oracle.sol

250:         if (msg.sender != emergencyAdmin && msg.sender != owner()) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

419:         if (msg.sender != owner) {

435:         if (msg.sender != address(nonfungiblePositionManager) || from == address(this)) {

484:         if (tokenOwner[tokenId] != msg.sender) {

515:         if (loanOwner != msg.sender && !transformApprovals[loanOwner][tokenId][msg.sender]) {

561:         if (!isTransformMode && tokenOwner[tokenId] != msg.sender && address(this) != msg.sender) {

621:         if (owner != msg.sender) {

814:         if (msg.sender != emergencyAdmin && msg.sender != owner()) {

935:         if (msg.sender != owner) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

101:         if (!operators[msg.sender]) {

220:         if (owner != msg.sender) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/automators/Automator.sol

105:         if (msg.sender != withdrawer) {

124:         if (msg.sender != withdrawer) {

232:         if (vaults[msg.sender]) {

245:         if (owner != msg.sender) {

252:         if (msg.sender != address(weth)) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

88:         if (!operators[msg.sender] || !vaults[vault]) {

102:         if (!operators[msg.sender] && !vaults[msg.sender]) {

205:         if (owner != msg.sender) {

228:         if (msg.sender != withdrawer) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

98:         if (!operators[msg.sender] || !vaults[vault]) {

112:         if (!operators[msg.sender] && !vaults[msg.sender]) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/V3Utils.sol

102:         if (nonfungiblePositionManager.ownerOf(tokenId) != msg.sender) {

362:         if (msg.sender != address(nonfungiblePositionManager)) {

915:         if (msg.sender != address(weth)) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/Swapper.sol

161:         if (address(_getPool(tokenIn, tokenOut, fee)) != msg.sender) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="NC-18"></a>[NC-18] Constant state variables defined more than once

Rather than redefining state variable constant, consider using a library to store all constants as this will prevent data redundancy

*Instances (4)*:

```solidity
File: src/InterestRateModel.sol

12:     uint256 private constant Q96 = 2 ** 96;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

27:     uint256 private constant Q96 = 2 ** 96;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

34:     uint256 private constant Q96 = 2 ** 96;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

21:     uint256 internal constant Q96 = 2 ** 96;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

### <a name="NC-19"></a>[NC-19] Consider using named mappings

Consider moving to solidity version 0.8.18 or later, and using [named mappings](https://ethereum.stackexchange.com/questions/51629/how-to-name-the-arguments-in-mapping/145555#145555) to make it easier to understand the purpose of each mapping

*Instances (13)*:

```solidity
File: src/V3Oracle.sol

56:     mapping(address => TokenConfig) public feedConfigs;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

115:     mapping(address => TokenConfig) public tokenConfigs;

154:     mapping(uint256 => Loan) public loans; // tokenID -> loan mapping

157:     mapping(address => uint256[]) private ownedTokens; // Mapping from owner address to list of owned token IDs

158:     mapping(uint256 => uint256) private ownedTokensIndex; // Mapping from token ID to index of the owner tokens list (for removal without loop)

159:     mapping(uint256 => address) private tokenOwner; // Mapping from token ID to owner

163:     mapping(address => bool) public transformerAllowList; // contracts allowed to transform positions (selected audited contracts e.g. V3Utils)

164:     mapping(address => mapping(uint256 => mapping(address => bool))) public transformApprovals; // owners permissions for other addresses to call transform on owners behalf (e.g. AutoRange contract)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

60:     mapping(uint256 => PositionConfig) public positionConfigs;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/automators/Automator.sol

34:     mapping(address => bool) public operators;

35:     mapping(address => bool) public vaults;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

45:     mapping(uint256 => mapping(address => uint256)) public positionBalances;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

50:     mapping(uint256 => PositionConfig) public positionConfigs;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

### <a name="NC-20"></a>[NC-20] Adding a `return` statement when the function defines a named return variable, is redundant

*Instances (6)*:

```solidity
File: src/V3Oracle.sol

272:     function _getReferenceTokenPriceX96(address token, uint256 cachedChainlinkReferencePriceX96)
             internal
             view
             returns (uint256 priceX96, uint256 chainlinkReferencePriceX96)
         {
             if (token == referenceToken) {
                 return (Q96, chainlinkReferencePriceX96);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

255:     /// @notice Retrieves owner of a loan
         /// @param tokenId The unique identifier of the loan - which is the corresponding UniV3 Position
         /// @return owner Owner of the loan
         function ownerOf(uint256 tokenId) external view override returns (address owner) {
             return tokenOwner[tokenId];

288:     /// @inheritdoc IERC4626
         function convertToShares(uint256 assets) external view override returns (uint256 shares) {
             (, uint256 lendExchangeRateX96) = _calculateGlobalInterest();
             return _convertToShares(assets, lendExchangeRateX96, Math.Rounding.Down);

294:     /// @inheritdoc IERC4626
         function convertToAssets(uint256 shares) external view override returns (uint256 assets) {
             (, uint256 lendExchangeRateX96) = _calculateGlobalInterest();
             return _convertToAssets(shares, lendExchangeRateX96, Math.Rounding.Down);

492:     /// @notice Method which allows a contract to transform a loan by changing it (and only at the end checking collateral)
         /// @param tokenId The token ID to be processed
         /// @param transformer The address of a whitelisted transformer contract
         /// @param data Encoded transformation params
         /// @return newTokenId Final token ID (may be different than input token ID when the position was replaced by transformation)
         function transform(uint256 tokenId, address transformer, bytes calldata data)
             external
             override
             returns (uint256 newTokenId)
         {
             if (tokenId == 0 || !transformerAllowList[transformer]) {
                 revert TransformNotAllowed();
             }
             if (transformedTokenId > 0) {
                 revert Reentrancy();
             }
             transformedTokenId = tokenId;
     
             (uint256 newDebtExchangeRateX96,) = _updateGlobalInterest();
     
             address loanOwner = tokenOwner[tokenId];
     
             // only the owner of the loan, the vault itself or any approved caller can call this
             if (loanOwner != msg.sender && !transformApprovals[loanOwner][tokenId][msg.sender]) {
                 revert Unauthorized();
             }
     
             // give access to transformer
             nonfungiblePositionManager.approve(transformer, tokenId);
     
             (bool success,) = transformer.call(data);
             if (!success) {
                 revert TransformFailed();
             }
     
             // may have changed in the meantime
             tokenId = transformedTokenId;
     
             // check owner not changed (NEEDED because token could have been moved somewhere else in the meantime)
             address owner = nonfungiblePositionManager.ownerOf(tokenId);
             if (owner != address(this)) {
                 revert Unauthorized();
             }
     
             // remove access for transformer
             nonfungiblePositionManager.approve(address(0), tokenId);
     
             uint256 debt = _convertToAssets(loans[tokenId].debtShares, newDebtExchangeRateX96, Math.Rounding.Up);
             _requireLoanIsHealthy(tokenId, debt);
     
             transformedTokenId = 0;
     
             return tokenId;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/transformers/V3Utils.sol

92:     /// @notice Execute instruction with EIP712 permit
        /// @param tokenId Token to process
        /// @param instructions Instructions to execute
        /// @param v Signature values for EIP712 permit
        /// @param r Signature values for EIP712 permit
        /// @param s Signature values for EIP712 permit
        function executeWithPermit(uint256 tokenId, Instructions memory instructions, uint8 v, bytes32 r, bytes32 s)
            public
            returns (uint256 newTokenId)
        {
            if (nonfungiblePositionManager.ownerOf(tokenId) != msg.sender) {
                revert Unauthorized();
            }
    
            nonfungiblePositionManager.permit(address(this), tokenId, instructions.deadline, v, r, s);
            return execute(tokenId, instructions);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

### <a name="NC-21"></a>[NC-21] `require()` / `revert()` statements should have descriptive reason strings

*Instances (1)*:

```solidity
File: src/utils/Swapper.sol

157:         require(amount0Delta > 0 || amount1Delta > 0); // swaps entirely within 0-liquidity regions are not supported

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="NC-22"></a>[NC-22] Take advantage of Custom Error's return value property

An important feature of Custom Error is that values such as address, tokenID, msg.value can be written inside the () sign, this kind of approach provides a serious advantage in debugging and examining the revert details of dapps such as tenderly.

*Instances (102)*:

```solidity
File: src/InterestRateModel.sol

92:             revert InvalidConfig();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

148:             revert PriceDifferenceExceeded();

187:             revert InvalidConfig();

212:             revert InvalidConfig();

222:                 revert InvalidConfig();

228:                 revert InvalidPool();

251:             revert Unauthorized();

256:             revert InvalidConfig();

284:             revert NotConfigured();

339:             revert ChainlinkPriceError();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

420:             revert Unauthorized();

436:             revert WrongContract();

485:             revert Unauthorized();

503:             revert TransformNotAllowed();

506:             revert Reentrancy();

516:             revert Unauthorized();

524:             revert TransformFailed();

533:             revert Unauthorized();

562:             revert Unauthorized();

572:             revert GlobalDebtLimit();

575:             revert DailyDebtIncreaseLimit();

587:             revert MinLoanSize();

616:             revert TransformNotAllowed();

622:             revert Unauthorized();

688:             revert TransformNotAllowed();

697:             revert DebtChanged();

705:             revert NotLiquidatable();

738:             revert SlippageError();

775:             revert InsufficientLiquidity();

794:             revert InvalidConfig();

815:             revert Unauthorized();

846:             revert InvalidConfig();

861:             revert CollateralFactorExceedsMax();

907:             revert GlobalLendLimit();

911:             revert DailyLendIncreaseLimit();

941:             revert InsufficientLiquidity();

974:             revert RepayExceedsDebt();

1009:                 revert MinLoanSize();

1200:             revert CollateralFail();

1232:                     revert CollateralValueLimit();

1240:                     revert CollateralValueLimit();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

102:             revert Unauthorized();

109:             revert NotConfigured();

116:             revert ExceedsMaxReward();

125:             revert NoLiquidity();

128:             revert LiquidityChanged();

136:             revert NotReady();

150:                 revert MissingSwapData();

221:             revert Unauthorized();

226:                 revert InvalidConfig();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/automators/Automator.sol

89:             revert InvalidConfig();

92:             revert InvalidConfig();

106:             revert Unauthorized();

125:             revert Unauthorized();

132:                 revert EtherSendFailed();

152:             revert TWAPCheckFailed();

223:                 revert EtherSendFailed();

233:             revert Unauthorized();

238:                 revert Unauthorized();

246:             revert Unauthorized();

253:             revert NotWETH();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

89:             revert Unauthorized();

103:             revert Unauthorized();

206:             revert Unauthorized();

229:             revert Unauthorized();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

99:             revert Unauthorized();

113:             revert Unauthorized();

119:             revert NotConfigured();

126:             revert ExceedsMaxReward();

134:             revert LiquidityChanged();

150:             revert SwapAmountTooLarge();

178:                 revert SameRange();

270:             revert NotReady();

281:             revert InvalidConfig();

310:                 revert NotSupportedFeeTier();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/V3Utils.sol

103:             revert Unauthorized();

143:             revert AmountError();

350:             revert NotSupportedWhatToDo();

363:             revert WrongContract();

368:             revert SelfSend();

399:             revert SameToken();

473:             revert SameToken();

636:                 revert TransferError(); // reverts for fee-on-transfer tokens

641:                 revert TransferError(); // reverts for fee-on-transfer tokens

646:                 revert TransferError(); // reverts for fee-on-transfer tokens

672:                     revert TooMuchEtherSent();

677:                     revert TooMuchEtherSent();

682:                     revert TooMuchEtherSent();

685:                 revert NoEtherToken();

785:                 revert AmountError();

796:                 revert AmountError();

869:                 revert EtherSendFailed();

906:             revert CollectError();

909:             revert CollectError();

916:             revert NotWETH();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

44:             revert NotLiquidatable();

103:                 revert NotEnoughReward();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

```solidity
File: src/utils/Swapper.sol

91:                     revert SwapFailed();

101:                 revert WrongContract();

112:                 revert SlippageError();

150:                 revert SlippageError();

162:             revert Unauthorized();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="NC-23"></a>[NC-23] Deprecated library used for Solidity `>= 0.8` : SafeMath

*Instances (1)*:

```solidity
File: src/transformers/AutoCompound.sol

6: import "@openzeppelin/contracts/utils/math/SafeMath.sol";

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

### <a name="NC-24"></a>[NC-24] Contract does not follow the Solidity style guide's suggested layout ordering

The [style guide](https://docs.soliditylang.org/en/v0.8.16/style-guide.html#order-of-layout) says that, within a contract, the ordering should be:

1) Type declarations
2) State variables
3) Events
4) Modifiers
5) Functions

However, the contract(s) below do not follow this ordering

*Instances (11)*:

```solidity
File: src/InterestRateModel.sol

1: 
   Current order:
   VariableDeclaration.Q96
   VariableDeclaration.YEAR_SECS
   VariableDeclaration.MAX_BASE_RATE_X96
   VariableDeclaration.MAX_MULTIPLIER_X96
   EventDefinition.SetValues
   VariableDeclaration.multiplierPerSecondX96
   VariableDeclaration.baseRatePerSecondX96
   VariableDeclaration.jumpMultiplierPerSecondX96
   VariableDeclaration.kinkX96
   FunctionDefinition.constructor
   FunctionDefinition.getUtilizationRateX96
   FunctionDefinition.getRatesPerSecondX96
   FunctionDefinition.setValues
   
   Suggested order:
   VariableDeclaration.Q96
   VariableDeclaration.YEAR_SECS
   VariableDeclaration.MAX_BASE_RATE_X96
   VariableDeclaration.MAX_MULTIPLIER_X96
   VariableDeclaration.multiplierPerSecondX96
   VariableDeclaration.baseRatePerSecondX96
   VariableDeclaration.jumpMultiplierPerSecondX96
   VariableDeclaration.kinkX96
   EventDefinition.SetValues
   FunctionDefinition.constructor
   FunctionDefinition.getUtilizationRateX96
   FunctionDefinition.getRatesPerSecondX96
   FunctionDefinition.setValues

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

1: 
   Current order:
   VariableDeclaration.MIN_PRICE_DIFFERENCE
   VariableDeclaration.Q96
   VariableDeclaration.Q128
   EventDefinition.TokenConfigUpdated
   EventDefinition.OracleModeUpdated
   EventDefinition.SetMaxPoolPriceDifference
   EventDefinition.SetEmergencyAdmin
   EnumDefinition.Mode
   StructDefinition.TokenConfig
   VariableDeclaration.feedConfigs
   VariableDeclaration.factory
   VariableDeclaration.nonfungiblePositionManager
   VariableDeclaration.referenceToken
   VariableDeclaration.referenceTokenDecimals
   VariableDeclaration.maxPoolPriceDifference
   VariableDeclaration.chainlinkReferenceToken
   VariableDeclaration.emergencyAdmin
   FunctionDefinition.constructor
   FunctionDefinition.getValue
   FunctionDefinition._checkPoolPrice
   FunctionDefinition._requireMaxDifference
   FunctionDefinition.getPositionBreakdown
   FunctionDefinition.setMaxPoolPriceDifference
   FunctionDefinition.setTokenConfig
   FunctionDefinition.setOracleMode
   FunctionDefinition.setEmergencyAdmin
   FunctionDefinition._getReferenceTokenPriceX96
   FunctionDefinition._getChainlinkPriceX96
   FunctionDefinition._getTWAPPriceX96
   FunctionDefinition._getReferencePoolPriceX96
   StructDefinition.PositionState
   FunctionDefinition._initializeState
   FunctionDefinition._getAmounts
   FunctionDefinition._getUncollectedFees
   FunctionDefinition._getFeeGrowthInside
   FunctionDefinition._getPool
   
   Suggested order:
   VariableDeclaration.MIN_PRICE_DIFFERENCE
   VariableDeclaration.Q96
   VariableDeclaration.Q128
   VariableDeclaration.feedConfigs
   VariableDeclaration.factory
   VariableDeclaration.nonfungiblePositionManager
   VariableDeclaration.referenceToken
   VariableDeclaration.referenceTokenDecimals
   VariableDeclaration.maxPoolPriceDifference
   VariableDeclaration.chainlinkReferenceToken
   VariableDeclaration.emergencyAdmin
   EnumDefinition.Mode
   StructDefinition.TokenConfig
   StructDefinition.PositionState
   EventDefinition.TokenConfigUpdated
   EventDefinition.OracleModeUpdated
   EventDefinition.SetMaxPoolPriceDifference
   EventDefinition.SetEmergencyAdmin
   FunctionDefinition.constructor
   FunctionDefinition.getValue
   FunctionDefinition._checkPoolPrice
   FunctionDefinition._requireMaxDifference
   FunctionDefinition.getPositionBreakdown
   FunctionDefinition.setMaxPoolPriceDifference
   FunctionDefinition.setTokenConfig
   FunctionDefinition.setOracleMode
   FunctionDefinition.setEmergencyAdmin
   FunctionDefinition._getReferenceTokenPriceX96
   FunctionDefinition._getChainlinkPriceX96
   FunctionDefinition._getTWAPPriceX96
   FunctionDefinition._getReferencePoolPriceX96
   FunctionDefinition._initializeState
   FunctionDefinition._getAmounts
   FunctionDefinition._getUncollectedFees
   FunctionDefinition._getFeeGrowthInside
   FunctionDefinition._getPool

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

1: 
   Current order:
   UsingForDirective.Math
   VariableDeclaration.Q32
   VariableDeclaration.Q96
   VariableDeclaration.MAX_COLLATERAL_FACTOR_X32
   VariableDeclaration.MIN_LIQUIDATION_PENALTY_X32
   VariableDeclaration.MAX_LIQUIDATION_PENALTY_X32
   VariableDeclaration.MIN_RESERVE_PROTECTION_FACTOR_X32
   VariableDeclaration.MAX_DAILY_LEND_INCREASE_X32
   VariableDeclaration.MAX_DAILY_DEBT_INCREASE_X32
   VariableDeclaration.nonfungiblePositionManager
   VariableDeclaration.factory
   VariableDeclaration.interestRateModel
   VariableDeclaration.oracle
   VariableDeclaration.permit2
   VariableDeclaration.asset
   VariableDeclaration.assetDecimals
   EventDefinition.ApprovedTransform
   EventDefinition.Add
   EventDefinition.Remove
   EventDefinition.ExchangeRateUpdate
   EventDefinition.WithdrawCollateral
   EventDefinition.Borrow
   EventDefinition.Repay
   EventDefinition.Liquidate
   EventDefinition.WithdrawReserves
   EventDefinition.SetTransformer
   EventDefinition.SetLimits
   EventDefinition.SetReserveFactor
   EventDefinition.SetReserveProtectionFactor
   EventDefinition.SetTokenConfig
   EventDefinition.SetEmergencyAdmin
   StructDefinition.TokenConfig
   VariableDeclaration.tokenConfigs
   VariableDeclaration.reserveFactorX32
   VariableDeclaration.reserveProtectionFactorX32
   VariableDeclaration.debtSharesTotal
   VariableDeclaration.lastExchangeRateUpdate
   VariableDeclaration.lastDebtExchangeRateX96
   VariableDeclaration.lastLendExchangeRateX96
   VariableDeclaration.globalDebtLimit
   VariableDeclaration.globalLendLimit
   VariableDeclaration.minLoanSize
   VariableDeclaration.dailyLendIncreaseLimitMin
   VariableDeclaration.dailyLendIncreaseLimitLeft
   VariableDeclaration.dailyLendIncreaseLimitLastReset
   VariableDeclaration.dailyDebtIncreaseLimitMin
   VariableDeclaration.dailyDebtIncreaseLimitLeft
   VariableDeclaration.dailyDebtIncreaseLimitLastReset
   StructDefinition.Loan
   VariableDeclaration.loans
   VariableDeclaration.ownedTokens
   VariableDeclaration.ownedTokensIndex
   VariableDeclaration.tokenOwner
   VariableDeclaration.transformedTokenId
   VariableDeclaration.transformerAllowList
   VariableDeclaration.transformApprovals
   VariableDeclaration.emergencyAdmin
   FunctionDefinition.constructor
   FunctionDefinition.vaultInfo
   FunctionDefinition.lendInfo
   FunctionDefinition.loanInfo
   FunctionDefinition.ownerOf
   FunctionDefinition.loanCount
   FunctionDefinition.loanAtIndex
   FunctionDefinition.decimals
   FunctionDefinition.totalAssets
   FunctionDefinition.convertToShares
   FunctionDefinition.convertToAssets
   FunctionDefinition.maxDeposit
   FunctionDefinition.maxMint
   FunctionDefinition.maxWithdraw
   FunctionDefinition.maxRedeem
   FunctionDefinition.previewDeposit
   FunctionDefinition.previewMint
   FunctionDefinition.previewWithdraw
   FunctionDefinition.previewRedeem
   FunctionDefinition.deposit
   FunctionDefinition.mint
   FunctionDefinition.withdraw
   FunctionDefinition.redeem
   FunctionDefinition.deposit
   FunctionDefinition.mint
   FunctionDefinition.create
   FunctionDefinition.createWithPermit
   FunctionDefinition.onERC721Received
   FunctionDefinition.approveTransform
   FunctionDefinition.transform
   FunctionDefinition.borrow
   FunctionDefinition.decreaseLiquidityAndCollect
   FunctionDefinition.repay
   FunctionDefinition.repay
   StructDefinition.LiquidateState
   FunctionDefinition.liquidate
   FunctionDefinition.withdrawReserves
   FunctionDefinition.setTransformer
   FunctionDefinition.setLimits
   FunctionDefinition.setReserveFactor
   FunctionDefinition.setReserveProtectionFactor
   FunctionDefinition.setTokenConfig
   FunctionDefinition.setEmergencyAdmin
   FunctionDefinition._deposit
   FunctionDefinition._withdraw
   FunctionDefinition._repay
   FunctionDefinition._getAvailableBalance
   FunctionDefinition._sendPositionValue
   FunctionDefinition._cleanupLoan
   FunctionDefinition._calculateLiquidation
   FunctionDefinition._handleReserveLiquidation
   FunctionDefinition._calculateTokenCollateralFactorX32
   FunctionDefinition._updateGlobalInterest
   FunctionDefinition._calculateGlobalInterest
   FunctionDefinition._requireLoanIsHealthy
   FunctionDefinition._updateAndCheckCollateral
   FunctionDefinition._resetDailyLendIncreaseLimit
   FunctionDefinition._resetDailyDebtIncreaseLimit
   FunctionDefinition._checkLoanIsHealthy
   FunctionDefinition._convertToShares
   FunctionDefinition._convertToAssets
   FunctionDefinition._addTokenToOwner
   FunctionDefinition._removeTokenFromOwner
   
   Suggested order:
   UsingForDirective.Math
   VariableDeclaration.Q32
   VariableDeclaration.Q96
   VariableDeclaration.MAX_COLLATERAL_FACTOR_X32
   VariableDeclaration.MIN_LIQUIDATION_PENALTY_X32
   VariableDeclaration.MAX_LIQUIDATION_PENALTY_X32
   VariableDeclaration.MIN_RESERVE_PROTECTION_FACTOR_X32
   VariableDeclaration.MAX_DAILY_LEND_INCREASE_X32
   VariableDeclaration.MAX_DAILY_DEBT_INCREASE_X32
   VariableDeclaration.nonfungiblePositionManager
   VariableDeclaration.factory
   VariableDeclaration.interestRateModel
   VariableDeclaration.oracle
   VariableDeclaration.permit2
   VariableDeclaration.asset
   VariableDeclaration.assetDecimals
   VariableDeclaration.tokenConfigs
   VariableDeclaration.reserveFactorX32
   VariableDeclaration.reserveProtectionFactorX32
   VariableDeclaration.debtSharesTotal
   VariableDeclaration.lastExchangeRateUpdate
   VariableDeclaration.lastDebtExchangeRateX96
   VariableDeclaration.lastLendExchangeRateX96
   VariableDeclaration.globalDebtLimit
   VariableDeclaration.globalLendLimit
   VariableDeclaration.minLoanSize
   VariableDeclaration.dailyLendIncreaseLimitMin
   VariableDeclaration.dailyLendIncreaseLimitLeft
   VariableDeclaration.dailyLendIncreaseLimitLastReset
   VariableDeclaration.dailyDebtIncreaseLimitMin
   VariableDeclaration.dailyDebtIncreaseLimitLeft
   VariableDeclaration.dailyDebtIncreaseLimitLastReset
   VariableDeclaration.loans
   VariableDeclaration.ownedTokens
   VariableDeclaration.ownedTokensIndex
   VariableDeclaration.tokenOwner
   VariableDeclaration.transformedTokenId
   VariableDeclaration.transformerAllowList
   VariableDeclaration.transformApprovals
   VariableDeclaration.emergencyAdmin
   StructDefinition.TokenConfig
   StructDefinition.Loan
   StructDefinition.LiquidateState
   EventDefinition.ApprovedTransform
   EventDefinition.Add
   EventDefinition.Remove
   EventDefinition.ExchangeRateUpdate
   EventDefinition.WithdrawCollateral
   EventDefinition.Borrow
   EventDefinition.Repay
   EventDefinition.Liquidate
   EventDefinition.WithdrawReserves
   EventDefinition.SetTransformer
   EventDefinition.SetLimits
   EventDefinition.SetReserveFactor
   EventDefinition.SetReserveProtectionFactor
   EventDefinition.SetTokenConfig
   EventDefinition.SetEmergencyAdmin
   FunctionDefinition.constructor
   FunctionDefinition.vaultInfo
   FunctionDefinition.lendInfo
   FunctionDefinition.loanInfo
   FunctionDefinition.ownerOf
   FunctionDefinition.loanCount
   FunctionDefinition.loanAtIndex
   FunctionDefinition.decimals
   FunctionDefinition.totalAssets
   FunctionDefinition.convertToShares
   FunctionDefinition.convertToAssets
   FunctionDefinition.maxDeposit
   FunctionDefinition.maxMint
   FunctionDefinition.maxWithdraw
   FunctionDefinition.maxRedeem
   FunctionDefinition.previewDeposit
   FunctionDefinition.previewMint
   FunctionDefinition.previewWithdraw
   FunctionDefinition.previewRedeem
   FunctionDefinition.deposit
   FunctionDefinition.mint
   FunctionDefinition.withdraw
   FunctionDefinition.redeem
   FunctionDefinition.deposit
   FunctionDefinition.mint
   FunctionDefinition.create
   FunctionDefinition.createWithPermit
   FunctionDefinition.onERC721Received
   FunctionDefinition.approveTransform
   FunctionDefinition.transform
   FunctionDefinition.borrow
   FunctionDefinition.decreaseLiquidityAndCollect
   FunctionDefinition.repay
   FunctionDefinition.repay
   FunctionDefinition.liquidate
   FunctionDefinition.withdrawReserves
   FunctionDefinition.setTransformer
   FunctionDefinition.setLimits
   FunctionDefinition.setReserveFactor
   FunctionDefinition.setReserveProtectionFactor
   FunctionDefinition.setTokenConfig
   FunctionDefinition.setEmergencyAdmin
   FunctionDefinition._deposit
   FunctionDefinition._withdraw
   FunctionDefinition._repay
   FunctionDefinition._getAvailableBalance
   FunctionDefinition._sendPositionValue
   FunctionDefinition._cleanupLoan
   FunctionDefinition._calculateLiquidation
   FunctionDefinition._handleReserveLiquidation
   FunctionDefinition._calculateTokenCollateralFactorX32
   FunctionDefinition._updateGlobalInterest
   FunctionDefinition._calculateGlobalInterest
   FunctionDefinition._requireLoanIsHealthy
   FunctionDefinition._updateAndCheckCollateral
   FunctionDefinition._resetDailyLendIncreaseLimit
   FunctionDefinition._resetDailyDebtIncreaseLimit
   FunctionDefinition._checkLoanIsHealthy
   FunctionDefinition._convertToShares
   FunctionDefinition._convertToAssets
   FunctionDefinition._addTokenToOwner
   FunctionDefinition._removeTokenFromOwner

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

1: 
   Current order:
   EventDefinition.Executed
   EventDefinition.PositionConfigured
   FunctionDefinition.constructor
   StructDefinition.PositionConfig
   VariableDeclaration.positionConfigs
   StructDefinition.ExecuteParams
   StructDefinition.ExecuteState
   FunctionDefinition.execute
   FunctionDefinition.configToken
   
   Suggested order:
   VariableDeclaration.positionConfigs
   StructDefinition.PositionConfig
   StructDefinition.ExecuteParams
   StructDefinition.ExecuteState
   EventDefinition.Executed
   EventDefinition.PositionConfigured
   FunctionDefinition.constructor
   FunctionDefinition.execute
   FunctionDefinition.configToken

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/automators/Automator.sol

1: 
   Current order:
   VariableDeclaration.Q64
   VariableDeclaration.Q96
   VariableDeclaration.MIN_TWAP_SECONDS
   VariableDeclaration.MAX_TWAP_TICK_DIFFERENCE
   EventDefinition.OperatorChanged
   EventDefinition.VaultChanged
   EventDefinition.WithdrawerChanged
   EventDefinition.TWAPConfigChanged
   VariableDeclaration.operators
   VariableDeclaration.vaults
   VariableDeclaration.withdrawer
   VariableDeclaration.TWAPSeconds
   VariableDeclaration.maxTWAPTickDifference
   FunctionDefinition.constructor
   FunctionDefinition.setWithdrawer
   FunctionDefinition.setOperator
   FunctionDefinition.setVault
   FunctionDefinition.setTWAPConfig
   FunctionDefinition.withdrawBalances
   FunctionDefinition.withdrawETH
   FunctionDefinition._validateSwap
   FunctionDefinition._hasMaxTWAPTickDifference
   FunctionDefinition._getTWAPTick
   FunctionDefinition._decreaseFullLiquidityAndCollect
   FunctionDefinition._transferToken
   FunctionDefinition._validateOwner
   FunctionDefinition.receive
   
   Suggested order:
   VariableDeclaration.Q64
   VariableDeclaration.Q96
   VariableDeclaration.MIN_TWAP_SECONDS
   VariableDeclaration.MAX_TWAP_TICK_DIFFERENCE
   VariableDeclaration.operators
   VariableDeclaration.vaults
   VariableDeclaration.withdrawer
   VariableDeclaration.TWAPSeconds
   VariableDeclaration.maxTWAPTickDifference
   EventDefinition.OperatorChanged
   EventDefinition.VaultChanged
   EventDefinition.WithdrawerChanged
   EventDefinition.TWAPConfigChanged
   FunctionDefinition.constructor
   FunctionDefinition.setWithdrawer
   FunctionDefinition.setOperator
   FunctionDefinition.setVault
   FunctionDefinition.setTWAPConfig
   FunctionDefinition.withdrawBalances
   FunctionDefinition.withdrawETH
   FunctionDefinition._validateSwap
   FunctionDefinition._hasMaxTWAPTickDifference
   FunctionDefinition._getTWAPTick
   FunctionDefinition._decreaseFullLiquidityAndCollect
   FunctionDefinition._transferToken
   FunctionDefinition._validateOwner
   FunctionDefinition.receive

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

1: 
   Current order:
   EventDefinition.AutoCompounded
   EventDefinition.RewardUpdated
   EventDefinition.BalanceAdded
   EventDefinition.BalanceRemoved
   EventDefinition.BalanceWithdrawn
   FunctionDefinition.constructor
   VariableDeclaration.positionBalances
   VariableDeclaration.MAX_REWARD_X64
   VariableDeclaration.totalRewardX64
   StructDefinition.ExecuteParams
   StructDefinition.ExecuteState
   FunctionDefinition.executeWithVault
   FunctionDefinition.execute
   FunctionDefinition.withdrawLeftoverBalances
   FunctionDefinition.withdrawBalances
   FunctionDefinition.setReward
   FunctionDefinition._increaseBalance
   FunctionDefinition._setBalance
   FunctionDefinition._withdrawBalanceInternal
   FunctionDefinition._checkApprovals
   
   Suggested order:
   VariableDeclaration.positionBalances
   VariableDeclaration.MAX_REWARD_X64
   VariableDeclaration.totalRewardX64
   StructDefinition.ExecuteParams
   StructDefinition.ExecuteState
   EventDefinition.AutoCompounded
   EventDefinition.RewardUpdated
   EventDefinition.BalanceAdded
   EventDefinition.BalanceRemoved
   EventDefinition.BalanceWithdrawn
   FunctionDefinition.constructor
   FunctionDefinition.executeWithVault
   FunctionDefinition.execute
   FunctionDefinition.withdrawLeftoverBalances
   FunctionDefinition.withdrawBalances
   FunctionDefinition.setReward
   FunctionDefinition._increaseBalance
   FunctionDefinition._setBalance
   FunctionDefinition._withdrawBalanceInternal
   FunctionDefinition._checkApprovals

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

1: 
   Current order:
   EventDefinition.RangeChanged
   EventDefinition.PositionConfigured
   FunctionDefinition.constructor
   StructDefinition.PositionConfig
   VariableDeclaration.positionConfigs
   StructDefinition.ExecuteParams
   StructDefinition.ExecuteState
   FunctionDefinition.executeWithVault
   FunctionDefinition.execute
   FunctionDefinition.configToken
   FunctionDefinition._getTickSpacing
   
   Suggested order:
   VariableDeclaration.positionConfigs
   StructDefinition.PositionConfig
   StructDefinition.ExecuteParams
   StructDefinition.ExecuteState
   EventDefinition.RangeChanged
   EventDefinition.PositionConfigured
   FunctionDefinition.constructor
   FunctionDefinition.executeWithVault
   FunctionDefinition.execute
   FunctionDefinition.configToken
   FunctionDefinition._getTickSpacing

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

1: 
   Current order:
   FunctionDefinition.constructor
   StructDefinition.LeverageUpParams
   FunctionDefinition.leverageUp
   StructDefinition.LeverageDownParams
   FunctionDefinition.leverageDown
   
   Suggested order:
   StructDefinition.LeverageUpParams
   StructDefinition.LeverageDownParams
   FunctionDefinition.constructor
   FunctionDefinition.leverageUp
   FunctionDefinition.leverageDown

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/transformers/V3Utils.sol

1: 
   Current order:
   UsingForDirective.SafeCast
   VariableDeclaration.permit2
   EventDefinition.CompoundFees
   EventDefinition.ChangeRange
   EventDefinition.WithdrawAndCollectAndSwap
   EventDefinition.SwapAndMint
   EventDefinition.SwapAndIncreaseLiquidity
   FunctionDefinition.constructor
   EnumDefinition.WhatToDo
   StructDefinition.Instructions
   FunctionDefinition.executeWithPermit
   FunctionDefinition.execute
   FunctionDefinition.onERC721Received
   StructDefinition.SwapParams
   FunctionDefinition.swap
   StructDefinition.SwapAndMintParams
   FunctionDefinition.swapAndMint
   StructDefinition.SwapAndIncreaseLiquidityParams
   FunctionDefinition.swapAndIncreaseLiquidity
   FunctionDefinition._prepareAddApproved
   StructDefinition.PrepareAddPermit2State
   FunctionDefinition._prepareAddPermit2
   FunctionDefinition._prepareAdd
   FunctionDefinition._swapAndMint
   FunctionDefinition._swapAndIncrease
   FunctionDefinition._swapAndPrepareAmounts
   FunctionDefinition._returnLeftoverTokens
   FunctionDefinition._transferToken
   FunctionDefinition._decreaseLiquidity
   FunctionDefinition._collectFees
   FunctionDefinition.receive
   
   Suggested order:
   UsingForDirective.SafeCast
   VariableDeclaration.permit2
   EnumDefinition.WhatToDo
   StructDefinition.Instructions
   StructDefinition.SwapParams
   StructDefinition.SwapAndMintParams
   StructDefinition.SwapAndIncreaseLiquidityParams
   StructDefinition.PrepareAddPermit2State
   EventDefinition.CompoundFees
   EventDefinition.ChangeRange
   EventDefinition.WithdrawAndCollectAndSwap
   EventDefinition.SwapAndMint
   EventDefinition.SwapAndIncreaseLiquidity
   FunctionDefinition.constructor
   FunctionDefinition.executeWithPermit
   FunctionDefinition.execute
   FunctionDefinition.onERC721Received
   FunctionDefinition.swap
   FunctionDefinition.swapAndMint
   FunctionDefinition.swapAndIncreaseLiquidity
   FunctionDefinition._prepareAddApproved
   FunctionDefinition._prepareAddPermit2
   FunctionDefinition._prepareAdd
   FunctionDefinition._swapAndMint
   FunctionDefinition._swapAndIncrease
   FunctionDefinition._swapAndPrepareAmounts
   FunctionDefinition._returnLeftoverTokens
   FunctionDefinition._transferToken
   FunctionDefinition._decreaseLiquidity
   FunctionDefinition._collectFees
   FunctionDefinition.receive

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

1: 
   Current order:
   StructDefinition.FlashCallbackData
   FunctionDefinition.constructor
   StructDefinition.LiquidateParams
   FunctionDefinition.liquidate
   FunctionDefinition.uniswapV3FlashCallback
   
   Suggested order:
   StructDefinition.FlashCallbackData
   StructDefinition.LiquidateParams
   FunctionDefinition.constructor
   FunctionDefinition.liquidate
   FunctionDefinition.uniswapV3FlashCallback

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

```solidity
File: src/utils/Swapper.sol

1: 
   Current order:
   EventDefinition.Swap
   VariableDeclaration.weth
   VariableDeclaration.factory
   VariableDeclaration.nonfungiblePositionManager
   VariableDeclaration.zeroxRouter
   VariableDeclaration.universalRouter
   FunctionDefinition.constructor
   StructDefinition.ZeroxRouterData
   StructDefinition.UniversalRouterData
   StructDefinition.RouterSwapParams
   FunctionDefinition._routerSwap
   StructDefinition.PoolSwapParams
   FunctionDefinition._poolSwap
   FunctionDefinition.uniswapV3SwapCallback
   FunctionDefinition._getPool
   
   Suggested order:
   VariableDeclaration.weth
   VariableDeclaration.factory
   VariableDeclaration.nonfungiblePositionManager
   VariableDeclaration.zeroxRouter
   VariableDeclaration.universalRouter
   StructDefinition.ZeroxRouterData
   StructDefinition.UniversalRouterData
   StructDefinition.RouterSwapParams
   StructDefinition.PoolSwapParams
   EventDefinition.Swap
   FunctionDefinition.constructor
   FunctionDefinition._routerSwap
   FunctionDefinition._poolSwap
   FunctionDefinition.uniswapV3SwapCallback
   FunctionDefinition._getPool

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="NC-25"></a>[NC-25] Use Underscores for Number Literals (add an underscore every 3 digits)

*Instances (5)*:

```solidity
File: src/InterestRateModel.sol

13:     uint256 public constant YEAR_SECS = 31557600; // taking into account leap years

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

144:             ? (priceX96 - verifyPriceX96) * 10000 / priceX96

145:             : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/transformers/AutoRange.sol

301:         if (fee == 10000) {

303:         } else if (fee == 3000) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

### <a name="NC-26"></a>[NC-26] Internal and private variables and functions names should begin with an underscore

According to the Solidity Style Guide, Non-`external` variable and function names should begin with an [underscore](https://docs.soliditylang.org/en/latest/style-guide.html#underscore-prefix-for-non-external-functions-and-variables)

*Instances (4)*:

```solidity
File: src/V3Vault.sol

157:     mapping(address => uint256[]) private ownedTokens; // Mapping from owner address to list of owned token IDs

158:     mapping(uint256 => uint256) private ownedTokensIndex; // Mapping from token ID to index of the owner tokens list (for removal without loop)

159:     mapping(uint256 => address) private tokenOwner; // Mapping from token ID to owner

161:     uint256 private transformedTokenId = 0; // transient storage (when available in dencun)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

### <a name="NC-27"></a>[NC-27] Event is missing `indexed` fields

Index event fields make the field more quickly accessible to off-chain tools that parse events. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Each event should use three indexed fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three fields, all of the fields should be indexed.

*Instances (38)*:

```solidity
File: src/InterestRateModel.sol

18:     event SetValues(

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

30:     event TokenConfigUpdated(address indexed token, TokenConfig config);

31:     event OracleModeUpdated(address indexed token, Mode mode);

32:     event SetMaxPoolPriceDifference(uint16 maxPoolPriceDifference);

33:     event SetEmergencyAdmin(address emergencyAdmin);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

68:     event ApprovedTransform(uint256 indexed tokenId, address owner, address target, bool isActive);

70:     event Add(uint256 indexed tokenId, address owner, uint256 oldTokenId); // when a token is added replacing another token - oldTokenId > 0

71:     event Remove(uint256 indexed tokenId, address recipient);

73:     event ExchangeRateUpdate(uint256 debtExchangeRateX96, uint256 lendExchangeRateX96);

75:     event WithdrawCollateral(

78:     event Borrow(uint256 indexed tokenId, address owner, uint256 assets, uint256 shares);

79:     event Repay(uint256 indexed tokenId, address repayer, address owner, uint256 assets, uint256 shares);

80:     event Liquidate(

93:     event WithdrawReserves(uint256 amount, address receiver);

94:     event SetTransformer(address transformer, bool active);

95:     event SetLimits(

102:     event SetReserveFactor(uint32 reserveFactorX32);

103:     event SetReserveProtectionFactor(uint32 reserveProtectionFactorX32);

104:     event SetTokenConfig(address token, uint32 collateralFactorX32, uint32 collateralValueLimitFactorX32);

106:     event SetEmergencyAdmin(address emergencyAdmin);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

11:     event Executed(

20:     event PositionConfigured(

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/automators/Automator.sol

27:     event OperatorChanged(address newOperator, bool active);

28:     event VaultChanged(address newVault, bool active);

30:     event WithdrawerChanged(address newWithdrawer);

31:     event TWAPConfigChanged(uint32 TWAPSeconds, uint16 maxTWAPTickDifference);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

18:     event AutoCompounded(

30:     event RewardUpdated(address account, uint64 totalRewardX64);

33:     event BalanceAdded(uint256 tokenId, address token, uint256 amount);

34:     event BalanceRemoved(uint256 tokenId, address token, uint256 amount);

35:     event BalanceWithdrawn(uint256 tokenId, address token, address to, uint256 amount);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

13:     event PositionConfigured(

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/V3Utils.sol

22:     event CompoundFees(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

23:     event ChangeRange(uint256 indexed tokenId, uint256 newTokenId);

24:     event WithdrawAndCollectAndSwap(uint256 indexed tokenId, address token, uint256 amount);

25:     event SwapAndMint(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

26:     event SwapAndIncreaseLiquidity(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/Swapper.sol

18:     event Swap(address indexed tokenIn, address indexed tokenOut, uint256 amountIn, uint256 amountOut);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="NC-28"></a>[NC-28] `public` functions not called by the contract should be declared `external` instead

*Instances (2)*:

```solidity
File: src/automators/Automator.sol

79:     function setVault(address _vault, bool _active) public onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/V3Utils.sol

98:     function executeWithPermit(uint256 tokenId, Instructions memory instructions, uint8 v, bytes32 r, bytes32 s)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

### <a name="NC-29"></a>[NC-29] Variables need not be initialized to zero

The default value for variables is zero, so initializing them to zero is superfluous.

*Instances (13)*:

```solidity
File: src/V3Vault.sol

118:     uint32 public reserveFactorX32 = 0;

124:     uint256 public debtSharesTotal = 0;

127:     uint256 public lastExchangeRateUpdate = 0;

131:     uint256 public globalDebtLimit = 0;

132:     uint256 public globalLendLimit = 0;

135:     uint256 public minLoanSize = 0;

138:     uint256 public dailyLendIncreaseLimitMin = 0;

139:     uint256 public dailyLendIncreaseLimitLeft = 0;

140:     uint256 public dailyLendIncreaseLimitLastReset = 0;

143:     uint256 public dailyDebtIncreaseLimitMin = 0;

144:     uint256 public dailyDebtIncreaseLimitLeft = 0;

145:     uint256 public dailyDebtIncreaseLimitLastReset = 0;

161:     uint256 private transformedTokenId = 0; // transient storage (when available in dencun)

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

## Low Issues

| |Issue|Instances|
|-|:-|:-:|
| [L-1](#L-1) | `approve()`/`safeApprove()` may revert if the current approval is not zero | 17 |
| [L-2](#L-2) | Use a 2-step ownership transfer pattern | 4 |
| [L-3](#L-3) | Some tokens may revert when zero value transfers are made | 23 |
| [L-4](#L-4) | Missing checks for `address(0)` when assigning values to address state variables | 6 |
| [L-5](#L-5) | `decimals()` is not a part of the ERC-20 standard | 4 |
| [L-6](#L-6) | Deprecated approve() function | 2 |
| [L-7](#L-7) | Do not use deprecated library functions | 15 |
| [L-8](#L-8) | `safeApprove()` is deprecated | 15 |
| [L-9](#L-9) | Division by zero not prevented | 49 |
| [L-10](#L-10) | External call recipient may consume all transaction gas | 5 |
| [L-11](#L-11) | Signature use at deadlines should be allowed | 1 |
| [L-12](#L-12) | Prevent accidentally burning tokens | 4 |
| [L-13](#L-13) | Possible rounding issue | 1 |
| [L-14](#L-14) | Loss of precision | 5 |
| [L-15](#L-15) | Solidity version 0.8.20+ may not work on other chains due to `PUSH0` | 9 |
| [L-16](#L-16) | Use `Ownable2Step.transferOwnership` instead of `Ownable.transferOwnership` | 4 |
| [L-17](#L-17) | File allows a version of solidity that is susceptible to an assembly optimizer bug | 9 |
| [L-18](#L-18) | Consider using OpenZeppelin's SafeCast library to prevent unexpected overflows when downcasting | 12 |
| [L-19](#L-19) | Unsafe ERC20 operation(s) | 2 |
| [L-20](#L-20) | Upgradeable contract not initialized | 2 |

### <a name="L-1"></a>[L-1] `approve()`/`safeApprove()` may revert if the current approval is not zero

- Some tokens (like the *very popular* USDT) do not work when changing the allowance from an existing non-zero allowance value (it will revert if the current approval is not zero to protect against front-running changes of approvals). These tokens must first be approved for zero and then the actual allowance can be approved.
- Furthermore, OZ's implementation of safeApprove would throw an error if an approve is attempted from a non-zero value (`"SafeERC20: approve from non-zero to non-zero allowance"`)

Set the allowance to zero immediately before each of the existing allowance calls

*Instances (17)*:

```solidity
File: src/V3Vault.sol

520:         nonfungiblePositionManager.approve(transformer, tokenId);

537:         nonfungiblePositionManager.approve(address(0), tokenId);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/transformers/AutoCompound.sol

280:             SafeERC20.safeApprove(IERC20(token0), address(nonfungiblePositionManager), type(uint256).max);

284:             SafeERC20.safeApprove(IERC20(token1), address(nonfungiblePositionManager), type(uint256).max);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

213:             SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), state.maxAddAmount0);

214:             SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), state.maxAddAmount1);

220:             SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), 0);

221:             SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), 0);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

165:         SafeERC20.safeApprove(IERC20(token), msg.sender, amount);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/transformers/V3Utils.sol

831:             SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), 0);

832:             SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), total0);

835:             SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), 0);

836:             SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), total1);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

72:         SafeERC20.safeApprove(data.asset, address(data.vault), data.liquidationCost);

78:         SafeERC20.safeApprove(data.asset, address(data.vault), 0);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

```solidity
File: src/utils/Swapper.sol

87:                 SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, params.amountIn);

94:                 SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, 0);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="L-2"></a>[L-2] Use a 2-step ownership transfer pattern

Recommend considering implementing a two step process where the owner or admin nominates an account and the nominated account needs to call an `acceptOwnership()` function for the transfer of ownership to fully succeed. This ensures the nominated EOA account is a valid and active account. Lack of two-step procedure for critical operations leaves them error-prone. Consider adding two step procedure on the critical functions.

*Instances (4)*:

```solidity
File: src/InterestRateModel.sol

11: contract InterestRateModel is Ownable, IInterestRateModel, IErrors {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

24: contract V3Oracle is IV3Oracle, Ownable, IErrors {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

30: contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

19: abstract contract Automator is Swapper, Ownable {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

### <a name="L-3"></a>[L-3] Some tokens may revert when zero value transfers are made

Example: <https://github.com/d-xo/weird-erc20#revert-on-zero-value-transfers>.

In spite of the fact that EIP-20 [states](https://github.com/ethereum/EIPs/blob/46b9b698815abbfa628cd1097311deee77dd45c5/EIPS/eip-20.md?plain=1#L116) that zero-valued transfers must be accepted, some tokens, such as LEND will revert if this is attempted, which may cause transactions that involve other tokens (such as batch operations) to fully revert. Consider skipping the transfer if the amount is zero, which will also save gas.

*Instances (23)*:

```solidity
File: src/V3Vault.sol

599:         SafeERC20.safeTransfer(IERC20(asset), isTransformMode ? msg.sender : owner, assets);

728:             SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), state.liquidatorCost);

779:             SafeERC20.safeTransfer(IERC20(asset), receiver, amount);

901:             SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

946:         SafeERC20.safeTransfer(IERC20(asset), receiver, assets);

986:                 SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

226:             SafeERC20.safeTransfer(token, to, amount);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

272:         SafeERC20.safeTransfer(IERC20(token), to, amount);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

88:             SafeERC20.safeTransfer(IERC20(token0), params.recipient, amount0 - added0);

91:             SafeERC20.safeTransfer(IERC20(token1), params.recipient, amount1 - added1);

94:             SafeERC20.safeTransfer(IERC20(token), params.recipient, amount);

170:             SafeERC20.safeTransfer(IERC20(token0), params.recipient, amount0);

173:             SafeERC20.safeTransfer(IERC20(token1), params.recipient, amount1);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/transformers/V3Utils.sol

578:             SafeERC20.safeTransferFrom(token0, msg.sender, address(this), needed0);

581:             SafeERC20.safeTransferFrom(token1, msg.sender, address(this), needed1);

584:             SafeERC20.safeTransferFrom(otherToken, msg.sender, address(this), neededOther);

872:             SafeERC20.safeTransfer(token, to, amount);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

85:         SafeERC20.safeTransfer(data.asset, msg.sender, data.liquidationCost + (fee0 + fee1));

91:                 SafeERC20.safeTransfer(data.swap0.tokenIn, data.liquidator, balance);

97:                 SafeERC20.safeTransfer(data.swap1.tokenIn, data.liquidator, balance);

106:                 SafeERC20.safeTransfer(data.asset, data.liquidator, balance);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

```solidity
File: src/utils/Swapper.sol

98:                 SafeERC20.safeTransfer(params.tokenIn, universalRouter, params.amountIn);

167:         SafeERC20.safeTransfer(IERC20(tokenIn), msg.sender, amountToPay);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="L-4"></a>[L-4] Missing checks for `address(0)` when assigning values to address state variables

*Instances (6)*:

```solidity
File: src/V3Oracle.sol

81:         referenceToken = _referenceToken;

83:         chainlinkReferenceToken = _chainlinkReferenceToken;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

178:         asset = _asset;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

61:         withdrawer = _withdrawer;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/utils/Swapper.sol

45:         zeroxRouter = _zeroxRouter;

46:         universalRouter = _universalRouter;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="L-5"></a>[L-5] `decimals()` is not a part of the ERC-20 standard

The `decimals()` function is not a part of the [ERC-20 standard](https://eips.ethereum.org/EIPS/eip-20), and was added later as an [optional extension](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/IERC20Metadata.sol). As such, some valid ERC20 tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.

*Instances (4)*:

```solidity
File: src/V3Oracle.sol

82:         referenceTokenDecimals = IERC20Metadata(_referenceToken).decimals();

215:         uint8 feedDecimals = feed.decimals();

216:         uint8 tokenDecimals = IERC20Metadata(token).decimals();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

179:         assetDecimals = IERC20Metadata(_asset).decimals();

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

### <a name="L-6"></a>[L-6] Deprecated approve() function

Due to the inheritance of ERC20's approve function, there's a vulnerability to the ERC20 approve and double spend front running attack. Briefly, an authorized spender could spend both allowances by front running an allowance-changing transaction. Consider implementing OpenZeppelin's `.safeApprove()` function to help mitigate this.

*Instances (2)*:

```solidity
File: src/V3Vault.sol

520:         nonfungiblePositionManager.approve(transformer, tokenId);

537:         nonfungiblePositionManager.approve(address(0), tokenId);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

### <a name="L-7"></a>[L-7] Do not use deprecated library functions

*Instances (15)*:

```solidity
File: src/transformers/AutoCompound.sol

280:             SafeERC20.safeApprove(IERC20(token0), address(nonfungiblePositionManager), type(uint256).max);

284:             SafeERC20.safeApprove(IERC20(token1), address(nonfungiblePositionManager), type(uint256).max);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

213:             SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), state.maxAddAmount0);

214:             SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), state.maxAddAmount1);

220:             SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), 0);

221:             SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), 0);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

165:         SafeERC20.safeApprove(IERC20(token), msg.sender, amount);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/transformers/V3Utils.sol

831:             SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), 0);

832:             SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), total0);

835:             SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), 0);

836:             SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), total1);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

72:         SafeERC20.safeApprove(data.asset, address(data.vault), data.liquidationCost);

78:         SafeERC20.safeApprove(data.asset, address(data.vault), 0);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

```solidity
File: src/utils/Swapper.sol

87:                 SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, params.amountIn);

94:                 SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, 0);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="L-8"></a>[L-8] `safeApprove()` is deprecated

[Deprecated](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/bfff03c0d2a59bcd8e2ead1da9aed9edf0080d05/contracts/token/ERC20/utils/SafeERC20.sol#L38-L45) in favor of `safeIncreaseAllowance()` and `safeDecreaseAllowance()`. If only setting the initial allowance to the value that means infinite, `safeIncreaseAllowance()` can be used instead. The function may currently work, but if a bug is found in this version of OpenZeppelin, and the version that you're forced to upgrade to no longer has this function, you'll encounter unnecessary delays in porting and testing replacement contracts.

*Instances (15)*:

```solidity
File: src/transformers/AutoCompound.sol

280:             SafeERC20.safeApprove(IERC20(token0), address(nonfungiblePositionManager), type(uint256).max);

284:             SafeERC20.safeApprove(IERC20(token1), address(nonfungiblePositionManager), type(uint256).max);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

213:             SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), state.maxAddAmount0);

214:             SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), state.maxAddAmount1);

220:             SafeERC20.safeApprove(IERC20(state.token0), address(nonfungiblePositionManager), 0);

221:             SafeERC20.safeApprove(IERC20(state.token1), address(nonfungiblePositionManager), 0);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

165:         SafeERC20.safeApprove(IERC20(token), msg.sender, amount);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/transformers/V3Utils.sol

831:             SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), 0);

832:             SafeERC20.safeApprove(params.token0, address(nonfungiblePositionManager), total0);

835:             SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), 0);

836:             SafeERC20.safeApprove(params.token1, address(nonfungiblePositionManager), total1);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

72:         SafeERC20.safeApprove(data.asset, address(data.vault), data.liquidationCost);

78:         SafeERC20.safeApprove(data.asset, address(data.vault), 0);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

```solidity
File: src/utils/Swapper.sol

87:                 SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, params.amountIn);

94:                 SafeERC20.safeApprove(params.tokenIn, data.allowanceTarget, 0);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="L-9"></a>[L-9] Division by zero not prevented

The divisions below take an input parameter which does not have any zero-value checks, which may lead to the functions reverting when zero is passed.

*Instances (49)*:

```solidity
File: src/InterestRateModel.sol

50:         return debt * Q96 / (cash + debt);

67:             borrowRateX96 = (utilizationRateX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

69:             uint256 normalRateX96 = (kinkX96 * multiplierPerSecondX96 / Q96) + baseRatePerSecondX96;

71:             borrowRateX96 = (excessUtilX96 * jumpMultiplierPerSecondX96 / Q96) + normalRateX96;

74:         supplyRateX96 = utilizationRateX96 * borrowRateX96 / Q96;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

120:         value = (price0X96 * (amount0 + fees0) / Q96 + price1X96 * (amount1 + fees1) / Q96) * Q96 / priceTokenX96;

121:         feeValue = (price0X96 * fees0 / Q96 + price1X96 * fees1 / Q96) * Q96 / priceTokenX96;

122:         price0X96 = price0X96 * Q96 / priceTokenX96;

123:         price1X96 = price1X96 * Q96 / priceTokenX96;

129:         uint256 derivedPoolPriceX96 = price0X96 * Q96 / price1X96;

144:             ? (priceX96 - verifyPriceX96) * 10000 / priceX96

145:             : (verifyPriceX96 - priceX96) * 10000 / verifyPriceX96;

304:             chainlinkPriceX96 = (10 ** referenceTokenDecimals) * chainlinkPriceX96 * Q96 / chainlinkReferencePriceX96

305:                 / (10 ** feedConfig.tokenDecimals);

342:         return uint256(answer) * Q96 / (10 ** feedConfig.feedDecimals);

353:             poolTWAPPriceX96 = Q96 * Q96 / priceX96;

369:             int24 tick = int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapSeconds)));

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

769:             _convertToAssets(totalSupply(), newLendExchangeRateX96, Math.Rounding.Up) * reserveProtectionFactorX32 / Q32;

1054:                 fees0 = uint128(liquidationValue * fees0 / feeValue);

1055:                 fees1 = uint128(liquidationValue * fees1 / feeValue);

1060:                 liquidity = uint128((liquidationValue - feeValue) * liquidity / (fullValue - feeValue));

1100:         uint256 maxPenaltyValue = debt * (Q32 + MAX_LIQUIDATION_PENALTY_X32) / Q32;

1105:             uint256 startLiquidationValue = debt * fullValue / collateralValue;

1107:                 (Q96 - ((fullValue - maxPenaltyValue) * Q96 / (startLiquidationValue - maxPenaltyValue)));

1109:                 + (MAX_LIQUIDATION_PENALTY_X32 - MIN_LIQUIDATION_PENALTY_X32) * penaltyFractionX96 / Q96;

1111:             liquidationValue = debt * (Q32 + penaltyX32) / Q32;

1116:             uint256 penaltyValue = fullValue * (Q32 - MAX_LIQUIDATION_PENALTY_X32) / Q32;

1137:             newLendExchangeRateX96 = (totalLent - missing) * newLendExchangeRateX96 / totalLent;

1188:                 + oldDebtExchangeRateX96 * (block.timestamp - lastRateUpdate) * borrowRateX96 / Q96;

1190:                 + oldLendExchangeRateX96 * (block.timestamp - lastRateUpdate) * supplyRateX96 / Q96;

1230:                             > lentAssets * collateralValueLimitFactorX32 / Q32

1238:                             > lentAssets * collateralValueLimitFactorX32 / Q32

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

155:                 state.amount0 -= state.feeAmount0 * params.rewardX64 / Q64;

156:                 state.amount1 -= state.feeAmount1 * params.rewardX64 / Q64;

187:                     state.amount0 -= state.amount0 * params.rewardX64 / Q64;

189:                     state.amount1 -= state.amount1 * params.rewardX64 / Q64;

194:             state.amount0 -= (config.onlyFees ? state.feeAmount0 : state.amount0) * params.rewardX64 / Q64;

195:             state.amount1 -= (config.onlyFees ? state.feeAmount1 : state.amount1) * params.rewardX64 / Q64;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/automators/Automator.sol

187:             return (int24((tickCumulatives[0] - tickCumulatives[1]) / int56(uint56(twapPeriod))), true);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

156:             state.maxAddAmount0 = state.amount0 * Q64 / (rewardX64 + Q64);

157:             state.maxAddAmount1 = state.amount1 * Q64 / (rewardX64 + Q64);

170:                 state.amount0Fees = state.compounded0 * rewardX64 / Q64;

171:                 state.amount1Fees = state.compounded1 * rewardX64 / Q64;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

143:             state.protocolReward0 = state.feeAmount0 * params.rewardX64 / Q64;

144:             state.protocolReward1 = state.feeAmount1 * params.rewardX64 / Q64;

195:             state.maxAddAmount0 = config.onlyFees ? state.amount0 : state.amount0 * Q64 / (params.rewardX64 + Q64);

196:             state.maxAddAmount1 = config.onlyFees ? state.amount1 : state.amount1 * Q64 / (params.rewardX64 + Q64);

236:                 state.protocolReward0 = state.amountAdded0 * params.rewardX64 / Q64;

237:                 state.protocolReward1 = state.amountAdded1 * params.rewardX64 / Q64;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

### <a name="L-10"></a>[L-10] External call recipient may consume all transaction gas

There is no limit specified on the amount of gas used, so the recipient can use up all of the transaction's gas, causing it to revert. Use `addr.call{gas: <amount>}("")` or [this](https://github.com/nomad-xyz/ExcessivelySafeCall) library instead.

*Instances (5)*:

```solidity
File: src/V3Vault.sol

522:         (bool success,) = transformer.call(data);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

130:             (bool sent,) = to.call{value: balance}("");

221:             (bool sent,) = to.call{value: amount}("");

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/V3Utils.sol

867:             (bool sent,) = to.call{value: amount}("");

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/Swapper.sol

89:                 (bool success,) = zeroxRouter.call(data.data);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol)

### <a name="L-11"></a>[L-11] Signature use at deadlines should be allowed

According to [EIP-2612](https://github.com/ethereum/EIPs/blob/71dc97318013bf2ac572ab63fab530ac9ef419ca/EIPS/eip-2612.md?plain=1#L58), signatures used on exactly the deadline timestamp are supposed to be allowed. While the signature may or may not be used for the exact EIP-2612 use case (transfer approvals), for consistency's sake, all deadlines should follow this semantic. If the timestamp is an expiration rather than a deadline, consider whether it makes more sense to include the expiration timestamp as a valid timestamp, as is done for deadlines.

*Instances (1)*:

```solidity
File: src/V3Oracle.sol

338:         if (updatedAt + feedConfig.maxFeedAge < block.timestamp || answer < 0) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

### <a name="L-12"></a>[L-12] Prevent accidentally burning tokens

Minting and burning tokens to address(0) prevention

*Instances (4)*:

```solidity
File: src/V3Vault.sol

904:         _mint(receiver, shares);

945:         _burn(owner, shares);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/transformers/AutoRange.sol

217:             (state.newTokenId,, state.amountAdded0, state.amountAdded1) = nonfungiblePositionManager.mint(mintParams);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/V3Utils.sol

726:         (tokenId, liquidity, added0, added1) = nonfungiblePositionManager.mint(mintParams);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

### <a name="L-13"></a>[L-13] Possible rounding issue

Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator. Also, there is indication of multiplication and division without the use of parenthesis which could result in issues.

*Instances (1)*:

```solidity
File: src/V3Vault.sol

1137:             newLendExchangeRateX96 = (totalLent - missing) * newLendExchangeRateX96 / totalLent;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

### <a name="L-14"></a>[L-14] Loss of precision

Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator

*Instances (5)*:

```solidity
File: src/InterestRateModel.sol

95:         baseRatePerSecondX96 = baseRatePerYearX96 / YEAR_SECS;

96:         multiplierPerSecondX96 = multiplierPerYearX96 / YEAR_SECS;

97:         jumpMultiplierPerSecondX96 = jumpMultiplierPerYearX96 / YEAR_SECS;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Vault.sol

1107:                 (Q96 - ((fullValue - maxPenaltyValue) * Q96 / (startLiquidationValue - maxPenaltyValue)));

1137:             newLendExchangeRateX96 = (totalLent - missing) * newLendExchangeRateX96 / totalLent;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

### <a name="L-15"></a>[L-15] Solidity version 0.8.20+ may not work on other chains due to `PUSH0`

The compiler for Solidity 0.8.20 switches the default target EVM version to [Shanghai](https://blog.soliditylang.org/2023/05/10/solidity-0.8.20-release-announcement/#important-note), which includes the new `PUSH0` op code. This op code may not yet be implemented on all L2s, so deployment on these chains will fail. To work around this issue, use an earlier [EVM](https://docs.soliditylang.org/en/v0.8.20/using-the-compiler.html?ref=zaryabs.com#setting-the-evm-version-to-target) [version](https://book.getfoundry.sh/reference/config/solidity-compiler#evm_version). While the project itself may or may not compile with 0.8.20, other projects with which it integrates, or which extend this project may, and those projects will have problems deploying these contracts/libraries.

*Instances (9)*:

```solidity
File: src/InterestRateModel.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/transformers/AutoCompound.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/transformers/V3Utils.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

### <a name="L-16"></a>[L-16] Use `Ownable2Step.transferOwnership` instead of `Ownable.transferOwnership`

Use [Ownable2Step.transferOwnership](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable2Step.sol) which is safer. Use it as it is more secure due to 2-stage ownership transfer.

**Recommended Mitigation Steps**

Use <a href="https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable2Step.sol">Ownable2Step.sol</a>
  
  ```solidity
      function acceptOwnership() external {
          address sender = _msgSender();
          require(pendingOwner() == sender, "Ownable2Step: caller is not the new owner");
          _transferOwnership(sender);
      }
```

*Instances (4)*:

```solidity
File: src/InterestRateModel.sol

4: import "@openzeppelin/contracts/access/Ownable.sol";

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

15: import "@openzeppelin/contracts/access/Ownable.sol";

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

16: import "@openzeppelin/contracts/access/Ownable.sol";

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

4: import "@openzeppelin/contracts/access/Ownable.sol";

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

### <a name="L-17"></a>[L-17] File allows a version of solidity that is susceptible to an assembly optimizer bug

In solidity versions 0.8.13 and 0.8.14, there is an [optimizer bug](https://github.com/ethereum/solidity-blog/blob/499ab8abc19391be7b7b34f88953a067029a5b45/_posts/2022-06-15-inline-assembly-memory-side-effects-bug.md) where, if the use of a variable is in a separate `assembly` block from the block in which it was stored, the `mstore` operation is optimized out, leading to uninitialized memory. The code currently does not have such a pattern of execution, but it does use `mstore`s in `assembly` blocks, so it is a risk for future changes. The affected solidity versions should be avoided if at all possible.

*Instances (9)*:

```solidity
File: src/InterestRateModel.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/AutoExit.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol)

```solidity
File: src/transformers/AutoCompound.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

```solidity
File: src/transformers/AutoRange.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol)

```solidity
File: src/transformers/LeverageTransformer.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

```solidity
File: src/transformers/V3Utils.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

```solidity
File: src/utils/FlashloanLiquidator.sol

2: pragma solidity ^0.8.0;

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol)

### <a name="L-18"></a>[L-18] Consider using OpenZeppelin's SafeCast library to prevent unexpected overflows when downcasting

Downcasting from `uint256`/`int256` in Solidity does not revert on overflow. This can result in undesired exploitation or bugs, since developers usually assume that overflows raise errors. [OpenZeppelin's SafeCast library](https://docs.openzeppelin.com/contracts/3.x/api/utils#SafeCast) restores this intuition by reverting the transaction when such an operation overflows. Using this library eliminates an entire class of bugs, so it's recommended to use it always. Some exceptions are acceptable like with the classic `uint256(uint160(address(variable)))`

*Instances (12)*:

```solidity
File: src/V3Oracle.sol

467:         fees0 = uint128(FullMath.mulDiv(feeGrowth0, position.liquidity, Q128));

468:         fees1 = uint128(FullMath.mulDiv(feeGrowth1, position.liquidity, Q128));

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

36:     uint32 public constant MAX_COLLATERAL_FACTOR_X32 = uint32(Q32 * 90 / 100); // 90%

38:     uint32 public constant MIN_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 2 / 100); // 2%

39:     uint32 public constant MAX_LIQUIDATION_PENALTY_X32 = uint32(Q32 * 10 / 100); // 10%

41:     uint32 public constant MIN_RESERVE_PROTECTION_FACTOR_X32 = uint32(Q32 / 100); //1%

43:     uint32 public constant MAX_DAILY_LEND_INCREASE_X32 = uint32(Q32 / 10); //10%

44:     uint32 public constant MAX_DAILY_DEBT_INCREASE_X32 = uint32(Q32 / 10); //10%

1054:                 fees0 = uint128(liquidationValue * fees0 / feeValue);

1055:                 fees1 = uint128(liquidationValue * fees1 / feeValue);

1060:                 liquidity = uint128((liquidationValue - feeValue) * liquidity / (fullValue - feeValue));

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/transformers/AutoCompound.sol

47:     uint64 public constant MAX_REWARD_X64 = uint64(Q64 / 50); // 2%

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

### <a name="L-19"></a>[L-19] Unsafe ERC20 operation(s)

*Instances (2)*:

```solidity
File: src/V3Vault.sol

520:         nonfungiblePositionManager.approve(transformer, tokenId);

537:         nonfungiblePositionManager.approve(address(0), tokenId);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

### <a name="L-20"></a>[L-20] Upgradeable contract not initialized

Upgradeable contracts are initialized via an initializer function rather than by a constructor. Leaving such a contract uninitialized may lead to it being taken over by a malicious user

*Instances (2)*:

```solidity
File: src/V3Oracle.sol

177:         PositionState memory state = _initializeState(tokenId);

395:     function _initializeState(uint256 tokenId) internal view returns (PositionState memory state) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

## Medium Issues

| |Issue|Instances|
|-|:-|:-:|
| [M-1](#M-1) | Contracts are vulnerable to fee-on-transfer accounting-related issues | 6 |
| [M-2](#M-2) | Centralization Risk for trusted owners | 18 |
| [M-3](#M-3) | `increaseAllowance/decreaseAllowance` won't work on mainnet for USDT | 2 |
| [M-4](#M-4) | Chainlink's `latestRoundData` might return stale or incorrect results | 1 |
| [M-5](#M-5) | Missing checks for whether the L2 Sequencer is active | 1 |

### <a name="M-1"></a>[M-1] Contracts are vulnerable to fee-on-transfer accounting-related issues

Consistently check account balance before and after transfers for Fee-On-Transfer discrepancies. As arbitrary ERC20 tokens can be used, the amount here should be calculated every time to take into consideration a possible fee-on-transfer or deflation.
Also, it's a good practice for the future of the solution.

Use the balance before and after the transfer to calculate the received amount instead of assuming that it would be equal to the amount passed as a parameter. Or explicitly document that such tokens shouldn't be used and won't be supported

*Instances (6)*:

```solidity
File: src/V3Vault.sol

728:             SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), state.liquidatorCost);

901:             SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

986:                 SafeERC20.safeTransferFrom(IERC20(asset), msg.sender, address(this), assets);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/transformers/V3Utils.sol

578:             SafeERC20.safeTransferFrom(token0, msg.sender, address(this), needed0);

581:             SafeERC20.safeTransferFrom(token1, msg.sender, address(this), needed1);

584:             SafeERC20.safeTransferFrom(otherToken, msg.sender, address(this), neededOther);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol)

### <a name="M-2"></a>[M-2] Centralization Risk for trusted owners

#### Impact

Contracts have owners with privileged rights to perform admin tasks and need to be trusted to not perform malicious updates or drain funds.

*Instances (18)*:

```solidity
File: src/InterestRateModel.sol

11: contract InterestRateModel is Ownable, IInterestRateModel, IErrors {

87:     ) public onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol)

```solidity
File: src/V3Oracle.sol

24: contract V3Oracle is IV3Oracle, Ownable, IErrors {

185:     function setMaxPoolPriceDifference(uint16 _maxPoolPriceDifference) external onlyOwner {

209:     ) external onlyOwner {

265:     function setEmergencyAdmin(address admin) external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

```solidity
File: src/V3Vault.sol

30: contract V3Vault is ERC20, Multicall, Ownable, IVault, IERC721Receiver, IErrors {

765:     function withdrawReserves(uint256 amount, address receiver) external onlyOwner {

788:     function setTransformer(address transformer, bool active) external onlyOwner {

837:     function setReserveFactor(uint32 _reserveFactorX32) external onlyOwner {

844:     function setReserveProtectionFactor(uint32 _reserveProtectionFactorX32) external onlyOwner {

870:     function setEmergencyAdmin(address admin) external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol)

```solidity
File: src/automators/Automator.sol

19: abstract contract Automator is Swapper, Ownable {

59:     function setWithdrawer(address _withdrawer) public onlyOwner {

69:     function setOperator(address _operator, bool _active) public onlyOwner {

79:     function setVault(address _vault, bool _active) public onlyOwner {

87:     function setTWAPConfig(uint16 _maxTWAPTickDifference, uint32 _TWAPSeconds) public onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol)

```solidity
File: src/transformers/AutoCompound.sol

243:     function setReward(uint64 _totalRewardX64) external onlyOwner {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol)

### <a name="M-3"></a>[M-3] `increaseAllowance/decreaseAllowance` won't work on mainnet for USDT

On mainnet, the mitigation to be compatible with `increaseAllowance/decreaseAllowance` isn't applied: <https://etherscan.io/token/0xdac17f958d2ee523a2206206994597c13d831ec7#code>, meaning it reverts on setting a non-zero & non-max allowance, unless the allowance is already zero.

*Instances (2)*:

```solidity
File: src/transformers/LeverageTransformer.sol

77:         SafeERC20.safeIncreaseAllowance(IERC20(token0), address(nonfungiblePositionManager), amount0);

78:         SafeERC20.safeIncreaseAllowance(IERC20(token1), address(nonfungiblePositionManager), amount1);

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol)

### <a name="M-4"></a>[M-4] Chainlink's `latestRoundData` might return stale or incorrect results

- This is a common issue: <https://github.com/code-423n4/2022-12-tigris-findings/issues/655>, <https://code4rena.com/reports/2022-10-inverse#m-17-chainlink-oracle-data-feed-is-not-sufficiently-validated-and-can-return-stale-price>, <https://app.sherlock.xyz/audits/contests/41#issue-m-12-chainlinks-latestrounddata--return-stale-or-incorrect-result> and many more occurrences.

`latestRoundData()` is used to fetch the asset price from a Chainlink aggregator, but it's missing additional validations to ensure that the round is complete. If there is a problem with Chainlink starting a new round and finding consensus on the new value for the oracle (e.g. Chainlink nodes abandon the oracle, chain congestion, vulnerability/attacks on the Chainlink system) consumers of this contract may continue using outdated stale data / stale prices.

More bugs related to chainlink here: [Chainlink Oracle Security Considerations](https://medium.com/cyfrin/chainlink-oracle-defi-attacks-93b6cb6541bf#99af)

*Instances (1)*:

```solidity
File: src/V3Oracle.sol

337:         (, int256 answer,, uint256 updatedAt,) = feedConfig.feed.latestRoundData();
             if (updatedAt + feedConfig.maxFeedAge < block.timestamp || answer < 0) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)

### <a name="M-5"></a>[M-5] Missing checks for whether the L2 Sequencer is active

Chainlink recommends that users using price oracles, check whether the Arbitrum Sequencer is [active](https://docs.chain.link/data-feeds/l2-sequencer-feeds#arbitrum). If the sequencer goes down, the Chainlink oracles will have stale prices from before the downtime, until a new L2 OCR transaction goes through. Users who submit their transactions via the [L1 Dealyed Inbox](https://developer.arbitrum.io/tx-lifecycle#1b--or-from-l1-via-the-delayed-inbox) will be able to take advantage of these stale prices. Use a [Chainlink oracle](https://blog.chain.link/how-to-use-chainlink-price-feeds-on-arbitrum/#almost_done!_meet_the_l2_sequencer_health_flag) to determine whether the sequencer is offline or not, and don't allow operations to take place while the sequencer is offline.

*Instances (1)*:

```solidity
File: src/V3Oracle.sol

337:         (, int256 answer,, uint256 updatedAt,) = feedConfig.feed.latestRoundData();
             if (updatedAt + feedConfig.maxFeedAge < block.timestamp || answer < 0) {

```

[Link to code](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol)
