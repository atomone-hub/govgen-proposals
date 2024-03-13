# Proposal 001: Equitable $ATONE Distribution in the Spirit of AtomOne's Founding Principles

## Changelog

* March 13th 2024: first draft

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
 dintelligent, aligned community governance structure.

## Decision

In accordance with AtomOne's foundational principles and the discussions
surrounding the token distribution, we propose the $ATONE distribution mechanism
outlined below, reflecting a balanced approach to reward participation,
engagement, and alignment with AtomOne's vision. Please note, the intent of the
distribution mechanism is to *increase* the total future supply of $ATONE with
respect to the current supply of $ATOM, therefore there won't be
**any penalties**, the mininum airdropped amount will be 1x the account balance.

1. **YES Votes to Proposal 848**: standard 1x multiplier for the $ATOM that
   voted *YES* at the snapshot, which is the minimum possible.
2. **NO and NWV Votes**: Acknowledged with a 3x multiplier on top of the $ATOM
   that voted *NO* and *NWV*, emphasizing the critical stance against the monetary
   token proposition and alignment with AtomOne's security philosophy. The
   resulting balance will essencially be 4x the original $ATOM balance.
2.1. Moreover, the $ATOM that voted *NWV* will also get at 3% bonus on top in
order to (slightly) reward the stronger political stance.
3. **Non-Voters**: It is considered to be *non-voting* the $ATOM that either did
   not vote or abstained. Assigned a base multiplier resulting from the blend of
   *YES*, *NO*, and *NWV* votes to essentially provide a "neutral" multiplier
   that reflects the turnout of proposal 848 accounting only for active votes.
   The multiplier `B` is computed as `B = Y + (N + V) * 4` where `Y` is the
   *relative* percentage of *YES* votes (i.e. the total $ATOMs that voted *YES*
   over the sum of total $ATOMs that voted either *YES*, *NO*, or *NWV*), and
   `N` and `V` are the *relative percentages* of respectively *NO* and *NWV* votes.
3.1. Moreover, the $ATOM that did not vote will get a 3% malus on top in order to
(slightly) punish inactivity
4. **Liquid $ATOM**: will receive a standard 1x multiplier.

The following table is also provided for a quick recap:

|                    |  DIDN'T VOTE  | YES | ABSTAIN | NO |    NWV    |
|:------------------:|:-------------:|:---:|:-------:|:--:|:---------:|
| Staking multiplier | B x malus |  1  |  B  |  4 | 4 x bonus |
| Liquid multiplier  |       1       |  1  |    1    |  1 |     1     |

[**RESERVED FOR DATA AND CODE**]
...

We acknowledge there are additional details to be discussed for the final $ATONE
distribution, such as for example [issue #13](https://github.com/atomone-hub/genesis/issues/13)
from the AtomOne genesis repo, but these are intentionally left out for the time
being as this proposal seeks to establish a baseline mechanism.

## Consequences

* Establishes a fair and principled token distribution mechanism that aligns with
  AtomOne's founding ethos.

* Sets a precedent for future similar endevours, demonstrating the importance of
  community alignment and shared values in token distribution decisions.

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
* the proposal directly.
