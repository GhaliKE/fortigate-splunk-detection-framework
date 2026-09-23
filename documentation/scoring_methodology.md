# Scoring methodology

The score prioritizes investigation and does not establish maliciousness.

| Component | Weight |
|---|---:|
| Firewall decision volume | 20 |
| Blocked connections | 20 |
| Blocking ratio | 30 |
| Unique destinations | 20 |
| Off-hours activity | 10 |

```text
blocked_connections /
(allowed_connections + blocked_connections) * 100
```

`allowed` maps to authorized, `block` or `blocked` maps to unauthorized,
`teardown` maps to session termination, and missing or unknown values map to
other. Teardown events are excluded from the denominator.

Risk levels are Low (0-29), Medium (30-59), High (60-79), and Critical
(80-100). The wide, balanced, and strict profiles use 20/10/70%, 50/25/80%,
and 100/50/90% minimum decisions/blocks/ratio respectively.

Thresholds should be recalibrated against local traffic and analyst capacity.
The repository contains no labeled ground truth, so no weight or threshold can
be interpreted as a validated detection-performance claim.
