CampusNet Pay Hub — Technical Design Document

Version: 1.0
Date: October 20, 2025
Audience: Engineers, technical leads, product owner, auditors
Purpose: Define the architecture and implementation plan for a modular dApp that accepts SOL and CNET, supports Devnet/Mainnet environments, and integrates with CampusNet DAO tooling.

1. Executive summary

CampusNet Pay Hub is a modular dApp that enables CampusNet DAO to accept, disburse, and track value in both SOL and the DAO token (CNET). The app supports two environments (Devnet for testing, Mainnet for production), provides wallet-native UX, automates payments from treasury multisigs, and logs transactions for governance reconciliation. The initial scope is an MVP capable of receiving and sending SOL and CNET, recording payments, and exposing a ledger for DAO auditors.

2. Goals & success criteria

Goals

Provide a secure payment interface for SOL and CNET.

Integrate with DAO treasury and multisig controls.

Support Devnet (sandbox) and Mainnet (production) modes with minimal config change.

Log all on-chain transactions and off-chain metadata for governance and audits.

Allow payments to contributors, accept payments (e.g., event fees), and support bounties.

Success criteria

End-to-end Devnet payments work: mint/send/receive SOL and CNET, logged and viewable.

Multisig execution of treasury disbursements validated.

App integrated with Discord role gating and Work-to-Earn systems (Dework integration stub).

Security review completed and no critical issues.

3. System overview & components

High-level components

Frontend: Next.js app with Wallet Adapter and UI.

Backend API / Middleware: Node.js (Express) or serverless functions for logging, off-chain business rules, and rate-limited RPC aggregation.

On-chain programs / smart contracts: Minimal custom Solana programs for payment routing and optional swap logic; primary reliance on existing SPL token behavior.

Treasury / Multisig: Squads / Goki Safe multisig on Solana mainnet; test equivalents on Devnet.

Data storage: Postgres (or Supabase) for metadata; event logs mirrored to IPFS for immutability.

Integrations: Phantom / Backpack wallet adapter, Dework / Wonderverse APIs, Guild.xyz/Collab.Land, Snapshot linkage.

4. Component details
4.1 Frontend

Stack

Next.js (React)

TypeScript

Tailwind CSS for UI

@solana/wallet-adapter (Phantom, Backpack, Solflare)

Recoil or Zustand for state

Charting: Recharts or simple data tables

Features

Wallet connect modal

Account dashboard (balances for SOL and CNET)

Payment widget (Pay in SOL / Pay in CNET)

Invoice / request generator (create payment request link)

Transaction history page (queries backend)

Admin pages for treasury signers to view pending multisig transactions (read-only unless signer connected)

Environment toggles

NEXT_PUBLIC_CLUSTER (devnet | mainnet)

NEXT_PUBLIC_CNET_MINT (mint address per env)

4.2 Backend / Middleware

Stack

Node.js + Express or Next.js API routes

TypeScript

Postgres / Supabase for persistence

Redis for caching / rate-limiting

Helius / QuickNode / RPC provider for Solana queries

Responsibilities

Validate and persist transaction metadata (task id, contributor id, proof links)

Normalize RPC interactions and error handling

Maintain mapping of devnet/mainnet mints and multisig addresses

Provide endpoints for frontend: /api/balance, /api/txs, /api/pay-request, /api/treasury/pending

Webhook consumer for Dework and Snapshot events

Security

API keys stored in Vault (or environment secrets)

Signed webhooks check with HMAC

Rate limits and IP allowlisting for admin endpoints

4.3 On-chain programs & smart contract considerations

Approach

Prefer SPL token standard and existing multisig tooling (Squads/Goki Safe). Avoid custom token contracts unless required.

Minimal custom program (optional) for:

Payment routing (receipt verification metadata)

Escrow handling for conditional payouts

Internal accounting hash anchor (store payment receipt hashes that map to IPFS records)

Data stored on-chain (if using custom program)

PaymentRecord: payer, payee, amount, token, ipfs_receipt_cid, timestamp, executor

Registry pointer: latest app version / config CID

Why minimal program

Reduces attack surface, leverages audited SPL and multisig tools.

Keeps upgrade path and audits simpler.

4.4 Treasury & Multisig integration

Tools

Squads (Solana Multisig UI) or Goki Safe

Configure multisig with 3-of-5 signers (initially founders + two trusted community signers)

Treasury wallet holds CNET mainnet and SOL for operations.

Workflow

For on-chain disbursements initiated via the app, create a multisig transaction proposal (Squads transaction).

Notify signers (Discord + email).

On approval threshold, transaction executes on-chain.

App polls Squads API for status updates and writes to off-chain ledger.

5. Data model and storage
5.1 Primary tables

users

id (uuid)

wallet_address

display_name

verified (boolean)

role (student | alumni | contributor | admin)

created_at

transactions

id (uuid)

tx_hash

payer_wallet

payee_wallet

amount

token_mint

token_symbol

cluster (devnet | mainnet)

status (pending | confirmed | failed)

ipfs_receipt_cid

metadata JSON (task id, proposal id)

created_at, confirmed_at

payment_requests

id

requester_wallet

amount

token_mint

description

expiration

status

audit_logs

id

event_type

payload JSON

created_at

5.2 Off-chain / IPFS

Receipts and supporting files uploaded to IPFS and linked via ipfs_receipt_cid.

Periodic snapshot of ledger uploaded to IPFS for immutable archival.

6. UX flows
6.1 Pay in SOL (MVP flow)

User opens payment widget, selects “Pay in SOL”.

Frontend composes transaction: SystemProgram.transfer or wallet-sign request.

User signs transaction in Phantom.

After confirmation, frontend posts transaction metadata to backend API (/api/txs) with proof links.

Backend verifies the transaction via RPC (confirmations) and stores transaction record.

If transaction is payment for bounty, call Dework API to mark task complete / trigger reward.

6.2 Pay in CNET (MVP flow)

User selects “Pay in CNET”; frontend creates SPL token transfer instruction to CNET_MINT.

Wallet signs and sends transaction.

Post confirmation, backend records transaction and anchors receipt to IPFS if requested.

If this triggers a bounty payout, the app creates a multisig proposal or direct transfer depending on threshold.

6.3 Treasury payout (admin flow)

Admin creates payout request in app (amount, recipient, token).

If amount < CORE_THRESHOLD (e.g., 5,000 CNET) the Core Team may approve via app (fast path).

For larger amounts, app creates a multisig transaction proposal on Squads.

Signers approve; Squads executes; app listens to Squads events and updates ledger.

7. Security model

Principles

Least privilege; do not store private keys in the app.

Signatures only via user wallets or multisig.

Keep business logic off-chain where it makes sense; on-chain for irreversible actions.

Immutable receipts anchored to IPFS.

Controls

Use Squads/Goki for treasury -> no single key holds funds.

Use HTTPS + CSP + secure cookie settings for frontend.

Rate limits and bot protections.

Audit logging for all admin and treasury actions.

Periodic automated backups to IPFS and secure cloud storage.

Dedicated security review before mainnet deploy.

8. Devnet / Mainnet deployment strategy

Environments

development — localnet for unit tests

staging — Devnet cluster and test data

production — Mainnet cluster

Configuration

All env-specific parameters in .env (do not check into git)

RPC_URL, CNET_MINT, TREASURY_ADDRESS, SQUADS_API_KEY

CI/CD pipelines switch configs based on branch:

main → production (requires manual gate)

develop → staging

Migration plan

Build & test on localnet

Deploy to Devnet, test all flows, integrate with test Squads multisig

Internal bug bounty & audit

Prepare Mainnet program & mint addresses, run deployment checklist

Execute Mainnet launch (multi-signer controlled)

9. Integrations & third-party services

Wallets: Phantom, Backpack, Solflare

RPC providers: Helius, QuickNode (with fallback)

Multisig: Squads, Goki Safe

Work-to-Earn: Dework / Wonderverse

Access gating: Guild.xyz / Collab.Land

IPFS: Pinata / Web3.Storage

Analytics: SolanaFM / custom dashboards

CI/CD: GitHub Actions or GitLab CI

10. Testing & QA plan

Unit tests

Smart contract unit tests (Anchor localnet)

Backend business logic (jest)

Frontend component tests (react-testing-library)

Integration tests

End-to-end on localnet

End-to-end on Devnet with test wallets and Squads

Security testing

Internal code review

External smart contract audit (required before mainnet)

Penetration test for the app and API

User testing

Closed beta with 20–50 community members on Devnet

Onboard test contributors, run mock bounty cycles

11. MVP scope & roadmap (milestones)

MVP (4–6 weeks) — Devnet

Wallet connect + balances (SOL & CNET-Dev)

Basic payment widget (SOL & CNET-Dev)

Backend ledger to store transactions

Treasury multisig integration read-only

Payment request links

Basic admin dashboard

Docs: DEVNET_SETUP.md, README, runbook

Post-MVP (6–12 weeks) — Staging -> Pre-mainnet

Dework integration for bounties

Multisig execution flow and signer notification

IPFS anchoring of receipts

Role gating integration (Guild.xyz)

E2E tests, security audit

Mainnet launch (Conditional)

Smart contract audits completed

Final mint and multisig funded

Mainnet config and manual gate deployment

Public launch announcement and DAO proposal to approve mainnet genesis

12. Operational considerations & governance alignment

Payment thresholds and multisig policies must mirror DAO governance (e.g., proposal thresholds).

Any change to payout logic, fee model, or treasury policy must be proposed via DAO governance and recorded in the changelog.

Keep an immutable audit trail: every payment reference must include proposal IDs or task IDs where relevant.

13. Estimated effort (high-level)

Frontend: 3–4 developer-weeks (1 dev)
Backend & infra: 3–4 developer-weeks (1 dev)
Integration with Squads/Dework/Guild: 2 developer-weeks (integration engineer)
Smart contract (optional minimal): 2–3 developer-weeks (Rust/Anchor dev)
QA & Audit prep: 2–4 weeks
Total: ~12–18 developer-weeks to production readiness (Devnet → mainnet contingent on audits and governance approvals).

14. Deliverables & files to produce

CampusNetPayHub_TechnicalDesign.md (this document)

DEVNET_SETUP.md (how to reproduce the environment)

deployment_playbook.md (step-by-step Mainnet launch checklist)

Frontend repo (Next.js)

Backend repo (API + DB migrations)

Smart contract repo (Anchor) — optional

CI/CD pipelines and Helm/terraform infra scripts (if using cloud infra)

Security audit report (third-party)

15. Next actions (immediate)

Approve design and MVP scope with Core Team.

Create repositories and basic CI templates.

Implement Devnet config and run local testnet flows.

Recruit an Anchor/Rust engineer for on-chain pieces (if needed).

Schedule external audit window post-staging completion.
