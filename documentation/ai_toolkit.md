# Splunk AI Toolkit

The model uses `DensityFunction` on `score_risque`. `fit` trains and stores
the model; `apply` evaluates new observations using that stored model.

- Training window: seven days
- Training granularity: one hour
- Aggregated training observations: 447,108
- Application window: four hours
- Application result: zero statistical outliers

The model complements explainable rules and does not replace analyst review.
