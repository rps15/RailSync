<div align="center">

# 🚆 RailSync

### Machine-Learning Powered Train ETA Prediction and Railway Operations Dashboard

</div>

---

RailSync is a web-based railway intelligence platform that combines machine-learning based ETA prediction with passenger and railway operator dashboards.

The system allows passengers to view train status, schedules, delays, and predicted arrival times, while railway operators can monitor trains, manage operational events, provide operational inputs, and observe their effect on ETA predictions.

> **Note:** RailSync is currently a prototype/demo system using simulated train movement and operational data.

---

## 📑 Table of Contents

- [Features](#-features)
- [Tech Stack](#️-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [System Architecture](#-system-architecture)
- [ML Prediction Flow](#-ml-prediction-flow)
- [API Endpoints](#-api-endpoints)
- [Dataset & Model](#-dataset)
- [Prototype Scope](#-prototype-scope)
- [Future Scope](#️-future-scope)
- [Testing](#-testing)
- [Security](#-security)
- [Contributing](#-contributing)
- [Author](#-author)

---

## ✨ Features

### 🤖 ML-Based ETA Prediction

RailSync uses a trained machine-learning model to predict the remaining travel time of a train between stations. The prediction system uses route and operational information to generate an estimated remaining travel time and ETA.

**Example prediction response:**

```json
{
    "train_no": 12723,
    "current_station": "Kazipet",
    "next_station": "Warangal",
    "predicted_remaining_time_min": 36.9,
    "operational_override_applied": false,
    "current_delay_min": -5.0,
    "congestion_score": 0.305
}
```

### 👤 Passenger Dashboard

Passengers can:

- View available trains
- View train status
- View current location
- View current delay
- View scheduled arrival
- View ML-predicted arrival
- View route information
- View downstream station projections
- View train details
- View railway alerts and events

### 🧑‍💼 Operator Dashboard

The operator dashboard provides a control-room style interface for railway operations.

Operators can:

- Monitor active trains
- View delayed trains
- Monitor trains requiring attention
- View high-risk trains
- View active operational events
- Add operational events
- Resolve operational events
- Provide operational inputs for train sections
  - Enter operational delay
  - Enter congestion information
  - Select event types
  - Add operator notes
- Trigger updated ETA predictions

### 🔐 Operator Authentication

Operator access is protected by a backend-verified login system.

```text
Operator Login
      ↓
FastAPI Authentication API
      ↓
Credential Verification
      ↓
Authenticated Session
      ↓
Operator Dashboard
```

Operator credentials can be configured using environment variables:

```env
OPERATOR_USERNAME=your_username
OPERATOR_PASSWORD=your_password
```

> ⚠️ Sensitive credentials should **never** be committed to Git.

### 🚨 Alerts & Operational Events

RailSync provides operational visibility through:

- Train delay alerts
- Congestion-related alerts
- Operational events
- Event severity
- Event status
- Operator notes
- Event resolution

### 📊 Analytics

The analytics dashboard provides visual information about railway operations and train performance. The frontend uses charts to display relevant operational and delay information.

### 🧪 Simulation

RailSync includes a simulation environment for testing different railway operating conditions.

Example scenarios include:

- Train delays
- Congestion
- Signal-related disruptions
- Speed restrictions
- Platform issues
- Weather-related conditions
- Operational events
- Recovery scenarios

The simulation is intended to demonstrate how changing operational conditions can affect train ETA and railway status.

### 🗓️ Train Schedule

The schedule page provides timetable information including:

- Train number
- Train name
- Route
- Stations
- Scheduled timings
- Running information

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | HTML, CSS, Vanilla JavaScript |
| **Backend** | Python |
| **API Framework** | FastAPI |
| **API Server** | Uvicorn |
| **Machine Learning** | Scikit-learn / XGBoost |
| **Data Processing** | Pandas, NumPy |
| **Model Serialization** | Joblib / Pickle |
| **Visualization** | Chart.js |
| **Mapping** | Leaflet.js |
| **Dataset** | Train ETA dataset with 10,000 records |

The frontend intentionally uses Vanilla JavaScript rather than a frontend framework, keeping the application lightweight and easy to deploy as a static frontend.

---

## 📁 Project Structure

```text
RailSync/
│
├── backend/
│   ├── data/
│   │   └── train_eta_initial_dataset_10000.csv
│   │
│   ├── model/
│   │   └── train_eta_best_model_withcorrespondece.pkl
│   │
│   ├── requirements.txt
│   └── main.py
│
├── frontend/
│   ├── css/
│   │
│   ├── js/
│   │   ├── alerts.js
│   │   ├── analytics.js
│   │   ├── app.js
│   │   ├── auth.js
│   │   ├── events.js
│   │   ├── map.js
│   │   ├── mockData.js
│   │   ├── operations.js
│   │   ├── operator.js
│   │   ├── passenger.js
│   │   ├── schedule.js
│   │   ├── simulation.js
│   │   ├── train.js
│   │   └── ui.js
│   │
│   ├── index.html
│   ├── passenger.html
│   ├── operator.html
│   ├── train.html
│   ├── schedule.html
│   ├── alerts.html
│   ├── events.html
│   ├── analytics.html
│   └── simulation.html
│
├── train_eta_best_model_withcorrespondece.pkl
├── train_eta_initial_dataset_10000.csv
├── .gitignore
└── README.md
```

> The backend uses the model and dataset located under `backend/model/` and `backend/data/`.

---

## 🚀 Getting Started

### Prerequisites

- Python 3.11+
- Git
- A modern web browser

### 1. Clone the Repository

```bash
git clone https://github.com/rishabh9195/RailSync.git
cd RailSync
```

### 2. Set Up the Backend

Move into the backend directory:

```bash
cd backend
```

Create a Python virtual environment:

```bash
python -m venv .venv
```

Activate the virtual environment:

```bash
# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate
```

Install all required dependencies:

```bash
pip install -r requirements.txt
```

#### ⚠️ Important ML Dependency

The trained model requires a compatible version of scikit-learn. The current environment uses:

```text
scikit-learn==1.7.2
```

The required dependency versions are pinned in `backend/requirements.txt`. This helps ensure that the serialized ML model can be loaded consistently across environments.

### 3. Configure Operator Credentials

The backend supports environment variables for operator credentials:

```env
OPERATOR_USERNAME=admin
OPERATOR_PASSWORD=your_password
```

> Do not commit `.env` files or real credentials to GitHub.

### 4. Start the Backend

From the `backend` directory:

```bash
uvicorn main:app --reload
```

| Service | URL |
|---------|-----|
| Backend | http://127.0.0.1:8000 |
| FastAPI Interactive Docs | http://127.0.0.1:8000/docs |

### 5. Start the Frontend

Open a **second terminal**, then:

```bash
cd frontend
python -m http.server 5500
```

Open the application at **http://localhost:5500**

---

## 🔄 System Architecture

```text
                    ┌──────────────────────┐
                    │   Passenger Portal   │
                    └──────────┬───────────┘
                               │
                               │ HTTP
                               ▼
┌────────────────────────────────────────────────┐
│                FastAPI Backend                 │
│                                                │
│ Authentication     Prediction     Operations   │
│      │                  │              │       │
│      │                  ▼              ▼       │
│      │              ML Model     Operational   │
│      │                            State        │
│      │                  │              │       │
│      └──────────────────┼──────────────┘       │
│                         ▼                      │
│                   ETA Prediction               │
└─────────────────────────┬──────────────────────┘
                          │
                          ▼
                 ┌───────────────────┐
                 │ Operator Dashboard│
                 └───────────────────┘
```

---

## 🤖 ML Prediction Flow

```text
Train Number
     │
Current Station
     │
Next Station
     │
     ▼
Route / Operational Features
     │
     ├── Distance
     ├── Current Delay
     ├── Congestion
     └── Other Model Features
     │
     ▼
Trained ML Pipeline
     │
     ▼
Predicted Remaining Time
     │
     ▼
Predicted Arrival Time
```

The backend exposes the prediction functionality through `POST /predict`.

### 🧑‍💼 Operational Input → ML Flow

RailSync allows operators to provide operational information for a train section.

```text
Operator
   │
   ├── Operational Delay
   ├── Congestion
   ├── Event Type
   └── Operator Note
   │
   ▼
/operations/update
   │
   ▼
Operational State
   │
   ▼
/predict
   │
   ▼
ML Prediction
   │
   ▼
Updated ETA
```

This allows the prototype to demonstrate how operational conditions can influence ETA predictions.

---

## 🔌 API Endpoints

| Category | Method | Endpoint |
|----------|--------|----------|
| Health | `GET` | `/` |
| Operator Authentication | `POST` | `/auth/operator/verify` |
| ETA Prediction | `POST` | `/predict` |
| Operational Data | `POST` | `/operations/update` |
| Operational Data | `GET` | `/operations/{train_no}` |
| Operational Data | `POST` | `/operations/clear` |
| Alerts | `GET` | `/alerts` |
| Alerts | `GET` | `/alerts/{train_no}` |

For the complete API specification, run the backend and open http://127.0.0.1:8000/docs

---

## 📊 Dataset

RailSync currently uses a dataset containing approximately **10,000 records** for train ETA prediction.

**Location:** `backend/data/train_eta_initial_dataset_10000.csv`

The dataset provides the historical information used by the ETA prediction pipeline.

## 🤖 Trained Model

**Location:** `backend/model/train_eta_best_model_withcorrespondece.pkl`

The FastAPI backend loads the serialized model and uses it to generate predictions through the `/predict` endpoint.

---

## 🧪 Prototype Scope

RailSync is currently a prototype for demonstrating machine-learning assisted railway ETA prediction and railway operations monitoring. The current system uses simulated/demo train movement and operational data, and is **not** connected to real railway operational systems.

It does **not** currently provide:

- Real-time GPS train tracking
- Live Indian Railways operational feeds
- Real signalling data
- Ticket booking
- Payment processing

These can be integrated in future versions.

---

## 🗺️ Future Scope

- Integration with real-time railway data feeds
- GPS-based train tracking
- Real railway operational data
- Weather API integration
- Track-condition data
- Larger historical datasets
- Improved ML models
- Model monitoring and evaluation
- Cloud deployment
- Scalable real-time infrastructure
- Passenger notifications
- Production-grade authorization and security

---

## 🧪 Testing

Backend tests can be added and executed using:

```bash
pytest
```

---

## 🔐 Security

Sensitive information should be stored using environment variables.

Never commit `.env` or real passwords/API keys to the repository. The `.gitignore` should also exclude virtual environments and Python cache files:

```gitignore
.venv/
__pycache__/
*.pyc
.env
```

---

## 🤝 Contributing

Contributions are welcome.

1. Fork the repository.
2. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature
   ```
3. Make your changes.
4. Commit your changes:
   ```bash
   git commit -m "Add your feature"
   ```
5. Push your branch:
   ```bash
   git push origin feature/your-feature
   ```
6. Open a Pull Request.

---

## 👤 Author

**Rishabh Gupta**

GitHub: [@rishabh9195](https://github.com/rishabh9195)

---

## 📌 Project Status

RailSync is an active prototype under development. The current version demonstrates:

- ✅ ML-based ETA prediction
- ✅ Passenger train tracking
- ✅ Railway operator dashboard
- ✅ Operator authentication
- ✅ Operational inputs
- ✅ Delay and congestion handling
- ✅ Alerts and events
- ✅ Analytics
- ✅ Simulation
- ✅ Train scheduling
