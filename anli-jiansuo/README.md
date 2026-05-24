# 案例检索 `anli-jiansuo`

针对诉讼案件中的法律观点，通过案例数据库进行语义检索，生成结构化的案例检索报告。

---

## 这个 Skill 做什么

律师在诉讼中经常需要找到支持自己论点的类案。这个 Skill 把案例检索的过程结构化：

1. 阅读案件材料，理解案情
2. 梳理需要案例支撑的法律观点，提交律师确认
3. 为每个观点设计多角度的语义检索策略
4. 执行检索、筛选、排序
5. 生成纯文本格式的检索报告（可直接粘贴到 Word）

每个法律观点独立生成一份报告，每份报告最多 10 个案例。

Skill 本身只定义工作流程，不绑定特定的案例数据库。你需要自行接入一个案例检索工具。

---

## 接入案例检索工具

本 Skill 需要一个支持自然语言语义检索的案例数据库工具。以下是目前已验证可用的方案。

### 方案一：北大法宝 API（推荐）

[北大法宝](https://www.pkulaw.com) 提供了 MCP 案例检索服务，支持自然语言语义检索。

#### 1. 注册并获取 API Key

访问 [法宝 MCP 控制台](https://mcp.pkulaw.com)，注册账号后进入控制台，在「我的服务」中找到「检索司法案例-语义」服务，获取 Authorization Bearer Token。

#### 2. 在 Skill 中使用

检索时通过 curl 调用北大法宝 API：

```bash
curl -s "https://apim-gateway.pkulaw.com/mcp-case-search-service" \
  -H "Authorization: Bearer 你的Token" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"jsonrpc":"2.0","method":"tools/call","params":{"name":"search_case","arguments":{"text":"自然语言案情描述"}},"id":1}'
```

参数说明：
- `text`：自然语言案情描述，用一段完整的话描述案件事实，不是关键词
- `id`：请求编号，每次调用递增即可

返回结果是 JSON 格式的案例列表，包含案例标题、法院、案号、判决日期、案由、裁判文书内容等字段。

#### 3. 解析返回结果

返回的 JSON 结构中，案例信息在 `result.content[0].text` 字段内（JSON 字符串，需二次解析）。每个案例包含以下字段：

| 字段 | 说明 |
|------|------|
| `title` | 案例标题 |
| `court_name` | 审理法院 |
| `case_number` | 案号 |
| `decision_date` | 判决日期 |
| `cause_of_action` | 案由 |
| `content` | 裁判文书内容（截取） |

可以用以下命令快速浏览检索结果：

```bash
curl -s [上述完整命令] | python3 -c "
import sys,json
data=json.load(sys.stdin)
cases = json.loads(data['result']['content'][0]['text'])
for i,c in enumerate(cases):
    print(f'--- Case {i+1} ---')
    print(f'Title: {c[\"title\"]}')
    print(f'Court: {c[\"court_name\"]}')
    print(f'Number: {c[\"case_number\"]}')
    print(f'Date: {c[\"decision_date\"]}')
    print(f'Cause: {c[\"cause_of_action\"]}')
    print(f'Content: {c[\"content\"][:600]}')
    print()
"
```

### 方案二：其他案例数据库

本 Skill 的工作流程不绑定北大法宝，任何支持自然语言语义检索的案例数据库都可以接入。如果你使用其他工具（如威科先行、无讼等），只需在第四步"执行检索"时替换为对应工具的调用方式即可。

---

## 使用方式

### Claude Code

```bash
# 将 SKILL.md 软链接到 Claude Code 的 skills 目录
ln -s $(pwd)/anli-jiansuo ~/.claude/skills/anli-jiansuo
```

安装后，在 Claude Code 中提供案件材料并说"帮我检索案例"即可触发。

### 其他 AI 工具

复制 `SKILL.md` 中 `---` 分隔线以下的全部内容，粘贴到 AI 工具的对话框中作为系统提示词。检索步骤需要手动执行 curl 命令或在 AI 工具中授权执行。

---

## 注意事项

- 本 Skill 只做案例检索和整理，不做案件分析、不做策略建议
- 检索报告为纯文本格式，不使用 Markdown 符号，可直接复制粘贴到 Word
- 检索结果来自第三方数据库，案例的完整性和准确性以数据库为准
- API Token 是你的个人凭证，请勿提交到公开仓库
