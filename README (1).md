# OD Growth Curve Analyser

Small script I wrote to make sense of OD600 readings from a bacterial growth curve without having to eyeball a graph every time.

It takes a list of OD readings (one per hour) and:
- Classifies each hour into a growth phase (Lag / Log / Stationary-Decline) based on OD thresholds
- Prints out each hour with its OD value and phase
- Tracks the hour with the biggest jump in OD between consecutive readings (i.e. the fastest growth point)
- Prints a summary of how many hours fell into each phase, plus the max jump

## How it works

Phase is decided using simple thresholds:
- OD < 0.1 → Lag phase
- 0.1 ≤ OD < 1.0 → Log phase
- OD ≥ 1.0 → Stationary/Decline

These are just rough cutoffs, feel free to tweak them for your own data.

## Usage

Edit the `od_readings` list at the top of `analyse_od.py` with your own hourly OD values, then run:

```
python analyse_od.py
```

Example output:

```
Hour:  1 | OD = 0.05 | Lag phase
Hour:  2 | OD = 0.06 | Lag phase
Hour:  3 | OD = 0.09 | Lag phase
Hour:  4 | OD = 0.18 | Log phase
Hour:  5 | OD = 0.34 | Log phase
Hour:  6 | OD = 0.61 | Log phase
Hour:  7 | OD = 0.95 | Log phase
Hour:  8 | OD = 1.20 | Stationary/Decline
Hour:  9 | OD = 1.35 | Stationary/Decline
Hour: 10 | OD = 1.42 | Stationary/Decline
Hour: 11 | OD = 1.44 | Stationary/Decline
Hour: 12 | OD = 1.43 | Stationary/Decline

Phase Summary: {'Lag phase': 3, 'Log phase': 4, 'Stationary/Decline': 5}
Maximum Jump at Hour: 7 (Maximum Change in OD: 0.34)
```

## Requirements

Just Python 3, no external libraries needed.

## Notes

This was mainly for a quick personal analysis, so it's not built to handle messy input (missing values, non-numeric data, etc). Might extend it later to plot the curve with matplotlib.
