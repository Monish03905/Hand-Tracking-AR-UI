# Hand Tracking AR UI

A futuristic AR interface that lives on your hand. A webcam tracks one hand with MediaPipe, and OpenCV draws a sci-fi HUD on top of it — radial gauges, concentric rings, tick marks, numeric readouts and a glowing core — that reacts to gestures.

![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-overlays-5C3EE8?logo=opencv&logoColor=white)
![MediaPipe](https://img.shields.io/badge/MediaPipe-Hands-0097A7)
![License](https://img.shields.io/badge/license-MIT-green)

## Features

- Real-time single-hand tracking with MediaPipe Hands.
- AR-style overlay anchored to the hand: glowing rings, 24 radial ticks, a stylised core and segmented HUD bars.
- Gesture-reactive modes — **open hand**, **pinch** and **fist** each change the interface.
- All graphics generated programmatically (no image assets).

## Stack

- Python 3.8+
- OpenCV
- MediaPipe (`mp.solutions.hands` — the legacy Solutions API)
- NumPy

## Install and run

```bash
git clone https://github.com/Monish03905/Hand-Tracking-AR-UI.git
cd Hand-Tracking-AR-UI

python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate

pip install -r requirements.txt
python main.py
```

Allow webcam access, hold one hand in frame, and switch gestures to see the HUD change.

## How it works

```text
frame → MediaPipe Hands → 21 landmarks
      → palm centre + hand span (radius)
      → gesture check (fingertip extension / pinch distance / fist)
      → draw glow circle, radial ticks, core pattern, HUD blocks
      → composite over the camera feed
```

`main.py` contains the drawing helpers (`draw_glow_circle`, `draw_radial_ticks`, `draw_core_pattern`, `draw_hud_details`) and the capture loop.

## Requirements file

```text
opencv-python
mediapipe
numpy
```

This project uses the legacy `mediapipe.solutions` API. If a newer MediaPipe release no longer ships it, install a version that still does, for example `mediapipe==0.10.14`.

## Troubleshooting

- **No detection** — improve lighting, show the palm to the camera, keep the hand ~40–80 cm away.
- **Lag** — close background apps; lower the capture resolution in `main.py`.
- **Import error on newer MediaPipe** — install the pinned versions from `requirements.txt` (0.10.14).
- **Wrong camera** — change the index in `cv2.VideoCapture(0)` in `main.py`.
- **Exit** — press `q` or `Esc` in the camera window.

## License

MIT — see [LICENSE](LICENSE).
