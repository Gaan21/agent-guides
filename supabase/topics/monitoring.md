# Monitoring and observability

For staging/production readiness and diagnosis. Preserve the operational review
and restore schedules below; calendar-neutral smoke checks do not replace them.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Hardening](hardening.md) |
| Performance diagnosis | [Performance](performance.md) |
| Deployment | [Deployment](deployment.md) |

## Operational review obligations

Review Security Advisor and Performance Advisor regularly; resolve critical findings
and investigate slow/high-call/high-total-time queries before proposing optimization.
Dashboard or authorized read-only inspection of pg_stat_statements/pg_stat_activity
can inform diagnosis; this is not permission for production tests or writes.

Monitor connections by service, idle/long-running queries, CPU/I/O, disk/growth,
cache hit ratios, scans/index use, request volume and function duration/errors.
Use lightweight structured logs with correlation IDs, status and duration. No PII,
tokens, secret keys or sensitive query/payload values; even key prefixes/hashes and
user IDs need a deliberate approved traceability policy, not automatic logging.

Configure owned alerts for high error rate, disk growth, pool exhaustion, recurring
slow queries and failed backups/disabled PITR. Thresholds must match project SLOs,
capacity and workload; example percentages are not verified platform requirements.
Record responders and the authorized inspection/incident plan.

Keep regular reviews: weekly advisors/slow queries, monthly access/key/capacity
review, and at least quarterly isolated restore testing. Retain stricter adopted
restore cadence. Check successful backups continuously; notify failures. Optional
Grafana/APM/uptime/log services require approved data handling and configuration.

Completion requires functioning alerts, advisor review, useful private logs and a
documented query/resource/backup inspection plan with named owners.
[Official observability](https://supabase.com/docs/guides/platform/metrics).
