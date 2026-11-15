# Technical evidence

Checked 15 November 2026. This file records technical evidence that can be checked again: contract addresses, transaction hashes, event and ABI fragments, the reference implementation, RPC calls and their results, and the technical docs pages on shielding, auditor access, and the privacy mechanism.

This file is not a smart-contract audit. It is not a cryptography audit. Reading documentation, reading a client bundle, and calling a public RPC does not audit a contract or a proof system. Where a claim is not supported by the evidence, the file says so.

Each item answers four questions: what was checked, where the code or data came from, what it proves, and what it cannot prove.

## 1. The live chain

### What was checked

The Rayls Public Chain testnet RPC and its chain ID.

### Where it came from

- Public RPC: `https://testnet-rpc.rayls.com` (found in the demo client bundle, see item 2).
- `eth_chainId` returned `0x6f5337` = **7,295,799** decimal.
- `eth_blockNumber` returned `0x16d645b` (about block 23,946,331) at the time of the check, 15 November 2026 14:40 UTC.

### What it proves

- The testnet chain ID is **7,295,799**. A third-party review (October 2026) states "Chain ID: 72957". That figure is wrong. 72957 is a prefix of 7295799, not the chain ID. The correct value is verified two ways: the demo bundle's chain config (`id:7295799`) and the live `eth_chainId` call.
- The public RPC answers read-only calls.

### What it cannot prove

- It does not prove which deployment the demo session of 13 November 2026 used. See item 3.
- `eth_getTransactionReceipt` returned null for a deployment transaction that the explorer lists as mined. The receipt could not be confirmed through this RPC endpoint. The transaction itself was returned by `eth_getTransactionByHash`. See item 3.

## 2. The demo client bundle

### What was checked

The JavaScript bundle served by the demo site, to find the chain config, the RPC and explorer URLs, the relayer URL, the deployed contract addresses, and the registry ABI.

### Where it came from

- Page: `https://enygma-testnet.rayls.com/` (HTTP 200, 3,645 bytes, SHA-256 `b615fd73aa999fb72529d37553ba0943d754e2f2e0f50468a07fe2e8fcb636c5`).
- Bundle: `https://enygma-testnet.rayls.com/assets/index-BmNruHc0.js` (HTTP 200, 1,338,924 bytes, SHA-256 `c878b635cab69d9c529f4cd9e6fcd8fb606c0e2a9a3bd42af39ea435f065ec81`).
- Fetched 15 November 2026 with a plain HTTP client. No sign-in, no password, no session. The bundle is public client code.

### What it proves

- The demo is a Vite-built web app. The chain config in the bundle is `id:7295799, name:'Rayls Testnet'`, RPC `https://testnet-rpc.rayls.com`, explorer `https://testnet-explorer.rayls.com`.
- The relayer URL is configured as `7295799=https://enygma-relayer-aafjr.ondigitalocean.app/rayls` (Sepolia uses the `/sepolia` path on the same host).
- The bundle embeds three deployment configs: Sepolia (`11155111.json`), Rayls testnet (`7295799.json`), and a second Rayls testnet deployment (`br/7295799.json`). The app selects a deployment by region code from the file path, defaulting to `uk` when no region is present.
- The bundle contains the UserRegistry ABI, including the auditor functions and events quoted in item 5.

### What it cannot prove

- The bundle fetched on 15 November 2026 may differ from the bundle served on 13 November 2026, when the demo session happened. Addresses and config from this bundle describe the deployment as of 15 November, not necessarily as of 13 November.
- A 40-hex string in a minified bundle is not automatically a contract address. The bundle also contains ABI-encoded calldata (for example `0x3659cfe6...`, the `upgradeToAndCall` selector followed by an address) and hashes. Only the addresses listed in the deployment configs in item 3 are presented here as contract addresses.

## 3. The deployed contracts

### What was checked

The contract addresses, deployment transaction hashes, block numbers, and auditor address in the bundle's Rayls testnet deployment configs, and their on-chain state through the public RPC and the testnet explorer.

### Where it came from

- The bundle's `7295799.json` deployment (called `yx` below) and `br/7295799.json` deployment (called `bx` below). See item 2 for the bundle.
- RPC `eth_getCode` calls to `https://testnet-rpc.rayls.com`.
- Testnet explorer API `https://testnet-explorer.rayls.com/api` (`getsourcecode`, `txlist`). See item 4.

### What it proves

Main Rayls testnet deployment (`7295799.json`):

| Contract | Address | Deployment tx | Block |
| --- | --- | --- | --- |
| RLS token | `0x07e17E17e17E17e17e17e17E17E17E17E17e17EA` | — | — |
| RlsGasForwarder | `0x753cc3Abe9A1c49536ee74F1f424fCF693AAB5DD` | `0xd6f3a03cc24320a6c050826b2d2973886a10b99d0ca5511ac0dbe01cafccbce3` | 21213648 |
| UserRegistry | `0xA473291FFb33e2276F364fAE169f03c4406719e9` | `0x472504db63c0a47fd71cdb3a1f22caf4510a61ce49d713e42bdadfea70d3f4a9` | 23212003 |
| SharedVaultProxy | `0x9C5Ad5e5Ea5b5910E7fD1E1CC7b70ce0e4bF06c2` | `0xa626fb912862868ebe94747d6d2256e18e3ed7cdd2cf4d2da0ccdf31c7f4c3a7` (recovered from logs; truncated in bundle read) | 21568375 |
| UsdrVault (vaultId 0) | `0x1edb224cf8637f92efadaf47ef9e70c044d75584` | — | 21380502 |
| RlsVault (vaultId 1) | `0x97b5d78dbe06d8c8c843f87b5aa2d8587b890795` | — | 21380517 |
| Verifier | `0xfa3a53ec650bfd4ca3e8461abce243382a1037af` | — | — |
| GenericGroth16Verifier | `0xc12f06f883b757c91069f9d94065a4c673ef356a` | — | — |
| PoseidonT3 / T5 / Wrapper | `0xc29f02220d8aed5c731de4aee9d7d8d24c94ef15` / `0x078c99bbbbf9dcf827ff085c9a4634213b18018b` / `0x0bc72bf5dd894164f7cc8f8b92c78eb7d2156f3f` | — | — |
| OwnerMultisig | `0xBf099175a241194C38E977735D59CCb22596d775` | `0xbc835c92b0b7bb288576ca7191a024316e7392660d298fc8b7791de44d5e23ed` | 21376989 |
| UserRegistryV1 (older) | `0x6Bd39b41f26b0A134869DEa79e3765Ce72363073` | `0x5293595a5469482aabeb9e4e851402b7a6e57ffc89f21a3d349aa6c35c922e7d` | 21376852 |

Second Rayls testnet deployment (`br/7295799.json`):

| Contract | Address | Deployment tx | Block |
| --- | --- | --- | --- |
| RlsGasForwarder | `0x2ef592329B8e01320170f8f8d759d9bcA94d1066` | `0x80ef114fc95879b7b6173917161938de39d0ae9e5704b64d65cd4613ce7cd940` | 22210853 |
| UserRegistry | `0x3E9435c1fe8432e21E80D7A8ab81EBfc8eC708E3` | `0xe3f0804da70964423a63dc95ca3f9bf888cdec80568699a74b59524c4694df8d` | 22210868 |
| UserRegistryImplementation | `0xB23124D2eE339d1E8175B9ec10D20217CE015c1C` | `0xebd30c62ae27fa071acd1f1409564b8c0c7c079dda3b34b7a81811b44941469e` | 23395961 |
| SharedVaultProxy | `0x94dafa3bf372cad68143ac535f845e74751d75ef` | — | — |
| TokenFactory | `0x7416094FFC5A1D0C2659DA0D5b81CeCc18f1BdAc` | `0x8d5ff0af2b75100b08575db862eae1f6a42e8d0c3d8dc00c503ac652d5b7b07c` | 22210874 |

The SharedVault (yx) deployment block 21568375 was verified from the transaction record, not inferred from the first log block. `eth_getTransactionByHash` for `0xa626fb91...` returns blockNumber `0x1491b77` (= 21568375) with `to` null (a contract-creation transaction) from the deployer `0xa5f0c684eb...`, and the explorer's transaction record (Blockscout v2, 15 November 2026) confirms block 21568375, status success, and `created_contract` `0x9C5Ad5e5Ea5b5910E7fD1E1CC7b70ce0e4bF06c2` — the SharedVault address. The explorer's receipt-status endpoint also returns status `1` (success). The testnet RPC returns null for `eth_getTransactionReceipt`, so the receipt itself was not read from the RPC; the block and the created contract are confirmed by the transaction record and the explorer.

The auditor address is the same in every deployment in the bundle (Sepolia, `7295799.json`, `br/7295799.json`):

- Auditor: `0x71AF09966CBED4434ccA97c40Fa38B8083548B95`. `eth_getCode` returned `0x`, so it holds no contract code. It is an account, not a contract.
- The `7295799.json` registry also records `auditorPublicKeyHash: 0x4151c50e9250f5818a53f9e48e734bd4209407d19f966ede4f7988dd4af863e5`.

`eth_getCode` on the testnet RPC returned non-empty bytecode for the registry and vault proxies (`0xA47329...`, `0x3E9435...`, `0x9C5Ad5...`, `0x94dafa...`) and for the RlsGasForwarder (`0x753cc3...`). All five return code starting with the standard Solidity preamble (`0x6080604052...`). The four proxies' code contains the EIP-1967 implementation slot constant; the gas forwarder's code does not. The RLS token address (`0x07e17E...`) was not checked with `eth_getCode` during the 15 November research. Checked on 15 November 2026 at 22:25 WIB, it returns 122 bytes of code containing the EIP-1967 slot, so the token itself is a proxy; its implementation was not checked. The second deployment's gas forwarder (`0x2ef592...`, `br/7295799.json`) was also checked on 15 November 2026 at 22:25 WIB: 4,394 bytes, no EIP-1967 slot.

The explorer `txlist` for the two registries shows only deployment and upgrade calls, from the deployer accounts only:

- `0xA47329...`: 7 transactions in the `txlist`, all on 10 November 2026 13:57:50–13:58:53 UTC, blocks 23212003–23212110, senders `0x08fbf5b9c2...` and `0xa5f0c684eb...`. The first is the deployment transaction, block 23212003, matching the bundle.
- `0x3E9435...`: 3 transactions in the `txlist`, all on 3 November 2026 12:32:40–12:36:33 UTC, blocks 22210868–22211254, sender `0xa5f0c684eb...`. The first is the deployment transaction, block 22210868, matching the bundle.

The `txlist` only lists transactions whose `to` field is the contract. The event logs tell a different story (see item 10): the `0xA47329...` registry emitted 143 logs across 76 transactions, and the `0x9C5Ad5...` vault emitted 803 logs across 204 transactions. Most interactions with these contracts arrive through calls from other contracts (for example the relayer and the gas forwarder), so they do not appear in the contract's `txlist` but do emit logs under the contract's address. One sample transaction was checked directly: `0xe2d442f5550172fa` has `to` equal to the registry itself and `from` the deployer `0x08fbf5b9c2...`, so it is one of the direct owner transactions.

The `7295799.json` deployment object in the bundle carries `retired: 2026-11-10`.

### What it cannot prove

- **Which deployment the 13 November 2026 demo session used is unknown, and the session's registration was not found.** The `0xA47329...` registry was active on 13 November: its logs run from 10 November 2026 13:57:50 UTC to 13 November 2026 22:05:57 UTC, with 63 `UserRegistered` and 63 `UsernameSet` events. The 63 usernames were decoded from the logs (see item 10). The demo username `@kittyrim` is not among them. No registered address matches the demo's truncated EVM address (`0x86800...00FC`, from screenshot 4). The `0x3E9435...` registry has no registrations at all. So the registration of `@kittyrim` on 13 November does not appear in either embedded registry. Possible reasons include a deployment that has since been replaced, or a bundle that changed between 13 and 15 November. None of these is established.
- The deployment transaction hashes in the tables are copied from the bundle's deployment record. Only the two registry deployment hashes were cross-checked against the explorer txlist (block numbers match). The others were not individually verified on-chain. The SharedVault deployment hash was truncated in the bundle read, but the full hash was recovered from the vault's own logs: `0xa626fb912862868ebe94747d6d2256e18e3ed7cdd2cf4d2da0ccdf31c7f4c3a7`, block 21568375. It matches the truncated bundle value.
- USDr is listed in the bundle at `0x0000000000000000000000000000000000000400`, a precompile address, not a normal contract address. Its on-chain nature was not checked beyond the bundle entry.

## 4. Contract source verification (explorer)

### What was checked

Whether the deployed proxy contracts have verified source code on the testnet explorer, and what that source is.

### Where it came from

- Testnet explorer API: `https://testnet-explorer.rayls.com/api?module=contract&action=getsourcecode&address=<address>`, checked 15 November 2026.

### What it proves

All four proxy addresses return verified source with the same compiler, `v0.8.28+commit.7893614a`:

| Address | ContractName | Source |
| --- | --- | --- |
| `0x9C5Ad5...` | SharedVaultProxy | `project/src/SharedVaultProxy.sol`, SSPL-1.0, 566 bytes |
| `0x94dafa...` | SharedVaultProxy | Same |
| `0xA47329...` | UserRegistryProxy | `project/src/UserRegistryProxy.sol`, SSPL-1.0, 557 bytes |
| `0x3E9435...` | UserRegistryProxy | Same |

The SharedVaultProxy source, in full (file `project/src/SharedVaultProxy.sol`):

```solidity
// SPDX-License-Identifier: SSPL-1.0
pragma solidity 0.8.28;

import {ERC1967Proxy} from "@openzeppelin/contracts/proxy/ERC1967/ERC1967Proxy.sol";

// SharedVaultProxy is the shared vault's address: it keeps the vault's tree, notes and tokens and delegates every call
// to the current SharedVault implementation, which the vault's owner replaces (SharedVault.upgradeTo). `data` is the
// implementation's initialize call.
contract SharedVaultProxy is ERC1967Proxy {
    constructor(address implementation, bytes memory data) ERC1967Proxy(implementation, data) {}
}
```

The comment in the source is the reason this snippet is quoted: it states the proxy keeps the vault's tree, notes and tokens and delegates every call to the current implementation, which the owner replaces.

### What it cannot prove

- Verifying a proxy's source proves the proxy code, not the implementation behind it. The implementation addresses are in the bundle (for example the `br` UserRegistryImplementation `0xB23124D2...`), but their source verification was not checked in this research.
- The proxy ABI returned by the explorer is 804 characters. It is the proxy's own interface, not the vault or registry logic. The full registry and vault ABIs are in the demo bundle (see item 5), not from the explorer.
- The UserRegistryProxy source was not quoted in full here because it is the same ERC1967Proxy pattern as the SharedVaultProxy above, with the contract name changed. The explorer returns it under `project/src/UserRegistryProxy.sol`.

## 5. The registry ABI: the auditor role in the deployed code

### What was checked

The auditor-related functions, events, and errors in the UserRegistry ABI embedded in the demo bundle.

### Where it came from

- The demo bundle, item 2. The ABI is embedded as JSON in the client code. No line numbers exist in a minified bundle, so locations are given as the ABI entry names.

### What it proves

The UserRegistry ABI embedded in the demo client bundle exposes auditor-related functions and events. Exact ABI fragments from the bundle:

```json
{"inputs":[{"internalType":"address","name":"account","type":"address"}],"name":"addAuditor","outputs":[],"stateMutability":"nonpayable","type":"function"}
```

```json
{"inputs":[],"name":"auditorPublicKey","outputs":[{"internalType":"bytes","name":"","type":"bytes"}],"stateMutability":"view","type":"function"}
```

```json
{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"account","type":"address"},{"indexed":true,"internalType":"address","name":"by","type":"address"}],"name":"AuditorAdded","type":"event"}
```

```json
{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"account","type":"address"},{"indexed":true,"internalType":"address","name":"by","type":"address"}],"name":"AuditorKeyGiven","type":"event"}
```

```json
{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"account","type":"address"}],"name":"AuditorPersonalKeySet","type":"event"}
```

Errors in the same ABI: `AlreadyAuditor`, `NoAuditor`, `NotAuditor`, `NotOwner`, `InvalidUsername`. Other functions in the ABI include `getAuditorAccounts`.

These entries show that the ABI in the bundle models auditors as accounts that can be added, stores an auditor public key, and defines events for an auditor being added, an auditor key being given, and an auditor personal key being set. The ABI alone does not prove the deployed implementation matches it; the on-chain logs in item 10 are the separate evidence that the deployed registry emitted these events.

### What it cannot prove

- It does not prove the auditor's access is scoped. Nothing in these ABI entries describes scoping by account, time window, or transaction. The ABI shows that auditors exist and can be added. It does not show what an auditor can or cannot read.
- It does not prove the demo session used this ABI. The bundle is from 15 November 2026; the demo session was 13 November 2026.
- Event logs for these events were retrieved and decoded (see item 10). On the `0xA47329...` registry, `AuditorAdded` was emitted 7 times, `AuditorKeyGiven` 4 times, and `AuditorPersonalKeySet` once. The first auditor added was the bundle's auditor address `0x71AF09966CBED4434ccA97c40Fa38B8083548B95`, and it later added four more auditor accounts itself. Only four of the seven added accounts have an `AuditorKeyGiven` event (`0x71AF09...`, `0x3bffb10f...`, `0xd04004a3...`, `0x23c5a513...`); the other three (`0x67359d4e...`, `0x7dd26477...`, `0xf52b7eba...`) have no key event in the logs (see item 10). The events prove auditors were added on-chain. They do not prove what any auditor can read.

## 6. The relayer

### What was checked

Where the demo sends its transactions.

### Where it came from

- The demo bundle's environment config: `VITE_RELAYER_URL`, `7295799=https://enygma-relayer-aafjr.ondigitalocean.app/rayls`.

### What it proves

- The demo submits transactions through a relayer hosted at `enygma-relayer-aafjr.ondigitalocean.app`, path `/rayls` for the testnet chain. This matches the docs, which state a relayer submits every Enygma Public transaction and runs the testnet faucet.

### What it cannot prove

- No request to the relayer was made in this research. Its behaviour, its logs, and what it records about a transaction were not checked.

## 7. The reference implementation (public repository)

### What was checked

The public Enygma reference repository: its structure, its protocol description, and what it says about auditing.

### Where it came from

- Repository: `https://github.com/raylsnetwork/Enygma`, commit `3c61be782cbd31b108eacbda662d3a0a9219f6ae`, read 15 November 2026 through the GitHub API.
- Key file: `enygma_payments/protocol_description.md` (37,302 bytes).
- The repository also contains `enygma_payments/contracts/enygma/` (Solidity source, Hardhat config), `enygma_demo/` (a demo app, including a 906,995-byte `index.html` and a README), `enygma_gnark_shared/`, `enygma_dvp/`, `enygma_dvp_auctions/`, `enygma_retail_payments/`, `docs/`, `scripts/`, and `source_of_true.md`.

### What it proves

The protocol description states its own status at the top of the document (file `enygma_payments/protocol_description.md`, lines 3–24):

> Sections 6's ciphertext payload (AES-GCM-256 encryption, HKDF-based per-block key rotation) and all of Section 7 (**Auditing**, in its entirety — long-term view-key sharing, ephemeral view-key sharing, and universal auditing) are **design, not implemented**: there is no AES-GCM/HKDF code anywhere in this repository outside this document, no "store encrypted payload" step, no tag-scanning retrieval path, and no auditor role, address, escrow, or event of any kind. Everything through Section 5 (**System Setup** — **Key Generation** — **Key Registration** — **Key Agreement** — **Issuing Tokens**) and the core of Section 6 (commitments, nullifiers, the ZK proof, and on-chain verification) matches the shipped code.

The same notice states, about scoped auditing in that construction:

> even if built, this specific construction could not deliver *scoped* auditing as written — the value that opens a transaction is a Pedersen blinding shared jointly by both parties, and the epoch anchor means one disclosure opens every transaction between that pair for the whole epoch window in both directions, so the only auditing mode this design can actually support is permanent and universal, not per-transaction and revocable.

Section 7 itself (file `enygma_payments/protocol_description.md`, lines 497–594) opens with:

> **Design, not implemented (Fix M-12).** No auditor role, address, escrow, key-sharing mechanism, or event exists anywhere in `enygma_payments` today — this entire section describes design intent only.

The protocol uses BN254, Pedersen commitments, Groth16 zero-knowledge proofs (which need a trusted setup), nullifiers against double-spending, and an anonymity set `k` (file `enygma_payments/protocol_description.md`, Notation section, lines 63–79).

### What it cannot prove

- This repository is the institutional payments protocol (`enygma_payments`). It is not the Enygma Public demo's contracts. Nothing in this research establishes that the deployed vault and registry contracts on the testnet are built from this code. The deployed proxies are verified on the explorer as ERC1967 proxies (item 4); their implementations were not compared against this repository.
- The "scoped auditing is impossible in this construction" statement is about this specific construction. It does not prove anything about the Enygma Public deployment's auditor model, which is a different implementation.
- The `enygma_demo/` directory in the repository was not compared against the live demo site. Whether the live demo is built from it is unknown.

## 8. Technical docs: how Enygma Public works

### What was checked

The docs pages that describe the two Enygma editions, the Public deployment's components, and what each party sees.

### Where it came from

- Rayls architecture page: `https://docs.rayls.com/docs/rayls-high-level-architecture`, updated 2026-11-11T21:37:02Z, read 15 November 2026.
- Enygma Public page: `https://docs.rayls.com/docs/enygma-public`, updated 2026-11-11T21:36:24Z, read 15 November 2026.
- Privacy and auditing page: `https://docs.rayls.com/docs/enygma-privacy-and-auditing`, updated 2026-11-11T15:26:41Z, read 15 November 2026 (already recorded in `findings/verified-facts.md`).

### What it proves

From the architecture page, verbatim in substance:

- Enygma comes in two editions: Enygma Sovereign (Private Network) and Enygma Public (Public Chain testnet). Both use Groth16 zero-knowledge proofs and ML-KEM-768 encryption. In both, one designated party can read every transaction: the Private Network operator in Enygma Sovereign, and the deployment's auditor in Enygma Public.
- In Enygma Public, keys come from a passkey, proofs are made in the browser (WebAssembly, "in a few seconds"), notes live in a vault contract as commitments in a Merkle tree, spending a note publishes its nullifier, and the registry holds each account's public keys, username, and view key encrypted to the deployment's auditor.
- A relayer submits every transaction and charges gas in RLS, from public RLS through an ERC-2771 gas forwarder or from shielded RLS. A shielded send shows only that a send happened, the relayer, and its gas fee.
- The notes and escrowed view keys are encrypted with ML-KEM-768. The zero-knowledge proofs, passkeys, and signatures are not post-quantum.
- Each Enygma Public fee includes a 15% commission to the Rayls Foundation.

From the Enygma Public page:

- The deployment's components are: Wallet (browser), Vault contracts, Registry, Verifier, Gas forwarder, Relayer (run by Rayls, runs the testnet faucet), Owner multisig, Auditor view.
- "An Enygma Public deployment is one set of these contracts with one auditor key. A deployment can be set up per country, so that each auditor reads only its own country's activity. An account registers separately in each deployment it uses. The testnet site runs one deployment, and Rayls is its auditor."
- "When an account registers, a copy of its view key is encrypted to the deployment's auditor, so the auditor can read every shielded payment: shielded from the public, not from the auditor. The auditor can read, but it can't freeze or move funds."

### What it cannot prove

- The docs describe the design. They do not prove the deployed contracts behave this way. The registry ABI (item 5) confirms an auditor role exists; it does not confirm the auditor reads every payment, and it does not describe scoping.
- The "one auditor key per deployment" statement sits next to the bundle's evidence of two Rayls testnet deployments (`7295799.json` and `br/7295799.json`). Whether "the testnet site runs one deployment" means one of these, and which one, is not established by the docs. See item 3.
- The privacy and auditing page describes Private Networks, not the Public Chain demo. Its "no scoped view keys" statement is recorded in `findings/verified-facts.md` and remains in conflict with the AMA and the blog (item 9).

## 9. The Rayls blog on auditability

### What was checked

Rayls' own blog post describing the Enygma audit model.

### Where it came from

- `https://www.rayls.com/blog/auditability-without-surveillance-why-mathematical-enforcement-beats-trusting-the-code`, read 15 November 2026.

### What it proves

The blog describes "mathematical enforcement" as the Enygma model: the cryptographic construction supports keys scoped to particular subsets of data, and the boundary is a mathematical constraint, not an administrator's configuration. Its examples: a regulator given a viewing key scoped to a specific bank's transactions over a specific time window; a counterparty bank given a viewing key scoped to a specific bilateral relationship; an internal compliance function scoped to AML analysis; a tax authority scoped to settlement events. It lists six required properties, including selective disclosure, scoped access, separation of visibility from authority, verifiability of correctness, revocability, and durability, and states that mathematical enforcement "by construction, delivers all six".

### What it cannot prove

- The blog is a statement of the model, not a measurement of the deployed system. It does not name a deployment, a contract, or a version.
- It conflicts with the docs page that states there are no scoped view keys and audit access is network-wide, and with the reference implementation's own note that scoped auditing is impossible in that construction (item 7). The conflict is recorded as unresolved in `findings/unknowns.md`. The blog does not resolve it. It adds a third official source on the scoped side, next to the AMA.

## 10. Event logs (retrieved and decoded)

### What was checked

All event logs emitted by the two embedded registries and the two embedded SharedVaults, from the first block to the latest block, through the testnet explorer API (`module=logs&action=getLogs`). The event topics were decoded by computing keccak256 of the event signatures in the demo bundle's ABI (keccak256 implemented locally in Python; verified against the known `Upgraded(address)` topic `0xbc7cd75a20ee27fd...`).

### Where it came from

- Explorer API, 15 November 2026: `https://testnet-explorer.rayls.com/api?module=logs&action=getLogs&address=<address>&fromBlock=0&toBlock=latest`.
- Block timestamps for the first and last log blocks, from the same explorer API (`module=block&action=getblockreward`).

### What it proves

Log counts per contract (all blocks, retrieved 15 November 2026):

| Contract | Logs | Transactions | Block range | Date range |
| --- | --- | --- | --- | --- |
| Registry `0xA47329...` (yx) | 143 | 76 | 23212003–23697459 | 10 Nov 2026 13:57:50 UTC – 13 Nov 2026 22:05:57 UTC |
| Registry `0x3E9435...` (bx) | 4 | 3 | 22210868–22211254 | 3 Nov 2026 |
| SharedVault `0x9C5Ad5...` (yx) | 803 | 204 | 21568375–23946566 | — 15 Nov 2026 14:41:04 UTC |
| SharedVault `0x94dafa...` (bx) | 10 | 6 | 22211086–22211236 | 3 Nov 2026 |

Decoded events, by count, across all four contracts:

| Event | Count | What it means |
| --- | --- | --- |
| `Commitment(uint256,uint256)` | 334 | A shielded note commitment was published (vault). |
| `EncryptedNote(uint256,uint256,bytes,bytes)` | 321 | An encrypted note was stored (vault). |
| `Nullifier(uint256,uint256,uint256)` | 107 | A note was spent, i.e. a shielded send or withdrawal happened (vault). |
| `UserRegistered(address,uint256,bytes,bytes,bytes)` | 63 | An account registered (registry). |
| `UsernameSet(address,string)` | 63 | A username was set for an account (registry). |
| `PartialWithdrawal(uint256,address,uint256,uint256)` | 13 | Part of a note was withdrawn (vault). |
| `PaidOut(uint256,address,address,uint256)` | 13 | A payout was made (vault). |
| `RoleGranted(bytes32,address,address)` | 11 | A role was granted. |
| `Upgraded(address)` | 7 | A proxy's implementation was upgraded. |
| `AuditorAdded(address,address)` | 7 | An auditor account was added (registry). |
| `Initialized(uint8)` | 5 | A proxy was initialised. |
| `CoinLocked(uint256,uint256,uint256)` | 5 | Coins were locked (vault). |
| `AuditorKeyGiven(address,address)` | 4 | An auditor key was given (registry). |
| `ImportClosed()` | 2 | An import was closed. |
| `OwnershipTransferred(address,address)` | 2 | Contract ownership moved. |
| `RoleRevoked(bytes32,address,address)` | 2 | A role was revoked. |
| `AuditorPersonalKeySet(address)` | 1 | An auditor personal key was set (registry). |

The auditor events, decoded, on the `0xA47329...` registry:

- `AuditorAdded`, 7 times. The first three were added by the deployer `0x08fbf5b9c2...` on 10 November 2026: the bundle's auditor `0x71AF09966CBED4434ccA97c40Fa38B8083548B95` (tx `0xf1b398d51a3d5f507c1fa13016361b499fefabd37e0777697e82bc60a4ca53dd`, block 23212015), `0x3bffb10f6f17f15164fbc0416f1bc42c56b2c191` (tx `0x0ef89d3739e3a24a15daf14377fc46bfea48d36e48a86213603d027e3d4d635e`, block 23212021), and `0xd04004a3715f8428674a01ffde2069c181d4b0fd` (tx `0xe2d442f5550172fa1b4235b7e6f84afeaaa951ffceea55a053feed942b23c428`, block 23212029). The other four were added by `0x71AF09...` itself: `0x23c5a5138ad66ff376a7a20248ec47a64d7b3fc9` (tx `0xc6261618d2cc6dd250f9b30504f27a16a0378e16b2a4e927f13a933e2eca1aef`, block 23222870), `0x67359d4ed15116fc5d15c96d0f0b049bae34688f` (tx `0x61874cfb2277bd640ae20e8ed08bafb68449c08f6484a7377c3ca3f16a9833d6`, block 23225307), `0x7dd26477c7f86a1d4cdfaeb73741577def7905ef` (tx `0xa90caaf3cdc40a5c5f0b6a52bdf2a4fc8887a62d7418a0b0c62d8ae222480073`, block 23225360), and `0xf52b7eba863ee3378cc9dd60efd62df1bb08f567` (tx `0x8075169c584b0b616874fa91513f017fd45fe7eae30e5a1568825a803c6f6dc9`, block 23225410).
- `AuditorKeyGiven`, 4 times: to `0x71AF09...`, `0x3bffb10f...`, `0xd04004a3...`, and `0x23c5a513...`.
- `AuditorPersonalKeySet`, once: for `0x23c5a513...` (tx `0x787bbe3cd3369aa325fdfbebf8b41e7554270c8867ca82505acd5f1e0edaf9a5`, block 23223818).

The 63 usernames were decoded from the `UsernameSet` log data on the `0xA47329...` registry. The first is `rayls-relayer` (the relayer's own account). The list includes test names (`aj`, `user_a`, `testing678`, `testingagain`) and real-looking names, including `anara`, `metalawyer`, `jerome66`, and `kittynim`. The demo username `@kittyrim` is not among the 63. No registered address matches the demo's truncated EVM address (`0x86800...00FC`, screenshot 4).

The yx SharedVault was active through the latest block checked: its last log is at block 23946566, 15 November 2026 14:41:04 UTC. The yx registry's last log is at block 23697459, 13 November 2026 22:05:57 UTC. The bx registry and vault have only their deployment and a few setup logs, all on 3 November 2026.

### What it cannot prove

- The vault events prove shielded activity happened (334 commitments, 321 encrypted notes, 107 nullifiers spent). They do not prove the demo session's own shield of 21.4 RLS is among them: vault events carry note commitments and hashes, not usernames, and the demo did not record its note data. No vault event was linked to the demo session.
- The logs show 63 registration events from 63 accounts on the yx registry. They do not prove those accounts belong to real people: the decoded usernames include test names (`testingagain`, `user_a`, `aj`) and the relayer's own account (`rayls-relayer`). They do not prove the demo session used this registry: `@kittyrim` is absent from the decoded usernames.
- The auditor events prove seven auditor accounts were added on-chain, but only four of them have an `AuditorKeyGiven` event (`0x71AF09...`, `0x3bffb10f...`, `0xd04004a3...`, `0x23c5a513...`). The other three (`0x67359d4e...`, `0x7dd26477...`, `0xf52b7eba...`) have no key event in the logs, so nothing here shows they received a key. They do not prove what any auditor can read: the `AuditorAdded` event carries only the account address and who added it, and even an `AuditorKeyGiven` event carries only the account address and who gave the key. Neither event proves what the key unlocks or that the account can read shielded transactions.
- The start date of the yx vault's logs was not established: only the last block's timestamp (15 November 2026 14:41:04 UTC) was fetched. The vault's first log block is 21568375; its date is not recorded here.

## 11. What was not found

Each item below is UNKNOWN, with the reason verification is blocked.

### 11.1 Full transaction hashes for the demo session

Not available. The only hash seen during the demo was a truncated display in screenshot 3 (`0xa8532?10..3caf5cee`). No full hash was recorded. The two registries embedded in the bundle were checked in full (item 10): the yx registry has 63 registrations, but `@kittyrim` is not among them, and no registered address matches the demo's truncated EVM address. The bx registry has no registrations at all. The demo session's transactions cannot be looked up on-chain from this research. Blocked by: the demo UI truncating hashes, and the deployed registry that the session used not being identified.

### 11.2 Event logs for the demo session

Retrieved for the embedded contracts (item 10), but the session's own events were not identified. The vault logs prove shielded activity (334 commitments, 107 nullifiers spent), but no vault event can be linked to the demo session's shield of 21.4 RLS, because vault events carry note commitments, not usernames, and the demo did not record its note data. Blocked by: the demo session's note data not being recorded.

### 11.3 Implementation contract source and its match to the public repo

Not checked. The proxies are verified (item 4). Their implementation contracts were not checked for verified source, and no implementation was compared against the public Enygma repository (item 7). Blocked by: time and scope, not by access. The implementation addresses are in the bundle and the explorer API is public, so this can be checked later.

### 11.4 The demo's proof generation

Not checked. The docs state proofs are made in the browser with WebAssembly in a few seconds, and the AMA states about 2.2 seconds. No proof was captured, timed independently, or verified against a verifier contract in this research. Blocked by: no proof data was recorded during the demo session.

### 11.5 The on-chain fee and commission split

Not verified on-chain. The 15% commission is verified from the demo UI and stated in the docs. No on-chain transaction was traced to confirm the commission is collected as described, or how the relayer's gas charge is split. Blocked by: the demo session's transactions not being located (item 11.1).

### 11.6 Whether the deployed code matches the public repository

Unknown. The deployed contracts are upgradeable proxies whose implementations were not compared to the public repo. The public repo's own protocol document states its auditing section is design, not implemented. No claim is made here that the deployed system implements, or fails to implement, any part of that document.

## 12. How to repeat these checks

- Chain ID: `curl -s -X POST https://testnet-rpc.rayls.com -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","id":1,"method":"eth_chainId","params":[]}'` — expect `0x6f5337`.
- Contract code: same endpoint, method `eth_getCode`, params `["<address>","latest"]`.
- Verified source: `https://testnet-explorer.rayls.com/api?module=contract&action=getsourcecode&address=<address>`.
- Transaction list: `https://testnet-explorer.rayls.com/api?module=account&action=txlist&address=<address>&page=1&offset=100&sort=asc`.
- Event logs: `https://testnet-explorer.rayls.com/api?module=logs&action=getLogs&address=<address>&fromBlock=0&toBlock=latest`. Decode topics with keccak256 of the event signatures from the bundle's ABI; the `UsernameSet` string is ABI-encoded in the log `data` field.
- Block timestamp: `https://testnet-explorer.rayls.com/api?module=block&action=getblockreward&blockno=<block>`.
- Demo bundle: `https://enygma-testnet.rayls.com/assets/index-BmNruHc0.js` (the hash in the filename may change when the site is rebuilt; fetch the page first and read the current script path).
- Reference repository: `https://github.com/raylsnetwork/Enygma`, file `enygma_payments/protocol_description.md`, commit `3c61be782cbd31b108eacbda662d3a0a9219f6ae`.
- Docs: `https://docs.rayls.com/docs/rayls-high-level-architecture`, `https://docs.rayls.com/docs/enygma-public`, `https://docs.rayls.com/docs/enygma-privacy-and-auditing`.
- Blog: `https://www.rayls.com/blog/auditability-without-surveillance-why-mathematical-enforcement-beats-trusting-the-code`.
