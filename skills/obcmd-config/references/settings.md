# Top-level settings

All of these are plain `key = value` lines at the **top** of `config.toml`, before any `[table]` or `[[table]]`.
All apply on save. Colors are `"#RRGGBB"`; `""` = theme / system color.

## Appearance

| Key | Type | Default | Meaning |
|---|---|---|---|
| `theme` | string | `""` = `"graphite-emerald"` | Whole color scheme: `graphite`, `graphite-emerald`, `emerald`, `teal`, `amber`, `mono`, `dark`. The single-color keys below override it |
| `bg_color` | color | `""` | Background of the file list, folder tree and preview. `""` = theme, then system |
| `text_color` | color | `""` | Text on that background. `""` = theme; if the theme has none, black or white by `bg_color` brightness. Gray text (cut rows, stale sizes) is mixed from these two automatically |
| `font_name` | string | `""` | Font of the file list and tree. `""` = system message font. A monospace font here makes the whole list monospace |
| `font_size` | int (pt) | `0` | File list, tree and preview text size. `0` = system. 14 or more switches to 32 px icons |
| `mono_font` | string | `""` | Monospace font for text previews and the remote "Mode" column. `""` = Consolas |
| `ui_font_size` | int (pt) | `0` | Toolbar, drive bar, tabs, address bar, status bar. Row heights follow it |
| `active_color` | color | theme | Accent of the active panel (tab and drive button tint) |
| `inactive_color` | color | theme | Same for inactive panels |
| `border_color` | color | theme | Border around the active panel |
| `prev_border_color` | color | `""` | With more than two panels: border of the previously active panel (the copy/move target). `""` = faded border color |
| `cursor_color` | color | `""` = `#99C8FF` (dark theme `#264F78`) | Background of the cursor row (where the arrow keys / a click put you). Inactive panels use `inactive_color` |
| `selected_color` | color | theme (`#E91E63` in the default theme) | Color of selected (marked) files |
| `selected_style` | string | `""` = `"text"` | `"text"`: selected files only change text color (Total Commander style). `"fill"`: the whole row gets a background |
| `selected_bg_color` | color | `""` | Row background for `"fill"`. `""` = a light tint of `selected_color` |
| `drive_color` | color | `""` | Background of the current drive's button on the drive bar. `""` = tint of the active / inactive color |
| `mtime_hours` | int list | `[1, 24, 168]` | Age bands in hours for coloring rows by modification time |
| `mtime_colors` | color list | `["#9C27B0", "#3F51B5", "#009688"]` | Color per band (purple / indigo / teal). `[]` turns the feature off |
| `splitter_width` | int (px) | `0` = 4 | Width of the draggable bar between panels (and between the tree and the panels) |
| `active_border` | int (px) | `0` = 5 | Width of the active panel's border |
| `toolbar_text` | bool | `false` | Show labels next to toolbar icons |
| `toolbar_height` | int (px) | `0` | Toolbar row height. `0` = text height + 9 |
| `toolbar_icon_size` | int (px) | `0` | Toolbar icon size. `0` = automatic |
| `drive_height` | int (px) | `0` | Drive bar row height. `0` = text height + 12 |
| `preview_icon_size` | int (px) | `0` | Icons of the preview's small toolbar. `0` ≈ 24 px. Applies to newly opened previews |
| `marquee_fill` / `marquee_border` | color | `"#AACCEE"` | Rubber-band selection rectangle (drag on empty space) |
| `tab_buttons` | bool | `true` | The `[+][◂][▸][▾]` buttons at the right of the tab bar. Without them: double-click the empty tab bar, or bind `tab_new` / `tab_scroll_left` / `tab_scroll_right` / `tab_list` |

### Which key colors what

```
┌ Menu bar ───────────────── follows the theme (drawn by obcmd)
├ Toolbar ────────────────── theme background; height toolbar_height, icons toolbar_icon_size
├ Drive bar [C:][D:][★] ──── current drive button: drive_color (""= tint of active/inactive color)
├ Tab bar ────────────────── current tab: active_color; inactive panel: inactive_color
├ Address bar, column header  same background as the list
│ ┌─────────────────────────┐
│ │ File list  ← bg_color    │ ← the tree and the preview too; text: text_color
│ └─────────────────────────┘
├ Status bar ─────────────── theme background
└ Panel border ───────────── border_color (active) / prev_border_color (previously active)
```

**`bg_color` only covers the file list, tree and preview.** The toolbar, drive bar, tab bar and status bar have no
key of their own — they follow `theme`. For an overall light/dark change use `theme`.

**Dark mode is `theme = "dark"`** (also **View > Theme (视图 > 主题)**, which writes this key). Everything follows:
lists, bars, menu bar, scrollbars, column headers, title bar, dialogs, previews. Fine-tune by overriding after it,
e.g. `bg_color = "#101010"` (text turns light automatically). Only drop-down boxes and buttons inside dialogs stay light
(Windows provides no dark style for them).
Single-color keys written with fixed values don't follow a theme switch — leave them `""` if the user wants the
menu switch to keep working.

**Theme vs. single colors**: `active_color`, `inactive_color`, `border_color`, `selected_color`, `bg_color`,
`text_color` and `cursor_color` override the theme when set, and follow it when `""`.
"Graphite theme but a green border" = `theme = "graphite"` + `border_color = "#0E9F6E"`.
The first six themes are light (background follows the system); only `dark` brings its own background.

### Row colors

Priority, highest first:

| Case | Effect | Keys |
|---|---|---|
| 1. Selected (Space / Insert / checkbox / Ctrl+click) | `"text"`: text color only; `"fill"`: row background | `selected_color`, `selected_style`, `selected_bg_color` |
| 2. Cursor row | Row background, black/white text picked automatically | `cursor_color`; inactive panels `inactive_color` |
| 3. Stale folder size (folder changed since measured) | Only the Size cell turns gray | not configurable |
| 4. Modification-time bands | Text color | `mtime_hours`, `mtime_colors` |
| 5. Everything else | Normal text color | |

Mouse hover never covers the cursor row or a filled selected row.

**Cursor vs. selection** (Total Commander model): the cursor is *where you are* (one row, moved by arrow keys or a click);
selection is *what is marked* (any number of rows, toggled with Space). A row can be both.

### Coloring by modification time

The two lists pair up by position; the shorter one decides how many bands exist:

```toml
mtime_hours  = [1, 24, 168]                        # hours
mtime_colors = ["#9C27B0", "#3F51B5", "#009688"]   # purple / indigo / teal
#               < 1 hour    < 24 hours  < 7 days      older = normal color
```

- "Younger than N hours" — order doesn't matter, the program sorts the bands.
- A 30-day band: 30 × 24 = **720** → `mtime_hours = [1, 24, 168, 720]`, plus a fourth color.
- Handy values: 1 day 24 · 3 days 72 · 7 days 168 · 15 days 360 · 30 days 720 · 90 days 2160 · 1 year 8760.
- Off: `mtime_colors = []`.
- A band with a malformed color is skipped silently.
- The default colors avoid the selection color (magenta `#E91E63`); keep it that way, or "new file" and "selected" look alike.
- On the dark theme the default colors have low contrast; suggest brighter ones.
- The **Age** column's cell background uses the same bands.

## Behavior

| Key | Type | Default | Meaning |
|---|---|---|---|
| `layout_rows` / `layout_cols` | int | `1` / `2` | Panel grid, up to 4 × 4. Also **View > Panel Layout (视图 > 面板布局)** |
| `drag_default` | string | `"copy"` | Plain drag & drop: `"copy"`, `"move"`, or `"auto"` (same drive moves, other drive copies). Ctrl = copy, Shift = move, Ctrl+Shift = shortcut, right-drag = menu always win. Dropping onto a folder in the same directory always moves |
| `terminal` | string | `""` | Command for "Open in Terminal". `{dir}` = target folder (quoted automatically). `""` = Windows Terminal new window, or cmd without it. Examples: `"wt.exe -w 0 nt -d {dir}"` (new tab in the open WT window), `"pwsh.exe"` (fastest), `"cmd.exe"`. The program name must not contain spaces — use a name found on PATH |
| `time_format` | string | `""` | Time columns. `""` = ISO `2026-09-22 15:07:09` (sorts correctly). `"system"` = Windows regional format. Custom: `yyyy yy MM M dd d HH H hh h mm ss tt`, other characters are copied, e.g. `"dd.MM.yyyy HH:mm"` |
| `language` | string | `""` | UI language as a language tag, e.g. `"en"`, `"zh-CN"`. The available ones are listed in **Options > Language (配置 > 语言)**, which also writes this key. `""` = Windows UI language; unknown values fall back to English |
| `close_action` | string | `""` = `"exit"` | What the window's × button does: `"exit"`, `"minimize"`, `"tray"`. Alt+F4 and **File > Exit (文件 > 退出)** always quit; with `"tray"` the tray icon's menu can quit too |
| `autosave_seconds` | int | `10` | Save session and caches every N seconds (only if changed). `0` = only on exit |
| `confirm_root_delete` | bool | `true` | Ask before deleting a first-level item of a drive or network share (`D:\code`, `C:\Windows`) |
| `list_checkboxes` | bool | `false` | A checkbox at the start of each row; ticking = selecting (same as Space) |
| `sync_columns` | bool | `false` | Dragging a column width changes it in the other panels too |
| `status_dir_items` | bool | `true` | Status bar shows how many folders/files the folder under the cursor contains (one level) |
| `status_load_ms` | int | `200` | Show a folder's load time in the status bar only when slower than this. `0` = always |
| `tree_follow` | string | `""` = `"collapse"` | How the folder tree follows the panel: `"collapse"` (expand to current, collapse others), `"expand"` (keep others open), `"select"` (highlight only if visible), `"off"`. Also **View > Tree Follows Panel (视图 > 目录树跟随)**. The old `tree_sync = false` means `"off"` when `tree_follow` is unset |
| `drive_bar_extras` | string list | `["desktop"]` | Buttons after the drives on the drive bar, in order: `desktop`, `home`, `documents`, `downloads`, `pictures`, `recycle`, or any folder path (`%ENV%` variables work). Missing paths are hidden. Right-click the recycle button = empty the Recycle Bin |
| `wsl_hide` | string list | `[]` | WSL distributions not shown, e.g. `["docker-desktop"]` |
| `wsl_labels` | table | `{}` | Display names, e.g. `wsl_labels = { "Ubuntu-22.04" = "wsl" }` |
| `branch_max_files` | int | `50000` | Branch view (Ctrl+B) refuses to flatten more files than this without asking |
| `check_update` | bool | `true` | Check for a new version once at startup (a static JSON; nothing about the machine is sent). Off = only **Help > Check for Updates (帮助 > 检查更新)** |

## Features

### Folder sizes (Space / Shift+Space)

| Key | Default | Meaning |
|---|---|---|
| `dirsize_confirm_gb` | `4.0` | Ask before recalculating a folder last measured above this size |
| `dirsize_reuse_cache` | `true` | Reuse cached first-level subfolder sizes whose modification time hasn't changed. Shift+Space forces a full recount |
| `dirsize_cache_depth` | `2` | While measuring, cache every subfolder up to this depth |
| `dirsize_cache_min_mb` | `10` | Deeper than that, cache only folders at least this big |
| `dirsize_db_max_mb` | `200` | Size limit of the cache in `obcmd.db`; oldest entries are dropped at startup. `0` = no limit |

### Duplicates and checksums

| Key | Default | Meaning |
|---|---|---|
| `dup_min_mb` | `10` | Find Duplicates only looks at files this big or larger. `0` = all sizes |
| `dup_confirm_gb` | `20.0` | Ask first when the candidates add up to more than this. `0` = never ask |
| `checksum_confirm_mb` | `256` | Ask before checksumming a single file larger than this (MB, not GB). `0` = never ask |

### Preview (Ctrl+Q quick view / F3 viewer / F4 edit)

| Key | Default | Meaning |
|---|---|---|
| `preview_max_mb` | `10` | Other file types (thumbnails, binaries) above this aren't previewed |
| `preview_image_max_mb` | `10` | Images |
| `preview_text_max_mb` | `10` | Markdown / HTML / JSON rendering; larger files show as plain text. Plain text and code have no limit |
| `preview_db_mem_mb` | `64` | SQLite databases up to this size are read into memory (the file isn't held open); larger ones are opened read-only in place. `0` = always in place |
| `preview_handler` | `true` | Use the system's preview handlers for Office, RTF, `.msg` and similar (starts Office in the background). Off = thumbnail only |
| `preview_html_script` | `true` | Let scripts run in previewed `.html` / `.svg` files. `false` = static rendering only (safer for untrusted pages) |
| `quickview_popup` | `false` | Ctrl+Q inside an archive or a remote folder: `false` asks whether to open the F3 viewer; `true` opens it without asking |

Markdown, HTML, PDF, audio and video previews need Microsoft Edge WebView2 (built into Windows 11).

### Everything search (Ctrl+Shift+F)

Needs [Everything](https://www.voidtools.com/) 1.4 or 1.5 running.

| Key | Default | Meaning |
|---|---|---|
| `everything_instance` | `""` | Everything instance name. Everything 1.5's default install is `"1.5a"`; 1.4 or no instance name = `""` |
| `everything_max_results` | `2000` | Maximum results fetched |
| `everything_min_chars` | `3` | Don't search with fewer characters (a CJK character counts as 1.5) |

### Compare folders (Shift+F2)

| Key | Default | Meaning |
|---|---|---|
| `compare_confirm_files` | `200000` | Pause and ask when the scan passes this many items (or runs longer than 5 s). `0` = never ask |

### Favorites (the ★ on the drive bar, Ctrl+D)

| Key | Default | Meaning |
|---|---|---|
| `favorites_filter_min` | `10` | Show the filter box only when there are more favorites than this. `0` = always |
| `favorites_keys` | `true` | Shortcut column (1–9, 0, a–z) in the favorites popup |
| `favorites_focus` | `"keys"` | With shortcuts and a filter box: `"keys"` focuses the list, `"filter"` focuses the filter box |
| `favorites_show_name` | `false` | Show a Name column besides the path |

The favorites themselves are stored in `obcmd.db`, not here.

### Remote SFTP (Pro)

Hosts come from `~/.ssh/config` (the tree's Remote group, or type `sftp://host/path` in the address bar). Uses the system's `ssh.exe` and your existing keys.

| Key | Default | Meaning |
|---|---|---|
| `sudo_hosts` | `[]` | Host aliases to open as root (`sudo -n sftp-server`); needs password-less sudo on the server |
| `sftp_server` | `""` | Path of `sftp-server` for those hosts. `""` = look in the usual places |

### Archives

Enter opens archives like folders; Alt+F6 extracts, Alt+F5 packs.

| Key | Default | Meaning |
|---|---|---|
| `sevenzip` | `""` | Path of `7z.exe`. `""` = search PATH and Program Files. Without 7-Zip, packing uses Windows' `tar.exe` |
| `archive_exts` | `[]` | Extra extensions to treat as archives, without the dot, e.g. `["pak"]`. Common 7-Zip formats are built in. Added ones are read-only |
