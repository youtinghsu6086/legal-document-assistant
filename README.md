# Legal Document Assistant

中国法律文书撰写全流程助手

---

一套面向中国执业律师的 AI Agent Skill，覆盖诉讼文书和非诉文书的核心场景。每个 Skill 不是模板填充，而是从接案分析到文书成稿的完整工作流程。

适用法域：中华人民共和国

---

## 目录

- [Skill 一览](#skill-一览)
- [谁适合用这个项目](#谁适合用这个项目)
- [前置准备](#前置准备)
- [安装与使用](#安装与使用)
- [几个关键设计决策](#几个关键设计决策)
- [未完待续](#未完待续)

---

## Skill 一览

### 1. 起诉状撰写 `qisuzhuang`　🚧 规划中

协助原告方律师完成民事起诉状的撰写。

### 2. [答辩状撰写 `dabianzhuan`](./dabianzhuan/)　✅

协助被告方律师完成从接案到撰写答辩状的全部工作。六个阶段依次推进：

材料接收与信息提取 → 程序性审查 → 实体法律关系分析 → 证据分析与质证准备 → 答辩策略制定 → 答辩状撰写

### 3. [合同审查 `hetong-shencha`](./hetong-shencha/)　✅

系统性审查合同条款，识别对委托人不利的风险点，输出修改建议和替代方案。支持 A/B/C 三档审查策略（按合同金额分级），直接在 Word 文档中生成批注。

### 4. [项目法律意见书 `falv-yijianshu`](./falv-yijianshu/)　✅

以战略顾问视角为项目出具法律意见书（备忘录格式）。采用对话分析 + 意见书生成的两阶段模式：

事实梳理 → 法律关系梳理 → 法规检索 → 风险四级分层 → 路径论证 → 框架确认 → 意见书撰写

### 5. 未完待续...

以上是目前已有和规划中的 Skill。如果你在执业中有其他高频文书需求（如仲裁申请书、律师函、尽职调查报告等），或者对现有 Skill 有改进建议，欢迎通过 [Issues](https://github.com/youtinghsu6086/legal-document-assistant/issues) 与我交流。

---

## 谁适合用这个项目

- 正在使用或准备使用 AI 工具辅助法律工作的**执业律师**
- 企业**法务人员**，需要起草或审查合同、出具内部法律意见
- **法学生**，希望通过 AI 辅助学习法律文书的结构和写法

你不需要会编程。本项目的 Skill 本质上是一套结构化的提示词（prompt），告诉 AI 应该按什么流程、什么标准来完成法律文书工作。

---

## 前置准备

### 你需要一个 AI 工具

本项目的 Skill 可以配合多种 AI 工具使用。以下列举一些常见选择：

**AI 编程工具（推荐，体验最佳）**

这类工具可以直接读取本地文件、创建文件、联网检索，配合 Skill 的全流程工作最为顺畅：

| 工具 | 说明 |
|------|------|
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | Anthropic 官方命令行工具，本项目的 Skill 格式原生适配 |
| [Cursor](https://cursor.sh) | AI 代码编辑器，可将 SKILL.md 设为 Rules |
| [Windsurf](https://codeium.com/windsurf) | AI 代码编辑器，类似 Cursor |
| [OpenCode](https://opencode.ai) | 开源 AI 编程工具 |

**对话式大模型（通用方案）**

如果你不使用编程工具，也可以直接把 `SKILL.md` 的内容复制粘贴到以下任何大模型的对话框中，作为系统提示词使用：

| 大模型 | 厂商 | 地址 |
|--------|------|------|
| Claude | Anthropic（美国） | claude.ai |
| ChatGPT | OpenAI（美国） | chatgpt.com |
| Gemini | Google（美国） | gemini.google.com |
| DeepSeek | 深度求索（中国） | chat.deepseek.com |
| 豆包 | 字节跳动（中国） | doubao.com |
| 通义千问 | 阿里巴巴（中国） | tongyi.aliyun.com |
| 文心一言 | 百度（中国） | yiyan.baidu.com |
| Kimi | 月之暗面（中国） | kimi.moonshot.cn |

> 提示：不同大模型的能力有差异。涉及法律分析的复杂任务，建议优先使用 Claude、ChatGPT 或 DeepSeek 等推理能力较强的模型。

### 合同审查 Skill 的额外依赖

合同审查（hetong-shencha）需要操作 Word 文档，运行时会用到 Python 和 lxml 库。如果你的环境中还没有安装，可以直接让 AI 工具帮你完成：

- 在 Claude Code 中输入：`帮我安装 python3 和 lxml`
- 在 Cursor 中同样可以要求 AI 帮你安装依赖

其他两个 Skill（答辩状、法律意见书）不需要任何额外依赖，开箱即用。

### 推荐的 MCP 工具（可选）

MCP（Model Context Protocol）是让 AI 工具调用外部能力的协议。以下 MCP 工具可以提升 Skill 的使用体验，但不是必须的：

| MCP 工具 | 用途 | 对应 Skill |
|----------|------|-----------|
| 网页搜索类（如 Firecrawl、Tavily） | 在线检索法律法规，验证法条是否现行有效 | 答辩状、法律意见书 |
| 文件系统类 | 读写本地文件（Claude Code 自带，无需额外安装） | 全部 |

如果你不知道怎么安装 MCP，同样可以直接问你的 AI 工具：`帮我安装 Firecrawl MCP`，它会引导你完成配置。

---

## 安装与使用

### 方式一：Claude Code 安装（推荐）

```bash
# 1. 克隆本仓库到本地
git clone https://github.com/youtinghsu6086/legal-document-assistant.git

# 2. 将需要的 Skill 软链接到 Claude Code 的 skills 目录
ln -s $(pwd)/legal-document-assistant/dabianzhuan ~/.claude/skills/dabianzhuan
ln -s $(pwd)/legal-document-assistant/hetong-shencha ~/.claude/skills/hetong-shencha
ln -s $(pwd)/legal-document-assistant/falv-yijianshu ~/.claude/skills/falv-yijianshu
```

安装完成后，在 Claude Code 中正常对话即可。例如：
- 粘贴一份起诉状，说"请帮我写答辩状"→ 自动触发答辩状 Skill
- 说"请审查这份合同"并提供 .docx 文件 → 自动触发合同审查 Skill
- 说"我们公司要做一个XX项目，请出具法律意见书"→ 自动触发法律意见书 Skill

### 方式二：复制提示词到任意 AI 工具

不需要安装任何东西：

1. 打开你需要的 Skill 文件夹（如 [dabianzhuan/SKILL.md](./dabianzhuan/SKILL.md)）
2. 点击 `SKILL.md` 文件，复制 `---` 分隔线以下的全部内容
3. 粘贴到你使用的 AI 工具的对话框中（作为第一条消息或系统提示词）
4. 然后正常提供案件材料、开始对话即可

---

## 几个关键设计决策

**为什么是分阶段流程而不是一键生成？**

法律文书质量取决于前期分析的深度。跳过分析直接出稿，表面上快，实际上律师要花更多时间修改。分阶段推进让律师在关键节点介入把关，最终成稿质量更高。

**为什么不引用训练数据中的法条？**

大模型训练数据中的法条存在条文编号错位、版本过期等问题。所有 Skill 要求法条必须经在线检索验证，无法验证的标注 `[待查]`，宁可留白不编造。

**为什么输出 .md 而不是 .docx？**

让 AI 直接输出 Word 文档，意味着要在提示词里定义字体、字号、行距、颜色等排版细节。这些排版指令会大量消耗 token，而且每个律师的排版习惯不同——你要宋体小四，他要仿宋三号，输出的格式大概率不是你想要的，最后还是得重新调。

我们的做法是：文书输出为 .md 文件，但内容是严格的纯文本——不使用加粗、标题符号、表格语法等任何 Markdown 特有标记，分层用中文序号（一、（一）、1.），引号用全角中文引号。你拿到后直接全选复制、粘贴到自己的 Word 模板里，零清理，排版按你自己的习惯来。

> 合同审查（hetong-shencha）是例外：它直接读取 .docx 并在原文上生成 Word 批注，因为合同审查的工作方式就是在原件上标注。


