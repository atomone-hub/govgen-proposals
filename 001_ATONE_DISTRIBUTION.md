# Proposal 001: Equitable ATONE Distribution in the Spirit of AtomOne's Founding Principles

## Changelog

* March 13th 2024: first draft
* March 14th 2024: add data and code
* March 21st 2024: update distribution to ensure non-voters do not exceed 1/3 of ATONE supply
* March 21st 2024: reduce the final supply by a factor of 10.
* March 28th 2024: update the base multiplier for *No* and *NWV* votes to x9
* April 3rd 2024: further text refinements for clarity and formality
* April 9th 2024: added disclaimer and clarifications on bonus and malus
* August 14th 2024: add Community Pool section and Vesting accounts note
* September 5th 2024: Update status to "Under review"
* September 13th 2024: Update status to "On Chain"

## Status

On Chain

## Summary

This proposal seeks to establish a fair and principled distribution mechanism 
for ATONE, the native token of the AtomOne chain, reflecting the foundational 
principles as outlined in the AtomOne 
[founding documents](https://github.com/atomone-hub/genesis).
The proposal tries to synthesize the 
[discussion](https://github.com/atomone-hub/genesis/issues/12)
around the ATONE distribution, and leveraging the snapshot from Cosmos Hub's
[proposal 848](https://www.mintscan.io/cosmos/proposals/848), 
it aims to reward participation and engagement while adhering to AtomOne's ethos
of intelligent distribution and governance.

> [!NOTE]
> This "*Sentiment Proposal*" is intended solely to assess the opinions and
> ideas of the GovGen community regarding the future of AtomOne.
> As such, the results of the vote on this Sentiment Proposal are not intended 
> to be, and will not be, binding or determinative in any way.
> 
> It is the proposal submitter's understanding and hope that the GovGen
> community will be able to use the results of this and other Sentiment
> Proposals to develop in the future a binding decision-making/governance
> process to be determined (potentially including an upgrade to GovGen's
> software) with a goal of shaping the potential AtomOne chain. At this early
> stage, this and other Sentiment Proposals are anticipated to be introduced
> with an intention to better understand the GovGen community’s general
> preferences and views, and also to measure the ratio of active participants
> to help determine the quorum for future proposals.

## Context

AtomOne's inception was driven by fundamental disagreements within the Cosmos
Hub's community, particularly regarding the nature of ATOM as a staking versus
monetary token and the broader vision for the network's future
[1](https://github.com/atomone-hub/genesis/blob/main/README.md)
[2](https://github.com/atomone-hub/genesis/blob/main/STAKING_VS_MONEY.md).
Proposal 848's passage, advocating for ATOM's "*halving*" without adequately
addressing security concerns, marked a pivotal moment that underscored the
necessity for AtomOne. AtomOne is thus not merely a technical divergence but
rather a philosophical stand for a network that remains true to the principles
of minimalism in its IBC/ICS hub functionality, robust security model, and an
intelligent, aligned community governance structure.

## Decision

In accordance with AtomOne's foundational principles and the discussions
surrounding the token distribution, we propose the ATONE distribution mechanism
outlined below, reflecting an attempt to create a balanced approach that rewards
participation, engagement, and alignment with AtomOne's vision. The intent of
the distribution mechanism is to *increase* the percentage ownership in the
network for the *NO* and *No With Veto* (NWV) votes on proposal 848, but to also
ensures that the percentage ownership of the non-voting categories does not
exceed a fixed 1/3 of the total supply. A decimation factor is also applied at
the end to reduce the total supply by a factor of 10.

**Note that, in addition, it is proposed that the ICF will be entirely slashed**.
However, we propose to mint some funds for the development of the chain
ecosystem, see the [Community Pool & reserved address](#community-pool--reserved-address)
section for more details.

> [!NOTE]
> We specifically refer to the *ATOM that voted* on proposal 848, and not
> accounts, to accurately reflect how the distribution mechanism will work,
> which also mirrors in practice how the `x/gov` tally works on the Cosmos Hub.
> The final balance for each account will be the result of the contributions
> from each ATOM with which the account either voted (and how), or did not.

> [!NOTE]
> In the context of this proposal, the term *voting* ATOM is intended to refer
> to ATOM that was used to vote on proposal 848 either directly or indirectly
> via delegation. A *non-voting* ATOM is ATOM that was not used to vote either
> directly or indirectly because the validator it is delegated to also did not
> vote.

> [!IMPORTANT]
> The following proposed mechanism does not explicitly account for the `K = 0.1`
> decimation factor. This factor is considered implicit as it will be applied
> indiscriminately alongside any other category-specific multiplier

1. **YES Votes to Proposal 848**: standard 1x multiplier for the ATOM that
   voted *YES* at the snapshot.

2. **NO and NWV Votes to Proposal 848**: 
   1. Acknowledged with a 8x multiplier on top of the ATOM that voted *NO* and
   *NWV*, emphasizing the critical stance against the monetary token proposition
   and alignment with AtomOne's security philosophy. The resulting balance will
   essentially be 9x the original ATOM balance.

   2. Plus, the ATOM that voted *NWV* will also get a 3% bonus on top in
   order to (slightly) reward the stronger political stance.

3. **ABSTAIN Votes to Proposal 848**: Assigned a multiplier `C` that ensures
   that the total percentage ownership of the *Abstain*, *Did Not Vote* (DNV)
   and *Not Staked* categories does not exceed a target percentage `t` of 1/3:
   ```math
   C = (t / (1 - t)) * ((y + 9n + 9nwv) / (a + dnv + u))
   ```
   where:
   - `C` is the multiplier to be found
   - `t` is the target percentage for the *non-voting* categories, which is *33%*.
   - `y` represents the total ATOM that voted *Yes*
   - `a` represents the total ATOM that voted *Abstain*
   - `n` represents the total ATOM that voted *No*
   - `nwv` represents the total ATOM that voted *No With Veto*
   - `dnv` represents the total ATOM that *Did Not Vote*
   - `u` represents the total ATOM that *Unbonded* (*Not Staked*)

4. **Did not vote (DNV) on Proposal 848**: It is considered to be *non-voting*
   the ATOM that did not vote at all (even through its delegations). The ATOM
   that *DNV* get the same multiplier as ATOM that voted *Abstain*, but they
   incur in an additional 3% malus to (slightly) punish inactivity.

5. **Unbonded ATOM (Not Staked)**: will equate to the *non-voting* category and
   receive the same multiplier as ATOM that *DNV*.

> [!NOTE]
> An account that has voted indirectly through its delegations may see its
> balance affected by different multipliers depending on the votes of its
> delegations.
> The same reasoning applies in the case of *weighted* votes.
> Moreover, it is always the case that for any account that has both bonded as
> well as unbonded ATOM, the resulting ATONE balance will come from the
> contribution of each part as already discussed.

> [!NOTE]
> For this ATONE distribution, all Cosmos Hub's vesting accounts will be
> considered as normal accounts meaning that the ATONE equivalent for those
> Cosmos Hub (ATOM) vested tokens will be immediately available in AtomOne. Any
> votes from staked vested tokens will be treated by the distribution algorithm
> similarly to normal staked tokens.

The following table is also provided for a quick recap:

|                     |  DNV      | YES | ABSTAIN | NO |    NWV    |
|---------------------|-----------|-----|---------|----|-----------|
| Bonded multiplier   | C x malus |  1  |    C    | 9  | 9 x bonus |
| Unbonded multiplier | C x malus |  -  |    -    | -  |     -     |

> [!NOTE]
> *bonus* and *malus* are multipliers, respectively equal to `1.03` and `0.97`
> as per the above specifications. These multipliers incorporate the original
> quantity and the actual bonus/malus, i.e. they are computed as `1 + 0.03` and
> `1 - 0.03` respectively.

Accompanying code that implements the proposed distribution mechanism is
available at [https://github.com/atomone-hub/govbox](https://github.com/atomone-hub/govbox). Please refer to the 
[PROP-001.md](https://github.com/atomone-hub/govbox/blob/master/PROP-001.md)
document for a more detailed breakdown and further details on code, data and
applied formulae.
To obtain the final distribution, we also apply a decimation factor `K = 0.1`
when computing balances.
According to the current calculations - which **may** change - the potential
ATONE distribution will be of approximately ~97 Millions.

|                   |   TOTAL    | DID NOT VOTE |    YES    |     NO     | NOWITHVETO |  ABSTAIN  | NOT STAKED |
|-------------------|------------|--------------|-----------|------------|------------|-----------|------------|
| ATONE Distributed | 96,997,800 |   10,445,719 | 6,374,676 | 48,015,988 | 10,780,005 | 5,672,466 | 15,708,946 |
| *% Ownership*     |            | 11%          | 7%        | 50%        | 11%        | 6%        | 16%        |
| *% ATOM prop 848* |            | 20%          | 21%       | 16%        | 3%         | 10%       | 30%        |

### Community Pool & reserved address

The AtomOne Community Pool balance follows a different procedure, we propose
that 1/18 of the ATONE distributed be minted to feed the Community Pool. This
corresponds to an amount of 5,388,766 ATONE.

The same amount will be minted to feed a reserved address for future funding of
the Treasury DAO.

### Total supply

- The proposed ATONE supply is **107,775,332 ATONE**:
  ```
  ATONE Distributed + Community Pool + Reserved address 
  96,997,800        + 5,388,766      + 5,388,766        = 107,775,332
  ```
  which is around ~3/10 (31.43%) of the ATOM supply at the time of proposal 848
  (342,834,268).
- The `C` multiplier is computed as ~1.62.
- The ICF slashing represents a total of 12,677,878 ATOM

> [!WARNING]
> While we have explained and detailed the proposed methodology, we cannot
> guarantee the accuracy of reliability of any of the accompanying code and 
> resulting preliminary data. Although every effort has been made to ensure
> accuracy and reliability, there is no guarantee that the tools will remain
> unchanged or error-free as further developments occur. Voters should exercise
> caution and discretion when utilizing these tools, and understand that any
> information or calculations provided by them are subject to revision.

We acknowledge there are additional details to be discussed for the final ATONE
distribution, such as for example 
[issue #13](https://github.com/atomone-hub/genesis/issues/13)
from the AtomOne genesis repo, but these are intentionally left out of this
proposal as it only seeks to establish a baseline distribution mechanism.

## Consequences

* Establishes a fair and structured token distribution mechanism that aligns 
  with AtomOne's founding ethos.

* Sets a precedent for future endeavors, demonstrating the importance 
  of community alignment and shared values in token distribution decisions.

## Alternatives

Should this proposal fail to reach approval from the community, alternative
distribution mechanisms might be discussed and used instead. We did not evaluate
alternative mechanisms as part of this proposal, but the proposal methodology
was revised based on community feedback during the
[GovGen Townhalls](https://github.com/atomone-hub/genesis/tree/main/GovGen_Townhalls).

## Governance votes

* **YES**: You support the outlined ATONE distribution mechanism, recognizing
           the importance of aligning with AtomOne's core values and principles.
* **NO**: You do not support the proposed distribution mechanism and advocate for
          an alternative approach.
* **NO WITH VETO**: You strongly oppose the proposal due to perceived inequities
                    or deviations from AtomOne's foundational principles.
* **ABSTAIN**: You prefer to contribute to quorum without endorsing or opposing
  the proposal directly.
