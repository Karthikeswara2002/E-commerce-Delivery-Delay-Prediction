Delivery Delay Prediction Pipeline

Data Engineering + Machine Learning using Databricks, Delta Lake, and MLflow

Project Overview

Late deliveries negatively impact customer satisfaction and logistics efficiency. This project builds a complete end-to-end data pipeline and machine learning system to predict whether an order will be delivered late.

The project demonstrates both Data Engineering and Machine Learning workflows by building a scalable pipeline on Databricks with Delta Lake and MLflow.

The system processes raw order data, transforms it through a medallion architecture, and trains a model to predict delivery delays.

Architecture
Raw Dataset
     │
     ▼
Bronze Layer (Raw Data Ingestion)
     │
     ▼
Silver Layer (Data Cleaning & Feature Preparation)
     │
     ▼
Gold Layer (Aggregated ML Dataset)
     │
     ▼
Feature Engineering
     │
     ▼
SMOTE (Handle Class Imbalance)
     │
     ▼
XGBoost Model Training
     │
     ▼
MLflow Experiment Tracking
Data Engineering Pipeline

The project follows the Medallion Architecture:

Bronze Layer

Stores raw ingested data without transformations.

Tasks:

Data ingestion

Schema validation

Raw Delta table storage

Example tables:

orders
order_items
products
customers
sellers
payments

Stored as:

Delta tables
Silver Layer

Data cleaning and transformation layer.

Operations performed:

Remove duplicate records

Handle null values

Standardize column formats

Convert timestamps

Feature preparation

Examples:

delivery_days
shipping_delay
order_total_value
item_count
Gold Layer

Curated dataset used for machine learning.

Contains aggregated features such as:

Feature	Description
item_count	Number of items per order
total_price	Total order value
freight_value	Shipping cost
product_weight	Weight of items
product dimensions	Length, width, height

This layer is optimized for analytics and ML modeling.

Machine Learning Pipeline

The ML pipeline predicts whether an order will be delivered late.

Target variable:

is_late_delivery
0 → On-time delivery
1 → Late delivery

Workflow:

Feature dataset
     │
     ▼
Train-Test Split
     │
     ▼
SMOTE (handle imbalance)
     │
     ▼
XGBoost Training
     │
     ▼
Model Evaluation
     │
     ▼
MLflow Experiment Tracking
Handling Class Imbalance

The dataset contains severe imbalance:

On-time deliveries  ≈ 93%
Late deliveries     ≈ 7%

To address this issue, SMOTE (Synthetic Minority Oversampling Technique) was applied to the training dataset.

After balancing:

On-time deliveries ≈ 70%
Late deliveries ≈ 30%

This improves the model's ability to detect late deliveries.

Model

Model used:

XGBoost Classifier

Reasons:

Excellent performance on tabular data

Handles nonlinear relationships

Built-in regularization

Efficient training

Model Evaluation

Metrics used:

Metric	Purpose
Accuracy	Overall prediction correctness
Precision	Correct late delivery predictions
Recall	Ability to detect delayed deliveries
F1 Score	Balance between precision and recall
ROC-AUC	Model discrimination ability

Example results:

Metric	Score
Accuracy	~0.83
Precision	~0.15
Recall	~0.32
F1 Score	~0.21
ROC-AUC	~0.67
Experiment Tracking

Experiments are tracked using MLflow.

Logged items include:

Model parameters

Evaluation metrics

Confusion matrix

Model artifacts

Input schema

Benefits:

Reproducible experiments

Model comparison

Easier deployment

Technologies Used

Data Engineering:

Databricks

Apache Spark

Delta Lake

Python

Machine Learning:

Scikit-learn

XGBoost

Imbalanced-learn (SMOTE)

Experiment Tracking:

MLflow

Visualization:

Matplotlib

Seaborn

Dataset Limitations

Several limitations affect the predictive performance.

1. Severe Class Imbalance

Late deliveries represent only ~7% of records, making it difficult for models to learn minority class patterns.

2. Missing Logistics Variables

Important operational variables are not available:

Traffic conditions

Weather impact

Courier delays

Warehouse processing times

These factors strongly influence delivery delays.

3. Limited Geographic Information

The dataset includes city-level data only, without precise distance between seller and customer.

Distance is often a key driver of delivery delays.

4. Lack of Temporal Patterns

Delivery delays are affected by:

Holiday seasons

Peak sales periods

Weekend logistics

These temporal patterns are not fully represented.

Future Improvements

Potential improvements include:

Adding geographic distance features

Incorporating weather data

Using temporal features

Applying advanced imbalance techniques

Deploying the model as a real-time prediction API

Project Structure
delivery-delay-prediction
│
├── notebooks
│   ├── data_engineering_pipeline.ipynb
│   └── model_training.ipynb
│
├── data
│   └── raw_dataset.csv
│
├── models
│   └── delivery_delay_model
│
├── images
│   └── confusion_matrix.png
│
└── README.md
Key Takeaways

This project demonstrates:

✔ Building data engineering pipelines using Databricks and Delta Lake
✔ Applying Medallion Architecture
✔ Handling imbalanced datasets
✔ Training XGBoost models
✔ Tracking experiments using MLflow