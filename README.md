# Legal Document Assistant

Claude Code Skills for Chinese legal document drafting (中国法律文书撰写助手).

## Skills

| Skill | Description | Status |
|-------|-------------|--------|
| [dabianzhuan](./dabianzhuan/) | 民事答辩状撰写全流程工作助手 | ✅ Available |
| hetong-shencha | 合同审查助手 | 🚧 Planned |
| qisuzhuang | 民事起诉状撰写助手 | 🚧 Planned |
| falv-yijianshu | 项目法律意见书撰写助手 | 🚧 Planned |

## Installation

Add this repository as a Claude Code skill source:

```bash
claude skill add --from https://github.com/youtinghsu6086/legal-document-assistant
```

Or clone and symlink individual skills:

```bash
git clone https://github.com/youtinghsu6086/legal-document-assistant.git
ln -s $(pwd)/legal-document-assistant/dabianzhuan ~/.claude/skills/dabianzhuan
```

## Usage

Each skill is triggered contextually in Claude Code. For example, provide a complaint document (起诉状) and ask Claude to draft a defense statement (答辩状), and the `dabianzhuan` skill will activate.

## Applicable Jurisdiction

All skills are designed for the **People's Republic of China** legal system (中华人民共和国法律体系).

## License

MIT
