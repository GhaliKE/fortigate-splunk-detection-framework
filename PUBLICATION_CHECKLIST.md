# Public release checklist

This checklist reflects the current public state of the repository. The
original report, presentation, generated files, and unverified figures are not
tracked or published.

- [x] No real organizational logs
- [x] No internal IP addresses
- [x] No internal hostnames
- [x] No customer names
- [x] No organizational usernames or email addresses
- [x] No internal Splunk URLs
- [x] No API keys, passwords, tokens, or secrets
- [x] No confidential screenshots
- [x] Only RFC 5737 addresses in examples
- [x] README results verified
- [x] 98.84% described only as investigation-volume reduction
- [x] Zero anomaly and zero outlier results preserved
- [x] No unsupported accuracy or detection-rate claims
- [x] Dashboards reviewed
- [x] SPL files reviewed
- [x] License reviewed
- [x] Final diff reviewed before publication
- [x] Git history checked for secrets before publication
- [x] Public contributors reviewed; only `GhaliKE` is currently listed
- [x] No social image published without an anonymized, cleared asset

## Intentionally excluded material

The original academic report, presentation, LaTeX sources, generated outputs,
and unverified figures are retained only in a local, Git-ignored backup. They
are not public release material.

Expected anonymized images are listed in [`images/README.md`](images/README.md).
No image is currently published because the available screenshots and
organizational graphics have not been independently cleared for release.

The optional `searches/synthetic_validation.spl` file was not present in the
source workspace and was not fabricated. Synthetic validation coverage is
provided by [`examples/synthetic_test_data.csv`](examples/synthetic_test_data.csv)
and [`searches/comparison_rules_ml.spl`](searches/comparison_rules_ml.spl).
The limitations summary is provided in
[`documentation/limitations.md`](documentation/limitations.md).

## Renames

| Original name | Public name |
|---|---|
| `dashboards/acces_sensibles.xml` | `dashboards/sensitive_access.xml` |
| `searches/fortigate_global_queries.spl` | `searches/global_monitoring.spl` |
| `searches/sensitive_access_queries.spl` | `searches/sensitive_access.spl` |
| `searches/ssh_threat_hunting_queries.spl` | `searches/ssh_threat_hunting.spl` |
| `searches/classification_actions.spl` | `searches/action_normalization.spl` |
| `searches/baseline_behaviorale.spl` | `searches/behavioral_baseline.spl` |
| `documentation/installation_and_reuse_guide.md` | `documentation/installation_guide.md` |
| `mappings/detection_framework_mapping.md` | `mappings/security_framework_mapping.md` |
| `results/current_results.md` | `results/reference_results.md` |
