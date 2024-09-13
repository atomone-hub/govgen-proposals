# AtomOne Tokenomics

AtomOne is a proof-of-stake blockchain initially forked from [Cosmos Hub](https://github.com/cosmos/gaia) and incorporating significant design improvements. These improvements include a dual token model, an innovative implementation of Interchain Security, a revamped validator selection and a substantial redesign of the chain’s governance and DAO structure.  

This proposed AtomOne Tokenomics aims to highlight the innovative aspects of this design and explain the newly introduced concepts.

## Dual Token Model

The AtomOne chain uses two tokens, ATONE and PHOTON, each fulfilling distinct roles to ensure the chain’s security and efficient transaction processing.

1. **ATONE \- The Native Staking and Governance Token**

ATONE is the native staking and governance token of the AtomOne chain that is used to secure the network through a Proof of Stake (PoS) mechanism. Stakers of ATONE are rewarded with newly generated tokens as inflation to incentivize participation in the network’s security. Non-stakers experience a dilution of their holdings due to this inflationary mechanism.  
* **Staking and Inflation:** By staking ATONE, users participating in securing the network will be rewarded with inflationary ATONE tokens. The inflation rate is dynamic, targeting a staking participation rate of 2/3 of all ATONEs. The maximum inflation rate is capped at 20% annually (non-compounded), with no minimum rate, allowing for potential deflation. ICA staking will be forbidden.  
* **Economic Incentives:** Staked ATONE functions as voting shares, economic incentive shares, and security bonds. The inflation rewards and transaction fees minus taxes are distributed proportionally based on each delegator's staking amount, and staked ATONE is converted into Bonded Share Units.  
* **Unbonding and Redelegation:** The unbonding period for ATONE is set at a minimum of 3 weeks. Redelegation of staked ATONE will be permitted up to twice per unbonding period.  
* **Utility:** ATONE is a token specifically designed for staking to support the governance of the AtomOne Hub. The token's primary role is to secure the network and support community participation in governance, as such it is not meant to function as a general medium of exchange or as a store of value. While ATONE will be transferable, its intended purpose and functionality is to support the decentralized governance and management of the AtomOne Hub, setting it apart from traditional money or securities.  

2. **PHOTON \- The Fee Token**

PHOTON serves as the transaction fee token for the initial AtomOne chain and for the future AtomOne Hub. It is the sole fee token for all transactions on the root and core shards, as well as for Inter-Blockchain Communication (IBC) and Interchain Security (ICS) payments. 
* **Fee Structure:** PHOTON is required for all transaction fees, except for ATONE to PHOTON burn transactions, where ATONE can be used for the burn-related fees.  
* **Conversion Mechanism:** PHOTON tokens can be acquired by burning ATONE tokens at a predetermined dynamic conversion rate. This conversion is one-way, meaning once ATONE is burned to create PHOTON, it cannot be reverted back. At any moment if all ATONE were burned to PHOTON, there would be a total of 1 billion PHOTON. The conversion rate for burning X ATONE is equal to (1 billion PHOTON \- existing PHOTON) \* X / (existing ATONE).  
* **Utility:** PHOTON is a token specifically created to be the sole fee token of the entire AtomOne Hub. While the only way to mint PHOTON is by burning ATONE, after minting the PHOTON token is expected to be transferable.
<br>

## Supply and Distribution

* **Initial Supply:** At genesis, approximately 107 million ATONE tokens (specifically, 107,775,332 ATONE) will be minted and distributed via airdrop to Cosmos Hub addresses based on a predefined distribution proposal and governance approved criteria as described in the following proposal \[[read draft proposal](https://github.com/atomone-hub/govgen-proposals/blob/main/001\_ATONE\_DISTRIBUTION.md)\].  
* **Burn-to-Mint Mechanism:** The only way to mint PHOTON tokens is through the burning of ATONE tokens. The total mintable PHOTON supply is capped at 1 billion tokens. This mechanism ensures a controlled and transparent supply of PHOTON, tied directly to the burning of ATONE.  
* **Non-Reversible Burn:** Once ATONE tokens are converted into PHOTON, they cannot be converted back. This one-way conversion helps in maintaining the economic structure and stability of the AtomOne chain.
<br>

## AtomOne Hub and Interchain Security (ICS)

The AtomOne Hub comprises multiple chains, including:
* **Root Hub Chain:** The AtomOne chain, where staking and governance transactions occur.  
* **Core Shards:** Chains secured by Interchain Security (ICS) and governed by the root hub chain.  
* **Consumer Shards:** Other sovereign zones that are partially or fully secured by AtomOne Hub ICS but maintain their own governance mechanisms.
<br>

## ICS Design and Governance:

* **ICS Implementation:** The AtomOne chain will develop the ICS design that will allow the AtomOne chain to become the AtomOne ICS Hub. ICS functionality activation within the AtomOne chain is subject to AtomOne governance approval.  
* **ICS Fees in PHOTON:** Core shards and consumer shards will pay their ICS fees in PHOTON for the security services provided by the AtomOne Hub. ICS fees can be collected directly per transaction or paid by the consumer chain directly via Interchain Accounts (ICA) at predefined epochs.  
* **Fee Distribution:** The ICS fees will be collected in a decentralized body such as an on-chain community pool, a Decentralized Autonomous Organization (DAO) governed by the community, or a decentralized elected decision making authority that will decide upon their future use and distribution among the different network participants of the AtomOne chain (such as validators, contributors, stakers or others). The future spends of the ICS fees will be determined through governance proposals and/or through a mechanism defined by a specific law.
