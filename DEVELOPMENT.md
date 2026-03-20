# DEVELOPMENT.md — Development & Product Team

## Team Structure

- **Developer**: Builds features, writes code, opens PRs
- **Project Manager**: Reviews data, proposes solutions, negotiates direction with Rich

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

## PR Workflow

### Step 1: Create Jira Ticket

Developer or PM creates a Jira ticket in the AIC project:
- **Type**: Story (for features) or Bug (for issues)
- **Title**: Clear description (e.g., "Landing page redesign for better conversion")
- **Description**: What needs to be done, why, and expected outcome
- **Assignee**: Developer
- **Label**: `development` or `ops` (for operations team tasks)

**Example ticket (AIC-1)**:
```
Title: Landing Page Redesign - Improve Quiz Conversion
Type: Story
Status: To Do
Description:
- Current quiz completion rate: 60%
- Target: 70% (with redesign)
- Work includes:
  * Simplify value prop above fold
  * Add progress bar to reduce abandonment
  * Redesign results screen with clear CTA
  * Add testimonials/social proof
- Acceptance criteria:
  * Quiz completion rate test shows 70%+ in staging
  * Mobile-responsive design
  * Load time < 2 seconds
- Estimate: 40 hours
```

### Step 2: Create Feature Branch

Developer checks out a feature branch:

```bash
git checkout -b feature/AIC-1-landing-page-redesign
```

### Step 3: Write Code

Developer builds the feature with:
- **Clean code**: Well-organized, documented
- **Unit tests**: For critical logic
- **Documentation**: README or inline comments explaining changes
- **Commits**: Descriptive commit messages

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

### Step 5: Rich Reviews & Approves

Rich reviews the PR:
- Checks code quality
- Reviews design changes
- Verifies functionality in staging
- Approves or requests changes

Rich can reply with:
```
Looks great. Small tweak: Can you adjust the CTA button color to match our brand blue (#2563EB)? Otherwise, approved to merge.
```

### Step 6: Merge to Main

Once approved, developer merges to main:

```bash
git merge feature/AIC-1-landing-page-redesign --ff-only
git push origin main
```

**Note**: Only `main` branch is pushed to production. Features sit in main until marked "ready to deploy" in AVAILABLE-FEATURES.md.

### Step 7: Mark Ready (If Deployment Needed)

If the feature should go live, update AVAILABLE-FEATURES.md:

```markdown
## Ready to Deploy (Will go live on next heartbeat)
- [x] AIC-1: Landing Page Redesign (merged, awaiting approval to deploy)
```

### Step 8: Heartbeat Deploys

Heartbeat checks AVAILABLE-FEATURES.md daily:
- Sees AIC-1 is marked "ready"
- Pulls latest `main` branch
- Deploys feature to production
- Updates AVAILABLE-FEATURES.md to "Recently Deployed"

---

## Project Manager Role

PM is not just project management — **PM is also creative strategy advisor**.

### PM Responsibilities

1. **Review daily/weekly agent reports** (from Reporting Agent)
   - What's working? (networking, content, conversions)
   - What's not? (low engagement, stalled leads)

2. **Analyze data** deeply
   - Traffic patterns
   - Conversion rates
   - Lead quality
   - Engagement metrics

3. **Propose solutions** based on data
   - What feature/change would improve results?
   - Why would it help?
   - What's the estimated impact?

4. **Estimate impact** in terms Rich cares about
   - Revenue impact (more leads, higher conversion)
   - Cost savings (automation efficiency)
   - Time saved (dev hours to build it)

5. **Create Jira tickets** for proposed features
   - PM writes the ticket with full context
   - Creates acceptance criteria
   - Provides data backing the proposal

6. **Email proposals to Rich** with data + impact estimate
   - Subject: "Proposal: [Feature Name] (AIC-#)"
   - Rich approves via email reply
   - Once approved, Dev starts on Jira ticket

7. **Negotiate direction** with Rich
   - Rich might say "no, prioritize [other thing]"
   - PM adjusts backlog and communicates with Dev

---

## PM Proposal Workflow (Detailed Example)

### Scenario: Quiz Completion Rate Dropping

**Data from Reporting Agent** (Week 2 report):
```
Quiz Starts: 30
Quiz Completions: 18 (60%)
High-fit Leads: 8
Demos Booked: 0

Insight: Quiz starts are good, but completions are low. 
12 leads lost (40% abandonment) = potential $60k/year lost revenue
```

### PM Analysis
- Root cause: Quiz results screen doesn't have clear next steps
- Users see results but don't know what to do
- They leave without booking a demo

### PM Creates Jira Ticket (AIC-1)

**Title**: Landing Page Redesign - Improve Quiz Conversion
**Type**: Story
**Priority**: High (direct revenue impact)
**Description**: See branching strategy section above

### PM Sends Email to Rich

```
Subject: Proposal: Landing Page Redesign (AIC-1) — Improve Quiz Conversion

Hi Rich,

Data from this week shows a concerning trend:
- Quiz starts: 30 ✅ (good)
- Quiz completions: 18 (60%) ⚠️ (losing 40%)
- High-fit leads: 8
- Demos booked: 0 ❌ (should be 3-4)

The bottleneck: Quiz results don't have a clear "book a demo" CTA. 
Users see their audit results but don't know the next step, so they leave.

PROPOSED SOLUTION: Landing Page Redesign (AIC-1)
- Simplify quiz intro for clarity
- Add progress bar (psychology: people feel invested)
- Redesign results screen with prominent "Book Your Audit" CTA
- Add testimonials above fold (social proof)
- Mobile optimizations

ESTIMATED IMPACT:
- Quiz completion: 60% → 70% (retain 3 more leads/week)
- Demo bookings: 0 → 3-4/week
- Cost per demo: $1,500 (AIC-1 dev time, amortized)
- Value per demo: ~$5k retainer = $15k annual value
- ROI: 10x in first month

TIMELINE: Dev estimates 2-3 weeks (40 hours)

APPROVAL NEEDED:
Is this the right priority for next 2 weeks?
Any changes to the proposal?

Thanks,
PM
```

### Rich Replies

```
Subject: RE: Proposal: Landing Page Redesign (AIC-1) — Improve Quiz Conversion

Approved. Love the data and approach.

One addition: In the results screen, can we add "guaranteed 7-month payback" messaging? 
That's our biggest differentiator vs. competitors.

Create the Jira ticket and have Dev start when ready.

Rich
```

### PM Updates Jira Ticket

PM adds Rich's feedback to the AIC-1 ticket:
```
Acceptance Criteria:
✓ Quiz completion rate 70%+ in staging
✓ Mobile-responsive design
✓ "Guaranteed 7-month payback" messaging on results screen
✓ Load time < 2 seconds
```

Changes ticket status to "In Progress" and assigns to Dev.

### Dev Starts Work

Dev checks out feature branch and begins work:
```bash
git checkout -b feature/AIC-1-landing-page-redesign
# ... 2-3 weeks of development ...
git push origin feature/AIC-1-landing-page-redesign
# Opens PR to main
```

### Rich Reviews + Approves PR

PR is reviewed by Rich, approved, merged to main.

### Feature Sits in Main (Not Live Yet)

The redesigned landing page is now in `main` but not live.
Staging version available at: `https://staging.example.com`

### Rich Decides When to Deploy

Once Rich sees the staging version working well, he marks it "ready to deploy":

```markdown
## AVAILABLE-FEATURES.md

## Ready to Deploy (Will go live on next heartbeat)
- [x] AIC-1: Landing Page Redesign (approved by Rich, ready for traffic)
```

### Heartbeat Deploys to Production

Next daily heartbeat:
1. Checks AVAILABLE-FEATURES.md
2. Sees AIC-1 is ready
3. Pulls latest main branch code
4. Deploys to production
5. Confirms deployment via email to Rich

Result: Live landing page redesign, driving 3-4 more demos/week.

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

### Backlog Management

Tickets live in Jira, but summary available in DEVELOPMENT.md:

**Active** (In progress):
- AIC-1: Landing Page Redesign (Dev: 40 hrs)

**Ready** (Waiting for Dev):
- AIC-2: Automated Email Sequences (PM proposal approved)
- AIC-3: Quiz Analytics Dashboard (In discussion with Rich)

**Proposed** (Awaiting PM proposal):
- Content Agent Improvements
- SMS Notification System
- Referral Tracking

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

## Deployment Checklist (Before Marking "Ready")

Before PM marks a feature "ready to deploy", confirm:

- [ ] PR merged to main
- [ ] Code tested in staging
- [ ] Mobile-responsive verified
- [ ] Load time acceptable
- [ ] Email templates reviewed (if applicable)
- [ ] Database migrations ready (if applicable)
- [ ] Rollback plan documented
- [ ] Rich has reviewed and approved

---

## Communication Flow

```
Daily Operations:
Reporting Agent → Email to Rich (5 PM daily)
                ↓
Rich reviews, replies with steering
                ↓
Agents adjust for next day

Weekly Development:
PM monitors data → PM creates Jira tickets → PM emails proposal to Rich
                                                        ↓
Rich approves (email) → Dev starts work (Jira ticket) → Dev opens PR
                                                        ↓
Rich reviews PR → Approves → Dev merges to main → Feature in staging
                                                        ↓
Rich marks "ready to deploy" in AVAILABLE-FEATURES.md
                                                        ↓
Heartbeat deploys to production → Confirmation email to Rich
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
