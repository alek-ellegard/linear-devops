# The Four Types of Work in DevOps

## Overview
Based on The Phoenix Project, all work in IT falls into four categories. Understanding and tracking these separately is crucial for managing flow and reducing bottlenecks.

## The Four Types

### 1. Business Projects 🎯
**Definition**: Work that directly delivers value to customers or generates revenue.

**Characteristics:**
- Comes from business/product requirements
- Has direct customer impact
- Usually has deadlines tied to business goals
- Highest visibility to leadership

**Examples in Linear:**
- New feature development
- Customer-requested enhancements
- Product launches
- API integrations for clients
- Mobile app features

**Linear Implementation:**
```
Label: work/business
Priority: High/Urgent
Project: Q1 Product Launch
Template: Feature Request
```

### 2. Internal Projects 🔧
**Definition**: Work that enables the organization to deliver business value more effectively.

**Characteristics:**
- Improves internal capabilities
- Often technical in nature
- May not be visible to customers
- Enables future business projects

**Examples in Linear:**
- Infrastructure upgrades
- CI/CD pipeline improvements
- Monitoring system implementation
- Documentation efforts
- Tool migrations
- Security hardening

**Linear Implementation:**
```
Label: work/internal
Priority: Medium
Project: Infrastructure Modernization
Template: Internal Improvement
```

### 3. Changes 🔄
**Definition**: Work generated from the first two types - modifications to existing systems.

**Characteristics:**
- Often scope creep from projects
- Updates to existing features
- Configuration changes
- Performance optimizations

**Examples in Linear:**
- Adding fields to existing APIs
- Updating deployment configurations
- Modifying database schemas
- Adjusting monitoring thresholds
- Changing business rules

**Linear Implementation:**
```
Label: work/changes
Priority: Based on parent project
Link: Related to original issue
Template: Change Request
```

### 4. Unplanned Work 🚨
**Definition**: Incidents and emergencies that interrupt planned work.

**Characteristics:**
- Disrupts all other work types
- Often caused by technical debt
- Creates negative cycle if not managed
- Most expensive type of work

**Examples in Linear:**
- Production outages
- Security incidents
- Critical bugs
- Emergency patches
- Data corruption issues
- "Everything is on fire" situations

**Linear Implementation:**
```
Label: work/unplanned
Priority: Urgent
Status: Skip Backlog → In Progress
Template: Incident Report
```

## The Hidden Cost of Unplanned Work

> "Unplanned work kills your ability to do planned work" - The Phoenix Project

### Impact Analysis
- **1 hour of unplanned work** = 2-3 hours of lost productive time (context switching)
- **Each incident** disrupts 3-5 people on average
- **Recovery time** = 23 minutes to regain focus after interruption

### Tracking in Linear

Create a dashboard to monitor:
```javascript
// Weekly Unplanned Work Ratio
unplanned_issues / total_issues * 100

// Target: < 20% of total work
// Warning: 20-30%
// Critical: > 30%
```

## Work Type Distribution

### Healthy Distribution (Target)
```
Business Projects:  40% ████████
Internal Projects:  30% ██████
Changes:           20% ████
Unplanned Work:    10% ██
```

### Unhealthy Distribution (Common)
```
Business Projects:  30% ██████
Internal Projects:  10% ██
Changes:           20% ████
Unplanned Work:    40% ████████ ⚠️
```

## Managing Work Types in Linear

### 1. Triage Process

**Daily Triage Meeting (15 min):**
1. Review all items in Triage status
2. Classify by work type
3. Assign appropriate labels
4. Route to correct workflow:
   - Business → Product Owner review
   - Internal → Tech Lead review
   - Changes → Link to parent project
   - Unplanned → Immediate action

### 2. Cycle Planning

**Allocation Strategy:**
```
Week 1:
- Monday-Wednesday: Business Projects (60%)
- Thursday: Internal Projects (20%)
- Friday: Changes & Tech Debt (20%)

Week 2:
- Monday-Tuesday: Business Projects (40%)
- Wednesday-Thursday: Internal Projects (40%)
- Friday: Buffer for Unplanned Work (20%)
```

### 3. Custom Views

Create these Linear views:

**"Current Sprint - By Type"**
- Group by: work/* labels
- Filter: Current cycle
- Sort: Priority descending

**"Unplanned Work Trend"**
- Filter: work/unplanned
- Time range: Last 30 days
- Chart: Created over time

**"Technical Debt Backlog"**
- Filter: work/internal AND tag/tech-debt
- Sort: Age (oldest first)

## Reducing Unplanned Work

### Strategy 1: Fix Root Causes
Track patterns in incidents:
```
Label combinations to watch:
- work/unplanned + component/authentication = Auth system needs refactoring
- work/unplanned + time/after-deployment = Deploy process needs improvement
- work/unplanned + day/monday = Weekend changes causing issues
```

### Strategy 2: Improve Internal Projects
Invest in:
- Better monitoring (catch issues before customers)
- Automated testing (prevent bugs)
- Documentation (reduce confusion)
- Automation (eliminate toil)

### Strategy 3: Manage Changes Better
- Require change advisory board (CAB) review
- Implement feature flags
- Use canary deployments
- Maintain change calendar

## Workflow by Work Type

### Business Projects
```
Triage → Backlog → Sprint Planning → Todo → In Progress → Review → Done → Released
        ↓
    Product Review
```

### Internal Projects
```
Triage → Tech Backlog → Todo → In Progress → Review → Done → Released
        ↓
    Tech Lead Review
```

### Changes
```
Triage → Impact Assessment → Todo → In Progress → Review → Done → Released
        ↓
    Link to Parent
```

### Unplanned Work
```
Incident Alert → In Progress → Review → Done → Post-Mortem
                ↓
            Skip Triage
```

## Reporting Metrics

### Weekly Metrics to Track

1. **Work Type Distribution**
   - Count of issues by type
   - Story points by type
   - Time spent by type

2. **Unplanned Work Impact**
   - Number of incidents
   - MTTR (Mean Time To Recovery)
   - Engineers interrupted

3. **Flow Efficiency**
   - Cycle time by work type
   - Blocked time
   - WIP limits adherence

### Monthly Review Questions

- Is unplanned work trending up or down?
- Which internal projects would reduce unplanned work?
- Are business projects being delayed by other work types?
- What changes are causing the most issues?

## Anti-Patterns to Avoid

### ❌ Everything is Urgent
If everything is urgent, nothing is. Use priority levels correctly.

### ❌ Ignoring Internal Work
Technical debt compounds. Allocate time for improvements.

### ❌ Not Tracking Unplanned Work
Can't improve what you don't measure.

### ❌ Changes Without Context
Always link changes to their source project/issue.

## Implementation Checklist

### Week 1: Setup
- [ ] Create work type labels
- [ ] Train team on classifications
- [ ] Set up triage process

### Week 2: Tracking
- [ ] Start labeling all work
- [ ] Create work type views
- [ ] Begin daily triage

### Week 3: Analysis
- [ ] Review work distribution
- [ ] Identify patterns in unplanned work
- [ ] Adjust cycle planning

### Week 4: Optimization
- [ ] Implement improvements
- [ ] Set work type targets
- [ ] Create dashboards

## Key Takeaways

1. **All work fits into four types** - Business, Internal, Changes, Unplanned
2. **Unplanned work is the enemy** - It disrupts everything else
3. **Track everything** - You can't manage what you don't measure
4. **Balance is crucial** - Neglecting any type creates problems
5. **Internal work prevents fires** - Invest in it to reduce unplanned work

## Next Steps

- Configure [LABELS.md](./LABELS.md) for work type tracking
- Set up [TEMPLATES.md](./TEMPLATES.md) for each work type
- Review [METRICS.md](./METRICS.md) for tracking effectiveness
