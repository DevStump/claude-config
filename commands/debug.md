# Debug Command

Systematic debugging approach for Dynasty Nerds issues. Help identify and fix problems efficiently.

## Debug Workflow

### 1. Understand the Problem
- What is the expected behavior?
- What is actually happening?
- When did it start failing?
- Can it be reproduced consistently?

### 2. Gather Information

Check relevant logs:
```bash
# API logs
pnpm bg:api:logs

# Frontend logs  
pnpm bg:expo:logs

# Database logs
docker compose logs gm2-dev-db
```

### 3. Isolate the Issue

Determine the layer:
- **Frontend**: UI not updating, navigation issues
- **API**: Endpoints failing, wrong data returned
- **Database**: Query errors, missing data
- **External**: Platform API issues, third-party services
- **State**: Zustand store issues, cache problems

### 4. Add Strategic Logging

Add temporary console.logs to trace execution:
```typescript
console.log('🔍 DEBUG: [location] - [variable]:', variable);
```

Key locations:
- Function entry/exit points
- Before/after API calls
- State updates
- Error boundaries

### 5. Test Hypotheses

Common Dynasty Nerds issues:

#### Authentication Issues
- Check JWT token in localStorage
- Verify user session in database
- Test with dev credentials

#### League Sync Problems
- Check platform API status
- Verify league permissions
- Review transformation logic
- Check rate limiting

#### Data Display Issues
- Verify API response shape
- Check TypeScript types match
- Review Zustand state
- Test with different rank types

#### Performance Problems
- Check for N+1 queries
- Review React re-renders
- Check BullMQ job processing
- Monitor memory usage

### 6. Verification Steps

After identifying the issue:
1. Write a failing test that reproduces it
2. Fix the issue
3. Verify test now passes
4. Check for similar issues elsewhere
5. Remove all debug logging

## Dynasty Nerds Specific Debugging

### Database Queries
```bash
# Connect to database directly
DATABASE_URL_GM2="postgresql://postgres:postgres@0.0.0.0:5435/gm2" psql

# Check specific tables
\dt              # List tables
\d "TableName"   # Describe table
SELECT * FROM "TableName" LIMIT 10;
```

### API Testing
```bash
# Test endpoints directly
curl http://localhost:3333/api/endpoint \
  -H "Authorization: Bearer [token]"
```

### Frontend State
```javascript
// In browser console
localStorage.getItem('jwt-state')
localStorage.getItem('gm-store')
```

### Common Error Patterns

#### "Cannot read property of undefined"
- Check for missing null checks
- Verify data exists before accessing
- Add optional chaining (?.)

#### "Unique constraint violation"  
- Check for duplicate data
- Review upsert logic
- Verify database constraints

#### "Invalid token"
- Token expired
- Wrong environment
- User logged out elsewhere

#### "League not found"
- League hidden by user
- Platform sync failed
- Permissions changed

## Clean Up After Debugging

**IMPORTANT**: After fixing the issue:
1. Remove ALL console.log statements added
2. Remove any debug code
3. Ensure no sensitive data was logged
4. Update tests to prevent regression
5. Document the fix if it's non-obvious

## When to Escalate

Ask the senior developer when:
- Issue involves payment/billing
- Production data might be corrupted
- Security vulnerability suspected
- Can't reproduce the issue
- Fix requires architectural changes

## Debug Output Format

When reporting findings:
```
🐛 Issue: [Brief description]
📍 Location: [File:line]
🔍 Cause: [Root cause]
✅ Fix: [What was changed]
🧪 Test: [Test added/updated]
```

Remember: Good debugging is methodical. Don't guess - investigate, verify, then fix.