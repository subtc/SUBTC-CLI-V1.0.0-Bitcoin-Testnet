title: SUBTC-CLI V1.0.0 — Bitcoin Testnet
Date: 2026-03-17

# SUBTC-CLI V1.0.0 — Bitcoin Testnet

[![Version](https://img.shields.io/badge/version-1.0.0-blue)](https://subtc.net/api)
[![Go](https://img.shields.io/badge/go-1.20-green)](https://golang.org/)
[![License](https://img.shields.io/badge/license-Apache_2.0-yellow)](https://www.apache.org/licenses/LICENSE-2.0)

Gateway V4.2 · Stateless · Idempotent · curl-first

---

## ⚡ Usage
subtc <command> [args]

---

## 🔑 Key Management
subtc key create           # Create & save API key
subtc key status           # Verify current key

---

## 💼 Wallet Management
subtc wallet create            # Create testnet wallet
subtc wallet list              # List all wallets
subtc wallet receive <wid>     # Generate receive address
subtc wallet balance <wid>     # Show balance (SAT + BTC)

---

## 📤 Send BTC
subtc send <wid> <addr> <sat> [idem]    # Idempotent send (min 50,000 sat)

---

## 📥 Inbox / Receive
subtc inbox <wid> <expected_sat>         # Pre-configured receive inbox

---

## ⏱ Wait / Poll
subtc wait <wid> <addr> <sat> [timeout_sec] [callback_url]   # Long-poll or webhook on payment
subtc poll <wid> <addr> <sat>                                # Single poll check
subtc poll <wid> <addr> <sat> --loop                          # Loop poll until confirmed

---

## ⚙️ Config
subtc config show               # Show stored config
subtc config set-key <key>      # Store API key
subtc health                    # Node health check

---

## 📝 Examples
subtc key create
subtc wallet create
subtc wallet receive wlt_abc123
subtc wallet balance wlt_abc123
subtc send wlt_abc123 tb1qXXX 50000
subtc wait wlt_abc123 tb1qXXX 20000 300
subtc poll wlt_abc123 tb1qXXX 20000 --loop

---

## 📌 Units & Fees
1 BTC = 100,000,000 SAT  
Fee: 3%  
Minimum send: 50,000 SAT  

---

## 🌐 Documentation
https://subtc.net/api

---

## 🖥 Test on Linux
Install tools and build CLI:

go build -o subtc subtc-cli.go

Example run:

root@subtc:~/subtc# ./subtc key create
Key Created
────────────────────────────────────────────
key: SUBTC-KEY-3f470eb8d4d0499c12178d5c8c348a66c0c33d7ec941cdd7
✓ Key saved → ~/.subtc.json

root@subtc:~/subtc# ./subtc wallet create
Wallet Created · testnet
