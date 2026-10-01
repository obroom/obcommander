# Files next to obcmd.exe besides config.toml

When the user asks about these, don't look in `config.toml`.

| File | Holds | Close obcmd before editing? |
|---|---|---|
| `obcmd.db` | favorites, search history, folder-size cache, comments | **yes** — SQLite, held open by the program |
| `session.toml` | tabs, column widths, hidden columns, window position, panel split | **yes** — rewritten from memory on exit |
| `search_exclude.txt` | folders left out of Everything search results | no — applies on save |
| `compare_exclude.txt` | names left out of Compare Folders | no — applies on the next compare |
| `lang/*.toml` | UI text; extra languages | restart |

## search_exclude.txt

One folder name per line; `#` starts a comment. Results whose path contains `\name\` are dropped. Subpaths work
(`.cargo\registry`). Saving applies immediately, even to a search in progress. The funnel button in the search bar
turns the whole list off temporarily.

Created with these defaults when missing:
`node_modules`, `.git`, `.svn`, `.hg`, `target`, `__pycache__`, `.venv`, `.cargo\registry`, `.rustup`,
`$RECYCLE.BIN`, `System Volume Information`.
To exclude another folder, append a line such as `dist`.

## compare_exclude.txt

Same format. Created on the first compare. Matches files and folders (a name equal to an entry, or a path ending
in `\entry`). Applies on **Recompare**; the compare bar's Exclude button turns it off temporarily.
Defaults: `.git`, `.svn`, `.hg`, `node_modules`, `target`, `__pycache__`, `.venv`, `.idea`, `.vs`, `$RECYCLE.BIN`,
`System Volume Information`, `Thumbs.db`, `desktop.ini`, `.DS_Store`.

## session.toml

Maintained by the program: written every `autosave_seconds` and on exit.

```toml
single / active / tree_on / tree_w / preview_zoom / preview_web_zoom   # global state
col_fracs / row_fracs            # panel divider positions (fractions)
[window]                         # x y w h maximized
[[panels]]                       # one per panel
cur = 0                          # current tab index
[[panels.tabs]]                  # path / sort / desc / locked
[panels.col_widths]              # widths by column name; 0 = hidden
```

The one edit worth making by hand: to reset a column's width, **quit obcmd**, delete its line under
`[panels.col_widths]` (or the whole section), then start obcmd. Deleting the whole file is safe too — layout and
folders go back to defaults. Editing while obcmd runs is pointless: it overwrites the file on exit.

## obcmd.db

SQLite:

| Table | Columns | Normally managed by |
|---|---|---|
| `favorites` | path (primary key, case-insensitive) / name / added | ★ list (✕ removes), address-bar star, Ctrl+D |
| `searches` | text (primary key) / used / hits / last | the search box; up to 500 kept, the ▾ menu shows 20 |
| `dirsizes` | path / parent / bytes / mtime / used | measuring folders with Space; limited by `dirsize_db_max_mb` |
| `comments` | path (primary key, case-insensitive) / parent / note / updated | Ctrl+Shift+M or right-click **Edit Comment (编辑备注)** |

Day-to-day use happens in the UI. For bulk changes, **quit obcmd first**, then use any SQLite client:

```sql
INSERT OR IGNORE INTO favorites(path, name, added)
VALUES ('d:\code', 'Code', strftime('%s','now'));
```

Paths are stored normalized and lower-case, without a trailing backslash (except drive roots like `d:\`).
To clear the size cache: `DELETE FROM dirsizes;` after quitting. Deleting `obcmd.db` also deletes favorites, search
history and comments; delete `obcmd.db-wal` and `obcmd.db-shm` along with it.

An old `[[favorites]]` list in config.toml is imported once, only while the favorites table is empty; afterwards it
can be deleted.

## lang/*.toml

The UI text. The built-in languages are embedded in the exe; files in the `lang/` folder next to it are added at
startup and can add languages or override built-in text.

- **Add a language**: start from `en.toml` in the `lang/` folder of https://github.com/obroom/obcommander (the
  built-in languages are published there), rename it to a language tag (e.g. `ja-JP.toml`), translate the right-hand
  sides, put it in the `lang/` folder next to obcmd.exe, restart. Its first line `name = "…"` is the name shown in
  **Options > Language (配置 > 语言)**. Missing keys fall back to English. Translations can be contributed there.
- **Change built-in text**: a file with the same name (e.g. `lang/en.toml`) overrides the built-in one key by key —
  it only needs the lines being changed.
- `{name}`-style placeholders are filled in at runtime; they can move within a sentence but must stay.
