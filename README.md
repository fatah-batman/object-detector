# Object Detector

Real-time object detection from your webcam using [YOLOv10](https://github.com/THU-MIG/yolov10) through the [Ultralytics](https://docs.ultralytics.com/) library, with OpenCV for video display and [cvzone](https://github.com/cvzone/cvzone) for labels.

Each detected object is outlined with a bounding box and labeled with its class name and confidence score.

## Features

- Live webcam capture with OpenCV
- Object detection with the pretrained `yolov10n.pt` model
- Bounding boxes and labels with confidence percentages
- Press `Esc` to close the window and release the camera

## Requirements

- Python 3.9 or newer
- A webcam
- macOS, Linux, or Windows (the camera permission steps below are for macOS)

## Installation

1. Clone the repository and go into the project folder:

   ```bash
   git clone https://github.com/<your-username>/object-detector.git
   cd object-detector
   ```

2. Create and activate a virtual environment:

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate   # macOS / Linux
   .venv\Scripts\activate      # Windows
   ```

3. Install the dependencies:

   ```bash
   pip install ultralytics opencv-python cvzone
   ```

4. Make sure `yolov10n.pt` is in the project folder. The first run downloads it automatically if it's missing. You can also download it from the [YOLOv10 releases](https://github.com/THU-MIG/yolov10/releases).

## Usage

Run the script from the project folder:

```bash
python main.py
```

A window titled **frame** opens and shows the webcam feed with detections drawn on it.

### Controls

| Key   | Action                               |
| ----- | ------------------------------------ |
| `Esc` | Close the window and stop the camera |

The video window needs focus for key presses to register, so click on it before pressing `Esc`.

## macOS Camera Permissions

If you see `not authorized to capture video` or `camera failed to properly initialize`:

1. Go to **System Settings → Privacy & Security → Camera**.
2. Enable the toggle for the app you run Python from, such as Terminal, iTerm, Cursor, or VS Code.
3. Fully quit and reopen that app, then run the script again.

If the app isn't listed, reset the permission prompt with `tccutil reset Camera` and run the script again.

## Project Structure

```
object-detector/
├── main.py          # Webcam capture and object detection loop
├── yolov10n.pt      # YOLOv10 nano model weights
├── .venv/           # Local virtual environment (not committed)
├── .gitignore
└── README.md
```

## How It Works

1. `cv2.VideoCapture(0)` opens the default webcam.
2. Each frame is passed to the YOLO model, which returns detected objects and their bounding boxes.
3. For each box, the script draws a rectangle with OpenCV and writes the class name and confidence with `cvzone.putTextRect`.
4. The annotated frame is shown in a window until `Esc` is pressed.

## Troubleshooting

- `Could not open webcam`: Check camera permissions, and make sure no other app (such as Zoom or FaceTime) is using the camera.
- `Failed to read frame from webcam`: The camera disconnected or another app took control of it. Restart the script.
- `Slow or laggy video`: The model runs on each frame. A GPU speeds it up considerably. On a CPU, expect a lower frame rate.
