# Architecture

```text
FortiGate logs
  -> Splunk indexing
  -> action normalization
  -> aggregation
  -> indicator calculation
  -> weighted scoring
  -> threshold filtering
  -> dashboards
  -> analyst investigation
```

Data-quality assessment, a behavioral baseline, Splunk AI Toolkit, security
framework mapping, and Detection Pack documentation provide complementary
controls. The framework remains read-only Shadow Mode: it does not block
traffic or create incidents automatically.
