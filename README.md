
# STX-FundForge - Community Startup Funding DAO

A Clarity smart contract for decentralized community funding pools where users can contribute STX, propose startups to fund, vote on proposals, and distribute funds based on collective decisions.

---

## 📜 Contract Overview

This contract allows STX holders to:

1. **Create and manage funding pools**.
2. **Contribute to active pools**.
3. **Submit funding proposals for startups**.
4. **Vote on proposals using contribution-weighted votes**.
5. **Execute successful proposals after a voting period**.

---

## 📦 Features

* ✅ **Create Pools**: Any user can initialize a new funding pool.
* 💸 **Contribute STX**: Users contribute at least `u1000000` microSTX to a pool.
* 📝 **Submit Proposals**: Anyone can submit a proposal once the pool has reached the `u100000000` threshold.
* 🗳 **Vote on Proposals**: Contributors vote using their contribution amount as voting power.
* ⏱ **Time-Bound Voting**: Voting is open for approximately 24 hours (`u144` blocks).
* 🔐 **Execution Logic**: After the voting period, proposals are executed or rejected based on vote majority.
* ⚖ **DAO Governance**: Transparent, rule-based, and democratic.

---

## 🔧 Constants

| Constant             | Value        | Description                                |
| -------------------- | ------------ | ------------------------------------------ |
| `CONTRACT_OWNER`     | `tx-sender`  | Address that deploys the contract          |
| `MIN_CONTRIBUTION`   | `u1000000`   | Minimum contribution (1 STX)               |
| `VOTING_PERIOD`      | `u144`       | Voting duration (\~24 hours)               |
| `PROPOSAL_THRESHOLD` | `u100000000` | Minimum pool size for proposal eligibility |

---

## ⚠ Error Codes

| Error Code               | Code         | Description                             |
| ------------------------ | ------------ | --------------------------------------- |
| `ERR_NOT_AUTHORIZED`     | `(err u100)` | User is not authorized                  |
| `ERR_INSUFFICIENT_FUNDS` | `(err u101)` | Pool does not have enough funds         |
| `ERR_POOL_NOT_FOUND`     | `(err u102)` | Pool does not exist or is inactive      |
| `ERR_INVALID_AMOUNT`     | `(err u103)` | Contribution amount is too low          |
| `ERR_ALREADY_VOTED`      | `(err u104)` | User has already voted                  |
| `ERR_VOTING_CLOSED`      | `(err u105)` | Voting is closed or not started         |
| `ERR_BELOW_THRESHOLD`    | `(err u106)` | Pool has not reached proposal threshold |

---

## 🗂️ Data Structures

### 🏊 `pools`

Each pool contains:

* `total-funds`: Total contributed
* `active`: Is the pool still open?
* `creator`: Pool creator
* `created-at`: Block height when created

### 👥 `contributions`

Tracks user contributions per pool.

### 🧾 `proposals`

Each proposal contains:

* `startup`: Target principal
* `amount`: Requested amount
* `description`: Purpose
* `votes-for`: Weighted votes in favor
* `votes-against`: Weighted votes against
* `status`: `"active"`, `"executed"`, or `"rejected"`
* `created-at`: Block height of creation

### ✅ `votes`

Tracks individual votes per user/proposal.

---

## 📘 Public Functions

### 🔹 `create-pool`

Creates a new funding pool.

### 🔹 `contribute (pool-id, amount)`

Contribute STX to a specific pool.

### 🔹 `submit-proposal (pool-id, startup, amount, description)`

Submit a proposal to fund a startup.

### 🔹 `vote (pool-id, proposal-id, vote-for)`

Vote on a proposal. Vote is weighted by user contribution.

### 🔹 `execute-proposal (pool-id, proposal-id)`

Executes proposal after the voting period. Transfers funds if passed.

---

## 📖 Read-Only Functions

* `get-pool`
* `get-contribution`
* `get-proposal`
* `get-vote`

Each of these returns respective data if available.

---

## 🛡 Security & Governance

* All fund transfers use `stx-transfer?` with strict error handling.
* Voting system prevents duplicate votes.
* Voting and proposal eligibility tied to contributions and time.
* Proposals can only be executed after voting closes and based on majority.

---

## 🧪 Example Usage (Pseudocode)

```clojure
;; Create a pool
(create-pool) ;; returns pool-id

;; Contribute
(contribute u1 u2000000) ;; contributes 2 STX to pool 1

;; Submit proposal after threshold reached
(submit-proposal u1 'SPXYZ... u50000000 "Seed funding for DeFi app")

;; Vote
(vote u1 u1 true) ;; vote in favor

;; Execute proposal after 24 hrs
(execute-proposal u1 u1)
```

---

## 🧾 License

MIT License. Free to use and modify.

---
