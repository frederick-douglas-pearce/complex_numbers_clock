# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

An interactive analog clock that visualizes time as complex numbers using Pygame and Matplotlib. Clock hands are represented as complex number vectors with real/imaginary components and phase angles, displayed alongside real-time plots.

## Tech Stack

- **Python 3.10** with **Pipenv** for dependency management
- **Pygame** (pygame-ce) for the clock display window
- **Matplotlib** with `pygame_matplotlib` backend for embedding plots in the Pygame surface
- **Jupyter Notebook** (`complex_numbers_clock.ipynb`) — all code lives in a single notebook

## Setup & Running

```bash
pipenv install          # Install dependencies
pipenv run jupyter lab  # Launch JupyterLab, then run the notebook cells in order
```

## Architecture

The entire application is in `complex_numbers_clock.ipynb` with four main cells:

1. **Imports** — Sets matplotlib backend to `pygame_matplotlib.backend_pygame`
2. **Functions** — All display and math functions
3. **Parameters** — Configuration (start time, display options, screen ratios, colors)
4. **Main loop** — Pygame event loop that draws clock, digital time, and plots each frame

### Key Concepts

- **Clock hands as complex vectors**: Hour, minute, and second hands have a radius (magnitude) and theta (phase angle). Theta is measured counterclockwise from the real axis (3 o'clock position), then converted to principal value (-180°, 180°].
- **Coordinate system**: `polar_to_cartesian()` converts (r, theta) to screen coordinates where theta=0° is 12 o'clock on the display (rotated 90° from math convention).
- **Three display modes** controlled by `display_digital` and `display_plots` booleans:
  - Analog clock with Re/Im axes (always shown)
  - Digital time + complex number representation
  - Matplotlib plots of real/imaginary parts and phase angles over time
- **Time source**: Either real-time (`start_time = "now"`) or stepping from a fixed start time by `time_delta` increments each frame.
- **`clock_vals_dict`**: A `defaultdict(list)` accumulating all time series data (radii, angles, real/imag parts) across frames for plotting.

### Screen Layout

The screen splits into a left portion (clock) and right portion (digital display + plots) when `display_digital` or `display_plots` is enabled. The `clock_w_ratio` parameter controls the width split.
