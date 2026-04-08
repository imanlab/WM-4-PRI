# Simultaneous Prediction of Optical and Tactile Sensation (SPOTS)

This repository contains the code and resources for the paper:

**World Model for Physical Robot Interactions: Simultaneous Visual and Tactile Predictions for Enhanced Accuracy**
*(Under review at Elsevier Robotics and Autonomous Systems – RAS)*

**Authors:** Willow Mandil, Amir Ghalamzan Esfahani

---

## 🚀 Quick Start

```bash
git clone https://github.com/imanlab/object_pushing_MarkedFrictionDataset.git
pip install -r requirements.txt
python3 format_data.py
python3 model_trainer.py
```

---

## Overview

Predicting outcomes of robot actions in **contact-rich environments** is a key challenge in robotics. Most existing approaches rely primarily on vision, neglecting the role of tactile sensing in understanding physical interactions.

This work introduces **SPOTS (Simultaneous Prediction of Optical and Tactile Sensations)**, a multi-modal world model that jointly predicts future visual and tactile observations.

### Key Insights

* Vision-only models perform well when physical properties are visually observable
* Tactile sensing becomes critical in physically ambiguous scenarios (e.g. friction differences)
* Multi-modal models improve long-horizon prediction accuracy

---

## Key Contributions

* Dual-pipeline multi-modal architecture (SPOTS) enabling simultaneous prediction of vision and touch
* Systematic comparison of fusion strategies (SVG, SVG-TE, SVTG, SPOTS)
* Two datasets for multi-modal physical interaction learning
* Analysis of when multi-modality provides benefit

---

## Method

We model interaction as a forward prediction problem:

$$
\hat{f}*{t:t+H} = F(f*{t-c:t}, x_{t-c:t}, a_{t:t+H})
$$

Where:

* (f): sensory observations (vision and tactile)
* (x): robot state
* (a): future actions

### Models

| Model  | Description                   |
| ------ | ----------------------------- |
| SVG    | Vision-only baseline          |
| SVG-TE | Vision conditioned on tactile |
| SVTG   | Single-pipeline multi-modal   |
| SPOTS  | Dual-pipeline multi-modal     |

---

## Robot Set up and Approach

<p align="center">
<img src="https://github.com/imanlab/WM-4-PRI/blob/master/assets/SPOTS_abstract_5_.jpg" width="500">
<p/>

## Datasets

Two datasets and their descriptions can be found at:

  - [Marked Friction Dataset](https://github.com/imanlab/object_pushing_MarkedFrictionDataset)
  - [Household Objects Dataset](https://github.com/imanlab/)

<p align="center">
<img src="https://github.com/imanlab/WM-4-PRI/blob/master/assets/data_collection_household.jpg" width="500">
<p/>

<p align="center">
  <img src="https://github.com/imanlab/WM-4-PRI/blob/master/assets/DatasetExampleLarge_.jpeg" width="500">
</p>

### Household Objects Dataset

* ~5,500 pushing trials
* Diverse objects
* Seen/unseen splits

### Visually Identical Dataset

* Same object, different friction
* Designed to isolate physical ambiguity

Download:

```bash
git clone https://github.com/imanlab/object_pushing_MarkedFrictionDataset.git
```

---

## Installation

### Requirements

* Python 3.8
* PyTorch, torchvision
* NumPy, SciPy
* OpenCV
* Matplotlib
* tqdm
* GPU recommended

```bash
pip install -r requirements.txt
```

---

## Data Formatting

```bash
python3 format_data.py
```

Specify:

* Context length
* Prediction horizon
* Output path
* Tactile format (vector/image)
* Image resolution

---

## Training

```bash
python3 model_trainer.py
```

Example:

```bash
python3 model_trainer.py \
  --model_name="SPOTS_SVG_ACTP" \
  --batch_size=32 \
  --epochs=100 \
  --device="cuda:0" \
  --model_save_path="/path/to/save/" \
  --train_data_dir="/path/to/data/" \
  --scaler_dir="/path/to/scaler/"
```

---

## Testing

```bash
python3 modester.py
```

Supports:

* Quantitative evaluation (MAE, PSNR, SSIM)
* Qualitative visualisation
* Tactile prediction analysis

---

## Key Findings

* Multi-modal models do not always outperform vision-only models
* Gains appear when physical properties are not visually observable
* SPOTS providmproved robustness and generalisation

---

## Repository Structure

```
├── models/
├── data_formatting/
├── training/
├── evaluation/
├── assets/
├── README.md
```

---

## Citation

```bibtex
@article{mandil2025spots,
  title={World Model for Physical Robot Interactions: Simultaneous Visual and Tactile Predictions for Enhanced Accuracy},
  author={Mandil, Willow and Ghalamzan-Esfahani, Amir},
  journal={Robotics and Autonomous Systems (under review)},
  year={2025}
}
```

---

## Acknowledgements

Supported by:

* UK Centre for Doctoral Training in Agri-Food Robotics (AgriFoRwArdS)

---

## License

MIT License

---

## Maintainers

* Willow Mandixcxcl 
* Amir Ghalamzan Esfahani – University of Sheffield – [a.ghalamzan@sheffield.ac.uk](mailto:a.ghalamzan@sheffield.ac.uk)


