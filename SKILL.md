---
name: buildlog
description: Automatically log AI coding sessions to buildlog.ai for replay and sharing
version: 1.0.0
author: buildlog.ai
repository: https://github.com/buildlog/skill
homepage: https://buildlog.ai
---

# Buildlog Skill

Log your AI-assisted coding sessions for replay on buildlog.ai.

## CRITICAL: Automatic Logging

**You MUST log your activity to `~/.buildlog/agent-feed.jsonl` when working in this project.**

At the END of EVERY response where you make changes or answer a coding question:

1. Append a JSON line summarizing what the user asked
2. Append a JSON line summarizing what you did

### Format

```bash
# Log the user's prompt
echo '{"type":"prompt","content":"<brief summary of what user asked>"}' >> ~/.buildlog/agent-feed.jsonl

# Log your action with files modified
echo '{"type":"action","content":"<what you did>","filesModified":["path/to/file1.ts","path/to/file2.ts"]}' >> ~/.buildlog/agent-feed.jsonl
```

### Example

User asks: "Add a dark mode toggle to the header"

At the end of your response, run:
```bash
echo '{"type":"prompt","content":"Add dark mode toggle to header"}' >> ~/.buildlog/agent-feed.jsonl
echo '{"type":"action","content":"Added ThemeToggle component with sun/moon icons, integrated into Header, added useTheme hook","filesModified":["components/ThemeToggle.tsx","components/Header.tsx","hooks/useTheme.ts"]}' >> ~/.buildlog/agent-feed.jsonl
```

### Rules

1. **Always log** - Every response that involves code changes must be logged
2. **Be concise** - Keep content under 200 characters
3. **List files** - Include all files you created or modified in `filesModified`
4. **Use terminal** - Run the echo commands, don't just show them
5. **Log at the end** - After all your code changes are complete

### JSON Schema

```typescript
interface FeedEntry {
  type: 'prompt' | 'action' | 'note';
  content: string;           // Brief description (max 200 chars)
  filesModified?: string[];  // Relative paths of modified files
  filesCreated?: string[];   // Relative paths of created files
}
```

## Why This Matters

Buildlog captures AI coding sessions so developers can:
- Share how they built something
- Learn from others' workflows  
- Create tutorials and documentation
- Review and debug past sessions

The VS Code extension watches `~/.buildlog/agent-feed.jsonl` and incorporates your logs into the recording automatically.

## More Info

- Website: https://buildlog.ai
- VS Code Extension: Search "Buildlog" in marketplace
- Upload recordings: https://buildlog.ai/upload
