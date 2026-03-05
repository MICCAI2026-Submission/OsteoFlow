# OsteoFlow: Lyapunov-Guided Flow Distillation for Predicting Bone Remodeling after Mandibular Reconstruction

This repository contains the reference implementation for **OsteoFlow**, a two-stage teacher–student pipeline for predicting **Year-1 post-operative CT** from **Day-5 CT** following mandibular reconstruction. The approach combines **diffeomorphic registration** and **rectified flow modeling** to learn bone remodeling dynamics at the graft–host interface. During training, a registration-based teacher provides trajectory guidance, while the student learns an **image-space transport field** regularized with an analytical Lyapunov constraint. At inference time, only the student model is required.

## Components

| Component | Role | Entry point |
|---|---|---|
| **Teacher (SVF)** | Diffeomorphic registration via stationary velocity fields (SVF) used to generate supervision trajectories during training | `Code/OsteoFlow_Teacher_V0.py` |
| **Student (Rectified Flow + Lyapunov)** | Image-space rectified flow trained via trajectory distillation with Lyapunov regularization and resection-aware loss | `Code/OsteoFlow_Student_V0.py` |

## Figures

The figures below correspond to the **Methods** and **Results** sections of the accompanying paper.

### Figure 1 (Methods)
![Figure 1](assets/figure1.png)

Preprocessing and the teacher–student distillation framework used to guide the student velocity field.

### Figure 2 (Results)
![Figure 2](assets/figure2.png)

Model predictions for three representative cases (union, partial union, and nonunion) visualized on the resection plane and two orthogonal central slices.

## Checkpoints and data

Pretrained checkpoints will be released and linked here.

The dataset used in this study is **internal and cannot be publicly distributed**. In case of acceptance, access requests can be directed to the **corresponding author**.

## Quickstart

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the teacher model:

```bash
python Code/OsteoFlow_Teacher_V0.py
```

Run the student model:

```bash
python Code/OsteoFlow_Student_V0.py
```

## Repository layout

```text
OsteoFlow/
│
├── README.md
├── requirements.txt
├── Code/
│   ├── OsteoFlow_Teacher_V0.py
│   └── OsteoFlow_Student_V0.py
│
├── assets/
│   ├── figure1.png
│   └── figure2.png
│
└── Results/
```

## Reproducibility notes

If you modify file paths, keep the directory names consistent under `BASE_DIR`. The teacher model is used only during training to guide the trajectory distillation process. Inference uses the student model alone, enabling fast prediction of Year-1 remodeling from Day-5 CT inputs.
