# Contributing

Thanks for helping improve the Kickbacks Setup Kit. Every fix you add helps the next person searching GitHub for **Kickbacks Cursor setup**, **Kickbacks incompatible**, or **Claude Code earn money**.

This repo is **documentation only** — it does not contain Kickbacks extension source code.

**Quick ways to help (no PR required):**

- ⭐ **Star the repo** if it saved you time — boosts GitHub search visibility
- 📣 **Share** [SHARE.md](./SHARE.md) copy-paste messages with your team
- ✅ **Post a [setup success story](https://github.com/ckryptickunal/kickbacks-setup/issues/new?template=setup-success.yml)** — builds trust for new users
- 🐛 **Open a doc issue** if something's unclear or outdated

## What to contribute

- Clearer steps for Cursor, VS Code, Remote-SSH, or Windows
- Updated extension IDs or CLI commands when Kickbacks or Claude Code changes
- Troubleshooting for new status bar states or error messages
- Typos, broken links, or confusing wording

## What not to contribute

- Kickbacks extension code (see the [official repo](https://github.com/andrewmccalip/kickbacks.ai))
- `.vsix` files or marketplace bypass instructions
- Steps that require reading user code or completing OAuth on their behalf

## How to submit changes

1. Fork https://github.com/ckryptickunal/kickbacks-setup
2. Edit the relevant file:
   - **Humans** → `USER-GUIDE.md` (keep the Google Docs paste block plain-text)
   - **Agents** → `INSTRUCTIONS.md` (keep STEP-xxx numbering and GATE semantics)
3. Open a pull request with:
   - What you changed and why
   - Which Kickbacks / Claude Code versions you tested (if any)

## Proofreading checklist

Before merging doc changes, verify:

- [ ] Extension IDs match [Kickbacks package.json](https://github.com/andrewmccalip/kickbacks.ai/blob/main/package.json)
- [ ] Install order still recommends Claude Code before Kickbacks
- [ ] All URLs resolve
- [ ] INSTRUCTIONS.md one-line prompt still works when pasted into an agent
- [ ] USER-GUIDE paste block has no markdown tables (Google Docs friendly)
