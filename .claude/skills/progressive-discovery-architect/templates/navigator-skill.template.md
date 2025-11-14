---
name: {project-name}-navigator
description: Navigate {project-name} codebase efficiently using progressive discovery. Use when exploring this project, understanding its architecture, locating code, or answering questions about how it works. IMPORTANT - this skill teaches context-efficient navigation.
---

# {Project Name} Navigator

Navigate this codebase using progressive discovery principles - only load what you need.

## When to Use This Skill

- User asks about project structure or architecture
- Need to understand {key concept 1}, {key concept 2}, or {key concept 3}
- Looking for specific code ({component 1}, {component 2}, etc.)
- Want to understand {specifications/API/features}
- {Creating/modifying/using} {project artifacts}

## Navigation Strategy

### 1. Start with Documentation Hub

**Always start here first:**
```
Read: docs/README.md
```

This gives you:
- Complete navigation map
- Quick reference for key concepts
- Links to all specific topics

### 2. Progressive Loading Pattern

**Don't load everything!** Follow this pattern:

```
Question: "How does {concept} work?"
    ↓
1. Read docs/README.md (find relevant section)
    ↓
2. Read docs/{category}/{concept}.md ({concept} specs only)
    ↓
3. Done! (don't read unrelated docs)
```

### 3. Documentation Map

| Question | Read This File | Don't Read |
|----------|---------------|------------|
| How do I start? | `docs/getting-started.md` | Architecture, API |
| What does this do? | `docs/project-overview.md` | Implementation |
| How does it work? | `docs/architecture/overview.md` | Guides |
| What are {entities}? | `docs/{category}/{entities}.md` | Implementation |
| How do I use the API? | `docs/api/{reference}.md` | Other specs |
| {Specific question}? | `docs/{category}/{topic}.md` | Other topics |

## Code Navigation

### Core Implementation Files

**Only read code when documentation isn't sufficient:**

```
{main-module}/
├── {component1}.{ext}     # Description
├── {component2}.{ext}     # Description
└── {component3}.{ext}     # Description
```

### Example Navigation Flows

#### Flow 1: Understanding {Key Concept}
```
1. Read: docs/README.md (get overview)
2. Read: docs/{category}/{concept}.md (understand concept)
3. Stop here unless need implementation details
```

#### Flow 2: Using the {API/Tool/Feature}
```
1. Read: docs/README.md (find API section)
2. Read: docs/api/{reference}.md (API reference)
3. Look at: {example-file} (only if need examples)
```

#### Flow 3: {Common Task}
```
1. Read: docs/guides/{task}.md (full guide)
2. Look at: {example-directory}/ (example)
3. Use: {command} (test)
```

## File Structure Reference

```
{project-root}/
├── docs/                      # START HERE
│   ├── README.md             # Navigation hub
│   ├── getting-started.md    # Quick start
│   ├── project-overview.md   # Purpose & concepts
│   ├── {category1}/          # Category 1 docs
│   ├── {category2}/          # Category 2 docs
│   └── guides/               # How-to guides
│
├── {source-dir}/
│   ├── {component1}.{ext}    # Main components
│   └── {component2}.{ext}
│
├── {examples-dir}/           # Examples
└── {tests-dir}/              # Tests
```

## Quick Commands

```bash
# {Command description}
{command} --flag

# {Command description}
{command} --other-flag

# Show structure
tree {directory}
```

## Anti-Patterns (Don't Do This)

❌ **Bad**: Read all docs at once
```
Read: docs/README.md
Read: docs/getting-started.md
Read: docs/project-overview.md
Read: docs/{category}/*.md
... (wastes context)
```

✅ **Good**: Progressive discovery
```
Read: docs/README.md (navigation)
User asks: "How does {X} work?"
Read: docs/{category}/{X}.md (specific topic)
Done!
```

❌ **Bad**: Read code before docs
```
Read: {source}/{component}.{ext} (hard to understand without context)
```

✅ **Good**: Docs first, code if needed
```
Read: docs/api/{reference}.md (API reference with examples)
Then: Read {source}/{component}.{ext} (only if need implementation)
```

## Context Efficiency Rules

### Rule 1: Documentation First
- Always check docs/ before reading code
- Documentation has examples and explanations
- Code is raw implementation (harder to understand)

### Rule 2: Specific Before General
- Read specific topic doc, not everything
- Use docs/README.md to find right doc
- Don't load unrelated documentation

### Rule 3: Examples Over Implementation
- Look at {examples}/ before reading {source}/
- Real examples show practical usage
- Implementation can wait

### Rule 4: Test Your Understanding
- After reading, try to answer user's question
- Only load more if answer is incomplete
- Don't preemptively load "just in case"

## Common Questions - Quick Answers

**Q: What does this project do?**
```
Read: docs/project-overview.md
```

**Q: How do I {common task}?**
```
Read: docs/guides/{task}.md
Look at: {examples}/{task}/
```

**Q: What's the difference between {A} and {B}?**
```
Read: docs/{category}/{entities}.md (Comparison section)
```

**Q: How does {system/component} work?**
```
Read: docs/architecture/overview.md (System flow section)
Then: docs/api/{reference}.md (if need API details)
```

## Progressive Discovery Workflow

```
User Question
    ↓
1. Read docs/README.md
   └─ Find relevant section
    ↓
2. Read specific doc
   └─ Get targeted information
    ↓
3. Answer question
   └─ If answer incomplete, identify gap
    ↓
4. Read next specific doc
   └─ Fill knowledge gap only
    ↓
5. Stop when answer is complete
   └─ Don't keep loading "for context"
```

## Success Metrics

You're using this skill correctly when:
- ✅ You start with docs/README.md
- ✅ You read 1-3 docs max per question
- ✅ You can answer without reading code
- ✅ You know where to find information without reading it

You're NOT using it correctly when:
- ❌ You read all docs upfront
- ❌ You read code before documentation
- ❌ You can't find the right doc to read
- ❌ You load entire {source}/ directory

## Remember

**This project prioritizes context efficiency.**

The documentation is structured for progressive discovery because:
1. You don't need everything to answer most questions
2. Context windows are limited resources
3. Focused reading = faster, better answers
4. Over-loading context = waste and confusion

**Always start with docs/README.md and navigate from there.**
