# User flow

The Enygma demo flow as observed on 13 November 2026. Steps marked "done" were completed in the test session. Steps marked "not done" were seen but not completed.

## Sign-up

```
open demo
  -> pick username (@kittyrim, available instantly)     [done]
  -> create passkey (Google Password Manager)           [done]
  -> create recovery PIN (required right after passkey) [done]
  -> wallet created
```

## Public faucet

```
wallet screen -> Faucet (public)
  -> one click, no passkey                             [done]
  -> received 5 $USD and 50 $RLS
```

## Register keys

```
wallet screen -> register your keys
  -> passkey created
  -> get test funds
  -> register your keys
  -> encrypt your view key for the auditor ("Quantum-private")
  -> check the fees (shown about 8.004 RLS)
  -> approve with passkey and sign
  -> confirm onchain
  -> fee confirmed 7.1932 RLS, balance after 42.8067 RLS   [done]
```

## Shield

```
wallet screen -> Shield
  -> confirm with passkey
  -> encrypt note and sign the $RLS transfer ("Quantum-private")
  -> check the fees (shown about 4.14 RLS)
  -> approve with passkey and sign
  -> confirm onchain (about 15 seconds, spinner only)
  -> fee confirmed 3.5814 RLS, shielded 21.4 RLS,
     balance after 17.8252 RLS                          [done]
```

## Shielded faucet

```
wallet screen -> Faucet (shielded)
  -> one click, no passkey                             [done]
  -> received 50 RLS and 5 $USD into the shielded balance (RECONSTRUCTION — amounts inferred from the final wallet balance; no dedicated screenshot; see demo-testing/test-report.md, section 6)
```

## Send

```
wallet screen -> Send
  -> choose Shielded or Public
  -> choose token ($RLS)
  -> enter recipient (@username or 0x...)
  -> list of registered users shown (48)
  -> [not done] no send was completed
```

## Invite

```
wallet screen -> Invite button visible
  -> [not done] invite screen not opened, flow not tried
```

## Wallet screen

The wallet screen shows: total value ($10.15 at the end of the test run), EVM address (truncated), Enygma Spend address (truncated), Enygma View address (truncated), four actions (Send, Receive, Faucet, Invite), three tabs (Assets, Invites, Activity), and a per-asset table with Total / Public / Shielded columns.
