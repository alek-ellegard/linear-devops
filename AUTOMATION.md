# Linear Automation Guide for DevOps Teams

## Overview
Automation reduces toil and ensures consistency. This guide covers Linear's automation capabilities, integration patterns, and custom automation scripts.

## Linear Native Automation

### Auto-Labeling Rules

#### Title-Based Triggers
```javascript
// Linear Automation Rules (Settings → Automation)

Rule: "Auto-label Incidents"
If: Title contains ["down", "outage", "incident", "emergency"]
Then: 
  - Add labels: work/unplanned, type/incident, priority/critical
  - Move to: In Progress
  - Assign to: On-call engineer
  - Notify: #incidents channel

Rule: "Auto-label Documentation"
If: Title contains ["docs", "documentation", "readme"]
Then:
  - Add labels: work/internal, type/documentation
  - Set estimate: Small
  - Add to project: Documentation Backlog

Rule: "Auto-label Toil"
If: Title contains ["automate", "manual", "repetitive", "[TOIL]"]
Then:
  - Add labels: work/internal, type/toil, value/automation
  - Require: ROI calculation in description
```

#### Description Patterns
```javascript
Rule: "Customer Reported"
If: Description contains ["customer reported", "user reported", "client found"]
Then:
  - Add label: source/customer
  - Set priority: High
  - Set SLA: 4 hours
  - Notify: Product Manager

Rule: "Security Issue"
If: Description contains ["security", "vulnerability", "CVE", "exploit"]
Then:
  - Add label: type/security
  - Set priority: Critical
  - Mark as: Private
  - Notify: Security team
```

### State-Based Automation

#### Workflow Transitions
```javascript
Rule: "Auto-close Done Issues"
If: 
  - State = Done
  - Age > 14 days
  - No recent activity
Then:
  - Move to: Closed
  - Archive issue

Rule: "Escalate Blocked Items"
If:
  - State = Blocked OR Label = status/blocked
  - Duration > 48 hours
Then:
  - Add label: needs-escalation
  - Notify: Team lead
  - Add comment: "Blocked for 48+ hours, needs attention"

Rule: "Stale In Progress"
If:
  - State = In Progress
  - No activity > 3 days
Then:
  - Add label: status/stale
  - Comment: "@assignee Is this still being worked on?"
  - Notify: Assignee
```

### SLA Enforcement

```javascript
Rule: "Critical Issue SLA"
If: 
  - Priority = Critical
  - Created
Then:
  - Set due date: Now + 4 hours
  - Add label: sla/critical
  - Start timer

Rule: "SLA Warning"
If:
  - Has label: sla/critical
  - Due date < 1 hour
  - State != Done
Then:
  - Escalate to: Manager
  - Add label: sla/at-risk
  - Send alert: Slack + Email

Rule: "SLA Breach"
If:
  - Due date passed
  - State != Done
  - Priority = Critical
Then:
  - Add label: sla/breached
  - Notify: Leadership
  - Create: Post-mortem issue
```

## GitHub Integration Automation

### Branch and PR Automation

```yaml
# .github/linear.yml
automation:
  branch:
    pattern: "{team}-{number}-{title}"
    onCreate:
      - moveToState: "In Progress"
      - assignToAuthor: true
      - addComment: "Development started"
  
  pullRequest:
    onOpen:
      - moveToState: "In Review"
      - notifyReviewers: true
      - checkCriteria:
          - tests: passing
          - coverage: ">80%"
    
    onMerge:
      - moveToState: "Done"
      - addComment: "Merged PR #{pr_number}"
      - triggerDeployment: staging
    
    onClose:
      - addLabel: "pr-closed"
      - askReason: true
```

### Deployment Automation

```yaml
# .github/workflows/deploy.yml
name: Deploy and Update Linear

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to Production
        run: ./deploy.sh
      
      - name: Update Linear Issue
        uses: linear-app/action@v1
        with:
          api-key: ${{ secrets.LINEAR_API_KEY }}
          action: update-state
          state: "Released"
          comment: "Deployed to production in ${{ github.run_id }}"
```

## Slack Integration Automation

### Notification Rules

```javascript
// Slack App Configuration

Channel: "#incidents"
Triggers:
  - New issue with priority = Critical
  - New issue with type/incident label
  - State change to Blocked
Format: 
  "🚨 {priority} Issue: {title}
   Assignee: {assignee}
   Link: {linear_url}"

Channel: "#standup"
Triggers:
  - Daily at 9:30 AM
  - Summary of current sprint
Format:
  "📊 Sprint Progress:
   - Todo: {count}
   - In Progress: {count}
   - Blocked: {count}
   - Done: {count}"

Channel: "#releases"
Triggers:
  - State changed to Released
Format:
  "🚀 Released: {title}
   Type: {labels}
   Link: {linear_url}"
```

### Interactive Slack Commands

```javascript
// Slack Slash Commands

/linear create [title]
  Creates issue in Linear from Slack
  Auto-adds label: source/slack
  Returns: Linear issue link

/linear triage
  Shows all items in Triage state
  Allows: Quick labeling and routing
  Updates: Linear in real-time

/linear oncall
  Shows: Current on-call engineer
  Lists: Active incidents
  Allows: Create new incident
```

## Custom Automation Scripts

### Linear API Automation

#### Auto-Assignment Based on Component
```python
import requests
from datetime import datetime

LINEAR_API_KEY = "your_api_key"
LINEAR_API_URL = "https://api.linear.app/graphql"

def auto_assign_by_component(issue_id, component_label):
    """Auto-assign issues based on component expertise"""
    
    component_owners = {
        "component/frontend": "user_id_1",
        "component/backend": "user_id_2",
        "component/database": "user_id_3",
        "component/infrastructure": "user_id_4"
    }
    
    if component_label in component_owners:
        assignee_id = component_owners[component_label]
        
        mutation = """
        mutation($issueId: String!, $assigneeId: String!) {
          issueUpdate(
            id: $issueId,
            input: { assigneeId: $assigneeId }
          ) {
            success
            issue { id, assignee { name } }
          }
        }
        """
        
        response = requests.post(
            LINEAR_API_URL,
            json={
                "query": mutation,
                "variables": {
                    "issueId": issue_id,
                    "assigneeId": assignee_id
                }
            },
            headers={"Authorization": LINEAR_API_KEY}
        )
        
        return response.json()

# Webhook handler
def handle_webhook(payload):
    if payload["action"] == "create":
        issue = payload["data"]
        for label in issue["labels"]:
            if label.startswith("component/"):
                auto_assign_by_component(issue["id"], label)
```

#### Toil Tracker and ROI Calculator
```python
def calculate_toil_roi(issue_data):
    """Calculate ROI for toil automation"""
    
    manual_time_hours = issue_data.get("manual_time", 0)
    frequency_per_year = issue_data.get("frequency", 0)
    development_hours = issue_data.get("dev_hours", 0)
    
    annual_hours_saved = manual_time_hours * frequency_per_year
    roi_percentage = (annual_hours_saved / development_hours) * 100
    
    # Update Linear issue with ROI
    mutation = """
    mutation($issueId: String!, $roi: String!) {
      issueUpdate(
        id: $issueId,
        input: { 
          customFields: [{
            customFieldId: "roi_field_id",
            value: $roi
          }]
        }
      ) {
        success
      }
    }
    """
    
    roi_string = f"ROI: {roi_percentage:.0f}% ({annual_hours_saved}h/year)"
    
    # Add label based on ROI
    if roi_percentage > 500:
        add_label(issue_data["id"], "roi/excellent")
    elif roi_percentage > 200:
        add_label(issue_data["id"], "roi/good")
    else:
        add_label(issue_data["id"], "roi/low")
    
    return roi_string
```

### CI/CD Pipeline Integration

#### Jenkins Integration
```groovy
// Jenkinsfile
pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Update Linear issue
                    updateLinearIssue(
                        issueId: env.LINEAR_ISSUE_ID,
                        state: 'In Progress',
                        comment: "Build started: ${env.BUILD_URL}"
                    )
                }
                sh 'make build'
            }
        }
        
        stage('Test') {
            steps {
                sh 'make test'
            }
            post {
                failure {
                    updateLinearIssue(
                        issueId: env.LINEAR_ISSUE_ID,
                        addLabel: 'tests-failing',
                        comment: "Tests failed: ${env.BUILD_URL}"
                    )
                }
            }
        }
        
        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                sh 'make deploy'
                updateLinearIssue(
                    issueId: env.LINEAR_ISSUE_ID,
                    state: 'Released',
                    comment: "Deployed to production"
                )
            }
        }
    }
}

def updateLinearIssue(Map args) {
    sh """
        curl -X POST https://api.linear.app/graphql \
        -H "Authorization: ${LINEAR_API_KEY}" \
        -H "Content-Type: application/json" \
        -d '${linearMutation(args)}'
    """
}
```

## Monitoring Integration

### PagerDuty to Linear
```python
def create_incident_from_page(pagerduty_incident):
    """Create Linear incident from PagerDuty"""
    
    mutation = """
    mutation($title: String!, $description: String!, $priority: Int!) {
      issueCreate(
        input: {
          title: $title,
          description: $description,
          priority: $priority,
          labelIds: ["work_unplanned_id", "type_incident_id"],
          stateId: "in_progress_id",
          teamId: "team_id"
        }
      ) {
        success
        issue { id, url }
      }
    }
    """
    
    variables = {
        "title": f"[INCIDENT] {pagerduty_incident['summary']}",
        "description": f"""
        **PagerDuty Incident**: {pagerduty_incident['html_url']}
        **Service**: {pagerduty_incident['service']['name']}
        **Urgency**: {pagerduty_incident['urgency']}
        **Created**: {pagerduty_incident['created_at']}
        
        **Alert Details**:
        {pagerduty_incident['body']['details']}
        """,
        "priority": 0 if pagerduty_incident['urgency'] == 'high' else 1
    }
    
    response = linear_api_call(mutation, variables)
    
    # Post to Slack
    if response['data']['issueCreate']['success']:
        issue_url = response['data']['issueCreate']['issue']['url']
        post_to_slack(
            channel="#incidents",
            message=f"New incident created: {issue_url}"
        )
    
    return response
```

### Datadog Metrics to Linear
```python
def track_sli_breach(metric_data):
    """Create issue when SLI is breached"""
    
    if metric_data['value'] < SLI_THRESHOLD:
        create_linear_issue(
            title=f"SLI Breach: {metric_data['metric_name']}",
            description=f"""
            Current value: {metric_data['value']}
            Threshold: {SLI_THRESHOLD}
            Duration: {metric_data['duration']}
            
            Dashboard: {metric_data['dashboard_url']}
            """,
            labels=["sli-breach", "type/incident"],
            priority="high"
        )
```

## Webhook Automation

### Linear Webhook Handler
```javascript
// Express.js webhook handler
const express = require('express');
const app = express();

app.post('/webhooks/linear', async (req, res) => {
    const { action, data, type } = req.body;
    
    switch(type) {
        case 'Issue':
            await handleIssueWebhook(action, data);
            break;
        case 'Comment':
            await handleCommentWebhook(action, data);
            break;
        case 'Project':
            await handleProjectWebhook(action, data);
            break;
    }
    
    res.status(200).send('OK');
});

async function handleIssueWebhook(action, issue) {
    if (action === 'create') {
        // Auto-enrich issue
        await enrichIssue(issue);
        
        // Check for patterns
        await checkForDuplicates(issue);
        await suggestRelatedIssues(issue);
    }
    
    if (action === 'update') {
        // Track state transitions
        await trackStateTransition(issue);
        
        // Update external systems
        await syncToJira(issue);
        await updateConfluence(issue);
    }
}
```

## Advanced Automation Patterns

### Smart Prioritization
```javascript
function calculatePriority(issue) {
    let score = 0;
    
    // Customer impact
    if (issue.labels.includes('source/customer')) score += 30;
    if (issue.description.includes('data loss')) score += 50;
    if (issue.description.includes('security')) score += 40;
    
    // Business impact
    const affectedUsers = extractNumber(issue.description, 'affected users');
    score += Math.min(affectedUsers / 10, 30);
    
    // Technical factors
    if (issue.labels.includes('env/production')) score += 20;
    if (issue.labels.includes('component/payment')) score += 25;
    
    // Set priority based on score
    if (score >= 70) return 'Critical';
    if (score >= 40) return 'High';
    if (score >= 20) return 'Medium';
    return 'Low';
}
```

### Intelligent Assignment
```javascript
function assignBasedOnExpertise(issue) {
    const expertise = {
        'john': ['frontend', 'react', 'css'],
        'sarah': ['backend', 'python', 'api'],
        'mike': ['database', 'postgres', 'optimization'],
        'lisa': ['infrastructure', 'kubernetes', 'aws']
    };
    
    // Score each engineer
    const scores = {};
    for (const [engineer, skills] of Object.entries(expertise)) {
        scores[engineer] = 0;
        for (const skill of skills) {
            if (issue.title.toLowerCase().includes(skill) ||
                issue.description.toLowerCase().includes(skill)) {
                scores[engineer] += 10;
            }
        }
        
        // Consider current workload
        const currentWork = await getEngineerWorkload(engineer);
        scores[engineer] -= currentWork * 2;
    }
    
    // Assign to best match
    const bestMatch = Object.entries(scores)
        .sort(([,a], [,b]) => b - a)[0][0];
    
    return assignIssue(issue.id, bestMatch);
}
```

## Automation Monitoring

### Track Automation Effectiveness
```yaml
Metrics to Track:
  - Rules triggered per day
  - Time saved per automation
  - False positive rate
  - Manual override frequency

Dashboard Queries:
  - "How many issues auto-labeled correctly?"
  - "Average time from create to assign?"
  - "Percentage of issues needing manual intervention?"
  - "Which automations save the most time?"

Review Cadence:
  - Daily: Check for failures
  - Weekly: Review effectiveness
  - Monthly: Optimize rules
  - Quarterly: ROI analysis
```

## Best Practices

### 1. Start Simple
- Begin with basic labeling
- Add complexity gradually
- Test thoroughly before enabling

### 2. Avoid Over-Automation
- Keep human in the loop for critical decisions
- Allow manual overrides
- Log all automated actions

### 3. Monitor and Iterate
- Track automation metrics
- Review false positives
- Adjust rules based on feedback

### 4. Document Everything
- Document what each automation does
- Include disable instructions
- Maintain automation runbook

### 5. Test in Staging
- Test automations on test projects first
- Run in parallel before switching
- Have rollback plan

## Troubleshooting

### Common Issues

**Automation Not Triggering**
- Check webhook URL is correct
- Verify API key has permissions
- Review automation logs
- Test with simple rule first

**Too Many False Positives**
- Refine trigger conditions
- Add exclusion rules
- Require multiple conditions
- Add confirmation step

**Performance Issues**
- Batch API calls
- Add rate limiting
- Use async processing
- Cache frequent queries

## Implementation Checklist

### Week 1: Basic Automation
- [ ] Set up auto-labeling rules
- [ ] Configure GitHub integration
- [ ] Enable Slack notifications
- [ ] Test state transitions

### Week 2: Advanced Rules
- [ ] Implement SLA tracking
- [ ] Add escalation rules
- [ ] Configure auto-assignment
- [ ] Set up monitoring alerts

### Week 3: Custom Scripts
- [ ] Deploy webhook handler
- [ ] Implement ROI calculator
- [ ] Add PagerDuty integration
- [ ] Create automation dashboard

### Week 4: Optimization
- [ ] Review automation metrics
- [ ] Refine rules based on data
- [ ] Document all automations
- [ ] Train team on overrides

## Next Steps

1. Start with [SETUP.md](./SETUP.md) for initial configuration
2. Configure [LABELS.md](./LABELS.md) for automation triggers
3. Review [METRICS.md](./METRICS.md) to track automation ROI
4. Follow [DAILY_OPERATIONS.md](./DAILY_OPERATIONS.md) for automation monitoring
