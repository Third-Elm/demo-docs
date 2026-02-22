# PRD Best Practices

## Requirements

### Be Specific

Bad: "The API should be fast"

Good: "The API must respond to all read requests within 200ms at P95"

### Be Testable

Every requirement should have correctness criteria that can be verified:

- "Users can create tasks" → "When a POST request is sent to /tasks with valid data, a 201 response is returned with the created task"

### Avoid Ambiguity

Words to avoid:

- "fast", "slow", "quickly"
- "user-friendly", "intuitive"
- "scalable", "performant"
- "should" (use "must" or "may")

## Structure

### Progressive Detail

- Start with the problem, not the solution
- Put the most important information first
- Link to details rather than embedding them

### Cross-References

- Link to related ADRs when requirements depend on technical decisions
- Reference other PRDs when initiatives are related
- Include paths to design docs or prototypes

## Common Mistakes

1. **Solution-izing too early**: Describe what you need, not how to build it
2. **Vague correctness criteria**: "Works correctly" is not testable
3. **Missing edge cases**: What happens when things fail?
4. **No priority**: All requirements are not equal

## Delta PRDs

When updating requirements in a new dated entry:

1. Link to previous PRD
2. State only what changed
3. Explicitly mark superseded sections
4. Keep the same structure for easy comparison
