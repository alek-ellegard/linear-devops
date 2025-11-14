# Daily Operations Guide for Linear

## Overview
Consistent daily practices create rhythm and predictability. This guide outlines daily, weekly, and monthly operational cadences for DevOps teams using Linear.

## Daily Practices

### Morning Routine (9:00 - 10:00 AM)

#### 1. Check Operational Health (9:00 - 9:15)
```yaml
Review Dashboards:
  - System status dashboard
  - Error budget remaining
  - Overnight incidents
  - Failed deployments

Linear Views:
  - "Incidents - Last 24h"
  - "Critical Priority"
  - "Blocked Items"

Actions:
  - Acknowledge any new incidents
  - Check on-call handoff notes
  - Review automation failures
```

#### 2. Triage New Work (9:15 - 9:30)
```yaml
Linear Triage View:
  Filter: State = Triage
  Sort: Created DESC
  
For Each Item:
  1. Read and understand
  2. Apply work type label
  3. Set initial priority
  4. Move to appropriate state:
     - Urgent → In Progress
     - Clear → Backlog
     - Unclear → Needs Info
     - Invalid → Close
```

#### 3. Team Standup (9:30 - 10:00)
```yaml
Format: Walking the Board
Tools: Linear Board View + Screen Share

Process:
  1. Start from right (Done/Blocked)
  2. Move left (Review → In Progress → Todo)
  3. Each person updates on their items
  4. Flag blockers immediately
  5. Confirm today's priorities

Linear Filters:
  - "My Work - In Progress"
  - "Team - Current Sprint"
  - "Blocked - All"
```

### Afternoon Check-in (4:00 - 4:30 PM)

#### End of Day Review
```yaml
Personal Tasks:
  - Update issue statuses
  - Comment on progress
  - Flag any blockers
  - Prepare tomorrow's plan

Team Tasks:
  - Review PR queue
  - Check deployment status
  - Update sprint burndown
  - Handoff to next timezone

Linear Actions:
  - Move completed items to Done
  - Update time estimates
  - Create follow-up issues
  - Schedule tomorrow's work
```

## Weekly Cadences

### Monday - Sprint Planning

#### Morning: Sprint Kick-off
```yaml
Time: 10:00 - 12:00
Participants: Entire team

Preparation:
  - Product owner prioritizes backlog
  - Tech lead reviews technical items
  - Previous sprint metrics ready

Agenda:
  1. Sprint Retrospective (15 min)
  2. Sprint Goals (15 min) 
  3. Capacity Planning (15 min)
  4. Story Selection (60 min)
  5. Risk Assessment (15 min)

Linear Setup:
  - Create new cycle
  - Move committed items to Todo
  - Assign owners
  - Set sprint goals
```

#### Afternoon: Technical Planning
```yaml
Time: 2:00 - 3:00
Participants: Engineering team

Activities:
  - Break down large stories
  - Identify dependencies
  - Plan pair programming
  - Schedule code reviews

Linear Actions:
  - Create sub-issues
  - Link dependencies
  - Add technical notes
  - Set up automation rules
```

### Tuesday - Deep Work

#### Focus Time
```yaml
Morning Block: 9:00 - 12:00
  - No meetings
  - Slack to "Do Not Disturb"
  - Work on highest priority items

Afternoon Block: 1:00 - 4:00
  - Continue morning work
  - Or pair programming sessions
  - Code reviews

Linear Focus:
  - Work only from "My Todo" view
  - Update progress every 2 hours
  - Move items through workflow
```

### Wednesday - Collaboration

#### Cross-Team Sync
```yaml
Time: 10:00 - 11:00
Participants: Team leads

Topics:
  - Dependencies
  - Shared resources
  - Upcoming changes
  - Incident patterns

Linear Review:
  - Cross-team projects
  - Shared components
  - Dependency tracking
```

#### Documentation Time
```yaml
Time: 2:00 - 4:00
Focus: Documentation debt

Activities:
  - Update runbooks
  - Write post-mortems
  - Document new features
  - Review old docs

Linear Filter:
  - type/documentation
  - Labels: needs-docs
```

### Thursday - Quality & Improvement

#### Code Review Day
```yaml
Morning: 9:00 - 12:00
  - Review all pending PRs
  - Provide feedback
  - Pair on complex reviews

Linear Integration:
  - PRs link to issues
  - Update issue status
  - Comment on progress
```

#### Tech Debt Time
```yaml
Afternoon: 2:00 - 4:00
Activities:
  - Refactoring
  - Upgrade dependencies
  - Fix deprecations
  - Improve tests

Linear Focus:
  - type/tech-debt
  - work/internal
  - Priority: Medium/Low
```

### Friday - Wrap Up & Learning

#### Sprint Review
```yaml
Time: 10:00 - 11:00
Participants: Team + Stakeholders

Agenda:
  - Demo completed work
  - Review metrics
  - Gather feedback
  - Celebrate wins

Linear Reports:
  - Completed this cycle
  - Velocity chart
  - Cycle time analysis
```

#### Learning Time
```yaml
Time: 2:00 - 4:00
Options:
  - Team tech talk
  - Online course
  - Experiment with new tool
  - Hackathon project

Linear Task:
  - Create learning issues
  - Track experiments
  - Document findings
```

## Monthly Practices

### First Monday - Strategic Review

#### Quarterly Planning Check
```yaml
Time: Full morning
Participants: Leadership + Tech leads

Review:
  - OKR progress
  - Roadmap alignment
  - Resource allocation
  - Budget status

Linear Analysis:
  - Projects completed
  - Work type distribution
  - Velocity trends
  - Bottleneck patterns
```

### Second Tuesday - Operational Excellence

#### Post-Mortem Review
```yaml
Time: 2:00 - 4:00
Participants: Engineering team

Review:
  - All incidents from past month
  - Pattern analysis
  - Action items progress
  - Process improvements

Linear Tracking:
  - type/incident analysis
  - Post-mortem action items
  - Preventive measures
```

### Third Wednesday - Tool & Process

#### Tooling Review
```yaml
Evaluate:
  - Linear usage patterns
  - Integration effectiveness
  - Automation success rate
  - Missing capabilities

Actions:
  - Update templates
  - Refine labels
  - Adjust workflows
  - Fix automations
```

### Last Friday - Team Health

#### Team Retrospective
```yaml
Time: 2:00 - 4:00
Format: Full team discussion

Topics:
  - What went well
  - What needs improvement
  - Team happiness
  - Process friction

Linear Updates:
  - Adjust team settings
  - Update workflows
  - Refine processes
```

## On-Call Operations

### Handoff Process

#### Daily On-Call Handoff
```yaml
Time: 9:00 AM
Duration: 15 minutes

Outgoing Engineer:
  - Review incidents handled
  - Update runbooks if needed
  - Note any ongoing issues
  - Brief incoming engineer

Linear Handoff:
  - Reassign active incidents
  - Update on-call field
  - Review priority items
  - Check escalation status
```

### Incident Response

#### Incident Workflow
```yaml
1. Alert Received:
   - Acknowledge immediately
   - Create Linear incident
   - Apply labels: work/unplanned, type/incident
   - Set priority based on impact

2. Initial Response:
   - Join incident channel
   - Start investigation
   - Update Linear issue every 30 min
   - Escalate if needed

3. Resolution:
   - Fix or mitigate issue
   - Update status to Resolved
   - Note resolution time
   - Schedule post-mortem

4. Follow-up:
   - Create post-mortem issue
   - Link related issues
   - Track action items
   - Update documentation
```

## Slack Integration Practices

### Channel Structure
```yaml
Channels:
  #standup - Daily updates
  #incidents - Active incidents
  #deployments - Deployment status
  #linear-feed - All Linear updates
  #team-social - Non-work chat

Linear Notifications:
  #incidents: Priority = Critical/High
  #standup: Daily summary
  #deployments: State = Released
```

### Daily Slack Routine
```yaml
Morning:
  - Post standup summary
  - Share priority items
  - Note any blockers

Afternoon:
  - Update progress
  - Call for reviews
  - EOD summary

Format:
  "📅 Today's Focus: [Linear link]
   ✅ Completed: X items
   🚧 In Progress: Y items
   🚫 Blocked: Z items"
```

## GitHub Integration Practices

### Branch Management
```yaml
Naming Convention:
  Pattern: {team}-{issue-number}-{brief-description}
  Example: eng-123-fix-auth-bug

Automation:
  - Branch created → In Progress
  - PR opened → In Review
  - PR merged → Done
  - Deploy success → Released
```

### Code Review Process
```yaml
Daily Review Time:
  - Check PR queue twice daily
  - Prioritize by issue priority
  - Review within 4 hours for High

Linear Integration:
  - Link PR to issue
  - Update issue comments
  - Track review time
  - Auto-close on merge
```

## Reporting Rhythms

### Daily Reports
```yaml
What: Standup summary
When: 10:00 AM
Where: #standup channel
Content:
  - Yesterday's completions
  - Today's priorities
  - Blockers
  - Sprint burndown
```

### Weekly Reports
```yaml
What: Sprint progress
When: Friday 4:00 PM
To: Stakeholders
Content:
  - Velocity
  - Completed features
  - Upcoming work
  - Risks/blockers
```

### Monthly Reports
```yaml
What: Executive summary
When: First Monday
To: Leadership
Content:
  - DORA metrics
  - Work distribution
  - Incident analysis
  - Team health
  - Next month focus
```

## Quick Reference Checklist

### Daily Must-Do's
- [ ] Check operational health (9:00)
- [ ] Triage new issues (9:15)
- [ ] Attend standup (9:30)
- [ ] Update issue statuses (ongoing)
- [ ] Review PRs (2x daily)
- [ ] End of day update (4:00)

### Weekly Must-Do's
- [ ] Monday: Sprint planning
- [ ] Tuesday: Deep work blocks
- [ ] Wednesday: Documentation
- [ ] Thursday: Code reviews & tech debt
- [ ] Friday: Sprint review & learning

### Monthly Must-Do's
- [ ] Week 1: Strategic review
- [ ] Week 2: Post-mortem analysis
- [ ] Week 3: Tool optimization
- [ ] Week 4: Team retrospective

## Emergency Procedures

### Production Down
1. Create Critical incident in Linear
2. Page on-call if needed
3. Join incident bridge
4. Update status every 30 min
5. Focus on mitigation first
6. Root cause second

### Data Loss Risk
1. Stop all changes immediately
2. Escalate to leadership
3. Document everything
4. Coordinate recovery
5. Customer communication
6. Post-mortem required

### Security Incident
1. Isolate affected systems
2. Notify security team
3. Create Private issue in Linear
4. Follow security runbook
5. Legal/compliance notification
6. Detailed post-mortem

## Tips for Success

1. **Consistency is Key**: Same time, same process, every day
2. **Automate Routine**: Let Linear handle status updates
3. **Communicate Early**: Flag issues before they're critical
4. **Document as You Go**: Don't leave it for later
5. **Protect Focus Time**: Deep work needs protection
6. **Review and Adjust**: Process should evolve

## Next Steps

1. Set up [AUTOMATION.md](./AUTOMATION.md) for daily automations
2. Configure [METRICS.md](./METRICS.md) dashboards
3. Create calendar blocks for routines
4. Set up Slack reminders
5. Train team on processes
