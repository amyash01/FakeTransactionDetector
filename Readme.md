# 🛡️ Fake Transaction Detector (FTD)

> **A hybrid fraud detection platform combining rules, graph analytics, and unsupervised ML.**
> *Designed to expose fake and anomalous transactions with explainable scoring.*

---

## 🌟 Overview
FTD is a Flask-based transaction analysis engine that blends:
1. **Deterministic Rules (DDIE)** for hard-rule violations such as future timestamps, negative amounts, duplicates, and burst activity.
2. **Graph Network Analysis** for uncovering circular money flows, laundering loops, and suspicious recipient relationships.
3. **Unsupervised ML (UAIC)** for behavioral anomaly scoring using an Isolation Forest-like model.

The system adds transparent reasoning to every decision so analysts can understand why a transaction was flagged.

---

## 🚀 What FTD Does
* Detects fraudulent transaction patterns in CSV uploads.
* Produces per-transaction anomaly scores and explanations.
* Supports judge-mode scoring for live transaction evaluation.
* Generates downloadable intelligence reports in PDF format.
* Includes dashboards for a main view, live analysis, and architecture visualization.

---

## 🔍 Detectable Anomaly Types
FTD is built to identify:
* **Future timestamps** and invalid dates
* **Negative or zero amounts**
* **High-velocity burst transactions**
* **Duplicate or replayed records**
* **Impossible travel or location conflicts**
* **Money laundering loops and cyclic transfers**
* **Graph-based suspicious destination patterns**

---

## 📁 Repository Structure
```text
fake-transaction-detector/
├── app.py                       # Flask application entrypoint
├── Procfile                     # Production startup config for Gunicorn
├── requirements.txt             # Python dependency list
├── Readme.md                    # Project documentation
├── CSV/                         # Sample CSV datasets and demos
├── sample_data/                 # Sample input data for model initialization
├── static/                      # CSS, JS, generated reports, assets
│   ├── css/
│   └── js/
├── templates/                   # HTML UI templates
│   ├── index.html
│   ├── phonepe.html
│   └── architecture.html
├── tests/                       # Unit tests and validation logic
└── utils/                       # Core analysis engines and utilities
    ├── ddie.py
    ├── explain.py
    ├── graph_anomaly.py
    ├── preprocessing.py
    ├── scoring.py
    ├── ssg.py
    ├── uaic.py
    └── report_generator_v2.py
```

> Note: The actual project uses uploaded CSV files for analysis and does not require a separate demo generator script.

---

## 🛠️ Tech Stack
* **Backend:** Python 3.x, Flask
* **Data Processing:** Pandas, NumPy
* **ML / Anomaly Detection:** scikit-learn, UAIC engine
* **Graph Analytics:** NetworkX
* **Explainability:** custom explanation engine
* **Deployment:** Gunicorn (via `Procfile`)

---

## 🚀 Running the Project
### 1. Create or activate a Python environment
```bash
python -m venv .venv
.venv\Scripts\activate
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Start the server
```bash
python app.py
```

### 4. Open the app
Visit:
```text
http://127.0.0.1:5000
```

### 5. Analyze transactions
Upload a CSV file through the dashboard and launch the analyzer.

---

## 🧭 Main Application Routes
| Route | Description |
|---|---|
| `/` | Main dashboard page |
| `/live` | Live transaction analysis page |
| `/architecture` | Architecture visualization page |
| `/api/upload` | POST CSV file upload endpoint |
| `/api/analyze/<file_id>` | GET full analysis for uploaded CSV |
| `/api/user_profile/<file_id>/<user_id>` | GET historical user profile data |
| `/api/generate_report/<file_id>` | GET PDF intelligence report URL |
| `/api/judge` | POST single transaction evaluation |
| `/api/judge_history` | GET judge-mode transaction history |

---

## 📂 Sample Data and Demo Files
* Use the sample CSV files in `CSV/` for quick testing.
* The app also loads context from `sample_data/` during startup if present.

---

## 🧪 Testing
Run the repository tests with:
```bash
python -m pytest tests
```

---

## 💡 Notes
* The app stores uploaded CSV content in-memory while the server is running.
* Generated reports are written to `static/` and returned as accessible URLs.
* For production deployment, use `gunicorn app:app` or the provided `Procfile`.

---

## 📌 Quick Start
1. Install dependencies
2. Run `python app.py`
3. Navigate to `http://127.0.0.1:5000`
4. Upload a sample CSV and inspect anomaly results

---

## 📎 Additional Resources
* `app.py` — application flow and API endpoints
* `utils/ddie.py` — rule engine logic
* `utils/graph_anomaly.py` — graph-based anomaly detection
* `utils/uaic.py` — ML scoring and model behavior
* `utils/explain.py` — explanation generation
* `utils/report_generator_v2.py` — report PDF creation
