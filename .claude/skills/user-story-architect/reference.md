# User Story Architect - LLM Reference

## Core Pattern

The skill follows the pattern from CONSUL project:

1. **Project Context** → Understand what exists
2. **Current Understanding** → Document what you know
3. **Critical Questions** → Identify what you need to know
4. **Areas to Explore** → Plan discovery
5. **Next Steps** → Define actions

## User Story Quality

### Good Story
```
As an infrastructure engineer
I want one-command EC2 deployments
So that I can focus on service configuration instead of AWS details
```
- Specific user (not generic)
- Clear capability (what, not how)
- Business value explicit

### Bad Story
```
As a user
I want a REST API
So that the system is better
```
- Generic user
- Solution not need
- Vague value

## Question Patterns

### Transform Vague → Specific

| Vague Statement | Clarifying Questions |
|-----------------|---------------------|
| "It's slow" | How slow exactly? When? What's acceptable? |
| "Better monitoring" | What metrics? What alerts? Who gets notified? |
| "More secure" | What threats? What compliance? What access control? |
| "Easier to use" | What's hard now? How often? Who struggles? |

### Discovery Flow

1. **Start broad**: "Walk me through your workflow..."
2. **Drill into pain**: "What's most frustrating about that?"
3. **Quantify impact**: "How often does this happen?"
4. **Explore solutions**: "What would ideal look like?"
5. **Validate understanding**: "So you're saying..."

## User Group Identification

Look for differences in:
- **Roles**: Developer vs Operations vs Security
- **Frequency**: Daily users vs occasional users
- **Expertise**: Novices vs experts
- **Goals**: Speed vs stability vs compliance
- **Access**: Read-only vs read-write vs admin

## Extracting Requirements

### From Stories to Requirements

Story: "As a developer, I want automated deployments so that I can ship features faster"

Extracts to:
- **Functional**: System must support automated deployments
- **Performance**: Deployment time < 5 minutes
- **Security**: Deployments must use IAM roles
- **Integration**: Must integrate with existing CI/CD

### Requirement Categories

1. **Functional** (what it does)
2. **Non-Functional** (how well it does it)
   - Performance
   - Security
   - Reliability
   - Scalability
3. **Integration** (what it connects to)
4. **Constraints** (what limits it)

## Common Patterns

### Infrastructure Projects
- Multiple user groups (dev/ops/security)
- Focus on automation and self-service
- Security and compliance critical
- Integration with existing tools

### Developer Tools
- Speed and simplicity paramount
- Hide complexity
- Good defaults with escape hatches
- Clear error messages

### Migration Projects
- Backward compatibility crucial
- Phased rollout necessary
- Data integrity critical
- Rollback strategy required

## Anti-Patterns to Avoid

1. **Solutionizing**: User says "I need Kubernetes" → Ask "What problem are you solving?"
2. **Feature Creep**: Adding nice-to-haves → Focus on core value
3. **Single Perspective**: Only talking to one user type → Find all stakeholders
4. **Assumption Stacking**: Building on unvalidated assumptions → Verify baseline first
5. **Vague Acceptance**: "Make it better" → Define measurable success

## Output Quality Checklist

✅ **Complete Documentation Has:**
- Multiple user groups identified
- Specific, testable stories
- Questions with context
- Prioritized requirements
- Clear next steps

❌ **Red Flags:**
- Generic "as a user" stories
- Missing "so that" clauses
- Questions without context
- No validation planned
- Single user perspective

## Integration with Other Skills

- Use **progressive-discovery-architect** after stories are complete
- Feed requirements to technical design
- Stories drive test scenarios
- Questions become documentation sections