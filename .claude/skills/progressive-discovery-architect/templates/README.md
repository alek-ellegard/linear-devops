# Progressive Discovery Templates

Reusable templates for implementing progressive discovery documentation.

## Available Templates

### 1. docs-README.template.md
Main documentation hub template.

**When to use**: Starting a new project's documentation

**Customize**:
- Replace `{PROJECT_NAME}` with project name
- Replace `{project-name}` with kebab-case project identifier
- Replace `{Category N}` with your topic categories
- Replace `{Topic N}` with specific documentation topics
- Replace `{User Type N}` with target audience types

### 2. navigator-skill.template.md
Navigation skill template for `.claude/skills/{project-name}-navigator/SKILL.md`

**When to use**: Creating navigation skill after docs are structured

**Customize**:
- Replace `{project-name}` with kebab-case identifier
- Replace `{Project Name}` with display name
- Replace `{key concept N}` with core concepts
- Replace `{component N}` with code components
- Replace `{category}` with doc categories
- Replace `{ext}` with file extension (.py, .ts, .go, etc.)
- Update documentation map table
- Update navigation flows
- Customize file structure reference

### 3. NAVIGATION.template.md
Quick navigation reference guide template.

**When to use**: Creating supplementary navigation guide

**Customize**:
- Replace `{project-name}` with kebab-case identifier
- Update navigation patterns
- Customize file map
- Add project-specific tips

## Usage Pattern

### Step 1: Copy Template
```bash
cp .claude/skills/progressive-discovery-architect/templates/docs-README.template.md docs/README.md
```

### Step 2: Replace Placeholders
Find and replace all `{PLACEHOLDER}` values:
- `{PROJECT_NAME}` → "My Awesome Project"
- `{project-name}` → "my-awesome-project"
- `{Category 1}` → "Architecture"
- `{Topic 1}` → "System Overview"
- etc.

### Step 3: Customize Structure
Adapt sections to your project:
- Add/remove categories
- Adjust topic hierarchy
- Modify navigation paths
- Update examples

### Step 4: Validate
- [ ] All placeholders replaced
- [ ] Links work correctly
- [ ] Examples are project-specific
- [ ] File paths match actual structure

## Placeholder Reference

### Common Placeholders

| Placeholder | Example | Description |
|-------------|---------|-------------|
| `{PROJECT_NAME}` | "dotclaude" | Display name for project |
| `{project-name}` | "dotclaude" | Kebab-case identifier |
| `{Category N}` | "Architecture" | Documentation category |
| `{Topic N}` | "System Design" | Specific doc topic |
| `{User Type N}` | "Developers" | Target audience |
| `{key concept N}` | "Bundle" | Core domain concept |
| `{component N}` | "Loader" | Code component |
| `{category}` | "architecture" | Directory name |
| `{ext}` | "py" | File extension |
| `{command}` | "uv run load.py" | CLI command |

### Project-Specific Placeholders

Add your own placeholders for:
- Domain-specific terms
- Tool names
- API endpoints
- Configuration options

## Customization Examples

### Example 1: Python Library

```markdown
# MyLib Documentation

## Core Documentation

### API Reference
- [Core API](./api/core.md) - Main library API
- [Utilities](./api/utils.md) - Helper functions

### Architecture
- [Design Overview](./architecture/overview.md) - System design
```

### Example 2: Web Application

```markdown
# MyApp Documentation

## Core Documentation

### Features
- [Authentication](./features/auth.md) - User authentication
- [Dashboard](./features/dashboard.md) - Main dashboard

### Deployment
- [Setup Guide](./deployment/setup.md) - Installation
```

### Example 3: CLI Tool

```markdown
# MyCLI Documentation

## Core Documentation

### Commands
- [Command Reference](./commands/reference.md) - All commands
- [Recipes](./commands/recipes.md) - Common recipes

### Configuration
- [Config Guide](./config/guide.md) - Configuration options
```

## Validation Checklist

After using templates:

```markdown
Structure:
□ docs/README.md created from template
□ Categories match project needs
□ Topics are focused and scannable
□ File paths are correct

Navigation Skill:
□ .claude/skills/{project}-navigator/SKILL.md created
□ Description activates on relevant questions
□ Documentation map is complete
□ Navigation flows are accurate
□ Code structure matches project

Quick Reference:
□ docs/NAVIGATION.md created
□ File map is current
□ Success metrics defined
□ Pro tips are project-specific

Integration:
□ All placeholders replaced
□ Links work
□ Examples are concrete
□ Cross-references accurate
```

## Tips for Success

### 1. Start Small
Don't create all docs at once. Start with:
1. docs/README.md (hub)
2. docs/getting-started.md
3. docs/project-overview.md

Then expand as needed.

### 2. Iterate
Templates are starting points. Adjust based on:
- Project complexity
- User needs
- Common questions

### 3. Test Navigation
Try navigating as an LLM would:
1. Start at docs/README.md
2. Follow links for common questions
3. Verify you reach answers efficiently

### 4. Measure Efficiency
Track token usage:
- Before: How many tokens to answer?
- After: How many tokens with progressive discovery?
- Goal: 5-10x reduction

## See Also

- `../SKILL.md` - Complete workflow guide
- `../../../docs/` - Real implementation example
- `../../../wip/spec_model_research.md` - Research methodology
