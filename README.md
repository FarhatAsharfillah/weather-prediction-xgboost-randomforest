# Real-Time Pothole Detection: YOLOv11 vs CNN

![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)

##  Project Overview
This repository contains a comparative research study evaluating the performance of **YOLOv11** (a state-of-the-art one-stage object detector) against a baseline **CNN (MobileNetV2)** architecture for real-time pothole detection. The dataset utilizes a dynamic dashcam perspective (Field of View) to simulate real-world early warning systems in vehicles.

---

##  YOLOv11 Performance & Visualizations
YOLOv11 demonstrated superior spatial abstraction and robustness. The model's performance was evaluated through a precision-recall trade-off analysis over 50 epochs.

### 1. Precision, Recall, and F1-Score
<img width="2250" height="1500" alt="BoxF1_curve" src="https://github.com/user-attachments/assets/9c028415-52f8-439c-b050-407b6a6543f7" />
<img width="2250" height="1500" alt="BoxR_curve" src="https://github.com/user-attachments/assets/debe4f5c-fc94-413c-a49b-e92c32729776" />
<img width="2250" height="1500" alt="BoxPR_curve" src="https://github.com/user-attachments/assets/71f1879f-d4a0-47d0-b7b6-d522ca8c06cc" />
<img width="2250" height="1500" alt="BoxP_curve" src="https://github.com/user-attachments/assets/f2638bd3-ceba-4136-8a03-b8588d4287a2" />

* **PR Curve (mAP@0.5):** Achieved an Area Under Curve (AUC) of **0.702 (70.23%)**. The curve maintains stability above 0.8 precision at mid-recall ranges.
* **F1-Confidence Sweet Spot:** The optimal operational threshold is at **0.320 confidence**, yielding a peak **F1-Score of 0.69**. This is the recommended threshold for deployment to balance false positives (false alarms) and false negatives (missed detections).
* **P-Curve & R-Curve:** Reached absolute localization accuracy (1.00) at 0.887 confidence, with a maximum recall ceiling of 0.80.

### 2. Confusion Matrix (Class Separation)
<img width="3000" height="2250" alt="confusion_matrix_normalized" src="https://github.com/user-attachments/assets/f1ea10ef-f5c1-465b-a887-c72debb6a2e7" />
<img width="3000" height="2250" alt="confusion_matrix" src="https://github.com/user-attachments/assets/6e9441ca-7572-49ac-9178-e9d15d7610e3" />

* High concentration on the **True Positive** diagonal, proving accurate classification and localization of potholes.
* Moderate False Negatives and False Positives indicate strong model robustness against background noise and complex asphalt textures without triggering excessive false alarms.

### 3. Spatial Distribution & Depth Perception
<img width="1600" height="1600" alt="labels" src="https://github.com/user-attachments/assets/910c4593-e0ca-4dbb-abd7-0849718657c9" />

* Bounding boxes are heavily clustered in the center-to-lower quadrants of the canvas, perfectly representing a logical dashcam Field of View.
* The dominance of small-to-medium bounding boxes confirms the model successfully learned depth perception, recognizing distant road damages.

### 4. Training Convergence (Loss Metrics)
<img width="2400" height="1200" alt="results" src="https://github.com/user-attachments/assets/5431cfcf-25a7-483a-b3f8-a262f0a087ee" />

* Training over 50 epochs showed a smooth, exponential decrease across Box Loss, Class Loss, and DFL Loss.
* Synchronized validation loss confirms **healthy convergence without any signs of overfitting**.

---

## ⚠️ The CNN "Accuracy Paradox"
At first glance, the baseline CNN (MobileNetV2) achieved a **100.00% Validation Accuracy** and a 0.0001 Loss. However, empirical analysis revealed this as a critical anomaly caused by **extreme Class Imbalance**. 

Due to the lack of "empty asphalt" images in natural datasets, the CNN was forced to compare complex real-world pothole images against a small set of synthetic normal-road images. Despite implementing Class Weighting, the CNN suffered from severe overfitting—memorizing the binary differences between real and synthetic images rather than actually learning the morphology of road damages.

---

## 💡 Conclusion
For dashcam-perspective infrastructure damage detection—where object size, placement, and backgrounds are highly dynamic—a pure whole-image classification approach (CNN) is irrelevant and highly susceptible to negative data bias. 

**YOLOv11 is objectively superior.** With a **70.23% mAP** and excellent spatial abstraction capabilities, YOLOv11 provides a stable, rational, and deployment-ready architecture for vehicular early warning systems.

<img width="1920" height="1920" alt="val_batch2_pred" src="https://github.com/user-attachments/assets/31f16a5c-1392-43a1-af45-1bade8f74e01" />
<img width="1920" height="1920" alt="val_batch0_pred" src="https://github.com/user-attachments/assets/21e75a26-54d9-487a-8932-4d5f513ebb96" />
<img width="1920" height="1920" alt="val_batch1_pred" src="https://github.com/user-attachments/assets/8f4766d4-de5a-46f5-9c51-22f88ee85a8b" />
