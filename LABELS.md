# Linear Label Taxonomy for DevOps Teams

## Overview
A well-structured label system enables powerful filtering, reporting, and automation. This guide provides a comprehensive labeling strategy based on DevOps best practices.

## Label Hierarchy

### Primary Categories (Mutually Exclusive)

#### Work Type Labels (work/*)
**Purpose**: Classify work according to Phoenix Project categories

```yaml
work/business     # Customer-facing features
work/internal     # Infrastructure, tools, improvements  
work/changes      # Modifications to existing systems
work/unplanned    # Incidents, emergencies, firefighting
```

#### Type Labels (type/*)
**Purpose**: Specific classification of issue type

```yaml
type/feature      # New functionality
type/bug          # Defect in existing functionality
type/incident     # Production issue
type/documentation # Documentation work
type/infrastructure # Infrastructure changes
type/toil         # Manual, repetitive work
type/security     # Security-related work
type/tech-debt    # Technical debt
type/experiment   # Proof of concept, spike
```

### Secondary Categories (Multiple Allowed)

#### Priority Labels (priority/*)
**Purpose**: Urgency and importance classification

```yaml
priority/critical  # Production down, data loss risk
priority/high      # Significant impact, SLA risk
priority/medium    # Normal priority
priority/low       # Nice to have, no urgency
```

#### Value Labels (value/*)
**Purpose**: Track value delivery type

```yaml
value/customer     # Direct customer value
value/revenue      # Revenue impacting
value/cost-saving  # Reduces operational costs
value/risk-reduction # Mitigates risks
value/enabler      # Enables other work
value/automation   # Reduces manual work
```

#### Component Labels (component/*)
**Purpose**: System architecture mapping

```yaml
component/frontend     # UI/UX components
component/backend      # API, services
component/database     # Data layer
component/infrastructure # AWS, K8s, etc.
component/monitoring   # Observability stack
component/security     # Security components
component/ci-cd        # Pipeline, builds
```

#### Status Labels (status/*)
**Purpose**: Additional status information beyond workflow states

```yaml
status/blocked       # Waiting on dependency
status/needs-info    # Requires clarification
status/ready        # Ready to work
status/at-risk      # Deadline risk
status/on-hold      # Temporarily paused
```

### Operational Labels

#### Team Labels (team/*)
**Purpose**: Cross-team collaboration tracking

```yaml
team/platform      # Platform team
team/sre          # Site Reliability
team/security     # Security team
team/data         # Data engineering
```

#### Time Labels (time/*)
**Purpose**: Temporal tracking

```yaml
time/q1-2024      # Quarter tracking
time/sprint-23    # Sprint specific
time/urgent-week  # This week priority
time/next-cycle   # Next sprint
```

#### Environment Labels (env/*)
**Purpose**: Environment-specific issues

```yaml
env/production    # Production only
env/staging       # Staging environment
env/development   # Dev environment
env/all          # All environments
```

## Label Organization Strategies

### 1. Hierarchical Structure

Create label groups in Linear:

```
Work Classification
├── work/business
├── work/internal
├── work/changes
└── work/unplanned

Issue Types
├── type/feature
├── type/bug
├── type/incident
└── type/documentation

Priority Levels
├── priority/critical
├── priority/high
├── priority/medium
└── priority/low
```

### 2. Color Coding System

```yaml
Color Scheme:
  Red:        # Critical, incidents, blockers
  Orange:     # High priority, warnings
  Yellow:     # Medium priority, attention needed
  Green:      # Complete, good to go
  Blue:       # Informational, components
  Purple:     # Value tracking
  Gray:       # Low priority, archived
```

**Applied Colors:**
- `priority/critical` → Red (#FF0000)
- `work/unplanned` → Red (#FF0000)
- `type/incident` → Red (#FF0000)
- `priority/high` → Orange (#FFA500)
- `status/blocked` → Orange (#FFA500)
- `work/business` → Blue (#0066CC)
- `value/customer` → Green (#00AA00)
- `type/documentation` → Gray (#808080)

### 3. Naming Conventions

**Rules:**
1. Always lowercase
2. Use forward slash for hierarchy
3. No spaces (use hyphens)
4. Singular, not plural
5. Action-oriented when possible

**Good Examples:**
- ✅ `work/internal`
- ✅ `type/security`
- ✅ `component/auth-service`

**Bad Examples:**
- ❌ `Work/Internal` (wrong case)
- ❌ `bugs` (plural)
- ❌ `high priority` (space)

## Label Combinations for Common Scenarios

### Production Incident
```yaml
Required Labels:
- work/unplanned
- type/incident
- priority/critical OR priority/high
- env/production

Optional Labels:
- component/[affected-component]
- status/blocked (if waiting)
```

### Technical Debt Cleanup
```yaml
Required Labels:
- work/internal
- type/tech-debt
- priority/medium OR priority/low

Optional Labels:
- value/risk-reduction
- component/[area]
```

### Customer Feature Request
```yaml
Required Labels:
- work/business
- type/feature
- value/customer

Optional Labels:
- priority/[based-on-impact]
- time/[target-quarter]
```

### Toil Automation
```yaml
Required Labels:
- work/internal
- type/toil
- value/automation

Optional Labels:
- value/cost-saving
- component/[area]
```

## Label Automation Rules

### Auto-Labeling Triggers

```javascript
// Pseudo-code for Linear automation

// Auto-label based on title keywords
if (title.contains("down") || title.contains("outage")) {
  labels.add("work/unplanned", "type/incident", "priority/critical");
}

if (title.contains("[TOIL]")) {
  labels.add("work/internal", "type/toil", "value/automation");
}

// Auto-label based on template
if (template === "Customer Bug Report") {
  labels.add("work/business", "type/bug");
}

// Auto-label based on project
if (project === "Q1 Infrastructure") {
  labels.add("work/internal", "time/q1-2024");
}
```

### Label-Based Routing

```javascript
// Route based on labels
if (labels.contains("priority/critical")) {
  assignee = getOnCallEngineer();
  notify("#incidents-channel");
  skipTriage = true;
}

if (labels.contains("type/documentation")) {
  project = "Documentation Backlog";
  assignee = getTechWriter();
}
```

## Label Analytics

### Key Metrics to Track

#### Work Distribution
```sql
-- Weekly work type distribution
SELECT 
  work_label,
  COUNT(*) as issue_count,
  AVG(cycle_time) as avg_cycle_time
FROM issues
WHERE created_at > NOW() - INTERVAL '7 days'
GROUP BY work_label;
```

#### Toil Tracking
```sql
-- Monthly toil percentage
SELECT 
  COUNT(CASE WHEN 'type/toil' IN labels THEN 1 END)::float / 
  COUNT(*) * 100 as toil_percentage
FROM issues
WHERE created_at > NOW() - INTERVAL '30 days';
```

#### Incident Patterns
```sql
-- Component incident frequency
SELECT 
  component_label,
  COUNT(*) as incident_count
FROM issues
WHERE 'type/incident' IN labels
  AND created_at > NOW() - INTERVAL '90 days'
GROUP BY component_label
ORDER BY incident_count DESC;
```

## Label Governance

### Monthly Label Audit

1. **Review Usage**
   - Labels used < 5 times → Consider removal
   - Labels used > 100 times → Consider splitting

2. **Check Consistency**
   - Similar labels → Merge
   - Misspelled labels → Fix or remove
   - Orphaned labels → Archive

3. **Team Feedback**
   - Missing labels?
   - Confusing labels?
   - Automation improvements?

### Label Ownership

```yaml
Label Owners:
  work/*:      DevOps Lead
  type/*:      Tech Lead
  priority/*:  Product Manager
  component/*: Architecture Team
  value/*:     Business Analyst
```

## Common Anti-Patterns

### ❌ Over-Labeling
**Problem**: 10+ labels per issue
**Solution**: Use only essential labels (3-5 typical)

### ❌ Duplicate Concepts
**Problem**: `bug`, `defect`, `issue` all exist
**Solution**: Choose one, remove others

### ❌ Personal Labels
**Problem**: `john-reviewing`, `sarah-todo`
**Solution**: Use assignees and status instead

### ❌ Temporary Labels
**Problem**: `needs-discussion-tuesday`
**Solution**: Use comments or due dates

## Quick Reference Card

### Essential Label Combinations

| Scenario | Required Labels |
|----------|----------------|
| Production Down | `work/unplanned` + `type/incident` + `priority/critical` |
| Customer Bug | `work/business` + `type/bug` + `priority/high` |
| New Feature | `work/business` + `type/feature` + `value/customer` |
| Tech Debt | `work/internal` + `type/tech-debt` |
| Documentation | `work/internal` + `type/documentation` |
| Security Issue | `type/security` + `priority/critical` |
| Blocked Work | `status/blocked` |
| Automation | `type/toil` + `value/automation` |

### Label Decision Tree

```
Is it planned work?
├─ NO → work/unplanned
│   └─ Is production affected?
│       ├─ YES → type/incident + priority/critical
│       └─ NO → priority/high
└─ YES → Is it for customers?
    ├─ YES → work/business
    │   └─ New feature? → type/feature
    │       └─ Bug? → type/bug
    └─ NO → work/internal
        └─ Documentation? → type/documentation
            └─ Infrastructure? → type/infrastructure
                └─ Toil? → type/toil
```

## Implementation Checklist

### Week 1: Core Labels
- [ ] Create work/* labels
- [ ] Create type/* labels
- [ ] Create priority/* labels
- [ ] Set up color coding

### Week 2: Extended Labels
- [ ] Create component/* labels
- [ ] Create value/* labels
- [ ] Create status/* labels
- [ ] Configure label groups

### Week 3: Automation
- [ ] Set up auto-labeling rules
- [ ] Configure label-based routing
- [ ] Create label-based views
- [ ] Test automation flows

### Week 4: Refinement
- [ ] Audit label usage
- [ ] Remove unused labels
- [ ] Document label guide
- [ ] Train team

## Best Practices Summary

1. **Start Simple**: Begin with core labels, add as needed
2. **Be Consistent**: Follow naming conventions strictly
3. **Document Everything**: Maintain label descriptions
4. **Automate Where Possible**: Reduce manual labeling
5. **Review Regularly**: Monthly audits prevent label sprawl
6. **Train the Team**: Everyone should understand the system

## Next Steps

1. Configure [WORKFLOWS.md](./WORKFLOWS.md) for label-based routing
2. Set up [AUTOMATION.md](./AUTOMATION.md) for auto-labeling
3. Create [METRICS.md](./METRICS.md) dashboards using labels
