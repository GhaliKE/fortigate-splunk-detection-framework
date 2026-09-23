# Data quality

Field completeness is the percentage of assessed events in which a field is
populated. It does not guarantee that populated values are accurate.

The reference assessment covered 12,474,308 events:

| Field | Completeness |
|---|---:|
| `srcip` | 99.18% |
| `dstip` | 99.18% |
| `dstport` | 96.84% |
| `action` | 95.67% |
| `service` | 92.81% |

Deployments should repeat the assessment after onboarding a new FortiGate
source, sourcetype, or parser.
