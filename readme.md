# 🚀 Spam Detection using MLOps | DVC • DVCLive • AWS S3

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![DVC](https://img.shields.io/badge/DVC-Data%20Version%20Control-purple)
![AWS S3](https://img.shields.io/badge/Storage-AWS%20S3-orange)
![DVCLive](https://img.shields.io/badge/Tracking-DVCLive-yellowgreen)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 🧩 Project Overview

This repository demonstrates a **complete MLOps workflow** for a **Spam Detection System** built using **Data Version Control (DVC)**, **DVCLive**, and **AWS S3**.

It showcases how to:
- Version control data, models, and experiments
- Automate ML pipelines using DVC
- Track metrics and experiments using DVCLive
- Use AWS S3 as a remote storage for scalable artifact management
- Maintain full reproducibility and transparency in the ML lifecycle

---

## 🧠 Objective

To implement an **end-to-end, reproducible, and automated MLOps pipeline** for spam message classification that adheres to industry best practices in experiment tracking, data versioning, and CI/CD-friendly ML workflows.

---

## 🧰 Tech Stack

| Category | Tools / Technologies |
|-----------|----------------------|
| **Programming Language** | Python 3.8+ |
| **Data Versioning** | [DVC](https://dvc.org/) |
| **Experiment Tracking** | [DVCLive](https://dvc.org/doc/dvclive) |
| **Storage Backend** | AWS S3 |
| **Version Control** | Git & GitHub |
| **Libraries Used** | pandas, numpy, scikit-learn |

---

## ⚙️ Project Workflow

### **1️⃣ Project Setup**
```bash
# Clone the repository
git clone https://github.com/<your-username>/spam-detection-mlops.git
cd spam-detection-mlops

# Create virtual environment & install dependencies
pip install -r requirements.txt
```

## Structure of the project

```bash
spam-detection-mlops/
├── src/
│   ├── data_preprocessing.py
│   ├── train.py
│   ├── evaluate.py
├── data/              # Raw and processed data (ignored by Git)
├── models/            # Trained model artifacts (ignored by Git)
├── reports/           # Evaluation results
├── params.yaml        # Hyperparameters for reproducibility
├── dvc.yaml           # DVC pipeline definition
├── .gitignore
└── README.md
```


#### Add these folders to .gitignore:
```bash
data/
models/
reports/
```

### **2️⃣ Initialize DVC Pipeline (Without Params)**
```bash
dvc init
```


#### Define stages in dvc.yaml:
```bash
stages:
  preprocess:
    cmd: python src/data_preprocessing.py
    outs:
      - data/processed
  train:
    cmd: python src/train.py
    deps:
      - data/processed
    outs:
      - models/model.pkl
  evaluate:
    cmd: python src/evaluate.py
    deps:
      - models/model.pkl
    outs:
      - reports/metrics.json
```

#### Run and test the pipeline:
```bash
dvc repro
dvc dag
```

### **3️⃣ Add Parameters to Pipeline**

Create a params.yaml file:
```bash
train:
  test_size: 0.2
  random_state: 42
  n_estimators: 100
```

Update dvc.yaml to include params:
```bash
params:
  - train.test_size
  - train.random_state
  - train.n_estimators
```

Reproduce pipeline:
```bash
dvc repro
```


### **4️⃣ Experiment Tracking with DVCLive**

Install and integrate DVCLive:
```bash
pip install dvclive
```

In your train.py:
```bash
from dvclive import Live

with Live() as live:
    for epoch in range(epochs):
        # Training loop
        live.log("train_accuracy", accuracy)
        live.log("val_loss", val_loss)
```

Run experiments:
```bash
dvc exp run
```

Visualize experiment results:
```bash
dvc exp show
```

Manage experiments:
```bash
dvc exp remove <exp-name>
dvc exp apply <exp-name>
```

### **5️⃣ Configure AWS S3 as DVC Remote Storage**

Add your AWS S3 remote:
```bash
dvc remote add -d myremote s3://your-bucket-name/path
dvc remote modify myremote endpointurl https://s3.amazonaws.com
```

Push data and models to remote:
```bash
dvc push
```

To pull on another machine:
```bash
dvc pull
```


#### ☁️ Remote Storage Management

-All data, models, and reports are stored in AWS S3, ensuring:
-Centralized and scalable artifact management
-Seamless collaboration
-Reproducible ML experiments

#### ✅ Outcomes
-Automated ML pipeline with reproducibility
-Versioned data and models
-Real-time experiment tracking with metrics
-Cloud-based remote storage with AWS S3
-MLOps best practices for CI/CD readiness

🧑‍💻 Author

**Rajat Singh**
📍 AI/ML, Data Science & MLOps Enthusiast
🔗 [GitHub](https://github.com/Rajat2774)
 | 💼 [LinkedIn](www.linkedin.com/in/rajat-singh-6558aa294)

