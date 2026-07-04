# 🔌 MS COIN NETWORK API Reference (v18.6)

The **MS Coin Network** provides a lightweight, high-performance REST API gateway. It allows exchanges, block explorers, wallets, and third-party applications to securely interact with the blockchain without exposing the underlying master node logic.

---

## 📋 Overview

- **Base URL:** `http://<NODE_IP>:8081`
- **Protocol:** HTTP/REST
- **Content-Type:** `application/json`

---

# API Endpoints

- [Network Synchronization](#-1-network-synchronization)
- [Wallet & Identity](#-2-wallet--identity)
- [Transactions & Economy](#-3-transactions--economy)

---

# 📡 1. Network Synchronization

## GET `/api/blocks`

Returns the latest confirmed blocks from the blockchain.

**Purpose**

- Block explorers
- Network synchronization
- Blockchain inspection

### Response

```json
[
  {
    "index": 1234,
    "timestamp": 1712345678,
    "previous_hash": "...",
    "hash": "...",
    "nonce": 48291,
    "transactions": [
      {
        "sender": "...",
        "receiver": "...",
        "amount": 100
      }
    ]
  }
]
```

---

## GET `/api/funding`

Returns the current verified funding collected through the Polygon USDT Oracle.

### Response

```json
{
  "collected": 12456.87
}
```

---

# 🔐 2. Wallet & Identity

## GET `/api/new_wallet`

Generates a brand-new offline wallet.

The following cryptographic components are created securely:

- BIP39 Seed Phrase
- Ed25519 Keypair
- RSA Keypair

### Response

```json
{
  "status": "ok",
  "seed_phrase": "word1 word2 word3 ...",
  "address": "<PUBLIC_KEY>",
  "private_key": "<HEX>",
  "rsa_public": "<RSA_HEX>"
}
```

---

## POST `/api/portfolio`

Returns the wallet balance and automatically consolidates hidden stealth payments (Auto Sweep).

### Request

```json
{
  "private_key": "<HEX>"
}
```

### Response

```json
{
  "balance": 15250,
  "address": "<PUBLIC_KEY>",
  "rsa_public_key": "<RSA_HEX>"
}
```

---

## POST `/api/recover`

Restores a wallet using its original seed phrase.

### Request

```json
{
  "seed_phrase": "word1 word2 word3 ..."
}
```

### Response

```json
{
  "status": "ok",
  "private_key": "<HEX>",
  "address": "<PUBLIC_KEY>"
}
```

---

# 💸 3. Transactions & Economy

## GET `/api/balance`

Returns the balance of the Foundation/Treasury wallet.

### Response

```json
{
  "status": "ok",
  "address": "<TREASURY_PUBLIC_KEY>",
  "balance": 9823456
}
```

---

## POST `/api/pay`

Creates an encrypted stealth payment.

The payment payload is encrypted using the recipient's RSA public key before it is written to the blockchain.

### Request

```json
{
  "sender_private_key": "<HEX>",
  "receiver_rsa_public": "<RSA_HEX>",
  "amount": 1000
}
```

### Response

```json
{
  "status": "success"
}
```

---

## POST `/api/buy_mscoin`

Creates a dynamic payment invoice for the Alpha Presale using the Polygon USDT Oracle.

### Request

```json
{
  "crypto_type": "USDT",
  "investor_address": "<MS_COIN_ADDRESS>",
  "amount_usd": 250.00
}
```

### Response

```json
{
  "status": "pending",
  "deposit_address": "<USDT_DEPOSIT_ADDRESS>",
  "required_amount": 250.00,
  "payment_reference": "<REFERENCE_ID>"
}
```

---

# ✅ HTTP Status Codes

| Code | Description |
|------|-------------|
| `200` | Request successful |
| `400` | Invalid request payload |
| `401` | Authentication failed |
| `404` | Resource not found |
| `500` | Internal server error |

---

# 🔒 Security Notes

- Private keys are **never stored** by the API.
- Wallet generation is performed completely offline.
- Payments are protected using **RSA encryption**.
- Wallet addresses use **Ed25519** cryptography.
- Seed phrases follow the **BIP39** standard.
- All sensitive operations should be performed over HTTPS in production.

---

# 📌 Version

**MS Coin Network API**  
**Version:** `18.6`
