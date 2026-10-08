# Mental Health Signal

Mental Health Signal is a student wellness analytics project that predicts a mental-health score using student profile, digital habits, academic activity, sleep, physical activity, and perceived stress information.

> **Important:** This project provides a statistical estimate only. It is not a medical diagnosis, professional mental-health assessment, or substitute for qualified care.

## Features

- Responsive web interface for collecting student wellness information.
- FastAPI backend with validation for every submitted response.
- Machine-learning prediction using the trained model.
- JSON API endpoint for automated requests.
- CORS support for browser-based requests.
- Model artifact included in the repository.

## Project structure

```text
.
├── index.html          # Frontend application
├── style.css           # Frontend styling
├── script.js           # Form validation and API requests
├── main.py             # FastAPI application and prediction route
├── Mental_Health_Model.pkl
├── ML_Project.ipynb    # Notebook used for model development
├── Student Social Media And Mental Health Impact.csv
├── requirements.txt     # Python dependencies
└── README.md
```

## Requirements

- Python 3.9 or newer
- Git
- A browser
- Internet access for installing Python packages

## Install dependencies

Open PowerShell in the project directory and run:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

If PowerShell blocks activation, run the following command once:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

## Run the project locally

Start the FastAPI server from the project root:

```powershell
uvicorn main:app --host 127.0.0.1 --port 2200 --reload
```

Open the frontend in a browser:

```text
index.html
```

The frontend currently uses the deployed API URL in `script.js`. To use the local backend, replace the `API_BASE` value with:

```javascript
const API_BASE = "http://127.0.0.1:2200";
```

Then refresh the browser and submit the form.

## API endpoints

### Welcome

```http
GET /
```

The endpoint returns a one-item welcome response. For example, the API may return:

```json
[
  "Welcome Guys"
]
```

### Predict mental-health score

```http
POST /predict
Content-Type: application/json
```

Example request:

```json
{
  "age": 21,
  "gender": "Female",
  "country": "India",
  "academic_level": "Undergraduate",
  "most_used_platform": "Instagram",
  "purpose_of_use": "Networking",
  "avg_daily_usage_hours": 3.4,
  "daily_unlocks": 56,
  "study_hours": 2.5,
  "physical_activity_hours": 1.2,
  "sleep_hours_per_night": 7.1,
  "stress_level": "Medium"
}
```

Example response:

```json
{
  "predicted_mental_health_score": 6.78
}
```

The API validates the submitted values using Pydantic. Invalid values return a `422 Unprocessable Entity` response.

## How the prediction works

1. The frontend collects student profile and habit information.
2. The frontend sends the data to the FastAPI `/predict` endpoint.
3. The API groups unusual country values under `Other`.
4. The input is converted into the expected machine-learning format.
5. The trained model predicts a score from `0` to `10`.

The output is an estimate based on the training data and model configuration. It should not be interpreted as a diagnosis or a guarantee of future mental-health status.

## Run the API from a terminal

```powershell
python -m pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 2200 --reload
```

The API is available at:

- http://127.0.0.1:2200
- http://localhost:2200

## Deployment

The frontend currently uses the deployed API URL:

```text
https://mansik-santulan-score.onrender.com
```

You can deploy this FastAPI application to a platform such as Render, Railway, Fly.io, or Azure. The model file must remain available in the deployment environment at the path used by `main.py`.

## License and disclaimer

This project is intended for educational and research purposes. It does not provide medical advice, treatment recommendations, or emergency support. If someone is experiencing serious distress or immediate danger, they should contact a licensed healthcare professional or local emergency service.
