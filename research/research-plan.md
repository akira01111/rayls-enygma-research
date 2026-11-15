# Research plan

Date: 13–15 November 2026.
Tester: one person, on a phone, demo username `@kittyrim`.
Status: initial documentation complete. Testing incomplete (send and invite untested).

## Questions

The research started from the Rayls weekly quest question: what is a private EVM, and why would a financial institution need one?

That question breaks into smaller ones:

1. What does the Enygma demo actually let a user do?
2. What is hidden when a transaction is shielded, and from whom?
3. Who can still see a shielded transaction, and under what limits?
4. What does each step cost, and are the shown costs the costs charged?
5. Where does the demo confuse or mislead a first-time user?
6. What does the AMA claim that the demo cannot confirm?
7. Where do the AMA and the docs disagree?

## Scope

In scope:

- The Enygma demo on the Rayls Public Chain testnet, as tried on 13 November 2026.
- The user-facing flows: sign-up, faucet, key registration, shielding, send screen, invite entry point.
- The fee displays and the confirmation steps.
- The auditor-access model, as described in the AMA and in the official docs.
- The weekly quest context: one article per week, max 10 points.

Out of scope:

- The Rayls mainnet. Nothing here is mainnet evidence.
- Rayls Private Networks as deployed systems. The docs describe them; they were not tested.
- Enygma source code and cryptography. No code review was done.
- The invite flow and the shielded send, until someone tests them.
- Price, token value, or investment questions.

Related work, separate repository: mainnet block research at <https://github.com/akira01111/rayls-mainnet-block-research>.

## Method

1. Try the demo by hand, one step at a time, and record each screen. Three screen recordings were made. Five screenshots were kept. Transcription of the three recordings returned no speech segments. The recordings are silent screen captures, not transcripts and not evidence of any conversation.
2. Record every number exactly as shown. Check the arithmetic after (faucet amounts minus fees against the shown balances).
3. Listen to the Enygma AMA in full (38 minutes 43 seconds) and take notes. The AMA was listened to on 13 November 2026. No transcript file exists, so AMA content is recorded as paraphrase.
4. Read the official docs pages directly, 15 November 2026: privacy and auditing, architecture, and Enygma Public, plus the Rayls auditability blog. Quote them where they matter.
5. Label every finding. See `README.md` for the labels.
6. Record conflicts instead of resolving them by picking a side.

## What was not done

- No shielded send was completed.
- The invite flow was not tried.
- No auditor account was tested. The auditor model is described, not observed.
- No contract logic was reviewed line by line. The deployed contracts were inspected on 15 November 2026 (demo bundle, RPC, explorer, event logs) — see `technical-evidence/technical-evidence.md`. The demo session's own contract addresses and transaction hashes were not recorded.
- The docs were not read in full. Three pages were read directly on 15 November 2026 (privacy and auditing, architecture, Enygma Public), plus the auditability blog. Other Enygma docs pages are still unchecked.

## Reproducing the demo run

The demo is at `enygma-testnet.rayls.com`. It is password-gated. The password is provided in Rayls quest materials and is not recorded in this repository.

Steps, in order: sign up with a username, create a passkey, take test funds from the public faucet, register keys, shield funds, optionally use the shielded faucet. The send screen and the invite button are visible from the wallet screen. Each step is described with exact figures in `demo-testing/test-report.md`.

The demo state is a testnet. Balances and usernames from 13 November 2026 may not persist.
