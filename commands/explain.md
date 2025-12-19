# Explain Command

Help understand complex code sections in the Dynasty Nerds codebase by providing clear, educational explanations.

## What to Explain

When given code or a file path with `$ARGUMENTS`, provide:

1. **High-level purpose** - What problem does this solve?
2. **How it works** - Step-by-step breakdown
3. **Key concepts** - Dynasty Nerds specific patterns
4. **Dependencies** - What it relies on
5. **Usage examples** - How/where it's used

## Explanation Structure

### For Functions/Methods
```
Purpose: [What it does in plain English]

Parameters:
- param1: [description and type]
- param2: [description and type]

Returns: [what it returns and why]

How it works:
1. [Step 1 explanation]
2. [Step 2 explanation]

Example usage:
[Code example]

Related: [Links to similar functions or docs]
```

### For Components
```
Purpose: [What UI/functionality it provides]

Props:
- prop1: [purpose and type]
- prop2: [purpose and type]

State management:
- [What state it uses/modifies]

User interactions:
- [What users can do]

Renders:
- [What it displays]

Used in: [Where this component appears]
```

### For Complex Logic

Break down into:
1. **Input** - What data comes in
2. **Processing** - Transformation steps
3. **Output** - What gets returned/saved
4. **Side effects** - Database updates, API calls

## Dynasty Nerds Specific Patterns

### League Sync
Explain:
- Platform API integration (Sleeper, ESPN, etc.)
- Data transformation pipeline
- Database storage strategy
- Error handling approach

### Fantasy Scoring
Explain:
- Scoring system rules
- Projection calculations
- Value computations
- Ranking algorithms

### UI Architecture
Explain:
- Legacy (nerd-core-rn) vs v3.0 (reusables)
- State management with Zustand
- Navigation with Expo Router
- Theme/styling approach

## Code Quality Insights

Also explain:
- **Why** it's written this way
- **Trade-offs** made
- **Potential improvements**
- **Common pitfalls** to avoid

## Learning Focus

Remember the user is a novice programmer, so:
- Avoid excessive jargon
- Relate to concepts they know
- Provide analogies when helpful
- Suggest related documentation to read

## Example Explanations

### Simple
"This function fetches league data from Sleeper's API, transforms it to match our database schema, and saves it. It's called whenever a user syncs their leagues."

### Detailed
"This BullMQ job processor handles league sync operations:
1. Receives a job with league ID and platform
2. Calls the appropriate platform parser
3. Transforms the data using our standardized format
4. Updates the database with new information
5. Publishes a Socket.IO event to update the UI
It uses retry logic for API failures and logs errors to Datadog."

## Additional Context

Always mention:
- Where to find tests for this code
- Related documentation in /docs
- Similar patterns elsewhere in codebase
- Who to ask for more details (senior dev areas)

The goal is to help the user understand not just WHAT the code does, but WHY it's structured this way and HOW it fits into the larger system.