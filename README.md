# StrideAssist trial data

This repository holds the data recorded with the StrideAssist ankle wearable for the paper:

A. Raj, K. Tyagi, V. Gupta, and S. Anandakumar, "StrideAssist: A Severity-Adaptive Tactile Gait-Cueing Ankle Wearable Implemented as a SPINE Body Sensor Network Node."

School of Computer Science and Engineering, Vellore Institute of Technology, Vellore, India.
Corresponding author: S. Anandakumar (s.anandakumar@vit.ac.in)

## What was recorded

Three healthy adult volunteers (P1, P2, P3) each did one scripted trial on 15 October 2026. The volunteers were the student authors, aged 21 to 22, and all gave verbal consent. The files hold no names or other personal details. Each walker is known only by a code.

The node was an ESP32 with an MPU6050 worn at the ankle. It sampled at 100 Hz and analysed a 1.5 s window of the acceleration magnitude about every 0.75 s. For each window it sent its features, the gait state it decided on and the cue it played to the laptop over the SPINE protocol through USB serial. The laptop recorded every window and labelled it with the task the walker had been asked to do.

Trial protocol (about 4 minutes):

| phase | task | true state | time (s) | cue mode |
|---|---|---|---|---|
| 0 | stand still | still | 15 | adaptive |
| 1 | calibration walk | (not labelled) | 12 | adaptive |
| 2 | walk normally | normal | 30 | adaptive |
| 3 | shuffle: short, quick, dragging steps | shuffle | 30 | adaptive |
| 4 | freeze: stop and tremble the leg in place | freeze | 15 | adaptive |
| 5 | walk normally | normal | 20 | adaptive |
| 6 | stand still | still | 12 | adaptive |
| 7 | walk normally | normal | 20 | fixed |
| 8 | shuffle | shuffle | 20 | fixed |
| 9 | freeze | freeze | 15 | fixed |
| 10 | walk normally | normal | 15 | fixed |
| 11 | stand still | still | 10 | fixed |

A window gets a true state only if it lies wholly inside one phase and starts at least 1 s after that phase began, to allow for the walker's reaction time. Other windows have an empty true_state and are not scored.

## Files

In `trials/`, for each trial `<walker>_<date>_<time>`:

| file | contents |
|---|---|
| `.csv` | one row per analysis window (columns below) |
| `.spine.log` | every SPINE packet sent (`>`) and received (`<`), with time in seconds, packet type, source and destination address, sequence number and payload in hex |
| `_link.json` | link summary: windows received and lost, bad frames, alarms, acknowledgment times |
| `_results.md` | scored tables for that trial |

`RESULTS.md` pools all three trials (676 scored windows). These are the numbers reported in the paper.

## CSV columns

| column | meaning |
|---|---|
| t_ms | node time at the end of the window, in ms |
| state | gait state decided on the node: 0 normal, 1 shuffle, 2 freeze, 3 still |
| severity | smoothed severity, 0 to 1 |
| inst_severity | severity of this window before smoothing, 0 to 1 |
| freeze_index | power in 3 to 8 Hz divided by power in 0.5 to 3 Hz |
| std_mg | standard deviation of the acceleration magnitude, in mg |
| range_mg | range of the acceleration magnitude, in mg |
| stride_iv_std | standard deviation of the stride intervals, in s |
| cue_hz | commanded tap rate, in Hz (the servo plays at most 2.0 Hz) |
| cue_level | cue strength, 0 to 1 |
| pattern | 0 no cue, 1 single tap, 2 freeze double tap |
| mode | A adaptive cueing, F fixed cueing (1.0 Hz at 50 %) |
| source | -1 means live sensor data (every row here is live) |
| calibrated | 1 after the calibration walk was done |
| true_state | task the walker was asked to do, same codes as state; empty if not scored |
| phase | protocol phase number from the table above |

## Notes

- The freeze latency in the results files is measured from the first scored freeze window. The paper reports the delay from the freeze instruction instead (1.5 s on average), which includes the 1 s reaction allowance and the window length.
- Windows were about 0.77 to 0.79 s apart during these trials, not exactly 0.75 s, because the node was also writing a log to its flash memory.
- The public Daphnet freezing-of-gait dataset used in the paper is not copied here. It is available from the UCI Machine Learning Repository (doi:10.24432/C56K78).

## Licence

The data are shared under the Creative Commons Attribution 4.0 licence (CC BY 4.0). Please cite the paper above if you use them.
