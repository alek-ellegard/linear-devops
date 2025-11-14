# Linear Setup Guide for DevOps Teams

## Overview
This guide covers the initial configuration of Linear for a 5-10 person DevOps team, implementing principles from The Phoenix Project and SRE best practices.

## Prerequisites
- Linear workspace created
- Team members invited
- GitHub integration configured
- Slack integration configured

## Phase 1: Foundation Setup (Week 1)

### 1. Team Configuration

Create your team structure:
```
Teams:
├── Engineering (primary team)
├── Infrastructure (optional, for larger teams)
└── Operations (optional, for larger teams)
```

For teams under 10 people, a single "Engineering" team is recommended to avoid silos.

### 2. Cycle Configuration

**Recommended Settings:**
- **Duration**: 2 weeks
- **Start Day**: Monday
- **Auto-rollover**: Enabled
- **Cooldown**: 1 day between cycles

**Capacity Planning:**
- 60% allocated to planned work
- 20% reserved for unplanned/incident work
- 20% for technical debt and improvements

### 3. Workflow States

Configure your workflow with these states:

```
Triage → Backlog → Todo → In Progress → In Review → Done → Released
```

**State Purposes:**
- **Triage**: New, unprocessed work
- **Backlog**: Accepted but not scheduled
- **Todo**: Scheduled for current cycle
- **In Progress**: Actively being worked on
- **In Review**: Code review or validation
- **Done**: Work complete, not yet deployed
- **Released**: Deployed to production

### 4. Enable Key Features

In Settings → General:
- ✅ Enable Triage
- ✅ Enable Cycles
- ✅ Enable Projects
- ✅ Enable Estimates (use points or t-shirt sizes)
- ✅ Enable Priority levels
- ✅ Enable Due dates

### 5. Archive Rules

Configure auto-archive to reduce clutter:
- Archive "Done" issues after 14 days
- Archive "Cancelled" issues after 7 days
- Never archive issues with "documentation" label

## Phase 2: Integration Setup

### GitHub Integration

1. Connect GitHub organization
2. Configure branch naming:
   ```
   Pattern: {team-key}-{issue-number}-{issue-title}
   Example: ENG-123-fix-auth-bug
   ```
3. Enable automatic status updates:
   - Branch created → In Progress
   - PR opened → In Review
   - PR merged → Done

### Slack Integration

1. Connect Slack workspace
2. Create dedicated channels:
   - `#linear-notifications` - All updates
   - `#linear-incidents` - High priority issues
   - `#linear-standup` - Daily summaries

3. Configure notifications:
   - New incidents → `#linear-incidents`
   - Cycle summaries → `#linear-standup`
   - Personal mentions → Direct messages

## Phase 3: Access and Permissions

### Role Configuration

**Admin Access:**
- Team leads
- DevOps managers
- Can modify workflows, labels, and templates

**Member Access:**
- All team members
- Can create/edit issues
- Can manage own work

**Guest Access:**
- Stakeholders
- Read-only access to specific projects

### API Setup

Generate API keys for:
- CI/CD integration
- Monitoring tools
- Custom automations

Store keys securely in your secrets manager.

## Phase 4: Initial Data Migration

### Import Existing Work

1. Export current tickets from existing system (Jira, GitHub Issues, etc.)
2. Map fields to Linear structure:
   ```
   Old System → Linear
   Epic → Project
   Story → Issue
   Task → Sub-issue
   Bug → Issue with "bug" label
   ```

3. Use Linear's import tool or API for bulk creation

### Historical Data

Consider importing:
- Last 3 months of closed issues (for velocity tracking)
- All open issues
- Active projects only

## Quick Start Checklist

### Week 1
- [ ] Create workspace and invite team
- [ ] Configure team settings and cycles
- [ ] Set up workflow states
- [ ] Create initial labels (see LABELS.md)
- [ ] Configure GitHub integration

### Week 2  
- [ ] Create issue templates (see TEMPLATES.md)
- [ ] Set up Slack notifications
- [ ] Import existing work items
- [ ] Configure automation rules
- [ ] Train team on keyboard shortcuts

### Week 3
- [ ] Run first sprint planning in Linear
- [ ] Establish daily standup process
- [ ] Create custom views for team
- [ ] Set up initial dashboards
- [ ] Gather team feedback

## Common Pitfalls to Avoid

1. **Over-configuration**: Start simple, add complexity as needed
2. **Too many teams**: Creates silos, defeats DevOps principles
3. **Ignoring keyboard shortcuts**: Linear is keyboard-first by design
4. **Not using Triage**: Critical for managing incoming work
5. **Skipping integrations**: Automation reduces toil significantly

## Success Indicators

After setup, you should have:
- ✅ All work visible in one place
- ✅ Automatic status updates from GitHub
- ✅ Clear workflow from idea to production
- ✅ Slack notifications for critical events
- ✅ Team adopting keyboard-driven workflow

## Next Steps

1. Review [WORK_TYPES.md](./WORK_TYPES.md) - Understanding the Four Types of Work
2. Configure [TEMPLATES.md](./TEMPLATES.md) - Setting up issue templates
3. Implement [LABELS.md](./LABELS.md) - Label taxonomy system
4. Set up [AUTOMATION.md](./AUTOMATION.md) - Automation rules

## Resources

- [Linear Keyboard Shortcuts](https://linear.app/docs/keyboard-shortcuts)
- [Linear API Documentation](https://developers.linear.app)
- [The Phoenix Project](https://itrevolution.com/the-phoenix-project/)
- [Google SRE Book](https://sre.google/sre-book/)
