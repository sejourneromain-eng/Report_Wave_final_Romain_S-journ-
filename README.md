# Report Wave Final - Romain S. Journé

<div align="center">
  <img src="https://www.ufrj.br/wp-content/themes/ufrj/images/logo-ufrj.png" alt="UFRJ Logo" width="240" />
</div>

<p align="center">
  <img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/sejourneromain-eng/Report_Wave_final_Romain_S-journ-" />
  <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/sejourneromain-eng/Report_Wave_final_Romain_S-journ-" />
  <img alt="GitHub language count" src="https://img.shields.io/github/languages/count/sejourneromain-eng/Report_Wave_final_Romain_S-journ-" />
  <img alt="GitHub top language" src="https://img.shields.io/github/languages/top/sejourneromain-eng/Report_Wave_final_Romain_S-journ-" />
</p>

<p align="center">
  <a href="https://github.com/sejourneromain-eng/Report_Wave_final_Romain_S-journ-">
    <img alt="GitHub Repository" src="https://img.shields.io/badge/GitHub-Repository-181717?logo=github&logoColor=white" />
  </a>
</p>

This project focuses on wave detection and analysis from video sequences using computer vision and YOLOv8. It includes scripts for downloading video content, extracting frames, creating datasets, training a model, and evaluating wave-related risk indicators.

## Overview

The repository contains tools for:

- downloading video data from YouTube,
- extracting frames from videos stored locally or in Google Drive,
- preparing a dataset for training,
- training a YOLOv8 model,
- running inference on video streams,
- displaying annotated results and risk-related statistics.

This work is designed for a research and prototype pipeline related to coastal or ocean wave monitoring.

---

## Project structure

```text
Report_Wave_final_Romain_S-journ-
├── README.md
├── Code to create frame of a video youtube.md
├── code to create frame of a video in a drive
├── Code to see the training
├── Code to train the YOLOv8 AI
├── take data on Copernicus
└── .git/
```

### File descriptions

- [Code to create frame of a video youtube.md](Code%20to%20create%20frame%20of%20a%20video%20youtube.md)  
  Downloads a video from YouTube, saves it in Google Drive, and extracts frames at a fixed interval.

- [code to create frame of a video in a drive](code%20to%20create%20frame%20of%20a%20video%20in%20a%20drive)  
  Opens a video already stored in Google Drive and saves frames into a dataset folder.

- [Code to see the training](Code%20to%20see%20the%20training)  
  Demonstrates model loading, inference, object detection, and annotated output generation.

- [Code to train the YOLOv8 AI](Code%20to%20train%20the%20YOLOv8%20AI)  
  Contains the YOLOv8 training workflow using Ultralytics and a pre-trained model.

- [take data on Copernicus](take%20data%20on%20Copernicus)  
  Used for gathering environmental or geospatial data, including Copernicus data access workflows.

---

## Workflow

1. Collect or download video data.
2. Extract frames from the video at a chosen interval.
3. Store the resulting frames in a drive or dataset folder.
4. Train a YOLOv8 model with the prepared dataset.
5. Run inference on new videos.
6. Visualize detections and risk indicators.

---

## Main technical components

### 1. Frame extraction from YouTube

The script in [Code to create frame of a video youtube.md](Code%20to%20create%20frame%20of%20a%20video%20youtube.md) includes:

- `yt-dlp` to download the video,
- Google Drive integration,
- automatic folder creation,
- frame extraction every `FRAME_INTERVAL` frames.

Typical parameters:

- `URL_YOUTUBE`
- `DRIVE_PROJECT_FOLDER`
- `DESTINATION_IMAGES_FOLDER`
- `FRAME_INTERVAL`

### 2. Frame extraction from Drive

The script [code to create frame of a video in a drive](code%20to%20create%20frame%20of%20a%20video%20in%20a%20drive) uses OpenCV to:

- read a local or mounted video,
- iterate over frames,
- save JPEG images in a target directory,
- create the output folder if needed.

### 3. YOLOv8 training

The script [Code to train the YOLOv8 AI](Code%20to%20train%20the%20YOLOv8%20AI) contains the core training flow with:

- installation of `ultralytics`,
- Google Drive mounting,
- use of a pretrained `yolov8c.pt` model,
- dataset YAML configuration,
- model output saved to a project folder.

Example:

```bash
!yolo train \
  model=yolov8c.pt \
  data=/content/drive/MyDrive/Project_Yolo_v9/Waveproject.yaml \
  project=/content/drive/MyDrive/Wave/Project \
  name=train \
  epochs=75 \
  batch=10 \
  imgsz=640 \
  save=True
```

### 4. Inference and result visualization

The script [Code to see the training](Code%20to%20see%20the%20training) demonstrates:

- loading a trained model,
- processing a video frame by frame,
- drawing detection boxes,
- computing wave-related metrics,
- displaying a global risk status overlay.

---

## Dependencies

- Python 3.9+
- OpenCV (`cv2`)
- `yt-dlp`
- `ultralytics`
- Google Drive
- Google Colab (recommended for this workflow)

Install the main packages with:

```bash
pip install yt-dlp
pip install ultralytics
pip install opencv-python
```

---

## Usage example

1. Open the project in Google Colab.
2. Mount your Google Drive.
3. Download or load the source video.
4. Extract frames to a dedicated dataset folder.
5. Train the YOLOv8 model.
6. Apply the model to a new video sequence.
7. Review annotated outputs and detection metrics.

---

## Notes

- This project is intended as a research and prototype pipeline.
- Drive paths must be adapted to the real folder structure in your environment.
- Model parameters, frame intervals, and risk thresholds may need adjustment depending on the dataset and use case.

---

## Author

Romain S. Journé

## Institution

Universidade Federal do Rio de Janeiro (UFRJ)

## License

This repository is shared for academic and demonstration purposes. Please cite the original work when reusing or adapting the material.
