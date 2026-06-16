# Kickbacks Setup Kit

**Free setup guide for [Kickbacks.ai](https://kickbacks.ai)** — earn up to **50% of ad revenue** while Claude Code or Codex shows its “thinking…” spinner in **Cursor**, **VS Code**, or the **terminal**.

[![Kickbacks.ai](https://img.shields.io/badge/Kickbacks.ai-website-111?labelColor=6366f1)](https://kickbacks.ai)
[![VS Code Marketplace](https://img.shields.io/badge/Install-VS%20Code%20Marketplace-007ACC?logo=visualstudiocode&logoColor=white)](https://marketplace.visualstudio.com/items?itemName=Kickbacksai.kickbacks-ai)
[![Agent playbook](https://img.shields.io/badge/Agent-INSTRUCTIONS.md-000?labelColor=22c55e)](./INSTRUCTIONS.md)

> **Community documentation.** Not affiliated with ShiftKeys, Inc. or Kickbacks.ai. For official support: [support@kickbacks.ai](mailto:support@kickbacks.ai) · [GitHub issues](https://github.com/andrewmccalip/kickbacks.ai/issues)

---

## What is Kickbacks?

While Claude Code or Codex is working, you normally see spinner verbs like *“Discombobulating…”*. **Kickbacks** replaces that line with a small sponsored message. Advertisers bid for the slot; you earn on impressions and clicks. Your balance appears in the editor status bar and on [kickbacks.ai](https://kickbacks.ai).

**Kickbacks does not read your code, prompts, or AI chat.** It only changes display text during wait states.

---

## Pick your path

| You are… | Start here | Time |
|----------|------------|------|
| **Human** — want step-by-step clicks | [USER-GUIDE.md](./USER-GUIDE.md) | ~10 min |
| **AI agent** — Cursor, Claude Code, Codex, Copilot | [INSTRUCTIONS.md](./INSTRUCTIONS.md) or [AGENTS.md](./AGENTS.md) | ~15 min |
| **Maintainer / proofreader** | [TRACE.md](./TRACE.md) | — |

### Quick start (humans)

1. Open **Cursor** or **VS Code**.
2. **Extensions** → search **Claude Code** → Install (skip if you already have it).
3. **Extensions** → search **Kickbacks** → Install **Kickbacks.ai**.
4. **Cmd/Ctrl+Shift+P** → **Developer: Reload Window**.
5. Click **Kickbacks: Sign in** in the bottom status bar → sign in with Google.
6. Use Claude or Codex normally. Earnings accrue while they “think.”

Full details, status bar meanings, and troubleshooting: **[USER-GUIDE.md](./USER-GUIDE.md)**

### Quick start (AI agents)

Paste this into your agent chat:

```
Fetch and execute INSTRUCTIONS.md from https://github.com/ckryptickunal/kickbacks-setup
Run STEP-001 onward. Report PASS/FAIL after each ACTION. Stop at every GATE until I reply.
Install extensions in order: Claude Code first, then Kickbacks.
```

Or open [INSTRUCTIONS.md](./INSTRUCTIONS.md) locally and follow the runbook (STEP-001 … STEP-025).

---

## Requirements

| Requirement | Why |
|-------------|-----|
| **Cursor** or **VS Code** | Kickbacks is an editor extension |
| **Claude Code** and/or **Codex** | Something must show the “thinking” spinner |
| **Google account** | Sign-in and earnings tracking |
| **Internet** | Ads and balance sync from kickbacks.ai |

**Install order matters:** Claude Code extension **before** Kickbacks ([issue #13](https://github.com/andrewmccalip/kickbacks.ai/issues/13)).

---

## Compatibility (June 2026)

| Surface | Where ads show | Requirement |
|---------|----------------|-------------|
| Spinner overlay | Claude Code panel in editor | Claude Code + Kickbacks |
| Thinking shimmer | Codex / ChatGPT panel | OpenAI ChatGPT extension + Kickbacks |
| Status-bar line | Claude Code **terminal CLI** | Any Claude Code CLI version |
| Spinner verb | Claude Code **terminal CLI** | Claude Code **2.1.143+** |

Works on **VS Code**, **Cursor**, Remote-SSH, and devcontainers.

---

## Official Kickbacks links

| Resource | URL |
|----------|-----|
| Website & dashboard | https://kickbacks.ai |
| VS Code Marketplace | https://marketplace.visualstudio.com/items?itemName=Kickbacksai.kickbacks-ai |
| Extension source (read-only) | https://github.com/andrewmccalip/kickbacks.ai |
| Compatibility & bugs | https://github.com/andrewmccalip/kickbacks.ai/issues |

---

## Repository layout

```
kickbacks-setup/
├── README.md          ← You are here
├── AGENTS.md          ← Entry point for AI coding agents
├── INSTRUCTIONS.md    ← Full agent runbook (STEP-001 … STEP-025)
├── USER-GUIDE.md      ← Human guide (Google Docs paste-ready)
├── TRACE.md           ← Research notes for maintainers
└── CONTRIBUTING.md    ← How to improve this kit
```

**Raw URLs for agents** (fetch without cloning):

- Instructions: `https://raw.githubusercontent.com/ckryptickunal/kickbacks-setup/main/INSTRUCTIONS.md`
- User guide: `https://raw.githubusercontent.com/ckryptickunal/kickbacks-setup/main/USER-GUIDE.md`

---

## FAQ

**Does Kickbacks slow down Claude or Codex?**  
No meaningful impact — it only changes display text during wait states.

**Do I need to sign in?**  
Yes, to earn. Preview ads before sign-in do not count toward your balance.

**I only use `claude` in Terminal — do I still need the editor extension?**  
Yes. Install Claude Code and Kickbacks in Cursor/VS Code, sign in from the status bar, then use the terminal as usual.

**Cursor or VS Code?**  
Both work the same way. On some Macs, the `code` CLI points to Cursor — agents should prefer the `cursor` CLI when installs fail.

**Is this open source?**  
This setup kit is MIT-licensed documentation. The Kickbacks extension itself is source-available (ShiftKeys, Inc.), not open source.

---

## Contributing

Found a typo, outdated extension ID, or clearer troubleshooting step? See [CONTRIBUTING.md](./CONTRIBUTING.md).

---

## License

Documentation in this repository is licensed under the [MIT License](./LICENSE). Kickbacks.ai and the Kickbacks extension are trademarks of their respective owners.
