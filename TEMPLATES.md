# Linear Issue Templates for DevOps Teams

## Overview
Well-designed templates ensure consistent issue creation, capture necessary information, and reduce back-and-forth clarification.

## Template Categories

### 🎯 Business Work Templates

#### Feature Request Template
```markdown
## Summary
[One-line description of the feature]

## Business Value
- **Customer Impact**: [How this helps users]
- **Revenue Impact**: [Estimated value]
- **Strategic Alignment**: [Which goal this supports]

## Requirements
### Functional Requirements
- [ ] Requirement 1
- [ ] Requirement 2

### Non-Functional Requirements
- Performance: [Expected metrics]
- Security: [Requirements]
- Scalability: [Expected load]

## Success Criteria
- [ ] Metric 1 achieved
- [ ] User story completed
- [ ] Documentation updated

## Dependencies
- [ ] API team approval
- [ ] Database migration
- [ ] Third-party service setup

---
Labels: work/business, type/feature
Project: [Auto-assign to current quarter]
Estimate: [T-shirt size]
```

#### Customer Bug Report Template
```markdown
## Bug Summary
[Brief description]

## Environment
- **Affected Service**: [Service name]
- **Environment**: [ ] Production [ ] Staging [ ] Development
- **First Seen**: [Date/time]
- **Frequency**: [ ] Constant [ ] Intermittent [ ] Once

## Impact
- **Affected Users**: [Number/percentage]
- **Business Impact**: [Revenue/operations impact]
- **Workaround Available**: [ ] Yes [ ] No

## Steps to Reproduce
1. Step one
2. Step two
3. Expected: [What should happen]
4. Actual: [What actually happens]

## Evidence
- Error messages: 
- Screenshots: 
- Log snippets: 
- Monitoring links: 

## Root Cause (if known)
[Initial investigation findings]

---
Labels: work/business, type/bug, priority/high
Template: Customer Bug
SLA: 4 hours
```

### 🔧 Internal Work Templates

#### Infrastructure Improvement Template
```markdown
## Improvement Summary
[What we're improving and why]

## Current State
- **Problem**: [What's wrong now]
- **Pain Points**: [Specific issues]
- **Technical Debt**: [What debt this addresses]

## Proposed Solution
- **Approach**: [High-level solution]
- **Technologies**: [Tools/services to use]
- **Timeline**: [Estimated duration]

## Benefits
- [ ] Performance improvement: [Metrics]
- [ ] Cost reduction: [Amount]
- [ ] Reliability increase: [SLA improvement]
- [ ] Developer experience: [Time saved]

## Implementation Plan
1. Phase 1: [Description]
2. Phase 2: [Description]
3. Rollback plan: [How to revert]

## Risks
- Risk 1: [Description] - Mitigation: [Plan]
- Risk 2: [Description] - Mitigation: [Plan]

---
Labels: work/internal, type/infrastructure
Project: Infrastructure Modernization
Estimate: [Story points]
```

#### Documentation Task Template
```markdown
## Documentation Need
[What needs to be documented]

## Type
[ ] Architecture Diagram
[ ] Runbook
[ ] API Documentation
[ ] User Guide
[ ] Configuration Guide
[ ] Troubleshooting Guide

## Audience
- Primary: [Who will use this]
- Secondary: [Who else needs it]

## Current State
- [ ] No documentation exists
- [ ] Documentation outdated
- [ ] Documentation incomplete

## Required Sections
- [ ] Overview
- [ ] Prerequisites
- [ ] Step-by-step instructions
- [ ] Examples
- [ ] Troubleshooting
- [ ] FAQ

## Location
- Repository: [Where it will live]
- Format: [ ] Markdown [ ] Wiki [ ] Confluence

---
Labels: work/internal, type/documentation
Priority: Medium
Estimate: Small
```

#### Toil Reduction Template
```markdown
## Toil Description
[Manual, repetitive task to automate]

## Current Process
1. Manual step 1 [Time: X min]
2. Manual step 2 [Time: Y min]
3. Total time per occurrence: [Sum]
4. Frequency: [Daily/Weekly/Monthly]
5. Annual hours spent: [Calculation]

## Automation Proposal
- **Solution**: [Automation approach]
- **Tools**: [Scripts/services to use]
- **Investment**: [Development hours]
- **ROI**: [Hours saved annually]

## Success Metrics
- [ ] Process fully automated
- [ ] Manual intervention < 5%
- [ ] Time reduction > 80%
- [ ] Documentation complete

## Implementation
- [ ] Write automation script
- [ ] Add monitoring
- [ ] Create runbook
- [ ] Train team
- [ ] Monitor for 2 weeks

---
Labels: work/internal, type/toil, value/automation
Priority: Based on ROI
```

### 🔄 Change Work Templates

#### Configuration Change Template
```markdown
## Change Summary
[What is being changed]

## Related To
- Parent Issue: #[Issue number]
- Original Request: [Link]

## Change Details
- **System**: [Affected system]
- **Current Value**: [Existing config]
- **New Value**: [Proposed config]
- **Reason**: [Why this change]

## Impact Analysis
- [ ] Requires restart: Yes/No
- [ ] Downtime needed: [Duration]
- [ ] Performance impact: [Expected]
- [ ] Security impact: [Assessment]

## Testing Plan
- [ ] Dev environment tested
- [ ] Staging validation
- [ ] Load test if needed
- [ ] Rollback tested

## Approval Required
- [ ] Tech lead
- [ ] Security team
- [ ] Product owner

---
Labels: work/changes, type/config
Link: Parent issue
Priority: Inherit from parent
```

### 🚨 Unplanned Work Templates

#### Incident Report Template
```markdown
## Incident Summary
**Status**: [ ] Investigating [ ] Identified [ ] Monitoring [ ] Resolved

## Impact
- **Severity**: [ ] Critical [ ] High [ ] Medium [ ] Low
- **Start Time**: [Timestamp]
- **Detection Time**: [Timestamp]
- **Recovery Time**: [Timestamp]
- **MTTR**: [Calculated]

## Affected Systems
- Primary: [Service name]
- Dependencies: [List affected]
- Customer Impact: [Description]

## Timeline
- HH:MM - [Event description]
- HH:MM - [Event description]
- HH:MM - [Event description]

## Root Cause
[5 Whys analysis or initial findings]

## Resolution
- **Immediate Fix**: [What was done]
- **Long-term Fix**: [What needs to be done]

## Follow-up Actions
- [ ] Post-mortem scheduled
- [ ] Monitoring added
- [ ] Documentation updated
- [ ] Customer communication sent

---
Labels: work/unplanned, type/incident, priority/urgent
Assignee: On-call engineer
Skip to: In Progress
```

#### Emergency Change Template
```markdown
## Emergency Change Required
**Justification**: [Why this can't wait]

## Change Description
[What needs to be changed immediately]

## Risk Assessment
- **Risk of Making Change**: [Low/Medium/High]
- **Risk of NOT Making Change**: [Low/Medium/High]
- **Blast Radius**: [What could be affected]

## Approval
- [ ] On-call approval obtained
- [ ] Manager notified
- [ ] CAB retroactive review scheduled

## Implementation
- [ ] Change implemented
- [ ] Verification complete
- [ ] Monitoring confirmed
- [ ] Team notified

---
Labels: work/unplanned, type/emergency
Priority: Urgent
Status: In Progress
```

## Template Best Practices

### 1. Keep Templates Focused
- One template per specific use case
- Don't create generic "catch-all" templates
- Review and refine based on usage

### 2. Use Smart Defaults
```yaml
Default Settings:
  Customer Bug:
    Priority: High
    SLA: 4 hours
    Auto-assign: On-call
  
  Feature Request:
    Priority: Medium
    Project: Current Quarter
    Estimate: Required
  
  Infrastructure:
    Priority: Medium
    Labels: [work/internal]
    Workflow: Tech Review Required
```

### 3. Placeholder Text
Use Linear's placeholder format for dynamic content:
```markdown
## Issue Title
{{What problem are you experiencing?}}

## Environment
{{Which environment is affected?}}

## Steps to Reproduce
{{Provide detailed steps}}
```

### 4. Conditional Sections
Structure templates to guide users:
```markdown
## For Production Issues Only
(Complete this section if production is affected)
- Customer impact: 
- Revenue impact: 
- Workaround: 

## For Development Issues Only
(Complete this section for non-production)
- Branch affected: 
- Last working commit: 
```

## Template Automation

### Auto-Assignment Rules
```javascript
// Pseudo-code for Linear automation
if (template === "Incident Report") {
  assignee = getCurrentOncall();
  priority = "Urgent";
  skipTriage = true;
}

if (template === "Documentation Task") {
  labels.add("needs-review");
  project = "Documentation Sprint";
}
```

### SLA Enforcement
```javascript
// Set due dates based on template
if (template === "Customer Bug" && priority === "High") {
  dueDate = now() + 4.hours;
  labels.add("sla-critical");
}
```

## Template Governance

### Monthly Review Process
1. **Usage Analytics**
   - Which templates are most used?
   - Which fields are typically left empty?
   - Common modifications after creation?

2. **Team Feedback**
   - Survey: Are templates helpful?
   - What's missing?
   - What's unnecessary?

3. **Refinement**
   - Update based on feedback
   - Remove unused templates
   - Add new templates for emerging patterns

### Template Ownership
```yaml
Template Owners:
  Feature Request: Product Manager
  Infrastructure: Tech Lead
  Incident Report: SRE Team
  Documentation: DevOps Lead
  
Responsibilities:
  - Quarterly review
  - Update based on process changes
  - Train team on usage
  - Monitor completion quality
```

## Quick Reference

### When to Use Which Template

| Situation | Template | Auto-Actions |
|-----------|----------|--------------|
| Customer reports issue | Customer Bug Report | Notify on-call, set SLA |
| New feature idea | Feature Request | Add to backlog, notify PM |
| System needs upgrade | Infrastructure Improvement | Tech review, estimation |
| Manual task identified | Toil Reduction | Calculate ROI, prioritize |
| Production is down | Incident Report | Page on-call, skip triage |
| Process needs docs | Documentation Task | Assign writer, set deadline |
| Config needs update | Configuration Change | Link parent, require approval |
| Emergency fix needed | Emergency Change | Bypass CAB, notify team |

## Implementation Timeline

### Week 1: Core Templates
- [ ] Create Incident Report template
- [ ] Create Feature Request template
- [ ] Create Bug Report template
- [ ] Train team on usage

### Week 2: Specialized Templates
- [ ] Create Infrastructure template
- [ ] Create Documentation template
- [ ] Create Toil Reduction template
- [ ] Set up automation rules

### Week 3: Refinement
- [ ] Gather feedback
- [ ] Adjust templates
- [ ] Add conditional logic
- [ ] Create team-specific variants

### Week 4: Optimization
- [ ] Analyze usage patterns
- [ ] Remove unused fields
- [ ] Add missing information
- [ ] Document best practices

## Next Steps

1. Review [LABELS.md](./LABELS.md) for template label configuration
2. Configure [AUTOMATION.md](./AUTOMATION.md) for template-based rules
3. Set up [WORKFLOWS.md](./WORKFLOWS.md) for template routing
