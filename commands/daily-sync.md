# Daily Sync Command

Perform a complete sync with the main branch to start your day with a clean, up-to-date workspace.

## Steps to Execute

1. **Check current branch status**
   - Show current branch name
   - Check for uncommitted changes
   - If changes exist, ask whether to stash or commit them

2. **Fetch latest from remote**
   ```bash
   git fetch origin main
   ```

3. **Show what's new**
   - Display recent commits from team: `git log --oneline HEAD..origin/main`
   - Highlight any files you've been working on

4. **Merge main into current branch**
   ```bash
   git merge origin/main
   ```

5. **Check for dependency updates**
   - If package.json changed: run `pnpm install`
   - If schema.prisma changed: run `pnpm generate`
   - If migrations added: notify about `pnpm db:migrate:deploy`

6. **Verify environment is ready**
   - Check Docker is running
   - Verify database containers are up
   - Ensure development servers are ready with `pnpm bg:status`

7. **Run quick validation**
   ```bash
   pnpm typecheck
   pnpm lint
   ```

8. **Report status**
   Provide summary:
   - ✅ Branch updated with X new commits
   - ✅ Dependencies current
   - ✅ Database schema current  
   - ✅ Development environment ready
   - Any warnings or actions needed

## Conflict Resolution

If merge conflicts occur:
1. List conflicted files
2. Offer to help resolve them
3. Explain what each side changed
4. After resolution, run tests to ensure nothing broke

## Quick Health Check

After sync, quickly verify:
- No TypeScript errors
- No lint issues  
- Tests still pass for files you're working on

## Dynasty Nerds Specific

Check for updates in:
- Player data updates
- New platform integrations
- Scoring system changes
- UI component library updates (v3.0 changes)

This ensures you start each day conflict-free and aware of team changes!