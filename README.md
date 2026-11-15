# rayls-enygma-research

This repository documents an independent review of the Rayls Enygma testnet demo.

The research covers the user-facing flows, transaction shielding, fee displays, confirmation steps, and the auditor-access model described by the Rayls team.

It combines observations from a hands-on demo session with information from official documentation and the Enygma AMA.

The repository also records what has not yet been verified. A feature appearing in the interface does not automatically mean that the underlying operation has been tested successfully.

Last updated: 15 November 2026.

## Research scope

The subject is the Enygma demo on the Rayls Public Chain testnet, as tried on 13 November 2026. The demo is a browser wallet at `enygma-testnet.rayls.com`. The tester signed up, used the faucets, registered keys, shielded funds, and opened the send screen. No shielded send was completed. The invite flow was not tried.

The research also covers the auditor-access model. Two sources describe it differently: the Enygma AMA and the official docs page on privacy and auditing. Both versions are recorded here, with the conflict marked as unresolved. See `findings/unknowns.md`.

Out of scope: the Rayls mainnet, Rayls Private Networks (Sovereign chains and the Hub) as deployed systems, and any security audit of the cryptography. The public reference repository and the demo's client bundle were read for the technical evidence in `technical-evidence/technical-evidence.md`. That reading is not a code audit. A separate repository holds the mainnet block research: <https://github.com/akira01111/rayls-mainnet-block-research>.

## What was tested

One hands-on session, 13 November 2026, on a phone:

| Step | Result |
| --- | --- |
| Sign-up and passkey | Completed. Username `@kittyrim`. |
| Public faucet | Completed, as shown by a completed checklist item on the register screen; no dedicated faucet screenshot. 5 $USD and 50 $RLS per that checklist item. |
| Register keys | Completed. Fee confirmed at 7.1932 RLS. |
| Shield 21.4 RLS | Completed. Fee confirmed at 3.5814 RLS. |
| Shielded faucet | RECONSTRUCTION. No dedicated screenshot; 50 RLS and 5 $USD inferred from the final wallet balance.¹ |
| Shielded send | Not completed. The send screen was opened only. |
| Invite | Not tried. |

¹ No dedicated screenshot; amounts reconstructed from the final wallet balance (screenshot 4). See `demo-testing/test-report.md`.

Full detail, with exact figures, is in `demo-testing/test-report.md`. Screenshots are in `demo-testing/screenshots/`.

## Key observations

- The fee shown on one screen changed by the confirm screen, twice. Register showed about 8.004 RLS and confirmed at 7.1932 RLS. Shield showed about 4.14 RLS and confirmed at 3.5814 RLS. Both confirmed fees were lower than the shown estimates.
- One shield action asked for the passkey/PIN twice.
- The confirm-onchain step took about 15 seconds with only a spinner and no progress detail.
- The demo UI itself shows a 15% Rayls Foundation commission inside each fee breakdown.
- The AMA and the docs disagree on auditor access. The AMA answer describes access scoped per account and per time. The docs page, updated 11 November 2026, states there are no scoped view keys and that audit access is network-wide. This conflict is unresolved. The docs page describes Private Networks; the demo runs on the Public Chain testnet. That difference is recorded here only as possible context. It is not a proven explanation for the conflict, and it does not resolve it. See `findings/unknowns.md`.
- Technical evidence added 15 November 2026: the testnet chain ID is 7,295,799, verified by a live RPC call. The deployed registry and vault proxies are verified on the testnet explorer, and the demo bundle names the auditor address. Event logs were retrieved and decoded: 63 registrations on the testnet registry and 803 vault events, including 7 `AuditorAdded` events — but only 4 of the 7 added accounts have an `AuditorKeyGiven` event, so nothing here shows the other 3 received a key, and no event proves what any auditor can read. The demo username `@kittyrim` is not among the 63 registered usernames, so the deployment the 13 November session used is still unknown. See `technical-evidence/technical-evidence.md`.

## Evidence and sources

- Five screenshots from the demo session, 13 November 2026, in `demo-testing/screenshots/`. Each file lists its SHA-256 in `demo-testing/test-report.md`.
- Three silent screen recordings of the demo run. Transcription returned no speech segments. Their SHA-256 values are in `sources/source-register.md`.
- Enygma AMA, Rayls Labs X post 2120881854442065955, 38 minutes 43 seconds, listened 13 November 2026. No verbatim transcript exists. AMA notes are paraphrase from listening notes. See `ama/ama-notes.md`.
- Official docs, read directly 15 November 2026: <https://docs.rayls.com/docs/enygma-privacy-and-auditing> (page updated 11 November 2026), <https://docs.rayls.com/docs/rayls-high-level-architecture> (updated 11 November 2026), <https://docs.rayls.com/docs/enygma-public> (updated 11 November 2026).
- Technical evidence, checked 15 November 2026: the demo client bundle (SHA-256 recorded), the public RPC (`eth_chainId` 7,295,799), the testnet explorer API (verified proxy source, registry transaction lists), and the public Enygma reference repository's protocol document. Full detail in `technical-evidence/technical-evidence.md`.
- Rayls website: <https://www.rayls.com/>. Docs home: <https://docs.rayls.com/>. Transparency Portal: <https://transparency.rayls.com/>.

The full source list is in `sources/source-register.md`.

## Verification methodology

Every finding carries one label:

- **VERIFIED FACT.** Checked directly, with evidence. A screenshot, a docs page read, or a completed demo step.
- **OFFICIAL CLAIM.** Stated by Rayls or a team member. Not independently verified.
- **OBSERVATION.** Seen or experienced during the demo session.
- **INFERENCE.** A provisional reading of the evidence. Marked as such.
- **RECONSTRUCTION.** A number or event inferred from indirect evidence, not a directly observed or directly recorded transaction.
- **UNKNOWN.** Not found, not tested, or not decidable from the evidence.

Labels are not mixed in one paragraph. A claim from the AMA stays a claim until something independent confirms it. A testnet result is never presented as mainnet evidence.

Numbers are recorded exactly as shown. Where the shown figures differ from exact arithmetic, the difference is noted as an unresolved discrepancy.

## Known limitations

- One tester, one session, one phone. Results may differ on another device or at another time.
- The shielded send was not completed, so nothing here proves a shielded send hides sender, amount, and receiver. That claim rests on the AMA answer alone.
- The invite flow was not tried.
- The AMA notes are paraphrase, not a transcript. Exact wording was not captured.
- No contract addresses or full transaction hashes for the demo session were recorded. The demo UI truncates addresses and hashes. Contract addresses for the deployments in the demo bundle are recorded in `technical-evidence/technical-evidence.md`.
- The demo is password-gated. The password is provided in Rayls quest materials and is not recorded in this repository.
- This repository is a research archive. It is not a security audit.

## Current audit status

Status as of 15 November 2026. Full detail in `audit/audit-status.md`.

- Demo testing: done for the steps listed above. Send and invite remain untested.
- Docs check: three pages read directly (privacy and auditing, architecture, Enygma Public). The passage the AMA calls outdated has not been found.
- Technical evidence: demo bundle, RPC, explorer, and reference repository checked 15 November 2026. The deployment the 13 November session used is still unknown.
- AMA notes: written from listening notes. No transcript.
- Open conflict: AMA scoped-auditor description vs docs network-wide statement. Unresolved. The Rayls blog and the reference repository's protocol document were added as sources on 15 November 2026; they do not settle it.
- Next steps: complete one shielded send, try the invite flow, identify the deployment a new run uses, capture full transaction hashes.

## Repository structure

```
rayls-enygma-research/
├── README.md
├── research/
│   ├── research-plan.md
│   ├── technical-overview.md
│   └── open-questions.md
├── findings/
│   ├── verified-facts.md
│   ├── official-claims.md
│   ├── observations.md
│   └── unknowns.md
├── demo-testing/
│   ├── test-report.md
│   ├── user-flow.md
│   └── screenshots/
├── ama/
│   └── ama-notes.md
├── technical-evidence/
│   └── technical-evidence.md
├── sources/
│   └── source-register.md
└── audit/
    └── audit-status.md
```

`research/` holds the plan, the technical summary, and the open questions. `findings/` holds the labelled findings, one category per file. `demo-testing/` holds the test report, the user flow, and the screenshots. `ama/` holds the AMA notes. `technical-evidence/` holds the checkable technical evidence: contract addresses, transaction hashes, ABI fragments, the reference implementation, RPC results, and the technical docs. `sources/` holds the source register. `audit/` holds the status of the work.
