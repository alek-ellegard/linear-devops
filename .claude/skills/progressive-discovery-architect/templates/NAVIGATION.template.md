# Navigation Guide for LLMs

Quick reference for efficiently navigating this codebase.

## 🎯 Primary Skill

**Use the `{project-name}-navigator` skill** for all navigation needs.

Location: `.claude/skills/{project-name}-navigator/SKILL.md`

## 🚀 Quick Start for LLMs

### Step 1: Always Start Here
```
Read: docs/README.md
```

### Step 2: Navigate to Specific Topic
Based on the question, read **one** of these:

| Question Type | Read This |
|---------------|-----------|
| Getting started | `docs/getting-started.md` |
| What is this? | `docs/project-overview.md` |
| How does it work? | `docs/architecture/overview.md` |
| {Specific question} | `docs/{category}/{topic}.md` |

### Step 3: Stop When You Have the Answer
Don't keep loading files "just in case"!

## 📋 Navigation Patterns

### Pattern 1: Understanding Concepts
```
Question: "{Conceptual question}?"

Flow:
1. Read docs/README.md → find relevant section
2. Read docs/{category}/{topic}.md → read explanation
3. Answer with specific details
4. Stop (don't read code, other docs, etc.)
```

### Pattern 2: Using the {API/Tool}
```
Question: "How do I {use feature}?"

Flow:
1. Read docs/README.md → find API/Guide section
2. Read docs/{api/guides}/{reference}.md → find usage
3. Copy example code
4. Stop (documentation has complete examples)
```

## ⚠️ Anti-Patterns (Don't Do This)

### ❌ Reading Everything Upfront
```
# BAD - wastes 50k tokens
Read: docs/README.md
Read: docs/getting-started.md
Read: docs/project-overview.md
Read: docs/architecture/overview.md
... (continues loading everything)
```

### ✅ Progressive Discovery
```
# GOOD - uses only 5k tokens
Read: docs/README.md
User asks: "How does {X} work?"
Read: docs/{category}/{X}.md
Answer question
Done!
```

## 🎓 Context Efficiency Rules

### Rule 1: Documentation > Code
Read docs first, only read code if docs don't answer

### Rule 2: Specific > General
Target the exact doc you need, not adjacent ones

### Rule 3: One Topic at a Time
Answer one question with one doc

### Rule 4: Stop When Done
Got the answer? Stop reading

## 🗺️ File Map Reference

```
docs/README.md              ← START HERE (always)
├── getting-started.md      ← Installation
├── project-overview.md     ← Purpose & concepts
├── {category1}/
│   └── {topic}.md          ← Specific topics
└── guides/
    └── {task}.md           ← How-to guides
```

## 💡 Pro Tips

1. **Bookmark docs/README.md** - it's your map
2. **Read descriptions** - they tell you what each doc contains
3. **Use decision trees** - they guide you to the right doc
4. **Trust the structure** - docs are organized for progressive discovery

## 📊 Success Metrics

### Doing it right:
- ✅ Start with docs/README.md
- ✅ Read 1-3 docs per question
- ✅ Answer without code
- ✅ Use <5k tokens per question

### Doing it wrong:
- ❌ Load all docs upfront
- ❌ Read code before docs
- ❌ Can't find right doc
- ❌ Use >20k tokens per question

---

**Remember**: Progressive discovery = context efficiency = better answers faster
