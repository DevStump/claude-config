# Dev Environment Startup Command

## Quick Start
`/user:dev-start` - Complete development environment setup

## What This Does

Automates the entire development startup process:

1. **Docker Check & Start**
   - Checks if Docker Desktop is running
   - Prompts to start Docker if not running
   - Waits for Docker to be ready

2. **Database Services**
   - Starts PostgreSQL, MySQL, Redis containers via `pnpm predev`
   - Ensures all containers are healthy

3. **Development Servers**
   - Starts backend API server (port 3333) via `pnpm bg:api:dev`
   - Starts frontend Expo server (port 1234) via `pnpm bg:expo:dev`
   - Monitors startup progress

4. **Authentication Setup**
   - Inserts test email code into database for easy login
   - Backend: localhost:3333/dev-login with bryanarendt@gmail.com / PASS1234
   - Frontend: localhost:1234 with email code PASS1234

## Manual Process (What This Automates)

If you want to do it manually:

```bash
# 1. Start Docker Desktop from Applications

# 2. Start database containers
pnpm predev

# 3. Start backend and frontend servers
pnpm bg:dev

# 4. Set up test login (if needed)
node scripts/insert-test-email-code.mjs

# 5. Access services
# Backend: http://localhost:3333/dev-login
#   Email: bryanarendt@gmail.com
#   Password: PASS1234
#
# Frontend: http://localhost:1234
#   Email: bryanarendt@gmail.com
#   Code: PASS1234
```

## Troubleshooting

### Docker Not Starting
- Open Docker Desktop manually from Applications folder
- Wait for Docker icon in menu bar to show "Docker Desktop is running"

### Port Already in Use
- Backend (3333): The bg:api:dev script auto-kills existing processes
- Frontend (1234): The bg:expo:dev script auto-kills existing processes

### Login Issues
- The script automatically ensures test email code exists
- Code is refreshed to stay valid (within 24 hours)
- Database must be running first (handled by predev)

## Command Options

- `/user:dev-start` - Full setup with prompts
- `/user:dev-start --skip-docker` - Skip Docker check (if already running)
- `/user:dev-start --servers-only` - Only start servers (skip Docker/DB)

## Related Commands

- `/user:dev-stop` - Stop all services
- `pnpm bg:status` - Check server status
- `pnpm bg:logs` - View recent logs
- `pnpm bg:restart` - Restart servers

## Implementation

The command will:
1. Check Docker status via `docker info`
2. If not running, prompt: "Docker not running. Please start Docker Desktop from Applications"
3. Run `pnpm predev` to start containers
4. Run `pnpm bg:dev` to start servers
5. Run `node scripts/insert-test-email-code.mjs`
6. Provide URLs and login info when ready