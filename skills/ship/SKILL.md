---
name: ship
description: Prepares a production launch. Use when deploying to production, or when asking what must be in place before shipping: a pre-launch checklist, monitoring, a staged rollout, or a rollback plan.
---

# Ship

## Overview

Ship with confidence. The goal is not just to deploy, it is to deploy safely, with monitoring in place, a rollback plan ready, and a clear understanding of what success looks like. Every launch should be reversible, observable, and incremental.

## When to use

- Deploying a feature to production for the first time.
- Releasing a significant change to users.
- Migrating data or infrastructure.
- Opening a beta or early access program.
- Any deployment that carries risk, which is all of them.

## The pre-launch checklist

### Code quality

- [ ] All tests pass (unit, integration, e2e).
- [ ] Build succeeds with no warnings.
- [ ] Lint and type checking pass.
- [ ] Code reviewed and approved.
- [ ] No TODO comments that should be resolved before launch.
- [ ] No `console.log` debugging statements in production code.
- [ ] Error handling covers expected failure modes.

### Security

- [ ] No secrets in code or version control.
- [ ] The ecosystem's dependency audit (`npm audit`, `pip-audit`, `cargo audit`, ...) shows no critical or high vulnerabilities.
- [ ] Input validation on all user-facing endpoints.
- [ ] Authentication and authorization checks in place.
- [ ] Security headers configured (CSP, HSTS, and the rest).
- [ ] Rate limiting on authentication endpoints.
- [ ] CORS configured to specific origins, not wildcard.

### Performance

- [ ] Core Web Vitals within "Good" thresholds.
- [ ] No N+1 queries in critical paths.
- [ ] Images optimized (compression, responsive sizes, lazy loading).
- [ ] Bundle size within budget.
- [ ] Database queries have appropriate indexes.
- [ ] Caching configured for static assets and repeated queries.

### Accessibility

- [ ] Keyboard navigation works for all interactive elements.
- [ ] Screen reader can convey page content and structure.
- [ ] Color contrast meets WCAG 2.1 AA (4.5:1 for text).
- [ ] Focus management correct for modals and dynamic content.
- [ ] Error messages are descriptive and associated with form fields.
- [ ] No accessibility warnings in axe-core or Lighthouse.

### Infrastructure

- [ ] Environment variables set in production.
- [ ] Database migrations applied, or ready to apply.
- [ ] DNS and SSL configured.
- [ ] CDN configured for static assets.
- [ ] Logging and error reporting configured.
- [ ] Health check endpoint exists and responds.

### Documentation

- [ ] README updated with any new setup requirements.
- [ ] API documentation current.
- [ ] Decision records written for any architectural decisions.
- [ ] Changelog updated.
- [ ] User-facing documentation updated, if applicable.

## Feature flag strategy

Ship behind feature flags to decouple deployment from release:

```typescript
const flags = await getFeatureFlags(userId);

if (flags.taskSharing) {
  return <TaskSharingPanel task={task} />;
}

// Default: existing behavior
return null;
```

Feature flag lifecycle:

```text
1. DEPLOY with flag OFF     -> Code is in production but inactive
2. ENABLE for team or beta  -> Internal testing in production
3. GRADUAL ROLLOUT          -> 5% -> 25% -> 50% -> 100% of users
4. MONITOR at each stage    -> Error rates, performance, user feedback
5. CLEAN UP                 -> Remove the flag and dead code after full rollout
```

Rules:

- Every feature flag has an owner and an expiration date.
- Clean up flags within two weeks of full rollout.
- Do not nest feature flags; it creates exponential combinations.
- Test both flag states (on and off) in CI.

## Staged rollout

The rollout sequence:

```text
1. DEPLOY to staging
   - Full test suite in staging
   - Manual smoke test of critical flows

2. DEPLOY to production (flag OFF)
   - Verify deployment succeeded (health check)
   - Check error monitoring (no new errors)

3. ENABLE for team (flag ON for internal users)
   - Team uses the feature in production
   - 24-hour monitoring window

4. CANARY rollout (flag ON for 5% of users)
   - Monitor error rates, latency, user behavior
   - Compare metrics: canary vs baseline
   - 24 to 48 hour monitoring window
   - Advance only if all thresholds pass

5. GRADUAL increase (25% -> 50% -> 100%)
   - Same monitoring at each step
   - Ability to roll back to the previous percentage at any point

6. FULL rollout (flag ON for all users)
   - Monitor for one week
   - Clean up the feature flag
```

Rollout decision thresholds:

| Metric | Advance (green) | Hold and investigate (yellow) | Roll back (red) |
| --- | --- | --- | --- |
| Error rate | Within 10% of baseline | 10 to 100% above baseline | More than 2x baseline |
| P95 latency | Within 20% of baseline | 20 to 50% above baseline | More than 50% above baseline |
| Client JS errors | No new error types | New errors under 0.1% of sessions | New errors over 0.1% of sessions |
| Business metrics | Neutral or positive | Decline under 5% (may be noise) | Decline over 5% |

Roll back immediately if:

- Error rate increases by more than 2x baseline.
- P95 latency increases by more than 50%.
- User-reported issues spike.
- Data integrity issues are detected.
- A security vulnerability is discovered.

## Monitoring and observability

What to monitor:

```text
Application metrics:
- Error rate (total and by endpoint)
- Response time (p50, p95, p99)
- Request volume
- Active users
- Key business metrics (conversion, engagement)

Infrastructure metrics:
- CPU and memory utilization
- Database connection pool usage
- Disk space
- Network latency
- Queue depth, if applicable

Client metrics:
- Core Web Vitals (LCP, INP, CLS)
- JavaScript errors
- API error rates from the client
- Page load time
```

Error reporting:

```typescript
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  componentDidCatch(error: Error, info: React.ErrorInfo) {
    reportError(error, {
      componentStack: info.componentStack,
      userId: getCurrentUser()?.id,
      page: window.location.pathname,
    });
  }

  render() {
    if (this.state.hasError) {
      return <ErrorFallback onRetry={() => this.setState({ hasError: false })} />;
    }
    return this.props.children;
  }
}

app.use((err: Error, req: Request, res: Response, next: NextFunction) => {
  reportError(err, {
    method: req.method,
    url: req.url,
    userId: req.user?.id,
  });

  // Do not expose internals to users
  res.status(500).json({
    error: { code: 'INTERNAL_ERROR', message: 'Something went wrong' },
  });
});
```

Post-launch verification, in the first hour:

```text
1. Health endpoint returns 200
2. Error monitoring shows no new error types
3. Latency shows no regression
4. The critical user flow works when tested manually
5. Logs are flowing and readable
6. The rollback mechanism works (dry run if possible)
```

## Error budget release gate

The service's error budget, the fraction of requests or time the SLO allows to fail, decides whether it is safe to ship. Use it as an objective gate, not a negotiation:

```text
Budget remaining over 20%   -> Ship normally; monitor closely
Budget remaining 0 to 20%   -> Slow rollouts only; no high-risk changes
Budget exhausted            -> Freeze feature work; focus on reliability
Budget resets               -> Resume normal pace; bake in the fix that recovered it
```

A high burn rate during a canary, consuming budget faster than the baseline pace, is a hold signal, treated the same as an elevated error rate.

## Rollback strategy

Every deployment needs a rollback plan before it happens:

```markdown
## Rollback plan for [feature/release]

### Trigger conditions
- Error rate more than 2x baseline
- P95 latency over [X]ms
- User reports of [specific issue]

### Rollback steps
1. Disable the feature flag, if applicable.
   OR
1. Deploy the previous version: `git revert <commit> && git push`
2. Verify the rollback: health check, error monitoring.
3. Communicate: notify the team of the rollback.

### Database considerations
- Migration [X] has a rollback: <verified command or runbook link>
- Data inserted by the new feature: [preserved / cleaned up]

### Time to rollback
- Feature flag: under 1 minute
- Redeploy previous version: under 5 minutes
- Database rollback: under 15 minutes
```

## Common rationalizations

| Rationalization | Reality |
| --- | --- |
| "It works in staging, it will work in production" | Production has different data, traffic patterns, and edge cases. Monitor after deploy. |
| "We do not need feature flags for this" | Every feature benefits from a kill switch. Even simple changes can break things. |
| "Monitoring is overhead" | Without monitoring you discover problems from user complaints instead of dashboards. |
| "We will add monitoring later" | Add it before launch. You cannot debug what you cannot see. |
| "Rolling back is admitting failure" | Rolling back is responsible engineering. Shipping a broken feature is the failure. |
| "The error rate looks fine, keep shipping" | Check the burn rate, not just the current rate. Consuming budget faster than baseline is a hold signal even when thresholds are green. |

## Red flags

- Deploying without a rollback plan.
- No monitoring or error reporting in production.
- Big-bang releases (everything at once, no staging).
- Feature flags with no expiration or owner.
- No one monitoring the deploy for the first hour.
- Production configuration done by memory, not code.
- "It is Friday afternoon, let us ship it."
- Error budget exhausted but feature work continues unchanged.

## Verification

Before deploying:

- [ ] Pre-launch checklist completed (all sections green).
- [ ] Feature flag configured, if applicable.
- [ ] Rollback plan documented.
- [ ] Monitoring dashboards set up.
- [ ] Team notified of the deployment.

After deploying:

- [ ] Health check returns 200.
- [ ] Error rate is normal.
- [ ] Latency is normal.
- [ ] Critical user flow works.
- [ ] Logs are flowing.
- [ ] Rollback tested, or verified ready.

For every shipped service:

- [ ] Error budget policy in place: know what action to take when budget drops below 20% and when it is exhausted.
