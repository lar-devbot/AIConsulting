# AGENT-DIAGRAM.md — The Complete 8-Agent System

## Visual Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                    AICONSULTING SYSTEM                          │
│                  (8 Autonomous Subagents)                       │
└─────────────────────────────────────────────────────────────────┘

                     OPERATIONS LAYER (6 Agents)
                           ↓

┌──────────────────┬──────────────────┬──────────────────┐
│  Content Agent   │ Networking Agent │   Audit Agent    │
│  (8 AM posts)    │  (11 AM requests)│  (2 PM offers)   │
│  50+ engagement  │  30% accept rate │  1-2 audits/week │
└──────────────────┴──────────────────┴──────────────────┘

┌──────────────────┬──────────────────┬──────────────────┐
│ Research Agent   │   Sales Agent    │ Reporting Agent  │
│ (continuous)    │   (1 PM qual)    │  (5 PM → Rich)   │
│ 2-3 insights/wk │ 5+ leads/week    │ Email + GitHub   │
└──────────────────┴──────────────────┴──────────────────┘

                           ↓
                    (All data flows to)
                           ↓
                   Reporting Agent
                   (Synthesizes all metrics)
                           ↓
                    Email @ 5 PM to Rich
                           ↓
           Rich replies with steering (optional)
                           ↓
         Agents adjust for next 24 hours

                              
                   DEVELOPMENT LAYER (2 Agents)
                           ↓

┌──────────────────────────────────────────┐
│        Project Manager Agent             │
│  • Monitors daily operations data        │
│  • Identifies improvement opportunities  │
│  • Creates Jira tickets (AIC-#)          │
│  • Emails proposals to Rich              │
│  • Waits for approval                    │
└──────────────────────────────────────────┘
                           ↓
              Rich approves (email)
                           ↓
┌──────────────────────────────────────────┐
│         Developer Agent                  │
│  • Watches Jira for "Ready to Build"     │
│  • Writes code (feature branches)        │
│  • Opens PR when done                    │
│  • Tests in staging                      │
│  • Waits for Rich's PR approval          │
│  • Merges to main                        │
└──────────────────────────────────────────┘
                           ↓
              Feature in staging
                           ↓
              Rich approves staging
                           ↓
    Rich marks "ready to deploy" in
           AVAILABLE-FEATURES.md
                           ↓
          Heartbeat (6 AM daily check)
                           ↓
         Deploys to production
                           ↓
          Feature goes live
```

---

## Agent Details

### Operations Layer (6 Agents)

#### 1. Content Agent
**Purpose**: Generate and publish LinkedIn posts 3x/week
**Schedule**: 8 AM Mon/Wed/Fri
**Cycle**: 
- Receives theme from MESSAGING.md
- Generates 3 post options
- Sends to Rich for approval 24h before posting
- Publishes at 8 AM
- Tracks engagement
**Metrics**: 50+ reactions per post
**Rich's role**: Approve/edit/skip (24h before posting)

#### 2. Networking Agent
**Purpose**: Send personalized connection requests and DMs
**Schedule**: 11 AM requests, 12:30 PM DMs (daily)
**Cycle**:
- Identifies 20 prospects matching ICP
- Sends personalized connection requests
- Sends 5 follow-up DMs to recent acceptances
- Tracks accept rate and response rate
- Flags warm leads
**Metrics**: 30%+ accept rate, 5+ warm leads/week
**Rich's role**: Steer targeting (industry, geography, profile type)

#### 3. Audit Agent
**Purpose**: Convert warm leads to booked audits
**Schedule**: 2 PM offers, 6 PM follow-ups (daily)
**Cycle**:
- Sends audit offer emails (10-15/day)
- Manages calendar bookings
- Sends nurture sequences to non-responders
- Tracks conversion rate
**Metrics**: 1-2 audits booked/week
**Rich's role**: Adjust offer frequency, email copy, calendar availability

#### 4. Research Agent
**Purpose**: Monitor market and identify opportunities
**Schedule**: Continuous (2-3x daily web searches)
**Cycle**:
- Searches for AI market trends
- Analyzes competitor positioning
- Identifies new case study opportunities
- Monitors SMB automation landscape
- Highlights positioning insights
**Metrics**: 2-3 actionable insights/week
**Rich's role**: Approve/reject recommendations

#### 5. Sales Agent
**Purpose**: Qualify leads and schedule demos
**Schedule**: 1 PM qualification (daily)
**Cycle**:
- Receives warm leads from Networking/Audit/Landing page
- Sends qualification emails
- Scores leads (hot/warm/cold)
- Schedules demos when qualified
- Tracks pipeline status
**Metrics**: 5+ qualified leads/week, 2-3 demos/week
**Rich's role**: Set qualification criteria, control demo frequency

#### 6. Reporting Agent
**Purpose**: Aggregate all metrics and send Rich daily report
**Schedule**: 5 PM daily (every day)
**Cycle**:
- Pulls latest metrics from all 6 agents
- Synthesizes into one email
- Sends to rich@strategiesoverstress.com
- Saves to GitHub `/reports/week-XX.md`
- Commits to repo
**Metrics**: Timeliness (5 PM ± 5 min), completeness
**Rich's role**: Review (15-30 min), reply with steering if needed

---

### Development Layer (2 Agents)

#### 7. Project Manager Agent
**Purpose**: Propose features based on data
**Schedule**: Continuous monitoring, weekly proposals
**Cycle**:
- Monitors Reporting Agent emails (every day @ 5 PM)
- Analyzes: What's working? What's not?
- Identifies improvement opportunity
- Calculates ROI estimate (value/cost/timeline)
- Creates Jira ticket (AIC-#) with full context
- Sends proposal email to Rich
- Waits for approval
- Notifies Dev Agent when approved
- Tracks Dev progress
- Repeats weekly
**Metrics**: 1-2 proposals/week, ROI accuracy
**Rich's role**: Approve (yes/no/maybe) via email

#### 8. Developer Agent
**Purpose**: Build features from Jira tickets
**Schedule**: Continuous (starts when ticket is "Ready to Build")
**Cycle**:
- Watches Jira for new tickets assigned to Dev
- Checks out feature branch (feature/AIC-#-name)
- Writes code, commits frequently
- Tests in staging environment
- Opens PR to main with description
- Waits for Rich's PR approval
- Merges to main (once approved)
- Notifies PM Agent feature is done
- Returns to Jira to watch for next ticket
**Metrics**: Code quality, test coverage, deployment speed
**Rich's role**: Review PR, approve merge

---

## Daily Flow

### 8 AM: Content Agent Posts
- Publishes Mon/Wed/Fri post
- Tracks engagement
- Prepares next week's drafts for approval

### 11 AM: Networking Agent Outreach
- Sends 20 connection requests
- Personal touches referencing prospect activity
- Tracks acceptance

### 12:30 PM: Networking Agent DMs
- Sends 5 follow-up DMs to recent connections
- Personalized based on their profile
- Tracks responses

### 1 PM: Sales Agent Qualification
- Sends qualification emails to warm leads
- Asks about budget, timeline, pain point
- Scores responses (hot/warm/cold)

### 2 PM: Audit Agent Offers
- Sends audit offer emails to warm leads
- Includes Calendly link for booking
- Personalized for each prospect

### 6 PM: Audit Agent Follow-ups
- Sends reminder emails to no-responders (day 3+)
- Escalating CTA (soft → harder)
- Tracks email opens

### 5 PM: Reporting Agent Email
- Synthesizes all daily metrics
- Sends email to Rich
- Saves to GitHub
- **Rich reviews (15 min)**
- **Rich replies with steering (optional, 10 min)**

---

## Weekly Flow

### Monday-Sunday: Research Agent
- Continuous monitoring of AI market
- Competitive analysis
- Case study identification
- Findings included in Reporting Agent email

### Anytime: Project Manager Agent
- When opportunity identified, PM proposes
- Emails Rich with analysis + ROI
- Creates Jira ticket (AIC-#)
- **Rich approves (email)**
- **PM notifies Dev Agent**

### When PR Opens: Developer Agent
- **Rich reviews PR** (15-30 min)
- **Rich approves or requests changes**
- **Dev merges when approved**

### When Feature Complete: Deployment Gate
- **Rich reviews staging**
- **Rich marks "ready to deploy" in AVAILABLE-FEATURES.md**
- **Heartbeat deploys next morning (6 AM)**

---

## Decision Gates (Where Rich Steps In)

```
                    ┌─────────────────────────┐
                    │     Content Agent       │
                    │  (Daily posts)          │
                    └────────────┬────────────┘
                                 ↓
                   Rich approves 24h before
                   (content drafts)
                                 ↓
                    ┌─────────────────────────┐
                    │   All other 5 agents    │
                    │  (Run autonomously)     │
                    │  (Steering via email)   │
                    └────────────┬────────────┘
                                 ↓
                   Reporting Agent email @ 5 PM
                                 ↓
                    Rich steers (optional)
                   (Affects next 24 hours)
                                 ↓
                    ┌─────────────────────────┐
                    │   PM Agent (weekly)     │
                    │  (Proposes features)    │
                    └────────────┬────────────┘
                                 ↓
                    Rich approves proposal
                   (Yes/No/Maybe via email)
                                 ↓
                    ┌─────────────────────────┐
                    │    Dev Agent            │
                    │  (Builds feature)       │
                    └────────────┬────────────┘
                                 ↓
                      Dev opens PR
                                 ↓
                    Rich reviews PR
                   (Approves merge)
                                 ↓
                      Feature in staging
                                 ↓
                    Rich marks "ready to deploy"
                   (in AVAILABLE-FEATURES.md)
                                 ↓
                    Heartbeat deploys
                                 ↓
                    Feature goes live
```

---

## Rich's Time Investment

| Activity | Time/Day | Time/Week |
|---|---|---|
| Review Reporting Agent email | 15-30 min | 2-3.5 hours |
| Reply with steering (if needed) | 10-15 min | 0-2 hours |
| Review PM proposal (if arrives) | 15-20 min | 0-1 hour |
| Review PR (if arrives) | 15-30 min | 0-1 hour |
| **Total** | **55-95 min** | **2-7.5 hours** |

**Average**: ~3-4 hours/week oversight for a fully autonomous operation

---

## System Health Indicators

**Watch these metrics to know if the system is working**:

**Green** (All good):
- ✅ Content engagement: 50+/post
- ✅ Network accept rate: 30%+
- ✅ Audits booked: 1-2/week (by week 4)
- ✅ Sales demos booked: 2-3/week (by week 6)
- ✅ PM proposals: 1-2/week (data-driven)
- ✅ Dev velocity: 1 feature/week

**Yellow** (Attention needed):
- ⚠️ Content engagement: 20-50/post (trending down)
- ⚠️ Network accept rate: 15-30% (below target)
- ⚠️ Audits booked: 0/week (need to investigate)
- ⚠️ Sales conversion: <10% (qualification too loose?)
- ⚠️ PM proposals: None/week (no improvement identified?)
- ⚠️ Dev blocked: 1+ weeks (missing dependencies?)

**Red** (Immediate action):
- ❌ Content engagement: <20/post (wrong angle?)
- ❌ Network accept rate: <15% (poor targeting or personalization)
- ❌ Audits: No conversions 4+ weeks in (need to pivot)
- ❌ PM Agent not proposing (not analyzing data?)
- ❌ Dev Agent stuck (scope creep? unclear requirements?)
- ❌ Reporting Agent offline (email not arriving?)

---

## Failure Modes & Recovery

**If Content Engagement Drops**:
- Rich replies: "@ContentAgent try more opinion-based posts"
- Agent adjusts angle for next 3 posts
- Measure impact next week

**If Network Accept Rate Drops**:
- Rich replies: "@NetworkingAgent increase personalization, reference their recent activity"
- Agent updates approach immediately
- Should see improvement in 5-7 days

**If Audits Don't Convert**:
- Rich replies: "@AuditAgent change email angle, try softer CTA"
- Agent adjusts template for next batch
- PM may propose email nurture sequence feature

**If Dev Is Stuck**:
- PM Agent notices: "Dev started AIC-3 a week ago, PR not opened yet"
- PM checks in with Dev Agent
- Unblocks or adjusts scope with Rich's help

**If Heartbeat Deployment Fails**:
- Reporting Agent alerts in next email
- Rich approves rollback
- Dev Agent fixes bug
- PM Agent creates bug ticket (AIC-bug-1)

---

## Example: One Complete Week

**Monday 8 AM**: Content Agent posts (gets 45 reactions)
**Monday 11 AM**: Networking Agent sends 20 requests (8 accepted immediately)
**Monday 1 PM**: Sales Agent has 2 warm leads, sends qualification emails
**Monday 2 PM**: Audit Agent sends 12 offers

**Tuesday**: All agents continue daily cycles
...
**Friday 8 AM**: Content Agent posts
**Friday 5 PM**: Reporting Agent synthesizes week:

```
Content: 3 posts, avg 38 reactions (trending down from 45)
Network: 140 requests, 32% accept (on track)
Audits: 15 offers, 1 booked (slow, needs work)
Sales: 4 qualified leads, 0 demos yet
Research: Found 3 new case studies, AI budget shift trend
```

**Friday 6 PM**: Rich reviews email, replies:

```
@ContentAgent: Engagement down. Try the "here's why you're failing" angle.
@AuditAgent: Only 1 audit booked, try different email copy.
@SalesAgent: 0 demos with 4 qualified leads. Tighten qualification to budget-confirmed only.
```

**Saturday-Sunday**: Agents adjust for week 2

**Monday (Week 2)**: New cycle starts with adjustments

---

**Agent system**: Fully autonomous
**Rich's role**: Steering + Approval gates only
**Result**: Professional operation running on its own

---

Created: 2026-03-20
Status: All 8 agents documented and ready to deploy
