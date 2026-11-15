# Technical overview

This file summarises what Enygma is, from the docs and the AMA. Each paragraph carries one label. Nothing here is a security finding.

## What Enygma is

**OFFICIAL CLAIM.** Rayls describes Enygma as a programmable privacy layer for EVM-compatible blockchains. It is built for confidential transactions and data sharing. Institutions use it to transact without publishing transaction details. Source: <https://www.rayls.com/blog/private-verifiable-and-compliant-what-is-rayls-enigma> and <https://www.rayls.com/blog/introducing-rayls-enygma-a-new-era-of-privacy-for-evm-chains>.

**VERIFIED FACT.** The demo runs on the Rayls Public Chain testnet. The demo header shows "Rayls Public Chain Testnet" and the username. The demo URL is `enygma-testnet.rayls.com`.

## How shielding works in the demo

**OBSERVATION.** Shielding moves funds from a public balance to a shielded balance. The wallet screen shows both balances side by side, with separate totals for $USD and $RLS. The shield flow has five steps: confirm with passkey, encrypt the note and sign the transfer, check the fees, approve with passkey and sign, confirm onchain.

**OFFICIAL CLAIM.** In the AMA, Alex said an outsider sees only that a shielded transfer happened, plus the commission. Sender, amount, and receiver are hidden. The proof for the transfer is built in the browser in about 2.2 seconds. Gas is paid in shielded RLS.

**UNKNOWN.** The shielded send was not completed in this research, so the claim that a send hides sender, amount, and receiver was not tested. The demo UI labels the encryption step "Quantum-private". What that label guarantees was not verified.

## The auditor model

**OFFICIAL CLAIM (AMA).** An auditor can see all shielded transactions. Access can be scoped per account and per time. A law-enforcement request can be limited to disclosing a single transaction. The pilot auditor is the Rayls Foundation. Who audits later is undecided, possibly a third-party law firm. The docs saying the auditor view is limited are outdated, per the AMA answer.

**VERIFIED FACT (docs).** The official docs page "Who sees what: privacy and oversight" states the opposite on scoping: "Audit access is network-wide" and "There are no scoped view keys. You can't give an auditor a key limited to one account, one time window or one transaction." Source: <https://docs.rayls.com/docs/enygma-privacy-and-auditing>, read 15 November 2026, page updated 11 November 2026.

**INFERENCE.** The two sources may describe different deployments. The docs page describes Rayls Private Networks (Sovereign chains and a Hub). The demo runs on the Public Chain testnet. That environment difference is possible context only. It is not a proven explanation for the conflict, and it does not resolve it. See `findings/unknowns.md`.

**VERIFIED FACT (docs).** Per the same docs page, the Private Network operator holds each participant's view key, not its spend key, so it can read transfers but cannot sign or move funds. The operator sees only what crosses the Hub. Activity inside a member's own Sovereign chain never reaches the Hub and stays outside the operator's view. Mint and burn amounts, and the participant, are public on the Hub.

**OBSERVATION.** The demo UI includes an "Encrypt your view key for the auditor" step during key registration. The view key is encrypted for the auditor as part of registration. The demo UI itself does not show who the auditor is. The demo's client bundle, read 15 November 2026, names the auditor address `0x71AF09966CBED4434ccA97c40Fa38B8083548B95` in every deployment it embeds. See `technical-evidence/technical-evidence.md`.

## Deployment and on-chain evidence

**VERIFIED FACT.** The testnet chain ID is 7,295,799, verified by a live `eth_chainId` call to `https://testnet-rpc.rayls.com` on 15 November 2026. The deployed registry and vault proxies are verified on the testnet explorer. The full addresses, deployment transaction hashes, RPC results, and the registry ABI's auditor functions are in `technical-evidence/technical-evidence.md`.

**UNKNOWN.** Which deployment the 13 November 2026 demo session used. The bundle embeds two Rayls testnet deployments. The first is marked retired on 10 November 2026. The yx registry was active on 13 November 2026: it has 143 logs in total, running through 13 November 22:05:57 UTC (block 23697459). The registration of `@kittyrim` on 13 November does not appear in either registry's on-chain history. See `findings/unknowns.md`, question 11.

## Fees

**VERIFIED FACT.** The demo charges a 15% Rayls Foundation commission inside each fee. The register fee was 7.1932 RLS: 6.255 gas plus 0.9382 commission. The shield fee was 3.5814 RLS: gas 3.1142 RLS plus commission 0.4671 RLS, which sum to 3.5813 RLS, 0.0001 RLS below the total shown by the demo UI. The cause of the 0.0001 RLS difference is unknown. Recorded as an unresolved discrepancy. Both breakdowns are visible in the screenshots.

**OFFICIAL CLAIM (AMA).** In this version, Rayls Foundation takes a 15% commission. The demo UI confirms the 15% figure independently.

**VERIFIED FACT.** The fee shown before confirm differed from the fee charged, twice. See `demo-testing/test-report.md`.

## Limits stated by Rayls

**OFFICIAL CLAIM (AMA).** Quantum-private applies only to the shielded pool. The Rayls chain itself is still like Ethereum. There is no mobile app yet; the website runs on a phone.

**OFFICIAL CLAIM (docs).** Each Enygma transaction names up to six participants. Participants not part of the payment receive a commitment to zero. With four to six participants, a participant that receives nothing learns only that value may have moved between some of the others. Source: <https://docs.rayls.com/docs/enygma-privacy-and-auditing>.

**UNKNOWN.** Whether the six-participant anonymity set applies to the Public Chain demo, or only to Private Networks, was not established. The demo does not show participant counts for a transfer.
