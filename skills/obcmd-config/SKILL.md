---
name: obcmd-config
description: Configure the OB Commander (obcmd) file manager by editing its config.toml — colors, themes, fonts, columns, keyboard shortcuts, toolbar, menus, preview, search and more. Use when the user mentions obcmd, OB Commander or its config.toml, or asks to change how the file manager looks or behaves. 通过聊天配置 OB Commander (obcmd) 文件管理器 — 改配色/字体/列/快捷键/工具栏/菜单/预览/搜索等。用户提到 obcmd、OB Commander、"改一下文件管理器的配置"、config.toml 时使用。
---

# Configuring OB Commander

OB Commander (`obcmd.exe`) is a dual-pane file manager for Windows. It has no settings window:
**everything lives in `config.toml` next to `obcmd.exe`** (it is portable). A saved change applies
immediately (hot reload). The one exception is `columns`, which needs a restart.

Reply in the user's language. Menu names below are given in English and Chinese, e.g. **View > Theme (视图 > 主题)**;
give both. If the user's UI is in another language, the menus are in the same places — describe the position
(e.g. "the fourth menu, View") and give the English name.

## Workflow

1. **Find the file**: `config.toml` in the same folder as `obcmd.exe`. If you don't know where that is,
   ask the user, or tell them to use **Options > Open config.toml (配置 > 打开配置文件)**.
   No file = all defaults; just create it.
2. **Read before you edit**: change only the keys the user asked about; keep every other line, comments included.
3. **TOML rules that bite**:
   - **Top-level keys (`key = value`) must come before every table** — `[keys]`, `[wsl_labels]`, `[[columns]]`,
     `[[toolbar]]`, `[[crumb]]`, `[[menu]]`, `[[context]]`, `[[context_bg]]`, `[[commands]]`.
     A key written after a table header belongs to that table and silently does nothing.
   - Colors are strings `"#RRGGBB"`; `""` = use the theme / system color.
   - For numbers, `0` usually means "automatic / follow the system / no limit" — see each key.
   - A table like `[[menu]]`, `[[toolbar]]`, `[[crumb]]`, `[[context]]` or `columns` **replaces** the built-in
     default entirely; it does not append. To add one item, copy the whole default and edit it.
4. **A file that fails to parse is ignored** (the program keeps the last good settings), so the user just sees
   "nothing happened". After editing, check the TOML is valid.
5. **Tell the user** it applies on save — except `columns`, which needs obcmd restarted.

## Where to look

Read only the reference file you need:

| The user wants to change… | Read |
|---|---|
| Theme, dark mode, colors, fonts, sizes of bars and borders, row colors by modification time | [references/settings.md](references/settings.md) — Appearance |
| Panel layout, drag & drop, terminal, time format, language, close button, auto-save, tree, drive bar | [references/settings.md](references/settings.md) — Behavior |
| Folder sizes, duplicates, checksums, preview limits, Everything search, compare folders, favorites, SFTP, archives | [references/settings.md](references/settings.md) — Features |
| Which columns show, column widths, the Comment column | [references/sections.md](references/sections.md) — Columns |
| Keyboard shortcuts | [references/sections.md](references/sections.md) — Shortcuts, plus [references/commands.md](references/commands.md) |
| Top menu, toolbar, address-bar buttons, right-click menu, icons | [references/sections.md](references/sections.md) |
| Their own commands (run a script / tool on the selected files) | [references/sections.md](references/sections.md) — Custom commands |
| A command name for `[keys]` / `cmd =` | [references/commands.md](references/commands.md) |
| Favorites, search history, session (tabs, column widths), search/compare exclusion lists | [references/other-files.md](references/other-files.md) — these are **not** in config.toml |

## Common requests

**Dark mode** — `theme = "dark"`, nothing else. The whole window follows (lists, bars, scrollbars, title bar,
dialogs, previews). Don't build dark mode out of individual color keys: the bars, scrollbars and dialogs would
stay light. The user can also switch in **View > Theme (视图 > 主题)**, which writes the same key.

**Bigger text** — `font_size` (file list, tree, preview) and `ui_font_size` (toolbar, tabs, address bar, status bar), in points; `0` = system.

**Total Commander keys** — copy and move have no default key (F5 is Refresh, F6 is New File). For TC habits:

```toml
[keys]
copy    = "F5"
move    = "F6"
refresh = "Ctrl+R"
newfile = "Shift+F4"
```

**Show more columns** — `columns` (restart needed); see references/sections.md for names and width limits:

```toml
columns = [ { col = "name" }, { col = "ext" }, { col = "size" }, { col = "age" }, { col = "time" }, { col = "attrs" } ]
```

**Run their own tool on the selection** — a `[[commands]]` entry; see references/sections.md.

## Not in config.toml

| File (next to obcmd.exe) | Holds | Close obcmd before editing? |
|---|---|---|
| `obcmd.db` | favorites, search history, folder-size cache, comments | **yes** (SQLite, held open) |
| `session.toml` | tabs, column widths and hidden columns, window position, panel split | **yes** (rewritten on exit) |
| `search_exclude.txt` / `compare_exclude.txt` | folders skipped by search / compare | no, applies on save / next compare |
| `lang/*.toml` | UI text, extra languages | restart |

Details: [references/other-files.md](references/other-files.md).
