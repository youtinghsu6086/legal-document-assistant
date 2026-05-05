# md2pdf — Markdown 转 PDF

`md2pdf` 是一个通用命令行工具，将任意 Markdown 文件转为排版好的 PDF，支持中文排版优化。

---

## 适用场景

- 将 Markdown 笔记、文档转为 PDF 以便打印或分享
- 将 AI 生成的 `.md` 内容转为正式排版的 PDF
- 配合本项目的 Skill（答辩状、法律意见书、案件分析报告等），将输出文书一键转为 PDF

直接打开 `.md` 文件会看到 Markdown 标记符号（`#`、`*`、`-` 等），不适合直接发送或打印。转为 PDF 后可正常使用。

---

## 前置准备

md2pdf 依赖以下两个工具。可手动安装，也可在 Claude Code 中输入 `帮我安装 pandoc 和 Chrome`：

| 依赖 | 作用 | 怎么装 |
|------|------|--------|
| pandoc | 把 .md 转成网页格式 | 终端运行 `brew install pandoc` |
| Google Chrome | 把网页格式转成 PDF | [google.com/chrome](https://www.google.com/chrome/) 下载安装 |

---

## 怎么用

### 第一步：安装

```bash
# 创建个人脚本目录（如已有则跳过）
mkdir -p ~/bin

# 将 md2pdf 链接到该目录（注意替换 /path/to/ 为实际仓库路径）
ln -s /path/to/legal-document-assistant/md2pdf/md2pdf ~/bin/md2pdf

# 将 ~/bin 加入 PATH（如已加过则跳过）
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

安装完成后，在任意终端窗口、任意目录下均可直接使用 `md2pdf` 命令。

### 第二步：使用

```bash
md2pdf /path/to/文书.md
```

几秒钟后，同目录下出现同名 `.pdf` 文件。也可以先输入 `md2pdf `（带空格），再把 `.md` 文件从访达拖进终端窗口，路径会自动填入。

### 具体例子

```bash
# 转换答辩状
md2pdf ~/Desktop/案件/张某某答辩状.md
# → 生成 ~/Desktop/案件/张某某答辩状.pdf

# 转换法律意见书
md2pdf ~/Documents/法律意见书/某项目法律意见书.md
# → 生成 ~/Documents/法律意见书/某项目法律意见书.pdf
```

### 拖拽输入路径

在终端输入 `md2pdf `（末尾带空格），把 `.md` 文件从访达拖进终端窗口，路径自动填入，按回车即可。

### 配合 Claude Code 使用

生成文书后让 Claude Code 接着转换：

> 帮我生成答辩状，然后 md2pdf 转为 PDF

---

## PDF 样式

生成的 PDF 针对中文法律文书做了排版优化：

- **字体**：苹方（macOS 默认中文字体）
- **字号**：12pt
- **行距**：1.8 倍
- **首行缩进**：两个字符宽度
- **标题层级**：一级标题居中、二级标题带下划线

无需二次调整，可直接打印或发送。

---

## 自定义样式

如需调整字体、字号、行距等样式，可在 Claude Code 中说明需求（示例："帮我把 md2pdf 的正文字号改成 14pt，去掉首行缩进"），Claude Code 会直接修改脚本，改完即刻生效。

也可以手动编辑 `md2pdf/md2pdf` 脚本中的 CSS 部分来调整样式。

---

## 常见问题

**Q：输入 `md2pdf` 提示 `command not found`**

A：新开一个终端窗口，或运行 `source ~/.zshrc`。

**Q：拖拽文件进去后报"找不到文件"**

A：检查一下文件路径里有没有空格没被正确处理。把文件路径用引号包起来：`md2pdf "文件路径.md"`。

**Q：中文显示成方块或乱码**

A：系统可能缺少苹方字体。在 Claude Code 中输入 `帮我把 md2pdf 的字体改成宋体`，或手动编辑脚本中的 `font-family` 设置。

**Q：支持 Windows 吗**

A：当前版本仅支持 macOS。Windows 用户可通过 WSL 尝试，或直接将 `.md` 文件内容复制到 Word 中排版。
