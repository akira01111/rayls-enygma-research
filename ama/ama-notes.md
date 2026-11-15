# Enygma AMA notes

Source: Rayls Labs X post 2120881854442065955, 38 minutes 43 seconds. Listened in full on 13 November 2026.

## Note on the source

No verbatim transcript exists. A fetch attempt for a transcript file returned a Cloudflare challenge page, not a transcript. Everything below is paraphrase from listening notes, not quotation. Exact wording was not captured. Timestamps are approximate, from the listening notes.

Speaker: Alex (Alex Buelau), answering questions. The notes below record what was said, not what was verified.

## Questions and answers

### Q1. Auditor access (asked by the tester, answered at about 38:43)

Question: if transactions are private, who audits them?

Answer, paraphrased: an auditor can see all shielded transactions. Access can be scoped per account and per time. A law-enforcement request can be limited to disclosing a single transaction. The pilot auditor is the Rayls Foundation. Who audits later is undecided. It could be a third-party law firm.

The answer also said the docs saying the auditor view is limited are outdated. The specific docs page or passage was not recorded.

Status: OFFICIAL CLAIM. The docs page read 15 November 2026 states the opposite on scoping. See `findings/unknowns.md`, question 1. The conflict is unresolved.

### Shielded transfers: what an outsider sees

Answer, paraphrased: an outsider sees only that a shielded transfer happened, plus the commission. Sender, amount, and receiver are hidden. The proof for the transfer is built in the browser in about 2.2 seconds. Gas is paid in shielded RLS.

Status: OFFICIAL CLAIM. The shielded send was not completed in the demo session, so this was not tested.

### Commission

Answer, paraphrased: in this version, Rayls Foundation takes a 15% commission.

Status: OFFICIAL CLAIM, with independent support. The demo UI shows the same 15% commission inside the fee breakdowns. See `demo-testing/test-report.md`.

### Scope of privacy

Answer, paraphrased: quantum-private applies only to the shielded pool. The Rayls chain itself is still like Ethereum. There is no mobile app yet. The website runs on a phone.

Status: OFFICIAL CLAIM. The "Quantum-private" label appears in the demo UI. What it guarantees was not verified.

### Invite flow

Answer, paraphrased: the invite flow lets someone receive shielded RLS with no gas trace on chain.

Status: OFFICIAL CLAIM. The invite flow was not tried.

### UX

Answer, paraphrased: UX is the biggest weakness. The most valuable feedback covers the simplest flow: sign up, send, shield, invite. What worked, what confused or broke, and what to change first.

Status: OFFICIAL CLAIM. The demo session found three UX issues that fit this exactly: fees changing between screens, a double passkey prompt, and a 15-second spinner with no progress detail. See `findings/observations.md`.

## Implications recorded at the time

- The auditor answer is the core of the quest question. A bank needs privacy from the public and visibility for an auditor. The AMA describes both halves.
- The scoped-access description is the part that conflicts with the docs. That conflict was found after the AMA listen, during the docs read on 15 November 2026.
- The AMA answer on what an outsider sees cannot be confirmed from the demo alone, because no shielded send was completed.

## What is missing

- A verbatim transcript. None exists in this research.
- The exact wording of the auditor answer. Only the paraphrase above was recorded.
- The docs passage the answer calls outdated. Not recorded.
- Any other questions asked in the AMA. Only the items above were noted.
