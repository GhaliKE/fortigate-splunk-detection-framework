# FortiGate / Splunk Detection and Risk Prioritization Framework

## Project overview

This project is an explainable monitoring and risk-prioritization framework
built with Splunk SPL for FortiGate traffic logs. It combines firewall action
normalization, weighted risk scoring, configurable noise reduction, behavioral
analysis, and statistical anomaly detection to help analysts prioritize network
sources for investigation.

The framework operates in read-only Shadow Mode. It does not perform automatic
blocking, infrastructure modification, or automatic incident creation.

## Problem statement

Raw firewall telemetry is high-volume and mixes authorized traffic, denied
connections, session termination events, and incomplete fields. Analysts need
an auditable way to reduce investigation volume without presenting a heuristic
score as proof of compromise.

## Architecture

```text
FortiGate logs
  -> Splunk indexing
  -> action normalization
  -> aggregation and indicator calculation
  -> weighted scoring
  -> threshold filtering
  -> dashboards
  -> analyst investigation
```

Supporting components cover data quality, behavioral baselines, Splunk AI
Toolkit, security-framework mapping, and Detection Pack documentation. See
[`documentation/architecture.md`](documentation/architecture.md).

## Key features

- Global FortiGate traffic monitoring
- Sensitive access monitoring for SSH, RDP, SMB, and SSL/VPN
- SSH threat hunting
- Firewall action normalization
- Explainable risk scoring normalized to 100
- Configurable wide, balanced, and strict noise-reduction profiles
- Behavioral baselines using Z-scores
- Splunk AI Toolkit `DensityFunction` integration
- FortiGate field-completeness assessment
- Synthetic validation using RFC 5737 documentation addresses
- MITRE ATT&CK, NIST CSF, and CIS Controls mapping

## Dashboard overview

Import the XML files in [`dashboards/`](dashboards/) as Classic XML
dashboards. The global dashboard summarizes volume and actions; the sensitive
access dashboard prioritizes remote-service activity; and the SSH dashboard
supports deeper threat hunting. No screenshot is included until it has been
independently anonymized; the expected image set is documented in
[`images/README.md`](images/README.md).

## Firewall action normalization

| Raw action | Normalized meaning |
|---|---|
| `allowed` | `authorized` |
| `block` or `blocked` | `unauthorized` |
| `teardown` | session termination |
| missing or unknown | `other` |

`teardown` events are excluded from the blocking ratio because they are not
treated as firewall denial decisions equivalent to `block`.

```text
blocking_ratio =
  blocked_connections /
  (allowed_connections + blocked_connections) * 100
```

## Explainable risk scoring

The reference score is designed for investigation prioritization:

- Firewall decision volume: 20 points
- Blocked connections: 20 points
- Blocking ratio: 30 points
- Unique destinations: 20 points
- Off-hours activity: 10 points

Risk levels are Low (0-29), Medium (30-59), High (60-79), and Critical
(80-100). The score is designed to prioritize investigation. It does not prove
that a source is malicious.

## Noise-reduction methodology

The profiles are configurable filters applied before investigation:

| Profile | Decisions | Blocks | Blocking ratio | Calibration result |
|---|---:|---:|---:|---:|
| Wide | 20 | 10 | 70% | 119 retained |
| Balanced | 50 | 25 | 80% | 74 retained |
| Strict | 100 | 50 | 90% | 46 retained |

The balanced profile is the reference configuration. The difference between 74
sources in calibration and 81 in the live measurement reflects executions at
different times on continuously ingested data.

## Behavioral baseline

The baseline uses a 24-hour history window, 30-minute buckets, connection count
and unique destinations, and mean/standard-deviation Z-scores. The minimum
anomaly threshold is 3 and the minimum volume is 10 connections. Zero
behavioral anomalies exceeded the selected threshold during the tested period.

## Splunk AI Toolkit

`DensityFunction` is applied to the `score_risque` feature. The model is
trained (`fit`) over seven days at one-hour granularity and stores 447,108
aggregated observations. `apply` evaluates new observations over a four-hour
window. Zero statistical outliers were identified during the application
period. This means recent scores remained consistent with the learned
distribution; it does not mean that risk was absent.

## Data-quality assessment

The field-completeness assessment covered 12,474,308 events:

- `srcip`: 99.18%
- `dstip`: 99.18%
- `dstport`: 96.84%
- `action`: 95.67%
- `service`: 92.81%

Field completeness measures whether a field is populated. It does not
guarantee that the value is accurate. See
[`documentation/data_quality.md`](documentation/data_quality.md).

## Synthetic validation

[`examples/synthetic_test_data.csv`](examples/synthetic_test_data.csv) uses
only RFC 5737 addresses. It exercises normal traffic, a high-volume SSH scan,
intermediate suspicious activity, and teardown-heavy traffic. This validates
the engine logic; it does not measure performance on real incidents.

## Reference results

The reference live measurement analyzed 6,979 network sources during four
hours. 81 sources matched the balanced prioritization criteria, while 6,898
were removed from the priority investigation list: a 98.84% reduction in
investigation volume. The field-completeness assessment included 12,474,308
events. The AI Toolkit used a seven-day training period, one-hour aggregation,
and 447,108 aggregated training observations. Zero behavioral anomalies and
zero statistical outliers were observed; drift was stable.

**The 98.84% value represents a reduction in investigation volume. It is not a
detection rate, an accuracy score, a precision measurement, a recall
measurement, or a false-positive rate.**

A prioritized source is not automatically confirmed as malicious. Human
investigation and additional context remain necessary. See
[`results/reference_results.md`](results/reference_results.md).

## Repository structure

```text
dashboards/       Splunk Classic XML dashboards
searches/         Reusable SPL searches
documentation/    Architecture, methods, operations, and limitations
mappings/         Security framework mappings
results/          Reference measurements
examples/         Fully synthetic validation data
images/           Anonymized publication-image requirements
```

## Installation and reuse

Read [`documentation/installation_guide.md`](documentation/installation_guide.md)
before adapting the searches. Set the target index and sourcetype for the
destination environment, confirm action values, import the dashboards, and
test searches in a non-production context. Train the AI Toolkit model
separately before using `apply`; permissions and performance requirements are
environment-specific.

## Security and privacy

Do not submit organizational logs, internal addresses, hostnames, usernames,
URLs, credentials, tokens, or unredacted screenshots. Use synthetic data and
review the checklist in [`PUBLICATION_CHECKLIST.md`](PUBLICATION_CHECKLIST.md).
Report accidental exposure privately to the repository maintainer rather than
opening a public issue.

## Limitations

There is no labeled ground truth, accuracy/precision/recall/F1 measurement, or
claim of production detection performance. The weights are heuristic, the
thresholds are environment-specific, the historical period is limited, and
the statistical model is univariate. The framework performs no automatic
blocking or incident creation and cannot replace contextual human review. See
[`documentation/limitations.md`](documentation/limitations.md).

## Future improvements

Potential extensions include labeled validation data, multivariate baselines,
calibration by environment, richer asset context, and controlled feedback
from analyst outcomes.

## Author

This repository is a public technical portfolio and reusable Detection Pack.
Add maintainer attribution here when publishing the repository.

## License

Released under the MIT License; see [`LICENSE`](LICENSE).

FortiGate, Fortinet, Splunk, MITRE, NIST, and CIS are trademarks or names of
their respective owners. This project is independent and is not affiliated
with or officially endorsed by them.

## Disclaimer

This material is provided for educational and defensive engineering purposes.
Validate queries, permissions, data handling, and thresholds in the target
environment before use.
