# Report Wave Final - Romain S. Journé

<div align="center">
  <img src="https://raw.githubusercontent.com/sejourneromain-eng/Report_Wave_final_Romain_S-journ-/main/ufrj-logo.png" alt="UFRJ Logo" width="420" />
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

## Abstract

This repository documents a research-oriented workflow for the automatic detection and characterization of wave dynamics from visual data. The project combines computer vision, deep learning, and geospatial data processing to extract informative frames from video sequences and train a YOLOv8-based model for object detection in coastal or oceanic scenes.

The objective is to build a reproducible pipeline for dataset preparation, model training, and inference analysis, with a focus on wave pattern recognition and risk assessment in marine environments.

---

## Research context

The workflow is designed for experimental analysis in the context of image-based coastal monitoring. It integrates:

- video acquisition from online sources and local storage,
- frame extraction and dataset curation,
- deep learning-based object detection,
- video annotation and visual interpretation,
- environmental and hydrodynamic reasoning through risk indicators.

This approach is relevant to applications such as coastal surveillance, marine observation, and automated analysis of wave behavior from remote visual sources.

---

## Repository structure

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
  Video acquisition script using YouTube download tools and automatic frame extraction for dataset generation.

- [code to create frame of a video in a drive](code%20to%20create%20frame%20of%20a%20video%20in%20a%20drive)  
  Extraction pipeline for videos already available on Google Drive, transforming them into image datasets.

- [Code to see the training](Code%20to%20see%20the%20training)  
  Model inspection and inference script used to visualize annotated detections and computed risk-related overlays.

- [Code to train the YOLOv8 AI](Code%20to%20train%20the%20YOLOv8%20AI)  
  Model training pipeline based on Ultralytics YOLOv8 and pretrained weights.

- [take data on Copernicus](take%20data%20on%20Copernicus)  
  Reference script or procedure for acquiring environmental or geospatial data from Copernicus-related sources.

---

## Methodology

### 1. Data acquisition

Video data are collected from external sources and stored in a structured project directory. The scripts are designed to operate in Google Colab and Google Drive environments, which facilitates large-scale processing and dataset storage.

### 2. Frame extraction and dataset preparation

The extraction process samples frames from the video stream at fixed intervals in order to reduce redundancy while preserving temporal coverage. This stage yields a curated image set suitable for supervised learning and visual analysis.

### 3. Model training

The training pipeline relies on YOLOv8, a state-of-the-art real-time object detection architecture. A pretrained `yolov8c.pt` model is used as a starting point, followed by transfer learning on the custom wave dataset.

Typical training configuration:

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

### 4. Inference and annotation

Once trained, the model is applied to new video sequences. Detection results are annotated directly on the frames, with visual overlays for object localization and risk assessment. This enables both qualitative inspection and quantitative monitoring of wave-related events.

---

## Scientific relevance

This project sits at the intersection of:

- computer vision,
- deep learning,
- coastal environment monitoring,
- hydrodynamic interpretation of image sequences.

It contributes to the development of low-cost and scalable visual analysis methods for marine observation and early detection of hazardous wave conditions.

---

## Technical dependencies

- Python 3.9+
- OpenCV (`cv2`)
- `yt-dlp`
- `ultralytics`
- Google Drive API / Drive integration
- Google Colab environment

Installation:

```bash
pip install yt-dlp
pip install ultralytics
pip install opencv-python
```

---

## Proposed workflow

1. Acquire video material from the selected source.
2. Establish the dataset structure under Google Drive.
3. Extract relevant frames with controlled temporal sampling.
4. Train the YOLOv8 model on labeled or weakly supervised data.
5. Perform inference on new sequences.
6. Validate detection quality and interpret wave behavior.
7. Refine model parameters and thresholds for improved robustness.

---

## Limitations and future work

- Dataset quality and annotation consistency remain critical factors for model reliability.
- The workflow may require domain-specific tuning to improve generalization across wave regimes and coastal scenes.
- Further integration with remote sensing products or Copernicus data could support more robust environmental interpretation.
- Additional quantitative metrics could be added to validate model performance more rigorously.

---

## Author

Romain S. Journé

## Institution

Universidade Federal do Rio de Janeiro (UFRJ)

## License

This repository is distributed for academic, research, and educational use. Reuse and adaptation are encouraged with appropriate attribution to the original project.
