# SIP 004 - PGP + git voting

The Superalgos ecosystem has a lot of code and documents to manage, and the Constitution requires that these be managed through a voting consensus of ALGO Stream operators. Regardless of how the ALGO token is managed, the code, documents, and voting should be done on git, using PGP signatures and identities. Specifically, the following changes are suggested:

1. Move all existing documents into git, formatting in plaintext for easier edits and discussion.
2. Require all future publications to be put in git (distributed) and only after on the website (centralized)
3. Require all algo code to be reference by a git hash, at minimum, and a full git repository once/if algo code is open sourced.
4. Require all Team Members to have a public PGP key signed by m of n other Team Members.
5. Require all Stream-qualifying contributions to be made via signed git Pull Request.
6. Require all votes to be accompanied by PGP signature.

For an example of #5, see the PR associated with this SIP. This SIP is signed with my PGP key, and I am submitting it via PR. Additional signatures can be added, until the required number are met for the change to be merged. This process can just as easily apply to a constitutional change as a Stream-qualifying contribution.

## Git

At the time of writing, Superalgos uses git for storage of all of it's code, and some of it's documentation, including this SIP. Furthermore, many of the team members already maintain local repositories, and can act as witnesses to any changes that might happen. (I.e. Luis would know if I changed the UserModule, and could specify the changes bit by bit).

Furthermore, though centralized, github currently provides a common interface for managing the team's distributed git tree. For instance, Pull Requests are a convenient process that can be used in tandem with vote counting, and additional checks for legal and technical quality.

In short, git is a ready-made distributed filesystem appropriate for publishing and managing all Superalgos documents. It is already used by the team, and probably by any algo developers and exchanges that might join the network.

The reference git implementation already includes an HTTP server, making any git user a "node" on the network. Additionally, I (isysd) have already implemented a [PGP signature counting check](https://github.com/isysd-mirror/http-server/blob/isysd/index.js#L219) extension to this standard git HTTP server.

## PGP

[SIP 001](https://github.com/Superalgos/Improvement-Proposals/blob/master/SIP%20001%20-%20Auth-Streaming-MVP-P2P-Roadmap.md) calls for all Superalgos users to be identified by PGP public key. This would allow them to discover and assess trustworthiness of peers on the Superalgos network without any point of centralization.

Some Team Members (me, at least) already PGP sign contributions. These signatures are currently ignored, but could be required and automatically checked with very little work.

Currently, RSA is the most common algorithm used with PGP, but there is support for ECC, including secp256k1, the curve used by Bitcoin.

To connect PGP with git, simply run these two commands:

```shell
git config --global user.signingkey $YOUR_PGP_KEY_FINGERPRINT
git config --global commit.gpgsign true
```

That's it, now any commits you make will be signed by your PGP key, and considered valid votes/contributions by Superalgos.

## Charter and Constitutional Requirements

> Provision for a mechanism to amend, update and evolve the ALGO Governance Charter.

> The decision to conduct each MEO shall be subject to approval by the Governing Body, who will receive the following details from the Superalgos Organization for consideration and approval:
> + The Exchange of choice;
> + The date and duration of the offering;
> + The price of the ALGO Token at the offering;
> + The cap of the offering, meaning the number of ALGO Tokens to be offered;
> + Any other variable affecting the structure of the offering;
> + An explanation of how the MEO Plan fits on the current Fundraising Plan, or justifying any potential deviation.

> The Governing Body will vote on three distinct types of proposals, all of them to be covered in detail further down this document:
> + Annual Fundraising Plan;
> + MEO Plan;
> + ALGO Stream Proposal;
> + ALGO Competition Prizes Fund matters;
> + Constitution amendments, as specified in the Constitution.

> For every contract signed with Exchanges, the Superalgos Organization shall publish a report containing the following information:
> + Due diligence report on functional, infrastructure and security of the Exchange.
> + A transparency report on the fees and / or incentives allocated to the Exchange for services rendered.
> + A report on the structure of the deal with the Exchange in relation with the business involving the volume generated by the Trading and Asset Management Marketplace.
> The aforementioned reports shall be published within 30 days after the MEO’s closing date.

> The Superalgos Organization shall keep a public log of all Areas of Responsibility, their corresponding categories, and the person / entity to which the area may be assigned.

> The log shall be published on the project’s website, to be maintained by the Superalgos Organization. The log shall be updated on a monthly basis.

> These areas shall be published in the Areas of Responsibility Log and shall be made available for anyone to apply to.

This sort of public document publishing must be done in a hashed and version controlled manner. I.e. exactly which version and document are we voting on? Where is the source for it, so I can read before voting? How can peers be sure historical documents weren't tampered with?

> In order for the amendment to be enacted, the following conditions must be met:
> + a minimum of 50% of existing votes must be casted;
> + 75% of the votes casted shall be “yes” votes.

> Votes are attached to the ALGO Streams each Team Member holds.

> Each ALGO Stream is entitled to as many votes as the numeric Size of the ALGO Stream. Therefore, each Team Member is entitled to as many votes as the sum of the Sizes of all ALGO Streams the Team Member may hold.

> The Governing Body shall approve the Fundraising Plan with 50% + 1 “yes” votes. In case the plan is rejected, the Superalgos Organization shall present a new plan.

> + The Governing Body shall approve the MEO Plan with 50% + 1 “yes” votes. In case the plan is rejected, the Superalgos Organization shall present a new plan.

> In order for the amendment to be enacted, the following conditions must be met:
> + a minimum of 50% of existing votes must be casted;
> + 75% of the votes casted shall be “yes” votes.

This sort of vote counting requires a consensus system that is aware of all voting members and weights, as well as specific document versions. It must also be able to process many thousands of votes per issue. Imagine storing all of that metadata in an Ethereum smart contract, or (god forbid) an off-chain database to be audited manually.

> The Governing Body is formed by all Team Members in existence at any specific point in time in which a vote is called for. 

> The contribution of Team Members is compensated with ALGO Streams granted by other Team Members, thus, the Size and number of ALGO Streams a Team Member holds is a direct measure of the value of the contributions as perceived by other Team Members.

> Candidates are evaluated by Team Members and the area is assigned with 50% + 1  “yes” votes. After assignment, the candidate is considered a Aspirant Team Member.

Team Members will be required to sign each other's keys, and to vote on any contributions to be merged. This Team Member approval and registration process is a direct analogy for the PGP Web of Trust (key signing).

Key signing makes this vote provable and a permanent reputation.

> The criteria for activating the ALGO Stream shall be clearly specified: the Team Member candidate shall deliver certain value to the project, perform a certain amount of work or produce a certain deliverable—which shall be clearly defined—before the ALGO Stream is activated.

> Any Team Member may present candidates to fill any Area of Responsibility that is properly identified and defined, as prescribed earlier in these Rules (point 2).

> Once the Aspirant Team Member has delivered the work specified (in point 2), Team Members may approve the work with 50% + 1  “yes” votes. In case the work is not approved, the Aspirant Team Member may iterate until the approval is granted. 

These are basically team workflow issues, easily addressable through Pull Request management.

> The ALGO Stream Keeper is the person actually creating, assigning, enabling, disabling and reassigning streams, and is appointed and removed by the Superalgos Organization.

This responsibility can now be distributed into a smart contract of m of n votes.

> The ALGO Stream Supervisor is the person in charge of monitoring ALGO Streams, and is appointed and removed by the Superalgos Organization. 

> The ALGO Stream Supervisor does periodic checks on the work performed by Team Members. In case a Team Member becomes unresponsive or neglects the area of responsibility—and after proper notice has been given to the party and the Core Team—the ALGO Stream Supervisor may pause the ALGO Stream.

> In case the Team Member resumes work as expected, the ALGO Stream Supervisor may resume the ALGO Stream.

> In case the Team Member does not resume work as expected, the ALGO Stream Keeper may stop the ALGO Stream.

> In case a replacement is found for the unresponsive Team Member, the ALGO Stream Keeper may reset the associated ALGO Stream and re-assign it to the new Team Member. 

This can be more like a "issue report" process, where anyone can report an issue with a contract or contribution. If sufficient votes agree with the complaint, a pause or stop of the Stream may be enacted by the group.

> Develop the governance system so that it can work at scale, supporting the participation of thousands of Team Members.

Tens of millions of people use git, and many of those already use PGP to sign git commits. For example, the Bitcoin core team signs most commits, and all releases with PGP keys.

Git and PGP are free to use, having no built-in cost, allowing thousands of voting actions to take place without any gas expenditure. Paying to vote would be a serious dis-incentive.
