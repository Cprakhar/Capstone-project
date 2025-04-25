# 🧠 Capstone Project: End-to-End ML Deployment on AWS EKS 🚀

This repository contains an end-to-end Machine Learning pipeline integrated with **MLflow**, **DVC**, **Flask**, **Docker**, **CI/CD**, and deployed on **AWS EKS**. Monitoring is done using **Prometheus & Grafana**. All infrastructure is production-grade and scalable.

---

## 🔧 Project Stack

| Area                | Tools Used |
|---------------------|------------|
| ML Workflow         | MLflow, DVC, Scikit-learn |
| Data Versioning     | DVC, S3 |
| Model Registry      | MLflow on DagsHub |
| Experiment Tracking | MLflow |
| App Framework       | Flask |
| Containerization    | Docker |
| CI/CD               | GitHub Actions |
| Deployment          | AWS EKS, Kubernetes |
| Monitoring          | Prometheus, Grafana |
| Infrastructure      | eksctl, kubectl, AWS CLI |

---

## 📁 Project Structure

```bash
.
├── .github/workflows/       # CI/CD workflow files
├── data/                    # Data files tracked by DVC
├── dvc.yaml                 # DVC pipeline definition
├── params.yaml              # Pipeline parameters
├── src/                     # Core project source code
│   ├── data_ingestion.py
│   ├── data_preprocessing.py
│   ├── feature_engineering.py
│   ├── model_building.py
│   ├── model_evaluation.py
│   └── register_model.py
├── flask_app/               # Flask REST API for model serving
│   ├── app.py
│   ├── Dockerfile
│   ├── requirements.txt
│   └── ...
├── tests/                   # Unit tests
└── README.md
```

---

## 🚀 How to Run the Project Locally

### 🏗️ Set Up Environment

```bash
# Clone the repo
git clone https://github.com/Cprakhar/Capstone-project.git
cd Capstone-project

# Create and activate virtual env
conda create -n venv python=3.12 -y
conda activate venv

# Install dependencies
pip install -r flask_app/requirements.txt
```

### 🧪 Run ML Pipeline

```bash
# Initialize DVC and run the pipeline
dvc init
dvc repro
```

### 📦 Run Flask App

```bash
# Run locally
cd flask_app
python app.py

# OR using Docker
docker build -t capstone-app:latest .
docker run -p 8888:5000 -e DAGSHUB_TOKEN=your_dagshub_token capstone-app:latest
```

---

## 🛠️ Setup CI/CD

 CI/CD is triggered via GitHub Actions:
- Runs tests
- Builds Docker image
- Pushes to AWS ECR
- Deploys to AWS EKS

Ensure these GitHub secrets are set:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`
- `AWS_ACCOUNT_ID`
- `ECR_REPOSITORY`
- `DAGSHUB_TOKEN`

---

## ☸️ Deployment on AWS EKS

- Cluster created using `eksctl`
- Docker image deployed using Kubernetes manifests
- LoadBalancer service exposes the app externally

```bash
# Verify deployment
kubectl get pods
kubectl get svc

# Access Flask API
curl http://<external-ip>:5000
```

---

## 📊 Monitoring with Prometheus + Grafana

- Prometheus scrapes metrics from Flask app.
- Grafana visualizes and tracks the model performance and requests.

Prometheus config (`/etc/prometheus/prometheus.yml`):

```yaml
scrape_configs:
  - job_name: "capstone-app"
    static_configs:
      - targets: ["<external-ip>:5000"]
```

Grafana accessible at `http://<ec2-ip>:3000`

---

## 📌 Key Features

- ✅ Version-controlled code & data (DVC + Git)
- ✅ Model training pipeline with parameter tuning
- ✅ CI/CD with GitHub Actions
- ✅ Dockerized REST API
- ✅ EKS deployment with autoscaling
- ✅ Live monitoring with Prometheus & Grafana
