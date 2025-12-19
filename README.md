# .claude Folder Guide

## Quick Reference

**What Claude Reads Automatically:**
- ✅ Only `.md` files in the **root** `.claude/` folder
- ❌ Files in subfolders are NOT auto-read (must be referenced explicitly)

**Current Active Files:**
- `CLAUDE.md` - Your workflow preferences and daily instructions
- `README.md` - This file (folder structure guide)

## Folder Structure

### In GitHub Repository
```
.claude/
├── CLAUDE.md              # Core workflow preferences (auto-read)
├── README.md              # This guide (auto-read)
├── settings.json          # Claude configuration
├── settings.local.json    # Git safety and permissions
│
├── commands/              # Reusable global commands
│   ├── daily-sync.md      # Sync with main, update dependencies
│   ├── debug.md           # Debug issues systematically
│   └── explain.md         # Get explanation of code
│
└── agents/                # Specialized AI agents
    ├── pr-assistant.md    # Help create pull requests
    └── test-writer.md     # Generate test files
```

### Local Only (Gitignored)
```
.claude/
├── projects/              # 📁 Conversation history (auto-managed)
├── todos/                 # 📁 Active todo lists
├── statsig/               # 📁 Telemetry data
├── shell-snapshots/       # 📁 Terminal session snapshots
├── ide/                   # 📁 IDE-specific settings
├── .last-cleanup          # 📄 Cleanup timestamp
└── .DS_Store              # 📄 Mac system file
```

## When to Add Files

### Root Directory (Auto-Read)
Only add files here if they should apply to **EVERY** Claude conversation:
- Global workflow preferences
- Universal rules or guidelines
- Daily operational instructions

### Subfolders (Manual Reference)
Use subfolders for content that's only needed occasionally:
- **commands/** - Reusable workflows accessed via `/user:command-name`
- **agents/** - Specialized agents for specific domains

## Best Practices

1. **Keep Root Minimal** - Only essential, daily-use files
2. **Organize by Topic** - Use subfolders for specific domains
3. **Archive Old Content** - Move outdated files to `archive/`
4. **Run Weekly Cleanup** - Auto-runs Sundays at 2am
5. **Review Quarterly** - Remove truly obsolete content

## Maintenance

- **Projects Folder**: Auto-managed by Claude (keeps recent conversations)
- **Todos Folder**: Stores active task lists
- **Local folders**: Not synced to GitHub, managed locally

## Key Files

| File | Purpose | When Modified |
|------|---------|--------------|
| CLAUDE.md | Core workflow rules | As needed |
| settings.json | Claude configuration | Rarely |
| settings.local.json | Security/permissions | Rarely |

## How to Use Commands & Agents

### 📝 Commands (Direct Execution)
Commands are markdown files that provide instructions for specific tasks.

**Usage:** `/user:command-name [optional arguments]`

**Available Commands:**
```bash
# Global Commands (from ~/.claude/commands/)
/user:daily-sync         # Sync with main, update dependencies
/user:explain [code]     # Get explanation of code/function
/user:debug [issue]      # Debug specific issue systematically
```

### 🤖 Agents (Task Delegation)
Agents are specialized AI assistants for complex tasks. You don't call them directly - ask Claude to use them.

**Usage:** "Use the [agent-name] agent to [task]"

**Available Agents:**
```bash
# Global Agents (from ~/.claude/agents/)
test-writer      # "Use test-writer agent to create tests for this feature"
pr-assistant     # "Use pr-assistant agent to help create a PR"
```

### Key Difference
- **Commands**: Quick, specific tasks you trigger directly
- **Agents**: Complex, multi-step tasks Claude delegates to specialists

## Need Help?

- Review CLAUDE.md for workflow preferences
- Use `/user:explain` to understand any complex code
- Use `/user:debug` to troubleshoot issues systematically
- Use `/user:daily-sync` to sync with main branch