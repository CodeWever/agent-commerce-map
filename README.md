# The Agent Commerce Map

Every way AI agents pay and get paid, in one place. Free, open, and machine-readable.

Agents can find each other now. The next question is how they pay each other, and how a human stays in charge while they do it. This map is the answer we could find in one place: every live way agents move money, from open protocols to hosted rails to card networks, with live status, real costs, and what each path actually requires.

Read the X article: [Agents can find each other. Now they need to pay each other.](https://x.com/DavidWever/article/2114462384052146293)

Version 1.0.0, October 25, 2026. All entries were checked against their official sources on that date. This layer moves fast. Verify on the source before you build on it.

## Five to start with, one per job

If you are new to agent payments, start here. Each of these is the best at one job.

1. **x402** - Learn the open standard everything else plugs into. HTTP-native, zero protocol fees, live and processing millions of transactions.
2. **Coinbase CDP x402 Facilitator** - The easiest way to accept x402 payments. First 1,000 onchain transactions a month free, then $0.001 each.
3. **Google AP2** - The authorization layer. Signed mandates that prove the user authorized the agent to pay for a specific purchase.
4. **Circle Agent Stack** - Give an agent its own policy-controlled wallet, with gas-free nanopayments down to $0.000001.
5. **Wever Pay** - Splits, escrow, invoicing, and disputes in one MCP, settled in USDC on Base.

## How to use this map

Pick your job first, then the entry. Paying for an API call is a different job from holding an agent's money, and both are different from settling a dispute. The categories below follow the job. Each entry states its live status, its chain and settlement asset, and its fees as published. Where a fee is not published, the map says so instead of guessing.

Data files: `agent-commerce-map.json` and `agent-commerce-map.yaml` carry the same entries in machine-readable form, so agents can read this map too. Categories live in `agent-commerce-categories.yaml`.

## Settlement protocols

Open standards that define how a payment is requested, authorized, and settled.

### x402

The open, HTTP-native payment standard. A server answers an unpaid request with 402 Payment Required, the client pays in crypto, the server serves the resource.

- Status: live, production-ready, millions of transactions processed
- Chain and asset: any EVM chain, Solana, and more; stablecoins first
- Fees: zero protocol fees; network gas separate
- Run by: x402 Foundation
- https://x402.org

### Google AP2 - Agent Payments Protocol

An open protocol for agent payments built on signed, verifiable mandates (intent, cart, payment) that prove the user authorized the agent to pay for a specific purchase. Published as specification v0.2, donated to the FIDO Alliance.

- Status: live as a published specification (v0.2, not yet 1.0)
- Chain and asset: payment-agnostic, cards, stablecoins, real-time bank transfers
- Fees: not published (open protocol, not a priced service)
- Run by: originated by Google with 60+ organizations; now with the FIDO Alliance
- https://ap2-protocol.org

### MPP - Machine Payments Protocol

An open protocol that lets agents pay for API services, designed rail-agnostic so different payment networks can implement it. Settles on Tempo.

- Status: live as a published protocol
- Chain and asset: rail-agnostic; settles on Tempo
- Fees: not published
- Run by: associated with Tempo (Tempo Labs)
- https://mpp.dev

## Payment rails and products

Hosted services an agent or developer calls to move money.

### Coinbase CDP x402 Facilitator

Coinbase's hosted x402 service that verifies signed payments and settles them onchain, so a seller runs no settlement infrastructure of its own.

- Status: live, over 100 million transactions processed
- Chain and asset: all ERC-20 tokens on supported EVM networks (Base, Polygon, Arbitrum, Monad, World) and SPL tokens on Solana
- Fees: first 1,000 onchain transactions a month free, then $0.001 each; verification always free; gas separate
- Run by: Coinbase Developer Platform
- https://docs.cdp.coinbase.com/x402/welcome

### Wever Pay / Wever Labs MCP

Wever Labs' MCP-accessible money toolkit: paid tools and commerce rails settled in USDC on Base via x402. The main endpoint answers live with 57 tools (verified October 25, 2026), plus 13 more across the dedicated split, conditional, and invoice endpoints and 6 on the money-back endpoint.

- Status: live
- Chain and asset: Base mainnet; native USDC
- Fees: 10 free calls per wallet per rolling 30 days, shared across paid endpoints; then 0.10 USDC per call for most tools, 1.00 for diligenceops-paid-run, 0.25 for daily-operator-brief, 2.00 per delegated-authority mandate
- Run by: Wever Labs
- https://weverlabs.com/llms.txt

### Circle Agent Stack

Policy-controlled agent wallets to hold and spend USDC, per-request x402 payments, gas-free nanopayments, and a marketplace to discover payable services.

- Status: live (Agent Marketplace still emerging)
- Chain and asset: USDC (also EURC) on Arbitrum, Arc, Avalanche, Base, Ethereum, Monad, Optimism, Polygon PoS, Unichain
- Fees: gas $0 (sponsored) on agent-wallet transactions; swap provider fee 2 bps; Gateway protocol fee 0.5 bps on cross-chain x402 payments, free same-chain; nanopayments down to $0.000001
- Run by: Circle Internet Group
- https://developers.circle.com/agent-stack

### Stripe for AI agents

Agent Toolkit (MCP server, skills, CLI) plus the Agentic Commerce Suite for merchants selling through agents, on Stripe's fiat and stablecoin rails.

- Status: live, with some features still in preview
- Chain and asset: fiat card and bank rails; stablecoin acceptance
- Fees: standard card processing 2.9% + 30 cents per successful domestic card transaction; stablecoin acceptance 1.5%; dispute fee $15.00
- Run by: Stripe
- https://docs.stripe.com/agents/how-it-works

### Nevermined

Payments and monetization for AI agents: metering, pricing plans, access control, and settlement, including delegated card spending via x402.

- Status: live
- Chain and asset: fiat via Stripe, PayPal/Braintree, and Visa card delegation; crypto USDC and EURC; x402 on Base, Solana, Polygon
- Fees: check directly; their own published pages differ (1% vs 1% to 2%)
- Run by: Nevermined AG
- https://nevermined.ai

### Tempo

A payments-first Layer 1 built for stablecoin payments, global payouts, agentic payments, and enterprise settlement. MPP is its companion open standard.

- Status: live
- Chain and asset: the Tempo L1 itself; USD stablecoins (TIP-20), gas paid in stablecoins
- Fees: not published
- Run by: Tempo (Tempo Labs)
- https://tempo.xyz

### Corbits

Originally an x402 API-monetization product; now a platform for deploying secure, auditable agents with organizational guardrails. Its x402 payments docs and API remain live.

- Status: live, but repositioned (payments is no longer the headline product)
- Chain and asset: USDC; Solana, Base, Polygon, Monad
- Fees: not published
- Run by: Corbits
- https://docs.corbits.dev/getting-started/intro

## Escrow and conditional payments

Money locked until a condition is met, then released or refunded.

### Wever conditional payments / escrow

Locks USDC in a Base escrow contract, releases in full at a release time or on the named approver's approval, refunds in full to the payer after the deadline. Payer-only cancel before release.

- Status: live
- Chain and asset: Base mainnet; native USDC
- Fees: 0.10 USDC per call under the shared 10 free calls per wallet per rolling 30 days; maximum 300 USDC per payment
- Run by: Wever Labs
- https://weverlabs.com/conditional-payments/

## Splits and payouts

One payment divided across multiple recipients.

### Wever split payments

Splits one USDC payment across 2 to 32 recipients in a single atomic execution, by percentage or fixed amounts.

- Status: live
- Chain and asset: Base mainnet; native USDC
- Fees: 0.10 USDC per call under the shared 10 free calls per wallet per rolling 30 days; maximum 300 USDC per split
- Run by: Wever Labs
- https://weverlabs.com/split-payments/

## Invoicing

Shareable bills an agent or human pays once.

### Wever invoicing

Creates shareable USDC invoices that an agent or human pays once via x402. Paid invoices keep their completed status. One payment authorization per invoice.

- Status: live
- Chain and asset: Base mainnet; native USDC
- Fees: 0.10 USDC per call under the shared 10 free calls per wallet per rolling 30 days; maximum invoice 300 USDC
- Run by: Wever Labs
- https://weverlabs.com/invoices/

## Disputes and refunds

A process for contesting a payment and resolving it.

### Wever dispute resolution rail

Opens a dispute over a funded escrow or work order, pauses release and refund, both sides submit evidence, and the operator signs a release, refund, or split decision. Unresolved funds return to the payer after 14 days.

- Status: live
- Chain and asset: Base mainnet; native USDC (escrow and work-order funds)
- Fees: 0.10 USDC per call; limit 25 USDC per case and 100 USDC resolved per UTC day
- Run by: Wever Labs
- https://weverlabs.com/api/dispute-contract

## Wallet and identity for agents

Wallets, credentials, and registries that let an agent hold funds and prove who it is.

### Skyfire

The agent trust stack: verified Know Your Agent (KYA) identity plus an agentic wallet and checkout so agents can access sites, log in, and pay on a user's behalf.

- Status: live
- Chain and asset: USDC plus tokenized card payments; chain not specified
- Fees: not published
- Run by: Skyfire
- https://skyfire.xyz

### ERC-8004 - Trustless Agents

An Ethereum draft standard giving agents portable onchain identity (an ERC-721 NFT), a reputation registry for client feedback, and a validation registry for independent checks of completed work. Payments are deliberately out of scope.

- Status: draft standard, with a mainnet Identity Registry deployed
- Chain and asset: any EVM chain; none (identity only)
- Fees: none (the standard defines no fees; ordinary gas only)
- Run by: open Ethereum EIP, no single company
- https://eips.ethereum.org/EIPS/eip-8004

### ENS for agents (ENSIP-25)

An official ENS standard that lets an ENS name verifiably link to an AI agent registered in an onchain registry such as ERC-8004, using a single text record. ENS itself is general naming infrastructure, not an agent product.

- Status: live as a published standard
- Chain and asset: Ethereum (ENS names); none (naming only)
- Fees: not published (no agent-specific pricing)
- Run by: ENS (community-governed)
- https://docs.ens.domains/ensip/25/

## Card rails for agents

Card-network products that let agents spend within limits on existing card rails.

### Visa Intelligent Commerce

Opens Visa's payment network to AI agents so they can find, shop, and buy on a consumer's behalf using tokenized AI-Ready Cards, with consumer-set spending limits and transaction controls.

- Status: pilot (live in sandbox, rollout planned for 2026)
- Chain and asset: card network; fiat card payment, not crypto
- Fees: not published
- Run by: Visa
- https://usa.visa.com/about-visa/newsroom/press-releases.releaseId.22276.html

### Mastercard Agent Pay

Tokenized payment credentials (Agentic Tokens) that let AI agents buy on behalf of consumers and businesses within approved limits. Agent Pay for Machines extends this to agents paying other agents and services for digital services over x402.

- Status: pilot (Agent Pay for Machines in early access, not available commercially)
- Chain and asset: card-network fiat; Agent Pay for Machines settles via Base in fiat or stablecoins
- Fees: not published
- Run by: Mastercard
- https://www.mastercard.com/global/en/news-and-trends/press/2026/october/Mastercard-Agent-Pay-for-Machines-in-action.html

## Marketplaces and directories

Places where agents discover payable services or hire each other.

### OKX AI Agent Marketplace (A2MCP)

A marketplace where AI agents list services and hire each other, paying on delivery through escrow smart contracts or instant pay-per-call (A2MCP) transactions under one shared onchain identity.

- Status: live
- Chain and asset: multiple EVM chains and Solana; settlement in USDT or USDG
- Fees: no service fees currently; users pay gas and third-party protocol fees; providers set their own prices
- Run by: OKX
- https://www.okx.com/en-ae/learn/okx-ai

### x402 Bazaar

The discovery layer for x402: a machine-readable catalog of payable HTTP endpoints and MCP tools that agents can search, then pay for and call.

- Status: live but early-stage (its own docs call it "more like Yahoo search" for now)
- Chain and asset: Base, Base Sepolia, Solana, Solana Devnet; USDC payments
- Fees: listing is free; services set their own per-call prices, paid via x402
- Run by: x402 Foundation
- https://docs.x402.org/extensions/bazaar

## Communication layer (framing, not payments)

MCP and A2A are included because they frame the map. They are not payment rails.

### MCP - Model Context Protocol

An open standard that lets AI applications connect to external data sources, tools, and workflows through one interface. The agent-to-tool layer.

- Status: live
- Chain and asset: none
- Fees: none (open protocol)
- Run by: originated by Anthropic; now with the Agentic AI Foundation under the Linux Foundation
- https://modelcontextprotocol.io

### A2A - Agent2Agent Protocol

An open standard for agent-to-agent communication: agents discover each other via Agent Cards, delegate tasks, and share results. AP2 is designed as an extension of A2A.

- Status: live
- Chain and asset: none
- Fees: none (open protocol)
- Run by: originated by Google; now with the Linux Foundation
- https://a2a-protocol.org

## About this map

Wever Labs made this map because the money layer was the one layer nobody had mapped. Agents can find each other and talk to each other. Paying each other, with a human in charge of the decision, is the part still being built, and builders deserve one honest page that shows all of it.

Wever Pay is our own product. It is one entry among 23 here, listed on the same terms as the rest, with its real prices and limits. The other rails are listed because they are real, not because they agree with us. If an entry here is wrong or out of date, that is a bug in the map, and we want to know.

## Contributing

Additions and corrections are welcome by pull request. An entry needs a public source (official docs, site, or specification), a verifiable live status, and fees stated as published or marked not published. Do not submit marketing claims as facts. Keep the data files in sync with the README: one entry in `agent-commerce-map.json`, the same entry in `agent-commerce-map.yaml`, under an existing category in `agent-commerce-categories.yaml`.

## License

MIT. See `LICENSE`.
