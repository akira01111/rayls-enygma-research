# Enygma demo test report

Tester: one person, on a phone, demo username `@kittyrim`.
Date: 13 November 2026.
Demo: `enygma-testnet.rayls.com`, Rayls Public Chain testnet.
Method: each step done by hand, in order. Three screen recordings made. Five screenshots kept. Transcription of the three recordings returned no speech segments. The recordings are silent screen captures, not transcripts and not evidence of any conversation.

## Result summary

| Step | Result |
| --- | --- |
| Sign-up and passkey | Completed |
| Public faucet | Completed. 5 $USD, 50 $RLS |
| Register keys | Completed. Fee 7.1932 RLS |
| Shield 21.4 RLS | Completed. Fee 3.5814 RLS |
| Shielded faucet | RECONSTRUCTION. 50 RLS, 5 $USD (see section 6) |
| Shielded send | Not completed. Screen opened only |
| Invite | Not tried |

## Step by step

### 1. Sign-up and passkey

The username `@kittyrim` was available instantly. The passkey was created through Google Password Manager. A recovery PIN was required right after the passkey. That step was not expected.

The recovery PIN value is not recorded anywhere in this repository.

### 2. Public faucet

One click, no passkey. Received 5 $USD and 50 $RLS. Screenshot 1 (the register-keys screen, `1-fee-register.png`) shows this as a completed checklist item: "Get test $USD and $RLS — 5 $USD and 50 $RLS". The screenshot itself documents the register step. The faucet amounts appear in its checklist, not on a separate faucet screen.

### 3. Register keys

The fee shown on the previous screen was about 8.004 RLS. The confirmed fee was 7.1932 RLS: 6.255 gas plus 0.9382 Rayls Foundation commission (15%). Balance after: 42.8067 RLS. Wallet value shown at that point: $5.07.

The register flow steps, as shown in screenshot 1:

1. Passkey created
2. Get test $USD and $RLS
3. Register your keys
4. Encrypt your view key for the auditor (labelled "Quantum-private")
5. Check the fees
6. Approve with your passkey and sign
7. Confirm onchain

### 4. Shield 21.4 RLS

The fee shown on the previous screen was about 4.14 RLS. The confirmed fee was 3.5814 RLS. The breakdown as shown in the demo UI: gas 3.1142 RLS; Rayls Foundation commission 0.4671 RLS; sum of the components 3.5813 RLS; total shown by the demo UI 3.5814 RLS. Difference: 0.0001 RLS. The cause is unknown. Recorded as an unresolved discrepancy. Shielded amount: 21.4 RLS. Balance after: 17.8252 RLS.

The shield flow steps, as shown in screenshots 2 and 3:

1. Confirm with your passkey
2. Encrypt your note and sign the $RLS transfer (labelled "Quantum-private")
3. Check the fees
4. Approve with your passkey and sign
5. Confirm onchain

One shield action asked for the passkey/PIN twice.

### 5. Confirm onchain

The confirm-onchain step took about 15 seconds with only a spinner and no progress detail. Screenshot 3 shows the step in progress. A partial transaction hash was visible: `0xa8532?10..3caf5cee` (truncated display). The full hash was not recorded.

### 6. Shielded faucet

One click, no passkey. The amounts (50 RLS and 5 $USD) are a reconstruction from the final wallet — see the note below.

RECONSTRUCTION — not direct evidence of the faucet transaction. No dedicated screenshot of the shielded faucet step exists. The amounts are reconstructed from the final wallet (screenshot 4) and the draft notes: shielded $USD is 5, and shielded $RLS is 71.4, which decomposes exactly as 21.4 shielded plus 50 from the shielded faucet. See the reconciliation below. Until a recording or screenshot of the step itself is checked, this stays a reconstruction, not a directly evidenced transaction.

### 6b. Faucet reconciliation

The public faucet and the shielded faucet are two separate transactions, to two separate balances. Checked against the screenshots:

- Public faucet: 5 $USD and 50 $RLS, to the public balance. Visible in screenshot 1 as a completed checklist item on the register-keys screen ("Get test $USD and $RLS — 5 $USD and 50 $RLS"). The screenshot's primary subject is the register step.
- Shielded faucet: 50 RLS and 5 $USD, to the shielded balance. RECONSTRUCTION from the final wallet (screenshot 4), as noted above — not direct evidence of the faucet transaction.
- No double-count. The final wallet columns sum exactly to the totals: $USD 5 public + 5 shielded = 10; $RLS 17.8252 public + 71.4 shielded = 89.2252. Shielded $RLS 71.4 = 21.4 (shield action) + 50 (shielded faucet). Each faucet's funds appear once, in one column only.
- Unresolved discrepancy (0.0001 RLS). The demo's intermediate displayed balances differ from exact subtraction by 0.0001 RLS in two places: 50 − 7.1932 = 42.8068, but the demo shows 42.8067; 42.8067 − 21.4 − 3.5814 = 17.8253, but the demo shows 17.8252. The shield fee components also sum 0.0001 RLS below the shown total: 3.1142 + 0.4671 = 3.5813, but the demo shows 3.5814. The cause of these 0.0001 RLS differences is unknown. They are recorded here as an unresolved discrepancy, not attributed to rounding or to any other cause. The figures in this report are the figures as shown. The final totals are exact.

### 7. Final wallet

Screenshot 4 shows the final state:

| Asset | Total | Public | Shielded |
| --- | --- | --- | --- |
| $USD | 10 ($10.00) | 5 | 5 |
| $RLS | 89.2252 ($0.16) | 17.8252 | 71.4 |

Total wallet value: $10.15.

Arithmetic check: 17.8252 + 71.4 = 89.2252. Shielded 71.4 = 21.4 shielded + 50 from the shielded faucet. $USD 10 = 5 + 5.

The wallet screen also shows an EVM address, an Enygma Spend address, and an Enygma View address, all truncated by the UI. The full values were not recorded.

### 8. Send screen

The send screen was opened. It lists 48 registered users. The shielded-send fee noted in the draft was 4.115 RLS; that figure is recorded in the draft notes, not visible in screenshot 5. No send was completed. No recipient was chosen. No send was confirmed.

### 9. Invite

Not tried. The wallet screen shows an Invite button. Nothing further was observed.

## Issues found

1. The fee shown before confirm changed by the confirm screen, twice. Both times the confirmed fee was lower. Nothing was overcharged. The issue is that the user decides on a number that then moves.
2. One shield action asked for the passkey/PIN twice.
3. The confirm-onchain step took about 15 seconds with only a spinner. No progress detail, no indication of what was happening.
4. A recovery PIN was required right after the passkey, with no warning.

## What this report does not claim

- It does not claim a shielded send hides sender, amount, and receiver. No send was completed.
- It does not claim the invite flow works as described in the AMA. It was not tried.
- It does not claim anything about mainnet performance. This is a testnet demo.
- It does not claim the auditor model works as described. No auditor account was tested.

## Screenshots

All five screenshots are in `demo-testing/screenshots/`. Captured 13 November 2026.

| File | SHA-256 | Shows |
| --- | --- | --- |
| `1-fee-register.png` | `25a81a188885382185ff1230b396f0c972e90aad14a3f41baac8a481d95e1c0e` | Register-keys fee: 7.1932 RLS, balance after 42.8067 RLS |
| `2-fee-shield.png` | `95a4a1cba323335af8471cab11bc55d13b0c8d5ce6da07d63b0db982ec39ffd8` | Shield fee: 3.5814 RLS, shielding 21.4 RLS, balance after 17.8252 RLS |
| `3-confirm-onchain.png` | `8ef88c03ae481fe4944340920a9d15978cc439ae6b1d2ca7c99331b06bd2f51b` | Confirm-onchain step in progress, partial tx hash |
| `4-wallet-akhir.png` | `5d37b3f89ebee2a3d43a9abbaa02903c1197e3b6a682e03859bd03e2f69c484a` | Final wallet: $10.15, $RLS 89.2252 (17.8252 public, 71.4 shielded) |
| `5-send-48-user.png` | `a77696cc8e598bad1a9aa48337d44cbf813f1a4c141e045d92e81f77df73b295` | Send screen, 48 registered users |

The screenshots show a truncated demo address in the first frame. No password, PIN, key, or full address appears in any screenshot.
