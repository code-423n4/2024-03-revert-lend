# Revert Lend audit details
- Total Prize Pool: $88,500 in USDC
  - HM awards: $42,900 in USDC
  - Analysis awards: $2,600 in USDC
  - QA awards: $1,300 in USDC
  - Bot Race awards: $3,900 in USDC
  - Gas awards: $1,300 in USDC
  - Judge awards: $29,450 in USDC
  - Lookout awards: $4,200 USDC (Notion: Sum of Pre-sort fee + Pre-sort early bonus)
  - Scout awards: $500 in USDC
  - Mitigation Review: $2,350 in USDC (*Opportunity goes to top 3 certified wardens based on placement in this audit.*)
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2024-03-revert-lend/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts March 4, 2024 20:00 UTC
- Ends March 15, 2024 20:00 UTC

## Automated Findings / Publicly Known Issues

The 4naly3er report can be found [here](https://github.com/code-423n4/2024-03-revert-lend/blob/main/4naly3er-report.md).

Automated findings output for the audit can be found [here](https://github.com/code-423n4/2024-03-revert-lend/blob/main/bot-report.md) within 24 hours of audit opening.

_Note for C4 wardens: Anything included in this `Automated Findings / Publicly Known Issues` section is considered a publicly known issue and is ineligible for awards._

Note from Revert:

Liquidations of undercollateralized positions may be temporarly disabled when the pool price of a position is moved away too much from the oracle price. This issue is automatically resolved by arbitrage in most cases, but if there is not enough incentive to do so, the liquiditor has enough incentive to do the arbitrage as part of the liquidation process - because of the liquidation premium. For more details see Finding 4 in the audit by Hydn (see below).

# Overview

This repository contains the smart contracts for Revert Lend protocol.

It uses Foundry as development toolchain.

To get an understanding of the basic concepts, and advanced topics like transformers please read the whitepaper.

## Links

- **Previous audits:** 
[Hydn](https://github.com/code-423n4/2024-03-revert-lend/blob/main/audits/HYDN_-_Revert_Finance_Vault_Audit_Report.docx.pdf)

- **Documentation:**
[Whitepaper](https://github.com/revert-finance/lend-whitepaper/blob/main/Revert_Lend-wp.pdf)

- **Website:**
[revert.finance](https://revert.finance)

- **Twitter:** 
[@revertfinance](https://twitter.com/revertfinance)

- **Discord:**
[Revert Discord](https://discord.gg/KZexNMsS)


# Scope

| Contract | SLOC | Purpose | Libraries used |  
| ----------- | ----------- | ----------- | ----------- |
| [src/V3Vault.sol](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Vault.sol) | 887 | Vault contract which keeps V3 Positions, lent assets and handles loans. | [`@openzeppelin`](https://github.com/OpenZeppelin/openzeppelin-contracts) [`@v3-core`](https://github.com/Uniswap/v3-core) [`@v3-periphery`](https://github.com/Uniswap/v3-periphery) [`@permit2`](https://github.com/uniswap/permit2) |
| [src/V3Oracle.sol](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/V3Oracle.sol) | 371 | Oracle which handles Chainlink Feeds, Uniswap V3 TWAPs to get values of V3 Positions | [`@openzeppelin`](https://github.com/OpenZeppelin/openzeppelin-contracts) [`@v3-core`](https://github.com/Uniswap/v3-core) [`@v3-periphery`](https://github.com/Uniswap/v3-periphery) [`@chainlink`](https://github.com/smartcontractkit/chainlink) |
| [src/InterestRateModel.sol](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/InterestRateModel.sol) | 65 | Calculates interest rates for V3Vault | [`@openzeppelin`](https://github.com/OpenZeppelin/openzeppelin-contracts) |
| [src/automators/AutoExit.sol](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/AutoExit.sol) | 185 | Lets Revert controlled bot auto-exit positions | [`@openzeppelin`](https://github.com/OpenZeppelin/openzeppelin-contracts) [`@v3-core`](https://github.com/Uniswap/v3-core) [`@v3-periphery`](https://github.com/Uniswap/v3-periphery) |
| [src/automators/Automator.sol](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/automators/Automator.sol) | 181 | Base class which adds handling of operator, fees and permissions for automator contracts. | [`@openzeppelin`](https://github.com/OpenZeppelin/openzeppelin-contracts) [`@v3-core`](https://github.com/Uniswap/v3-core) [`@v3-periphery`](https://github.com/Uniswap/v3-periphery) |
| [src/transformers/AutoCompound.sol](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoCompound.sol) | 200 | Lets Revert controlled bot auto-compound positions (also when they are used as collateral) | [`@openzeppelin`](https://github.com/OpenZeppelin/openzeppelin-contracts) [`@v3-core`](https://github.com/Uniswap/v3-core) [`@v3-periphery`](https://github.com/Uniswap/v3-periphery) |
| [src/transformers/AutoRange.sol](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/AutoRange.sol) | 235 | Lets Revert controlled bot auto-range positions (also when they are used as collateral) | [`@openzeppelin`](https://github.com/OpenZeppelin/openzeppelin-contracts) [`@v3-core`](https://github.com/Uniswap/v3-core) [`@v3-periphery`](https://github.com/Uniswap/v3-periphery) |
| [src/transformers/LeverageTransformer.sol](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/LeverageTransformer.sol) | 133 | Lets positions being leveraged by borrowing, swapping and readding to collateralized position atomically. Also supports deleveraging. | [`@openzeppelin`](https://github.com/OpenZeppelin/openzeppelin-contracts) [`@v3-core`](https://github.com/Uniswap/v3-core) [`@v3-periphery`](https://github.com/Uniswap/v3-periphery) |
| [src/transformers/V3Utils.sol](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/transformers/V3Utils.sol) | 750 | V3Utils contract (atomic swap and manage liquidity functions) which works with V3Vault and supports Permit2. | [`@openzeppelin`](https://github.com/OpenZeppelin/openzeppelin-contracts) [`@v3-core`](https://github.com/Uniswap/v3-core) [`@v3-periphery`](https://github.com/Uniswap/v3-periphery) [`@permit2`](https://github.com/uniswap/permit2) |
| [src/utils/FlashloanLiquidator.sol](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/FlashloanLiquidator.sol) | 89 | Util contract to do atomic liquidations using a Uniswap V3 Flashloan | [`@openzeppelin`](https://github.com/OpenZeppelin/openzeppelin-contracts) [`@v3-core`](https://github.com/Uniswap/v3-core) [`@v3-periphery`](https://github.com/Uniswap/v3-periphery) |
| [src/utils/Swapper.sol](https://github.com/code-423n4/2024-03-revert-lend/blob/main/src/utils/Swapper.sol) | 118 | Base class which adds logic for doing swaps with UniversalRouter, 0x Router and pool swaps. | [`@openzeppelin`](https://github.com/OpenZeppelin/openzeppelin-contracts) [`@v3-core`](https://github.com/Uniswap/v3-core) [`@v3-periphery`](https://github.com/Uniswap/v3-periphery) |


## Out of scope

Everything NOT in /src

# Additional Context

- Roles in the protocol: Owner (which will be set to a Multisig and Timelock), EmergencyAdmin (which will be set to a Multisig), Operators (which are EOA used by bots to call actions in Automator contracts)

- Special ERC20 tokens like fee-on-transfer or rebasing tokens are not supported. Usage of them will revert.

- The only allowed ERC721 are UniswapV3 positions.

- The protocol should be able to be deployed on any EVM compatible chain - by using chain specific config values

- `V3Vault`: Should comply with `ERC/EIP4626`


## Attack ideas (Where to look for bugs)
- Reentrancy
- Share calculation
- Price manipulation
- Crafted ERC-20 Tokens
- Crafted external swap calldata

## Main invariants
- Debt can never be bigger than lent assets (after all loans are payed back or liquidated).

## Scoping Details 
```
- If you have a public code repo, please share it here: https://github.com/revert-finance/vault (private for now)   
- How many contracts are in scope?: 11   
- Total SLoC for these contracts?: 3000  
- How many external imports are there?: 10  
- How many separate interfaces and struct definitions are there for the contracts within scope?: 4  
- Does most of your code generally use composition or inheritance?: both   
- How many external calls?: 10   
- What is the overall line coverage percentage provided by your tests?: 80
- Is this an upgrade of an existing system?: No
- Check all that apply (e.g. timelock, NFT, AMM, ERC20, rollups, etc.): NFT, AMM, ERC-20 Token  
- Is there a need to understand a separate part of the codebase / get context in order to audit this part of the protocol?: UniswapV3, Permit2  
- Does it use an oracle?: Chainlink, Uniswap V3 TWAP
- Describe any novel or unique curve logic or mathematical models your code uses: No 
- Is this either a fork of or an alternate implementation of another project?: False  
- Does it use a side-chain?: No
```

# Tests

First time run 

```sh
forge install
```

to get dependencies. Then:

Because the v3-periphery library (Solidity v0.8 branch) in lib/v3-periphery/contracts/libraries/PoolAddress.sol has a different POOL_INIT_CODE_HASH than the one deployed on Mainnet this needs to be changed for the integration tests to work properly and for deployment!

bytes32 internal constant POOL_INIT_CODE_HASH = 0xa598dd2fba360510c5a8f02f44423a4468e902df5857dbce3ca162a43a3a31ff;

needs to be changed to 

bytes32 internal constant POOL_INIT_CODE_HASH = 0xe34f199b19b2b4f47f68442619d555527d244f78a3297ea89325f843f87b8b54;

Most tests use a forked state of Ethereum Mainnet. You can run all tests with: 

```sh
forge test
```


## Miscellaneous

Employees of Revert and employees' family members are ineligible to participate in this audit.
