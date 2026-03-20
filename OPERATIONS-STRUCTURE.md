# OPERATIONS-STRUCTURE.md — The Complete Autonomous System

This document explains how the entire AIConsulting operation works: 6 autonomous agents executing daily + development team building features + Rich steering everything via email.

---

## The System in a Nutshell

**Every day**:
1. Six agents run autonomously (content, networking, audits, research, sales, reporting)
2. Rich receives one email at 5 PM with all metrics
3. If Rich wants adjustments, he replies with steering instructions
4. Agents adjust for the next day

**Every week**:
1. PM proposes features based on data
2. Rich approves via email
3. Dev builds (opens PR, tests in staging)
4. Rich reviews PR + approves merge
5. Feature sits in main until Rich marks "ready to deploy"
6. Heartbeat deploys when ready

**Result**: Fully autonomous operation that Rich oversees via email only.

---

## The Six Daily Agents

### 1. Content Agent
**Time**: 8 AM (Mon/Wed/Fri)
**Output**: LinkedIn posts (3x/week)
**Goal**: 50+ reactions per post
**Input**: Theme (myth-busting, behind-the-scenes, proof points)

Rich sees drafts 24h before posting → can approve/edit/skip

### 2. Networking Agent
**Time**: 11 AM (daily) + 12:30 PM (daily)
**Output**: 20 connection requests + 5 follow-up DMs per day
**Goal**: 30%+ accept rate, 5+ warm leads/week
**Input**: ICP (10-50 person SMBs, $1M-$50M, CEO/founder)

Rich steers: Industry targeting, personalization approach

### 3. Audit Agent
**Time**: 2 PM offers, 6 PM follow-ups (daily)
**Output**: Audit offers + calendar bookings + email nurture sequences
**Goal**: 1-2 audits booked per week
**Input**: Warm leads from Networking Agent, Landing page, DMs

Rich steers: Offer frequency, email copy, calendar availability

### 4. Research Agent
**Time**: Continuous (2-3x daily)
**Output**: Market trends, case study ideas, positioning insights
**Goal**: 2-3 actionable insights per week
**Input**: AI news feeds, competitor analysis, audit feedback

Rich steers: Research focus areas, what matters for our positioning

### 5. Sales Agent
**Time**: 1 PM qualification, ongoing pipeline (daily)
**Output**: Qualified leads, demos booked, pipeline tracking
**Goal**: 5+ qualified leads/week, 2-3 demos/week
**Input**: Leads from all sources, qualification rubric

Rich steers: Qualification criteria, demo frequency, pipeline management

### 6. Reporting Agent
**Time**: 5 PM (daily)
**Output**: Email report + GitHub commit
**Goal**: Clear, actionable summary
**Input**: Data from all 5 agents above

Rich sees: One email with all metrics + can reply with steering

---

## The Development Team

### Developer (Autonomous Subagent)
- Watches Jira tickets in AIC project
- Writes code for approved features
- Opens PRs with detailed descriptions
- Tests in staging before opening PR
- Merges only when Rich approves PR

### Project Manager (Autonomous Subagent + Creative Advisor)
- Reviews daily Reporting Agent emails
- Analyzes: What's working? What's not?
- Proposes features based on data
- Creates Jira tickets with full context
- Emails proposals to Rich with impact estimates
- Negotiates direction with Rich if he suggests alternatives
- Updates product roadmap based on Rich's feedback

---

## Rich's Daily/Weekly Workflow

### Monday-Sunday: 5 PM
Rich receives Reporting Agent email with metrics:
```
Content: 3 posts published, avg 45 reactions
Networking: 140 connection requests sent, 32% accept rate (38 new connections)
Audits: 15 offers sent, 2 booked
Sales: 5 qualified leads, 1 demo scheduled
Research: AI market shift to outcome-based pricing, SMB opportunity growing
```

**Rich's decision**: Reply with steering or skip (default: no changes)

**Example steering reply**:
```
@ContentAgent: "Here's why your AI project fails" posts are outperforming.
Keep that theme going. Try more opinionated takes.

@NetworkingAgent: Accept rate is solid. Increase personal touches in connection requests.

@AuditAgent: Booking rate is low (13%). Try a different email angle or softer CTA.
```

Agents implement changes by next day.

### Weekly: PM Proposal
When PM identifies an opportunity:
```
Subject: Proposal: Email Nurture Sequence (AIC-3) — Warm Up Cold Leads

Data: 20% of audit offers get no response (4/week). 
Solution: 3-email nurture sequence that keeps prospects warm.
Impact: Convert 20% of cold leads to warm, +1 demo/week
Cost: $5k dev time
Timeline: 1 week

Approval?
```

**Rich replies**: "Approved" or "Pass, prioritize X instead" or "Let me see email copy first"

Once approved, Dev creates Jira ticket + starts building.

### Weekly: PR Review
When Dev opens PR:
```
[AIC-3] Email Nurture Sequence - Warm Up Cold Leads

Changes:
- 3 automated emails (days 1, 3, 7)
- Personalized based on audit findings
- CTA escalates (soft → harder)

Testing: Email sent in staging, confirmed delivery + opens
```

Rich reviews staging + approves: "LGTM, merge when ready"

Dev merges to main. Feature sits in staging.

### As-Needed: Deployment Decision
Rich reviews staging version. If happy, marks in AVAILABLE-FEATURES.md:
```
## Ready to Deploy
- [x] AIC-3: Email Nurture Sequence (approved, ready for production)
```

Heartbeat deploys automatically next day (6 AM check).

---

## Daily Schedule (Times EDT)

```
8:00 AM   — Content Agent publishes Mon/Wed/Fri posts
11:00 AM  — Networking Agent sends 20 connection requests
12:30 PM  — Networking Agent sends 5 follow-up DMs
1:00 PM   — Sales Agent sends qualification emails
2:00 PM   — Audit Agent sends audit offer emails
6:00 PM   — Audit Agent sends follow-up reminders
5:00 PM   — Reporting Agent generates daily report + emails to Rich + commits to GitHub
6:00 AM   — Heartbeat checks AVAILABLE-FEATURES.md, deploys marked features (if any)
```

---

## The Jira Project (AIC)

**URL**: https://loveamethystrose.atlassian.net/projects/AIC

All features, bugs, and improvements tracked here. Format: `AIC-1`, `AIC-2`, etc.

**Types**:
- **Story**: Feature (from PM proposal)
- **Bug**: Issues found in production
- **Task**: Maintenance, documentation

---

## Weekly/Monthly Reports (GitHub Archive)

Every week, the Reporting Agent saves a comprehensive report to GitHub:

```
/reports/
  ├── week-01-report.md  (2026-03-26)
  ├── week-02-report.md  (2026-04-02)
  ├── week-03-report.md  (2026-04-09)
  └── ...
```

This creates a permanent record of what happened each week, useful for:
- Trend analysis (is engagement going up or down?)
- Course correction (did steering changes work?)
- Learning (what worked, what didn't)
- Reporting to stakeholders

---

## Decision-Making Framework

### Operations Decisions (Daily)
- **Who decides**: Rich (via email reply to Reporting Agent)
- **Timeline**: Same day (5 PM report → next morning implementation)
- **Examples**: Content themes, network targeting, audit offers, demo frequency
- **Effort**: 15-30 min/day to review and steer

### Development Decisions (Weekly/As-Needed)
- **Who decides**: Rich (via email reply to PM proposal + PR review)
- **Timeline**: 
  - Proposal approval: Same day
  - PR review: Within 24 hours
  - Deployment: When Rich marks "ready"
- **Examples**: Feature priorities, technical approach, design decisions
- **Effort**: 15-30 min per proposal, 15-30 min per PR

### Strategic Decisions (Monthly+)
- **Who decides**: Rich
- **Timeline**: As-needed (monthly review of PLAN.md progress)
- **Examples**: Pivot to new market, adjust messaging, change service tiers
- **Effort**: 1-2 hours per month

---

## What Gets Automated (Agents)

✅ **Content creation & publishing** (LinkedIn posts)
✅ **Network outreach** (connection requests, DMs)
✅ **Lead generation** (audit offers, calendar bookings)
✅ **Sales qualification** (lead scoring, demo scheduling)
✅ **Market research** (trends, case studies, positioning)
✅ **Reporting** (daily metrics, weekly archive)
✅ **Feature development** (code, PRs, testing)
✅ **Project management** (proposal creation, roadmap)
✅ **Deployments** (Heartbeat checks AVAILABLE-FEATURES.md)

### What Rich Does (Steering Only)

✅ **Strategic direction** (via PM conversations)
✅ **Quality gates** (PR approvals, deployment decisions)
✅ **Course correction** (reply to daily email with steering)
✅ **Final approval** (PR merge, feature launch)

---

## Communication Flow (Simple Diagram)

```
DAILY (Reporting Agent → Email to Rich @ 5 PM)
├─ Content metrics
├─ Networking metrics
├─ Audit metrics
├─ Sales metrics
├─ Research insights
└─ Recommended adjustments

Rich reviews → Replies with steering (optional)
└─ Agents adjust for next 24h

---

WEEKLY (PM → Email to Rich)
├─ Jira ticket created (AIC-#)
├─ Proposal sent with:
│  ├─ Data analysis
│  ├─ Problem statement
│  ├─ Solution + impact estimate
│  └─ Timeline/cost
└─ Rich approves (email) → Dev starts work

Dev writes code → Opens PR → Rich reviews → Approves
└─ Feature merges to main (not live yet)

Rich reviews staging → Marks "ready to deploy" in AVAILABLE-FEATURES.md
└─ Heartbeat deploys next day

---

MONTHLY (Rich reviews progress vs. PLAN.md)
└─ Adjust strategy if needed
```

---

## Success Metrics (By Phase)

### Phase 1: Positioning (Weeks 1-2)
- [ ] LinkedIn profile rebranded
- [ ] 3x/week content cadence started
- [ ] 200+ new connections
- [ ] Engagement trending up (target: 50+ per post)

### Phase 2: Validation (Weeks 3-4)
- [ ] 10 free audits completed
- [ ] Market feedback collected
- [ ] Messaging refined
- [ ] First 1-2 leads responding to audits

### Phase 3: Productization (Weeks 5-6)
- [ ] 3 service packages defined
- [ ] 2-3 case studies drafted
- [ ] Landing page live
- [ ] Quiz funnel collecting leads

### Phase 4: Funnel (Weeks 7-8)
- [ ] 30+ quiz starts
- [ ] 5-10 high-fit leads identified
- [ ] 2-3 meetings booked
- [ ] Pipeline forming

### Phase 5: Scale (Weeks 9-12)
- [ ] 3-5 clients closed
- [ ] $15-30k MRR achieved
- [ ] Repeatable playbook documented
- [ ] Agents running smoothly

---

## Failure Modes & Guardrails

### If Content Engagement Drops
**Guardrail**: Reporting Agent alerts in weekly report
**Fix**: Rich steering email → adjust themes
**Escalation**: PM proposes landing page or email overhaul (AIC-#)

### If Lead Quality Drops
**Guardrail**: Sales Agent tracks conversion rate
**Fix**: Rich narrows qualification criteria (budget, timeline)
**Escalation**: PM proposes targeting change or messaging adjustment

### If Demos Aren't Converting
**Guardrail**: Sales Agent + Reporting Agent flag low demo conversion
**Fix**: Rich adjusts sales script (via PM proposal)
**Escalation**: Record calls, analyze objections, propose overhaul

### If Deployment Breaks Production
**Guardrail**: Heartbeat monitors for errors
**Fix**: Rich approves rollback
**Escalation**: PM creates bug ticket (AIC-#), Dev fixes

---

## Onboarding a New Team Member

If Rich wants to add a human team member (e.g., real PM or Dev):

1. **Give them access to**:
   - Jira project (AIC)
   - GitHub repo (lar-devbot/AIConsulting)
   - Email inbox (for Reporting Agent)
   - Staging/Production environments

2. **They read**:
   - PLAN.md (understand the goal)
   - AGENTS.md (understand the agents)
   - DEVELOPMENT.md (understand the workflow)
   - STEERING.md (understand how to work with Rich)

3. **They start by**:
   - Shadowing agents for 1 week (learn the rhythm)
   - Creating first Jira ticket (learn the process)
   - Proposing first feature (learn PM communication)

---

## Technical Stack (Deployment)

- **Repo**: GitHub (lar-devbot/AIConsulting)
- **Project Tracking**: Jira (AIC project)
- **Agents**: OpenClaw cron jobs + subagents
- **Reports**: Markdown files in `/reports/` folder
- **Production**: (TBD — depends on what we're building)
- **Staging**: (TBD — for feature testing)

---

## Key Files

| File | Purpose |
|---|---|
| **PLAN.md** | 90-day execution roadmap |
| **MESSAGING.md** | Sales narrative + positioning |
| **SERVICES.md** | Service packages + pricing |
| **AGENTS.md** | Detailed agent specifications |
| **DEVELOPMENT.md** | Dev team workflow + Jira integration |
| **STEERING.md** | How Rich directs teams |
| **AVAILABLE-FEATURES.md** | Deployment gate |
| **/reports/** | Weekly metrics + trend archive |

---

## Next Steps (Immediate)

1. ✅ **Repo created** (AIConsulting on GitHub)
2. ✅ **Jira project created** (AIC on loveamethystrose instance)
3. ⏳ **Create cron jobs** (Agents start running)
4. ⏳ **Launch Content Agent** (Start daily posts)
5. ⏳ **Launch Networking Agent** (Start connection requests)
6. ⏳ **Launch Audit Agent** (Start booking audits)
7. ⏳ **Launch Research Agent** (Start monitoring market)
8. ⏳ **Launch Sales Agent** (Start qualifying leads)
9. ⏳ **Launch Reporting Agent** (Start daily emails)
10. ⏳ **Assign Dev** (Start working on AIC tickets)
11. ⏳ **Assign PM** (Start monitoring data, proposing features)

---

## Success Looks Like

- **Daily**: Rich spends 15-30 min reviewing email report + steering (optional)
- **Weekly**: PM proposes 1-2 features, Dev is actively building
- **Monthly**: 30-50% progress toward PLAN.md milestones
- **Quarterly**: $30k/month revenue achieved, operations running smoothly

---

**Operational Structure**: Complete
**Deployed**: 2026-03-20
**Next review**: 2026-04-06 (end of Phase 1)
