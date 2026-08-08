# Chainlink Prediction Settler

[![CI](https://github.com/tenalirama2005/chainlink-prediction-settler/actions/workflows/rust.yml/badge.svg)](https://github.com/tenalirama2005/chainlink-prediction-settler/actions)
[![Solidity](https://img.shields.io/badge/Solidity-0.8.19-363636?logo=solidity)](contracts/PredictionMarket.sol)
[![Rust](https://img.shields.io/badge/Rust-1.75-orange?logo=rust)](settler/)
[![Chainlink CRE](https://img.shields.io/badge/Chainlink-CRE-375BD2?logo=chainlink)](workflow/)
[![Network](https://img.shields.io/badge/Network-Sepolia-6851FF)](https://eth-sepolia.blockscout.com/address/0xEA856dF995C58DEc18221C907DC221c4487Ae499)
[![Blog](https://img.shields.io/badge/dev.to-Blog-0A0A0A?logo=devdotto)](https://dev.to/tenalirama2025/how-i-built-3-chainlink-cre-workflows-in-one-week-fba-oracle-privacy-payroll-defi-4nha)
[![Demo Video](https://img.shields.io/badge/YouTube-Demo_Video-red?logo=youtube)](https://youtu.be/YD14xtCYnM0)
[![CRE Workflows](https://img.shields.io/badge/CRE_Workflows-3_Active-375BD2)](https://chain.link)
[![Deployment](https://img.shields.io/badge/Deployment-Live-brightgreen)](https://chain.link)

> FBA oracle + privacy payroll + DeFi intelligence — 3 CRE workflows on Chainlink

An AI-powered prediction market settlement system applying Stellar's Federated
Byzantine Agreement (FBA) protocol to multi-LLM oracles for Byzantine
fault-tolerant on-chain settlement.

---

## Quick Start

### Prerequisites

**1. Install Rust:**
```powershell
winget install Rustlang.Rust.MSVC
```

**2. Install Bun:**
```powershell
winget install Oven-sh.Bun
```

**3. Install CRE CLI:**
```powershell
bun x cre-setup
```

**4. Clone and build:**
```powershell
git clone https://github.com/tenalirama2005/chainlink-prediction-settler
cd chainlink-prediction-settler
cargo build
```

### Run Everything with One Command

```powershell
.\deploy.ps1
```

Interactive menu handles everything:

```
╔══════════════════════════════════════════════════════════════╗
║     Chainlink Prediction Settler — FBA Consensus Oracle      ║
║     3 CRE Workflows: FBA Oracle + Privacy Payroll + DeFi     ║
╚══════════════════════════════════════════════════════════════╝

Select an option:

  [1] Simulate FBA Consensus        (FREE — no API keys needed)
  [2] Live FBA Consensus             (requires Claude + OpenAI API keys)
  [3] Run ALL 3 CRE Simulations      (requires CRE CLI)
  [4] Run payroll_mcp simulation     (requires CRE CLI)
  [5] Run hyperliquid_mcp — Live DEX prices BTC/ETH/DOGE (requires CRE CLI)
  [6] Run ai_prediction_mcp simulation (requires CRE CLI)
  [7] Check contract status          (FREE — no API keys needed)
  [8] Deploy to CRE                  (requires CRE Early Access)
  [9] Exit
```

**Start with Option 1** — free, no API keys, no CRE account needed.
**Option 3** runs all 3 CRE workflows in sequence automatically.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    CHAINLINK CRE LAYER                          │
│                                                                 │
│  ┌──────────────┐  ┌──────────────────┐  ┌──────────────────┐  │
│  │ payroll_mcp  │  │ hyperliquid_mcp  │  │ ai_prediction    │  │
│  │              │  │                  │  │ _mcp             │  │
│  │ Privacy-     │  │ DEX Market       │  │ FBA Oracle       │  │
│  │ preserving   │  │ Intelligence     │  │ (Claude+GPT-4o)  │  │
│  │ batch settle │  │ BTC/ETH spreads  │  │                  │  │
│  └──────┬───────┘  └────────┬─────────┘  └────────┬─────────┘  │
└─────────┼───────────────────┼──────────────────────┼────────────┘
          │                   │                      │
          ▼                   ▼                      ▼
┌─────────────────────────────────────────────────────────────────┐
│                    RUST CLI (settler)                           │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │              FBA CONSENSUS ENGINE                       │   │
│  │   Claude Opus ──┐                                       │   │
│  │                 ├──► Quorum Intersection ──► SETTLE     │   │
│  │   GPT-4o    ────┘    (Stellar Protocol)    or REVIEW    │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
          │
          ▼
┌─────────────────────────────────────────────────────────────────┐
│              ETHEREUM SEPOLIA (Smart Contract)                  │
│  PredictionMarket.sol                                           │
│  0xEA856dF995C58DEc18221C907DC221c4487Ae499                    │
│  Question: "Did the Fed cut rates at March 2025 FOMC?"         │
└─────────────────────────────────────────────────────────────────┘
```

---

## Three CRE Workflows

### ai_prediction_mcp — FBA Consensus Oracle
- Claude Opus and GPT-4o independently evaluate prediction statements
- FBA engine computes quorum intersection
- On agreement: auto-settle on-chain
- On disagreement: autonomous settlement BLOCKED — human review triggered
- API keys managed at DON level via CRE secrets — never exposed

### payroll_mcp — Privacy-Preserving Settlement
- Recipient addresses and salary amounts never appear on-chain
- Only keccak256 batch hash recorded on-chain
- CRE Confidential Compute keeps all sensitive data private

### hyperliquid_mcp — DeFi Market Intelligence
- Queries 229 Hyperliquid perpetual markets via CRE Confidential HTTP
- Fetches live prices for BTC, ETH and DOGE simultaneously
- API credentials managed at DON level — never exposed
- Built on prior private Hyperliquid project experience

---

## Live Output Examples

**FBA Consensus:**
```
Statement:    "Did the Fed cut rates at March 2025 FOMC?"
Claude Opus:  NO  |  99% confidence
GPT-4o:       NO  |  95% confidence
FBA Outcome:  NO  |  97% confidence
Quorum:       ✅ INTERSECTED
Safety:       ✅ CLEARED
Action:       SETTLE NO — Fed held rates confirmed
```

**Hyperliquid DEX Live Prices:**
```
✅ BTC: $68,129.50 | Spread: 0.10 bps
📈 Bid: $68,128.82 📉 Ask: $68,130.18

✅ ETH: $1,982.65  | Spread: 0.10 bps
📈 Bid: $1,982.63  📉 Ask: $1,982.67

✅ DOGE: $0.09     | Spread: 0.10 bps
📈 Bid: $0.09      📉 Ask: $0.09

🏦 Market Depth: 229 perpetual markets
🔗 Source: Hyperliquid DEX via CRE Confidential HTTP
```

---

## Live FBA Result

```
Statement:    "Did the Fed cut rates at March 2025 FOMC?"
Claude Opus:  NO  |  99% confidence
GPT-4o:       NO  |  95% confidence
FBA Outcome:  NO  |  97% confidence
Quorum:       ✅ INTERSECTED
Safety:       ✅ CLEARED
Action:       SETTLE NO — Fed held rates confirmed
```

---

## Smart Contract

**PredictionMarket.sol — Ethereum Sepolia**

| Field | Value |
|-------|-------|
| Address | [`0xEA856dF995C58DEc18221C907DC221c4487Ae499`](https://eth-sepolia.blockscout.com/address/0xEA856dF995C58DEc18221C907DC221c4487Ae499) |
| Question | Did the Fed cut rates at March 2025 FOMC? |
| Network | Ethereum Sepolia Testnet |
| Verified | Sourcify ✅ Blockscout ✅ Routescan ✅ |

---
## Hackathon Submission — Tracks Entered

Submitted to the following Chainlink hackathon prize tracks. Amounts shown are the
published track prizes, not winnings. Result: did not place.

| Track | Amount | Qualification |
|-------|--------|---------------|
| Prediction Markets | $16,000 | FBA consensus settles real on-chain predictions |
| Privacy | $16,000 | payroll_mcp — batch hash only, amounts never on-chain |
| CRE & AI | $17,000 | 3 production CRE workflows running on DON |
| Risk & Compliance | $16,000 | FBA blocks unsafe settlements — human review triggered |
| DeFi | $16,000 | hyperliquid_mcp — DEX intelligence via confidential HTTP |

---

## Repository Structure

```
chainlink-prediction-settler/
├── .github/workflows/     # CI — Rust fmt, clippy, build, test
├── contracts/             # PredictionMarket.sol (Solidity)
├── settler/src/           # Rust CLI — main.rs, fba.rs
├── workflow/
│   ├── payroll_mcp/       # Privacy-preserving payroll
│   ├── hyperliquid_mcp/   # DeFi market intelligence
│   └── ai_prediction_mcp/ # FBA consensus oracle
├── deploy.ps1             # ← One command to run everything
└── README.md
```

---

## Author

**Venkateshwar Rao Nagala**

- 📝 Blog: [How I Built 3 Chainlink CRE Workflows in One Week](https://dev.to/tenalirama2025/how-i-built-3-chainlink-cre-workflows-in-one-week-fba-oracle-privacy-payroll-defi-4nha)
- 🎬 Demo: [Chainlink-Prediction-Settler](https://youtu.be/YD14xtCYnM0)
- 🐙 GitHub: [tenalirama2005](https://github.com/tenalirama2005)
- 📧 tenalirama2019@gmail.com

---

*Built with Rust. Orchestrated with Chainlink CRE. Settled on Ethereum Sepolia.*

*From Assembler to blockchain — one late night at a time.* 🚀
