# Complex Numbers Clock

An interactive analog clock that represents clock hands as complex number vectors, serving as an intuitive introduction to complex numbers.

## Goal

Complex numbers can feel abstract. This project makes them tangible by mapping the familiar motion of clock hands to the complex plane. Each hand becomes a vector with a real component, an imaginary component, and a phase angle — all updated and visualized in real time.

## How It Works

The clock face is overlaid with real (horizontal) and imaginary (vertical) axes. As the hour and minute hands move, the application continuously decomposes each hand into its complex number representation and displays:

- **Analog clock** — A traditional clock face with Re/Im axes, tick marks for scale, and arrow-tipped hands
- **Digital time** — Standard digital time alongside the complex number form (e.g. `0.53+0.31i:0.00+0.74i`)
- **Time-series plots** — Matplotlib charts showing real/imaginary parts and phase angles of each hand over time

### Complex Number Mapping

Each clock hand is treated as a vector from the center of the clock:

- **Magnitude (r):** The length of the hand, normalized to the clock radius (hour ~0.61, minute ~0.74, second ~0.9)
- **Phase angle (θ):** Measured counterclockwise from the real axis (3 o'clock), converted to the principal value in (-180°, 180°]
- **Real part:** r·cos(θ)
- **Imaginary part:** r·sin(θ)

## Setup

Requires Python 3.10. Dependencies are managed with Pipenv.

```bash
pipenv install
pipenv run jupyter lab
```

Then open `complex_numbers_clock.ipynb` and run all cells in order. The Pygame window will appear with the clock.

## Configuration

Key parameters in the notebook's "Set parameters" cell:

| Parameter | Description |
|---|---|
| `start_time` | `"now"` for real time, or a fixed time like `"00:00:00"` |
| `time_delta` | How much time advances per frame (e.g. `{'minutes': 59}`) |
| `display_digital` | Show digital time and complex representation |
| `display_plots` | Show real/imag and phase angle plots |
| `display_seconds` | Show the second hand |
| `screen_ratio_w_h` | Window size as a fraction of display resolution |
| `clock_w_ratio` | Fraction of window width allocated to the clock |
| `fps` | Frames per second |

## Dependencies

- [pygame-ce](https://pyga.me/) — Clock display window
- [Matplotlib](https://matplotlib.org/) + [pygame-matplotlib](https://pypi.org/project/pygame-matplotlib/) — Embedded time-series plots
- [JupyterLab](https://jupyter.org/) — Notebook runtime
