# SUBTC-CLI-V1.0.0-Bitcoin-Testnet
SUBTC CLI V1.0.0 — Bitcoin Testnet

Gateway V4.2 · Stateless · Idempotent · curl-first
Usage:
  subtc <command> [args]
Key:
  subtc key create                         Create & save API key
  subtc key status                         Verify current key
Wallet:
  subtc wallet create                      Create testnet wallet
  subtc wallet list                        List all wallets
  subtc wallet receive  <wid>              Generate receive address
  subtc wallet balance  <wid>              Show balance (SAT + BTC)
Send:
  subtc send <wid> <addr> <sat> [idem]     Idempotent send (min 50,000 sat)
Inbox:
  subtc inbox <wid> <expected_sat>         Pre-configured receive inbox
Wait / Poll:
  subtc wait <wid> <addr> <sat> [timeout_sec] [callback_url]
                                           Long-poll or webhook on payment
  subtc poll <wid> <addr> <sat>            Single poll check
  subtc poll <wid> <addr> <sat> --loop     Loop poll until confirmed
Config:
  subtc config show                        Show stored config
  subtc config set-key <key>               Store API key
  subtc health                             Node health check
Examples:
  subtc key create
  subtc wallet create
  subtc wallet receive  wlt_abc123
  subtc wallet balance  wlt_abc123
  subtc send  wlt_abc123  tb1qXXX  50000
  subtc wait  wlt_abc123  tb1qXXX  20000  300
  subtc poll  wlt_abc123  tb1qXXX  20000  --loop
Units:  1 BTC = 100,000,000 SAT · Fee: 3% · Min send: 50,000 SAT
Docs:   https://subtc.net/api

# TEST ON LINUX 
install tools 🔥 
go build -o subtc subtc-cli.go

root@subtc:~/subtc# ./subtc key create
Key Created
────────────────────────────────────────────
key:                 SUBTC-KEY-3f470eb8d4d0499c12178d5c8c348a66c0c33d7ec941cdd7
✓ Key saved → ~/.subtc.json
root@subtc:~/subtc# ./subtc wallet create
Wallet Created · testnet
────────────────────────────────────────────
wallet_id:           w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758
{
  "ok": true,
  "request_id": "66d6705f7e7a1c82",
  "result": {
    "coin": "btc",
    "net": "test",
    "wallet_id": "w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758"
  }
}
root@subtc:~/subtc# ./subtc wallet receive
✗ usage: subtc wallet receive <wallet_id>
root@subtc:~/subtc# ./subtc wallet receive w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758
Receive Address
────────────────────────────────────────────
address:             tb1qwphc20fty0l42cn3tnwv32uz85zm9jm2thdl4y
{
  "ok": true,
  "request_id": "98683c2957cadb69",
  "result": {
    "address": "tb1qwphc20fty0l42cn3tnwv32uz85zm9jm2thdl4y",
    "addresses": [
      "tb1qwphc20fty0l42cn3tnwv32uz85zm9jm2thdl4y"
    ],
    "coin": "btc",
    "net": "test",
    "wallet_id": "w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758"
  }
}
root@subtc:~/subtc# ./subtc wallet balance w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758
Balance · w_ce9e16e59a…
────────────────────────────────────────────
balance:             48500 sat  (0.00048500 BTC)
unconfirmed:         0 sat  (0.00000000 BTC)
{
  "ok": true,
  "request_id": "3843d95815b06e0a",
  "result": {
    "addresses": [
      "tb1qwphc20fty0l42cn3tnwv32uz85zm9jm2thdl4y"
    ],
    "balance_sat": 48500,
    "balance_source": "getbalances",
    "coin": "btc",
    "confirmed_sat": 48500,
    "immature_sat": 0,
    "net": "test",
    "unconfirmed_sat": 0,
    "wallet_id": "w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758"
  }
}
root@subtc:~/subtc# ./subtc send w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758 tb1qjcr7lcucmwudwqscew4r078gxkw549ruq5r97w 30000
✗ minimum send is 50000 sat (got 30000)
root@subtc:~/subtc# ./subtc send w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758 tb1qjcr7lcucmwudwqscew4r078gxkw549ruq5r97w 50000
Send BTC · testnet
────────────────────────────────────────────
wallet_id:           w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758
to:                  tb1qjcr7lcucmwudwqscew4r078gxkw549ruq5r97w
amount:              50000 sat  (0.00050000 BTC)
idempotency:         send-1773768995
{
  "detail": {
    "hint": "rpc error"
  },
  "error": "SEND_FAILED",
  "ok": false
}
root@subtc:~/subtc# ./subtc wallet balance w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758
Balance · w_ce9e16e59a…
────────────────────────────────────────────
balance:             97000 sat  (0.00097000 BTC)
unconfirmed:         0 sat  (0.00000000 BTC)
{
  "ok": true,
  "request_id": "52180cb3b9d20395",
  "result": {
    "addresses": [
      "tb1qwphc20fty0l42cn3tnwv32uz85zm9jm2thdl4y"
    ],
    "balance_sat": 97000,
    "balance_source": "getbalances",
    "coin": "btc",
    "confirmed_sat": 97000,
    "immature_sat": 0,
    "net": "test",
    "unconfirmed_sat": 0,
    "wallet_id": "w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758"
  }
}
root@subtc:~/subtc# ./subtc send w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758 tb1qjcr7lcucmwudwqscew4r078gxkw549ruq5r97w 50000
Send BTC · testnet
────────────────────────────────────────────
wallet_id:           w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758
to:                  tb1qjcr7lcucmwudwqscew4r078gxkw549ruq5r97w
amount:              50000 sat  (0.00050000 BTC)
idempotency:         send-1773769023
✓ Transaction broadcast
txid:                3d72d72aa9f43be50e4dfb35971107252143fdf3da859d97d74427336b5ef8fd
{
  "ok": true,
  "request_id": "359a5d64c67a4ee3",
  "result": {
    "coin": "btc",
    "fee_addr": "tb1q2dn34v7l3jmn30zuwgkzry23td949qtrre46cw",
    "fee_bps": 300,
    "net": "test",
    "network_fee_by": "service_fee",
    "requested_sat": 50000,
    "send_method": "sendmany",
    "sent_sat": 48500,
    "service_fee_sat": 1500,
    "txid": "3d72d72aa9f43be50e4dfb35971107252143fdf3da859d97d74427336b5ef8fd",
    "wallet_id": "w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758"
  }
}
root@subtc:~/subtc# ./subtc wait w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758 tb1qwphc20fty0l42cn3tnwv32uz85zm9jm2thdl4y 20000
Waiting for Funds
────────────────────────────────────────────
wallet_id:           w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758
address:             tb1qwphc20fty0l42cn3tnwv32uz85zm9jm2thdl4y
expected_sat:        20000 sat  (0.00020000 BTC)
timeout:             300 sec
mode:                long-poll (blocking…)
received:            97000 sat  (0.00097000 BTC)
{
  "ok": true,
  "request_id": "ae34e901e5ca030f",
  "result": {
    "address": "tb1qwphc20fty0l42cn3tnwv32uz85zm9jm2thdl4y",
    "coin": "btc",
    "expected_sat": 20000,
    "net": "test",
    "received_sat": 97000,
    "status": "confirmed",
    "wallet_id": "w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758"
  }
}
root@subtc:~/subtc# ./subtc poll w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758 tb1qwphc20fty0l42cn3tnwv32uz85zm9jm2thdl4y 20000 --loop
Poll
────────────────────────────────────────────
wallet_id:           w_ce9e16e59a72cd59840ce2256662a2400bc114ea3758
address:             tb1qwphc20fty0l42cn3tnwv32uz85zm9jm2thdl4y
expected_sat:        20000 sat  (0.00020000 BTC)
mode:                loop every 3 sec — Ctrl+C to stop
✅   received: 97000 sat  (0.00097000 BTC) reached: true
