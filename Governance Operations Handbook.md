CampusNetDAO Governance Operations Handbook

Version: 1.0
Date: October 2025
Token: CNET
Chain: Solana Devnet

1. Purpose

This document defines the operational framework for CampusNetDAO’s governance — detailing proposal flow, council responsibilities, voting procedures, and emergency decision-making.
It serves as the manual for how power, process, and participation interact within the DAO’s governance ecosystem.

2. Governance Structure
Body	Primary Function	Composition	Voting Power
Community	Submits & votes on proposals	Open to all CNET holders	1 vote per token
Core Council	Executes approved proposals	5–9 elected members	Weighted (Council quorum ≥70%)
Working Groups	Executes domain-specific tasks	Appointed by Core Council	None (report-only)
Advisory Board	Strategic direction, partnerships	Invite-only	Non-voting
3. Governance Lifecycle Overview

Governance follows a 5-phase lifecycle — from Proposal Drafting to Implementation.

Phase 1: Drafting

Proposer creates a Draft Proposal (DP) using the DAO’s template.

DP is posted to Discord → #proposals-draft for open review (minimum 48 hours).

Community feedback is encouraged to refine the draft before submission.

Phase 2: Submission

Once refined, proposer uploads the final proposal to CampusNetDAO Governance Portal (e.g., Snapshot or Realms).

Each proposal must include:

Title & Summary

Motivation

Implementation Plan

Budget (if applicable)

Timeline

Contact wallet

Phase 3: Review

The Core Council reviews all proposals within 72 hours for compliance, feasibility, and duplication.

If approved for vote, proposal status changes to “Active”.

Phase 4: Voting

Voting is conducted on-chain via Snapshot (off-chain) or Realms (Solana).

Each CNET token represents one vote.

Quorum = 10% of total token supply (minimum).

Approval threshold = ≥60% “For” votes.

Phase 5: Implementation

Once approved, execution is coordinated by the Core Council or designated Working Group.

Funds (if any) are released through the Treasury Multisig Wallet.

Completion report is filed in /records/proposals/{proposal_id}.md.

4. Proposal Categories
Type	Description	Voting Duration
Governance Proposal (GP)	Amendments to Constitution, voting rules, or DAO structure.	5 days
Treasury Proposal (TP)	Requests for funding, grants, or bounties.	4 days
Operational Proposal (OP)	Infrastructure, app updates, or technical decisions.	3 days
Emergency Proposal (EP)	Critical security or treasury safeguard actions.	24 hours
5. Proposal ID Convention

Each proposal is uniquely tagged for tracking and audit purposes:

CNET-{YEAR}-{CATEGORY}-{ID}
Example: CNET-2025-GP-03

6. Voting Platforms
Platform	Function	Notes
Snapshot	Off-chain token-weighted voting	Used for general governance
Realms (Solana)	On-chain governance	Used for treasury & execution
Discord Polls	Pre-voting sentiment	Non-binding; for community alignment
7. Treasury Governance
Structure

Primary Treasury: Managed via a 3-of-5 Multisig (Core Council).

Community Pool: Used for small grants & rewards (≤500 CNET).

Reserve Pool: Locked for DAO stability; not accessible without supermajority.

Security

Treasury keys are held by elected signers with rotating access.

Treasury transactions are announced publicly before execution.

Smart contracts undergo quarterly audits.

8. Emergency Procedures

When DAO integrity or assets are at risk:

Emergency Proposal (EP) initiated by ≥2 Core Council members.

Voting window = 24 hours.

Quorum reduced to 5%.

Upon approval, Council may:

Pause treasury operations.

Freeze contracts.

Lock token transfers temporarily.

All emergency actions must be reversed or ratified by community vote within 72 hours post-crisis.

9. Governance Rewards
Action	Reward (CNET)
Proposal Submission	100
Voting Participation	20
Proposal Execution (Council)	150
Community Discussion Contribution	10

Rewards are distributed monthly via the Governance Incentive Pool.

10. Governance Review Cycle

Governance systems are audited quarterly to:

Assess proposal success rates.

Evaluate voting participation trends.

Review treasury health.

Recommend procedural improvements.

Reports are published as GovernanceReports_Q{n}_YYYY.md in /reports/governance/.

11. Governance Accountability

Inactive Council members (no participation for 2 cycles) are subject to DAO vote for replacement.

Conflict of Interest must be disclosed in every proposal or review.

Violations (nepotism, manipulation, bribery) lead to immediate suspension and public report.

12. Amendment & Versioning

This handbook can only be modified through a Governance Proposal (GP) approved by ≥70% vote.

Updated versions are logged in /changelog/GovernanceOps.md.

Authorized by:
CampusNetDAO Core Council
Version 1.0 — October 2025
