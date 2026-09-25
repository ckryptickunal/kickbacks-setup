# kickbacks-setup: public problem and user-feedback corpus

**Researched:** 2026-09-25. **Repo:** https://github.com/ckryptickunal/kickbacks-setup. **Scope:** Third-party community setup guide for Kickbacks.ai, not the vendor or a product Kunal controls.

**Evidence boundary:** These are problem-space reports about comparable workflows/products, not users of this repository. Some are questions or interested builders rather than verified defects. Follow each original link before using an item for implementation. Relevance is a product hypothesis, not a claim that Kunal’s repo currently behaves this way.

## Source records

### KICKBACKS-SETUP-01
- date: 2026-06-11
- audience: Kickbacks user on Cursor/Claude Code
- evidence: An official-product issue reports a Claude Code version change made a spinner hook incompatible and sign-in did not register.
- source: https://github.com/andrewmccalip/kickbacks.ai/issues/13
- kickbacks-setup relevance: Troubleshooting guidance should check supported versions and refer to vendor fixes, not patch blindly.

### KICKBACKS-SETUP-02
- date: 2026-06-12
- audience: Kickbacks user
- evidence: An official-product issue reports ads stopping after a VS Code message; window reload was described as a workaround.
- source: https://github.com/andrewmccalip/kickbacks.ai/issues/43
- kickbacks-setup relevance: Separate install failures from post-install serving problems; flag vendor-dependent workarounds.

### KICKBACKS-SETUP-03
- date: 2026-06-13
- audience: Kickbacks extension user
- type: GitHub issue
- evidence: The extension sign-in directed a user to Google although the website offered more sign-in methods.
- source: https://github.com/andrewmccalip/kickbacks.ai/issues/78
- kickbacks-setup relevance: Guide should describe actual supported extension sign-in flow and link the vendor issue.

### KICKBACKS-SETUP-04
- date: 2026-06-11
- audience: Kickbacks CLI-only user
- type: GitHub issue
- evidence: A clean Claude/Codex CLI install without IDE extensions could not attach the expected hook, according to issue discussion.
- source: https://github.com/andrewmccalip/kickbacks.ai/issues/5
- kickbacks-setup relevance: Differentiate IDE extension setup from terminal-only support.

### KICKBACKS-SETUP-05
- date: 2026-06-12
- audience: Cursor user
- type: GitHub issue
- evidence: The author asks whether the extension can show in Cursor’s native chat UI.
- source: https://github.com/andrewmccalip/kickbacks.ai/issues/42
- kickbacks-setup relevance: Clarify supported surface and avoid suggesting unsupported placements.

## Assessment and limits

The source sample is narrow. It shows concrete problems worth checking, not a complete market survey or proof of demand for this specific repo. For promising signals, test the current repo against a user scenario and ask actual users before turning it into a roadmap. No private repository content used.
