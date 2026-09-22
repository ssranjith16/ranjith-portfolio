# AI-Powered Animal-Vehicle Collision Avoidance System

A computer-vision prototype for detecting animals on highways and generating collision-risk warnings using **YOLOv8**, monocular distance estimation, vehicle-speed monitoring, and multi-modal alerts.

## Features

- Real-time animal detection with YOLOv8
- Support for highway-relevant animal classes
- Basic IoU-based object tracking
- Monocular distance estimation using bounding-box height
- Time-to-Collision (TTC) calculation
- Risk levels: SAFE, CAUTION, WARNING, DANGER
- Visual warning overlays
- Optional audio alerts
- Optional Raspberry Pi GPIO buzzer/LED integration
- Speed monitoring with simulation support
- CSV/JSON session logging
- Camera calibration utilities
- Unit tests for detection and distance-estimation components

## Project Structure

```text
animal-vehicle-collision-avoidance/
├── main.py
├── train.py
├── config.py
├── setup.py
├── requirements.txt
├── data/
│   ├── indian_highway_animals.yaml
│   └── custom_dataset.yaml
├── models/
│   ├── detector.py
│   └── train.py
├── utils/
│   ├── alert_system.py
│   ├── camera_calibration.py
│   ├── data_logger.py
│   ├── distance_estimator.py
│   └── speed_monitor.py
└── tests/
    ├── test_detector.py
    └── test_distance.py
```

## Installation

Python 3.8+ is recommended.

```bash
python -m venv .venv
pip install -r requirements.txt
```

## Run

The application is designed to process a webcam or video source configured in `config.py`.

```bash
python main.py
```

## Training

The project includes YOLOv8 training scripts for an eight-class animal dataset: cow, buffalo, dog, nilgai, camel, elephant, horse, and goat.

```bash
python models/train.py --data dataset
```

Or:

```bash
python train.py
```

The dataset is intentionally excluded from this repository because image/label collections can be large.

## Distance and Collision Risk

Distance is estimated using triangle similarity:

```text
distance = (focal_length × real_object_height) / pixel_object_height
```

Time-to-Collision (TTC) is calculated from estimated distance and vehicle speed.

The thresholds in `config.py` are prototype parameters and should be calibrated and validated for the target camera, vehicle, and operating environment before any real-world safety use.

## Testing

```bash
python -m unittest discover -s tests -v
```

## Notes

Generated logs, output videos, virtual environments, caches, datasets, and model binaries are excluded from version control.

This is a research/prototype system and is not a certified automotive safety system or a substitute for validated vehicle safety controls.
