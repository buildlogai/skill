---
name: buildlog
description: Automatically log AI coding sessions to buildlog.ai for replay and sharing
version: 1.0.0
author: buildlog.ai
repository: https://github.com/buildlog/skill
homepage: https://buildlog.ai
---

# Buildlog Skill

## MANDATORY: Log Every Response

You MUST run this at the END of EVERY response where you make changes:

```bash
echo '{"type":"prompt","content":"<what user asked>"}' >> ~/.buildlog/agent-feed.jsonl
echo '{"type":"action","summary":"<what you did>","filesModified":["file1.ts"]}' >> ~/.buildlog/agent-feed.jsonl
```

**DO NOT SKIP THIS.** The buildlog extension watches this file to record the session.

## Quick Reference

- `type: "prompt"` - Log the user's request (summarize in `content`)
- `type: "action"` - Log what you did (include `filesModified` array)
- `type: "note"` - Optional observations or decisions

## Example

User: "Add a login button to the header"

After making changes, run:
```bash
echo '{"type":"prompt","content":"Add login button to header"}' >> ~/.buildlog/agent-feed.jsonl
echo '{"type":"action","summary":"Added LoginButton component to Header with auth integration","filesModified":["components/Header.tsx","components/LoginButton.tsx"]}' >> ~/.buildlog/agent-feed.jsonl
```

## JSON Schema

```typescript
interface PromptEntry {
  type: 'prompt';
  raw?: string;              // Exact user prompt (up to 2000 chars)
  content: string;           // Brief summary (max 200 chars)
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
}
```

## Why This Matters

Buildlog captures AI coding sessions so developers can:
- Share how they built something
- Learn from others' workflows  
- Create tutorials and documentation

**Remember: Log at the END of your response, AFTER all code changes.**
