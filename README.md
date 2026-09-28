<p align="center">
  <img src="assets/logo.svg" width="96" alt="OB Commander logo">
</p>

<h1 align="center">OB Commander</h1>

<p align="center">
  A fast, portable dual-pane file manager for Windows, in the spirit of Total Commander.
</p>

<p align="center">
  <b>English</b> · <a href="README.zh-CN.md">简体中文</a> ·
  <a href="https://obcommander.com">Website</a> ·
  <a href="https://github.com/kookob/obcommander/releases">Download</a>
</p>

---

## Highlights

- **Undo / redo for file operations** (Ctrl+Z / Ctrl+Y) — copy, move, delete and rename, several levels deep.
  Deletions are restored from the Recycle Bin, and the undo history is shared with Windows Explorer.
- **Folder sizes** — press Space on a folder (or size them all at once) and sort by size.
  With Pro, sizes are remembered, so a folder you have measured stays measured after a restart.
- **Instant previews** (Ctrl+Q / F3) *(Pro)* — images, text and code, Markdown, PDF, Office documents, SQLite databases and more,
  with a full built-in text editor in the F3 window.
- **Compare directories** (Shift+F2) *(Pro)* — two folder trees aligned side by side: same, different, or on one side only.
- **Find duplicate files** by content, and clean them up with undo.
- **Archives as folders** *(Pro)* — browse zip, 7z, rar, tar, iso and more like ordinary folders.
- **Remote SFTP tabs** — work on servers as if they were local folders *(Pro)*.
- **Everything search** built in, tabs, a folder tree, batch rename, checksums, custom commands *(Pro)*.
- **Portable** — one exe; settings live next to it in `config.toml`, applied the moment you save.
  An [AI agent skill](#ai-agent-skill) lets you change them by chatting.

## Download

Get the latest Windows build from **[Releases](https://github.com/kookob/obcommander/releases)** —
look for tags that start with `win-`.

- Windows 10 / 11, x64. Portable: no installer, nothing written to the registry.
- Markdown, HTML and PDF previews use Microsoft Edge WebView2, which ships with Windows 11.

| Platform | Status |
|---|---|
| Windows | Available |
| macOS | Planned |
| Linux | Planned |

## Pricing

- **Free for personal and home use** (non-commercial use) of the basic features — no account needed.
- **Commercial use** — any use for a company or organisation, or for work, including freelance work — is free to evaluate for 30 days, then requires a paid licence for each user.
- **Pro features** require a paid licence, including for personal use: the F3 viewer and Ctrl+Q quick view, browsing archives as folders, remembered folder sizes, folder compare, custom commands and remote SFTP. Try them free for 30 days from inside the app — no card, no account.
- One licence covers **2 computers** (say, work and home) and includes future updates. Licence holders get **email support**.
- Activating or starting a trial contacts our licence server **once**; after that the licence is checked offline. (The update check at start-up is separate, sends no personal data and can be turned off.)

The [LICENSE](LICENSE) defines these terms precisely. Pricing at [obcommander.com](https://obcommander.com).

## AI agent skill

`skills/obcmd-config` teaches an AI agent how to edit OB Commander's `config.toml` — colors, themes, fonts, columns,
shortcuts, toolbar, menus and more. It follows the open [Agent Skills](https://agentskills.io) format, so the same folder
works in any agent that supports it.

**Claude Code**

```
/plugin marketplace add kookob/obcommander
/plugin install obcmd@obcommander
```

**Other agents** — copy the `skills/obcmd-config` folder into the agent's skills directory:

| Agent | Skills directory |
|---|---|
| OpenAI Codex | `~/.codex/skills/` |
| Gemini CLI | `~/.gemini/skills/` (or `~/.agents/skills/`) |
| Claude Code (manual) | `~/.claude/skills/` |
| Other Agent Skills–compatible tools | see the tool's documentation |

```powershell
git clone --depth 1 https://github.com/kookob/obcommander "$env:TEMP\obcommander"
Copy-Item -Recurse "$env:TEMP\obcommander\skills\obcmd-config" "$HOME\.codex\skills\"
```

An MCP server is planned and will be installable the same way.

## Translations

The app ships in 9 languages: English, 简体中文, 繁體中文, Deutsch, Français, Español, Português (Brasil), Русский and 日本語.
More languages, how to install them and how to add your own: see [`lang/`](lang). Pull requests with new or corrected translations are welcome.

## Feedback

Bug reports and feature requests: [Issues](https://github.com/kookob/obcommander/issues).
Licence questions: [support@obcommander.com](mailto:support@obcommander.com).

This repository holds releases, documentation and agent integrations; the source code is not published here.

## License

OB Commander is proprietary software, free for personal and home use; see [LICENSE](LICENSE).
