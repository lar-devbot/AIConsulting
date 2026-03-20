# DEVELOPMENT.md — Autonomous Dev & PM Agents

## Agent Structure

- **Developer Agent** (Autonomous Subagent): Builds features, writes code, opens PRs
- **Project Manager Agent** (Autonomous Subagent): Reviews data, proposes solutions, creates Jira tickets

Both agents run continuously. Rich has approval gates at key decision points.

---

## Jira Project: AIConsulting (AIC)

**Jira URL**: https://loveamethystrose.atlassian.net/projects/AIC
**Project Key**: AIC
**Project Name**: AIConsulting
**Instance**: loveamethystrose.atlassian.net

This is where all tickets, features, bugs, and PM proposals are tracked.

---

## Branching Strategy

All feature branches follow this format:

```
feature/AIC-<ticket-number>-<descriptive-name>
```

**Examples**:
- `feature/AIC-1-landing-page-redesign`
- `feature/AIC-2-quiz-funnel-implementation`
- `feature/AIC-3-automated-email-sequence`
- `feature/AIC-12-content-agent-improvements`

---

## Developer Agent Workflow

### Step 1: Watch Jira for New Tickets

Developer Agent watches the AIC Jira project for new tickets assigned to it.

**Trigger**: PM creates ticket (AIC-#) and marks "Ready to Build"

### Step 2: Check Out Feature Branch

Developer creates feature branch:

```bash
git checkout -b feature/AIC-1-landing-page-redesign
```

### Step 3: Write Code

Developer builds the feature with:
- **Clean code**: Well-organized, documented
- **Unit tests**: For critical logic
- **Documentation**: README or inline comments explaining changes
- **Commits**: Descriptive, reference Jira ticket

Example commits:
```
git commit -m "AIC-1: Add progress bar to quiz (reduces abandonment by 5%)"
git commit -m "AIC-1: Redesign results screen with social proof section"
git commit -m "AIC-1: Mobile-responsive improvements, test on iOS/Android"
```

### Step 4: Open Pull Request

Developer opens a PR to `main` with:

```
Title: [AIC-1] Landing Page Redesign - Improve Quiz Conversion

Description:
This PR addresses quiz completion rate drop from 60% to target 70%.

Changes:
- Redesigned quiz intro for clearer value prop
- Added progress bar (psychological trick to reduce abandonment)
- Redesigned results screen with immediate CTA
- Added testimonials above fold for social proof
- Mobile-responsive improvements

Impact:
- Expected quiz completion: 60% → 70%
- Expected demo booking increase: 0 → 3-4/week
- Load time maintained at <2 seconds (tested in staging)

Testing:
- Tested on Chrome, Safari, Firefox (desktop)
- Tested on iOS Safari and Android Chrome
- Staging URL: https://staging.example.com
- Quiz completion test shows 68% in staging (close to target)

Closes: AIC-1
```

### Step 5: Wait for Rich's Approval

Rich reviews the PR (code quality, design, functionality) and replies:

```
Looks great. Small tweak: Can you adjust the CTA button color 
to match our brand blue (#2563EB)? Otherwise, approved to merge.
```

Developer makes adjustments if needed, then merges.

### Step 6: Merge to Main

Once Rich approves:

```bash
git merge feature/AIC-1-landing-page-redesign --ff-only
git push origin main
```

**Note**: Feature sits in `main` (live code) but not deployed until Rich marks "ready" in AVAILABLE-FEATURES.md.

---

## Project Manager Agent

PM Agent is autonomous and runs continuously, monitoring data and proposing improvements.

### PM Agent Schedule

- **Continuous**: Monitor Reporting Agent emails (new ones arrive @ 5 PM daily)
- **Daily analysis**: Review metrics, trends, opportunities
- **Weekly proposals**: Identify top improvement opportunity, create Jira ticket + email to Rich
- **On-demand**: Adjust backlog based on Rich's feedback

### PM Agent Workflow

#### Step 1: Monitor Daily Data

PM watches for new Reporting Agent emails (every day @ 5 PM).

**Data reviewed**:
- Content engagement (posts, reactions, comments)
- Network growth (connections, DM responses, warm leads)
- Audit booking rate
- Sales conversion metrics
- Research insights

**Analysis**:
- What's working? (high engagement, conversions increasing)
- What's not? (low completion rate, stalled leads)
- What's the trend? (improving or declining?)

#### Step 2: Identify Improvement Opportunities

PM answers: "What feature/change would improve results?"

**Examples**:
- "Quiz completion rate dropping → Landing page redesign could improve UX"
- "No demo conversions → Email nurture sequence could warm up cold leads"
- "Low content engagement → Adjust posting times / themes"
- "Quiz abandonment high → Add progress bar (psychology)"

#### Step 3: Estimate Impact

PM calculates:
- **Revenue impact**: How many more leads/demos/sales?
- **Cost impact**: How many dev hours needed?
- **Timeline**: How long to build?
- **ROI**: Is it worth doing?

**Example calculation**:
```
Current: 30 quiz starts, 18 completions (60%)
Proposed: Landing page redesign
Impact: 30 quiz starts, 21 completions (70%) = 3 more leads/week
Value: 3 leads × $5k/month = $15k annual value
Cost: 40 hours dev time
Timeline: 2-3 weeks
ROI: $15k value vs. $6k cost = 2.5x in month 1
```

#### Step 4: Create Jira Ticket

PM creates new Jira ticket in AIC project:

**Ticket format**:
```
Title: Landing Page Redesign - Improve Quiz Conversion
Type: Story
Priority: High (direct revenue impact)
Estimate: 40 hours
Description:

PROBLEM:
Quiz completion rate is 60%, losing 12 leads/week.
Users see results but don't know next steps.

SOLUTION:
Redesign landing page to:
- Simplify value prop
- Add progress bar
- Redesign results screen with clear CTA
- Add testimonials/social proof

IMPACT:
- Completion rate: 60% → 70%
- Additional leads: 3/week
- Revenue value: $15k/year
- Cost: 40 hours dev time
- ROI: 2.5x in month 1

ACCEPTANCE CRITERIA:
- Quiz completion rate ≥ 70% in staging tests
- Mobile-responsive design
- Load time < 2 seconds
- "Guaranteed 7-month payback" messaging included

BLOCKED BY: None
DEPENDS ON: None
```

#### Step 5: Email Proposal to Rich

PM sends email to Rich with detailed proposal:

```
Subject: Proposal: Landing Page Redesign (AIC-1) — Improve Quiz Conversion

Hi Rich,

Data from this week shows a problem:

CURRENT STATE:
- Quiz starts: 30 ✅
- Quiz completions: 18 (60%) ⚠️ ← Losing 12 leads
- Demos booked: 0 ❌

ROOT CAUSE:
Users complete quiz but see results without clear "next steps."
They don't know what to do, so they leave.

PROPOSED SOLUTION:
Landing Page Redesign (AIC-1)

What we'd change:
- Simplify quiz intro (clearer value prop above fold)
- Add progress bar (psychology: invested users complete more)
- Redesign results screen with prominent "Book Your Audit" CTA
- Add testimonials/social proof section
- Mobile-responsive improvements

ESTIMATED IMPACT:
- Quiz completion: 60% → 70% (3 more leads/week)
- Annual value: $15k (3 leads × $5k/month)
- Dev cost: 40 hours (~$6k in labor)
- Timeline: 2-3 weeks
- ROI: 2.5x in month 1 alone

JIRA TICKET:
Created: AIC-1 (full acceptance criteria included)

APPROVAL NEEDED:
[ ] Yes, start immediately
[ ] Yes, but with adjustments (see below)
[ ] No, prioritize something else
[ ] Not yet, wait until [date]

If yes, I'll notify Dev Agent to start work.

Thanks,
PM
```

#### Step 6: Wait for Rich's Decision

Rich replies to the email:

**Option A: Approved**
```
Approved. Start immediately.

One addition: Make sure the results screen includes 
"Guaranteed 7-month payback" messaging — that's our #1 differentiator.

Let me know when Dev opens the PR.
```

PM replies to confirm, notifies Dev Agent to start work on AIC-1.

**Option B: With tweaks**
```
Approved, but I want to see two versions of the CTA button color
(blue vs. green) and A/B test them. Otherwise, same scope.

Let me know when ready.
```

PM updates AIC-1 ticket, notifies Dev Agent.

**Option C: Postponed**
```
Good analysis, but I want to focus on sales first.
Pause this until we have 3+ demos booked.

What's the next opportunity you see?
```

PM notes this in Jira backlog, moves on to next opportunity.

#### Step 7: Continuous Monitoring

While Dev is building, PM:
- Watches for new data/trends
- Identifies next proposal opportunity
- Prepares follow-up features
- Tracks Dev progress (watches PR activity)

---

## Rich's Decision Points

### 1. PM Proposal Review (Email)
**When**: PM sends proposal email
**Rich decides**: Approve, tweak, postpone, or reject
**Timeline**: Same day reply

### 2. PR Code Review (GitHub)
**When**: Dev opens PR
**Rich decides**: Approve merge, request changes, or reject
**Timeline**: Within 24 hours

### 3. Deployment Decision (AVAILABLE-FEATURES.md)
**When**: Feature is merged and in staging
**Rich decides**: Mark "ready to deploy" or hold
**Timeline**: When tested in staging

---

## Ticket Numbering & Backlog

### Ticket Format

All tickets use this format:
```
AIC-1: [Feature/Bug Name]
AIC-2: [Feature/Bug Name]
AIC-3: [Feature/Bug Name]
...
```

Increment by 1 for each new ticket.

### Backlog Status

Tickets in Jira show:

**To Do** (Awaiting approval from Rich):
- AIC-2: Automated Email Sequences (PM proposal sent, waiting for approval)
- AIC-3: Quiz Analytics Dashboard (In discussion with Rich)

**Ready to Build** (Approved, waiting for Dev):
- AIC-1: Landing Page Redesign (Approved by Rich, waiting for Dev to start)

**In Progress** (Dev is building):
- AIC-1: Landing Page Redesign (Dev on feature branch, PR in progress)

**In Review** (PR open, waiting for Rich approval):
- AIC-1: Landing Page Redesign (PR open at #1, awaiting Rich approval to merge)

**Done** (Merged to main, in staging):
- AIC-1: Landing Page Redesign (PR #1 merged, in staging, ready for deployment decision)

**Deployed** (Live on production):
- None yet

---

## Code Quality Standards

### Commits
- Descriptive: Explain WHAT and WHY
- Reference Jira ticket: `git commit -m "AIC-1: Add progress bar to quiz"`
- Atomic: One feature per commit
- No WIP commits in main branch

### PRs
- Title includes ticket number: `[AIC-1] Landing Page Redesign`
- Description explains context, changes, and testing
- No merges without Rich approval
- All CI checks passing before merge

### Documentation
- README updates if new systems added
- Inline comments for complex logic
- Commit messages double as documentation

---

## Deployment Checklist

Before marking a feature "ready to deploy" in AVAILABLE-FEATURES.md, confirm:

- [ ] PR merged to main
- [ ] Code tested in staging
- [ ] Mobile-responsive verified
- [ ] Load time acceptable
- [ ] Email templates reviewed (if applicable)
- [ ] Database migrations ready (if applicable)
- [ ] Rollback plan documented
- [ ] Rich has reviewed staging and approved

---

## Communication Flow

```
DAILY:
Reporting Agent email (5 PM) → Rich reviews → Replies with steering (optional)

WEEKLY:
PM monitors data → Identifies opportunity → Creates Jira ticket → Sends proposal email
                                                                        ↓
Rich approves (email) → PM notifies Dev Agent → Dev starts work (feature branch)
                                                                        ↓
Dev writes code → Opens PR → Rich reviews → Approves merge → Dev merges to main
                                                                        ↓
Feature in staging → Rich reviews staging → Marks "ready to deploy" in AVAILABLE-FEATURES.md
                                                                        ↓
Heartbeat deploys to production → Feature goes live
```

---

## Tools & Access

- **Jira**: https://loveamethystrose.atlassian.net/projects/AIC
- **GitHub**: https://github.com/lar-devbot/AIConsulting
- **Staging**: (TBD)
- **Production**: (TBD)

---

**Development structure created**: 2026-03-20
**Jira Project**: AIC (https://loveamethystrose.atlassian.net/projects/AIC)
**Dev Agent**: Autonomous subagent
**PM Agent**: Autonomous subagent
