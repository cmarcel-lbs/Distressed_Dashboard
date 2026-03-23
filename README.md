# Corporate Distress Early Warning System — Dashboard
**E628 Data Science for Business | Person 3 (Ibrahim)**

## Folder structure
```
project/
├── app.py              ← main Dash application
├── requirements.txt    ← Python dependencies
├── Procfile            ← Render.com / Heroku process file
├── README.md
└── assets/             ← static images served by Dash automatically
    ├── roc_curves.png
    ├── confusion_matrices.png
    ├── tuning_results.png
    ├── shap_beeswarm.png
    ├── shap_waterfall.png
    ├── feature_importance.png
    ├── model_comparison.png
    └── risk_tier_chart.png
```

## Run locally
```bash
pip install -r requirements.txt
python app.py
# Open http://127.0.0.1:8050
```

## Deploy on Render.com (step-by-step)

1. Push this folder to a **GitHub repository**
2. Go to https://render.com and click **New → Web Service**
3. Connect your GitHub repo
4. Set these fields:
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `gunicorn app:server`
   - **Environment**: Python 3
5. Click **Create Web Service**
6. Wait ~2 minutes — Render will give you a live URL
7. Test all 4 panels on the live URL
8. Share the URL with the team (Person 4 needs it for Section 5)

## Dashboard panels

| Panel | Description | Key widgets |
|-------|-------------|-------------|
| 1 — Risk screener | Filter 18 companies by tier + threshold | Checklist, Slider, RadioItems, DataTable |
| 2 — Model performance | CV results, ROC curves, confusion matrices, tuning | Static images + interactive bar |
| 3 — Feature importance & SHAP | Gini importances + per-company SHAP waterfall | Dropdown, interactive bar |
| 4 — Company deep dive | Radar chart + probability breakdown per firm | Dropdown, Radar, Bar |

## Colour palette (matches Person 4 / Cristian)
```python
COLORS = {
    "distressed": "#E84855",
    "stable":     "#2E86AB",
    "neutral":    "#888888",
    "highlight":  "#F4A261",
    "background": "#1F2D3D",
}
TIER_COLORS = {
    "Critical": "#E84855",
    "High":     "#F4A261",
    "Moderate": "#FFD166",
    "Low":      "#2E86AB",
}
```

## Edge case handling
- Empty filter results show a clear user-friendly message (no crash)
- NaN feature values are replaced with 0.5 (midpoint) in the radar chart
- All data is embedded directly in `app.py` — no CSV files required at runtime
