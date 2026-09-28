# Command names

Use these in `[keys]` (`name = "key"`) and as `cmd = "..."` in `[[menu]]`, `[[toolbar]]`, `[[crumb]]`,
`[[context]]` and `[[context_bg]]`. "—" = no default key. Names of `[[commands]]` entries work the same way.

## Panels and tabs

| Command | Does (en / zh) | Default key |
|---|---|---|
| `switch_panel` | Switch active panel / 切换活动面板 | Tab |
| `single` | Single-panel mode / 单窗模式 | Ctrl+Shift+P |
| `swap` | Swap panels / 交换面板 | Ctrl+U |
| `layout_RxC` | Panel layout, e.g. `layout_2x2` (1–4 each) / 面板布局 | — |
| `tab_new` / `tab_close` | New tab / close tab / 新建 / 关闭标签 | Ctrl+T / Ctrl+W |
| `tab_reopen` | Reopen closed tab / 重新打开关闭的标签 | Ctrl+Shift+T |
| `tab_next` / `tab_prev` | Next / previous tab / 下一个 / 上一个标签 | Ctrl+Tab / Ctrl+Shift+Tab |
| `tab_lock` | Lock tab (navigation opens new tabs) / 锁定标签 | Ctrl+L |
| `tab_list` | All tabs… / 全部标签… | — |
| `tab_scroll_left` / `tab_scroll_right` | Scroll the tab bar / 标签栏左滚 / 右滚 | — |
| `quit` | Exit / 退出 | Alt+F4 |

## Navigation

| Command | Does | Default key |
|---|---|---|
| `back` / `forward` | Back / forward / 后退 / 前进 | Alt+Left / Alt+Right |
| `path` | Edit the address bar / 编辑地址栏 | Alt+D |
| `refresh` | Refresh / 刷新 | F5 |
| `favorites` | Favorites list / 收藏夹 | — (the ★ on the drive bar) |
| `fav_toggle` | Bookmark current folder / 收藏当前目录 | Ctrl+D |
| `drive_a` … `drive_z` | Go to that drive (nothing if absent) / 跳到该盘 | — |
| `desktop` | Go to the desktop / 桌面 | — |
| `recycle_bin` | Open the Recycle Bin / 回收站 | — |
| `wsl_1` … `wsl_10` | Go to the Nth WSL distribution (drive-bar order) / 第 N 个 WSL 发行版 | — |
| `tree` | Folder tree on/off / 目录树 | Ctrl+Shift+E |
| `branch` | Branch view: flatten subfolders / 分支视图 (平铺子目录) | Ctrl+B |
| `columns` | Column view (Finder-style) / 分栏视图 | — |
| `checkboxes` | Row checkboxes on/off / 行首复选框 | — |

## Files

| Command | Does | Default key |
|---|---|---|
| `copy` / `move` | Copy / move to the other panel / 复制 / 移动到另一面板 | — (TC habit: F5 / F6) |
| `newfile` | New file / 新建文件 | F6 |
| `mkdir` | New folder / 新建文件夹 | F7 |
| `rename` | Rename / 重命名 | F2 |
| `multi_rename` | Multi-rename / 批量重命名 | Ctrl+M |
| `delete` | Delete (Shift = permanently) / 删除 | F8, Delete |
| `undo` / `redo` | Undo / redo file operations / 撤销 / 重做 | Ctrl+Z / Ctrl+Y |
| `clip_copy` / `clip_cut` / `clip_paste` | Clipboard copy / cut / paste / 复制 / 剪切 / 粘贴 | Ctrl+C / Ctrl+X / Ctrl+V |
| `copy_path` | Copy full path / 复制完整路径 | Ctrl+Shift+C |
| `copy_dir` | Copy containing folder path / 复制所在文件夹路径 | Ctrl+Shift+D |
| `copy_name` | Copy file name / 复制文件名 | Ctrl+Shift+N |
| `copy_wsl` | Copy WSL path / 复制 WSL 路径 | — |
| `copy_all_names` / `copy_all_paths` | Copy all names / full paths in the folder / 目录内全部文件名 / 完整路径 | — |
| `pack` / `extract` | Pack / extract archives / 打包 / 解压 | Alt+F5 / Alt+F6 |
| `comment` | Edit comment / 编辑备注 | Ctrl+Shift+M |
| `properties` | Properties / 属性 | Alt+Enter |
| `context_menu` | Windows context menu / 系统右键菜单 | Shift+F10, Apps |
| `terminal` | Open in terminal / 在终端中打开 | Ctrl+\` |
| `dirsize_all` | Calculate all folder sizes / 计算所有文件夹大小 | Alt+Shift+Enter |

## View, preview and tools

| Command | Does | Default key |
|---|---|---|
| `quickview` | Quick view: preview in the other panel / 快速查看 | Ctrl+Q |
| `view` | View in its own window / 查看 | F3 |
| `edit` | Edit a text file in the viewer window / 编辑 | F4 |
| `search` | Everything search bar / Everything 搜索 | Ctrl+Shift+F |
| `search_scope` | Search scope: current folder / all drives / 搜索范围 | Ctrl+Alt+Enter |
| `locate` | Open a search result's folder in the other panel / 定位到文件 | Ctrl+Enter |
| `filter_hidden` | Quick filter: hide non-matching rows / 快速过滤: 藏起不匹配的行 | Ctrl+S |
| `compare` | Compare folders / 比较目录 | Shift+F2 |
| `dup` | Find duplicates / 查找重复文件 | — |
| `dup_keep_shortest` / `dup_keep_oldest` / `dup_keep_cursor` | Select all but one per duplicate group / 每组保留… | — |
| `checksum` / `checksum_create` / `checksum_verify` | Checksums / create SHA256SUMS / verify a checksum file / 校验和 | — |

## Selection

| Command | Does | Default key |
|---|---|---|
| `sel_toggle` | Select/deselect current (folders also get measured) / 选中/取消当前项 | Space* |
| `sel_toggle_down` | Select and move down / 选中并下移 | Insert* |
| `sel_all` / `sel_invert` | Select all / invert / 全选 / 反选 | Ctrl+A / `*`* |
| `sel_pattern_add` / `sel_pattern_sub` | Select / deselect by pattern / 按通配符选择 / 取消 | `+`* / `-`* |

\* Built into the file list (Total Commander habits); not managed by `[keys]` and can't be removed, but the commands
can still get extra keys or go on the toolbar and menus.

Also built in and not configurable: Esc cancels size calculation or clears the filter; Ctrl+Alt+letter jumps to the
next file starting with that letter; typing letters opens the quick filter.

## Program

| Command | Does | Default key |
|---|---|---|
| `open_config` | Open config.toml / 打开配置文件 | — |
| `usercmd_help` | Add a custom command (template) / 添加自定义命令… | — |
| `check_update` | Check for updates / 检查更新 | — |
| `docs` / `homepage` / `feedback` | Documentation / website / report an issue / 使用文档 / 官方网站 / 反馈问题 | — |
| `license` / `about` | License / about / 授权 / 关于 | — |

## Only in menus and bars

| `cmd` | Where | Meaning |
|---|---|---|
| `-` | menu, toolbar, crumb, context | Separator |
| `layout`, `theme`, `language`, `tree_follow`, `sftp`, `user_commands` | `[[menu]]` | Built-in submenus (see sections.md) |
| `shell_more`, `shell` | `[[context]]`, `[[context_bg]]` | Windows context menu, folded or inline |
