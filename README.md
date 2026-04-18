# Legal Document Assistant

中国法律文书撰写全流程助手

---

一套面向中国执业律师的 AI Agent Skill，覆盖诉讼文书和非诉文书的核心场景。每个 Skill 不是模板填充，而是从接案分析到文书成稿的完整工作流程。

可用于 Claude Code、Cursor 等 AI 编程工具，也可以直接复制 `SKILL.md` 内容作为提示词粘贴到任何对话式 AI 中使用。

---

## Skill 一览

### 1. 起诉状撰写 `qisuzhuang`　🚧 规划中

协助原告方律师完成民事起诉状的撰写。

### 2. [答辩状撰写 `dabianzhuan`](./dabianzhuan/)　✅

协助被告方律师完成从接案到撰写答辩状的全部工作。六个阶段依次推进：

材料接收与信息提取 → 程序性审查 → 实体法律关系分析 → 证据分析与质证准备 → 答辩策略制定 → 答辩状撰写

### 3. [合同审查 `hetong-shencha`](./hetong-shencha/)　✅

系统性审查合同条款，识别对委托人不利的风险点，输出修改建议和替代方案。

### 4. [项目法律意见书 `falv-yijianshu`](./falv-yijianshu/)　✅

以战略顾问视角为项目出具法律意见书（备忘录格式）。采用对话分析 + 意见书生成的两阶段模式：

事实梳理 → 法律关系梳理 → 法规检索 → 风险四级分层 → 路径论证 → 框架确认 → 意见书撰写

---

## 安装

**Claude Code 安装：**

```bash
git clone https://github.com/youtinghsu6086/legal-document-assistant.git
ln -s $(pwd)/legal-document-assistant/dabianzhuan ~/.claude/skills/dabianzhuan
ln -s $(pwd)/legal-document-assistant/hetong-shencha ~/.claude/skills/hetong-shencha
ln -s $(pwd)/legal-document-assistant/falv-yijianshu ~/.claude/skills/falv-yijianshu
```

**其他 AI 工具：** 打开对应文件夹下的 `SKILL.md`，复制全部内容作为系统提示词即可。

---

## 几个关键设计决策

**为什么是分阶段流程而不是一键生成？**
法律文书质量取决于前期分析的深度。跳过分析直接出稿，表面上快，实际上律师要花更多时间修改。分阶段推进让律师在关键节点介入把关，最终成稿质量更高。

**为什么不引用训练数据中的法条？**
大模型训练数据中的法条存在条文编号错位、版本过期等问题。所有 Skill 要求法条必须经在线检索验证，无法验证的标注 `[待查]`，宁可留白不编造。

**为什么最终文书不用 Markdown 格式？**
律师的工作产出要交给当事人和法院，最终都在 Word 里。意见书和答辩状的输出采用纯文本中文序号体系，粘贴到 Word 后零清理。

---

适用法域：中华人民共和国　｜　License：MIT
