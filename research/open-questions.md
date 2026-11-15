# Open questions

Status: 15 November 2026. Ordered by how much they matter to the research.

## 1. Does the auditor model in the AMA match the docs?

The AMA answer describes auditor access scoped per account and per time, with law-enforcement disclosure limited to a single transaction. The docs page "Who sees what: privacy and oversight", updated 11 November 2026, states there are no scoped view keys and audit access is network-wide.

Possible explanations, none confirmed:

- The AMA described a planned design, not the current one.
- The AMA described the Public Chain demo variant, while the docs describe Private Networks. That environment difference is possible context only. It is not a proven explanation for the conflict, and it does not resolve it.
- The docs page is outdated, and the AMA is the newer statement. The docs page was updated 11 November 2026; the AMA was 12 November 2026. The dates are one day apart and do not settle it.
- The two sources use "auditor" to mean different roles.

What would settle it: a statement from Rayls that names the deployment (Public Chain testnet vs Private Network) and the scoping behaviour, or a direct test of an auditor account. Neither exists in this research.

## 2. Does a shielded send hide sender, amount, and receiver?

The AMA says yes. The demo was not taken that far. The send screen was opened; no send was completed. Until someone completes a shielded send and checks what appears on chain, this is an AMA claim, not a verified fact.

## 3. What does the invite flow do?

The wallet screen shows an Invite button. The AMA describes the invite flow as letting someone receive shielded RLS with no gas trace on chain. It was not tried. What the invite link contains, what the recipient sees, and whether any on-chain trace appears are all unknown.

## 4. What does "Quantum-private" guarantee in the demo?

The label appears in the demo UI on two steps: encrypting the view key for the auditor, and encrypting the note for a shield transfer. The official docs (architecture and Enygma Public pages, read 15 November 2026) state the notes and escrowed view keys are encrypted with ML-KEM-768, and that the zero-knowledge proofs, passkeys, and signatures are not post-quantum. What the label guarantees in practice for a user was not verified. No proof was captured or checked.

## 5. Which docs pages describe the auditor view as limited?

The AMA answer says the docs saying the auditor view is limited are outdated. The specific docs page or passage was not recorded during the AMA listen. The docs page read for this research states the opposite (network-wide access), so the "outdated" passage, if it exists, is a different page. It has not been found.

## 6. Do the six-participant anonymity set and the relayer masking apply to the Public Chain demo?

The docs describe these for Private Networks. The demo runs on the Public Chain testnet. The demo does not show participant counts or relayer details for a transfer. Whether the demo shares these properties is unknown.

## 7. What are the full transaction hashes and contract addresses?

The demo UI truncates addresses and transaction hashes. One partial hash was visible during the confirm-onchain step: `0xa8532?10..3caf5cee` (truncated display). No full hash was recorded. Contract addresses for the deployments in the demo bundle are now recorded in `technical-evidence/technical-evidence.md`, but no full transaction hash for the demo session was recorded and the session's registry is unidentified. Without the session's own hashes, no on-chain check of the demo transactions is possible from this research.

## 8. Is the fee estimate a quote or an estimate?

The shown fee changed before confirm, twice, both times downward. The demo does not label the first figure as an estimate. Whether the change comes from gas price movement, a recalculation, or a different fee path is unknown.

## 9. Does the demo state persist?

The session was on 13 November 2026. Whether the testnet wallet, balances, and username still exist, and whether the demo has changed since, was not re-checked.

## 10. What is the status of Enygma on the Public Chain?

Third-party reviews (October 2026) state the docs mark Enygma as in production on Private Networks and coming soon to the Public Chain, and that the Public Chain explorer shows no live Enygma privacy layer. Those reviews were not independently verified here. The demo itself is live on the Public Chain testnet, which is a testnet deployment, not a mainnet one.
