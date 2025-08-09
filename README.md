# Nose-Controlled Virtual Cursor

Hands-free mouse cursor control using your webcam. Tracks the nose tip with facial landmarks and detects eye blinks to trigger mouse clicks.

## Features

- Nose tip tracking (landmark #30) with on-frame green dot visualization
- Real-time cursor control mapped from camera to screen
- Blink detection using Eye Aspect Ratio (EAR) on landmarks 36–41
  - Single blink → single click
  - Double blink (within 0.4s) → double click
- On-screen overlays: blink status, EAR values, nose status, FPS, cursor info
- Adjustable EAR threshold via slider
- Pause/Resume with keyboard (P)

## Requirements

- Python 3.9+ (tested on 3.13)
- Windows/macOS/Linux desktop session

Install dependencies:

```bash
python -m venv .venv
.venv\\Scripts\\activate  # Windows PowerShell
# source .venv/bin/activate  # macOS/Linux
pip install -r requirements.txt
```

Model file (auto-download on first run):

- `shape_predictor_68_face_landmarks.dat` will be downloaded from `https://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2` and decompressed automatically if not present.
- If auto-download fails, download manually and place the `.dat` file in the project root.

## Usage

```bash
python main.py
```

Controls:

- P: Pause/Resume cursor movement
- Q or Esc: Quit
- Slider (Controls window): Adjust EAR threshold (0.10–0.40)

## Tips & Calibration

- Ensure your face is well lit and fully visible to the camera.
- Start with the default EAR threshold; adjust if false blinks or missed blinks occur.
- If movement is jittery, lower the smoothing alpha in `main.py` (`SMOOTHING_ALPHA`). Higher values are more responsive but less smooth.
- If cursor range feels inverted/wrong, remember the preview is mirrored; mapping uses normalized coordinates to screen space.

## Notes

- `pyautogui` may require accessibility permissions on macOS; grant when prompted.
- On Linux Wayland sessions, consider Xorg or additional permissions for global cursor control.
- If the webcam fails to open on Windows, try changing `CAM_INDEX` in `main.py` or using DirectShow backend already selected.

## License

MIT


