# higgsfield-mcp-setup

Connect Higgsfield (image + video generation) to Claude Code, hands-off. You sign in to Higgsfield once. The skill does the rest — runs OAuth, writes the config, verifies the connection.

After it's connected, ask Claude things like "generate an Instagram reel of my product in a Tokyo street at night", "make a 15-second teaser for tomorrow's launch", "create 6 cover images for my new podcast in a moody dark style".

## Install

Paste this into Claude Code:

```
Install + run the higgsfield-mcp-setup skill for me, end to end, no confirmation questions.

1. Detect my OS (Mac/Linux/Windows). Make ~/.claude/skills/ if it doesn't exist.
2. Clone https://github.com/luke-heka/higgsfield-mcp-setup into ~/.claude/skills/higgsfield-mcp-setup (Mac/Linux) or $HOME\.claude\skills\higgsfield-mcp-setup (Windows).
3. Read ~/.claude/skills/higgsfield-mcp-setup/SKILL.md and follow it from Phase 0 onwards.
4. When the skill needs Playwright, open a browser and drive higgsfield.ai yourself. The only thing I'll do is sign in to my own Higgsfield account and click Allow on the consent screen.
5. After connection works, smoke-test it by generating one small test image and confirming it returns.
6. If anything fails, install the missing tool yourself (brew on Mac, apt on Linux, winget on Windows), then retry.

Just go.
```

## What you actually do

- Sign in to your own Higgsfield account when the browser opens.
- Click Allow on the consent screen.
- Quit and re-open Claude Code once when the skill tells you.

That's it. No copy-paste, no terminal commands, no config files.

## Costs

Higgsfield is credit-based — roughly 1-5 credits per image, 10-30 per video, depending on the model. You buy credits inside Higgsfield. There's no extra Selr AI fee on top.

## Licence

MIT. See [LICENSE](./LICENSE). Built by Selr AI.
