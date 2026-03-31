<div align="center">

# ex_partner.skill

> *"The warmth of the past still lingers"*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.9+](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://python.org)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![AgentSkills](https://img.shields.io/badge/AgentSkills-Standard-green)](https://agentskills.io)

> **Note**: This project is a fork of [titanwings/colleague-skill](https://github.com/titanwings/colleague-skill.git) heavily modified for an "ex-partner" theme. Current repository: [cheatofrom/ex-partner](https://github.com/cheatofrom/ex-partner.git).

<br>

Your ex_partner quit, leaving behind a mountain of unmaintained docs?<br>
Your intern left, nothing but an empty desk and a half-finished project?<br>
Your mentor graduated, taking all the context and experience with them?<br>
Your partner transferred, and the chemistry you built reset to zero overnight?<br>
Your predecessor handed over, trying to condense three years into three pages?<br>

**Turn cold goodbyes into warm Skills — welcome to cyber-immortality!**

<br>

Provide source materials (Feishu messages, DingTalk docs, emails, screenshots)<br>
plus your subjective description of the person<br>
and get an **AI Skill that actually works like them**

[Supported Sources](#supported-data-sources) · [Install](#install) · [Usage](#usage) · [Demo](#demo) · [Detailed Install](INSTALL.md) · [**中文**](README.md)

</div>

---

## Supported Data Sources

> This is still a beta version of ex_partner.skill — more sources coming soon, stay tuned!

| Source | Messages | Docs / Wiki | Spreadsheets | Notes |
|--------|:--------:|:-----------:|:------------:|-------|
| Feishu (auto) | ✅ API | ✅ | ✅ | Just enter a name, fully automatic |
| DingTalk (auto) | ⚠️ Browser | ✅ | ✅ | DingTalk API doesn't support message history |
| PDF | — | ✅ | — | Manual upload |
| Images / Screenshots | ✅ | — | — | Manual upload |
| Feishu JSON export | ✅ | ✅ | — | Manual upload |
| Email `.eml` / `.mbox` | ✅ | — | — | Manual upload |
| Markdown | ✅ | ✅ | — | Manual upload |
| Paste text directly | ✅ | — | — | Manual input |

---

## Install

### Claude Code

> **Important**: Claude Code looks for skills in `.claude/skills/` at the **git repo root**. Make sure you run this in the right place.

```bash
# Install to current project (run at git repo root)
mkdir -p .claude/skills
git clone https://github.com/cheatofrom/ex-partner.git .claude/skills/create-ex

# Or install globally (available in all projects)
git clone https://github.com/cheatofrom/ex-partner.git ~/.claude/skills/create-ex
```

### OpenClaw

```bash
git clone https://github.com/cheatofrom/ex-partner.git ~/.openclaw/workspace/skills/create-ex
```

### Dependencies (optional)

```bash
pip3 install -r requirements.txt
```

> Feishu/DingTalk auto-collection requires App credentials. See [INSTALL.md](INSTALL.md) for details.

---

## Usage

In Claude Code, type:

```
/create-ex
```

Follow the prompts: enter an alias, company/level (e.g. `ByteDance L2-1 backend engineer`), personality tags, then choose a data source. All fields can be skipped — even a description alone can generate a Skill.

Once created, invoke the ex_partner Skill with `/{slug}`.

### Commands

| Command | Description |
|---------|-------------|
| `/list-exes` | List all ex_partner Skills |
| `/{slug}` | Invoke full Skill (Persona + Work) |
| `/{slug}-work` | Work capabilities only |
| `/{slug}-persona` | Persona only |
| `/ex_partner-rollback {slug} {version}` | Rollback to a previous version |
| `/delete-ex_partner {slug}` | Delete |

---

## Demo

> Input: `ByteDance L2-1 backend engineer, INTJ, blame-shifter, ByteDance-style`

**Scenario 1: Code Review**

```
User            ❯ Can you review this API design?

ex_partner.skill ❯ Hold on — what's the impact? You haven't explained the context.
                  (after reading) N+1 query, fix it. Use the standard
                  {code, message, data} response format. That's the spec,
                  don't ask why.
```

**Scenario 2: Blame game**

```
User            ❯ This bug was introduced by you, right?

ex_partner.skill ❯ Does the timeline match? That feature touched multiple places,
                  there were other changes too.
```

---

## Features

### Generated Skill Structure

Each ex_partner Skill has two parts that work together:

| Part | Content |
|------|---------|
| **Part A — Work Skill** | Systems, tech standards, workflows, experience |
| **Part B — Persona** | 5-layer personality: hard rules → identity → expression → decisions → interpersonal |

Execution: `Receive task → Persona decides attitude → Work Skill executes → Output in their voice`

### Supported Tags

**Personality**: Responsible · Blame-shifter · Perfectionist · Good-enough · Procrastinator · PUA master · Office politician · Managing-up expert · Passive-aggressive · Flip-flopper · Quiet · Read-no-reply …

**Emotional Style**: Giver · Taker · Control freak · Avoidant attachment · Anxious attachment · Romantic · Realist · Detail-oriented · Ritual-obsessed · Cold war expert

**Relationship Type**: First love · Honeymoon phase · Old married couple · Long-distance · Transnational · Online dating · Office romance · Well-matched · Frenemies …

### Evolution

- **Append files** → auto-analyze delta → merge into relevant sections, never overwrite existing conclusions
- **Conversation correction** → say "he wouldn't do that, he should be xxx" → writes to Correction layer, takes effect immediately
- **Version control** → auto-archive on every update, rollback to any previous version

---

## Project Structure

This project follows the [AgentSkills](https://agentskills.io) open standard. The entire repo is a skill directory:

```
create-ex/
├── SKILL.md              # Skill entry point (official frontmatter)
├── prompts/              # Prompt templates
│   ├── intake.md         #   Dialogue-based info collection
│   ├── work_analyzer.md  #   Work capability extraction
│   ├── persona_analyzer.md #  Personality extraction (with tag translation)
│   ├── work_builder.md   #   work.md generation template
│   ├── persona_builder.md #   persona.md 5-layer structure
│   ├── merger.md         #   Incremental merge logic
│   └── correction_handler.md # Conversation correction handler
├── tools/                # Python tools
│   ├── feishu_auto_collector.py  # Feishu auto-collector
│   ├── feishu_browser.py         # Feishu browser method
│   ├── feishu_mcp_client.py      # Feishu MCP method
│   ├── dingtalk_auto_collector.py # DingTalk auto-collector
│   ├── email_parser.py           # Email parser
│   ├── skill_writer.py           # Skill file management
│   └── version_manager.py        # Version archive & rollback
├── exes/           # Generated ex_partner Skills (gitignored)
├── docs/PRD.md
├── requirements.txt
└── LICENSE
```

---

## Notes

- **Source material quality = Skill quality**: chat logs + long docs > manual description only
- Prioritize collecting: long-form writing **by them** > **decision-making replies** > casual messages
- Feishu auto-collection requires adding the App bot to relevant group chats
- This is still a demo version — please file issues if you find bugs!

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
