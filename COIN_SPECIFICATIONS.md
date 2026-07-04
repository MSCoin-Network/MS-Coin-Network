# 📊 MS COIN // CORE SPECIFICATIONS & TOKENOMICS

The MS Coin economy is mathematically secured by a dynamic emission schedule, ensuring long-term node profitability while preventing hyperinflation. The architecture combines a hard-capped primary emission with a highly controlled Tail Emission protocol.

---

## 🪙 1. Asset Specifications

* **Asset Name:** MS Coin
* **Ticker:** MSC
* **Network:** MS Coin Network (Layer-1 Native)
* **Consensus Mechanism:** Hybrid Master-Node Validation / Ghost Worker Hashcash
* **Cryptography:** Ed25519 (Signatures), RSA (Stealth Routing), ChaCha20-Poly1305 (Payloads)
* **Smallest Unit:** Mwei (1 MSC = 10,000 Mwei)

---

## 📈 2. Emission Schedule & Halving

The network utilizes a highly deflationary base-reward system that dynamically halves based on block height, mirroring the digital scarcity of traditional store-of-value assets.

* **Genesis Block Reward:** 50 MSC
* **Halving Interval:** Every 100,000 Blocks
* **Halving Mechanism:** The base mining reward is bit-shifted (`>> 1`) per interval.

### Tail Emission (Long-Term Security)
To guarantee network security and node profitability after primary halvings are exhausted, the network enforces a strict **Tail Emission**.
* **Minimum Block Reward:** 1 MSC (10,000 Mwei)
* *Note: The reward will never drop below 1 MSC per block, ensuring Ghost Workers and nodes are perpetually incentivized to process stealth payloads.*

---

## 🏦 3. Treasury & Genesis Architecture

To fund the ecosystem, secure initial exchange liquidity, and power the upcoming Airdrop/Presale distribution, a Genesis Treasury architecture is implemented.

* **Genesis Burn Address:** `00000000000000000000000000000000`
* **Treasury Split:** A dynamically calculated fraction of the block reward is allocated to the Master Treasury during the early network phases to build supply for cross-chain liquidity bridging (e.g., USDT pairs).
* **Worker Split:** External "Ghost Workers" contributing CPU cycles to validate Mempool transactions receive an exact cut defined by the current network difficulty and reward epoch.

---

## 🛡️ 4. Network Difficulty & Validation

Difficulty is dynamically adjusted based on network load and pending mempool transactions to prevent rapid block generation attacks (Spam-Shield).

* **Target Hash:** SHA-256 (Leading Zeros Requirement)
* **Block Time:** Dynamic (Triggered strictly by mempool activity / Stealth Message volume)
* **Empty Block Prevention:** The network idles (`status: waiting`) when the mempool is empty, conserving global energy until an encrypted payload requires routing.
