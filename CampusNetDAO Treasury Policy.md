CampusNetDAO Treasury Policy

Version: 1.0
Chain: Solana Devnet
Token: CNET
Date: October 2025

1. Purpose

This Treasury Policy governs all financial activities of CampusNetDAO, including the custody, disbursement, and accountability of DAO-owned assets.
It ensures transparent, secure, and mission-aligned management of funds to maintain operational integrity and community trust.

2. Treasury Objectives

The DAO Treasury exists to:

Fund ecosystem growth and innovation.

Provide liquidity for DAO operations and partnerships.

Ensure sustainability through prudent reserves and investment practices.

Support contributor incentives, grants, and student initiatives.

Maintain DAO solvency independent of external funding sources.

3. Treasury Structure
Component	Description
Main Treasury Wallet	Primary custody for DAO assets; all disbursements originate here.
Operations Reserve	Covers DAO platform costs, audits, bounties, and infrastructure.
Community Fund	Supports community projects, scholarships, and contributor rewards.
Ecosystem Growth Fund	Grants, partnerships, hackathons, and marketing initiatives.
Emergency Reserve	5–10% of holdings held in liquid form (SOL/USDC) for crisis response.

Each wallet address is publicly listed and verifiable on Solana Explorer.

4. Treasury Authority and Signatories
Multi-Signature Security

Configuration: 3-of-5 multisig using trusted Council wallets.

Signatories: Appointed by DAO vote, reviewed every 6 months.

Rotation: Wallets rotated every 12 months to prevent long-term key concentration.

Access Rules

No single wallet may execute treasury transactions unilaterally.

All large disbursements (≥10% of reserves) require DAO-wide approval.

Emergency disbursements must be logged and disclosed within 48 hours.

5. Fund Allocation Policy
Category	Allocation % (Approx.)	Purpose
Operations	25%	Platform upkeep, security, infrastructure.
Community Fund	25%	Member incentives, student initiatives, scholarships.
Ecosystem Growth	35%	Grants, marketing, partnerships.
Emergency Reserve	10%	Liquidity buffer in SOL/USDC.
Audit & Compliance	5%	Independent review, legal filings.

Allocations are flexible and may shift upon DAO vote or quarterly review.

6. Payment Workflow
Standard Process

Proposal Submission: Contributor or team submits payment proposal with breakdown.

Review: Core Council validates deliverables and confirms milestone completion.

Approval: DAO vote or Council multisig (depending on fund size).

Disbursement: Transaction executed via smart contract or multisig approval.

Recordkeeping: Transaction hash logged in /treasury/transactions/ folder and on dashboard.

Threshold Rules
Amount (USD value)	Approval Level
≤ $500	Core Team approval
$501–$5,000	Council approval (3-of-5)
> $5,000	DAO vote (≥50% quorum)
7. Accepted Currencies

Primary: CNET (native DAO token)

Secondary: SOL, USDC

DAO maintains dual-asset payment support to ensure liquidity and stable contributor compensation.

Exchange between assets is handled via trusted Solana DEX (e.g., Jupiter, Raydium).

8. Treasury Reporting
Frequency	Deliverable	Responsible Party
Monthly	Income & expenditure summary	Treasury Council
Quarterly	Full audit report	Independent auditor
Annually	Treasury performance and allocation breakdown	Core Council

All reports are stored in /reports/treasury/ and pinned to IPFS for immutability.

9. Risk and Compliance Controls

Cold storage for long-term reserves.

Real-time monitoring via Solana block explorers and DAO dashboard.

Dual-auth verification for high-value transactions.

Compliance review for all external grants and partnerships.

Immediate suspension of signatory authority upon misconduct or inactivity.

10. Transition to Mainnet

Upon DAO vote for migration:

Devnet treasury is frozen and mirrored to a new Mainnet Treasury Contract.

All verified Devnet balances (CNET holdings) are airdropped at 1:1 ratio.

Treasury audit performed prior to migration to ensure data integrity.

11. Amendment and Oversight

Changes to this Treasury Policy require:

Proposal submission to DAO governance module.

≥66% supermajority approval.

Updated version stored in /changelog/TreasuryPolicy.md and IPFS hash announced in Discord and governance portal.

Authorized by:
CampusNetDAO Core Council
Version 1.0 — October 2025
