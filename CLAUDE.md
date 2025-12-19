# CLAUDE.md - Workflow Configuration

## Git & GitHub Workflow Preferences

### Commit Review Process
- **Always show proposed commit message** before executing
- Format: "I'll commit with: [message]. Would you like to tweak this?"
- Accept user modifications to commit message
- Use clear, descriptive messages following convention: `type: description`

### Auto-Push Policy
- **EVERY commit = automatic push to GitHub**
- No exceptions - commit and push are always paired
- Rationale: Immediate backup and visibility for team
- **After push: Always merge main** to stay current and avoid conflicts
- Format: "Pushed! Now let's merge main to stay current"
- Command sequence: commit → push → pull main → merge main

### Branch Management at Work Start
- **Always check**: "We're on branch X. Is this correct for your work?"
- Suggest new branch creation when appropriate
- Branch naming: `feature/description`, `fix/issue`, `chore/task`
- Remind to create new branches for new features/fixes

### Merge Strategy (Team Convention)
- **Always use merge commits** (never rebase) - Lead dev preference
- PRs squash all commits into single commit when merging to main
- This makes merge vs rebase irrelevant for staying current
- Rebase avoided because it's complicated and causes more conflicts
- Simple workflow: merge main frequently to stay current

### PR Creation Triggers
- Track number of commits pushed
- When user indicates work is complete, suggest PR
- Create verbose, comprehensive PR descriptions
- Include all changes, testing notes, and impact

### Git Education Mode
- **Always provide terminal commands** for user to try
- Format: "💡 Try it yourself: `git command here`"
- Include brief explanation of what command does
- Applies to: merge, checkout, pull, stash, rebase

## ⚠️ CRITICAL: Dangerous Git Commands Protection

### Commands That Are BLOCKED (in settings.local.json)
- `git rebase -i` or `--interactive` - Can rewrite history
- `git reset --hard` - PERMANENTLY DELETES uncommitted work
- `git push --force` or `-f` - Can destroy remote history
- `git clean -fd` or `-fdx` - Deletes untracked files forever
- `git filter-branch` - Rewrites entire repository history
- `git branch -D main/master` - Prevents accidental main branch deletion

### Commands That Require Confirmation
- `git rebase` - Can alter commit history
- `git reset` - Can lose staged changes
- `git clean` - Removes untracked files
- `git cherry-pick` - Can create duplicate commits
- `git commit --amend` - Modifies existing commits

### Safety Rules
- **Always warn user** when suggesting any history-altering operations
- **Format warnings**: "⚠️ WARNING: This action cannot be undone!"
- **Require explicit confirmation** for dangerous operations
- **Safe alternatives**: Always suggest safe alternatives first

## Proactive Prompts

### During Work Sessions
- After significant changes: "Ready to commit these changes?"
- At work session start: "Should we create a new branch?"
- After multiple commits: "Ready to create a PR?"
- When switching context: "Should we stash current changes?"

### Commit Suggestions
- Meaningful feature implementation completed
- Significant refactoring or reorganization finished
- End of productive work session (multiple changes accumulated)
- Before starting risky/experimental changes (checkpoint)
- Documentation or configuration improvements completed

## Development Environment

### Quick Start Command
- Use `/user:dev-start` to automate entire startup process
- Starts Docker, databases, servers, and sets up test logins

### Login Credentials (Development)
**Backend** (http://localhost:3333/dev-login):
- Email: `bryanarendt@gmail.com`
- Password: `PASS1234`

**Frontend** (http://localhost:1234):
- Email: `bryanarendt@gmail.com`
- Email Code: `PASS1234`

## Todo Management

### Project Planning Files
- Always write to-do lists in `/claude-planning/`
- As todos are checked off in terminal, check off in file too
- When file is complete, move to `/claude-planning/completed/`

### Folder Structure
```
/claude-planning/
├── 📌_PRIORITIES.md  # Track project priorities
├── [root]           # Active plans ready to implement
├── /completed/      # Move here after implementation
├── /wont-do/        # User manually moves skipped plans
├── /learnings/      # Explanations and teachings
├── /for-later/      # User manually moves future plans
└── /documentation/  # Records of changes made
```

## Communication Guidelines

- Be brutally honest, don't be a yes man
- If I am wrong, point it out bluntly
- I need honest feedback on my code
- Keep responses concise and actionable
- Skip unnecessary explanations unless asked

## Daily Status Report

At the start of the first conversation each day:
- Check when cleanup script last ran: `cat ~/.claude/.last-cleanup 2>/dev/null || echo "Never"`
- Report .claude folder size with proper units: `du -sh ~/.claude | awk '{print $1}' | sed 's/M/MB/; s/G/GB/; s/K/KB/'`
- Only show this once per day maximum
- Format: "📊 Claude folder: [size] | Last cleanup: [date]"
- Keep it to one brief line at conversation start

## File Naming Conventions

- **Folders**: Use kebab-case (e.g., `user-data/`, `api-endpoints/`)
- **Python scripts**: Use snake_case (e.g., `data_processor.py`)
- **Markdown files**: 
  - Human-facing: kebab-case (e.g., `project-summary.md`)
  - AI-facing: snake_case (e.g., `system_prompt.md`)
  - Config files: UPPER_SNAKE_CASE (e.g., `WORKFLOW_PREFERENCES.md`)

## Code Quality for Senior Dev Review

### Before Every Commit
- **Run linting**: Always run `pnpm lint` before committing
- **Run type checking**: Always run `pnpm typecheck` before committing  
- **Run relevant tests**: Run tests for modified files
- **Format code**: Run `pnpm format` to ensure consistent style
- If any of these fail, fix issues before committing
- Tell me about any warnings or errors you can't fix

### Code Standards
- **No console.log statements** in production code (use proper logging)
- **No commented-out code** unless explaining something complex
- **No TODO comments** without creating an issue/task
- **Clear variable names** - avoid single letters except in loops
- **Add types** to all function parameters and returns
- **Keep functions small** - if over 50 lines, suggest splitting

### Testing Requirements
- **Always run tests** after making changes: `pnpm test:smart [file]`
- **Update tests** when changing functionality
- **Add tests** for new features (ask if unsure how)
- Tell me if tests are missing or if you're unsure how to test something

## Git Commits

- Never commit or push unless I specifically ask you to
- When I ask to commit, always show the message first for review
- Every commit automatically pushes to GitHub
- After every push, merge in latest main to avoid conflicts
- Workflow: lint → typecheck → test → commit → push → fetch main → merge main
- Suggest creating PRs after significant work is complete

## Conflict Prevention

### Before Starting Work
- **Always pull latest main** first: `git pull origin main`
- Check for any merge conflicts before starting
- If conflicts exist, help me resolve them before continuing

### During Development  
- **Merge main frequently** (every 2-3 commits)
- Keep commits small and focused (one logical change per commit)
- If working on same files as others, merge main more often

### PR Best Practices
- **Small PRs are better** - easier for senior dev to review
- Suggest breaking large changes into multiple PRs
- Include in PR description:
  - What changed and why
  - How to test the changes
  - Any risks or areas needing extra review
  - Screenshots if UI changes