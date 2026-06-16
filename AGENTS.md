# Agent instructions — Kickbacks Setup Kit

This repository is a **setup helper** for [Kickbacks.ai](https://kickbacks.ai). Your job is to get the user earning from sponsored spinner ads in Cursor, VS Code, or the Claude Code terminal — safely and completely.

## Start here

1. **Read and execute** [`INSTRUCTIONS.md`](./INSTRUCTIONS.md) from **STEP-001** through completion.
2. **Report** `STEP-xxx: PASS` or `STEP-xxx: FAIL — <reason>` after every ACTION.
3. **Stop at every GATE** until the user replies. Do not skip Google sign-in or payout gates.
4. **Install order:** `anthropic.claude-code` **before** `Kickbacksai.kickbacks-ai`.

## Canonical URLs

| Document | GitHub | Raw (for fetch) |
|----------|--------|-----------------|
| Runbook | [INSTRUCTIONS.md](./INSTRUCTIONS.md) | https://raw.githubusercontent.com/ckryptickunal/kickbacks-setup/main/INSTRUCTIONS.md |
| Human guide | [USER-GUIDE.md](./USER-GUIDE.md) | https://raw.githubusercontent.com/ckryptickunal/kickbacks-setup/main/USER-GUIDE.md |

## Extension IDs

```
Kickbacksai.kickbacks-ai    # Kickbacks — install AFTER Claude Code
anthropic.claude-code       # Claude Code panel
openai.chatgpt              # Codex / ChatGPT panel
```

## Hard boundaries

| You may | You may not |
|---------|-------------|
| Detect OS and editor CLI (`cursor` vs `code`) | Complete Google OAuth in the browser |
| Install extensions via `$EDITOR_CLI --install-extension` | Read the user's code, prompts, or chat |
| Guide reload, sign-in clicks, smoke tests | Edit `webview/index.js` or `~/.claude/settings.json` manually |
| Troubleshoot with Diagnose output | Assume `code` is VS Code (often Cursor on Mac) |

## One-line user prompt

```
Execute INSTRUCTIONS.md from https://github.com/ckryptickunal/kickbacks-setup step by step (STEP-001 onward). Report PASS/FAIL after each ACTION. Stop at every GATE until I reply. Install extensions in order: Claude Code first, then Kickbacks.
```

## Success criteria

Setup is complete when **all** of the following are true:

- [ ] `kickbacksai.kickbacks-ai` installed
- [ ] User signed in (status bar shows `$` amounts)
- [ ] Status is not `Kickbacks incompatible` (or user accepts CLI-only earning)
- [ ] User saw a sponsored line **or** Diagnose reports `compatible: true`
- [ ] User understands preview ads ≠ earnings

Send the **Completion Report** template from INSTRUCTIONS.md § PHASE 8 when done.

## Escalation

- Extension bugs / version mismatch: https://github.com/andrewmccalip/kickbacks.ai/issues
- Doc errors in *this* repo: open an issue on https://github.com/ckryptickunal/kickbacks-setup
