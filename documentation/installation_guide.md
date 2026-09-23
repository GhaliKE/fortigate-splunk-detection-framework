# Installation and reuse

## Prerequisites

- Splunk Enterprise or Splunk Cloud with the required search permissions.
- FortiGate traffic events exposing `srcip`, `dstip`, `dstport`, `service`,
  `action`, `sentbyte`, and `rcvdbyte` where available.
- Splunk AI Toolkit/MLTK for `fit`, `apply`, `listmodels`, and `summary`.

## Procedure

1. Copy the searches into a controlled Splunk knowledge-object workflow.
2. Replace the example `index=fortigate` and
   `sourcetype=fortigate_traffic` with approved target values.
3. Inspect the actual values of `action` and confirm the normalization mapping.
4. Import the three dashboards as private Classic XML dashboards.
5. Run the searches over a small test window and inspect field completeness.
6. Train the AI Toolkit model once over an approved historical window.
7. Verify the stored model, then use `apply` for new observations.
8. Calibrate thresholds with SOC analysts before production use.

Keep training and application searches separate. Restrict model and dashboard
permissions to the minimum required. Test execution cost, time ranges, and
field extraction in the target environment. Do not use organizational logs in
this public repository.
