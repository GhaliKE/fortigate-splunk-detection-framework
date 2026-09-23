# Behavioral baseline

The baseline uses a 24-hour history window and 30-minute time buckets. It
tracks connection count and unique destinations per source, then calculates
the mean, standard deviation, and Z-score. A minimum Z-score of 3 and a
minimum volume of 10 connections are used in the reference configuration.

The tested period produced zero detected behavioral anomalies. This result is
not a claim that the environment contains no threats.
