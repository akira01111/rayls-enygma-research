# Observations

Things seen or experienced during the demo session, 13 November 2026. Observations are not claims about the system. They describe what the interface showed and how it behaved.

## What worked well

**OBSERVATION.** Sign-up was smooth. The username check is instant. The passkey setup through Google Password Manager just worked.

**OBSERVATION.** The public faucet is the easiest step. One click and the test tokens arrive. The shielded faucet is the same: one click, no passkey, straight into the shielded balance — amounts reconstructed from the final wallet; see `demo-testing/test-report.md`.

**OBSERVATION.** The step-by-step checklist makes it clear where the user is in each action. The tooltips explain what is happening.

## What was confusing

**OBSERVATION.** The fee changed between screens, twice. Register showed about 8.004 RLS and confirmed at 7.1932 RLS. Shield showed about 4.14 RLS and confirmed at 3.5814 RLS. Both confirmed fees were lower than the shown estimates. Nothing was overcharged. The problem is that a user deciding whether to confirm is deciding on a number that then moves.

**OBSERVATION.** One shield action asked for the passkey/PIN twice. It felt repetitive for a single action.

**OBSERVATION.** The confirm-onchain step took about 15 seconds with only a spinner. There was no progress detail and no indication of what was happening. It was not clear whether the step was stuck.

**OBSERVATION.** A recovery PIN was required right after the passkey. That step was not expected.

## What the interface shows

**OBSERVATION.** The wallet screen shows public and shielded balances side by side, with separate totals. It also shows an EVM address, an Enygma Spend address, and an Enygma View address, all truncated by the UI. The full values were not recorded.

**OBSERVATION.** The send screen has a Shielded/Public toggle, a token selector, a recipient field ("@username or 0x..."), and a list headed "Registered with Enygma (48)".

**OBSERVATION.** The wallet screen shows four actions: Send, Receive, Faucet, Invite. Three tabs: Assets, Invites, Activity.

**OBSERVATION.** Each fee breakdown shows the gas portion and the Rayls Foundation commission portion separately, with the commission labelled 15%.

## What was not observed

**OBSERVATION.** No shielded send was completed, so no send confirmation screen, no send receipt, and no post-send balance change was observed.

**OBSERVATION.** The invite screen was not opened. Nothing about the invite flow was observed beyond the button on the wallet screen.
