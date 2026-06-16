# Kickbacks.ai — Frequently Asked Questions

Answers to the questions people search for when setting up **Kickbacks** in **Cursor**, **VS Code**, or the **Claude Code terminal**.

→ **Setup guides:** [USER-GUIDE.md](../USER-GUIDE.md) · [INSTRUCTIONS.md](../INSTRUCTIONS.md) · [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)

---

## Getting started

### What is Kickbacks.ai?

Kickbacks is a free VS Code extension that replaces the “thinking…” spinner in **Claude Code** and **Codex** with a tiny sponsored message. You earn up to **50% of ad revenue** on impressions and clicks while your AI assistant works.

### How do I install Kickbacks in Cursor?

1. Install **Claude Code** extension first (Extensions → search “Claude Code”)
2. Install **Kickbacks.ai** (Extensions → search “Kickbacks”)
3. Reload window (`Cmd/Ctrl+Shift+P` → Developer: Reload Window)
4. Click **Kickbacks: Sign in** in the status bar → Google sign-in

Full steps: [USER-GUIDE.md](../USER-GUIDE.md)

### How do I install Kickbacks in VS Code?

Same steps as Cursor. Search Extensions for Claude Code, then Kickbacks. Works on local VS Code, Remote-SSH, and devcontainers.

### What do I need before installing?

- **Cursor** or **VS Code**
- **Claude Code** and/or **Codex** (ChatGPT extension) — something must show the spinner
- A **Google account** for sign-in and payouts
- **Internet connection**

### Why install Claude Code before Kickbacks?

Install order prevents `Kickbacks incompatible` and missing sign-in commands. Documented in [GitHub issue #13](https://github.com/andrewmccalip/kickbacks.ai/issues/13). Always: **Claude Code → Kickbacks → Reload Window**.

---

## Earnings & payouts

### How much can I earn?

You receive up to **50% of ad revenue**. Clicks pay roughly **50×** more than impressions. Actual amounts depend on advertiser bids and how much you use Claude/Codex.

### Do preview ads count before I sign in?

**No.** You may see real sponsored lines before sign-in — that's a live preview. **Earnings start only after Google sign-in.**

### Where do I see my balance?

In the editor **status bar** (`Kickbacks ($X today · $Y)`) and on the [kickbacks.ai](https://kickbacks.ai) dashboard.

### How do I get paid?

1. Sign in with Google in the extension
2. Visit [kickbacks.ai](https://kickbacks.ai) with the **same Google account**
3. Complete payout setup when prompted

### What are hourly and daily caps?

Kickbacks may limit earnings per hour/day. When capped, a red pill appears (`Hourly cap` / `Daily cap`). **Ads still show** — earning pauses until the timer resets.

---

## Privacy & safety

### Does Kickbacks read my code?

**No.** Kickbacks never reads your files, prompts, completions, or chat content. It only modifies spinner and status display text.

### What data does Kickbacks send?

Per the [marketplace listing](https://marketplace.visualstudio.com/items?itemName=Kickbacksai.kickbacks-ai):

- Anonymous device ID (until sign-in)
- Ad impression and click events
- Google email **after** sign-in (for earnings credit)

All communication goes to **kickbacks.ai** only.

### Can I fully remove Kickbacks?

Yes. Run **Kickbacks: Restore Claude Code** from the command palette, then uninstall the extension. Original Claude Code files are restored byte-for-byte.

### Does Kickbacks slow down Claude or Codex?

No meaningful impact. Only display text changes during wait states.

---

## Cursor, VS Code & terminal

### Does Kickbacks work in Cursor?

**Yes.** Kickbacks officially supports Cursor the same as VS Code.

### I only use Claude in Terminal — do I still need the editor extension?

**Yes.** Kickbacks locates Claude Code by scanning editor extension folders (`~/.cursor/extensions`, `~/.vscode/extensions`). Install Claude Code + Kickbacks in the editor, sign in from the status bar, then use `claude` in Terminal normally.

### What's the difference between panel ads and terminal ads?

| Surface | Where | Requirement |
|---------|-------|-------------|
| Panel spinner | Claude Code / Codex sidebar | Compatible extension build |
| Terminal status line | `claude` CLI | Any Claude Code version |
| Terminal spinner verb | `claude` CLI | Claude Code **2.1.143+** |

### My Mac `code` command installs fail — why?

On many Macs, `/usr/local/bin/code` symlinks to **Cursor**, not VS Code. Use the `cursor` CLI or full app path instead. Agents: see [INSTRUCTIONS.md STEP-010](../INSTRUCTIONS.md).

---

## Troubleshooting pointers

| Symptom | Go to |
|---------|-------|
| `Kickbacks incompatible` | [TROUBLESHOOTING.md](./TROUBLESHOOTING.md#kickbacks-incompatible) |
| Sign-in command not found | [TROUBLESHOOTING.md](./TROUBLESHOOTING.md#sign-in-command-not-found) |
| Balance stays $0.00 | [TROUBLESHOOTING.md](./TROUBLESHOOTING.md#balance-stays-000) |
| Kickbacks offline | [TROUBLESHOOTING.md](./TROUBLESHOOTING.md#kickbacks-offline) |
| RELOAD warning | Reload window via Command Palette |

Extension bugs: [official GitHub issues](https://github.com/andrewmccalip/kickbacks.ai/issues)

---

## About this repo

### Is this official Kickbacks documentation?

**No.** This is a **community setup kit** maintained to make installation easy for humans and AI agents. Official support: [support@kickbacks.ai](mailto:support@kickbacks.ai).

### How do I set up Kickbacks with an AI agent?

Paste into Cursor or Claude Code:

```
Fetch and execute INSTRUCTIONS.md from https://github.com/ckryptickunal/kickbacks-setup
Run STEP-001 onward. Report PASS/FAIL after each ACTION. Stop at every GATE until I reply.
```

See [AGENTS.md](../AGENTS.md) and [INSTRUCTIONS.md](../INSTRUCTIONS.md).

### How can I help improve this guide?

⭐ Star the repo · Open a [doc issue](https://github.com/ckryptickunal/kickbacks-setup/issues/new/choose) · Submit a PR — see [CONTRIBUTING.md](../CONTRIBUTING.md)
