# Legal Document Assistant

中国法律文书撰写全流程助手 - AI Agent Skills for Legal Document Drafting

## 📋 项目简介

本项目提供一套专业的法律文书撰写 Agent Skill，可用于 Claude Code、Cursor 等 AI 编程工具。每个 Skill 覆盖一类法律文书从接案到成稿的完整工作流程，不是简单的模板填充，而是结构化的法律分析 + 专业文书输出。

> P.S.：直接复制 `SKILL.md` 中的内容，作为提示词输入给对话式 AI（如豆包、DeepSeek、ChatGPT），也是好用的

## 🎯 核心功能

- 📝 **答辩状撰写**：六阶段全流程——材料提取、程序审查、实体分析、证据质证、策略制定、文书撰写
- 📑 **合同审查**：系统性合同条款审查，识别风险点并提供修改建议
- 📄 **法律意见书**：项目法律意见书（备忘录）撰写，四级风险分层，战略顾问视角分析
- ⚖️ **起诉状撰写**：（规划中）

## 📂 Skill 目录

| Skill | 说明 | 适用场景 | 状态 |
|-------|------|----------|------|
| [dabianzhuan](./dabianzhuan/) | 民事答辩状撰写 | 收到起诉状后，协助被告方律师撰写答辩状 | ✅ 可用 |
| [hetong-shencha](./hetong-shencha/) | 合同审查 | 审查合同条款，识别风险，提供修改建议 | ✅ 可用 |
| [falv-yijianshu](./falv-yijianshu/) | 项目法律意见书 | 为项目出具法律意见书（备忘录），全面分析法律风险与合规路径 | ✅ 可用 |
| qisuzhuang | 民事起诉状撰写 | 协助原告方律师撰写起诉状 | 🚧 规划中 |

## 🚀 快速开始

### 方式一：Claude Code 直接安装

```bash
claude mcp add legal-skills -- npx -y @anthropic-ai/claude-code-mcp@latest skill install https://github.com/youtinghsu6086/legal-document-assistant
```

### 方式二：手动安装

```bash
# 克隆仓库
git clone https://github.com/youtinghsu6086/legal-document-assistant.git

# 将需要的 skill 软链接到 Claude Code skills 目录
ln -s $(pwd)/legal-document-assistant/dabianzhuan ~/.claude/skills/dabianzhuan
ln -s $(pwd)/legal-document-assistant/hetong-shencha ~/.claude/skills/hetong-shencha
ln -s $(pwd)/legal-document-assistant/falv-yijianshu ~/.claude/skills/falv-yijianshu
```

### 方式三：直接复制提示词

每个文件夹下的 `SKILL.md` 内容可以直接复制，粘贴到任何 AI 对话工具中作为系统提示词使用。

## 💡 使用场景

### 答辩状（dabianzhuan）
```
用户：[粘贴起诉状内容]，请帮我写答辩状
→ 自动进入六阶段工作流程，逐步分析并生成答辩状
```

### 合同审查（hetong-shencha）
```
用户：请审查这份合同 [粘贴合同内容]
→ 逐条审查合同条款，输出风险点和修改建议
```

### 法律意见书（falv-yijianshu）
```
用户：我们公司要做一个XX项目，请出具法律意见书
→ 进入对话分析阶段，逐步完成事实梳理、法律检索、风险分析，最终生成备忘录格式意见书
```

## ⚙️ 设计原则

- **流程驱动**：每个 Skill 都有明确的阶段划分，按顺序推进，不跳步
- **律师审核**：AI 产出的是草稿和分析材料，关键节点等待律师确认后才继续
- **不编造法条**：无法确认的法律条文一律标注 `[待查]`，不凭记忆引用
- **立场明确**：始终站在委托人一方，分析服务于委托人利益
- **格式规范**：最终文书符合中国法律文书的格式规范，可直接粘贴到 Word 使用

## 📖 适用范围

- 适用法域：**中华人民共和国**法律体系
- 适用对象：执业律师、法务人员、法学研究者
- 语言：中文

## 📄 License

MIT
