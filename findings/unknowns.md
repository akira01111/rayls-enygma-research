# Unknowns

Information not found, not tested, or not decidable from the evidence. Status: 15 November 2026.

## 1. Auditor scoping: AMA vs docs

**UNKNOWN.** The AMA answer describes auditor access scoped per account and per time, with law-enforcement disclosure limited to a single transaction. The docs page "Who sees what: privacy and oversight" states there are no scoped view keys and audit access is network-wide.

The docs page was updated 11 November 2026. The AMA was 12 November 2026. The dates do not settle which statement is current.

The docs page describes Rayls Private Networks. The demo runs on the Public Chain testnet. That environment difference is possible context only. It is not a proven explanation for the conflict, and it does not resolve it.

More sources were checked on 15 November 2026, and they do not settle it either. The Enygma Public docs page states the deployment's auditor "can read every shielded payment", with no scoping described. Rayls' own blog "Auditability without surveillance" describes the Enygma model as viewing keys scoped to particular subsets of data, for example a regulator scoped to one bank's transactions over one time window. The public reference repository's protocol document states its auditing section is design, not implemented, and that scoped auditing could not be delivered in that construction at all. See `technical-evidence/technical-evidence.md`.

Until Rayls clarifies, or an auditor account is tested, this stays unknown. Neither source is treated as wrong. All are recorded.

## 2. Shielded send privacy

**UNKNOWN.** Whether a completed shielded send hides sender, amount, and receiver. The AMA says it does. The demo was not taken that far. No on-chain check was done.

## 3. Invite flow

**UNKNOWN.** What the invite link contains, what the recipient sees, and whether any on-chain trace appears. The flow was not tried.

## 4. Meaning of "Quantum-private"

**UNKNOWN.** The demo UI labels two steps "Quantum-private". The official docs now verify the mechanism behind the label: the architecture page and the Enygma Public page both state the notes and escrowed view keys are encrypted with ML-KEM-768, and that the zero-knowledge proofs, passkeys, and signatures are not post-quantum. What the label guarantees in practice for a user was not verified. No proof was captured or checked.

## 5. The docs passage the AMA calls outdated

**UNKNOWN.** The AMA answer says the docs saying the auditor view is limited are outdated. The specific page or passage was not recorded. The docs page read for this research states the opposite, so the passage in question, if it exists, is a different page. It has not been found.

## 6. Anonymity set and relayer on the Public Chain demo

**UNKNOWN.** The docs describe an anonymity set of up to six participants and sender masking through a relayer, for Private Networks. Whether these apply to the Public Chain demo is not established. The demo does not show participant counts or relayer details for a transfer.

## 7. Full transaction hashes for the demo session

**UNKNOWN.** No full transaction hash for the demo session was recorded. The demo UI truncates hashes. One partial hash was visible during confirm-onchain: `0xa8532?10..3caf5cee` (truncated display).

Contract addresses are no longer unknown. The deployed registry, vault, verifier, and forwarder addresses for the testnet deployments in the demo bundle are recorded in `technical-evidence/technical-evidence.md`, with deployment transaction hashes from the bundle and the explorer logs. The event logs for all four embedded contracts were retrieved and decoded (item 10 there): the yx registry has 63 registrations, the yx vault has 803 events, and the auditor events were decoded. But the demo username `@kittyrim` is not among the 63 decoded usernames, and no registered address matches the demo's truncated EVM address. The demo session's own transactions cannot be looked up on-chain from this research.

## 8. Why the shown fee changed

**UNKNOWN.** The shown fee changed before confirm, twice, both times downward. Whether the change comes from gas price movement, a recalculation, or a different fee path is unknown. The demo does not label the first figure as an estimate.

## 9. Demo persistence

**UNKNOWN.** Whether the testnet wallet, balances, and username from 13 November 2026 still exist, and whether the demo has changed since. Not re-checked.

## 10. Enygma status on the Public Chain

**UNKNOWN.** Third-party reviews (October 2026) state the docs mark Enygma as in production on Private Networks and coming soon to the Public Chain, and that the Public Chain explorer shows no live Enygma privacy layer. The second part is now contradicted for the testnet: verified Enygma contracts (registry and vault proxies, verifier, gas forwarder) exist on the Public Chain testnet, chain ID 7,295,799, with deployment transactions in November 2026. See `technical-evidence/technical-evidence.md`. The demo is live on the Public Chain testnet, which is a testnet deployment, not mainnet. Whether Enygma is live on the Public Chain mainnet is still unknown.

## 11. Which deployment the 13 November demo session used

**UNKNOWN.** The demo bundle embeds two Rayls testnet deployments (`7295799.json` and `br/7295799.json`). The first is marked `retired: 2026-11-10`, three days before the demo session. The yx registry was active on 13 November 2026 (its logs run to 13 November 22:05:57 UTC), with 63 registrations — but the demo username `@kittyrim` is not among the 63 decoded usernames, and no registered address matches the demo's truncated EVM address. The bx registry has no registrations at all. The registration of `@kittyrim` on 13 November does not appear in either registry's on-chain history. The app selects a deployment by region, defaulting to `uk`, but which deployment the session actually used was not recorded. See `technical-evidence/technical-evidence.md`, items 3 and 10.

## 12. Implementation source and match to the public repository

**UNKNOWN.** The deployed proxies are verified on the explorer, but their implementation contracts were not checked for verified source, and no implementation was compared against the public Enygma reference repository. Whether the deployed code matches the public repo is unknown. The implementation addresses are in the bundle and the explorer API is public, so this can be checked later. See `technical-evidence/technical-evidence.md`, items 4 and 10.
