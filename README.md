<div align="center">

# 🔮 VangardCLI

**An AI coding agent for your terminal, written in Python.**

*"The Light answers those who study it. So does the codebase."*
<br>— from the field notes

***

[![GitHub stars](https://img.shields.io/github/stars/dea6cat/vangardCLI?style=for-the-badge&logo=github&color=yellow)](https://github.com/dea6cat/vangardCLI/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/downloads/)

</div>

***

## 🌌 What This Is

I have spent a long time in the terminal, Guardian. Most tools there answer one question and fall silent. VangardCLI does more: it reads your files, runs your commands, fetches what it needs from the web, and keeps working until the task is done.

It is a Python rebuild of the Claude Code architecture, and it ships as a working CLI agent:

- **A real agent loop.** It calls tools, streams its replies, remembers the session, and works over many turns.
- **A faithful port.** It keeps the proven architecture, rewritten in idiomatic Python.
- **Built to study and extend.** The code is readable and tested, and you add new skills by writing Markdown.

***

## ✨ Features

### Streaming Agent

*Watch the answer take shape as it forms, like a Rift filling with Light.*

```text
>>> /stream on
>>> Explain tests/test_agent_loop.py
[streaming answer...]
• Read (tests/test_agent_loop.py) running...
  ↳ lines 1-180
>>> /render-last
```

- Direct replies stream straight from the API, and tool-driven agent loops stream too
- `/stream` toggles live output; `/render-last` re-renders the last reply as clean Markdown
- You can see each tool as it runs, and if streaming fails it falls back to the regular agent loop

### Skills

*Every scholar keeps a grimoire. Here yours is a folder of Markdown files.*

```md
---
description: Explain code with diagrams and analogies
allowed-tools:
  - Read
  - Grep
  - Glob
arguments: [path]
---

Explain the code in $path. Start with an analogy, then draw a diagram.
```

- Each skill is a `SKILL.md` file and becomes a slash command
- Skills can live in the project or in your user folder, take named arguments, and limit which tools they may use

### Multiple Providers

*One Light, many sources.*

```python
providers = ["Anthropic Claude", "OpenAI GPT", "Zhipu GLM"]  # + easy to extend
```

### Interactive REPL

```text
>>> Hello!
Assistant: Eyes up. I'm VangardCLI...

>>> /help         # Show commands
>>> /             # Show all commands & skills
>>> /save         # Save session
>>> /multiline    # Multi-paragraph input
>>> Tab           # Auto-complete
>>> /explain-code qsort.py   # Run a skill
```

### CLI

```bash
vangard              # Start REPL
vangard login        # Configure API
vangard --version    # Check version
vangard config       # View settings
```

***

## 📊 Status

*Where things stand today.*

| Component     | Status     | Count     |
| ------------- | ---------- | --------- |
| REPL Commands | ✅ Complete | 6+ built-ins |
| Tool System   | ✅ Complete | 30+ tools |
| Automated Tests | ✅ Present | Core suites for skills, providers, REPL, tools, context |
| Documentation | ✅ Complete | 10+ docs  |

### Core Systems

| System | Status | Description |
|--------|--------|-------------|
| CLI Entry | ✅ | `vangard`, `login`, `config`, `--version` |
| Interactive REPL | ✅ | Rich interactive output, history, tab completion, multiline |
| Multi-Provider | ✅ | Anthropic, OpenAI, GLM support |
| Session Persistence | ✅ | Save/load sessions locally |
| Agent Loop | ✅ | Tool calling loop implementation |
| Skill System | ✅ | SKILL.md-based slash-command skills with args + tool limits |
| Context Building | 🟡 | Initial prompt injection for workspace, git, and CLAUDE.md; deeper project understanding still needed |
| Permission System | 🟡 | Framework exists, needs integration |

### Tools (30+)

| Category | Tools | Status |
|----------|-------|--------|
| File Operations | Read, Write, Edit, Glob, Grep | ✅ Complete |
| System | Bash execution | ✅ Complete |
| Web | WebFetch, WebSearch | ✅ Complete |
| Interaction | AskUserQuestion, SendMessage | ✅ Complete |
| Task Management | TodoWrite, TaskManager, TaskStop | ✅ Complete |
| Agent Tools | Agent, Brief, Team | ✅ Complete |
| Configuration | Config, PlanMode, Cron | ✅ Complete |
| MCP | MCP tools and resources | ✅ Complete |
| Others | LSP, Worktree, Skill, ToolSearch | ✅ Complete |

### Roadmap

- ✅ **Phase 0**: Installable, runnable CLI
- ✅ **Phase 1**: Core agent MVP experience
- ✅ **Phase 2**: Real tool calling loop
- 🟡 **Phase 3**: Context, permissions, recovery (in progress)
- ⏳ **Phase 4**: MCP, plugins, extensibility
- ⏳ **Phase 5**: Python-native differentiators

**See [FEATURE_LIST.md](FEATURE_LIST.md) for detailed feature status and PR guidelines.**

***

## 🚀 Quick Start

*Every journey begins in the Tower.*

### Install

```bash
git clone https://github.com/dea6cat/vangardCLI.git
cd vangardCLI

# Create venv (uv recommended)
uv venv --python 3.11
source .venv/bin/activate

# Install
uv pip install -r requirements.txt
```

### Configure

#### Option 1: Interactive (Recommended)

```bash
python -m src.cli login
```

This flow will:

1. ask you to choose a provider: anthropic / openai / glm
2. ask for that provider's API key
3. optionally save a custom base URL
4. optionally save a default model
5. set the selected provider as default

The configuration is saved to `~/.vangard/config.json`. Example structure:

```json
{
  "default_provider": "glm",
  "providers": {
    "anthropic": {
      "api_key": "base64-encoded-key",
      "base_url": "https://api.anthropic.com",
      "default_model": "claude-sonnet-4-20250514"
    },
    "openai": {
      "api_key": "base64-encoded-key",
      "base_url": "https://api.openai.com/v1",
      "default_model": "gpt-4"
    },
    "glm": {
      "api_key": "base64-encoded-key",
      "base_url": "https://open.bigmodel.cn/api/paas/v4",
      "default_model": "glm-4.5"
    }
  }
}
```

### Run

```bash
python -m src.cli          # Start REPL
python -m src.cli --help   # Show help
```

That's all it takes: clone, configure, run.

***

## 💡 Usage

### REPL Commands

| Command      | Description           |
| ------------ | --------------------- |
| `/`          | Show commands & skills |
| `/help`      | Show all commands     |
| `/save`      | Save session          |
| `/load <id>` | Load session          |
| `/multiline` | Toggle multiline mode |
| `/clear`     | Clear history         |
| `/exit`      | Exit REPL             |

### Writing Skills

*A skill is a spell you write once and cast again and again.*

Skills are slash commands written in Markdown and stored under `.vangard/skills`. Each skill lives in its own directory, and its file must be named `SKILL.md`.

**1) Create a project skill**

```text
<project-root>/.vangard/skills/<skill-name>/SKILL.md
```

Example:

```md
---
description: Explains code with diagrams and analogies
when_to_use: Use when explaining how code works
allowed-tools:
  - Read
  - Grep
  - Glob
arguments: [path]
---

Explain the code in $path. Start with an analogy, then draw a diagram.
```

**2) Use it in the REPL**

```text
❯ /
❯ /<skill-name> <args>
```

Example:

```text
❯ /explain-code qsort.py
```

**Notes**

- User-level skills: `~/.vangard/skills/<skill-name>/SKILL.md`
- Tool limits: `allowed-tools` controls which tools the skill can use.
- Arguments: use `$ARGUMENTS`, `$0`, `$1`, or named args like `$path` (from `arguments`).
- Placeholder syntax: use `$path`, not `${path}`.

***

## 📦 Project Structure

```text
vangardCLI/
├── src/
│   ├── cli.py           # CLI entry
│   ├── providers/       # LLM providers
│   ├── repl/            # Interactive REPL
│   ├── skills/          # SKILL.md loading and creation
│   └── tool_system/     # Tool registry, loop, validation
├── tests/               # Core test suite
├── .vangard/
│   └── skills/          # Project-local custom skills
└── FEATURE_LIST.md      # Current feature status
```

***

## 🤝 Contributing

*Fireteams welcome.*

```bash
# Quick dev setup
pip install -e .[dev]
python -m pytest tests/ -v
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

***

## 📖 Documentation

- **[SETUP_GUIDE.md](docs/guide/SETUP_GUIDE.md)**: detailed installation
- **[CONTRIBUTING.md](CONTRIBUTING.md)**: development guide
- **[TESTING.md](docs/guide/TESTING.md)**: testing guide
- **[CHANGELOG.md](CHANGELOG.md)**: version history

***

## 🔒 Security

*Knowledge is power. Guard both.*

- Keep sensitive data out of Git
- API keys are stored in the config encoded, not encrypted
- `.env` files are git-ignored
- Intended for local development

***

## 📄 License

MIT License. See [LICENSE](LICENSE).

***

## 🙏 Acknowledgments

- Based on the Claude Code architecture
- An independent educational project
- Not affiliated with Anthropic or Bungie

***

<div align="center">

*"We study, we build, we share what we learn."*

If this tool helped you, a ⭐ on the repo helps it reach other Guardians.

**Written by dea6cat**

[⬆ Back to Top](#-vangardcli)

</div>
