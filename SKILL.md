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
# Log the user's prompt (include both raw and summary)
echo '{"type":"prompt","raw":"<exact user prompt up to 2000 chars>","content":"<brief summary of what user asked>"}' >> ~/.buildlog/agent-feed.jsonl

# Log your action with files modified
echo '{"type":"action","summary":"<what you did>","filesModified":["path/to/file1.ts","path/to/file2.ts"]}' >> ~/.buildlog/agent-feed.jsonl
```

### Example

User asks: "Add a dark mode toggle to the header component so users can switch between light and dark themes"

At the end of your response, run:
```bash
echo '{"type":"prompt","raw":"Add a dark mode toggle to the header component so users can switch between light and dark themes","content":"Add dark mode toggle to header"}' >> ~/.buildlog/agent-feed.jsonl
echo '{"type":"action","summary":"Added ThemeToggle component with sun/moon icons, integrated into Header, added useTheme hook","filesModified":["components/ThemeToggle.tsx","components/Header.tsx","hooks/useTheme.ts"]}' >> ~/.buildlog/agent-feed.jsonl
```

### Rules

1. **Always log** - Every response that involves code changes must be logged
2. **Include raw prompt** - Copy the user's exact prompt into `raw` (up to 2000 chars)
3. **Summarize** - Put a brief summary in `content` (under 200 chars)
4. **List files** - Include all files you created or modified in `filesModified`
5. **Use terminal** - Run the echo commands, don't just show them
6. **Log at the end** - After all your code changes are complete

### JSON Schema

```typescript
interface PromptEntry {
  type: 'prompt';
  raw?: string;              // Exact user prompt (up to 2000 chars)
  content: string;           // Brief summary (max 200 chars)
  context?: string[];        // Files referenced in the prompt
}

interface ActionEntry {
  type: 'action';
  summary: string;           // What was done (max 200 chars)
  filesModified?: string[];  // Relative paths of modified files
  filesCreated?: string[];   // Relative paths of created files
}

interface NoteEntry {
  type: 'note';
  content: string;           // Note content (max 200 chars)
  category?: 'observation' | 'decision' | 'blocker' | 'idea';
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
