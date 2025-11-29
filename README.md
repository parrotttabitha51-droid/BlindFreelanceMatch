# 🤝 BlindFreelanceMatch — Encrypted, Trustless Freelance Matching on FHEVM

**BlindFreelanceMatch** is a fully private freelance–client matchmaking system built on **Zama’s FHEVM**.
Freelancers and job creators submit **encrypted skillsets, experience levels, and rates/budgets**, and the contract performs a compatibility check **directly on encrypted data**.
No one — not even blockchain validators — can see profile information or preferences.

This project demonstrates how **end-to-end encrypted marketplaces** can run entirely on-chain without revealing sensitive details about users, skills, or salaries.

---

## ✨ Key Capabilities

* 🔐 **Confidential Profiles** — all attributes remain encrypted (skills, experience, budgets).
* 🧠 **Homomorphic Matching** — the smart contract checks skill overlap, level, and affordability using FHE.
* 🧩 **Bitmask Skill Matching** — matching based on encrypted bitwise skill vectors.
* 💸 **Budget-Safe Logic** — compares freelancer rates against client budgets without exposing numbers.
* 🛡 **Granular Access Control** via FHEVM ACL.
* 🔓 **Private or Public Decryption** based on user intent.
* 🌐 **Simple Frontend** using Zama Relayer SDK v0.3.0.

---

## 🏗 Tech Stack

| Layer                | Tools                 |
| -------------------- | --------------------- |
| Confidential Compute | Zama FHEVM            |
| Solidity Library     | `@fhevm/solidity`     |
| Encryption Flow      | Relayer SDK v0.3.0    |
| UI                   | Vanilla JS, HTML, CSS |
| Blockchain           | Sepolia FHEVM Testnet |
| Dev Tools            | Hardhat, Ethers.js v6 |

---

## 📦 Repository Layout

```
BlindFreelanceMatch/
├── contracts/
│   └── BlindFreelanceMatch.sol
├── deploy/
├── frontend/
│   └── index.html
├── hardhat.config.js
└── package.json
```

---

# 🔐 Smart Contract Summary

BlindFreelanceMatch stores two encrypted entities:

### Freelancers

* `skillsMask: euint256`
* `level: euint8`
* `rate: euint16`

### Jobs

* `requiredSkillsMask: euint256`
* `minLevel: euint8`
* `maxBudget: euint16`

### Matching Criteria (FHE-computed)

```
skillsOverlap   = freelancer.skillsMask AND job.skillsMask
hasSkills       = (skillsOverlap != 0)
levelSatisfied  = freelancer.level >= job.minLevel
withinBudget    = freelancer.rate <= job.maxBudget

match = hasSkills AND levelSatisfied AND withinBudget
```

The final encrypted result is stored as **euint8 (0 or 1)** and accessible only to authorized parties.

---

## 🚀 Getting Started

### Install

```bash
git clone https://github.com/parrotttabitha51-droid/BlindFreelanceMatch
cd BlindFreelanceMatch
npm install
```

### Environment Setup

```bash
npx hardhat vars set MNEMONIC
npx hardhat vars set INFURA_API_KEY
npx hardhat vars set ETHERSCAN_API_KEY
```

### Compile & Test

```bash
npm run compile
npm run test
```

---

## 🌐 Deployment

### Local FHEVM Node

```bash
npx hardhat node
npx hardhat deploy --network localhost
```

### Sepolia FHEVM

```bash
npx hardhat deploy --network sepolia
npx hardhat verify --network sepolia
```

Add your deployment address here after publishing.

---

# 🖥 Frontend Encryption Flow

Frontend uses:

* `@zama-fhe/relayer-sdk`
* `ethers.js v6`

Flow:

1. Connect wallet
2. Encrypt freelancer/job attributes
3. Submit encrypted profiles
4. Trigger encrypted matching
5. Decrypt privately or make result public

Supports:
✔ `createEncryptedInput`
✔ `userDecrypt`
✔ `publicDecrypt`

---

## 📚 Useful Links

* Zama FHEVM Docs — [https://docs.zama.ai/protocol](https://docs.zama.ai/protocol)
* Relayer SDK — [https://docs.zama.ai/protocol/relayer-sdk-guides/](https://docs.zama.ai/protocol/relayer-sdk-guides/)
* FHEVM Solidity Library — [https://github.com/zama-ai/fhevm-solidity](https://github.com/zama-ai/fhevm-solidity)
* Ethers v6 — [https://docs.ethers.org/v6/](https://docs.ethers.org/v6/)

---

## 🆘 Support

* GitHub Issues
* Zama Discord: [https://discord.gg/zama-ai](https://discord.gg/zama-ai)

---

## 📄 License

**BSD-3-Clause-Clear**
