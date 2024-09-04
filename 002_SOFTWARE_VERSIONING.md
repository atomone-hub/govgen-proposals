# Proposal 002: Cosmos' softwares versioning

## Changelog

* August 14th 2024: First draft

## Status

Draft

## Summary

This proposal defines the versions of the software stack used in AtomOne,
namely the versions of Cosmos-SDK, Tendermint/CometBFT and Gaia. It also
describes the reasoning behind the choice of these versions.

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

AtomOne intends to be a minimalist chain to limit the attack surface.
Therefore, the choice of software versioning is critical to ensure good
reliability, along with a limited set of dependencies and modules.

## Decision

### Cosmos-SDK

The more important part of the dependency is the Cosmos-SDK, so it is the first
version we need to define.

While v0.45 is a battle-tested version and has proven to be viable, an [audit
driven by OAK Security][audit] in early 2024 has reported some serious threats
that have been fixed in v0.47. 

On the other hand, while v0.50 brings some interesting features in term of
modularity, it is not used by the CosmosHub yet (at the time of writing,
Gaia v19 upgrade proposal is still in voting period).

In conclusion, we suggest that AtomOne depends on Cosmos-SDK v0.47.

### Tendermint/CometBFT

In order to ensure a good compatibility between the application and the
consensus engine, we suggest using the same version of the consensus engine
than the one used by Cosmos-SDK 0.47, which is CometBFT v0.37.

### Gaia

With the defined version of the Cosmos-SDK, this limits the choice of Gaia
codebase to fork to 4 versions:

- v15 fixes all the issues reported by the OAK audit
- v16 adds some IBC/ICS functionalities
- v17 upgrades ICS to 2.0
- v18 adds the wasmd and feemarket module

AtomOne will not have any VM functionality as
specified in the draft of the [Constitution], thus v18 gets automatically discarded.

Considering that the first version of AtomOne will not have IBC or ICS
enabled, there's no advantage in choosing to fork v16 or v17.

This left out v15, which is the version we propose to fork for AtomOne.

## Consequences

* Fork of Gaia v15 with Cosmos-SDK v0.47 and CometBFT v0.37

## Alternatives

Should this proposal fail to reach approval from the community, alternative
versions might be discussed and used instead. 

## Governance votes

* **YES**: You support the outlined software versioning choice.
* **NO**: You do not support the proposed software versioning choice and
  advocate for an alternative approach.
* **NO WITH VETO**: You strongly oppose the proposal due to perceived
  inequities or deviations from AtomOne's foundational principles.
* **ABSTAIN**: You prefer to contribute to quorum without endorsing or opposing
  the proposal directly.

[audit]: https://github.com/oak-security/audit-reports/blob/main/Cosmos%20SDK/2024-01-23%20Audit%20Report%20-%20Cosmos%20SDK%20v1.0.pdf
[Constitution]: https://github.com/atomone-hub/genesis/blob/main/CONSTITUTION.md#article-4b-the-implementation
