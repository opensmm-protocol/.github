# OpenSMM Protocol

**The open, provider-neutral protocol for ordering and executing social media growth services — built for AI agents.**

One canonical command set over REST and MCP. Pseudonymous provider showcase with gateway-measured quality. Direct settlement over x402 (USDC on Base): money flows agent → provider, never through the gateway.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Protocol](https://img.shields.io/badge/protocol-v0.1--draft-blue.svg)](https://github.com/opensmm-protocol/mcp-server/tree/main/spec/v0)
[![MCP](https://img.shields.io/badge/MCP-compatible-brightgreen.svg)](https://modelcontextprotocol.io)

## Why

Classic SMM panels lock agents out: every panel has its own quirky API, prepaid balances, no idempotency, no machine-readable quality data. OpenSMM separates three concerns they merge into one:

```text
AI Agent
   │
   ▼
OpenSMM Gateway        ← catalog, quotes, payments, idempotency, MCP/REST
   │ canonical commands
   ▼
OpenSMM Provider SPI   ← execution suppliers behind one adapter interface
   │
   ▼
Execution providers    ← classic panel APIs, REST v1 nodes, native workers
```

## The protocol in one minute

- **10 commands**, same over REST `/v0` and MCP: `searchServices → getQuote → createOrder → settle (x402) → getOrder`. One `clientReference` → one `orderId` on any transport.
- **Provider self-onboarding**: `registerProvider` — SSRF-guarded, healthchecked, catalog-synced in one call. Panels join with zero code (`smm-v2` and `rest-v1` dialects built in).
- **Pseudonymous showcase**: providers are `provider-alpha`, `provider-beta`, … Quality metrics are measured by the gateway from real orders, never self-reported. Tiers are computed by an [open formula](https://github.com/opensmm-protocol/mcp-server/blob/main/spec/v0/README.md#91-quality-tiers-computed-open-formula) anyone can verify.
- **Direct settlement (canonical)**: the provider's payout address is the `payTo` of its orders. Gateways route and measure — they don't custody funds.
- **Idempotency, decimal-string money, dual state machines** (`paymentStatus` ≠ `executionStatus`) — enforced by 86 tests.

## Repositories

| Repo | What |
|---|---|
| [`mcp-server`](https://github.com/opensmm-protocol/mcp-server) | Protocol spec v0 (`spec/v0`, JSON Schemas + examples) + reference gateway: core, REST, MCP, provider adapters, x402 rail |

## For AI agents

Start with [`llms.txt`](https://github.com/opensmm-protocol/mcp-server/blob/main/llms.txt).

## For supply nodes

Zero-code onboarding: [`docs/PROVIDER_ONBOARDING.md`](https://github.com/opensmm-protocol/mcp-server/blob/main/docs/PROVIDER_ONBOARDING.md) — including a copy-paste prompt for your AI assistant.

## Legal

OpenSMM is open-source software for routing and measuring API requests — not a marketplace operator, payment processor or escrow agent. Funds move peer-to-peer; the software never holds balances or private keys. MIT licensed, provided "as is".
