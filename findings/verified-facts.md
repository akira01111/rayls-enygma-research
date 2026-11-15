# Verified facts

Checked directly, with evidence. Date checked: 13 November 2026 for the demo session, 15 November 2026 for the docs read.

## Demo session, 13 November 2026

**VERIFIED FACT.** The Enygma demo runs at `enygma-testnet.rayls.com`. The tester signed up on a phone with username `@kittyrim`. The demo header shows "Rayls Public Chain Testnet". Evidence: screenshots 1–5.

**VERIFIED FACT.** Sign-up works with a passkey through Google Password Manager. The username check is instant. A recovery PIN is required right after the passkey. Evidence: demo run; the recovery PIN step was observed. The PIN value is not recorded anywhere.

**VERIFIED FACT.** The public faucet gives 5 $USD and 50 $RLS in one click, with no passkey. Evidence: screenshot 1 (the register-keys screen, `1-fee-register.png`) shows it as a completed checklist item: "Get test $USD and $RLS — 5 $USD and 50 $RLS". The screenshot's primary subject is the register step; the faucet amounts appear in its checklist.

**VERIFIED FACT.** Registering keys cost 7.1932 RLS. The fee shown on the previous screen was about 8.004 RLS. The confirmed breakdown: 6.255 gas plus 0.9382 Rayls Foundation commission (15%). Balance after: 42.8067 RLS. Evidence: screenshot 1.

**VERIFIED FACT.** Shielding 21.4 RLS cost 3.5814 RLS. The fee shown on the previous screen was about 4.14 RLS. The confirmed breakdown, as shown in the demo UI: gas 3.1142 RLS; Rayls Foundation commission 0.4671 RLS; sum of the components 3.5813 RLS; total shown by the demo UI 3.5814 RLS. Difference: 0.0001 RLS. The cause is unknown. Recorded as an unresolved discrepancy. Balance after: 17.8252 RLS. Evidence: screenshot 2.

**RECONSTRUCTION — from the final wallet balance, not direct evidence of the faucet transaction.** The shielded faucet is recorded as giving 50 RLS and 5 $USD in one click, straight into the shielded balance. Evidence: final wallet (screenshot 4) — shielded $USD 5 and shielded $RLS 71.4 = 21.4 + 50. No dedicated screenshot of the shielded faucet step exists. The amounts are reconstructed from the final wallet and the draft notes. See the faucet reconciliation in `demo-testing/test-report.md`.

**VERIFIED FACT.** The final wallet after the run: $10.15 total. $USD 10 total ($10.00): 5 public, 5 shielded. $RLS 89.2252 total ($0.16): 17.8252 public, 71.4 shielded. Evidence: screenshot 4. Arithmetic checks: 17.8252 + 71.4 = 89.2252. Shielded 71.4 = 21.4 shielded + 50 (the 50 is reconstructed as the shielded faucet; see the reconstruction note above). $USD 10 = 5 + 5.

**VERIFIED FACT.** The demo charges a 15% Rayls Foundation commission inside each fee. The figure appears in the demo UI itself, in the fee breakdowns of screenshots 1 and 2. It is not only an AMA statement.

**VERIFIED FACT.** The confirm-onchain step took about 15 seconds with only a spinner and no progress detail. Evidence: screenshot 3 shows the "Confirm onchain" step in progress; timing from the demo run.

**VERIFIED FACT.** One shield action asked for the passkey/PIN twice. Evidence: demo run.

**VERIFIED FACT.** The send screen lists 48 registered users. The tester opened the screen but did not complete a send. The shielded-send fee shown in the draft notes was 4.115 RLS; that figure is recorded in the draft, not visible in screenshot 5. Evidence: screenshot 5.

**VERIFIED FACT.** The shield flow has five steps: confirm with passkey; encrypt the note and sign the $RLS transfer; check the fees; approve with passkey and sign; confirm onchain. Evidence: screenshots 2 and 3.

**VERIFIED FACT.** The register flow has seven steps: passkey created; get test funds; register keys; encrypt the view key for the auditor; check the fees; approve with passkey and sign; confirm onchain. Evidence: screenshot 1.

**VERIFIED FACT.** The demo UI labels two steps "Quantum-private": encrypting the view key for the auditor, and encrypting the note for a shield transfer. Evidence: screenshots 1 and 2. What the label guarantees was not verified.

## Docs, read 15 November 2026

**VERIFIED FACT.** The docs page "Who sees what: privacy and oversight" states: "Audit access is network-wide. The operator, and anyone the network's rules allow to use its tools, such as a regulator, sees every transfer in the network." It also states: "There are no scoped view keys. You can't give an auditor a key limited to one account, one time window or one transaction." Source: <https://docs.rayls.com/docs/enygma-privacy-and-auditing>, page updated 2026-11-11T15:26:41Z.

**VERIFIED FACT.** The same docs page states the Private Network operator holds each participant's view key, not its spend key, so it can read transfers but cannot sign or move funds. It states the operator sees only what crosses the Hub, and activity inside a member's own Sovereign chain stays outside the operator's view. It states mint and burn amounts, and the participant, are public on the Hub.

**VERIFIED FACT.** The same docs page states each Enygma transaction names up to six participants, and participants not part of the payment receive a commitment to zero. It states the sender's wallet is masked: on a chain where transactions pay gas, a relayer submits each transaction.

**VERIFIED FACT.** The docs page describes Rayls Private Networks (Sovereign chains and a Hub). It does not describe the Public Chain demo. The demo runs on the Rayls Public Chain testnet. This difference matters for open question 1.

## Quest context

**VERIFIED FACT.** The Rayls weekly content quest allows one submission per week, max 10 points. The week in question closed Sunday 15 November 2026 23:59 UTC (Monday 16 November 2026 06:59 WIB). Submissions close around 29 November 2026. Source: quest brief as pasted 13 November 2026.

**VERIFIED FACT.** The first article in this quest series, on selective freezing, scored 85/100 and was approved. The second article, on 47 transactions in 2,400 mainnet blocks, was published 9 November 2026. Those articles are separate work and are not in this repository.
