# Kickbacks Setup Kit — Agent Handoff Trace

> **Purpose:** Complete audit trail for future agents proofreading or improving this kit.  
> **Created:** 2026-06-16  
> **Scope:** Standalone folder `kickbacks-setup/` at workspace root — **no changes** to other projects in this repo.

---

## 1. User request (verbatim intent)

The user wanted:

1. A **standalone** deliverable unrelated to existing workspace code.
2. **`INSTRUCTIONS.md`** — paste into Cursor / Claude Code so an agent can set up Kickbacks end-to-end.
3. **`USER-GUIDE.md`** — human-readable doc suitable for a **Google Sheet** (copy/paste for naive users).
4. A **GitHub repo**-ready folder with README pointing to both.
5. **Adaptive** coverage: Cursor, VS Code, Claude Code panel, Codex panel, terminal CLI.
6. Clear split: **agent-automated** vs **USER ACTION REQUIRED** (Google OAuth, payouts).
7. **TRACE** document for handoff to proofreading agents.

---

## 2. Source material consulted

| Source | URL | What we extracted |
|--------|-----|-------------------|
| Kickbacks website | https://kickbacks.ai | Product pitch, 50% revenue share, 4 ad surfaces, install flow, advertiser model |
| GitHub README | https://github.com/andrewmccalip/kickbacks.ai | Architecture (`src/adapters`, auth, metrics), install steps, compatibility table, build commands |
| Extension readme | `readme_extension.md` on GitHub | Status bar states, privacy, patching mechanism (`webview/index.js`, `~/.claude/settings.json`), commands, caps |
| VS Code Marketplace | https://marketplace.visualstudio.com/items?itemName=Kickbacksai.kickbacks-ai | Marketplace install count, full FAQ, blocked account state, reload warning, Cursor compatibility statement |
| package.json (GitHub) | raw main branch | Extension ID `Kickbacksai.kickbacks-ai`, commands (`kickbacks.signIn`, `kickbacks.diagnose`, etc.), publisher `Kickbacksai` |
| GitHub issue #13 | https://github.com/andrewmccalip/kickbacks.ai/issues/13 | Install order fix; CLI-only needs IDE extension present; Claude Code 2.1.173 anchor incompatibility |

---

## 3. Live environment verification (author machine)

Commands run on 2026-06-16 on the user's Mac (`darwin`):

| Check | Result |
|-------|--------|
| `/usr/local/bin/code` | Symlink → **Cursor**, not VS Code |
| `code --install-extension Kickbacksai.kickbacks-ai` | **Failed** — "Extension not found" (Cursor marketplace quirk via `code` shim) |
| `/Applications/Cursor.app/.../cursor --install-extension Kickbacksai.kickbacks-ai` | **Success** — v0.3.177 already installed |
| Installed extensions | `anthropic.claude-code`, `kickbacksai.kickbacks-ai`, `openai.chatgpt` (multiple versions in `~/.cursor/extensions/`) |
| `claude --version` | **2.1.178** |

**Implication documented:** agents must detect whether `code` is Cursor shim vs real VS Code; prefer explicit `cursor` CLI on Mac when install fails.

---

## 4. Files created

```
kickbacks-setup/
├── README.md           # Repo entry: links, doc routing, compatibility snapshot
├── INSTRUCTIONS.md     # Agent playbook (~350 lines): phases 0–10, troubleshooting tree
├── USER-GUIDE.md       # Human guide: 5 steps, status bar table, FAQ
└── TRACE.md            # This file
```

**Intentionally not created:**
- No `.vsix` bundling (install from marketplace only).
- No fork of Kickbacks source (license: source-available, not OSS).
- No changes under `kb-staging-harness/` or other workspace dirs.

---

## 5. Key design decisions

### 5.1 Two-document model

| Doc | Audience | Tone |
|-----|----------|------|
| INSTRUCTIONS.md | AI agents | Imperative, shell commands, stop gates, decision trees |
| USER-GUIDE.md | Humans / Google Sheet | Plain language, UI clicks, minimal terminal |

### 5.2 Install order: Claude Code → Kickbacks

Documented because GitHub issue #13 and community comments confirm reinstall in this order fixes `incompatible` and missing `kickbacks.signIn` command.

### 5.3 CLI-only users must install IDE extension

Kickbacks locates Claude Code by scanning `~/.cursor/extensions`, `~/.vscode/extensions`, etc. Documented in INSTRUCTIONS §8 and USER-GUIDE troubleshooting — easy to miss in official README.

### 5.4 Preview vs earning

Marketplace explicitly states pre-sign-in ads are preview only. Repeated in both docs to prevent "$0 why?" confusion.

### 5.5 Agent boundaries

Hard stops for:
- Google OAuth (browser)
- Payout setup on kickbacks.ai
- Running Claude CLI installers without user consent

### 5.6 Compatibility caveats included

- Claude Code **2.1.143+** for terminal spinner verb
- Known breakage on CC **2.1.173+** with older Kickbacks builds — point to GitHub issues, suggest `--force` update
- `Kickbacks: Restore Claude Code` for revert path

---

## 6. Extension & command reference (canonical)

```
Extension IDs:
  Kickbacksai.kickbacks-ai
  anthropic.claude-code
  openai.chatgpt

Install (replace $EDITOR_CLI with cursor or code):
  $EDITOR_CLI --install-extension anthropic.claude-code
  $EDITOR_CLI --install-extension Kickbacksai.kickbacks-ai

Palette commands:
  Kickbacks: Sign in          → kickbacks.signIn
  Kickbacks: Sign out           → kickbacks.signOut
  Kickbacks: Menu               → kickbacks.debugMenu
  Kickbacks: Restore Claude Code → kickbacks.restore
  Kickbacks: Diagnose           → kickbacks.diagnose
```

---

## 7. Known gaps / future improvements

Priority for proofreading agents:

| ID | Gap | Suggested fix |
|----|-----|---------------|
| G1 | No Windows-specific screenshots | Add optional `assets/` with 3 screenshots if repo publishes publicly |
| G2 | Codex extension ID may change | Re-verify `openai.chatgpt` periodically; add note in TRACE when it changes |
| G3 | Cursor `code` shim install failure | Add automated detection snippet that tries `cursor` if `code` fails (already in INSTRUCTIONS §1.2 / §2.3) |
| G4 | Payout flow details sparse | kickbacks.ai login UX not scraped (dynamic SPA); USER-GUIDE intentionally defers to site |
| G5 | Issue #13 may be fixed in 0.3.177+ | Re-test with Claude Code 2.1.178; update compatibility note if closed |
| G6 | No translated locales | USER-GUIDE is English-only |
| G7 | Google Docs heading styles | USER-GUIDE includes paste instructions for Title/Heading styles after import — user must apply manually once |
| G8 | Remote-SSH | Mentioned but not step-by-step with screenshots |

---

## 8. Proofreading checklist

- [ ] All URLs resolve (kickbacks.ai, marketplace, GitHub)
- [ ] Extension IDs match current `package.json` on GitHub main
- [ ] Install order still recommended by latest GitHub issues
- [ ] Status bar states match latest marketplace readme
- [ ] No accidental claims of open-source license (it's source-available)
- [ ] INSTRUCTIONS.md one-line prompt works when pasted into Cursor
- [ ] USER-GUIDE readable on mobile Google Sheets
- [ ] TRACE updated with proofreader name/date on each revision

---

## 9. Publishing notes

**Live repo:** https://github.com/ckryptickunal/kickbacks-setup

```
kickbacks-setup/
├── README.md           # SEO entry, FAQ, doc routing
├── AGENTS.md           # Agent entry point (AGENTS.md convention)
├── INSTRUCTIONS.md     # Agent runbook STEP-001 … STEP-025
├── USER-GUIDE.md       # Human guide (Google Docs paste block)
├── TRACE.md            # This file
├── CONTRIBUTING.md
├── LICENSE             # MIT (documentation only)
└── .github/ISSUE_TEMPLATE/
```

**Google Sheet:** Copy `USER-GUIDE.md` paste block into a tab titled "Kickbacks Setup". Link to the GitHub repo for the agent playbook.

**GitHub topics (SEO):** `kickbacks`, `kickbacks-ai`, `cursor`, `vscode`, `claude-code`, `codex`, `setup-guide`, `ai-agents`, `documentation`

---

## 10. Revision log

| Date | Author | Change |
|------|--------|--------|
| 2026-06-16 | Cursor agent (initial) | Created full kit from official docs + live CLI verification on user Mac |
| 2026-06-16 | Cursor agent (rev 2) | USER-GUIDE: Google Docs paste block, no markdown tables. INSTRUCTIONS: STEP-001–025 runbook with ACTION/SAY/EXPECT/GATE/IF FAIL |
| 2026-06-16 | Cursor agent (rev 3) | GitHub repo polish: AGENTS.md, CONTRIBUTING, LICENSE, issue templates, SEO README, canonical URLs |
| 2026-06-16 | Cursor agent (rev 4) | SEO + engagement: docs/FAQ, docs/TROUBLESHOOTING, SHARE.md, collapsible FAQ, mermaid diagram, success-story template, expanded topics |

---

*End of trace.*
