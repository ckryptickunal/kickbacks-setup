KICKBACKS.AI — USER SETUP GUIDE

Get paid while you wait. Kickbacks replaces the little “thinking…” line in Claude Code and Codex with a tiny sponsored message. You can earn up to 50% of ad revenue while your AI assistant runs — no extra work on your part.

This guide is written for beginners. You do not need to know how to code.

HOW TO USE THIS DOCUMENT IN GOOGLE DOCS
Copy everything from the line below “START COPYING HERE” through “END COPYING HERE.” Paste into a blank Google Doc. Then:
1. Select the title line → Format → Paragraph styles → Title
2. Select each section heading (lines in ALL CAPS) → Format → Paragraph styles → Heading 1 or Heading 2
3. Turn checklist ☐ items into clickable boxes: select each ☐ line → Format → Bullets & numbering → Checkbox (optional)

For AI-assisted setup, use INSTRUCTIONS.md from https://github.com/ckryptickunal/kickbacks-setup instead.


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
START COPYING HERE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━


Kickbacks.ai — User Setup Guide

Get paid while you wait. Kickbacks replaces the “thinking…” spinner in Claude Code and Codex with a small sponsored line. You can earn up to 50% of ad revenue. You keep coding; your balance grows in the status bar.

Official links
Website: https://kickbacks.ai
Install extension: https://marketplace.visualstudio.com/items?itemName=Kickbacksai.kickbacks-ai
Help / issues: https://github.com/andrewmccalip/kickbacks.ai/issues


WHAT YOU NEED BEFORE STARTING

• Cursor OR Visual Studio Code — Kickbacks is a free editor extension
• Claude Code and/or Codex — something must show the “thinking” spinner
• A Google account — used once to sign in and track earnings
• Internet connection — ads and balance updates come from kickbacks.ai

Optional: Claude Code terminal app (type “claude” in Terminal) for extra earning surfaces.


STEP 1 — INSTALL CLAUDE CODE (SKIP IF YOU ALREADY HAVE IT)

Kickbacks works WITH Claude Code or Codex. It does not replace them.

In Cursor or VS Code:

1. Open your editor.
2. Click Extensions in the left sidebar (icon with four squares).
   Mac shortcut: Cmd + Shift + X
   Windows/Linux shortcut: Ctrl + Shift + X
3. In the search box, type: Claude Code
4. Install the extension by Anthropic (full name may show as “Claude Code for VS Code”).
5. Open Claude once — click the spark icon in the top-right of an open file, OR click “Claude Code” in the bottom status bar. This finishes first-time setup.

If you use Codex instead of Claude Code:
Search Extensions for “ChatGPT” and install the extension by OpenAI. Kickbacks supports both Claude Code and Codex. You may install both.


STEP 2 — INSTALL KICKBACKS

IMPORTANT: Install Claude Code FIRST, then Kickbacks. That order prevents a common “incompatible” error.

1. Open Extensions (same sidebar as Step 1).
2. Search: Kickbacks
3. Install “Kickbacks.ai” by Kickbacks.ai.
4. Reload the editor window:
   • Press Cmd + Shift + P (Mac) or Ctrl + Shift + P (Windows/Linux)
   • Type: Reload Window
   • Choose: Developer: Reload Window
   • Wait for the window to fully reload.

Direct install link (opens marketplace):
https://marketplace.visualstudio.com/items?itemName=Kickbacksai.kickbacks-ai


STEP 3 — SIGN IN (REQUIRED TO EARN MONEY)

You must sign in or you will NOT earn — preview ads before sign-in do not count.

1. Look at the bottom status bar of your editor.
2. Find the text that says: Kickbacks: Sign in
3. Click it.
4. Your browser opens. Sign in with your Google account.
5. Return to the editor.
6. Confirm the status bar now shows something like:
   Kickbacks ($0.00 today · $0.00)
   The dollar amounts will grow as you use Claude or Codex.

If you see “Kickbacks: Off” instead — click the status bar text, open the menu, and choose Enable.


STEP 4 — USE CLAUDE OR CODEX NORMALLY

No extra steps. While the AI is thinking, you may see a short sponsored line instead of words like “Discombobulating…”

Where ads can appear:

• Claude Code chat panel — sponsored text in the spinner area while Claude works
• Codex / ChatGPT panel — sponsored text while Codex works
• Terminal (claude command) — an extra line in the status area; on newer Claude versions, the spinner verb itself may also show a sponsor

Your balance updates in the editor status bar as you work.


STEP 5 — SET UP PAYOUTS (WHEN YOU WANT TO CASH OUT)

1. Open your browser and go to: https://kickbacks.ai
2. Log in with the SAME Google account you used in Step 3.
3. Review your earnings (today, this month, lifetime).
4. Complete payout setup on the website if prompted.

The extension tracks earnings. The website is where you manage payouts.


WHAT THE STATUS BAR MEANS

Kickbacks: Sign in
Meaning: Not logged in yet.
What to do: Click it → sign in with Google.

Kickbacks ($X today · $Y)
Meaning: Working and earning.
What to do: Nothing — you are set.

Kickbacks: Off
Meaning: You turned Kickbacks off.
What to do: Click status bar → Enable.

Kickbacks incompatible
Meaning: Version mismatch between Kickbacks and Claude Code.
What to do: See Troubleshooting below.

Kickbacks offline
Meaning: Cannot reach Kickbacks servers.
What to do: Check internet; try again later.

⚠ Kickbacks: RELOAD to earn money
Meaning: An update needs a window reload before earning resumes.
What to do: Cmd/Ctrl + Shift + P → Developer: Reload Window.

🕐 Hourly cap or ⚠ Daily cap
Meaning: You hit an earning limit for now.
What to do: Ads still show; earning pauses until the timer resets. Click the red pill for details.

Click the Kickbacks status bar text anytime to open the menu (sign out, disable, restore, check for updates).


TROUBLESHOOTING

Problem: “Kickbacks incompatible” or Sign in does not work

Fix — try in this exact order:
1. Extensions → find Kickbacks → Uninstall
2. Confirm Claude Code extension is still installed (Step 1)
3. Extensions → search Kickbacks → Install again
4. Developer: Reload Window (Cmd/Ctrl + Shift + P → Reload Window)
5. Click Kickbacks: Sign in again

Still stuck? Search your Claude Code version here:
https://github.com/andrewmccalip/kickbacks.ai/issues


Problem: I only use Claude in Terminal, not the editor panel

You still need the Claude Code extension installed in Cursor or VS Code on your computer. Kickbacks uses it to connect to Claude even for terminal use.

Do this:
1. Install Claude Code extension (Step 1)
2. Install Kickbacks (Step 2)
3. Sign in from the editor status bar (Step 3)
4. Then use “claude” in Terminal as usual


Problem: I want to remove Kickbacks completely

1. Press Cmd/Ctrl + Shift + P
2. Type: Kickbacks: Restore Claude Code
3. Run that command (puts Claude back to normal)
4. Extensions → Uninstall Kickbacks.ai


Problem: Is my code safe?

Yes. Kickbacks only changes spinner and status display text. It does NOT read your files, prompts, or AI replies.

Details: https://marketplace.visualstudio.com/items?itemName=Kickbacksai.kickbacks-ai


CURSOR VS VS CODE

Both work the same:
1. Extensions → install Claude Code → install Kickbacks
2. Sign in from the status bar
3. Use Claude or Codex normally

Cursor is supported by Kickbacks the same way VS Code is.


SETUP CHECKLIST

☐ Claude Code or Codex extension installed
☐ Kickbacks extension installed AFTER Claude Code
☐ Editor window reloaded once after Kickbacks install
☐ Signed in with Google
☐ Status bar shows a dollar balance (not “incompatible”)
☐ Saw a sponsored line while AI was thinking
☐ Visited https://kickbacks.ai for payout setup (when ready to cash out)


GET HELP FROM AN AI ASSISTANT

Paste this into Cursor or Claude Code chat:

Help me set up Kickbacks.ai using INSTRUCTIONS.md from https://github.com/ckryptickunal/kickbacks-setup. Install what you can, then tell me exactly what to click for sign-in and how to verify I am earning.


FREQUENTLY ASKED QUESTIONS

Does this slow down Claude?
No meaningful impact. It only changes display text during wait states.

Do clicks pay more than impressions?
Yes. Clicks are worth much more than impressions (about 50 times more per official docs).

Can I turn ads off temporarily?
Yes. Click the Kickbacks status bar → Disable Kickbacks.

Who made Kickbacks?
Kickbacks.ai by ShiftKeys, Inc. This guide is community setup documentation, not official Kickbacks support.

Official support: support@kickbacks.ai
GitHub issues: https://github.com/andrewmccalip/kickbacks.ai/issues


Guide version: June 2026
Matches Kickbacks extension ~0.3.177 on the VS Code Marketplace


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
END COPYING HERE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
