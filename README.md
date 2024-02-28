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

[ ⭐️ SPONSORS: Are there any known issues or risks deemed acceptable that shouldn't lead to a valid finding? If so, list them here. ]


# Overview

[ ⭐️ SPONSORS: add info here ]

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

- [ ] Describe any novel or unique curve logic or mathematical models implemented in the contracts
- [ ] Please list specific ERC20 that your protocol is anticipated to interact with. Could be "any" (literally anything, fee on transfer tokens, ERC777 tokens and so forth) or a list of tokens you envision using on launch.
- [ ] Please list specific ERC721 that your protocol is anticipated to interact with.
- [ ] Which blockchains will this code be deployed to, and are considered in scope for this audit?
- [ ] Please list all trusted roles (e.g. operators, slashers, pausers, etc.), the privileges they hold, and any conditions under which privilege escalation is expected/allowable
- [ ] In the event of a DOS, could you outline a minimum duration after which you would consider a finding to be valid? This question is asked in the context of most systems' capacity to handle DoS attacks gracefully for a certain period.
- [ ] Is any part of your implementation intended to conform to any EIP's? If yes, please list the contracts in this format: 
  - `Contract1`: Should comply with `ERC/EIPX`
  - `Contract2`: Should comply with `ERC/EIPY`

## Attack ideas (Where to look for bugs)
*List specific areas to address - see [this blog post](https://medium.com/code4rena/the-security-council-elections-within-the-arbitrum-dao-a-comprehensive-guide-aa6d001aae60#9adb) for an example*

## Main invariants
*Describe the project's main invariants (properties that should NEVER EVER be broken).*

## Scoping Details 
```
- If you have a public code repo, please share it here: https://github.com/revert-finance/vault (private for now)   
- How many contracts are in scope?: 11   
- Total SLoC for these contracts?: 3000  
- How many external imports are there?: 10  
- How many separate interfaces and struct definitions are there for the contracts within scope?: 4  
- Does most of your code generally use composition or inheritance?: Composition   
- How many external calls?: 10   
- What is the overall line coverage percentage provided by your tests?: 80
- Is this an upgrade of an existing system?:
- Check all that apply (e.g. timelock, NFT, AMM, ERC20, rollups, etc.): NFT, AMM, ERC-20 Token  
- Is there a need to understand a separate part of the codebase / get context in order to audit this part of the protocol?: False  
- Please describe required context:   
- Does it use an oracle?: Chainlink, Uniswap V3 TWAP
- Describe any novel or unique curve logic or mathematical models your code uses: No 
- Is this either a fork of or an alternate implementation of another project?: False  
- Does it use a side-chain?:
- Describe any specific areas you would like addressed:
```

# Tests

*Provide every step required to build the project from a fresh git clone, as well as steps to run the tests with a gas report.* 

*Note: Many wardens run Slither as a first pass for testing.  Please document any known errors with no workaround.* 

## Miscellaneous

Employees of Revert and employees' family members are ineligible to participate in this audit.
