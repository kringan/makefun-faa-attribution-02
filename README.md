# Polymarket FAA outage attribution forecaster

Forecasts the Yes price of each market of the FAA outage attribution family
at every minute of the 240 minutes after a checkpoint, as 5 quantiles
(0.05 / 0.25 / 0.5 / 0.75 / 0.95), scored by mean pinball loss.

Method: centre on the last price (no drift); sigma = RMS of 1-minute
changes over the last 120 minutes (floor 0.0005, cap 0.01); spread grows
as sigma * h^0.3; outer quantiles widened 1.6x for heavy-tailed jumps.

Practice score (NVIDIA event, 6 cases): 0.267107 vs house baseline 0.363589,
beating the baseline on all 6 cases. Python 3.13, stdlib only, no network,
deterministic.
