# Official claims

Statements from Rayls or its team. Not independently verified. Source for all items in this file, unless noted otherwise: the Enygma AMA, Rayls Labs X post 2120881854442065955, 38 minutes 43 seconds, listened 13 November 2026. AMA content is paraphrase from listening notes. No verbatim transcript exists.

## Auditor access (AMA)

**OFFICIAL CLAIM.** An auditor can see all shielded transactions. Access can be scoped per account and per time. A law-enforcement request can be limited to disclosing a single transaction.

**OFFICIAL CLAIM.** The docs saying the auditor view is limited are outdated. The specific docs page or passage was not recorded during the AMA listen.

**OFFICIAL CLAIM.** The pilot auditor is the Rayls Foundation. Who audits later is undecided. It could be a third-party law firm.

Note: the docs page read 15 November 2026 states the opposite on scoping. See `findings/verified-facts.md` and `findings/unknowns.md`. The conflict is unresolved.

## What an outsider sees (AMA)

**OFFICIAL CLAIM.** When a shielded transfer happens, an outsider sees only that a shielded transfer happened, plus the commission. Sender, amount, and receiver are hidden.

**OFFICIAL CLAIM.** The proof for the transfer is built in the browser in about 2.2 seconds. Gas is paid in shielded RLS.

**OFFICIAL CLAIM.** The invite flow lets someone receive shielded RLS with no gas trace on chain. The invite flow was not tried in this research.

## Fees (AMA)

**OFFICIAL CLAIM.** In this version, Rayls Foundation takes a 15% commission. The demo UI shows the same 15% figure in the fee breakdowns, so this claim is also supported by direct observation. See `findings/verified-facts.md`.

## Scope of privacy (AMA)

**OFFICIAL CLAIM.** Quantum-private applies only to the shielded pool. The Rayls chain itself is still like Ethereum.

**OFFICIAL CLAIM.** There is no mobile app yet. The website runs on a phone.

## UX (AMA)

**OFFICIAL CLAIM.** UX is the biggest weakness. The most valuable feedback covers the simplest flow: sign up, send, shield, invite. What worked, what confused or broke, and what to change first.

## Docs and site (official pages)

**OFFICIAL CLAIM.** Rayls describes Enygma as a programmable privacy layer for EVM-compatible blockchains, built for confidential transactions and data sharing. Sources: <https://www.rayls.com/blog/private-verifiable-and-compliant-what-is-rayls-enigma> and <https://www.rayls.com/blog/introducing-rayls-enygma-a-new-era-of-privacy-for-evm-chains>.

**OFFICIAL CLAIM.** Rayls states Enygma has an Auditor View feature that lets authorized auditors access encrypted data when necessary. Source: the "Introducing Rayls Enygma" blog post above. How the Auditor View is scoped is exactly the point in dispute; see the conflict note above.

**OFFICIAL CLAIM.** The Enygma Public docs page states that when an account registers, a copy of its view key is encrypted to the deployment's auditor, "so the auditor can read every shielded payment: shielded from the public, not from the auditor. The auditor can read, but it can't freeze or move funds." No scoping is described on that page. Source: <https://docs.rayls.com/docs/enygma-public>, read 15 November 2026. See `findings/unknowns.md`, question 1.

**OFFICIAL CLAIM.** Rayls' blog "Auditability without surveillance" describes the Enygma model as mathematical enforcement: the cryptographic construction supports keys scoped to particular subsets of data, and the boundary is a mathematical constraint, not an administrator's configuration. Its examples include a regulator given a viewing key scoped to a specific bank's transactions over a specific time window, and a counterparty bank given a viewing key scoped to a specific bilateral relationship. Source: <https://www.rayls.com/blog/auditability-without-surveillance-why-mathematical-enforcement-beats-trusting-the-code>, read 15 November 2026. This conflicts with the docs page that states there are no scoped view keys. See `findings/unknowns.md`, question 1.
