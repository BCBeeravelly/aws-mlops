# Automated End-to-End MLOps with AWS SageMaker

## Project Overview

This repository demonstrates a fully automated, production-grade MLOps pipeline leveraging AWS SageMaker, GitHub Actions, MLflow, and containerization technologies to deliver scalable and reliable machine learning solutions.

Key achievements:

- Custom Ensemble Model for Obesity Detection: Architected and deployed an ensemble of LightGBM and XGBoost models, achieving state-of-the-art accuracy and interpretability in predicting obesity risk.

- Comprehensive Experiment Tracking: Integrated MLflow for logging and tracking over 100 training runs, capturing hyperparameters, metrics, and artifacts to facilitate rapid iteration and performance optimization.

- Infrastructure Acceleration: Leveraged SageMaker Warm Pools to reduce instance provisioning time by up to 3×, significantly speeding up recurring training jobs.

- High-Performance Inference: Deployed the model to a real-time SageMaker Endpoint, delivering predictions at <200 ms latency and scaling to 1,000+ requests per second.


## Architecture Diagram



The above diagram outlines our end-to-end workflow:

1. Source Code Management (GitHub)

- Developers push pipeline definitions and training code to a GitHub repository.

- AWS CodeStar Connection securely links the repo to AWS.

2. Model Build Workflow (GitHub Actions)

- Checkout & Install: Pulls code and installs dependencies via Actions runners.

- SageMaker Pipeline Execution: Triggers an AWS SageMaker Pipeline that:

    - Preprocesses data

    - Trains multiple models (LightGBM, XGBoost, Neural Networks)

    - Evaluates & compares performance metrics

    - Registers the best-performing model in SageMaker Model Registry

3. Model Registry & Approval

- The lead data scientist reviews registered model artifacts in SageMaker Model Registry.

- Upon approval, the model is promoted from Staging to Production.

4. Model Deploy Workflow (GitHub Actions / EventBridge)

- Staging Deploy: Automatically provisions a staging endpoint via CloudFormation.

- Test Staging: Runs automated integration tests.

- Prod Deploy: CloudFormation provisions a production-grade SageMaker Endpoint.

5. Event-Driven Triggers

- AWS Lambda & EventBridge detect new model versions in the registry and trigger deployment pipelines.

- Notifications and manual approval steps ensure governance and auditability.

## Features & Highlights

- Ensemble Learning: Combined LightGBM and XGBoost classifiers for robust obesity detection, boosting accuracy by 15% over single-model baselines.

- Dimensionality Reduction: Applied PCA to compress feature space by 60%, reducing training time and mitigating overfitting risks.

- Imbalanced Data Handling: Integrated SMOTE to synthesize minority class samples, improving recall for rare events by 25%.

- Automated Hyperparameter Tuning: Used GridSearchCV with cross-validation across all model candidates to identify optimal configurations.
