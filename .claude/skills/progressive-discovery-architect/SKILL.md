---
name: progressive-discovery-architect
description: Create progressive discovery documentation systems and navigation skills for codebases. Use when user wants to document a project with LLM-optimized structure, create navigation skills, or implement context-efficient documentation. This is a repeatable workflow pattern.
---

# Progressive Discovery Architect

Implement progressive discovery documentation systems that optimize for LLM context efficiency.

## When to Use This Skill

- User wants to document a codebase for LLM navigation
- Need to create "knowledge hub" style documentation
- Want to optimize documentation for context efficiency
- Creating navigation skills for codebases
- Implementing repeatable documentation patterns

## Core Principle

**Progressive Discovery**: Only load what you need, when you need it.

Traditional docs: Load everything upfront → waste 50k tokens
Progressive discovery: Navigate to specific topics → use 5k tokens per question

## The Pattern (What We Just Did)

### Phase 1: Research & Understand Domain
1. Deep research into domain model
2. Document all entity types and relationships
3. Create comprehensive research doc (for deep reference)

**Output**: `wip/spec_model_research.md`

### Phase 2: Create Documentation Hub
1. Design topic-focused doc structure
2. Create navigation README with progressive paths
3. Write concise, focused docs (one topic per file)

**Output**: `docs/` directory with hub structure

### Phase 3: Create Navigation Skill
1. Build skill that teaches navigation patterns
2. Include decision trees (question → file mapping)
3. Document anti-patterns and efficiency rules

**Output**: `.claude/skills/{project}-navigator/SKILL.md`

### Phase 4: Meta-Documentation
1. Create quick reference guides (like NAVIGATION.md)
2. Update main README with skill callout
3. Document the documentation system itself

**Output**: Meta-docs that explain the system

## Complete Workflow

### Step 1: Understand the Domain

**Goal**: Deep understanding before documentation

```markdown
Research checklist:
□ What is the project's purpose?
□ What are the core entities/concepts?
□ What are the relationships between them?
□ What questions will users/LLMs ask?
□ What are common use cases?
```

**Create**: Research document (can be verbose, it's for reference)
- Location: `wip/{topic}_research.md` or similar
- Include: Definitions, relationships, examples, open questions
- Quality: High completeness score (90%+)

### Step 2: Design Documentation Structure

**Goal**: Topic-focused hierarchy for progressive loading

```markdown
docs/
├── README.md                    # Navigation hub (always)
├── getting-started.md           # First steps
├── project-overview.md          # High-level concepts
├── {topic-1}/
│   └── {specific-doc}.md        # Focused topic docs
├── {topic-2}/
│   └── {specific-doc}.md
└── guides/
    └── {how-to-guide}.md
```

**Principles**:
- One topic per file (no megadocs)
- Clear hierarchy (topics in directories)
- README.md as navigation hub
- Predictable naming

### Step 3: Write Documentation Hub (README.md)

**Template**:

```markdown
# {Project} Documentation

**Progressive Discovery Knowledge Base**

IMPORTANT: Only load the knowledge you need.

## 🧭 For LLMs: Navigation Skill Available

Use the `{project}-navigator` skill for efficient navigation.

## Quick Links

- [Getting Started](./getting-started.md)
- [Project Overview](./project-overview.md)

## Core Documentation

### {Topic Category}
- [{Doc Title}](./{path}/{doc}.md) - Brief description

## Quick Reference

### Key Concepts
- **{Concept}**: Brief definition

### Key Commands
\`\`\`bash
command --example
\`\`\`
```

**Rules**:
- Include brief descriptions (helps LLM choose)
- Organize by topic/category
- Add quick reference section
- Point to navigation skill

### Step 4: Write Focused Topic Docs

**For each doc**:

```markdown
# {Topic Title}

Brief introduction (1-2 sentences).

## {Section 1}

Content focused on one aspect.

## {Section 2}

Another focused aspect.

## Examples

Concrete examples.

## Related

- [Related Doc 1](./path.md)
- [Related Doc 2](./path.md)
```

**Rules**:
- ✅ Single topic focus
- ✅ Scannable headings
- ✅ Code examples
- ✅ Tables for reference
- ❌ No tangents to other topics
- ❌ No duplicate content

### Step 5: Create Navigation Skill

**Location**: `.claude/skills/{project}-navigator/SKILL.md`

**Template**:

```markdown
---
name: {project}-navigator
description: Navigate {project} codebase efficiently using progressive discovery. Use when exploring this project, understanding its architecture, locating code, or answering questions about how it works.
---

# {Project} Navigator

Navigate this codebase using progressive discovery principles.

## When to Use This Skill

- User asks about project structure
- Need to understand {key concepts}
- Looking for specific code
- Want to understand specifications

## Navigation Strategy

### 1. Start with Documentation Hub

**Always start here first:**
\`\`\`
Read: docs/README.md
\`\`\`

### 2. Progressive Loading Pattern

**Don't load everything!** Follow this pattern:

\`\`\`
Question: "How does X work?"
    ↓
1. Read docs/README.md (find relevant section)
    ↓
2. Read docs/{topic}/{specific}.md (X specs only)
    ↓
3. Done! (don't read unrelated docs)
\`\`\`

### 3. Documentation Map

| Question | Read This File | Don't Read |
|----------|---------------|------------|
| How do I start? | \`docs/getting-started.md\` | Architecture, API |
| What does this do? | \`docs/project-overview.md\` | Implementation |
| How does it work? | \`docs/architecture/overview.md\` | Guides |

## Anti-Patterns (Don't Do This)

❌ Reading all docs at once
❌ Reading code before docs
❌ Loading unrelated context

✅ Progressive discovery
✅ Docs first, code if needed
✅ Specific topics only

## Context Efficiency Rules

### Rule 1: Documentation First
Always check docs/ before reading code

### Rule 2: Specific Before General
Read specific topic doc, not everything

### Rule 3: Stop When Done
Got the answer? Stop reading
```

**Key sections**:
- When to use (activation triggers)
- Navigation strategy (how to navigate)
- Documentation map (question → file)
- Anti-patterns (what NOT to do)
- Efficiency rules (best practices)

### Step 6: Create Quick Reference Guide

**Location**: `docs/NAVIGATION.md`

**Purpose**: Condensed navigation guide for quick reference

**Include**:
- Quick start (3 steps)
- File map (table format)
- Common questions → files
- Anti-patterns examples
- Success metrics

### Step 7: Validation

**Checklist**:
```markdown
Documentation Structure:
□ docs/README.md exists and is navigation hub
□ Each doc covers one focused topic
□ Clear hierarchy with directories
□ No duplicate content across docs

Navigation Skill:
□ Skill located in .claude/skills/
□ Description triggers on relevant questions
□ Includes decision trees (question → file)
□ Documents anti-patterns
□ Teaches efficiency rules

Integration:
□ Main README points to skill
□ NAVIGATION.md quick reference exists
□ All docs cross-reference appropriately
□ Examples demonstrate patterns
```

## Real Example: dotclaude Project

### What We Created

**Phase 1: Research**
- `wip/spec_model_research.md` - Complete domain research

**Phase 2: Documentation**
```
docs/
├── README.md                          # Hub
├── getting-started.md                 # Quick start
├── project-overview.md                # Concepts
├── architecture/overview.md           # System design
├── domain-model/entity-types.md       # Entities
├── api/models.md                      # API reference
├── claude-code/
│   ├── agents.md                      # Agent specs
│   └── skills.md                      # Skill specs
└── guides/create-bundle.md            # How-to
```

**Phase 3: Navigation Skill**
- `.claude/skills/dotclaude-navigator/SKILL.md`

**Phase 4: Meta-docs**
- `docs/NAVIGATION.md` - Quick reference
- `docs/SUMMARY.md` - Documentation index

### Results

**Before**: 50k tokens to understand basics
**After**: 5k tokens per question (10x efficiency)

**Before**: Load all docs, get confused
**After**: Navigate to specific topic, get answer

## Templates

### Minimal Setup (Small Project)

```
docs/
├── README.md              # Navigation hub
├── overview.md            # What/why/how
└── api.md                 # If applicable

.claude/skills/{project}-navigator/
└── SKILL.md               # Navigation skill
```

### Standard Setup (Medium Project)

```
docs/
├── README.md
├── getting-started.md
├── overview.md
├── architecture/
│   └── overview.md
├── api/
│   └── reference.md
└── guides/
    └── common-tasks.md

.claude/skills/{project}-navigator/
└── SKILL.md
```

### Full Setup (Large/Complex Project)

```
docs/
├── README.md
├── NAVIGATION.md          # Quick ref
├── SUMMARY.md             # Index
├── getting-started.md
├── overview.md
├── architecture/
│   ├── overview.md
│   └── components.md
├── domain-model/
│   └── entities.md
├── api/
│   └── reference.md
├── guides/
│   └── how-to.md
└── reference/
    └── specs.md

.claude/skills/{project}-navigator/
└── SKILL.md

wip/
└── research.md            # Deep research
```

## Adaptation Guidelines

### For Different Project Types

**Library/Framework**:
- Focus on API documentation
- Include usage examples
- Document patterns and best practices

**Application**:
- Focus on architecture and features
- Include user guides and workflows
- Document configuration and deployment

**Tool/CLI**:
- Focus on commands and usage
- Include examples and recipes
- Document configuration options

**Research/Experiment**:
- Focus on concepts and findings
- Include methodology and results
- Document open questions

### Scaling the Pattern

**Tiny project** (< 5 files):
- Single README.md with all info
- No navigation skill needed

**Small project** (5-20 files):
- docs/README.md + 2-3 topic docs
- Simple navigation skill

**Medium project** (20-100 files):
- Full docs/ structure with directories
- Comprehensive navigation skill
- Quick reference guide

**Large project** (100+ files):
- Multi-level docs/ hierarchy
- Navigation skill + meta-docs
- Multiple topic-specific skills

## Common Mistakes

### ❌ Mistake 1: Too Much in One Doc
**Problem**: Megadocs that cover everything
**Fix**: One topic per file, cross-reference related topics

### ❌ Mistake 2: No Navigation Hub
**Problem**: No clear starting point
**Fix**: Always create docs/README.md as hub

### ❌ Mistake 3: Code-First Documentation
**Problem**: Document code structure, not concepts
**Fix**: Document what/why before how/where

### ❌ Mistake 4: Missing Navigation Skill
**Problem**: LLM doesn't know efficient navigation patterns
**Fix**: Create navigation skill early

### ❌ Mistake 5: No Examples
**Problem**: Abstract explanations without concrete examples
**Fix**: Include code examples, file paths, command outputs

## Success Metrics

### Documentation Quality
- ✅ Can answer 80% of questions from docs alone
- ✅ Average 3-5k tokens per question
- ✅ LLM finds right doc in 1-2 hops
- ✅ No duplicate content across docs

### Navigation Efficiency
- ✅ Skill activates on relevant questions
- ✅ Clear decision trees (question → file)
- ✅ Anti-patterns documented
- ✅ Users report faster answers

### Maintainability
- ✅ Easy to update single topic
- ✅ Clear file organization
- ✅ No circular references
- ✅ Consistent formatting

## Workflow Checklist

Use this for each new project:

```markdown
□ Phase 1: Research
  □ Understand domain deeply
  □ Create research document
  □ Identify key concepts

□ Phase 2: Design Structure
  □ Plan docs/ hierarchy
  □ Choose template (minimal/standard/full)
  □ Decide topic categories

□ Phase 3: Write Documentation
  □ Create docs/README.md hub
  □ Write getting-started.md
  □ Write project-overview.md
  □ Write topic-specific docs
  □ Add code examples

□ Phase 4: Create Navigation Skill
  □ Write .claude/skills/{project}-navigator/SKILL.md
  □ Include decision trees
  □ Document anti-patterns
  □ Add efficiency rules

□ Phase 5: Meta-documentation
  □ Create docs/NAVIGATION.md
  □ Update main README
  □ Add SUMMARY.md if needed

□ Phase 6: Validate
  □ Test navigation paths
  □ Verify no duplicates
  □ Check cross-references
  □ Measure token efficiency
```

## Related Patterns

- **Research Context Engineering** - Deep research methodology (see user's context)
- **Progressive Disclosure** - UI pattern for revealing information gradually
- **Information Architecture** - Organizing content for findability
- **Context-Aware Documentation** - Docs that adapt to user needs

## Remember

**The goal is not comprehensive documentation.**
**The goal is context-efficient navigation.**

Traditional docs try to document everything upfront.
Progressive discovery docs help you find exactly what you need.

**Always optimize for the journey, not the destination.**

## Meta Note

This skill itself demonstrates the pattern:
- Focused topic (progressive discovery architecture)
- Clear sections (workflow, templates, examples)
- Decision trees (project type → template)
- Examples (dotclaude implementation)
- Anti-patterns (common mistakes)

Use this workflow to create similar documentation systems for any project.
