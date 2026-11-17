# StrideAssist scripted trials - 3 trial(s) pooled

Files: P1_20261015_001242.csv, P2_20261015_002709.csv, P3_20261015_214624.csv

```
=== Table 1: gait-state classification ===
true \ predicted      normal  shuffle   freeze    still
normal                   268       24        0        0   recall 0.92
shuffle                    5      135       29        4   recall 0.78
freeze                     4        2       91        0   recall 0.94
still                      1        2        3      108   recall 0.95

windows=676  4-state accuracy=0.891
abnormal gait (shuffle or freeze): sensitivity=0.952 specificity=0.929
freeze detection latency over 6 episodes: mean 125 ms, max 750 ms (window-level resolution 750 ms)

=== Table 2: adaptive vs fixed cueing ===
mode     true state    windows   cue Hz  intensity
adaptive normal            175     1.19       0.34
adaptive shuffle           105     1.77       0.63
adaptive freeze             48     2.06       0.98
adaptive still              84     0.04       0.02
fixed    normal            117     1.00       0.50
fixed    shuffle            68     1.00       0.50
fixed    freeze             49     1.00       0.50
fixed    still              30     1.00       0.50

Adaptive cueing should rise from normal -> shuffle -> freeze and stop when still; fixed cueing should stay at 1.00 Hz / 0.50 throughout.
```

## SPINE link

| trial | windows | lost | bad frames | alarms | ACK median / max (ms) |
|---|---|---|---|---|---|
| P1_20261015_001242.csv | 288 | 0 | 0 | 66 | 73.5 / 76.7 |
| P2_20261015_002709.csv | 285 | 0 | 0 | 44 | 76.2 / 79.5 |
| P3_20261015_214624.csv | 280 | 0 | 0 | 41 | 72.3 / 75.5 |
