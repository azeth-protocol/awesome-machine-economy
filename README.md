# Awesome Machine Economy [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of infrastructure for autonomous machine-to-machine commerce — where AI agents discover, trust, and pay each other.

The machine economy is the infrastructure layer where AI agents operate as economic participants: they hold funds, build reputation, discover services, negotiate terms, and settle payments — all without human intervention. This list covers the building blocks.

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

---

## Contents

- [The Stack](#the-stack)
- [Identity and Trust](#identity-and-trust)
- [Smart Accounts](#smart-accounts)
- [Payments](#payments)
- [Discovery and Registries](#discovery-and-registries)
- [Reputation](#reputation)
- [Messaging and Communication](#messaging-and-communication)
- [Agent Frameworks](#agent-frameworks)
- [MCP Servers](#mcp-servers)
- [Developer Tools](#developer-tools)
- [Standards](#standards)
- [Research](#research)

---

## The Stack

Machines participating in the economy need the same things humans need: an identity, a wallet, a way to find services, a way to communicate, and a way to pay. The difference is everything must be programmable, verifiable, and autonomous.

```
 Identity ─── Who am I? Can you trust me?
    │
 Account ──── Where do I hold funds? What are my limits?
    │
 Discovery ── How do I find the right service?
    │
 Messaging ── How do we negotiate and coordinate?
    │
 Payment ──── How do I pay and get paid?
    │
 Reputation ─ Did it go well? Would I use them again?
```

Each layer below maps to a part of this stack.

---

## Identity and Trust

*How machines prove who they are and establish trust.*

### On-Chain Identity

- [ERC-8004](https://eips.ethereum.org/EIPS/eip-8004) - Machine economy trust registry. On-chain identity, reputation, and validation for agents, services, and infrastructure. ERC-721 based.
- [Ethereum Attestation Service (EAS)](https://attest.org/) - On-chain and off-chain attestation infrastructure. Schema-based, composable attestations.
- [Verax](https://www.ver.ax/) - Attestation registry on Linea. Composable on-chain trust signals.
- [Olas Registry](https://registry.olas.network/) - On-chain agent registration via NFTs. Staking-based commitment signals.
- [ENS](https://ens.domains/) - Human-readable names for addresses and service endpoints.

### Authentication

- [ERC-8128](https://eips.ethereum.org/EIPS/eip-8128) - Sign-in with agents. HTTP challenge-response authentication using smart account signatures.
- [SIWE (Sign-In with Ethereum)](https://login.xyz/) - Authentication standard for Ethereum wallets. Foundation for agent auth flows.
- [W3C Decentralized Identifiers](https://www.w3.org/TR/did-core/) - Self-sovereign identity standard. Underlies many agent identity systems.
- [W3C Verifiable Credentials](https://www.w3.org/TR/vc-data-model/) - Cryptographically verifiable claims. Used by Google AP2 for agent authorization.
- [ZKProofport](https://zkproofport.app) - Zero-knowledge proof generation for AI agent identity. Prove Coinbase KYC, Country, Google OIDC, Google Workspace, or Microsoft 365 affiliation without revealing personal data. AWS Nitro Enclave TEE proving, x402-paid, ERC-8004 registered. ([Agent MCP](https://www.npmjs.com/package/@zkproofport-ai/mcp) | [GitHub](https://github.com/zkproofport/proofport-ai))

### Full-Stack Trust Infrastructure

- [Azeth](https://azeth.ai) - ERC-8004 identity, on-chain reputation, guardian-protected smart accounts, x402 payments, and service discovery in one SDK. MCP server with 30+ tools for AI agents. ([GitHub](https://github.com/azeth-protocol) | [npm](https://www.npmjs.com/package/@azeth/sdk))

---

## Smart Accounts

*Programmable wallets with enforced limits — machines that can hold and spend funds safely.*

### Standards

- [ERC-4337](https://eips.ethereum.org/EIPS/eip-4337) - Account abstraction. UserOperations, bundlers, paymasters. Smart accounts can pay gas in any token.
- [ERC-7579](https://eips.ethereum.org/EIPS/eip-7579) - Modular smart accounts. Validators, executors, hooks — interoperable across implementations.
- [ERC-7715](https://eips.ethereum.org/EIPS/eip-7715) - Session keys. Time-bounded, amount-limited, scope-restricted delegated signing.
- [ERC-6900](https://eips.ethereum.org/EIPS/eip-6900) - Modular account standard (alternative to 7579). Plugin-based architecture.

### Platforms

- [ZeroDev](https://zerodev.app/) - Modular smart account SDK. Session keys, batched transactions, gas sponsorship. ERC-7579 native.
- [Safe](https://safe.global/) - Multi-sig and modular smart accounts. $100B+ secured. Extensive module ecosystem.
- [Biconomy](https://biconomy.io/) - Smart account platform with session keys, paymaster, and bundler.
- [Coinbase Smart Wallet](https://www.coinbase.com/wallet/smart-wallet) - Passkey-based smart accounts on Base. Gas sponsorship built in.

### Infrastructure

- [Pimlico](https://pimlico.io/) - ERC-4337 bundler and paymaster. Alto (open-source bundler).
- [Stackup](https://stackup.sh/) - ERC-4337 bundler and paymaster infrastructure.
- [Alchemy Account Kit](https://www.alchemy.com/account-kit) - Smart account SDK with embedded wallets and gas management.

---

## Payments

*How machines pay each other — from micropayments to streaming to subscriptions.*

### x402 (HTTP 402)

The HTTP-native payment protocol. Server returns 402 with payment requirements, client pays on-chain, retries with proof.

- [x402 Protocol](https://github.com/coinbase/x402) - The specification. Coinbase + Cloudflare. USDC-native, middleware-friendly.
- [@x402/hono](https://www.npmjs.com/package/@x402/hono) - x402 middleware for Hono.
- [@x402/express](https://www.npmjs.com/package/@x402/express) - x402 middleware for Express.
- [@x402/fetch](https://www.npmjs.com/package/@x402/fetch) - Fetch wrapper that auto-handles 402 responses.
- [@azeth/provider](https://www.npmjs.com/package/@azeth/provider) - x402 provider tooling. Pre-settled smart account payments, SIWx sessions, payment agreements. ([GitHub](https://github.com/azeth-protocol/provider))
- [xPay Facilitator](https://github.com/xpaysh/xpay-x402) - Open x402 facilitator. No auth required.
- [@zkproofport-ai/mcp](https://www.npmjs.com/package/@zkproofport-ai/mcp) - Zero-knowledge proof generation MCP server paid via x402. Agents pay USDC on Base for ZK identity proofs (Coinbase KYC, Country, Google OIDC, Workspace, MS 365). Server-side proving in AWS Nitro Enclave TEE.

### Other Payment Protocols

- [Google AP2](https://developers.google.com/pay/agents) - Agent payment authorization. Payment-agnostic, Verifiable Credentials for audit trails.
- [OpenAI ACP](https://openai.com/) - Agentic Commerce Protocol. Stripe-powered checkout for ChatGPT and consumer AI.
- [Visa TAP](https://developer.visa.com/) - Trusted Agent Protocol. TradFi-to-crypto agent payment bridge.
- [Mastercard Agent Pay](https://developer.mastercard.com/) - Tokenized payments and agent wallet integration via card networks.
- [Superfluid](https://superfluid.finance/) - Real-time payment streaming. Pay per second for continuous services.
- [Sablier](https://sablier.com/) - Token streaming. Linear and dynamic payment schedules.
- [Lightning Network](https://lightning.network/) - Bitcoin L2. Sub-second settlement, near-zero fees.
- [Pay3](https://pay3.io/) - Stablecoin automation for agents. USDC/USDT autonomous payouts.

---

## Discovery and Registries

*How machines find the right service for a task.*

- [ERC-8004](https://eips.ethereum.org/EIPS/eip-8004) - On-chain trust registry. Query by capability, entity type, reputation. Universal for agents, services, and infrastructure.
- [Google A2A Agent Cards](https://google.github.io/a2a/) - JSON manifests at `/.well-known/agent.json`. Describe capabilities, skills, and interaction modes.
- [Glama](https://glama.ai/mcp/servers) - MCP server directory. Search, verify, and browse Model Context Protocol servers.
- [Smithery](https://smithery.ai/) - MCP server hosting and marketplace. Deploy and discover MCP servers.
- [mcp.so](https://mcp.so/) - MCP server registry. Searchable directory with install instructions.
- [PulseMCP](https://pulsemcp.com/) - MCP server directory with categories and ratings.
- [Olas](https://olas.network/) - Decentralized agent registry. NFT-based, staking-required registration.

---

## Reputation

*How machines build track records — objective, on-chain, payment-weighted.*

- [ERC-8004 Reputation Registry](https://eips.ethereum.org/EIPS/eip-8004) - On-chain reputation linked to identity entries. Stores feedback per interaction.
- [Azeth Reputation](https://azeth.ai) - Multi-dimensional scoring: uptime, response time, success rate, volume. Auto-feedback after every x402 payment. Reputation-aware service routing.
- [Karma3Labs](https://karma3labs.com/) - EigenTrust-based reputation. Compute global trust from local interactions via graph algorithms.
- [Gitcoin Passport](https://passport.gitcoin.co/) - Sybil-resistance via composable identity stamps. Aggregate proofs into a single score.
- [DegenScore](https://degenscore.com/) - On-chain reputation for DeFi. Soulbound tokens as proof of expertise.
- [Orange Protocol](https://orangeprotocol.io/) - Reputation and trust infrastructure. Composable reputation models.

---

## Messaging and Communication

*How machines negotiate, coordinate, and stream results.*

### Agent-to-Agent

- [XMTP](https://xmtp.org/) - E2E encrypted messaging for wallets and agents. Discovery via address. ([Agent SDK](https://www.npmjs.com/package/@xmtp/agent-sdk))
- [Google A2A](https://google.github.io/a2a/) - Agent-to-agent protocol. Task lifecycle, streaming, push notifications.
- [IBM ACP](https://github.com/IBM/acp) - Agent Communication Protocol. Cross-framework messaging with human-in-the-loop.
- [Waku](https://waku.org/) - Decentralized messaging protocol. Privacy-preserving, censorship-resistant.

### Agent-to-Tool

- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) - Anthropic's AI-to-tool protocol. Tools, resources, prompts. Adopted by Claude, Cursor, Windsurf.
- [OpenAI Function Calling](https://platform.openai.com/docs/guides/function-calling) - Structured tool use for GPT models.
- [LangChain Tools](https://python.langchain.com/docs/modules/tools/) - Tool abstraction layer for LLM applications.

---

## Agent Frameworks

*Frameworks for building AI agents that participate in the economy.*

- [LangGraph](https://langchain-ai.github.io/langgraph/) - Graph-based agent orchestration. Multi-agent workflows, persistence, human-in-the-loop.
- [CrewAI](https://crewai.com/) - Multi-agent collaboration. Role-based agents with delegation and task management.
- [OpenAI Agents SDK](https://github.com/openai/openai-agents-python) - Official OpenAI agent framework. Tool use, handoffs, guardrails.
- [AutoGPT](https://agpt.co/) - Autonomous AI agent platform. Long-running tasks, web interaction.
- [OpenClaw](https://openclaw.ai/) - Personal AI assistant. Cross-platform, skill-based architecture.
- [Eliza](https://elizaos.github.io/eliza/) - Multi-agent simulation. Character-based agents with social interaction.
- [CAMEL](https://www.camel-ai.org/) - Multi-agent communication framework for large-scale agent behavior.

---

## MCP Servers

*MCP servers for payments, DeFi, and machine economy operations.*

- [Azeth MCP](https://www.npmjs.com/package/@azeth/mcp-server) - Smart accounts, x402 payments, reputation, discovery, messaging. 30+ tools. ([GitHub](https://github.com/azeth-protocol/mcp-server))
- [Coinbase AgentKit](https://github.com/coinbase/agentkit) - Wallet management, transfers, DeFi on Base.
- [deBridge MCP](https://debridge.finance/) - Cross-chain swaps and bridges.
- [Stripe Agent Toolkit](https://github.com/stripe/agent-toolkit) - Payment processing, invoicing, subscriptions.
- [Uniswap MCP](https://github.com/uniswap) - DEX swaps and liquidity.
- [1inch MCP](https://1inch.io/) - DEX aggregator for optimal swap routing.
- [Aave MCP](https://aave.com/) - Lending and borrowing protocol tools.

> See [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) for the comprehensive MCP directory.

---

## Developer Tools

*SDKs, CLIs, and infrastructure for building in the machine economy.*

- [Azeth SDK](https://www.npmjs.com/package/@azeth/sdk) - TypeScript SDK. Smart accounts, x402 payments, reputation, discovery, messaging. ([GitHub](https://github.com/azeth-protocol/sdk))
- [Azeth CLI](https://www.npmjs.com/package/@azeth/cli) - Register, discover, pay, and manage machine participants from the terminal.
- [viem](https://viem.sh/) - TypeScript Ethereum library. Type-safe, tree-shakeable.
- [ethers.js](https://ethers.org/) - Complete Ethereum library. Widely adopted.
- [wagmi](https://wagmi.sh/) - React hooks for Ethereum.
- [Foundry](https://book.getfoundry.sh/) - Smart contract toolchain. Fast compilation, native fuzzing, Solidity testing.
- [Hardhat](https://hardhat.org/) - Ethereum development environment. Testing, debugging, deployment.
- [Tenderly](https://tenderly.co/) - Smart contract monitoring, debugging, and simulation.

---

## Standards

| Standard | What it does | Status |
|----------|-------------|--------|
| [ERC-4337](https://eips.ethereum.org/EIPS/eip-4337) | Account abstraction | Final |
| [ERC-6900](https://eips.ethereum.org/EIPS/eip-6900) | Modular accounts (alt) | Draft |
| [ERC-7579](https://eips.ethereum.org/EIPS/eip-7579) | Modular accounts | Draft |
| [ERC-7715](https://eips.ethereum.org/EIPS/eip-7715) | Session keys | Draft |
| [ERC-8004](https://eips.ethereum.org/EIPS/eip-8004) | Trust registry | Draft |
| [ERC-8128](https://eips.ethereum.org/EIPS/eip-8128) | Agent authentication | Draft |
| [x402](https://github.com/coinbase/x402) | HTTP payments | Active |
| [MCP](https://modelcontextprotocol.io/) | AI-to-tool protocol | Active |
| [A2A](https://google.github.io/a2a/) | Agent-to-agent protocol | Active |
| [CAIP-2](https://chainagnostic.org/CAIPs/caip-2) | Chain identifiers | Final |
| [CAIP-10](https://chainagnostic.org/CAIPs/caip-10) | Account identifiers | Final |

---

## Research

- [Coinbase: x402 Vision](https://www.coinbase.com/blog/x402-the-internet-payments-protocol) - HTTP 402 as the internet's native payment layer.
- [a16z: Crypto x AI](https://a16zcrypto.com/) - Why crypto infrastructure matters for autonomous agents.
- [Vitalik: Account Abstraction Roadmap](https://vitalik.eth.limo/) - The path to smart accounts as default.
- [McKinsey: AI Agent Economy](https://www.mckinsey.com/) - $5T projected market by 2030.
- [Gartner: Agentic AI](https://www.gartner.com/) - Enterprise agent adoption trends and forecasts.

---

## Contributing

Contributions welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
