# Filters

An augmented reality project that generates an interactive portal in the camera feed using real-time hand tracking. Through a natural gesture, the user can cycle through 8 different visual filters rendered live inside the portal.

---

## Features

- Real-time hand tracking using MediaPipe Hands.
- Perspective portal built dynamically from the index finger and thumb tips of both hands.
- Eight visual filters applied exclusively within the portal area.
- Filter switching via gesture: bringing the hands together triggers the transition to the next filter in the sequence.
- Hysteresis system to prevent accidental changes from tracking jitter or imprecision.

## Included filters

| Filter | Description |
|--------|-------------|
| `filter_grid` | Grid overlay on the original image |
| `filter_1` | Duotone segmented by luminosity thresholds |
| `filter_2` | Black-and-white dot pattern (halftone) |
| `filter_3` | Chromatic aberration with RGB channel separation |
| `filter_5` | Thermal camera simulation via colormap |
| `filter_6` | Vintage sepia style with vignette and grain |
| `filter_white` | Frosted glass effect over the image |
| `filter_pink` | Pink-magenta duotone halftone |

## Installation

Clone the repository:

```bash
git clone https://github.com/mishu006/Filters.git
cd Filters
```

Create a virtual environment:

```bash
python -m venv venv
```

Activate it:

```bash
venv\Scripts\activate      # Windows
source venv/bin/activate   # macOS / Linux
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

## Usage

```bash
python main.py
```

With the camera active, raise both hands with the index finger and thumb extended: the portal is generated automatically between them. Bring them together to "close" and advance to the next filter in the list. Press **`q`** with the window active to end execution.

## Project structure

```
Filters/
├── main.py             Entry point: capture loop and filter cycling
├── hand_tracking.py     Detection of extended fingers from the landmarks
├── geometry.py           Portal geometry and closing gesture detection
├── filters.py            Definition of the eight available filters
├── requirements.txt
└── README.md
```

## Extending the project

To add a new filter, simply define a function in `filters.py` that takes a crop in BGR format (`numpy.ndarray`) and returns a crop of the same size:

```python
def filter_new(roi: np.ndarray) -> np.ndarray:
    return roi
```

Then add it to the `FILTERS` list at the end of the file. The filter cycle adjusts automatically to the number of items in that list.

## Tech stack

- Python 3.10
- OpenCV
- MediaPipe
- NumPy

## License

This project is distributed under the MIT license.
