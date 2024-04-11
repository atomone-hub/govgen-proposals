# govgen-proposals
GovGen-dedicated repo to discuss upcoming governance proposals

> [!WARNING]
> THE [`govgend`](https://github.com/atomone-hub/govgen) BINARY MENTIONED IN
> THIS PAGE **HAS NOT BEEN AUDITED YET**.
>
> PLEASE USE **EXTREME CAUTION** WHEN USING THIS SOFTWARE, AND USE IT AT YOUR OWN RISK.
> FOR THE TIME BEING, WE ADVISE THAT YOU NOT USE IT WITH YOUR PERSONAL PRIVATE KEY(S).
>
> THIS IS **ESPECIALLY IMPORTANT** AS GOVGEN RELIES ON AND USES ACCOUNTS DERIVED FROM
> THE COSMOS HUB, AND THEREFORE THERE IS RISK OF COMPROMISING YOUR COSMOS HUB
> ACCOUNT AS WELL.

## How to draft a text proposal for AtomOne
- Create a new branch
- Create a copy of the file `XXX_proposal_template.md`
- Replace `XXX` by the next proposal id, and `proposal_template` by the title
  of your proposal
- Mark the status as 'Draft'
- Fill the different sections of the file
- Submit a PR to open discussions

## How to submit a proposal securely
Please follow the [guide](submit-tx-securely.md).

## How to fund a proposal
Once submitted, a proposal requires a 5,000 $govgen deposit to enter the voting
period. This means that some proposals must be crowdfunded by the community.
Any account can participate by adding a deposit to a proposal they are
interested in.

Assuming you have read the guide above, here is how to create a transaction to
add a deposit to a proposal. But first you need to know the proposal ID, which
you can get from the Explorer URL when viewing a proposal: for example, for
https://explorer.govgen.io/govgen/gov/42, the proposal ID is 42.

The following command creates the deposit transaction:
```
govgend tx gov deposit <PROPOSAL_ID> 5000000ugovgen \
   --from <ADDRESS> \
   --chain-id govgen-1 \
   --fees 5000ugovgen \
   --generate-only \
   --gas auto \
   --sequence <SEQUENCE_NUMBER> \
   > tx.unsigned.json
```
The `5000000ugovgen` is an example of deposit, you can set whatever you want,
as long as you have enough balance.

Once you have created your unsigned transaction, proceed to [step
4](submit-tx-securely.md#4-sign-the-transaction-offline-computer) of the guide
to submitting it.
