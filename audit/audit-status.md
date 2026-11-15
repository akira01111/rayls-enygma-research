# Audit status

Status: 15 November 2026.

This file records what has been checked, what has not, and what comes next. This repository is a research archive. It is not a security audit. The demo client bundle and the public reference repository's protocol document were read. No contract logic was reviewed line by line. No cryptography was tested.

## Done

| Item | Status | Evidence |
| --- | --- | --- |
| Demo session, sign-up to shielded faucet | Done | `demo-testing/test-report.md`, screenshots 1–4 |
| Fee displays and confirmation steps | Done | Screenshots 1–3, exact figures in the test report |
| Final wallet state | Done | Screenshot 4, arithmetic checked |
| Send screen opened | Done | Screenshot 5, 48 registered users |
| AMA listened in full | Done | `ama/ama-notes.md`, paraphrase notes |
| Docs page on privacy and auditing read directly | Done | `findings/verified-facts.md`, quoted |
| Architecture and Enygma Public docs pages read directly | Done | `technical-evidence/technical-evidence.md`, item 8 |
| Rayls auditability blog read directly | Done | `technical-evidence/technical-evidence.md`, item 9 |
| AMA-vs-docs conflict identified and recorded | Done | `findings/unknowns.md`, question 1 |
| Reference repository protocol document read | Done | `technical-evidence/technical-evidence.md`, item 7 |
| Demo client bundle inspected | Done | `technical-evidence/technical-evidence.md`, item 2 |
| Deployment contracts, RPC, and explorer checks | Done | `technical-evidence/technical-evidence.md`, items 1, 3, 4, 5 |
| Event logs retrieved and decoded | Done | `technical-evidence/technical-evidence.md`, item 10. 143 registry logs (63 registrations), 803 vault logs, auditor events decoded. The demo username `@kittyrim` is not among the 63 registered usernames. |
| Screenshots verified as containing no secrets | Done | Checked 15 Nov 2026. No password, PIN, key, or full address appears. Addresses in the screenshots are truncated by the demo UI. |

## Not done

| Item | Why it matters |
| --- | --- |
| Shielded send | The core privacy claim (sender, amount, receiver hidden) is untested. |
| Invite flow | The AMA claim of no gas trace is untested. |
| Auditor account test | The auditor model is described, not observed. |
| Demo session's own transaction hashes | Contract addresses and logs for the deployments are recorded, but the session's own hashes were not. `@kittyrim` is not among the 63 registered usernames on the yx registry. |
| Which deployment the 13 November session used | The bundle embeds two testnet deployments; the first is marked retired 10 November 2026. The yx registry was active on 13 November, but `@kittyrim` is not among its registrations. |
| Demo session's own vault events | Logs for the embedded contracts are decoded, but no vault event can be linked to the demo session's shield, because vault events carry note commitments, not usernames. |
| Deployed implementation source vs public repo | Proxies are verified; implementations were not checked or compared to the reference repository. |
| AMA transcript | No verbatim transcript exists. Notes are paraphrase. |
| Re-check of the demo | The demo may have changed since 13 November 2026. Not re-checked. |
| Event logs for the demo session | No logs were queried. The session's contracts are not identified, so there is no address to query. |

## Open conflicts

1. **Auditor scoping.** AMA: scoped per account and per time. Rayls blog: scoped viewing keys as the Enygma model. Docs (11 Nov 2026): no scoped view keys, access network-wide. Enygma Public docs: the auditor "can read every shielded payment", no scoping described. Reference repository: its auditing section is design, not implemented, and scoped auditing could not be delivered in that construction. Unresolved. The docs describe Private Networks; the demo runs on the Public Chain testnet. That environment difference is possible context only, not a proven explanation. See `research/open-questions.md`, question 1, and `technical-evidence/technical-evidence.md`.

## Next steps

1. Complete one shielded send. Record the full transaction hash. Check what appears on chain.
2. Try the invite flow. Record what the recipient sees.
3. Identify which deployment a new demo run uses, and record its registry address before starting.
4. Check the deployed implementations' verified source and compare them with the public reference repository.
5. Ask Rayls, in the open, which deployment the scoped-auditor description applies to.
6. Re-check the demo. Confirm whether the session state and the fee behaviour are the same.
7. Record full transaction hashes and contract addresses for any future demo run.

## Version note

This is the initial documentation. It covers the research available as of 15 November 2026: one demo session (13 Nov), one AMA listen (13 Nov), three docs pages read directly (15 Nov), the Rayls auditability blog (15 Nov), the public reference repository's protocol document (15 Nov), and the demo bundle, RPC, and explorer checks (15 Nov).
