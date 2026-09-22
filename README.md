## Network Security Project For Phising Data
# Network Security — ML Pipeline

An end-to-end machine learning system that detects network security threats from structured network traffic data. Built with a modular, production-style pipeline covering data ingestion, validation, transformation, model training, experiment tracking, and prediction.

**Author:** Rajan Kumar | B.Tech CSE, IIIT Sonepat | [GitHub](https://github.com/iiitianrajan)

---

## Overview

Most ML projects stop at a trained model in a notebook. This project goes further — it wraps the full lifecycle (raw data → prediction) into a reusable, config-driven pipeline:

```
Raw Data → Ingestion → Validation → Transformation → Training →
Evaluation → MLflow Tracking → Model Artifact → Prediction (API / Batch)
```

Each stage is an independent, testable component, which makes the pipeline easy to maintain, debug, and extend.

## Features

- **Data Ingestion** — reads source data from MongoDB Atlas and produces train/test splits as versioned artifacts
- **Data Validation** — schema checks and data-drift detection before data reaches training
- **Data Transformation** — feature preprocessing with a persisted preprocessor object for consistent inference-time transforms
- **Model Training & Tuning** — trains multiple candidate models with hyperparameter tuning and selects the best performer
- **Experiment Tracking** — logs parameters, metrics, and artifacts with **MLflow**, tracked remotely via **DagsHub**
- **Model Management** — pushes and versions the final model and preprocessor as artifacts
- **Prediction Service** — a **FastAPI** app exposing endpoints to trigger training and serve predictions, with interactive Swagger docs
- **Batch Prediction** — runs inference over a full dataset in one pass rather than record-by-record
- **Structured Logging & Custom Exceptions** — consistent, traceable error handling across the pipeline

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python |
| ML | Scikit-learn, Pandas, NumPy |
| API | FastAPI, Uvicorn |
| Experiment Tracking | MLflow, DagsHub |
| Database | MongoDB Atlas |
| Tooling | Git, GitHub, VS Code |

## Project Structure

```
networksecurity/
├── networksecurity/
│   ├── components/          # ingestion, validation, transformation, model trainer
│   ├── configuration/
│   ├── constants/
│   ├── entity/
│   ├── pipeline/            # training_pipeline.py
│   ├── utils/
│   ├── exception/
│   └── logging/
├── Artifacts/
├── config/
├── notebooks/
├── templates/
├── app.py
├── setup.py
├── requirements.txt
├── .gitignore
└── README.md
```

## Getting Started

### 1. Clone and set up the environment

```bash
git clone https://github.com/iiitianrajan/networksecurity.git
cd networksecurity
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 2. Configure environment variables

Create a `.env` file in the project root:

```env
MONGODB_URL=<your-mongodb-connection-string>
MLFLOW_TRACKING_URI=<your-mlflow-tracking-uri>
MLFLOW_TRACKING_USERNAME=<your-username>
MLFLOW_TRACKING_PASSWORD=<your-password>
```

> Never commit `.env` or credentials to GitHub.

### 3. Run the application

```bash
uvicorn app:app --reload
```

- App: `http://127.0.0.1:8000`
- API docs (Swagger): `http://127.0.0.1:8000/docs`

The training pipeline (ingestion → validation → transformation → training → evaluation → MLflow logging) can be triggered from the API.

## What This Project Demonstrates

- End-to-end ML pipeline design and modular architecture
- Data validation and preprocessing strategy for production data
- Model selection and hyperparameter optimization
- Experiment tracking and reproducibility with MLflow + DagsHub
- REST API development for model serving with FastAPI
- Batch inference workflows
- Clean logging and exception handling in a Python package

## Roadmap

- [ ] Docker containerization
- [ ] CI/CD with GitHub Actions
- [ ] AWS S3 for artifact storage
- [ ] AWS ECR + EC2 deployment
- [ ] Model monitoring and data drift alerts
- [ ] Automated retraining

---

*Feedback and contributions are welcome — feel free to open an issue or PR.*
