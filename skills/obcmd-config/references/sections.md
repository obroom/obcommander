# Columns, shortcuts, menus, toolbar and custom commands

Command names used below (`cmd = "..."`, `[keys]` entries) are listed in [commands.md](commands.md).

## Columns (`columns`) — restart needed

| `col` | Header (en / zh) | Default width | Meaning |
|---|---|---|---|
| `name` | Name / 名称 | 280 | Always first; added even if omitted; can't be hidden |
| `ext` | Ext / 扩展名 | 70 | Extension without the dot; empty for folders |
| `size` | Size / 大小 | 110 | File size; folders show `<DIR>` until measured with Space; links `<LNK>` |
| `age` | Age / 距今 | 100 | Time since modification ("3 min", "2 days"), refreshed every minute; background by the `mtime_hours` / `mtime_colors` bands; sorts by modification time, newest first |
| `time` | Modified / 修改时间 | 210 | Format: `time_format` |
| `created` | Created / 创建时间 | 210 | Empty in Everything search results |
| `accessed` | Accessed / 访问时间 | 210 | Empty in Everything search results |
| `attrs` | Attrs / 属性 | 60 | `R` read-only `H` hidden `S` system `A` archive `L` link `C` compressed `E` encrypted, e.g. `HA` |
| `dup` | Grp / 组 | 50 | Duplicate group number; empty outside the Find Duplicates view |
| `comment` | Comment / 备注 | 220 | The user's own note on a file (Ctrl+Shift+M). Not shown by default — the status bar shows the note of the cursor row anyway |

Without `columns`, the default is `name ext size age time`.
Remote (SFTP) panels add **Mode** and **Owner** columns automatically; they aren't configured here.

Write it as an inline array — it can sit anywhere among the top-level keys:

```toml
columns = [
    { col = "name", min_width = 200 },                  # at least 200 px
    { col = "ext", fixed_width = 55 },                  # always 55 px, can't be dragged
    { col = "size", min_width = 90, max_width = 130 },  # draggable within 90–130
    { col = "age" },
    { col = "time" },
]
```

The `[[columns]]` table form also works but must come before all other tables.

Rules:
- Order = display order. Only listed columns exist.
- A misspelled `col` is ignored silently; if none are valid, the defaults return.
- A user who configured `columns` before the Age column existed must add `{ col = "age" }` to get it.
- **Restart obcmd** after changing `columns`.

**Widths** aren't normally in config: widths the user drags are remembered in `session.toml`. The three optional keys
only constrain them, and win over the remembered width: `min_width`, `max_width` (`0` = no limit), `fixed_width`
(locked; the divider can't be dragged). Priority: `fixed_width` > `min/max_width` > remembered width > default.

**Hide / show** a column temporarily: right-click the column header. The choices are the columns configured here.
Hidden = width 0 in `session.toml`, kept across restarts.

## Shortcuts (`[keys]`)

```toml
[keys]
copy   = "F5"             # command = key
delete = "F8 | Delete"    # several keys: separate with " | "
quickview = ""            # "" = unbind
```

Key names: `Ctrl`, `Shift`, `Alt` joined with `+`, and letters, digits, `F1`–`F24`, `Tab`, `Enter`, `Esc`, `Space`,
`Ins`, `Del`, `Backspace`, `Left`, `Right`, `Up`, `Down`, `Home`, `End`, `PgUp`, `PgDn`, `Apps`, `` ` `` (or `Backtick`).

A `[keys]` entry replaces that command's default keys. Defaults are in [commands.md](commands.md); the everyday ones:
F2 rename · F3 view · F4 edit · **F5 refresh** · **F6 new file** · F7 new folder · F8 / Del delete ·
Ctrl+Q quick view · Ctrl+D bookmark folder · Ctrl+B branch view · Ctrl+Shift+F search · Ctrl+Z / Ctrl+Y undo / redo ·
Ctrl+\` terminal · Ctrl+Shift+T reopen closed tab.

**Copy and move have no default key** (F5 is Refresh, and a mistaken F5 would copy without asking). For Total
Commander habits bind `copy = "F5"`, `move = "F6"`, and give `refresh` and `newfile` other keys.

**Drive / desktop / WSL jumps have no default key**; suggest free keys such as `Ctrl+F1`…`Ctrl+F12`
(avoid `Alt+digit`, often taken by other tools, and `Alt+F4`):

```toml
[keys]
drive_c = "Ctrl+F1"
drive_d = "Ctrl+F2"
desktop = "Ctrl+F3"
wsl_1   = "Ctrl+F4"
```

## Icons (`icon` in `[[toolbar]]`, `[[crumb]]`, `[[commands]]`)

Icons are glyphs of the system icon font (Segoe Fluent Icons on Windows 11, Segoe MDL2 Assets on Windows 10), so a
config only names a code point or a character:

```toml
icon = "E756"   # 4 hex digits (recommended), no U+ or 0x
icon = "★"      # or one character, drawn with the icon font
```

Only 4-digit code points (U+0000–U+FFFF) work; emoji such as U+1F4C1 don't. Find code points in Microsoft's list
(https://learn.microsoft.com/windows/apps/design/style/segoe-fluent-icons-font) or in `charmap.exe` with the
"Segoe Fluent Icons" font; icons sit in U+E700–U+F8FF.

Built-in icons (used when `icon` is omitted):

| Command | Code | Command | Code | Command | Code |
|---|---|---|---|---|---|
| back | E72B | forward | E72A | refresh | E72C |
| tree | E90C | branch | E81E | columns | F246 |
| search | E721 | compare | E89A | delete | E74D |
| copy | E8C8 | move | E8DE | mkdir | E8F4 |
| newfile | E7C3 | rename | E8AC | terminal | E756 |
| properties | E946 | swap | E8AB | favorites / fav_toggle | E735 |

Other commands have no icon: a toolbar button falls back to its text, an address-bar button shows `?`.

## What can be configured

| Menu / bar | Configurable | Where |
|---|---|---|
| Top menu bar | yes | `[[menu]]` |
| Toolbar | yes | `[[toolbar]]` |
| Address-bar buttons, and the ▾ of Copy Path | yes | `[[crumb]]`, `[[crumb.items]]` |
| File list right-click menu | yes | `[[context]]` (on an item), `[[context_bg]]` (on empty space) |
| Column header menu | indirectly | its choices are the configured `columns` |
| Panel Layout submenu, favorites ★ list, search history ▾ | no | |
| Right-click in the tree, column view, Recycle Bin, remote and archive folders | no | |

`[[menu]]`, `[[toolbar]]`, `[[crumb]]`, `[[context]]` and `[[context_bg]]` each **replace** the default completely.
Items' `text` is optional (the command's own label is used); never write the shortcut into `text` — it is added from `[keys]`.
Toggle items (tree, quick view, branch, checkboxes, tab lock…) get their check marks automatically.

## Top menu (`[[menu]]`)

Default structure (`-` = separator; *(sub)* = submenu; *pseudo* = special item described below):

- **File (文件)**: newfile mkdir copy move - clip_cut clip_copy clip_paste rename multi_rename view edit delete
  *(sub)* Copy Path [copy_name copy_dir copy_path copy_wsl - copy_all_names copy_all_paths] comment
  - undo redo - pack extract *(sub)* Checksums [checksum - checksum_create checksum_verify]
  - dirsize_all search dup compare properties - quit
- **Mark (标记)**: sel_toggle sel_all sel_invert - sel_pattern_add sel_pattern_sub
  - *(sub)* Keep in Each Group… [dup_keep_shortest dup_keep_oldest dup_keep_cursor]
- **Commands (命令)**: back forward refresh *(sub)* Tabs [tab_new tab_close tab_reopen tab_lock - tab_prev tab_next tab_list]
  - path fav_toggle favorites - terminal *sftp* - *user_commands*
- **View (视图)**: quickview - tree *tree_follow* - branch columns checkboxes - switch_panel swap *layout* - *theme*
- **Options (配置)**: *language* - open_config
- **Help (帮助)**: docs homepage feedback - check_update - license about

Pseudo items (use as `cmd`): `layout` = Panel Layout submenu (1×1 single panel … 3×3), `theme` = light/dark,
`language` = available languages, `tree_follow` = tree-following modes, `sftp` = hosts from `~/.ssh/config`,
`user_commands` = the `[[commands]]` entries. In single-panel mode `switch_panel` is hidden automatically.

```toml
[[menu]]
title = "&File"            # & marks the Alt access key
[[menu.items]]
cmd = "copy"
[[menu.items]]
cmd = "-"                  # separator
[[menu.items]]
text = "Copy Path"         # submenu: text without cmd, then [[menu.items.items]]
[[menu.items.items]]
cmd = "copy_name"
[[menu.items.items]]
cmd = "copy_path"
[[menu.items]]
cmd = "layout"
```

## Toolbar (`[[toolbar]]`)

Default: back forward refresh - tree branch columns search - delete. (Favorites live on the drive bar's ★; add
`cmd = "favorites"` to put them on the toolbar. Compare isn't on it by default: `cmd = "compare"`.)

```toml
[[toolbar]]
cmd = "tree"        # "-" = separator
text = "Tree"       # tooltip; shown next to the icon when toolbar_text = true
icon = "E90C"       # optional
```

## Address-bar buttons (`[[crumb]]`)

Default: terminal, fav_toggle (bookmark star), copy_path (split button; its ▾ opens a menu).
The ▾ menu default: copy_wsl (WSL path of the **current folder**) - copy_all_names copy_all_paths.
Without an `icon`, the star shows filled when bookmarked, Copy Path shows a check mark after copying, and the column-view
button stays lit while on — setting `icon` loses those effects. Other commands work too (they act on that panel).

```toml
[[crumb]]
cmd = "terminal"
[[crumb]]
cmd = "fav_toggle"
[[crumb]]
cmd = "copy_path"
[[crumb.items]]           # the ▾ menu (only copy_path has one)
cmd = "copy_all_names"
[[crumb.items]]
cmd = "-"
[[crumb.items]]
cmd = "copy_wsl"
```

## File list right-click menu (`[[context]]`, `[[context_bg]]`)

Same item format as `[[menu.items]]`, plus two pseudo commands for the Windows (shell) context menu:
`shell_more` = shell menu folded into a "Show More Options" submenu, loaded only when hovered (default, fast);
`shell` = shell menu inline, loaded on every right-click (slow with many shell extensions). Neither = no shell menu.

Defaults:
- On an item: clip_cut clip_copy clip_paste rename view edit delete - copy move - *(sub)* Copy Path
  [copy_name copy_dir copy_path copy_wsl - copy_all_names copy_all_paths] comment pack extract - terminal properties - shell_more
- On empty space: newfile mkdir - clip_paste - refresh undo redo - terminal - shell_more

Commands act on what was right-clicked: an unselected row alone, or the whole selection when a selected row was
clicked. `[[commands]]` names can be used here too.

## Custom commands (`[[commands]]`)

Each entry runs an external command line. It appears under **Commands > User Commands (命令 > 用户命令)** and can be
bound in `[keys]` or placed in `[[toolbar]]` / `[[menu]]` / `[[context]]` by its `name`.
**Commands > User Commands > Add a Command… (添加自定义命令…)** appends a commented template to config.toml.

| Field | Meaning |
|---|---|
| `name` | **Required.** Name to reference it by; ignored if it clashes with a built-in command |
| `run` | **Required.** The command line |
| `text` | Menu label; default = `name` |
| `icon` | Toolbar icon (see Icons) |
| `cwd` | Working directory (placeholders allowed); default = the panel's folder, **not** the exe folder |
| `confirm` | Show the expanded command line and ask first |
| `each` | Run once per selected item (asks first above 20); default = once with all items |
| `wait` | Wait for it to finish: failures show the error output, and `refresh` becomes possible |
| `hide` | No console window (only with `wait = true`) |
| `refresh` | Refresh the panel afterwards (only with `wait = true`) |

Use `wait = true` for tools that finish (converters, packers). Long-running programs (editors, servers) need
`wait = false`, or obcmd waits forever.

Placeholders (anything else in `{...}` is left alone, so PowerShell braces are safe):

| Placeholder | Expands to |
|---|---|
| `{dir}` / `{dir2}` | Current panel folder / other panel folder (`{dir}` in single-panel mode) |
| `{app}` | Folder of obcmd.exe (for scripts shipped next to it, e.g. `{app}\scripts\x.ps1`) |
| `{cur}` | Full path of the cursor item |
| `{cur_name}` / `{cur_base}` / `{cur_ext}` | File name / name without extension / extension without the dot |
| `{sel}` | All selected items, **each quoted automatically**, space-separated |
| `{sel_list}` | Path of a temporary file listing the selected items, one per line |
| `{sel_count}` | Number of selected items |

- Only `{sel}` is quoted automatically — quote the others yourself: `"{dir}"`.
- With hundreds of files use `{sel_list}`: the command line is limited to about 32,000 characters.
- TOML `'...'` strings can't contain a single quote. Put PowerShell one-liners in a `.ps1` file, or use `'''...'''`.

```toml
[[commands]]
name = "webp"
text = "Convert to WebP (85%)"
run  = 'magick mogrify -format webp -quality 85 {sel}'
wait = true
hide = true
refresh = true

[[commands]]
name = "h265"
text = "Encode H.265 into the other panel"
run  = 'ffmpeg -i "{cur}" -c:v libx265 -crf 26 -c:a copy "{dir2}\{cur_base}.mp4"'
each = true
wait = true
confirm = true
refresh = true

[[commands]]
name = "serve"
text = "HTTP server here"
run  = 'python -m http.server 8000 --directory "{dir}"'   # keeps running: no wait

[keys]
webp = "Ctrl+Shift+W"
```
