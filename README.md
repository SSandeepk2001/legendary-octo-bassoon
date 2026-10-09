# Industrial Scrap Safety Detection with YOLO

A clean training and inference scaffold for object detection in industrial scrap imagery. The intended use is to help flag visible objects/hazards for human review—not to replace safety procedures or qualified inspectors.

> **Dataset and metrics:** No original annotated dataset or trained model weights are included. Add your authorized dataset and evaluate the model before reporting accuracy, mAP, or inspection-effort improvements. Resume figures must be supported by your actual experiment records.

## Features

- Ultralytics YOLO training entry point.
- Inference on an image or directory.
- Evaluation command for a trained checkpoint.
- Dataset YAML template and clear folder layout.
- Human-review disclaimer and data provenance notes.

## Setup

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# Linux/macOS: source .venv/bin/activate
pip install -r requirements.txt
```

## Dataset layout

Place images and YOLO-format label files in the following structure:

```text
dataset/
  images/
    train/
    val/
  labels/
    train/
    val/
```

Each label line must use `class_id x_center y_center width height` with normalized coordinates. Update `data.yaml` with your actual class names and dataset paths.

## Train

```bash
python src/train.py --data data.yaml --model yolov8n.pt --epochs 50 --imgsz 640
```

## Inference

```bash
python src/predict.py --weights runs/detect/train/weights/best.pt --source path/to/image-or-folder --output outputs
```

## Evaluate

```bash
python src/evaluate.py --weights runs/detect/train/weights/best.pt --data data.yaml
```

## Responsible use

- Test on a representative held-out dataset and report mAP50, mAP50-95, precision, recall, and per-class errors.
- Track false negatives carefully; missed hazards can be consequential.
- Treat model output as decision support. Human safety procedures and trained personnel remain authoritative.
- Do not upload identifiable, restricted, or proprietary facility images without authorization.

## Suggested results table

| Metric | Your measured result |
|---|---|
| Dataset version / split | Fill after experiment |
| Number of annotated images | Fill from dataset |
| Precision / Recall | Fill from evaluation |
| mAP@0.5 | Fill from evaluation |
| mAP@0.5:0.95 | Fill from evaluation |
| Inference hardware / latency | Fill after benchmarking |

Do not leave placeholder metrics in the final resume or claim results before running the experiment.
