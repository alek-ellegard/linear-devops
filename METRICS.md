# DevOps Metrics in Linear

## Overview
Measuring the right things drives improvement. This guide outlines key metrics for DevOps teams based on DORA metrics, SRE principles, and Phoenix Project insights.

## Core Metrics Framework

### DORA Metrics (DevOps Performance)

#### 1. Deployment Frequency
**Definition**: How often code is deployed to production
**Target**: Multiple times per day
**Linear Tracking**:
```yaml
Filter: 
  - State: Released
  - Time: Last 7 days
Calculation: Count / Days
Visual: Line chart over time
```

#### 2. Lead Time for Changes
**Definition**: Time from commit to production
**Target**: < 1 day
**Linear Tracking**:
```yaml
Measure: 
  - Start: First commit linked
  - End: State = Released
Filter: Type = feature OR bug
Visual: Histogram distribution
```

#### 3. Change Failure Rate (CFR)
**Definition**: Percentage of deployments causing incidents
**Target**: < 15%
**Linear Tracking**:
```yaml
Formula: 
  Incidents / Deployments * 100
Filter:
  - Incidents: work/unplanned + env/production
  - Deployments: State = Released
Period: Last 30 days
```

#### 4. Mean Time to Recovery (MTTR)
**Definition**: Time to restore service after incident
**Target**: < 1 hour
**Linear Tracking**:
```yaml
Measure:
  - Start: Incident created
  - End: Incident resolved
Filter: 
  - type/incident
  - priority/critical OR high
Visual: Average with trend line
```

## Phoenix Project Metrics

### Work Type Distribution

```yaml
Metric: Work Balance
Target Distribution:
  - Business Projects: 40%
  - Internal Projects: 30%
  - Changes: 20%
  - Unplanned Work: 10%

Linear Query:
  GROUP BY work/* labels
  COUNT by type
  Period: Current cycle
  
Alert When:
  - Unplanned > 25% (Red)
  - Internal < 20% (Yellow)
  - Business < 30% (Yellow)
```

### Flow Metrics

#### Cycle Time
```yaml
Definition: Time from Todo to Done
Target: < 3 days
Calculation:
  - P50: 2 days
  - P90: 5 days
  - P99: 10 days
  
Linear Filter:
  - Completed this cycle
  - Exclude: work/unplanned
```

#### Flow Efficiency
```yaml
Definition: Active time / Total time
Target: > 40%
Calculation:
  Active = In Progress time
  Waiting = Blocked + Review time
  Efficiency = Active / (Active + Waiting)
```

#### WIP Limit Adherence
```yaml
Definition: Percentage of time within WIP limits
Target: > 80%
Daily Check:
  - In Progress items per person
  - Total In Review items
  - Flag violations
```

## SRE Metrics

### Toil Metrics

#### Toil Percentage
```yaml
Definition: Time spent on manual, repetitive work
Target: < 50%
Measurement:
  - Count: type/toil issues
  - Time: Sum of estimates
  - Percentage: Toil time / Total time
  
Quarterly Goal: Reduce by 20%
```

#### Automation ROI
```yaml
Definition: Hours saved through automation
Calculation:
  - Manual time before
  - Automated time after
  - ROI = Hours saved annually / Development hours
  
Track:
  - Automation projects completed
  - Time saved per automation
  - Cumulative annual savings
```

### Reliability Metrics

#### Service Level Indicators (SLIs)
```yaml
Uptime SLI:
  - Target: 99.9%
  - Measure: Monitoring data
  - Track: Incidents affecting uptime

Performance SLI:
  - Target: P95 latency < 200ms
  - Measure: APM data
  - Track: Performance incidents
```

#### Error Budget
```yaml
Definition: Allowed downtime/errors
Monthly Budget: 43.2 minutes (99.9% SLA)
Tracking:
  - Consumed: Sum of incident durations
  - Remaining: Budget - Consumed
  - Alert: When 50% consumed
```

## Team Health Metrics

### Developer Experience

#### PR Review Time
```yaml
Metric: Time from PR open to first review
Target: < 4 hours
Track:
  - P50: 2 hours
  - P90: 8 hours
Alert: PRs waiting > 24 hours
```

#### Context Switching
```yaml
Metric: Number of issues per person per day
Target: < 3
Measure:
  - Issues touched per day
  - State changes per person
Ideal: 1-2 focused items
```

#### On-Call Load
```yaml
Metric: Incidents per on-call shift
Target: < 2 per week
Track:
  - Incidents by day of week
  - Incidents by time of day
  - Pages per engineer per month
```

### Velocity and Predictability

#### Sprint Velocity
```yaml
Metric: Story points completed per sprint
Track:
  - 3-sprint rolling average
  - Velocity trend
  - Capacity vs actual
```

#### Sprint Predictability
```yaml
Metric: Planned vs completed work
Target: > 80% of committed work completed
Calculate:
  - Items committed at planning
  - Items completed at review
  - Percentage achieved
```

## Custom Linear Dashboards

### Engineering Manager Dashboard

```javascript
// Weekly Executive Summary
const executiveDashboard = {
  sections: [
    {
      title: "Delivery Metrics",
      metrics: [
        "Features Released: X",
        "Bugs Fixed: Y",
        "Lead Time: Z days",
        "Velocity Trend: ↑/↓"
      ]
    },
    {
      title: "Quality Metrics",
      metrics: [
        "Change Failure Rate: X%",
        "MTTR: Y hours",
        "Open Bugs: Z",
        "Test Coverage: W%"
      ]
    },
    {
      title: "Team Health",
      metrics: [
        "Unplanned Work: X%",
        "On-Call Incidents: Y",
        "PR Review Time: Z hours",
        "Team Satisfaction: W/10"
      ]
    }
  ]
};
```

### Team Standup Dashboard

```yaml
Daily View:
  - In Progress by Person
  - Blocked Items (age)
  - PRs Awaiting Review
  - Yesterday's Completions
  - Today's Priorities
  - Cycle Burndown
```

### SRE Dashboard

```yaml
Reliability View:
  - Current Incidents
  - Error Budget Status
  - SLI Compliance
  - Recent Post-Mortems
  - Toil Percentage
  - Automation Pipeline
```

## Measurement Implementation

### Week 1: Basic Metrics
```yaml
Setup:
  - [ ] Configure cycle time tracking
  - [ ] Set up work type labels
  - [ ] Create velocity view
  - [ ] Enable GitHub metrics

Daily Track:
  - Issues created/completed
  - WIP limits
  - Blocked items
```

### Week 2: Flow Metrics
```yaml
Setup:
  - [ ] Implement flow efficiency calculation
  - [ ] Track state transitions
  - [ ] Set up bottleneck detection
  - [ ] Create cumulative flow diagram

Weekly Review:
  - Cycle time trends
  - Bottleneck analysis
  - WIP adherence
```

### Week 3: Quality Metrics
```yaml
Setup:
  - [ ] Track incidents
  - [ ] Measure MTTR
  - [ ] Calculate CFR
  - [ ] Monitor error budget

Incident Tracking:
  - Root cause categories
  - Time to detect
  - Time to resolve
  - Customer impact
```

### Week 4: Advanced Analytics
```yaml
Setup:
  - [ ] Create executive dashboard
  - [ ] Implement predictive metrics
  - [ ] Set up alerts
  - [ ] Automate reporting

Monthly Review:
  - Trend analysis
  - Goal progress
  - Team health survey
  - Improvement actions
```

## Metric Anti-Patterns

### ❌ Vanity Metrics
**Wrong**: Lines of code, number of commits
**Right**: Customer value delivered, reliability

### ❌ Individual Performance
**Wrong**: Issues per person, individual velocity
**Right**: Team velocity, collective ownership

### ❌ Output Over Outcome
**Wrong**: Features shipped
**Right**: Customer problems solved

### ❌ Gaming Metrics
**Wrong**: Closing issues to boost numbers
**Right**: Focus on flow and value

## Alerting Strategy

### Real-Time Alerts

```yaml
Critical Alerts (Page immediately):
  - Production incident created
  - Error budget < 20%
  - Deployment failure
  - WIP limit exceeded by 50%

Warning Alerts (Notify channel):
  - PR waiting > 24 hours
  - Issue blocked > 48 hours
  - Sprint at risk
  - Toil percentage > 60%

Info Alerts (Dashboard only):
  - Daily summary
  - Weekly trends
  - Sprint velocity
  - Team achievements
```

## Reporting Cadence

### Daily
- Standup metrics
- WIP status
- Blocked items
- Incident status

### Weekly
- Sprint progress
- Velocity tracking
- Work type distribution
- PR metrics

### Monthly
- DORA metrics
- Error budget review
- Toil analysis
- Team health survey

### Quarterly
- OKR progress
- Capacity planning
- Tool evaluation
- Process improvements

## Quick Reference Formulas

```javascript
// Cycle Time
cycleTime = dateCompleted - dateStarted;

// Lead Time  
leadTime = dateReleased - dateCreated;

// Flow Efficiency
flowEfficiency = activeTime / (activeTime + waitTime) * 100;

// Change Failure Rate
cfr = (incidents / deployments) * 100;

// MTTR
mttr = sum(resolutionTimes) / count(incidents);

// Toil Percentage
toilPercentage = (toilHours / totalHours) * 100;

// Sprint Predictability
predictability = (completedItems / committedItems) * 100;

// WIP Adherence
wipAdherence = (daysUnderLimit / totalDays) * 100;
```

## Tool Integration

### Linear + Monitoring Tools

```yaml
Datadog Integration:
  - Link incidents to Linear
  - Auto-create issues from alerts
  - Track MTTR automatically
  - Update incident status

Grafana Dashboards:
  - Embed Linear metrics
  - Correlate deploys with metrics
  - Show error budget
  - Display team velocity

PagerDuty Connection:
  - Create Linear incident on page
  - Track on-call metrics
  - Link post-mortems
  - Measure response times
```

## Best Practices

1. **Start Simple**: Track basics before advanced metrics
2. **Automate Collection**: Manual tracking won't last
3. **Make Visible**: Dashboards in team areas
4. **Review Regularly**: Weekly team, monthly management
5. **Act on Data**: Metrics without action are waste
6. **Avoid Blame**: Focus on system, not people
7. **Iterate**: Refine metrics based on value

## Next Steps

1. Implement [AUTOMATION.md](./AUTOMATION.md) for metric collection
2. Review [DAILY_OPERATIONS.md](./DAILY_OPERATIONS.md) for review cadence
3. Create custom dashboards in Linear
4. Set up alerting rules
5. Schedule regular metric reviews
