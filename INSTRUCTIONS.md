# Kickbacks.ai — Agent Setup Playbook

You are an AI coding agent. Execute this runbook **in order**. Do not skip steps. Do not batch unrelated steps without reporting results between them.

**Extension ID:** `Kickbacksai.kickbacks-ai`  
**Marketplace:** https://marketplace.visualstudio.com/items?itemName=Kickbacksai.kickbacks-ai  
**Website:** https://kickbacks.ai  
**This runbook:** https://github.com/ckryptickunal/kickbacks-setup/blob/main/INSTRUCTIONS.md  
**Raw URL (for fetch):** https://raw.githubusercontent.com/ckryptickunal/kickbacks-setup/main/INSTRUCTIONS.md

---

## How to use this document

| Symbol | Meaning |
|--------|---------|
| **ACTION** | You (agent) must run a command or perform a check now |
| **SAY** | Exact message to send the user (adapt OS names only) |
| **EXPECT** | Pass condition — if false, go to the **IF FAIL** step cited |
| **GATE** | Stop and wait for user reply before continuing |
| **USER** | User must do manually — you cannot substitute |

Maintain a running log in chat: after each ACTION, report `STEP-xxx: PASS` or `STEP-xxx: FAIL — <reason>`.

---

## PHASE 0 — Rules (read once, then execute)

### Allowed
- Run read-only shell checks before any install
- Install extensions via `$EDITOR_CLI --install-extension`
- Uninstall/reinstall Kickbacks only when troubleshooting prescribes it
- Ask the user to click UI elements, sign in, or reload the window

### Forbidden
- Complete Google OAuth for the user
- Read or summarize the user's code, prompts, or chat as part of setup
- Manually edit Claude Code `webview/index.js` or `~/.claude/settings.json`
- Assume `code` CLI is VS Code (on many Macs it symlinks to Cursor)
- Run `curl | bash` installers without explicit user consent

### Privacy (SAY once at start)
> Kickbacks only talks to kickbacks.ai. It sends ad/visibility events, a per-install ID, extension/host versions, and your account email after sign-in; your IP is stored only as a salted one-way hash. It never reads your code, prompts, files, or AI chat. More info: https://kickbacks.ai/faq

---

## PHASE 1 — Discover environment

### STEP-001 · Detect operating system

**ACTION** — run:
```bash
uname -s 2>/dev/null || echo Windows
```

**EXPECT** — output is one of: `Darwin`, `Linux`, `Windows`, or MINGW/CYGWIN variant.

**Record:** `OS = …`

**IF FAIL** — ask user: "Are you on Mac, Windows, or Linux?"

---

### STEP-002 · Resolve editor CLI binary

**ACTION** — run all that apply on user's machine:

```bash
# Try Cursor in PATH
if command -v cursor >/dev/null 2>&1; then
  echo "CURSOR_PATH=cursor"
  cursor --version 2>&1 | head -1
fi

# Try code in PATH
if command -v code >/dev/null 2>&1; then
  echo "CODE_PATH=code"
  code --version 2>&1 | head -1
  ls -l "$(command -v code)" 2>/dev/null || true
fi

# macOS app bundles
[ -x "/Applications/Cursor.app/Contents/Resources/app/bin/cursor" ] && echo "CURSOR_APP=/Applications/Cursor.app/Contents/Resources/app/bin/cursor"
[ -x "/Applications/Visual Studio Code.app/Contents/Resources/app/bin/code" ] && echo "VSCODE_APP=/Applications/Visual Studio Code.app/Contents/Resources/app/bin/code"
```

**ACTION** — choose `EDITOR_CLI`:
1. If user said **Cursor** → prefer `cursor`, then `CURSOR_APP` path, then `code` only if symlink points to Cursor and works
2. If user said **VS Code** → prefer real VS Code `code` or `VSCODE_APP`, not Cursor shim
3. If unknown → use whichever successfully runs `--list-extensions`

**ACTION** — verify CLI works:
```bash
$EDITOR_CLI --list-extensions >/dev/null 2>&1 && echo "CLI_OK" || echo "CLI_FAIL"
```

**EXPECT** — `CLI_OK`

**SAY** (on success):
> I found your editor CLI: `<EDITOR_CLI>`. I'll use this for extension installs.

**IF FAIL** — GATE: ask user to install Cursor or VS Code and enable shell command ("Install 'cursor' command in PATH" or "Install 'code' command in PATH" from Command Palette).

---

### STEP-003 · Detect which AI tools the user wants

**GATE** — ask exactly:
> Which do you use? Reply with letters, e.g. "A and C":
> A) Claude Code panel in Cursor/VS Code
> B) Codex / ChatGPT panel in Cursor/VS Code
> C) Claude Code in Terminal (`claude` command)
> D) Not sure — set up everything

**Record:** `WANTS_CLAUDE_PANEL`, `WANTS_CODEX_PANEL`, `WANTS_CLI` (true/false). If D → set all true.

---

### STEP-004 · List installed extensions

**ACTION** — run:
```bash
$EDITOR_CLI --list-extensions 2>/dev/null | grep -iE '^(kickbacksai\.kickbacks-ai|anthropic\.claude-code|openai\.chatgpt)$' || true
```

**Record:**

| Variable | true when line present |
|----------|------------------------|
| `HAS_KICKBACKS` | `kickbacksai.kickbacks-ai` |
| `HAS_CLAUDE_EXT` | `anthropic.claude-code` |
| `HAS_CODEX_EXT` | `openai.chatgpt` |

**SAY**:
> Installed: Kickbacks `<yes/no>`, Claude Code extension `<yes/no>`, Codex/ChatGPT extension `<yes/no>`.

---

### STEP-005 · Detect Claude Code CLI

**ACTION** — run:
```bash
command -v claude >/dev/null 2>&1 && claude --version 2>&1 | head -1 || echo "CLI_NOT_INSTALLED"
```

**Record:** `CLAUDE_CLI_VERSION` or `NONE`

**SAY** (if WANTS_CLI and NONE):
> Claude Code terminal app is not installed. I can share install instructions after we finish the editor setup.

**Note:** Terminal spinner-verb ads need CLI **≥ 2.1.143**. Status-bar line ads work on any CLI version.

---

### STEP-006 · Confirm Google sign-in willingness

**GATE** — ask:
> Kickbacks requires Google sign-in to earn money. Are you OK signing in with Google in your browser? Reply yes or no.

**EXPECT** — user says yes.

**IF FAIL** — stop runbook. **SAY**: You can still install Kickbacks but will only see preview ads until you sign in.

---

## PHASE 2 — Install extensions (agent)

**Order rule:** `anthropic.claude-code` BEFORE `Kickbacksai.kickbacks-ai` on first install ([issue #13](https://github.com/andrewmccalip/kickbacks.ai/issues/13)).

---

### STEP-007 · Install Claude Code extension

**Skip if:** `HAS_CLAUDE_EXT=true` OR `WANTS_CLAUDE_PANEL=false` AND `WANTS_CLI=false`

**SAY**:
> Installing Claude Code extension (required before Kickbacks)…

**ACTION** — run:
```bash
$EDITOR_CLI --install-extension anthropic.claude-code 2>&1
```

**EXPECT** — exit code 0 OR message "already installed"

**ACTION** — re-check:
```bash
$EDITOR_CLI --list-extensions | grep -i '^anthropic\.claude-code$'
```

**EXPECT** — line present → `STEP-007: PASS`

**IF FAIL** — try alternate CLI (Cursor app path vs code). If still fail → GATE: ask user to install "Claude Code" manually from Extensions sidebar, then confirm done.

---

### STEP-008 · Activate Claude Code extension once

**Skip if:** STEP-007 skipped

**SAY**:
> Please open the Claude Code panel once: click the spark icon (top-right of an open file) OR click "Claude Code" in the bottom status bar. Reply **done** when the panel has opened.

**GATE** — wait for user: `done`

---

### STEP-009 · Install Codex / ChatGPT extension

**Skip if:** `HAS_CODEX_EXT=true` OR `WANTS_CODEX_PANEL=false`

**SAY**:
> Installing Codex/ChatGPT extension…

**ACTION** — run:
```bash
$EDITOR_CLI --install-extension openai.chatgpt 2>&1
```

**EXPECT** — exit code 0 or already installed

**ACTION** — verify:
```bash
$EDITOR_CLI --list-extensions | grep -i '^openai\.chatgpt$'
```

**IF FAIL** — GATE: user installs "ChatGPT" by OpenAI from Extensions manually.

---

### STEP-010 · Install Kickbacks extension

**SAY**:
> Installing Kickbacks.ai extension…

**ACTION** — run:
```bash
$EDITOR_CLI --install-extension Kickbacksai.kickbacks-ai 2>&1
```

**IF FAIL** ("Extension not found") AND `EDITOR_CLI=code` — retry:
```bash
cursor --install-extension Kickbacksai.kickbacks-ai 2>&1
```
Update `EDITOR_CLI=cursor` if this succeeds.

**IF FAIL** on macOS — retry with full path:
```bash
/Applications/Cursor.app/Contents/Resources/app/bin/cursor --install-extension Kickbacksai.kickbacks-ai 2>&1
```

**ACTION** — verify:
```bash
$EDITOR_CLI --list-extensions | grep -i '^kickbacksai\.kickbacks-ai$'
```

**EXPECT** — line present → `STEP-010: PASS`

**IF FAIL** — GATE: user installs from https://marketplace.visualstudio.com/items?itemName=Kickbacksai.kickbacks-ai via Extensions search "Kickbacks".

---

### STEP-011 · Reinstall Kickbacks if previously broken

**Skip if:** STEP-010 fresh install AND user did not report incompatible / sign-in errors

**Run only if:** user has `HAS_KICKBACKS` before this session AND status was incompatible OR `kickbacks.signIn` not found

**SAY**:
> Fixing install order: reinstalling Kickbacks…

**ACTION** — run in order:
```bash
$EDITOR_CLI --uninstall-extension Kickbacksai.kickbacks-ai 2>&1
$EDITOR_CLI --install-extension anthropic.claude-code 2>&1
$EDITOR_CLI --install-extension Kickbacksai.kickbacks-ai 2>&1
```

**EXPECT** — Kickbacks listed again → `STEP-011: PASS`

---

### STEP-012 · Reload editor window

**SAY**:
> Reload your editor window so Kickbacks activates:
> 1. Press **Cmd+Shift+P** (Mac) or **Ctrl+Shift+P** (Windows/Linux)
> 2. Type: **Reload Window**
> 3. Select: **Developer: Reload Window**
> Reply **reloaded** when the window comes back.

**GATE** — wait for user: `reloaded`

---

## PHASE 3 — Sign in (USER)

### STEP-013 · Check status bar before sign-in

**SAY**:
> Look at the **bottom status bar**. What exact text do you see for Kickbacks?
> Examples: `Kickbacks: Sign in` · `Kickbacks ($0.00 today · $0.00)` · `Kickbacks: Off` · `Kickbacks incompatible`

**GATE** — wait for user to paste exact status text.

**Branch:**

| User text | Next step |
|-----------|-----------|
| `Kickbacks ($… today · …)` | Jump to **STEP-016** (already signed in) |
| `Kickbacks: Sign in` | **STEP-014** |
| `Kickbacks: Off` | **STEP-013b** |
| `Kickbacks incompatible` | **STEP-020** |
| `⚠ Kickbacks: RELOAD to earn money` | Repeat **STEP-012**, then **STEP-013** |
| `Kickbacks offline` | **STEP-021** |
| Nothing / no Kickbacks | **STEP-022** |

---

### STEP-013b · Enable Kickbacks if Off

**SAY**:
> Click the Kickbacks status bar text → open the menu → choose **Enable**. Reply with the new status text.

**GATE** — then re-run **STEP-013** logic.

---

### STEP-014 · USER sign-in

**SAY**:
> Sign in now (I cannot do this for you):
> 1. Click **Kickbacks: Sign in** in the status bar  
>    OR press Cmd/Ctrl+Shift+P → type **Kickbacks: Sign in** → Enter
> 2. Complete **Google sign-in** in the browser
> 3. Return to the editor
>
> **Important:** Ads shown BEFORE sign-in are preview only — you do not earn until sign-in completes.
>
> Reply **signed in** and paste the exact status bar text.

**GATE** — wait for `signed in` + status text.

**EXPECT** — status contains `$` and "today"

**IF FAIL** — if user reports `command 'kickbacks.signIn' not found` → **STEP-011** then **STEP-012** then **STEP-014** again.

---

### STEP-015 · Confirm sign-in success

**ACTION** — optional CLI check (extension host may not reflect auth; user confirmation is primary):
```bash
$EDITOR_CLI --list-extensions | grep -i kickbacks
```

**SAY** (on success):
> Sign-in looks good. Earnings accrue when Claude or Codex shows sponsored spinner lines while thinking.

**IF FAIL** — go to **PHASE 6** troubleshooting.

---

## PHASE 4 — Verify earning setup

### STEP-016 · Run Kickbacks Diagnose

**SAY**:
> Open Command Palette (Cmd/Ctrl+Shift+P) → run **Kickbacks: Diagnose**.
> Copy and paste the full output here (or a screenshot description including `compatible: true/false`).

**GATE** — wait for output.

**EXPECT** — `compatible: true` (ideal)

**IF FAIL** `compatible: false` — **STEP-020**; do not declare setup complete for panel ads.

---

### STEP-017 · Panel ad smoke test

**Skip if:** `WANTS_CLAUDE_PANEL=false` AND `WANTS_CODEX_PANEL=false`

**SAY**:
> Let's confirm ads appear:
> 1. Open Claude Code or Codex chat in the sidebar
> 2. Send: "Explain what a binary search is in two paragraphs"
> 3. While it thinks, watch the spinner line
>
> Reply with what you saw:
> A) Sponsored line (brand name / link)
> B) Only stock verbs like "Discombobulating..."
> C) No spinner / error

**GATE** — wait for A, B, or C.

| Reply | Next |
|-------|------|
| A | `STEP-017: PASS` → continue |
| B | **STEP-020** if incompatible; else note preview vs signed-in |
| C | ask user to confirm correct panel is open; retry once |

---

### STEP-018 · Terminal CLI smoke test

**Skip if:** `WANTS_CLI=false` OR `CLAUDE_CLI_VERSION=NONE`

**SAY**:
> Terminal check:
> 1. Open a terminal in your editor (or Terminal app)
> 2. Run: `claude`
> 3. Ask any short question
> 4. Watch for a Kickbacks line in the status area while thinking
>
> Reply **yes** if you saw a sponsored line, **no** if not.

**GATE**

**Note for agent:** CLI spinner-verb ads require `claude --version` ≥ 2.1.143. Status-bar line works on older versions.

---

### STEP-019 · Success criteria checklist

**ACTION** — mark each; all must pass before PHASE 5:

| # | Criterion | Pass? |
|---|-----------|-------|
| 1 | `kickbacksai.kickbacks-ai` installed | |
| 2 | User signed in (status shows `$`) | |
| 3 | Status is NOT `incompatible` (or user accepts CLI-only earning) | |
| 4 | User saw sponsored line OR Diagnose says compatible | |
| 5 | User told preview ads ≠ earnings | |

**SAY** (all pass):
> Core setup is complete. Optional next step: payout setup on kickbacks.ai.

**IF FAIL** — **PHASE 6** before declaring completion.

---

## PHASE 5 — Payouts (USER)

### STEP-023 · Dashboard and payout setup

**SAY**:
> To cash out later, complete this in your browser (I cannot do it for you):
> 1. Go to https://kickbacks.ai
> 2. Log in with the **same Google account**
> 3. Review earnings ledger
> 4. Connect **Stripe** and complete tax forms if the site prompts you
>
> How payouts work: monthly via **Stripe Connect**, once your balance crosses **US $10**.
>
> **Eligibility check:** payouts are **not yet available in some countries — including India, Pakistan, Bangladesh, Nigeria, and Vietnam.** If the user is in one of these, tell them they can still accrue a balance but cannot withdraw until their country is supported. Verify the current list at https://kickbacks.ai/faq.
>
> Note: If you hit hourly/daily caps, a red pill appears in the status bar (`Hourly cap` / `Daily cap`). Ads keep showing; earning pauses until reset.
>
> Reply **payout done** or **skip for now**.

**GATE** — either reply is OK to finish.

---

## PHASE 6 — Troubleshooting branches

Use when any STEP marks FAIL. Fix one branch, then **re-run from STEP-012** (reload) minimum.

---

### STEP-020 · Fix `Kickbacks incompatible`

**SAY**:
> Your Claude Code and Kickbacks versions may be out of sync. I'll update Kickbacks first.

**ACTION** — run:
```bash
$EDITOR_CLI --install-extension Kickbacksai.kickbacks-ai --force 2>&1
```

**SAY** — then **STEP-012** (reload) → **STEP-016** (Diagnose)

**IF still incompatible** — **SAY**:
> Check https://github.com/andrewmccalip/kickbacks.ai/issues for your Claude Code version. Panel ads may be blocked until Kickbacks ships an update. Terminal CLI status-bar ads may still work — try STEP-018.

---

### STEP-021 · Fix `Kickbacks offline`

**ACTION** — run:
```bash
curl -s -o /dev/null -w "%{http_code}" https://kickbacks.ai
```

**EXPECT** — `200` or `301`/`302`

**SAY** (if site down):
> kickbacks.ai appears unreachable from your network. Try again later.

**SAY** (if site up):
> The site is up; reload the window (STEP-012) and wait 1–2 minutes.

---

### STEP-022 · Kickbacks not visible in status bar

**SAY**:
> Kickbacks extension may not be active.
> 1. Extensions → confirm "Kickbacks.ai" is **Enabled**
> 2. Developer: Reload Window
> 3. If still missing, run **Kickbacks: Menu** from Command Palette — if command not found, repeat STEP-011.

---

### STEP-024 · Ads show but balance stays $0.00

**SAY** — ask user to confirm each:
> • Are you signed in (status shows dollar amounts)?
> • Did you see preview ads before sign-in? Those don't count.
> • Any red cap pill in the status bar?
> • Did status say RELOAD to earn money?

**ACTION** — if signed in and no caps: suggest **Kickbacks: Diagnose** output → search https://github.com/andrewmccalip/kickbacks.ai/issues

---

### STEP-025 · Full removal (only if user asks)

**SAY**:
> 1. Command Palette → **Kickbacks: Restore Claude Code**
> 2. Then I'll uninstall the extension.

**GATE** — user confirms restore done.

**ACTION**:
```bash
$EDITOR_CLI --uninstall-extension Kickbacksai.kickbacks-ai 2>&1
```

---

## PHASE 7 — Platform quick reference

| Platform | EDITOR_CLI hint | Extensions folder |
|----------|-----------------|-------------------|
| macOS Cursor | `cursor` or `/Applications/Cursor.app/.../cursor` | `~/.cursor/extensions/` |
| macOS VS Code | `/Applications/Visual Studio Code.app/.../code` | `~/.vscode/extensions/` |
| Windows | `cursor` or `code` in PATH | `%USERPROFILE%\.cursor\extensions` |
| Linux | `cursor` or `code` in PATH | `~/.cursor/extensions/` or `~/.vscode/extensions/` |
| Remote-SSH | Install extensions in **remote** window | remote home `.vscode-server` or `.cursor-server` |

**CLI-only users:** still require `anthropic.claude-code` extension installed in editor — Kickbacks locates Claude via extension directories. Sign-in happens in editor status bar; terminal patches `~/.claude/settings.json` automatically.

---

## PHASE 8 — Completion report

Fill and send to user:

```
═══════════════════════════════════════
KICKBACKS SETUP — COMPLETION REPORT
═══════════════════════════════════════

Environment
  OS: …
  Editor: Cursor / VS Code
  EDITOR_CLI: …
  Claude CLI: … / not installed

Extensions installed
  ☐ kickbacksai.kickbacks-ai
  ☐ anthropic.claude-code
  ☐ openai.chatgpt (if needed)

Completed by agent
  ☐ STEP-007–010 extensions
  ☐ STEP-012 reload guided
  ☐ STEP-016–018 verification

Completed by you
  ☐ Google sign-in
  ☐ Saw sponsored ad while AI thinking
  ☐ kickbacks.ai payout setup (or skipped)

Current status bar: …

If Claude Code updates later and ads stop:
  1. Developer: Reload Window
  2. Update Kickbacks (--force install)
  3. Reinstall Kickbacks after Claude Code extension

Help: https://github.com/andrewmccalip/kickbacks.ai/issues
═══════════════════════════════════════
```

---

## User paste prompt (one line)

```
Fetch and execute INSTRUCTIONS.md from https://github.com/ckryptickunal/kickbacks-setup — run STEP-001 onward. Report PASS/FAIL after each ACTION. Stop at every GATE until I reply. Install extensions in order: Claude Code first, then Kickbacks.
```

---

## Command reference

| Command Palette entry | Use |
|----------------------|-----|
| Kickbacks: Sign in | STEP-014 |
| Kickbacks: Diagnose | STEP-016 |
| Kickbacks: Menu | Enable/disable, updates |
| Kickbacks: Restore Claude Code | STEP-025 |
| Developer: Reload Window | STEP-012 |

---

*Runbook version: 2026-06-16 · Kickbacks v0.3.177 · Claude Code 2.1.178 · Facts re-verified against kickbacks.ai, kickbacks.ai/faq, and the VS Code Marketplace on 2026-06-16. Re-verify extension IDs and the payout country list on kickbacks.ai before major edits.*
