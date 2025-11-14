---
name: user-story-architect
description: Create and refine user stories through systematic interview patterns and structured documentation. Use when gathering requirements, conducting user interviews, creating user-stories.md files, or translating user needs into technical requirements. Optimized for LLM-driven requirement discovery.
allowed-tools: Read, Write, Edit, Grep, Glob, TodoWrite, AskUserQuestion
---

# User Story Architect

LLM-optimized system for capturing and refining user requirements through structured discovery and documentation.

## When to Use

Activate this skill when:
- Creating or updating user-stories.md
- Conducting requirements discovery with users
- Refactoring projects need user context captured
- Multiple user groups have conflicting needs
- Translating vague requirements into concrete stories

## Core Pattern (from CONSUL example)

### 1. Project Context
Document the current state and vision:
- What exists today (infrastructure, workflow, pain points)
- Who uses it (distinct user groups)
- What constraints are immutable
- What success looks like

### 2. Current Understanding
Capture what you know so far:
- Key requirements identified
- User stories drafted
- Technical decisions made
- Integration points mapped

### 3. Critical Questions
Generate specific questions organized by topic:
- Each question should have context (why it matters)
- Focus on concrete details, not abstracts
- Include examples to clarify what you're asking
- Explain impact on design/implementation

### 4. Areas Needing Exploration
Identify gaps in understanding:
- Workflows not yet mapped
- Edge cases not considered
- Integration details unclear
- Performance requirements unknown

## User Story Format

```
As a [specific user type]
I want [specific capability]
So that [business value/outcome]
```

**Quality Check:**
- User type is specific role, not generic "user"
- Capability describes what, not how
- Business value explains why this matters
- Story can be tested/validated
- Story can be implemented independently

## Question Generation Patterns

### For Each User Story, Ask:

**The What**
- What exactly does [feature] mean to you?
- What does success look like?
- What's included? What's not?

**The How Often**
- How frequently do you [action]?
- Is this daily/weekly/monthly?
- Peak times? Quiet times?

**The Current State**
- How do you handle this today?
- What tools do you use?
- How long does it take?
- What breaks?

**The Pain**
- What's most frustrating?
- Where do errors occur?
- What wastes time?
- What would you fix first?

**The Edge Cases**
- What if [component] fails?
- How do you rollback?
- What about migrations?
- Security concerns?

## Documentation Structure

```markdown
# [Project] User Stories

## Project Context
[Current state, vision, constraints]

## User Groups
### Group 1: [Name]
- Who they are
- What they need
- Current pain points

### Group 2: [Name]
[Repeat for each group]

## Current Understanding
### Requirements Identified
1. [Requirement with source]
2. [Requirement with source]

### User Stories (Draft)
[Stories organized by user group]

## Critical Questions

### Topic: [Area]
**Context**: [Why these questions matter]

**Questions**:
1. [Specific question]
   - Why it matters: [Impact]
   - Example: [Clarify with example]

2. [Next question]
   [Continue pattern]

## Areas Needing Exploration
### [Topic]
- What we know:
- What we need to learn:
- How to learn it:

## Next Steps
1. [Action with owner]
2. [Action with owner]
```

## Working Process

### Step 1: Read Existing Context
```bash
# Find existing requirements/stories
find . -type f -name "*.md" | xargs grep -l "user stor\|requirement\|As a"

# Look for TODOs indicating gaps
grep -r "TODO\|FIXME" --include="*.md"
```

### Step 2: Identify User Groups
Look for:
- Different roles (Developer vs Operations)
- Different access levels (Admin vs User)
- Different workflows (Creator vs Consumer)
- Different expertise (Expert vs Novice)

### Step 3: Extract Stories from Conversations
Transform statements like:
- "Deployments take forever" → "As a developer, I want faster deployments so that I can iterate quickly"
- "I never know what broke" → "As an operator, I want detailed error logs so that I can diagnose issues quickly"

### Step 4: Generate Critical Questions
For each story, ask:
1. Clarification (what exactly?)
2. Frequency (how often?)
3. Current state (what now?)
4. Pain points (what hurts?)
5. Success criteria (how to measure?)

### Step 5: Iterate Based on Answers
- Refine stories with new information
- Split compound stories
- Add discovered requirements
- Update priorities based on impact

## Templates

Use provided templates in `templates/`:
- `user-stories.template.md` - Complete structure
- `requirements.template.md` - Extracted requirements
- `interview-guide.template.md` - Question preparation

## Quality Indicators

✅ **Good User Story Documentation:**
- Multiple user groups identified
- Stories have clear business value
- Questions have context explaining why they matter
- Concrete examples from users
- Dependencies mapped
- Priorities based on impact

❌ **Red Flags:**
- Generic "as a user" stories
- Technical solutions masquerading as requirements
- No "so that" clauses
- Questions without context
- Single user perspective
- No validation planned

## Integration Points

Works with:
- **progressive-discovery-architect**: After stories, create navigation
- **requirements-engineer**: Transform stories to technical specs
- **domain-modeler**: Map stories to domain model