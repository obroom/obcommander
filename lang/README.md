# OB Commander languages

[中文说明](#中文)

## Built in

These languages ship inside `obcmd.exe`; nothing to download. Pick one under **Options > Language**.
By default OB Commander follows your Windows display language.

| File | Language |
|---|---|
| `en.toml` | English |
| `zh-CN.toml` | 简体中文 |
| `zh-TW.toml` | 繁體中文 |
| `de.toml` | Deutsch |
| `fr.toml` | Français |
| `es.toml` | Español |
| `pt-BR.toml` | Português (Brasil) |
| `ru.toml` | Русский |
| `ja.toml` | 日本語 |

## Download

These aren't built in; install them as described below.

| File | Language |
|---|---|
| `ko.toml` | 한국어 |
| `it.toml` | Italiano |
| `pl.toml` | Polski |
| `tr.toml` | Türkçe |
| `nl.toml` | Nederlands |
| `uk.toml` | Українська |
| `cs.toml` | Čeština |

More languages are on the way.

## Installing a language file

1. Open the `.toml` file here and click **Download raw file**.
2. Create a folder named `lang` next to `obcmd.exe` (if it isn't there yet) and put the file in it.
3. In OB Commander, open **Options > Language** and pick the new language.

A file with the same name as a built-in language replaces its text, so you can also use this to try a corrected translation.

## Fixing or adding a translation

Copy `en.toml`, rename it to a language tag (for example `it.toml` or `ko.toml`) and translate the text on the right-hand side of each `=`.
Keep every `{placeholder}` and the shortcut text after `\t`. Lines you haven't translated yet fall back to English.
Pull requests are welcome.

---

## 中文

**内置语言**：第一张表的 9 门已经在 `obcmd.exe` 里，不用下载，在「配置 > 语言」里选。默认跟随 Windows 的显示语言。

**下载语言**：第二张表的 7 门（한국어、Italiano、Polski、Türkçe、Nederlands、Українська、Čeština）按下面的步骤装，更多语言陆续加入。

**安装语言文件**：
1. 打开这里的 `.toml` 文件，点 **Download raw file** 下载。
2. 在 `obcmd.exe` 旁边建一个 `lang` 文件夹（已有就不用建），把文件放进去。
3. 在 OB Commander 里打开「配置 > 语言」，选新的语言。

文件名和内置语言相同时，会覆盖内置的文字，可以用来试改过的翻译。

**修改或新增翻译**：复制 `en.toml`，改名成语言代码（如 `it.toml`、`ko.toml`），翻译每个 `=` 右边的文字。`{占位符}` 和 `\t` 后面的快捷键要原样保留，没翻到的行会显示英文。欢迎提 PR。
