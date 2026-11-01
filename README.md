# CardioSense AI - Early Coronary Heart Disease Detection System

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=flat&logo=react&logoColor=61DAFB)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
![Accuracy](https://img.shields.io/badge/Ensemble_Accuracy-88.66%25-success?style=flat)
![AUC](https://img.shields.io/badge/AUC-93.77%25-blue?style=flat)

A full-stack web application for predicting 10-year coronary heart disease (CHD) risk using an ensemble of three machine learning models (XGBoost, LightGBM, and CatBoost).

## 🏥 Project Overview

CardioSense AI is a semester AI Project from the Department of Computer Science at **University of South Asia, Lahore**. The system analyzes clinical parameters from the Framingham Heart Study dataset to provide real-time CHD risk predictions.

**Team:**
- **Fahad Khan** (B-28417) - Data Pre-Processing, Feature Engineering, Documentation and Deployment
- **Hammad Ahmed** (B-28400) - Research, Dataset collection, EDA, Model Training

## 🎯 Features

✨ **Ensemble Machine Learning** - Combined predictions from three advanced models

📊 **Real-Time Analysis** - Instant risk assessment with visual insights

📈 **Comprehensive Charts** - Risk gauge, model comparison, feature importance

💯 **88.66% Accuracy, 93.77% AUC** - Ensemble result on a held-out test set from 4,240 patient records

🎨 **Modern UI** - Dark theme with glassmorphism, animations, and responsive design

⚡ **Fast Processing** - Quick predictions via FastAPI backend

## 🛠 Tech Stack

### Frontend
- **React 18** - UI framework
- **Vite** - Build tool
- **Framer Motion** - Animations
- **Recharts** - Data visualizations
- **Lucide React** - Icons
- **Tailwind CSS** - Styling

### Backend
- **FastAPI** - Python web framework
- **Uvicorn** - ASGI server
- **Scikit-learn** - ML utilities
- **NumPy** - Numerical operations

### ML Models
- **XGBoost** - Gradient boosting
- **LightGBM** - Fast boosting
- **CatBoost** - Categorical handling
- **SMOTE** - Class imbalance handling

---

## 📊 Model Performance

| Model | Accuracy | Precision | Recall | F1 | AUC |
|---|---|---|---|---|---|
| CatBoost | 88.39% | 95.41% | 80.95% | 87.58% | 93.52% |
| LightGBM | 88.25% | 93.44% | 83.17% | 88.01% | 93.78% |
| XGBoost | 87.55% | 94.09% | 81.92% | 87.58% | 93.35% |
| **Ensemble ★** | **88.66%** | **94.41%** | **82.20%** | **87.88%** | **93.77%** |

> All models are regularized, with a train/test gap below 5%.

---

## 📦 Project Structure

```
CardioSense AI/
├── frontend/                 # React + Vite application
│   ├── src/
│   │   ├── components/       # React components
│   │   │   ├── Navbar.jsx
│   │   │   ├── Hero.jsx
│   │   │   ├── HowItWorks.jsx
│   │   │   ├── Features.jsx
│   │   │   ├── PredictionForm.jsx
│   │   │   ├── ResultsSection.jsx
│   │   │   ├── results/      # Results sub-components
│   │   │   │   ├── RiskGauge.jsx
│   │   │   │   ├── ModelComparisonChart.jsx
│   │   │   │   ├── FeatureImportanceChart.jsx
│   │   │   │   ├── PatientSummary.jsx
│   │   │   │   └── Recommendations.jsx
│   │   │   ├── DatasetInsights.jsx
│   │   │   ├── TeamSection.jsx
│   │   │   └── Footer.jsx
│   │   ├── hooks/
│   │   │   └── usePrediction.js    # API hook
│   │   ├── utils/
│   │   │   └── healthRanges.js     # Health validation utilities
│   │   ├── App.jsx
│   │   ├── index.css
│   │   └── main.jsx
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
└── backend/                  # FastAPI application
    ├── main.py               # API endpoints
    ├── requirements.txt      # Python dependencies
    └── models/               # Trained .pkl model files
```

## 🚀 Quick Start

### Prerequisites
- Node.js 16+ (for frontend)
- Python 3.8+ (for backend)
- npm or pnpm

### Installation & Running

**Terminal 1 - Backend Setup:**
```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload --port 8000
```

The backend will start at `http://localhost:8000`

**Terminal 2 - Frontend Setup:**
```bash
cd frontend
npm install
npm run dev
```

The frontend will start at `http://localhost:5173`

## 📋 API Endpoints

### POST `/predict`
Submit patient clinical data for risk prediction.

**Request Body:**
```json
{
  "Sex": "Male",           // "Male" or "Female"
  "age": 55,               // 20-80 years
  "education": 4,          // 1-4
  "currentSmoker": "Yes",  // "Yes" or "No"
  "cigsPerDay": 10,        // 0-100
  "BPMeds": 1,             // 0 or 1
  "prevalentStroke": 0,    // 0 or 1
  "prevalentHyp": 1,       // 0 or 1
  "diabetes": "No",        // "Yes" or "No"
  "totChol": 240,          // 100-600 mg/dL
  "sysBP": 140,            // 80-300 mmHg
  "diaBP": 90,             // 40-200 mmHg
  "BMI": 25,               // 10-60 kg/m²
  "heartRate": 75,         // 40-200 bpm
  "glucose": 95            // 40-400 mg/dL
}
```

**Example Response:**
```json
{
  "ensemble_probability": 0.7167,
  "ensemble_prediction": 1,
  "risk_level": "HIGH",
  "xgboost_probability": 0.72,
  "lightgbm_probability": 0.68,
  "catboost_probability": 0.75,
  "feature_importance": {
    "Age": 0.18,
    "Systolic BP": 0.15,
    ...
  },
  "recommendations": [...]
}
```

### GET `/health`
Health check endpoint.

**Example Response:**
```json
{
  "status": "CardioSense AI API is running",
  "models": ["XGBoost", "LightGBM", "CatBoost"]
}
```

## 🤖 Model Files

The trained models are stored in `backend/models/` and loaded by the backend with `joblib`:

```python
import joblib

xgb_model = joblib.load("models/xgb_model.pkl")
lgbm_model = joblib.load("models/lgbm_model.pkl")
cat_model = joblib.load("models/cat_model.pkl")

xgb_prob = float(xgb_model.predict_proba(features)[0][1])
lgbm_prob = float(lgbm_model.predict_proba(features)[0][1])
cat_prob = float(cat_model.predict_proba(features)[0][1])
```

## 🎨 Design System

### Color Palette
- **Primary Background:** `#0A0F1E` (Deep dark navy-slate)
- **Card Surfaces:** `#0F1629`, `#111827`
- **Borders:** `#1E2A45`
- **Primary Accent:** `#E53E3E` (Heart red)
- **Secondary Accent:** `#10B981` (Emerald green)
- **Tertiary Accent:** `#3B82F6` (Electric blue)
- **Highlight:** `#06B6D4` (Cyan)
- **Purple Accent:** `#8B5CF6` (Violet)

### Typography
- **Headings:** Inter (700, 600 weights)
- **Body:** Inter (400, 500 weights)

### Effects
- Glassmorphism cards with backdrop blur
- Smooth hover transitions (200-300ms)
- Scale transforms and glowing box-shadows
- Framer Motion entrance animations
- Scroll-triggered reveal animations

## 📊 Framingham Dataset

The models are trained on the Framingham Heart Study cohort with:
- **4,240 patients** analyzed
- **15 clinical features** per patient
- **10-year CHD risk** as the prediction target
- **SMOTE** used to handle class imbalance
- **88.66% ensemble accuracy** and **93.77% AUC** on the test set

## 🔒 Security & Privacy

- Patient data is used only to generate the prediction and is not stored
- No external data transmission
- Update `allow_origins` in `main.py` before production deployment
- Always consult a qualified healthcare professional for medical decisions

## ⚠️ Disclaimer

This tool is for **informational and research purposes only**. It should not be used as a substitute for professional medical advice, diagnosis, or treatment. Always consult a qualified physician or healthcare provider for personalized medical evaluation.

## 📝 Development Notes

- **Frontend:** Single Page Application (SPA) built with React and Vite
- **Backend:** RESTful API with CORS enabled
- **Responsive:** Mobile-first design, optimized for 375px to 1440px widths
- **Accessibility:** Semantic HTML and ARIA labels

## 🔄 Build & Deployment

### Frontend Build
```bash
cd frontend
npm run build
```
Output: `dist/` folder ready for hosting

### Backend Deployment
```bash
cd backend
# Production
gunicorn -w 4 -k uvicorn.workers.UvicornWorker main:app
```

## 📄 License

This project is created for educational purposes at University of South Asia, Lahore.

## 🙏 Acknowledgments

- Framingham Heart Study dataset
- XGBoost, LightGBM, CatBoost communities
- React and FastAPI communities

---

**Last Updated:** November 2026
**Status:** Project is Completed
