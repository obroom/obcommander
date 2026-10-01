<p align="center">
  <img src="assets/logo.svg" width="96" alt="OB Commander logo">
</p>

<h1 align="center">OB Commander</h1>

<p align="center">
  Windows 上快速、便携的双栏文件管理器，Total Commander 那一路。
</p>

<p align="center">
  <a href="README.md">English</a> · <b>简体中文</b> ·
  <a href="https://obcommander.com">官网</a> ·
  <a href="https://github.com/obroom/obcommander/releases">下载</a>
</p>

---

## 亮点

- **文件操作能撤销 / 重做**（Ctrl+Z / Ctrl+Y）—— 复制、移动、删除、重命名都能撤，多级。
  撤销删除是从回收站原路还原，撤销记录跟资源管理器共用。
- **文件夹大小** —— 光标停在文件夹上按空格就算，也能一次全算完，再按大小排序。
  专业版会记住算过的结果，重启后还在。
- **即时预览**（Ctrl+Q / F3）*（专业版）*—— 图片、文本代码、Markdown、PDF、Office 文档、SQLite 数据库等，
  F3 窗口里还是一个完整的文本编辑器。
- **比较目录**（Shift+F2）*（专业版）*—— 两个文件夹连同子文件夹并排对齐：相同、不同、只有一边有，一眼看完。
- **查找重复文件** —— 按内容比对，清理完也能撤销。
- **压缩包当文件夹逛** *（专业版）*—— zip、7z、rar、tar、iso 等像普通文件夹一样浏览。
- **远程 SFTP 标签** —— 服务器上的文件像本地文件夹一样操作 *（专业版）*。
- 内置 **Everything 搜索**，还有标签页、目录树、批量重命名、校验和、自定义命令 *（专业版）*。
- **便携** —— 一个 exe；配置就在它旁边的 `config.toml` 里，保存即生效。
  装上 [AI skill](#ai-skill) 后，可以直接用聊天改配置。

## 下载

在 **[Releases](https://github.com/obroom/obcommander/releases)** 下载最新的 Windows 版，
标签以 `win-` 开头的就是。

- Windows 10 / 11，x64。便携版：不用安装，不写注册表。
- Markdown、HTML、PDF 预览用的是微软 Edge WebView2，Windows 11 自带。

| 平台 | 状态 |
|---|---|
| Windows | 已发布 |
| macOS | 计划中 |
| Linux | 计划中 |

## 价格

- **个人和家庭使用免费**（非商业使用），不用注册账号。
- **商业使用**可免费试用 30 天，之后需要按使用人数购买授权 —— 凡是为公司、组织或为工作而用，包括自由职业，都算商业使用。
- **专业版功能**需要购买授权，个人使用也一样：F3 查看和 Ctrl+Q 快速查看、压缩包当文件夹逛、记住文件夹大小、比较目录、自定义命令、远程 SFTP。在程序里就能免费试用 30 天，不用绑卡、不用注册。
- 一份授权可以在 **2 台电脑**上用（比如公司一台、家里一台），含以后的更新。购买授权可获得**邮件支持**。
- 激活或开始试用时连一次授权服务器，之后授权在本机离线验证。（启动时的检查更新是另一回事：不发送个人信息，可以关掉。）

各项的准确定义以 [LICENSE](LICENSE) 为准。价格见 [obcommander.com](https://obcommander.com)。

## AI skill

`skills/obcmd-config` 教 AI 怎么改 OB Commander 的 `config.toml` —— 配色、主题、字体、列、快捷键、工具栏、菜单等。
它用的是开放的 [Agent Skills](https://agentskills.io) 格式，支持这个格式的 AI 工具都能直接用同一个文件夹。

**Claude Code**

```
/plugin marketplace add obroom/obcommander
/plugin install obcmd@obcommander
```

**其他 AI 工具** —— 把 `skills/obcmd-config` 文件夹复制到对应的 skills 目录：

| 工具 | skills 目录 |
|---|---|
| OpenAI Codex | `~/.codex/skills/` |
| Gemini CLI | `~/.gemini/skills/`（或 `~/.agents/skills/`） |
| Claude Code（手动安装） | `~/.claude/skills/` |
| 其他支持 Agent Skills 的工具 | 见各自的文档 |

```powershell
git clone --depth 1 https://github.com/obroom/obcommander "$env:TEMP\obcommander"
Copy-Item -Recurse "$env:TEMP\obcommander\skills\obcmd-config" "$HOME\.codex\skills\"
```

MCP 服务在计划中，以后用同样的方式安装。

## 翻译

程序内置 9 门语言：English、简体中文、繁體中文、Deutsch、Français、Español、Português (Brasil)、Русский、日本語。
更多语言、怎么安装、怎么自己加一门，见 [`lang/`](lang)。欢迎提 PR 贡献新语言或修正翻译。

## 反馈

问题反馈和功能建议：[Issues](https://github.com/obroom/obcommander/issues)。
授权相关：[support@obcommander.com](mailto:support@obcommander.com)。

这个仓库只放发布版本、文档和 AI 工具集成，不公开源代码。

## 许可

OB Commander 是专有软件，个人和家庭使用免费。详见 [LICENSE](LICENSE)。
