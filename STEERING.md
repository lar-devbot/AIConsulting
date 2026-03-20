# STEERING.md — How Rich Directs Both Teams

Rich manages the AIConsulting operation through two simple steering mechanisms:
1. **Operations steering** via email replies to the daily Reporting Agent email
2. **Development steering** via email approvals of PM proposals + PR reviews

No complex dashboards, no approval loops (except content drafts). Everything is email-based.

---

## Operations Steering (Daily)

### How It Works

**5 PM**: Rich receives daily Reporting Agent email with operations metrics

**Example email**:
```
# AIConsulting Daily Report — 2026-03-27

## 📝 Content Agent
- Posts published: 2
- Engagement: 25 reactions/comments avg (target: 50)
- Issues: Engagement dropping week-over-week

## 🤝 Networking Agent
- Connections sent: 20
- Accept rate: 15% (target: 30%)
- DM responses: 1
- Issues: Accept rate declining

## 📋 Audit Agent
- Offers sent: 12
- Audits booked: 0
- Issues: No conversions yet

## 💼 Sales Agent
- Qualified leads: 0
- Demos booked: 0
- Issues: Too early (no leads yet)

## 🔧 Recommended Adjustments
1. Content Agent: Try more opinion-based posts, less news aggregation
2. Networking Agent: Increase personalization in connection requests
3. Audit Agent: Too early to judge; continue outreach

## ✋ Questions for Rich
Any steering changes for next 24 hours?
```

**If Rich wants to adjust agents**, he replies to this email:

```
Subject: RE: AIConsulting Daily Report — 2026-03-27

@ContentAgent: Agreed on the opinion posts. Let's do:
- Monday: "Here's why ChatGPT failed at customer support"
- Wednesday: "Why your AI project is going to fail (and how to fix it)"
- Friday: Proof point (case study or client success)

@NetworkingAgent: Accept rate dropping because we're not personalizing enough. 
Please reference their recent activity or company details in every connection request. 
Also stop targeting finance — focus only on SaaS + e-commerce for now.

@AuditAgent: Keep going. We should see conversions start week 4.

Everything else looks good.

Rich
```

### What Rich Can Steer

- **Content themes/angles**: "Do more X, less Y"
- **Network targeting**: "Focus on [industry], skip [industry]"
- **Qualification criteria**: "Only move to demo if they mention budget $20k+"
- **Audit offer frequency**: "Send fewer/more offers per day"
- **Email copy/tone**: "Make emails less formal" / "More personal"
- **Calendar availability**: "I can only do demos Tues/Wed 2-4 PM"
- **Overall priorities**: "Pause networking, focus on closing sales"

### What Agents Do With Steering

Agents pick up the reply and adjust for the next cycle:
- **Content Agent** immediately updates posting schedule + themes
- **Networking Agent** updates targeting + personalization approach
- **Audit Agent** updates offer frequency + email template
- **Sales Agent** updates qualification rubric
- Etc.

**No lag, no complex approval process** — agents implement changes the next day.

---

## Development Steering (Weekly/As-Needed)

### PM Proposal Workflow

**PM monitors daily operations data** (from Reporting Agent emails).

**When PM identifies an opportunity**, PM creates a Jira ticket + sends email proposal:

```
Subject: Proposal: Landing Page Redesign (AIC-1) — Improve Quiz Conversion

Hi Rich,

Data from this week shows:
- Quiz starts: 30 ✅
- Quiz completions: 18 (60%) ⚠️ — losing 12 leads
- Demos booked: 0

Problem: Quiz results don't clearly show "next steps." Users see results but don't know what to do.

PROPOSED SOLUTION: Landing Page Redesign
- Simplify value prop above fold
- Add progress bar (psychology)
- Redesign results screen with prominent "Book Audit" CTA
- Add testimonials for social proof

ESTIMATED IMPACT:
- Quiz completion: 60% → 70% (retain 3 more leads/week)
- Demos: 0 → 3-4/week (from improved conversion)
- Cost: $6k in dev time (40 hours)
- Value: 3 leads × $5k/month = $15k annual value
- ROI: 2.5x in month 1

TIMELINE: 2-3 weeks
APPROVAL NEEDED: Proceed?

Thanks,
PM
```

**Rich replies with approval or feedback**:

```
Subject: RE: Proposal: Landing Page Redesign (AIC-1) — Improve Quiz Conversion

Approved. Love the data.

One addition: "Guaranteed 7-month payback" messaging on the results screen.
That's our #1 differentiator.

Also, can you A/B test two CTA button colors (blue vs. green)?
Let's see what works better before we commit to one.

Create the Jira ticket and have Dev start when ready.

Rich
```

### PR Review Workflow

**Dev opens a PR** (example: `feature/AIC-1-landing-page-redesign`)

**Rich reviews the PR** and either:
1. **Approves to merge**: "Looks great. Merge when ready."
2. **Requests changes**: "Fix the typo in the CTA. Otherwise, approved."
3. **Rejects**: "This doesn't match the proposal. Let's discuss."

**Once merged**, feature sits in `main` (live code, but not yet deployed).

### Deployment Steering

**After PR is merged**, PM/Dev marks feature in AVAILABLE-FEATURES.md:

```markdown
## In Development (Not yet ready for live traffic)
- [x] AIC-1: Landing Page Redesign (PR merged, in staging)
```

**Rich reviews the staging version** and decides when to go live.

**When ready**, Rich updates AVAILABLE-FEATURES.md:

```markdown
## Ready to Deploy (Will go live on next heartbeat)
- [x] AIC-1: Landing Page Redesign (approved by Rich, ready for traffic)
```

**Heartbeat checks daily**: Are there features marked "ready"? Deploy them.

**Once deployed**, move to "Recently Deployed":

```markdown
## Recently Deployed
- [x] AIC-1: Landing Page Redesign (deployed 2026-03-30, +3 demos/week)
```

---

## Steering via Email (Examples)

### Example 1: Content Adjustment

```
Subject: RE: AIConsulting Daily Report — 2026-03-27

@ContentAgent: The "here's why you're failing" posts are getting 2x engagement vs. news aggregation.
Keep that going. Next week:
- Monday: "Why your AI project will fail (and how to prevent it)"
- Wednesday: "ChatGPT vs. agentic AI — why one works and one doesn't"
- Friday: Case study from this week's audit

Also try asking a question in the CTA to drive comments.

Rich
```

### Example 2: Network Targeting

```
Subject: RE: AIConsulting Daily Report — 2026-03-28

@NetworkingAgent: Accept rate improving but still below 30%. 
Increase personalization — every request should reference something specific about their company or recent activity.

Also, stop targeting finance & healthcare industries. Focus only on:
- SaaS (ops/founders)
- E-commerce (founders/CTOs)
- Professional services (managing partners)
NYC + US remote only.

This should fix the low accept rate.

Rich
```

### Example 3: Sales Tightening

```
Subject: RE: AIConsulting Daily Report — 2026-04-02

@SalesAgent: I see we have 8 qualified leads this week. Too many demos.

Going forward: Only move to demo if they explicitly mention budget $20k+.
Also, 2 demos per week max — I want quality conversations, not volume.

For the 8 leads we have: Prioritize the 2 with confirmed budget, skip the rest.

Rich
```

### Example 4: PM Proposal

```
Subject: RE: Proposal: Email Nurture Sequence (AIC-3) — Warm Up Cold Leads

Approved. This makes sense.

Budget: $8k in dev time (60 hours).
But run it by me before building — want to see the email copy first.

Create the Jira ticket and I'll review the email templates before Dev starts.

Rich
```

### Example 5: PR Approval

```
Subject: RE: PR #1 [AIC-1] Landing Page Redesign — Ready to Merge

LGTM. Two small fixes:
1. Line 142: "audits" should be "assessments" (brand consistency)
2. Blue button color #2563EB — make sure this is accessible (test contrast)

Once fixed, go ahead and merge. Ready to deploy to staging?

Rich
```

---

## Decision-Making Flow

### Operations (Daily)
```
Reporting Agent → Email to Rich (5 PM)
                ↓
Rich reviews (15 min) → Replies with steering (optional)
                ↓
Agents adjust for next 24h
```

### Development (Weekly)
```
PM monitors data → Creates Jira ticket → Sends proposal email
                                                ↓
                                        Rich approves (email)
                                                ↓
                                        Dev starts work → Opens PR
                                                ↓
                                        Rich reviews PR → Approves
                                                ↓
                                        Dev merges to main
                                                ↓
                                        Feature in staging
                                                ↓
                                        Rich marks "ready to deploy"
                                                ↓
                                        Heartbeat deploys to prod
```

---

## Key Principles

### 1. No Micromanagement
Rich doesn't approve every email, every post, every DM. He steers direction and adjusts course as needed.

### 2. Email Is The Interface
No dashboards, no complex tools. Everything happens via email replies.

### 3. Agents Are Smart
Once steered, agents execute without asking for permission at every step.

### 4. Data Drives Decisions
Every steering decision is based on metrics Rich sees in the daily report.

### 5. Fast Feedback Loop
Rich can adjust agents in hours; change is live by next day.

---

## Communication Channels

- **Daily operations**: Email from Reporting Agent (5 PM) ← Rich replies here
- **Weekly proposals**: Email from PM ← Rich approves here
- **PR reviews**: GitHub PR comments ← Rich approves here
- **Emergencies**: Direct email/message if something needs immediate attention

---

## Expected Rich Workload

- **Daily report review**: 15-30 minutes (5 PM)
- **Steering replies** (optional): 10-15 minutes if changes needed
- **PM proposal review**: 15-20 minutes when proposal arrives
- **PR reviews**: 15-30 minutes per PR
- **Total/week**: ~3-4 hours of oversight

---

**Steering mechanism**: Email-based, low-friction
**Deployed**: 2026-03-20
