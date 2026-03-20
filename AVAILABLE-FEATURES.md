# AVAILABLE-FEATURES.md — Deployment Gate

This file tracks which merged PRs are ready to go live. Features sit in `main` branch until Rich marks them "ready to deploy" here.

**Heartbeat checks this file daily**: If a feature is marked "ready", it gets deployed to production automatically.

---

## How It Works

1. **Dev writes code** → Opens PR → Tests in staging
2. **Rich approves PR** → Dev merges to main
3. **Feature sits in main** (live code, not live traffic)
4. **Rich reviews staging** and decides: "Is this ready for real users?"
5. **If yes**: Mark "ready to deploy" in this file
6. **Heartbeat sees it** → Deploys to production
7. **Once live**: Move to "Recently Deployed"

---

## Ready to Deploy (Will go live on next heartbeat)

Nothing yet — awaiting first feature merge.

---

## In Development (Not yet ready for live traffic)

No features currently in development.

---

## Recently Deployed

No deployments yet.

---

## Deployment Checklist (Before Marking "Ready")

Before marking a feature "ready to deploy", confirm:

- [ ] **Code merged to main**: PR is merged, no pending changes
- [ ] **Tested in staging**: Feature works as expected in staging environment
- [ ] **Mobile-responsive**: Works on desktop, tablet, mobile
- [ ] **Load time acceptable**: Feature doesn't slow down site
- [ ] **Accessibility checked**: Basic contrast/keyboard navigation
- [ ] **Email templates reviewed**: If feature involves emails
- [ ] **Database migrations ready**: If feature requires DB changes (and tested in staging)
- [ ] **Rollback plan documented**: How to revert if something breaks
- [ ] **Rich has reviewed staging**: PM/Dev showed Rich the feature working
- [ ] **Impact clear**: We know what success looks like (metrics)

---

## Feature Format

When marking a feature ready:

```markdown
## Ready to Deploy
- [ ] AIC-1: Landing Page Redesign (merged, tested in staging, ready for real traffic)
```

## Recently Deployed Format

When a feature goes live:

```markdown
## Recently Deployed
- [x] AIC-1: Landing Page Redesign (deployed 2026-03-30 10:00 AM EDT)
  - Impact: Quiz completion 60% → 68%, +2 demos/week
  - Status: ✅ Successful, no rollback needed
```

---

## Timeline Example

### Week 1-2: Feature Development

**AIC-1: Landing Page Redesign** is in development.

```markdown
## In Development (Not yet ready for live traffic)
- [ ] AIC-1: Landing Page Redesign (PR open, Dev coding, staging in progress)
```

### Week 3: PR Merged, Staging Ready

```markdown
## In Development (Not yet ready for live traffic)
- [ ] AIC-1: Landing Page Redesign (PR merged, staged at staging.example.com, awaiting Rich review)
```

Rich reviews staging, likes it, gives thumbs up.

### Week 4: Marked Ready

```markdown
## Ready to Deploy (Will go live on next heartbeat)
- [ ] AIC-1: Landing Page Redesign (approved by Rich, ready for production)
```

### Week 4 (Next Heartbeat): Deployed

Heartbeat runs, sees AIC-1 is ready, deploys to production.

```markdown
## Recently Deployed
- [x] AIC-1: Landing Page Redesign (deployed 2026-04-06 08:00 AM EDT)
  - Impact: Quiz completion 60% → 68%, +2 demos/week
  - Status: ✅ Successful, monitors show normal operation
```

### Week 5+: Archive

Once feature has been live for 2+ weeks and performing well, move to archive.

```markdown
## Recently Deployed (Archived)
- AIC-1: Landing Page Redesign (deployed 2026-04-06, running smooth, no issues)
```

---

## Feature Status Definitions

### In Development
- **Definition**: Code being written, PR open or in review
- **Status in code**: Feature branch exists, not merged to main
- **User impact**: None (only in development)
- **Typical duration**: 1-2 weeks

### Ready to Deploy
- **Definition**: Merged to main, tested in staging, Rich approved
- **Status in code**: Merged to main, but not deployed to production
- **User impact**: None (only live users will see it after deployment)
- **Typical duration**: 1-7 days (waiting for Heartbeat or Rich decision)

### Recently Deployed
- **Definition**: Live on production, users can see it
- **Status in code**: Live, running in production
- **User impact**: Yes, affects real users and metrics
- **Duration**: 2+ weeks

---

## Rollback Plan

If a deployed feature causes issues:

1. **Heartbeat monitors**: Alert if metrics drop unexpectedly
2. **Rich decides**: "Should we rollback?"
3. **If yes**: Revert to previous version
4. **Document**: Update AVAILABLE-FEATURES.md with what went wrong and why

---

## Notes

- This file is the **single source of truth** for what's deployed vs. what's staged
- Heartbeat checks this file daily at 6 AM EDT
- Only features marked "ready to deploy" will be deployed
- Rich has full control — no feature goes live without his approval
- If unsure, leave feature in "In Development" — no harm in waiting

---

## Current Status

- **Total features in pipeline**: 0
- **Features in development**: 0
- **Features ready to deploy**: 0
- **Features live**: 0
- **Last deployment**: None (awaiting first feature)

---

**Created**: 2026-03-20
**Next update**: When first PR is merged
