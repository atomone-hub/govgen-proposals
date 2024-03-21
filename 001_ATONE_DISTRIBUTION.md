# Proposal 001: Equitable $ATONE Distribution in the Spirit of AtomOne's Founding Principles

## Changelog

* March 13th 2024: first draft
* March 14th 2024: add data and code
* March 21th 2024: update distribution to ensure that active voters (yes and
  no) don't have less than 2/3 of the supply. Reduce the final supply by a
  factor of 10.

## Status

Draft

## Summary

This proposal seeks to establish a fair and principled distribution mechanism for
$ATONE, the native token of  AtomOne, reflecting the foundational principles as
outlined in the AtomOne [founding documents](https://github.com/atomone-hub/genesis).
The proposal tries to synthesize the [discussion](https://github.com/atomone-hub/genesis/issues/12)
around the $ATONE distribution, and leveraging the snapshot from Cosmos Hub's
[proposal 848](https://www.mintscan.io/cosmos/proposals/848), it aims to reward
participation and engagement while adhering to AtomOne's ethos of intelligent
distribution and governance.

## Context

AtomOne's inception was driven by fundamental disagreements within the Cosmos
Hub's community, particularly regarding the nature of $ATOM as a staking versus
monetary token and the broader vision for the network's future
[1](https://github.com/atomone-hub/genesis/blob/main/README.md)
[2](https://github.com/atomone-hub/genesis/blob/main/STAKING_VS_MONEY.md).
Proposal 848's passage, advocating for $ATOM's "*halving*" without adequately
addressing security concerns, marked a pivotal moment that underscored the
necessity for AtomOne. AtomOne, thus, is not merely a technical divergence but
a philosophical stand for a network that remains true to the principles of
minimalism in its IBC/ICS hub functionality, robust security model, and an
intelligent, aligned community governance structure.

## Decision

In accordance with AtomOne's foundational principles and the discussions
surrounding the token distribution, we propose the $ATONE distribution mechanism
outlined below, reflecting a balanced approach to reward participation,
engagement, and alignment with AtomOne's vision. The intent of the distribution
mechasnim is to *increase* the portion of no-voters regarding yes-voters, but
also to ensures that the total of non-voters, abstainers and unbonded $ATONE is
less than 1/3 of the supply. We consider that this portion of the supply needs
to be slashed to preserve a good majority of active voters (yes and no),
because we think this sleeping portion of the voting power might be harmful for
AtomeOne.

**Note that in addition the ICF will be entirely slashed**.

> [!NOTE]
> We specifically refer to the *$ATOM that voted*, and not accounts, to 
> accurately reflect how the distribution mechanism will work, which also
> mirrors in practice how the `x/gov` tally works on the Cosmos Hub.
> The final balance for each account will be the result of the contributions
> from each $ATOM with which they either voted (and how), or did not.

> [!NOTE]
> A *voting* $ATOM is $ATOM that has voted either directly or indirectly via 
> delegation.
> A *non-voting* $ATOM is $ATOM that did not vote either directly or indirectly
> because the validator it is delegated to also did not vote.

1. **YES Votes to Proposal 848**: standard 1x multiplier for the $ATOM that
   voted *YES* at the snapshot.

2. **NO and NWV Votes**: Acknowledged with a 3x multiplier on top of the $ATOM
   that voted *NO* and *NWV*, emphasizing the critical stance against the
   monetary token proposition and alignment with AtomOne's security philosophy.
   The resulting balance will essentially be 4x the original $ATOM balance.

   1. Moreover, the $ATOM that voted *NWV* will also get a 3% bonus on top in
   order to (slightly) reward the stronger political stance.

3. **ABSTAIN Votes**: Assigned a multiplier `C` resulting from a formula that
    ensures that the total of *abstainers*, *non-voting* and *unbonded* $ATONE
    is limited to 33% of the supply.

    The multiplier formula is the following:
    ```math
    C = \frac{t}{1-t} \cdot \frac{X_{Y} + 4 \cdot X_{N} + 4 \cdot Y_{NWV}}{X_{A}+X_{DNV}+X_{U}}
    ```
    <!-- TODO replace the formula with an image uploaded to IPFS ? Because
    probably the latex rendering won't work in standard markdown renderer -->
    
    where:
    - `C` is the multiplier
    - `t` is the target percentage, which is 33%.
    - `X` represent a supply in $ATOM, with annotations indicating the portion
    of the supply:
        - `Y` voted Yes
        - `A` voted Abstain
        - `N` voted No
        - `NWV` voted No With Veto
        - `DNV` DidN't Vote
        - `U` Unbonded

    > [!TIP]
    > Additionnal information about how we ended up with this formila can be
    > found [here](https://github.com/atomone-hub/govbox/blob/master/PROP-001.md#multiplier-formula)

4. **Did not vote**: It is considered to be *non-voting* the $ATOM that did not
   vote at all (even through its delegations). The $ATOMs that *did not vote*
   get the same multiplier as *abstainers*, but they incur in an additional 3%
   malus to (slightly) punish inactivity.

5. **Liquid $ATOM**: will equate to the *non-voting* category and receive the
   same multiplier as $ATOM that *did not vote*.

> [!NOTE]
> An account that has voted indirectly through its delegations may see its
> balance affected by different multipliers depending on the votes of its
> delegations.
> The same reasoning applies in the case of *weighted* votes.
> Moreover, it is always the case that for any account that has both staked as
> well as liquid $ATOM, the resulting $ATONE balance will be the result of the
> contributions of each part as already discussed.

The following table is also provided for a quick recap:

|                    |  DID NOT VOTE | YES | ABSTAIN | NO |    NWV    |
|:------------------:|:-------------:|:---:|:-------:|:--:|:---------:|
| Staking multiplier |    C x malus  |  1  |    C    | 4  | 4 x bonus |
| Liquid multiplier  |    C x malus  |  -  |    -    | -  |     -     |

Accompanying code that implements the proposed distribution mechanism is
available at [https://github.com/atomone-hub/govbox](https://github.com/atomone-hub/govbox). Please refer to the 
[PROP-001.md](https://github.com/atomone-hub/govbox/blob/master/PROP-001.md)
document for a more detailed breakdown, and some preliminary data.

According to the current calculations -- which **may** change -- the potential
$ATONE distribution will be of around ~485.03 Millions.

Finally, to reduce the final supply, we also apply a decimation factor when
computing final balances K=0.1 This results in a final total supply of 48,5M.

|                       |   TOTAL    | DID NOT VOTE |    YES    |     NO     | NOWITHVETO |  ABSTAIN  | NOT STAKED |
|-----------------------|------------|--------------|-----------|------------|------------|-----------|------------|
| Distributed           | 48,503,137 |    5,247,961 | 6,374,676 | 21,340,439 |  4,791,114 | 2,849,864 |  7,899,084 |
| Percentage over total |            | 11%          | 13%       | 44%        | 10%        | 6%        | 16%        |

- The $ATONE supply is ~0.141 times less than the $ATOM supply.
- The `C` multiplier regarding these figures is equal to ~0.814.
- The ICF slashing represents 12,590,970 $ATOM.

> [!WARNING]
> While we can attest for the correctness of the proposed methodology, we
> cannot guarantee the same is true for the accompanying code and resulting 
> preliminary data. Although every effort has been made to ensure accuracy and
> reliability, there is no guarantee that the tools will remain unchanged or
> error-free as further developments occur. Voters should exercise caution and
> discretion when utilizing these tools, and understand that any information or
> calculations provided by them are subject to revision.

We acknowledge there are additional details to be discussed for the final $ATONE
distribution, such as for example [issue #13](https://github.com/atomone-hub/genesis/issues/13)
from the AtomOne genesis repo, but these are intentionally left out for the time
being as this proposal seeks to establish a baseline mechanism.

## Consequences

* Establishes a fair and principled token distribution mechanism that aligns with
  AtomOne's founding ethos.

* Sets a precedent for future similar endeavors, demonstrating the importance 
  of community alignment and shared values in token distribution decisions.

## Alternatives

Should this proposal fail to reach approval from the community, alternative
distribution mechanisms might be discussed and used instead. We did not evaluate
alternative mechanisms as part of this proposal.

## Governance votes

* **YES**: You support the outlined $ATONE distribution mechanism, recognizing
           the importance of aligning with AtomOne's core values and principles.
* **NO**: You do not support the proposed distribution mechanism and advocate for
          an alternative approach.
* **NO WITH VETO**: You strongly oppose the proposal due to perceived inequities
                    or deviations from AtomOne's foundational principles.
* **ABSTAIN**: You prefer to contribute to quorum without endorsing or opposing
  the proposal directly.
