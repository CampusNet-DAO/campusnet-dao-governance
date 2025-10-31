CampusNetDAO Proposal Guidelines

Version: 1.0
Chain: Solana Devnet
Token: CNET
Date: October 2025

1. Purpose

This document defines the formal proposal and voting process for CampusNetDAO.
Its goal is to ensure structured, transparent, and efficient decision-making across all DAO operations — from treasury spending to policy updates, project approvals, and community initiatives.

2. Proposal Categories

Every DAO proposal falls into one of the following categories:

Category	Description	Example Use Cases
Governance	Changes to rules, structure, or DAO Constitution.	Amending voting power, council terms, or membership rules.
Treasury	Allocation or redistribution of DAO funds.	Paying contributors, grants, bounties, marketing, or reserves.
Operations	Routine DAO actions or community initiatives.	Launching campaigns, tool integrations, or new working groups.
Partnerships	Collaboration with institutions or external entities.	MoUs with universities, blockchain startups, or NGOs.
Technical Upgrades	Platform or protocol-level enhancements.	Smart contract upgrades, app improvements, or automation tools.
3. Proposal Lifecycle

All proposals follow a standardized 4-step process:

Ideation Stage

Community members discuss ideas in the #proposal-discussion forum or Discord channel.

Informal feedback and feasibility checks occur before submission.

Draft Submission

Proposer submits a written draft via the DAO Portal (or GitHub Pull Request in /proposals/).

Drafts must include purpose, budget (if any), and success metrics.

Review & Voting Preparation

Council and community reviewers ensure the proposal follows formatting and budget standards.

Once validated, the proposal moves to Snapshot or Realms for voting.

Voting & Execution

DAO token holders vote on-chain using CNET tokens.

If approved, the proposal is executed via multisig or automation bot (e.g., Goki, Squads, or Realms plugin).

4. Proposal Format

All proposals must adhere to the following format:

## Proposal Title
Short and descriptive name.

### Summary
A concise overview of what this proposal aims to achieve.

### Problem Statement
Describe the issue, gap, or opportunity that justifies the proposal.

### Proposed Solution
Detail your recommended solution or initiative.

### Implementation Plan
Step-by-step breakdown of execution strategy, tools, and responsibilities.

### Budget (if applicable)
| Item | Description | Amount (CNET/SOL) |
|------|--------------|-------------------|
| Example | Contributor reward | 500 CNET |

### Timeline
Expected delivery milestones (e.g., Week 1–4).

### Success Metrics
How success or impact will be measured.

### Risks & Mitigations
Potential issues and how they’ll be addressed.

### Voting Options
- ✅ Yes — Approve proposal as written  
- ❌ No — Reject the proposal  
- ⚙️ Amend — Send back for modification

5. Voting Framework

Eligibility:

Any wallet holding ≥1 CNET token can vote.

Delegated votes are supported via governance platforms (e.g., Realms).

Voting Period:

Minimum: 48 hours

Maximum: 7 days (for large treasury or policy changes)

Approval Thresholds:

Proposal Type	Minimum Approval	Quorum Requirement
Standard	51%	10% of circulating supply
Treasury (>5% funds)	66%	20% of circulating supply
Governance Amendment	75%	25% of circulating supply

Vote Weight:

1 CNET = 1 Vote.

Votes are tallied by wallet address at block snapshot.

Abstain Option:

Members may abstain; abstentions count toward quorum but not total votes.

6. Execution and Verification

Once a proposal passes, it’s queued in the DAO Executor program.

Treasury-related actions are approved via multi-signature (3-of-5) wallet authorization.

Execution proof (transaction hash) is attached to the proposal record for transparency.

7. Proposal Revisions

Any proposal rejected twice consecutively must be restructured before resubmission.

Minor corrections (e.g., grammar, formatting, typos) don’t require re-voting.

Major revisions trigger a new voting round with updated version tags (e.g., P-002-v2).

8. Archiving and Documentation

All proposals (passed, failed, or withdrawn) are stored permanently under /proposals/ in the DAO’s public repository.

Each proposal includes metadata:

Proposal ID

Author Wallet

Status (Draft / Voting / Executed / Failed)

Links to discussions and on-chain transactions

9. Enforcement

Any attempt to bypass the formal proposal process or execute unapproved treasury operations constitutes a DAO Policy Violation and may result in:

Suspension of governance rights,

Removal from operational roles, or

Community-led vote for accountability action.

10. Amendment Policy

Changes to this guideline must go through a Governance Proposal with ≥66% approval and be versioned in /changelog/ProposalGuidelines.md.

11. Ratification

This Proposal Guideline becomes active immediately upon DAO vote approval.

End of Document
CampusNetDAO — Building Trust through Structured Decentralization.
