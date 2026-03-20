# 🏛️ Governance Token Platform — Fullstack

A fullstack decentralized governance application built on **Stellar (Soroban)** with a **React** frontend. Token holders can create proposals, vote, and manage governance — all on-chain.

---
## Contract link: https://stellar.expert/explorer/testnet/contract/CAYQ5STCWDCIJAE2H5FW4B3W7LVRW3ZJZ5KQEDGAR7KPBRDY4UKLXIQF
<img width="1919" height="865" alt="Screenshot 2026-03-20 140854" src="https://github.com/user-attachments/assets/eb430347-d37a-4bac-8196-8f1b80c52034" />


<img width="1917" height="856" alt="Screenshot 2026-03-20 143435" src="https://github.com/user-attachments/assets/79ff3c14-39f2-404e-91a8-2ca913aa238e" />

## 🗂️ Project Structure

```
GovernanceTokenPlatform/
│
├── contracts/                  # Soroban Smart Contract (Rust)
│   └── governance/
│       ├── Cargo.toml
│       └── src/
│           └── lib.rs
│
├── frontend/                   # React Frontend
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.jsx
│   │   │   ├── ProposalCard.jsx
│   │   │   ├── CreateProposal.jsx
│   │   │   └── VoteModal.jsx
│   │   ├── pages/
│   │   │   ├── Home.jsx
│   │   │   ├── Proposals.jsx
│   │   │   └── Dashboard.jsx
│   │   ├── utils/
│   │   │   └── stellar.js      # Stellar SDK helpers
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── package.json
│   └── .env
│
└── README.md
```

---

## ⚙️ What It Does

| Layer | Tech | Role |
|---|---|---|
| Smart Contract | Rust + Soroban | Token management, proposals, voting |
| Blockchain | Stellar Testnet | Stores all on-chain state |
| Frontend | React + Vite | UI for interacting with the contract |
| Wallet | Freighter | Signs and submits transactions |

**User flow:**
1. Connect Freighter wallet
2. View token balance and active proposals
3. Create a new proposal (title + description)
4. Vote For / Against on any open proposal
5. See live vote counts update on-chain

---

## ✨ Features

- 🔗 **Freighter wallet integration** — connect, sign, submit
- 🪙 **Token balance display** — see your governance tokens
- 📜 **Proposal list** — all proposals fetched live from the contract
- 🗳️ **One-click voting** — For / Against with double-vote protection
- ➕ **Create proposals** — any token holder can submit
- 📊 **Vote tallies** — live vote counts per proposal
- 🌐 **Testnet ready** — deploys to Stellar Testnet out of the box

---

## 🚀 Getting Started

### Prerequisites

```bash
# Rust + WASM target
rustup target add wasm32-unknown-unknown

# Stellar CLI
cargo install --locked stellar-cli --features opt

# Node.js (v18+)
node --version
```

### 1 — Clone the repo

```bash
git clone https://github.com/your-username/GovernanceTokenPlatform.git
cd GovernanceTokenPlatform
```

### 2 — Build & deploy the contract

```bash
# Build
stellar contract build

# Deploy to testnet
stellar contract deploy \
  --wasm target/wasm32-unknown-unknown/release/governance.wasm \
  --source deployer \
  --network testnet
```

Copy the returned contract ID — you'll need it next.

### 3 — Initialize the contract

```bash
stellar contract invoke \
  --id <CONTRACT_ID> \
  --source deployer \
  --network testnet \
  -- init \
  --admin <YOUR_ADDRESS> \
  --supply 1000000
```

### 4 — Set up the frontend

```bash
cd frontend
npm install
```

Create a `.env` file:

```env
VITE_CONTRACT_ID=<YOUR_CONTRACT_ID>
VITE_NETWORK=TESTNET
VITE_HORIZON_URL=https://horizon-testnet.stellar.org
VITE_RPC_URL=https://soroban-testnet.stellar.org
```

### 5 — Run the frontend

```bash
npm run dev
```

Open [http://localhost:5173](http://localhost:5173)

---

## 🔌 Freighter Wallet Setup

1. Install the [Freighter browser extension](https://freighter.app)
2. Create or import a wallet
3. Switch network to **Testnet**
4. Fund your address via [Stellar Friendbot](https://friendbot.stellar.org)

---

## 📡 Smart Contract Functions

| Function | Description |
|---|---|
| `init(admin, supply)` | Initialize contract and mint tokens |
| `transfer(from, to, amount)` | Transfer tokens |
| `propose(proposer, title)` | Create a new proposal |
| `vote(voter, proposal_id)` | Vote on a proposal |
| `balance(account)` | Get token balance |
| `get_proposal(id)` | Fetch proposal data |

---

## 🔗 Deployed Contract

| Network | Contract ID |
|---|---|
| Stellar Testnet | `CDDXARJ6RXV7MLE3SVLXWEGB56CWLZPZB5PGQ4GBWBVCVRMVZ6QTTB` |
| Stellar Mainnet | Coming soon |

🔍 View on explorer: [stellar.expert/explorer/testnet](https://stellar.expert/explorer/testnet/contract/CDDXARJ6RXV7MLE3SVLXWEGB56CWLZPZB5PGQ4GBWBVCVRMVZ6QTTB)

---

## 🧪 Running Tests

```bash
# Contract tests
cargo test

# Frontend tests
cd frontend && npm run test
```

---

## 🛠️ Tech Stack

- **Soroban SDK** `v21` — smart contract framework
- **React** `v18` + **Vite** — frontend
- **Stellar SDK** (`@stellar/stellar-sdk`) — blockchain interaction
- **Freighter API** (`@stellar/freighter-api`) — wallet connection
- **Tailwind CSS** — styling

---

## 📄 License

MIT
