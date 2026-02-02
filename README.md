# Buildlog Skill

> Automatically log AI coding sessions to [buildlog.ai](https://buildlog.ai) for replay and sharing.

## Installation

```bash
npx skills add buildlog/skill
```

## What it does

This skill instructs AI agents to log their prompts and actions to `~/.buildlog/agent-feed.jsonl`. The [Buildlog VS Code extension](https://marketplace.visualstudio.com/items?itemName=buildlog.buildlog-recorder) watches this file and incorporates the logs into your recording.

## Usage

1. Install the skill in your project
2. Install the VS Code extension
3. Start a recording (`Cmd/Ctrl+Shift+R`)
4. Work with your AI agent as normal
5. Stop recording and upload to buildlog.ai

The agent will automatically log what you asked and what it did.

## Compatible Agents

Works with any agent that supports skills.sh:
- GitHub Copilot
- Cursor
- Claude Code
- Windsurf
- Cline
- And more...

## Links

- [buildlog.ai](https://buildlog.ai) - View and share buildlogs
- [VS Code Extension](https://marketplace.visualstudio.com/items?itemName=buildlog.buildlog-recorder)
- [OpenClaw Skill](https://github.com/buildlog/openclaw-skill) - Full programmatic integration for OpenClaw runtime

## License

MIT
