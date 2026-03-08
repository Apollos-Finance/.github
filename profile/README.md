# 🏛️ Apollos Finance
### The Autonomous Hedge Fund System

![Apollos Finance Banner](OG-Banner.jpeg)

Welcome to the official home of **Apollos Finance**, a decentralized yield protocol built on **Arbitrum** and **Base**. Apollos Finance pioneers the next generation of DeFi by integrating institutional-grade risk management with seamless cross-chain accessibility and decentralized AI intelligence.

---

## 🌟 The Apollos Edge (Key Features)

In the current DeFi landscape, liquidity providers are often caught between two fires: **Impermanent Loss (IL)** and **Loss-Versus-Rebalancing (LVR)**. Apollos Finance solves this through a multi-layered "Intelligence" approach:

*   **📈 Linearized Yield Engine:** High-performance 2x leveraged vaults that utilize **Aave V3 Credit Delegation** to neutralize price exposure, transforming market volatility into consistent delta-neutral yield.
*   **⚔️ Active LVR Protection:** Real-time LVR protection via **Uniswap V4 Hooks** and **Chainlink CRE**. Our "Reactive Defender" uses **Gemini AI** to detect toxic arbitrage flow in real-time and dynamically adjusts swap fees to protect LP profit.
*   **📊 Predictive Risk Analytics (VaR):** Beyond static data, Apollos provides **Value at Risk (VaR)** scores. Calculated via decentralized historical simulation, this gives users a real-time percentage estimate of potential hourly losses under extreme conditions.
*   **🛡️ Autonomous Solvency Audit:** A persistent **Circuit Breaker** system that monitors collateral-to-debt ratios 24/7. It can automatically pause borrowing or entire vaults to prevent liquidation during black-swan events.
*   **🧠 AI-Powered Transparency:** Our **Guardian Logs** translate complex technical events (rebalances, fee spikes, solvency audits) into natural language using AI, ensuring users always know the "Why" behind protocol movements.
*   **🌉 Seamless Cross-Chain UX:** A persistent "Store-and-Execute" architecture powered by **Chainlink CCIP** that enables "Auto-Zap" deposits across chains with a single click.

---

## 🏗️ The Modular Ecosystem

The Apollos Finance protocol is split into four specialized layers, each serving a critical role in our autonomous architecture:

### 🔗 [apollos-sc](https://github.com/ApollosFinance/apollos-sc) (The Core Layer)
The decentralized heart of the protocol, managing assets, leverage, and liquidity.
*   **ApollosVault.sol:** Hybrid ERC4626 vaults managing 2x leverage via **Aave V3 Credit Delegation** and custom off-chain NAV pricing.
*   **ApollosFactory.sol:** The central registry and factory responsible for deploying and tracking authorized leveraged vault markets.
*   **ApollosRouter.sol:** The primary user-facing entry point for local-chain deposits, withdrawals, and asset interactions.
*   **ApollosCCIPReceiver.sol:** A sophisticated cross-chain engine that handles **Chainlink CCIP** messages, supporting "Store-and-Execute" and "Auto-Zap" (bridging USDC and instantly depositing into vaults).
*   **SourceChainRouter.sol:** A lightweight router for non-hub chains (e.g., Base Sepolia) to initiate cross-chain deposit requests to the Arbitrum Hub.
*   **LVRHook.sol:** An advanced **Uniswap V4 Hook** that protects Liquidity Providers by dynamically adjusting swap fees based on AI-detected market volatility.
*   **DataFeedsCache.sol:** A high-speed on-chain cache storing decentralized AI-validated data, including NAV, VaR scores, and protocol health metrics.
*   **GenericWorkflowReceiver.sol:** A secure, decentralized security gateway that validates and routes authenticated reports from the **Chainlink DON**.

### 🧠 [apollos-cre](https://github.com/ApollosFinance/apollos-cre) (The Decentralized Brain)
Our "Off-Chain Intelligence Hub" powered by the **Chainlink Runtime Environment (CRE)**. We deploy a fleet of 7 specialized, decentralized workflows that form the operational mind of the protocol:
*   **⚔️ The Defender (LVR Protection):** *(Trigger: HTTP/Indexer)* An event-driven risk classifier. It listens to Uniswap V4 swap events in real-time, fetches binance and chainlink oracle volatility data, and queries **Gemini AI**. If toxic arbitrage is detected, it instantly triggers the LVRHook to dynamically raise swap fees.
*   **🛡️ The Auditor (Circuit Breaker):** *(Trigger: Cron)* An autonomous solvency monitor. Running on a strict schedule, it calculates high-precision Aave V3 collateral-to-debt ratios. It enforces 3 severity levels (Warn, Critical, Emergency) to automatically pause vault borrowing or entirely halt operations if health factors plummet.
*   **📊 The VaR Calculator (Risk Analyst):** *(Trigger: Cron)* An institutional-grade risk simulator. It fetches historical market Klines, executes a 95% Confidence Historical Simulation, adjusts the risk against the vault's real-time leverage, and publishes the resulting Basis Points (BPS) risk score securely on-chain.
*   **⚖️ The Strategist (Rebalancer):** *(Trigger: Cron)* The deterministic leverage engine. It constantly monitors the optimal 2x risk profile. If Aave Health Factors stray out of safe bounds, it autonomously executes complex on-chain rebalancing operations (leveraging up or de-leveraging).
*   **🧮 The Accountant (NAV Pricer):** *(Trigger: Cron)* The truth-seeker for share pricing. It synthesizes the total asset value across raw token balances, active Uniswap V4 LP positions, and Aave V3 debt/collateral to publish a hyper-accurate Net Asset Value (NAV) to the DataFeedsCache.
*   **🌉 The Bridge Manager:** *(Trigger: Cron)* The cross-chain logistics optimizer. It monitors adapter token balances on source chains (like Base) and automatically triggers CCIP "Store-and-Execute" batches to the Arbitrum Hub only when gas-efficient thresholds are met.
*   **📢 The Reporter (AI Transparency):** *(Trigger: EVM Log)* The voice of the protocol. It ingests raw technical blockchain logs (e.g., rebalances, fee spikes), prompts **Gemini AI** to translate them into human-readable narratives, and posts these "Guardian Logs" to the backend for the frontend dashboard.

### 🛰️ [apollos-be](https://github.com/ApollosFinance/apollos-be) (The Observability Hub)
A high-performance ingestion layer that bridges the decentralized DON with the user interface.
*   **Log Ingestion:** Validates and stores AI-generated "Guardian" narratives from CRE.
*   **Status API:** Provides a unified health dashboard for all protocol workers and background tasks.
*   **Intelligence Hub:** Analyzes historical market divergence between oracles and spot prices for transparency reports.

### 🏛️ [apollos-fe](https://github.com/ApollosFinance/apollos-fe) (The Command Center)
A sophisticated dashboard for managing cross-chain leveraged positions.
*   **Unified Dashboard:** Real-time management of afWETH, afWBTC, and afLINK positions with yield tracking.
*   **Bridge Flow UI:** Persistent cross-chain state machine that guides users through the CCIP "Store-and-Execute" process.
*   **Risk Visualizer:** Real-time visualization of VaR scores, Health Factors, and AI-driven protection logs.
*   **Protocol Transparency:** Integrated "Guardian Logs" displaying natural language explanations of all automated actions.

---

## 🛠️ Technology Stack

| Layer | Technologies |
| :--- | :--- |
| **Blockchain** | Solidity 0.8.20+, Foundry, Arbitrum Sepolia, Base Sepolia |
| **Interoperability** | Chainlink CCIP (Store-and-Execute), Cross-Chain Zap |
| **Intelligence** | Chainlink Runtime Environment (CRE), Keystone SDK |
| **Artificial Intelligence** | Google Gemini 2.0 Flash / 1.5 Pro |
| **Liquidity & Lending** | Uniswap V4 (Hooks), Aave V3 (Credit Delegation) |
| **Frontend** | Next.js 15 (App Router), Wagmi v2, Viem, Tailwind CSS v4 |

---

## 🚀 Join the Mission

Apollos Finance is more than a yield protocol; it's an experiment in combining **Decentralized Infrastructure** with **Artificial Intelligence** to create a safer, more efficient, and truly human-readable financial future.
*   **Learn more:** Check out our integrated documentation in the [Docs](https://apollos-finance.vercel.app/docs).

---
*Built with 🔥 by Apollos Finance Team to make DeFi smarter, safer, and human-readable.*
