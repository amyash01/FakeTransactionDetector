# Fake Transaction Detector

A sophisticated hybrid fraud detection platform that combines rule-based engines, graph analytics, and machine learning to identify fake transactions and financial anomalies in real-time.

## 🎯 Overview

FakeTransactionDetector is an advanced fraud detection system designed to protect financial systems by identifying suspicious and fraudulent transactions through multiple complementary detection methodologies. It processes transaction data through a sophisticated pipeline combining deterministic rules, graph-based anomaly detection, and ML-based scoring to achieve high accuracy and explainability.

**Key Capabilities:**
- Real-time transaction fraud detection
- Multi-method hybrid scoring (Rules + Graph + ML)
- Interactive web interface with visual dashboards
- Detailed fraud explanations and reports
- Batch processing support
- Graph-based circular fraud detection

## ✨ Features

### 1. **DDIE (Deterministic Data Integrity Engine)**
Rule-based detection engine that identifies obvious errors and anomalies:
- Duplicate transaction detection
- Timestamp violations and temporal anomalies
- Amount-based anomalies
- Missing field validation
- Time gap analysis between transactions
- Location conflict detection

### 2. **Graph Anomaly Detection**
Network analysis using transaction graphs:
- Models transactions as directed graphs (accounts as nodes, transactions as edges)
- Detects circular fraud patterns
- Community detection using Louvain algorithm
- Centrality-based anomaly scoring
- Identifies unusual transaction flow patterns

### 3. **ML-Based Anomaly Detection (UAIC)**
Machine learning models for behavioral analysis:
- User activity pattern analysis
- Statistical anomaly detection
- Feature extraction from transaction history

### 4. **Hybrid Scoring System**
Weighted combination of multiple detection methods:
- Rule score: 50% weight
- ML score: 40% weight
- Graph score: 10% weight
- Auto-tuned threshold optimization
- ROC curve analysis

### 5. **Explainability**
Transparent fraud explanations:
- SHAP (SHapley Additive exPlanations) integration
- LIME (Local Interpretable Model-agnostic Explanations)
- Rule-based reasoning
- Detailed fraud reports with PDF export

## 📦 Installation

### Prerequisites
- Python 3.8+
- pip package manager

### Setup

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd fake-transaction-detector
   ```

2. **Create virtual environment (recommended):**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application:**
   ```bash
   python app.py
   ```
   The application will be available at `http://localhost:5000`

## 🚀 Usage

### Web Interface

1. Navigate to `http://localhost:5000` in your browser
2. Upload a CSV file with transaction data
3. View real-time detection results with visualizations
4. Explore detailed fraud explanations
5. Generate and download comprehensive reports

### API Endpoints

#### Upload File
```bash
POST /upload
Content-Type: multipart/form-data

curl -F "file=@transactions.csv" http://localhost:5000/upload
```

#### Detect Fraud
```bash
POST /detect
Content-Type: application/json

{
  "file_id": "uploaded_file_id"
}
```

#### Get Results
```bash
GET /results?file_id=<file_id>
```

#### Generate Report
```bash
GET /report?file_id=<file_id>
Response: PDF file
```

#### Explain Decision
```bash
POST /explain
Content-Type: application/json

{
  "file_id": "file_id",
  "transaction_idx": 5
}
```

### Example Transaction Data Format

CSV with required columns:
- `sender`: Source account ID
- `receiver`: Destination account ID
- `amount`: Transaction amount
- `timestamp`: Transaction time (ISO 8601 or standard date format)
- `location`: Geographic location (optional)
- Additional behavioral features (optional)

## 🏗️ Architecture

```
Transaction Input
    ↓
Preprocessing & Cleaning
    ↓
├─→ DDIE (Rule Engine) → Rule Score
├─→ Graph Analysis → Graph Score
├─→ ML Model (UAIC) → ML Score
    ↓
Hybrid Scorer (Weighted Combination)
    ↓
Explainability Engine (SHAP/LIME)
    ↓
Report Generation & API Response
```

## 📂 Project Structure

```
fake-transaction-detector/
├── app.py                          # Flask application entry point
├── requirements.txt                # Python dependencies
├── Procfile                        # Heroku deployment config
├── README.md                       # This file
│
├── utils/                          # Core detection modules
│   ├── ddie.py                    # Deterministic Data Integrity Engine
│   ├── graph_anomaly.py           # Graph-based anomaly detection
│   ├── uaic.py                    # ML-based anomaly detection
│   ├── scoring.py                 # Hybrid scoring system
│   ├── explain.py                 # Explainability (SHAP/LIME)
│   ├── preprocess.py              # Data preprocessing
│   ├── profiling.py               # User profiling
│   ├── ssg.py                     # Statistical scoring
│   └── report_generator_v2.py     # PDF report generation
│
├── templates/                      # HTML templates
│   ├── index.html                 # Main dashboard
│   ├── architecture.html          # System architecture page
│   ├── phonepe.html               # PhonePe demo interface
│   └── ...
│
├── static/                         # Frontend assets
│   ├── css/                       # Stylesheets
│   │   ├── style.css
│   │   └── phonepe.css
│   └── js/                        # JavaScript
│       ├── app.js
│       └── phonepe.js
│
├── tests/                         # Unit tests
│   └── test_rules.py
│
├── sample_data/                   # Sample data for testing
│   └── sample.csv
│
└── CSV/                           # Test datasets
    ├── sample_transactions.csv
    ├── circular_fraud_demo.csv
    ├── graph_isolation_test.csv
    └── ...
```

## 🧪 Testing

Run unit tests:
```bash
python -m pytest tests/ -v
```

Test with sample data:
```bash
# Place CSV file in the application and run detection
python app.py
# Upload CSV/sample_transactions.csv via web interface
```

## 📊 Detection Performance

The hybrid system achieves high accuracy by:
- Combining multiple independent detection methods
- Leveraging diverse signal sources (rules, graph patterns, statistical anomalies)
- Auto-tuned threshold optimization using ROC curve analysis
- Explainable decisions for audit trails

## 🔧 Configuration

Key parameters in `utils/scoring.py`:
```python
rule_weight = 0.5      # Rule-based detection importance
ml_weight = 0.4        # Machine learning detection importance
graph_weight = 0.1     # Graph analytics importance
threshold = 0.6        # Fraud classification threshold
```

Adjust weights based on your specific use case and false positive tolerance.

## 📈 Demo Datasets

Sample CSV files are provided in the `CSV/` directory:
- `sample_transactions.csv` - Basic transaction set
- `circular_fraud_demo.csv` - Circular/ring fraud patterns
- `graph_isolation_test.csv` - Graph anomaly patterns
- `vigilo_demo_300.csv` - Large-scale demo dataset
- `all_rules_test_v2.csv` - Comprehensive rule testing

## 🤝 Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit changes (`git commit -am 'Add improvement'`)
4. Push to branch (`git push origin feature/improvement`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see LICENSE file for details.

## 📧 Support

For issues, questions, or suggestions:
- Open an issue on GitHub
- Check the Technical_Deep_Dive.html for detailed system documentation
- Review example implementations in the CSV/ directory

## 🔒 Security Considerations

- Sensitive transaction data should be handled with appropriate access controls
- Consider implementing authentication for API endpoints in production
- Enable HTTPS for all data transmission in production environments
- Regularly update dependencies for security patches

## 🎓 References

- [SHAP Documentation](https://shap.readthedocs.io/)
- [LIME Explainability](https://github.com/marcotcr/lime)
- [NetworkX Graph Analysis](https://networkx.org/)
- [Scikit-learn ML](https://scikit-learn.org/)

---

**Last Updated:** 2026-06-19  
**Version:** 2.0  
**Status:** Active Development
