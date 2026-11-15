# Source register

Every source used in this research. Status: 15 November 2026. Nothing here is invented. If a URL could not be verified, that is stated.

## Primary sources

| # | Source | What it is | Date | Status |
| --- | --- | --- | --- | --- |
| S1 | `enygma-testnet.rayls.com` | Enygma demo, Rayls Public Chain testnet | Tried 13 Nov 2026 | Live at the time. Password-gated; password not recorded here. |
| S2 | `demo-testing/screenshots/1-fee-register.png` | Screenshot, register-keys fee | 13 Nov 2026 | SHA-256 `25a81a18...e1c0e`. See test report for full hash. |
| S3 | `demo-testing/screenshots/2-fee-shield.png` | Screenshot, shield fee | 13 Nov 2026 | SHA-256 `95a4a1cb...9ffd8`. |
| S4 | `demo-testing/screenshots/3-confirm-onchain.png` | Screenshot, confirm-onchain step | 13 Nov 2026 | SHA-256 `8ef88c03...2f51b`. |
| S5 | `demo-testing/screenshots/4-wallet-akhir.png` | Screenshot, final wallet | 13 Nov 2026 | SHA-256 `5d37b3f8...c484a`. |
| S6 | `demo-testing/screenshots/5-send-48-user.png` | Screenshot, send screen, 48 users | 13 Nov 2026 | SHA-256 `a77696cc...3b295`. |
| S7 | Demo screen recordings (3 files) | Silent recordings of the demo run | 13 Nov 2026 | Transcription returned no speech segments. SHA-256: `38bab4c4daa56f07cdac8d6521ec106aa31baedcf836d2fd9f822b40206183d1`, `3a974582bb81e1226cbc5fd641a4ed74da73e56e0608b172c732ff24e482ed36`, `55629d8f0fa3a3ae7ed7b62623a81c9aebf7557e247dbb9ef134f373beb5edf3`. Source filenames not recorded. |
| S8 | Enygma AMA, Rayls Labs X post 2120881854442065955 | AMA replay, 38 min 43 s | Listened 13 Nov 2026 | Paraphrase notes only. No verbatim transcript exists. A transcript fetch returned a Cloudflare challenge page. Post URL not independently verified; the post ID is as recorded in the research notes. |
| S9 | <https://docs.rayls.com/docs/enygma-privacy-and-auditing> | Docs page, "Who sees what: privacy and oversight" | Read 15 Nov 2026; page updated 11 Nov 2026 | Read directly. Quoted in `findings/verified-facts.md`. |
| S10 | <https://docs.rayls.com/> | Rayls docs home | Noted 13 Nov 2026 | URL as used in the research. Individual pages: S9, S19, S20 read directly. |
| S11 | <https://www.rayls.com/> | Rayls website | Noted 13 Nov 2026 | URL as used in the research. |
| S12 | <https://transparency.rayls.com/> | Rayls Transparency Portal | Noted 13 Nov 2026 | URL as used in the research. Not checked in detail. |

## Secondary sources

| # | Source | What it is | Date | Status |
| --- | --- | --- | --- | --- |
| S13 | <https://www.rayls.com/blog/private-verifiable-and-compliant-what-is-rayls-enigma> | "What is Rayls Enygma?" | Published 2025-07-07, updated 2026-10-27 | Found by search 15 Nov 2026. Used for the official description of Enygma. |
| S14 | <https://www.rayls.com/blog/introducing-rayls-enygma-a-new-era-of-privacy-for-evm-chains> | "Introducing Rayls Enygma" | Published 2025-05-30, updated 2026-11-12 | Found by search 15 Nov 2026. Used for the Auditor View description. |
| S15 | Third-party review, "Who Can See Institutional Payments? Comparing Rayls Enygma and Oasis Sapphire" (Medium), <https://medium.com/@ffddfsdssfssfdfd/who-can-see-institutional-payments-comparing-rayls-enygma-and-oasis-sapphire-8a87350f959a> | Docs review, Oct 2026 | Found by search 15 Nov 2026 | Third-party claims only. Not independently verified. Page not opened — Medium blocked the request (403); title and date are as indexed by search, not confirmed from the page itself. Cited for the Enygma reference repo link and the docs-vs-implementation notes. |
| S16 | Third-party review, "What Does Rayls Enygma Actually Hide? A Look at Its Privacy Boundaries" (Medium), <https://medium.com/@no996865/what-does-rayls-enygma-actually-hide-a-look-at-its-privacy-boundaries-72fe53c3a036> | Docs review, Oct 2026 | Found by search 15 Nov 2026 | Third-party claims only. Not independently verified. Page not opened — Medium blocked the request (403); title and date are as indexed by search, not confirmed from the page itself. |

## Technical evidence (15 November 2026)

| # | Source | What it is | Date | Status |
| --- | --- | --- | --- | --- |
| S19 | <https://docs.rayls.com/docs/rayls-high-level-architecture> | Rayls architecture page, two Enygma editions | Read 15 Nov 2026; page updated 11 Nov 2026 | Read directly. Quoted in `technical-evidence/technical-evidence.md`, item 8. |
| S20 | <https://docs.rayls.com/docs/enygma-public> | Enygma Public docs page | Read 15 Nov 2026; page updated 11 Nov 2026 | Read directly. Quoted in `technical-evidence/technical-evidence.md`, item 8. |
| S21 | <https://www.rayls.com/blog/auditability-without-surveillance-why-mathematical-enforcement-beats-trusting-the-code> | Rayls blog, "Auditability without surveillance" | Read 15 Nov 2026 | Read directly. Quoted in `technical-evidence/technical-evidence.md`, item 9. |
| S22 | `https://enygma-testnet.rayls.com/assets/index-BmNruHc0.js` | Demo client bundle (Vite app) | Fetched 15 Nov 2026 | HTTP 200, 1,338,924 bytes, SHA-256 `c878b635cab69d9c529f4cd9e6fcd8fb606c0e2a9a3bd42af39ea435f065ec81`. Page SHA-256 `b615fd73aa999fb72529d37553ba0943d754e2f2e0f50468a07fe2e8fcb636c5`. |
| S23 | <https://testnet-explorer.rayls.com/api> | Testnet explorer API (`getsourcecode`, `txlist`, `getLogs`, `getblockreward`) | Checked 15 Nov 2026 | Public API. Proxy contracts verified (see `technical-evidence/technical-evidence.md`, item 4). Registry transaction lists retrieved. All logs for the two registries and two vaults retrieved and decoded (item 10); topics decoded with keccak256 of the bundle ABI's event signatures. |
| S24 | <https://testnet-rpc.rayls.com> | Rayls Public Chain testnet RPC | Checked 15 Nov 2026 | Public RPC. `eth_chainId` returned `0x6f5337` (7,295,799). `eth_getCode` returned bytecode for the registry and vault proxies. `eth_getTransactionReceipt` returned null for a mined deployment transaction; see `technical-evidence/technical-evidence.md`, item 3. |
| S25 | `enygma_payments/protocol_description.md` in S17 | Protocol description, including the auditing section | Read 15 Nov 2026 | Section 7 (Auditing) is marked design, not implemented, in the document itself. Quoted in `technical-evidence/technical-evidence.md`, item 7. |
| S17 | <https://github.com/raylsnetwork/Enygma> | Enygma public reference repository | Read 15 Nov 2026, commit `3c61be782cbd31b108eacbda662d3a0a9219f6ae` | Protocol description read; repository structure listed. See `technical-evidence/technical-evidence.md`, item 7. Not a code audit. |
| S18 | <https://explorer.rayls.com> | Rayls Public Chain explorer | Cited in S15 | Checked 15 Nov 2026 via the testnet explorer API. See S23. |

## Related work (out of scope)

| # | Source | What it is |
| --- | --- | --- |
| R1 | <https://github.com/akira01111/rayls-mainnet-block-research> | Separate repository: Rayls mainnet block research (47 transactions in 2,400 blocks). Not part of this Enygma research. |

## Working notes (not sources)

Two article drafts were written from this research on 13 November 2026. They are writing outputs, not evidence, and are not included in this repository. The facts in them come from the sources above.
