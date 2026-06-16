# Kickbacks.ai — Troubleshooting Guide

Fix the most common Kickbacks setup errors in **Cursor**, **VS Code**, and the **Claude Code terminal**.

→ **Setup from scratch:** [USER-GUIDE.md](../USER-GUIDE.md) · **Agent help:** [INSTRUCTIONS.md](../INSTRUCTIONS.md)

---

## Before you troubleshoot

Run through this 30-second checklist:

- [ ] **Claude Code** extension installed **before** Kickbacks
- [ ] Editor window **reloaded** after Kickbacks install
- [ ] **Signed in** with Google (status bar shows `$` amounts)
- [ ] Using **Claude Code or Codex** — Kickbacks needs a thinking spinner

---

## Kickbacks incompatible

**Status bar shows:** `Kickbacks incompatible`

**Cause:** Version mismatch between Kickbacks and Claude Code, or wrong install order.

### Fix (try in this exact order)

1. **Extensions** → **Kickbacks.ai** → **Uninstall**
2. Confirm **Claude Code** is still installed
3. **Extensions** → search **Kickbacks** → **Install**
4. **Cmd/Ctrl + Shift + P** → **Developer: Reload Window**
5. Click **Kickbacks: Sign in** again

### Still incompatible?

1. Update Kickbacks: Command Palette → **Kickbacks: Menu** → check for updates  
   Or run: `cursor --install-extension Kickbacksai.kickbacks-ai --force`
2. Run **Kickbacks: Diagnose** — note `compatible: true/false`
3. Check [official GitHub issues](https://github.com/andrewmccalip/kickbacks.ai/issues) for your Claude Code version

**Workaround:** Panel ads may be blocked, but **terminal status-bar ads** often still work. Try `claude` in Terminal after signing in from the editor.

---

## Sign-in command not found

**Error:** `command 'kickbacks.signIn' not found`

**Cause:** Kickbacks extension not fully activated — usually install order or missing reload.

### Fix

1. Uninstall Kickbacks
2. Reinstall **Claude Code** first, then **Kickbacks**
3. **Developer: Reload Window**
4. Try **Kickbacks: Sign in** again

If using an AI agent, re-run [INSTRUCTIONS.md STEP-011](../INSTRUCTIONS.md).

---

## Balance stays $0.00

**Status bar shows dollars but balance doesn't grow.**

Check each:

| Check | Action |
|-------|--------|
| Signed in? | Status must show `$` — not `Kickbacks: Sign in` |
| Preview ads? | Ads **before** sign-in don't earn |
| Cap hit? | Look for red `Hourly cap` or `Daily cap` pill |
| Reload needed? | Status says `⚠ RELOAD to earn money` → Reload Window |
| Actually thinking? | Kickbacks earns during spinner/wait states |

Run **Kickbacks: Diagnose** and share output in [official issues](https://github.com/andrewmccalip/kickbacks.ai/issues) if still stuck.

---

## Kickbacks offline

**Status bar shows:** `Kickbacks offline`

1. Check internet connection
2. Verify [kickbacks.ai](https://kickbacks.ai) loads in your browser
3. **Developer: Reload Window**
4. Wait 1–2 minutes — may be temporary backend issue

---

## Extension not found on Mac

**Error:** `Extension 'Kickbacksai.kickbacks-ai' not found` when using `code --install-extension`

**Cause:** On many Macs, `code` symlinks to **Cursor**, not VS Code.

### Fix

Use the correct CLI:

```bash
# Cursor (preferred on Mac if you use Cursor)
cursor --install-extension Kickbacksai.kickbacks-ai

# Or full path
/Applications/Cursor.app/Contents/Resources/app/bin/cursor --install-extension Kickbacksai.kickbacks-ai
```

Real VS Code users:

```bash
/Applications/Visual\ Studio\ Code.app/Contents/Resources/app/bin/code --install-extension Kickbacksai.kickbacks-ai
```

---

## RELOAD to earn money

**Status bar shows:** `⚠ Kickbacks: RELOAD to earn money`

Kickbacks updated in the background. Earning pauses until you reload.

1. **Cmd/Ctrl + Shift + P**
2. Type **Reload Window**
3. Select **Developer: Reload Window**

---

## Kickbacks not in status bar

1. **Extensions** → confirm **Kickbacks.ai** is **Enabled**
2. **Developer: Reload Window**
3. Command Palette → **Kickbacks: Menu** — if command missing, reinstall (see [Sign-in command not found](#sign-in-command-not-found))

---

## Kickbacks: Off

Click the status bar text → open menu → choose **Enable**.

---

## Terminal-only users

**Problem:** Using `claude` in Terminal but never opened the editor.

Kickbacks still requires editor extensions:

1. Install **Claude Code** in Cursor/VS Code
2. Install **Kickbacks** in Cursor/VS Code
3. **Sign in** from editor status bar
4. Use `claude` in Terminal — ads appear in status line (and spinner verb on CLI 2.1.143+)

---

## Remote-SSH / dev containers

Install extensions in the **remote** window, not just locally:

1. Connect to remote/devcontainer
2. Open Extensions sidebar
3. Install Claude Code + Kickbacks **on remote**
4. Reload remote window
5. Sign in from remote status bar

---

## Full removal

Only if you want to uninstall completely:

1. **Cmd/Ctrl + Shift + P** → **Kickbacks: Restore Claude Code**
2. Wait for confirmation
3. **Extensions** → Uninstall **Kickbacks.ai**

---

## Still stuck?

| Resource | Link |
|----------|------|
| Full FAQ | [docs/FAQ.md](./FAQ.md) |
| Human setup guide | [USER-GUIDE.md](../USER-GUIDE.md) |
| AI agent runbook | [INSTRUCTIONS.md](../INSTRUCTIONS.md) |
| Extension bugs | [github.com/andrewmccalip/kickbacks.ai/issues](https://github.com/andrewmccalip/kickbacks.ai/issues) |
| Doc improvements | [Open an issue on this repo](https://github.com/ckryptickunal/kickbacks-setup/issues/new/choose) |

**Helpful fix not listed here?** [Contribute it](../CONTRIBUTING.md) — others are searching for the same error.
