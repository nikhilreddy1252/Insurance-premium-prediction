# Insurance Premium Prediction API

A FastAPI-based web service that predicts insurance premiums using a machine learning model.

## Features

- **Input Validation**: Pydantic models validate age, weight, height, income, smoking status, city, and occupation
- **Computed Risk Factors**: Automatically calculates BMI, age group, lifestyle risk, and city tier
- **ML-Powered Predictions**: Uses a pre-trained scikit-learn model for premium estimation

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/nikhilreddy1252/Insurance-premium-prediction.git
cd Insurance-premium-prediction
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

### 3. Activate the virtual environment

**Windows:**
```powershell
venv\Scripts\Activate.ps1
```

**macOS/Linux:**
```bash
source venv/bin/activate
```

### 4. Install dependencies

```bash
pip install -r requirements.txt
```

## Usage

### Start the server

```bash
uvicorn app:app --reload --host 0.0.0.0 --port 8000
```

The API will be available at `http://localhost:8000`

### API Documentation

Interactive docs are automatically available at:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

### Make a prediction

**Endpoint:** `POST /predict`

**Example request:**

```bash
curl -X POST "http://localhost:8000/predict" \
  -H "Content-Type: application/json" \
  -d '{
    "age": 35,
    "weight": 75.5,
    "height": 1.75,
    "income_lpa": 8.5,
    "smoker": true,
    "city": "Mumbai",
    "occupation": "private_job"
  }'
```

**Example response:**

```json
{
  "predicted_premium": 12500.50
}
```

## Input Schema

| Field | Type | Description |
|-------|------|-------------|
| `age` | int | Age (1-119) |
| `weight` | float | Weight in kg |
| `height` | float | Height in meters |
| `income_lpa` | float | Annual income in lakhs (LPA) |
| `smoker` | bool | Smoking status |
| `city` | str | City of residence |
| `occupation` | str | One of: `retired`, `freelancer`, `student`, `government_job`, `business_owner`, `unemployed`, `private_job` |

### Computed Fields (automatic)

- **BMI**: `weight / (height²)`
- **Age Group**: `young` (<25), `adult` (25-44), `middle_aged` (45-59), `senior` (60+)
- **Lifestyle Risk**: `high`, `medium`, or `low` based on smoking and BMI
- **City Tier**: 1, 2, or 3 based on city classification

## Project Structure

```
.
├── app.py              # FastAPI application
├── model.pkl           # Pre-trained ML model
├── insurance.csv       # Training dataset
├── fastapi_ml_model.ipynb  # Model training notebook
├── frontend.py         # Frontend interface (optional)
├── requirements.txt    # Python dependencies
└── README.md           # This file
```

## License

MIT
