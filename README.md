# 🧠 Mental Health Prediction System

An AI-powered Mental Health Prediction System that uses machine learning to predict whether an individual may need mental health treatment, based on 15 behavioral, demographic, and occupational indicators.

---

## 📁 Project Structure

```
mental_health_prediction/
├── data/
│   └── Mental_Health_dataset1.csv   # Dataset (auto-copied)
├── models/
│   ├── model.pkl                    # Trained ML model (generated)
│   ├── label_encoders.pkl           # Feature encoders (generated)
│   └── metadata.json                # Model metrics & feature importances (generated)
├── train_model.py                   # Data preprocessing + model training
├── app.py                           # Flask REST API backend
├── frontend.py                      # Streamlit interactive frontend
├── requirements.txt                 # Python dependencies
└── README.md
```

---

## 🚀 Quick Start

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Train the Model

```bash
python train_model.py
```

This will:
- Load and preprocess `data/Mental_Health_dataset1.csv`
  Dataset Link: https://www.kaggle.com/datasets/bhavikjikadara/mental-health-dataset
  
- Train 3 models: RandomForest, GradientBoosting, LogisticRegression
- Select the best model by accuracy
- Save `model.pkl`, `label_encoders.pkl`, `metadata.json` to `models/`

### 3. Start the Flask Backend

```bash
python app.py
```

API runs at: `http://localhost:5000`

### 4. Launch the Streamlit Frontend

Open a new terminal:

```bash
streamlit run frontend.py
```

Frontend opens at: `http://localhost:8501`

---

## 🌐 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | API status check |
| GET | `/health` | Model readiness check |
| GET | `/metadata` | Model metrics and feature importances |
| GET | `/options` | Dropdown values for all features |
| GET | `/feature_importance` | Feature importance scores |
| POST | `/predict` | Single prediction |
| POST | `/batch_predict` | Bulk predictions from JSON array |

### Example: Single Prediction

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{
    "Gender": "Female",
    "Occupation": "Corporate",
    "SelfEmployed": "No",
    "FamilyHistory": "Yes",
    "DaysIndoors": "More than 2 months",
    "HabitsChange": "Yes",
    "MentalHealthHistory": "Yes",
    "IncreasingStress": "Yes",
    "MoodSwings": "High",
    "SocialWeakness": "Yes",
    "CopingStruggles": "Yes",
    "WorkInterest": "No",
    "MentalHealthInterview": "No",
    "CareOptions": "Not sure"
  }'
```

**Response:**
```json
{
  "prediction": "Yes",
  "confidence": 0.87,
  "probabilities": { "No": 0.13, "Yes": 0.87 },
  "risk_level": "High",
  "needs_treatment": true
}
```

---

## 📊 Dataset

- **File:** `Mental_Health_dataset1.csv`
- **Rows:** ~292 records
- **Target:** `Treatment` (Yes / No)
- **Features (15):**

| Feature | Description |
|---------|-------------|
| Gender | Biological sex |
| Occupation | Work category |
| SelfEmployed | Self-employment status |
| FamilyHistory | Family mental health history |
| DaysIndoors | Days spent indoors |
| HabitsChange | Changes in daily habits |
| MentalHealthHistory | Personal mental health history |
| IncreasingStress | Presence of increasing stress |
| MoodSwings | Frequency of mood changes |
| SocialWeakness | Difficulty in social settings |
| CopingStruggles | Difficulty coping |
| WorkInterest | Interest in work/activities |
| MentalHealthInterview | Discussed MH in job interview |
| CareOptions | Awareness of care options |

---

## 🤖 ML Models

Three models are trained and compared:

| Model | Notes |
|-------|-------|
| **RandomForest** | Ensemble of 200 decision trees |
| **GradientBoosting** | Boosted ensemble of 150 trees |
| **LogisticRegression** | Baseline linear classifier |

The best model (by test accuracy) is automatically selected and saved.

---

## 🖥️ Frontend Pages

| Page | Description |
|------|-------------|
| 🏠 Home | Overview, key metrics, how it works |
| 🔍 Predict | Interactive form with live prediction |
| 📊 Analytics | Model comparison, feature importance, EDA charts |
| 📁 Batch Predict | Upload CSV for bulk predictions |
| ℹ️ About | Tech stack, dataset info, API reference |

---

## ⚠️ Disclaimer

This tool is for **educational and research purposes only**.  
It does **NOT** replace professional medical or psychological advice.  
If you are experiencing mental health difficulties, please consult a licensed healthcare professional.

---

## 🛠️ Tech Stack

- **ML:** scikit-learn (RandomForest, GradientBoosting, LogisticRegression)
- **Backend:** Flask, flask-cors
- **Frontend:** Streamlit, Plotly
- **Data:** pandas, numpy
