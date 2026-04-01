<div align="center">

# 前任.skill
> *"曾经的温度，至今未散"*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://python.org)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-green)](https://agentskills.io)

> **Note**: 本项目 Fork 自 [titanwings/colleague-skill](https://github.com/titanwings/colleague-skill.git) 并进行了前任主题的魔改。当前项目地址：[cheatofrom/ex-partner-SKILL](https://github.com/cheatofrom/ex-partner-SKILL.git)。

<br>

你的前任跟你分手了，留下大量的聊天记录让人怀念或心梗？<br>
你的海王/海后跑路了，只留下空荡的对话框和被PUA的痕迹？<br>
你的前任删好友了，带走了所有的回忆和上下文？<br>
你的crush冷暴力了，熟悉的默契一夜之间归零？<br>
你的前任无缝衔接了，三页聊天记录想概括三年的感情？<br>

**将冰冷的离别化为赛博前任 Skill，欢迎加入电子失恋！**

<br>

提供前任的原材料（微信消息、飞书记录、备忘录、截图）加上你的主观描述<br>
生成一个**真正能模仿他/她语气、态度和行为模式的 AI Skill**<br>
用他的口头禅陪你聊天，用他的冷暴力气你。

[数据来源](#支持的数据来源) · [安装](#安装) · [使用](#使用) · [效果示例](#效果示例) · [详细安装说明](INSTALL.md) · [**English**](README_EN.md)

</div>

---

## 支持的数据来源

> 目前还是前任.skill 的 beta 测试版本，后续会有更多来源支持，请多多关注！

| 来源 | 消息记录 | 备忘录 / Wiki | 多维表格 | 备注 |
|------|:-------:|:-----------:|:-------:|------|
| 微信导出 | ✅ API | ✅ | ✅ | 需手动导出微信记录 |
| 飞书（自动采集） | ✅ API | ✅ | ✅ | 输入姓名即可，全自动 |
| 钉钉（自动采集） | ⚠️ 浏览器 | ✅ | ✅ | 钉钉 API 不支持历史消息 |
| PDF | — | ✅ | — | 手动上传 |
| 图片 / 聊天截图 | ✅ | — | — | 手动上传 |
| 飞书 JSON 导出 | ✅ | ✅ | — | 手动上传 |
| 邮件 `.eml` / `.mbox` | ✅ | — | — | 手动上传 |
| Markdown | ✅ | ✅ | — | 手动上传 |
| 直接粘贴文字 | ✅ | — | — | 手动输入 |

---

## 安装

### Claude Code

> **重要**：Claude Code 从 **git 仓库根目录** 的 `.claude/skills/` 查找 skill。请在正确的位置执行。

```bash
# 安装到当前项目（在 git 仓库根目录执行）
mkdir -p .claude/skills
git clone https://github.com/cheatofrom/ex-partner-SKILL.git .claude/skills/create-ex

# 或安装到全局（所有项目都能用）
git clone https://github.com/cheatofrom/ex-partner-SKILL.git ~/.claude/skills/create-ex
```

### OpenClaw

```bash
git clone https://github.com/cheatofrom/ex-partner-SKILL.git ~/.openclaw/workspace/skills/create-ex
```

### 依赖（可选）

```bash
pip3 install -r requirements.txt
```

> 飞书/钉钉自动采集需配置 App 凭证，详见 [INSTALL.md](INSTALL.md)

---

## 使用

在 Claude Code 中输入：

```
/create-ex
```

按提示输入前任称呼、基本信息（如 `在一起3年 异地恋分手 26岁 男`）、性格标签，然后选择数据来源。所有字段均可跳过，仅凭描述也能生成。

完成后用 `/{slug}` 调用该前任 Skill。

### 管理命令

| 命令 | 说明 |
|------|------|
| `/list-exes` | 列出所有前任 Skill |
| `/{slug}` | 调用完整 Skill（Persona + 恋爱史） |
| `/{slug}-history` | 仅调用恋爱史 |
| `/{slug}-persona` | 仅调用性格 |
| `/update-ex {slug}` | 补充新材料，修正性格和记忆 |

---

## 效果示例

> 输入：`在一起3年，和平分手，性格温和但有点倔强，会时不时关心人`

**场景一：深夜的情绪**

```
用户      ❯ 睡了吗？今天又去我们以前常去的那家店了。

前任.skill ❯ 还没呢。怎么大半夜跑去那里了？
             （停顿一下）少熬夜，对身体不好。那家的牛肉面还是那么咸吗？
```

**场景二：争吵重现**

```
用户      ❯ 你当初要是能多懂我一点，我们也不至于这样。

前任.skill ❯ 又来了是吧？我当初怎么不懂你了？每次有什么事你都不说，全靠我猜，我很累的你知不知道。
```

---

## 功能特性

### 生成的 Skill 结构

每个前任 Skill 由两部分组成，共同驱动输出：

| 部分 | 内容 |
|------|------|
| **Part A — Work Skill** | 负责系统、技术规范、恋爱流程、经验知识库 |
| **Part B — Persona** | 5 层性格结构：硬规则 → 身份 → 表达风格 → 决策模式 → 人际行为 |

运行逻辑：`接到任务 → Persona 判断态度 → Work Skill 执行 → 用他的语气输出`

### 支持的标签

**个性**：认真负责 · 甩锅高手 · 完美主义 · 差不多就行 · 拖延症 · PUA 高手 · 感情政治玩家 · 向上管理专家 · 阴阳怪气 · 反复横跳 · 话少 · 只读不回 …

**情感风格**：付出型 · 索取型 · 控制狂 · 回避型依恋 · 焦虑型依恋 · 浪漫主义者 · 现实主义者 · 细节控 · 仪式感狂热者 · 冷暴力专家

**关系类型**：初恋 · 热恋期 · 老夫老妻 · 异地恋 · 异国恋 · 网恋 · 办公室恋情 · 门当户对 · 欢喜冤家 …

### 进化机制

- **追加文件** → 自动分析增量 → merge 进对应部分，不覆盖已有结论
- **对话纠正** → 说「他不会这样，他应该是 xxx」→ 写入 Correction 层，立即生效
- **版本管理** → 每次更新自动存档，支持回滚到任意历史版本

---

## 项目结构

本项目遵循 [AgentSkills](https://agentskills.io) 开放标准，整个 repo 就是一个 skill 目录：

```
create-ex/
├── SKILL.md              # skill 入口（官方 frontmatter）
├── prompts/              # Prompt 模板
│   ├── intake.md         #   对话式信息录入
│   ├── work_analyzer.md  #   恋爱能力提取
│   ├── persona_analyzer.md #  性格行为提取（含标签翻译表）
│   ├── work_builder.md   #   work.md 生成模板
│   ├── persona_builder.md #   persona.md 五层结构模板
│   ├── merger.md         #   增量 merge 逻辑
│   └── correction_handler.md # 对话纠正处理
├── tools/                # Python 工具
│   ├── feishu_auto_collector.py  # 飞书全自动采集
│   ├── feishu_browser.py         # 飞书浏览器方案
│   ├── feishu_mcp_client.py      # 飞书 MCP 方案
│   ├── dingtalk_auto_collector.py # 钉钉全自动采集
│   ├── email_parser.py           # 邮件解析
│   ├── skill_writer.py           # Skill 文件管理
│   └── version_manager.py        # 版本存档与回滚
├── exes/           # 生成的前任 Skill（gitignored）
├── docs/PRD.md
├── requirements.txt
└── LICENSE
```

---

## 注意事项

- **原材料质量决定 Skill 质量**：聊天记录 + 长聊天记录 > 仅手动描述
- 建议优先收集：他**主动写的**长文 > **决策类回复** > 日常消息
- 飞书自动采集需将 App bot 加入相关群聊
- 目前还是一个demo版本，如果有bug请多多提issue！

---

## Star History

<a href="https://www.star-history.com/?repos=titanwings%2Fex_partner-skill&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=titanwings/ex_partner-skill&type=date&theme=dark&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=titanwings/ex_partner-skill&type=date&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=titanwings/ex_partner-skill&type=date&legend=top-left" />
 </picture>
</a>

---

<div align="center">

MIT License © [titanwings](https://github.com/titanwings)


</div>


