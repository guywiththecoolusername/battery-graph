# battery-graph
battery graph :)

A single-file web app that turns raw battery event logs into an interactive timeline. Drop in one or more `.txt` logs, and it charts capacity, voltage and discharge rate, shades AC vs. battery periods, and calculates how your battery behaves **while charging**.
The logs are to be generated using BatteryInfoView v1.27 

Everything runs locally in your browser. Your logs are never uploaded anywhere.

## Features

- **Drag & drop upload**, with support for multiple logs at once
- **Interactive chart**: hover anywhere along the X axis (not just on the line) to see the exact time and value, with a crosshair that follows your cursor
- **Compare runs**: load several logs and overlay them on one chart, aligned by elapsed time since each log's start
- **Metrics**: switch between % Capacity, Voltage and Rate
- **AC / battery shading** on single-log views
- **Charging drop rate**: average %/hr change measured *only* during intervals where the state is "Charging"
- **Summary stats**: samples, duration, avg/min/max capacity, avg voltage, time on AC vs. battery
- **Raw events table** with CSV export
- **5 themes**: Phosphor, Midnight, Amber CRT, Synthwave and Paper (light). Your choice is remembered between visits.
- Handles both **UTF-8 and UTF-16** log files

## Usage

Its a simple website, download it or host it :)

## Log format

The parser reads blocks like this: (if your logs don't look similar to this, it may fail)

```
==================================================
Event Time        : 10/9/2026 3:29:32 PM
Power State       : AC Power
% Capacity        : 79.5%
Capacity Value    : 48,810
Rate              : 0
Voltage           : 16,651
Event Type        : Timer
==================================================
```

## How the charging rate is calculated

For every pair of consecutive samples where the first sample's power state contains "Charging", the app sums the change in `% Capacity` and the elapsed time, then divides:

```
avg %/hr while charging = total % change across charging intervals / total hours spent charging
```

- **Positive**: the battery is actually gaining charge, as expected
- **Negative**: the battery is still losing charge even though the laptop reports "Charging". This usually means the charger can't keep up with the system's power draw.

## Notes

- With multiple logs loaded, the X axis switches to elapsed time so separate test runs line up. AC/battery shading is only shown for a single log.
- Y axes auto-scale to the data so small changes stay visible.

## Credits

Claude, idk how to code
