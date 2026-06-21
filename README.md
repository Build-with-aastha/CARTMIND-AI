# CARTMIND-AI
Smart Shopping AI: Return Reduction Engine
This repository contains the core logic and service architecture for the Smart Shopping AI, a predictive engine designed to reduce e-commerce returns by intervening before checkout.
🏗 Project Structure
The codebase is organized into five service layers as defined in the system architecture
:
├── src/
│   ├── experience_layer/      # UI widgets (Product Page, Checkout Banners)
│   ├── decisioning_layer/     # Real-time scoring APIs (Risk & XAI)
│   ├── intelligence_layer/    # Model Registry & Feature Stores (User/Product Models)
│   ├── data_layer/            # NLP pipelines & Transaction/Return logs
│   └── automation_layer/      # Retraining jobs & Self-Learning Loops
├── models/                    # Serialized GBT and NLP model files
├── scripts/                   # Batch retraining and daily insight generation
└── tests/                     # Precision/Recall validation and A/B test logic
🛠 Tech Stack
Modeling: Supervised classification (Gradient-Boosted Trees) for risk prediction; NLP for text classification and sentiment extraction
.
Infrastructure: Real-time path optimized for low-latency (<300ms) responses
.
Data Strategy: A centralized Feature Store pre-computes low-latency user/product features for real-time inference
.
🔌 API Endpoints (Core Engines)
1. Get Return Risk Score
Endpoint: POST /v2/predict-risk
Inputs: user_id, product_id, selected_size, variant_id
.
Logic: Combines User Profile AI (behavioral/physical data) with Product Intelligence (review-mined risk tags)
.
Response: risk_score (0-100), risk_level (Low/Med/High), and explanation_text
.
2. Get Size Recommendation
Endpoint: GET /v2/recommend-size
Logic: Cross-references user body profiles against brand-specific sizing patterns
.
Response: recommended_size, confidence_level
.
3. Generate Explainable Reason (XAI)
Endpoint: GET /v2/explain
Logic: Translates the top contributing model features into one of four standard categories: Size, Fabric, Expectation, or Quality
.
🔄 The Self-Learning Loop
The most critical automation in this repository is the Self-Learning Loop
.
Triggers: Triggered by PURCHASE_COMPLETED or RETURN_INITIATED events
.
Action: Updates the training dataset and triggers model recalibration to ensure the engine "learns" from every outcome
.
🧪 Testing & Evaluation
Before promotion to production, all models must pass:
Precision Audit: Ensuring "High-Risk" flags have high accuracy to prevent user alert fatigue
.
Fairness Check: Auditing scores for disparate impact across non-standard body types
.
A/B Validation: Measuring the Return Rate Reduction (RRR) against a held-out control group
.
🚀 Setup & Integration
Sync Data Layers: Connect to the PIM (Product Catalog) and OMS (Order Management)
.
Initialize Models: Run the NLP pipeline on existing review text to generate initial Product Risk Tags
.
Configure Thresholds: Set the risk percentage (default 70%) that triggers Return Prevention Mode
.
Refer to the [FR-1 to FR-10] Functional Requirements in the documentation for full implementation details
.
