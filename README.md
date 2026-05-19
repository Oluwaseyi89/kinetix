# Kinetix Protocol
**Autonomous AI Agents for the Sui Agentic Economy**

![Sui Move](https://img.shields.io/badge/Sui-Move%202024-blue)
![Python Backend](https://img.shields.io/badge/Python-FastAPI--AI-green)
![Next.js Web](https://img.shields.io/badge/Next.js-Frontend-black)
![Walrus Storage](https://img.shields.io/badge/Walrus-Audit--Logs-orange)

Kinetix is an autonomous Agentic Finance (AgentFi) and AI-native payment protocol custom-built for the Sui blockchain. By leveraging Sui's unique programmable object model and Programmable Transaction Blocks (PTBs), Kinetix executes multi-step machine-speed trading strategies, manages automated yield treasuries, and facilitates instantaneous machine-to-machine stablecoin micropayments with absolute financial safety.

## 🌟 Key Features

* **Intent-Driven Execution Engine** - Converts natural language commands into complex on-chain execution paths via an off-chain LLM interpreter.
* **Atomic Strategy Bundling** - Uses Sui PTBs to chain up to 100 deep financial actions (swaps, flash loans, staking) into a single transaction that rolls back cleanly if any parameter fails.
* **Sovereign Agent Objects** - Every automated strategy runs inside an isolated, user-owned Sui Move object vault with custom risk thresholds, bypassing shared-contract vulnerabilities.
* **TEE Secure Signing** - Ephemeral session keys are isolated inside a Trusted Execution Environment (TEE) to handle continuous machine trading safely without exposing root seed phrases.
* **Immutable Inference Audit Trails** - Chronological logs of every AI trade decision and market analysis are directly pushed to the Walrus decentralized storage network for trustless user verification.
* **zkLogin Onboarding** - Zero-friction onboarding allowing Web2 users to generate secure agent infrastructure instantly using Google or Twitch OAuth.

## 📋 Table of Contents

1. [System Architecture](#system-architecture)
2. [Repository Structure](#repository-structure)
3. [Quick Start](#quick-start)
    * [On-Chain Contracts (move)](#on-chain-contracts-move)
    * [AI Backend Core (backend-ai)](#ai-backend-core-backend-ai)
    * [Web Dashboard (frontend-web)](#web-dashboard-frontend-web)
4. [Development Workflow](#development-workflow)
5. [Testing](#testing)
6. [Deployment](#deployment)
7. [Security](#security)
8. [Contributing](#contributing)

## 🏗️ System Architecture
```
┌─────────────────────────────────────────────────────────────────────┐
│                        KINETIX SYSTEM ARCHITECTURE                  │
├─────────────────────────────────────────────────────────────────────┤
│                         Application Layer                           │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │               Next.js Web Dashboard (frontend-web)          │   │
│  │  • zkLogin / Wallet Adapter    • Real-Time Portfolio Yields │   │
│  │  • Intent Terminal UI          • Bot Performance Tracking    │   │
│  └───────────────────┬─────────────────────────────────────────┘   │
│                      │                                             │
│                      ▼ (Natural Language Intent JSON)              │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                    API Gateway & AI Backend                 │   │
│  │             FastAPI + LangChain Server (backend-ai)         │   │
│  └───────────────────┬─────────────────────────────────────────┘   │
│                      │                                             │
│                      ▼                                             │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                Service Layer & Execution                    │   │
│  │  ┌─────────────────┐ ┌─────────────────┐ ┌────────────────┐ │   │
│  │  │ Intent Parser   │ │ PTB Builder     │ │ Secure Signer  │ │   │
│  │  ├─────────────────┤ ├─────────────────┤ ├────────────────┤ │   │
│  │  │ Processes LLM   │ │ Packages atomic │ │ TEE Enclave    │ │   │
│  │  │ market paths    │ │ Move arguments  │ │ signs sub-sec  │ │   │
│  │  └────────┬────────┘ └────────┬────────┘ └────────┬───────┘ │   │
│  └───────────┼───────────────────┼───────────────────┼─────────┘   │
│              │                   │                   │             │
│              ▼                   ▼                   ▼             │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                    Sui Blockchain Layer                     │   │
│  │  ┌────────────────────────┐     ┌────────────────────────┐  │   │
│  │  │ Smart Contracts (move) │     │ Core DeFi Ecosystem    │  │   │
│  │  │ • agent.move (Vaults)  │◄───►│ • DeepBook (CLOB DEX)  │  │   │
│  │  │ • policy_guard.move    │     │ • Cetus / Scallop Pools│  │   │
│  │  │ • registry.move        │     │                        │  │   │
│  │  └────────┬───────────────┘     └────────────────────────┘  │   │
│              │                                                     │
│              ▼ (Immutable Log Streams)                             │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │                 Decentralized Audit Storage                 │   │
│  │  • Walrus Storage System (Cryptographic inference tracking) │   │
│  └─────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
```

### Core Components

* **Web Dashboard (Next.js/TypeScript)** - Elegant web client featuring an intuitive AI chat terminal for composing strategy intents, custom yield metric monitors, and native wallet tools.
* **AI Engine Backend (Python/FastAPI)** - Core brain compiling semantic user goals into optimized executable byte code, handling data pipelines, and managing machine enclaves.
* **Smart Contracts (Sui Move 2024)** - Immutable on-chain enforcement infrastructure maintaining state control, global protocol asset records, and run-time financial guardrails.
* **Walrus Data Node** - Secure decentralized streaming configuration mapping real-time operational decisions to public decentralization storage beds.

## 📁 Repository Structure
```
kinetix-monorepo/
├── move/                       # Sui Move Smart Contracts (Move 2024)
│   ├── sources/
│   │   ├── agent.move         # Defines the core autonomous 'Agent' object vault
│   │   ├── policy_guard.move  # Rule-engine restricting transaction bounds (Slippage, caps)
│   │   └── registry.move      # Protocol global state tracking registered objects
│   ├── tests/
│   │   └── agent_tests.move   # Local testing suite using sui::test_scenario
│   ├── Move.toml              # Manifest defining package and dependencies
│   └── Move.lock              # Pin file for dependencies
│
├── backend-ai/                  # Off-Chain AI Intent Engine (Python)
│   ├── src/
│   │   ├── interpreter.py     # Parses user natural language into target structured JSON
│   │   ├── ptb_builder.py     # Constructs raw binary Programmable Transaction Blocks
│   │   ├── secure_signer.py   # TEE integration logic interacting with ephemeral keys
│   │   └── walrus_logger.py   # Custom worker streaming audit inferences to Walrus
│   ├── main.py                # FastAPI server entry point
│   ├── requirements.txt       # Engine dependencies (pysui, langchain, fastapi)
│   └── .env.example           # RPC Endpoints, Enclave configurations, and AI keys
│
├── frontend-web/                # Client Dashboard Interface (Next.js)
│   ├── src/
│   │   ├── app/
│   │   │   ├── page.tsx       # Main Landing / Dashboard Overview
│   │   │   └── agents/        # Strategy Creation & Active Bot Monitoring UI
│   │   ├── components/
│   │   │   ├── WalletConnect.tsx    # Wrapper configuration for @mysten/dapp-kit
│   │   │   ├── StrategyTerminal.tsx # Conversational strategy chat interface
│   │   │   └── AgentCard.tsx        # Dynamic on-chain visual object renderer
│   │   ├── hooks/
│   │   │   └── useKinetix.ts        # Custom React hooks parsing chain events
│   │   └── utils/
│   │       └── suiClient.ts         # Initialized SuiClient instance
│   ├── package.json               # Next.js configurations
│   └── tailwind.config.js         # Responsive design stylings
│
├── docker-compose.yml           # Local execution setups (Redis tracking, local testnets)
├── package.json                 # Core workspace configuration entries
└── README.md                    # This file
```

## 🚀 Quick Start

### Prerequisites
* **Sui CLI** (For contract building and local testing environments)
* **Node.js 18+** with npm or yarn
* **Python 3.10+**
* **Docker & Docker Compose** (Optional, for Redis operational state tracking)

### One-Line Setup (macOS/Linux)
```bash
# Clone your fork of the project
git clone [https://github.com/<Your_Profile>/kinetix.git](https://github.com/<Your_Profile>/kinetix.git)
cd kinetix

# Launch local supporting databases
docker-compose up -d

# Initialize and run the Python AI Engine
cd backend-ai
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
python main.py

# In a new terminal - Build and test Move smart contracts
cd ../move
sui move build
sui move test

# In a new terminal - Launch the web dashboard interface
cd ../frontend-web
npm install
npm run dev
```

### Windows Setup

```bash
# Setup AI backend
cd backend-ai
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
copy .env.example .env
python main.py

# New terminal - Launch client app
cd ..\frontend-web
npm install
npm run dev
```

### 📱 Web Dashboard (frontend-web)

The React web client provides deep portfolio control windows alongside real-time strategy creation boards.

**Key Features**

- **Full @mysten/dapp-kit Assembly** — Smooth integration allowing immediate desktop connections alongside native zkLogin wrappers.

- **Dynamic Object Parsing** — Bypasses central API mapping directly to individual on-chain Object tracking configurations.

- **Conversational Strategy Inputs** — Simple natural language input processing panels handling live feedback streaming.

---

### 🔧 AI Backend Core (backend-ai)

High-performance processing middleware engine mapping structural abstract user actions into raw target blockchain payloads.

**Intent Processing Flow**

```
[Natural Language Input] ──➔ (LangChain Parser) ──➔ [JSON Strategy Parameters]
                                                          │
                                                          ▼
[Signed Transaction] ◄── (TEE Session Keys) ◄── (PTB Builder Mapping Engine)
```

### Key API Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/api/v1/agents/parse` | Compiles raw user text inputs into structural state parameters | JWT |
| POST | `/api/v1/execution/build-ptb` | Combines parameters into valid structural execution blocks | API-Key |
| GET | `/api/v1/analytics/logs/:id` | Queries historic cryptographic records from Walrus storage node | Public |

---

### 🔒 Security & Guardrails

**On-Chain Move Invariants**

- **Hot Potato Receipts** — Flash loans implement structural rules missing native capability definitions (drop, store), forcing exact atomic repayment steps before execution closure.

- **Policy Guard Assertions** — Rigid hardcoded max-slippage limitations and daily volumetric output barriers run natively within contract blocks to check validity before transaction finality.

**Operational Infrastructure**

- **Enclave Processing Barriers** — Signer services operate purely inside hardware-isolated structures preventing raw root phrase visibility across multi-party execution pipelines.

- **Auditable Operations Ledger** — Complete performance traces exist outside database tables, using cryptographic commitments mapping records permanently into Walrus nodes.

---

### 🤝 Contributing

1. Fork the repository
2. Create a specific feature branch (`git checkout -b feature/amazing-agent`)
3. Commit code changes following semantic tracking norms (`git commit -m 'feat: add deepbook routing agent'`)
4. Push updates to your active branch (`git push origin feature/amazing-agent`)
5. Open a comprehensive Pull Request

---

### 📞 Contact & Support

- **Discord:** Oluwaseyi89
- **Twitter:** @IsenewoE
- **Email:** isenewoephr2012@gmail.com
- **GitHub Issues:** Report bugs directly to our monorepo hub

---

Built with ❤️ for the Sui and AI Agentic ecosystems.