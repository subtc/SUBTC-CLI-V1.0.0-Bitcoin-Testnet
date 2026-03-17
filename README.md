title: SUBTC-CLI V1.0.0 — Bitcoin Testnet
Date: 2026-03-17

# SUBTC-CLI V1.0.0 — Bitcoin Testnet

SUBTC CLI V1.0.0 is a lightweight, stateless, curl-first command-line tool for interacting with the Bitcoin Testnet via SUBTC Gateway V4.2.  
It is idempotent, easy to use, and designed for developers and testers.

---

## Features
- Create and manage API keys
- Create and manage testnet wallets
- Generate receive addresses
- Check wallet balances (SAT + BTC)
- Send testnet BTC with idempotency
- Long-poll, webhook, or loop for incoming payments
- Config management and health checks

---

## Quick Start
Download and build the CLI from the official post:

https://subtc.net/post/subtc-cli-v1-0-0-bitcoin-testnet

Build and run:
go build -o subtc subtc-cli.go

Example commands:
./subtc key create
./subtc wallet create
./subtc wallet receive <wid>
./subtc wallet balance <wid>
./subtc send <wid> tb1qXXX 50000
./subtc wait <wid> tb1qXXX 20000
./subtc poll <wid> tb1qXXX 20000 --loop

---

## Commands Overview

### Key Management
./subtc key create           # Create & save API key
./subtc key status           # Verify current key

### Wallet Management
./subtc wallet create            # Create testnet wallet
./subtc wallet list              # List all wallets
./subtc wallet receive <wid>     # Generate receive address
./subtc wallet balance <wid>     # Show balance

### Send BTC
./subtc send <wid> <addr> <sat> [idem]    # Idempotent send (min 50,000 SAT)

### Inbox / Receive
./subtc inbox <wid> <expected_sat>         # Pre-configured receive inbox

### Wait / Poll
./subtc wait <wid> <addr> <sat> [timeout_sec] [callback_url]   # Long-poll or webhook on payment
./subtc poll <wid> <addr> <sat>                                # Single poll check
./subtc poll <wid> <addr> <sat> --loop                          # Loop poll until confirmed

### Config & Health
./subtc config show
./subtc config set-key <key>
./subtc health

---

## Units & Fees
1 BTC = 100,000,000 SAT  
Fee: 3%  
Minimum send: 50,000 SAT  

---

## Documentation
https://subtc.net/api

---

## Example Run
root@subtc:~/subtc# ./subtc key create
Key Created
key: SUBTC-KEY-3f470eb8d4d0499c12178d5c8c348a66c0c33d7ec941cdd7
✓ Key saved → ~/.subtc.json

root@subtc:~/subtc# ./subtc wallet create
Wallet Created · testnet

---

License: Apache 2.0
