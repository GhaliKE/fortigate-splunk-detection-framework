# Public release checklist

- [ ] No real organizational logs
- [ ] No internal IP addresses
- [ ] No internal hostnames
- [ ] No customer names
- [ ] No usernames or email addresses
- [ ] No internal Splunk URLs
- [ ] No API keys, passwords, tokens, or secrets
- [ ] No confidential screenshots
- [ ] Only RFC 5737 addresses in examples
- [ ] README results verified
- [ ] 98.84% described only as investigation-volume reduction
- [ ] Zero anomaly and zero outlier results preserved
- [ ] No unsupported accuracy or detection-rate claims
- [ ] Dashboards reviewed
- [ ] SPL files reviewed
- [ ] License reviewed
- [ ] Final diff reviewed before commit
- [ ] Git history checked for secrets before push

## Deferred publication items

The original academic report, presentation, LaTeX sources, generated outputs,
and unverified figures are retained in `_local_backup/originals/` and are not
public release material.

Expected anonymized images are listed in [`images/README.md`](images/README.md).
No image is currently published because the available screenshots and
organizational graphics have not been independently cleared for release.

The following requested artifacts were not present in the source workspace and
were not fabricated: `searches/synthetic_validation.spl` and
publication-ready anonymized screenshots. The limitations summary is provided
in `documentation/limitations.md`.

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
