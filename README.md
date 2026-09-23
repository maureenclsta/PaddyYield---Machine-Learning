# 🌾 Paddy Yield Prediction System

A machine learning application that predicts rice (paddy) yield from agricultural cultivation data — land area, seed usage, fertilization, and crop protection inputs — and serves the prediction through an interactive Streamlit web app.

---

## 🎥 Live Demo

- **Demo Video:** [Watch on Google Drive](https://drive.google.com/file/d/1rsxZ-KoJeUb3_j_LDoSpgeTKJPQCuy7o/view?usp=drivesdk)
- **Live Application:** [paddy-yield-prediction.streamlit.app](https://2aolml-l49mtt5tx7f4sj8heeu9kx.streamlit.app)

---

## 🎯 Project Purpose

Rice yield is influenced by many interacting cultivation factors — land preparation, seeding rate, fertilizer dosage, and pest/weed control — which makes manual estimation difficult for farmers and agricultural planners. This project builds a regression model that learns from historical paddy cultivation records to estimate total yield (in Kg) from a set of measurable farming inputs, and packages it into a simple web form so that a user can enter their own field data and immediately get a yield estimate along with basic productivity feedback.

The intended users are farmers, agricultural students, or planners who want a quick, data-driven estimate of expected rice yield based on their cultivation practices.

---

## ✨ Features

- 📋 **Categorized input form** — cultivation parameters are grouped into logical sections: main land area, nursery/seedbed, main field preparation, fertilization & nutrition, and crop protection
- 🌳 **Yield prediction** powered by an Optimized Random Forest Regressor trained on historical paddy cultivation data
- 📊 **Productivity ratio calculation** — converts the total predicted yield into Kg per hectare
- 🚦 **Productivity classification** — automatically labels the result as *Rendah* (Low), *Sedang* (Medium), or *Tinggi* (High) based on the yield-per-hectare ratio
- 💡 **Rule-based cultivation recommendations** — generates guidance on seed rate, soil fertility, macro-fertilizer strategy, micronutrients, and weed/pest protection based on the values entered
- 🎨 **Custom-styled interface** with light and dark mode support
- 🖼️ Branded header image (crop logo)

---

## ⚙️ How It Works

1. The user opens the Streamlit app and is shown a form of numeric input fields grouped into five categorized cards (land area, nursery, main field preparation, fertilization, crop protection).
2. The user enters values reflecting their actual field conditions (each field has a sensible default value pre-filled).
3. On clicking **"Hitung Prediksi Hasil Panen"** (Calculate Yield Prediction), the app assembles the inputs into a single-row DataFrame and reindexes it to match the exact feature order the model was trained on (`feature_columns.pkl`).
4. The input row is scaled using the saved `StandardScaler` (`robust_standard_scaler.pkl`).
5. The scaled input is passed to the trained Random Forest model (`best_random_forest_model.pkl`), which returns a predicted total yield in Kg.
6. The app derives the yield-per-hectare ratio and classifies it into a productivity tier (Low / Medium / High).
7. The prediction, productivity ratio, and tier are displayed in a result card, followed by a set of rule-based cultivation recommendations generated from the input values.

---

## 🧰 Tech Stack

### Programming Language
- Python

### Frameworks / Libraries
- [Streamlit](https://streamlit.io/) — web app framework / UI
- pandas — data handling
- NumPy
- scikit-learn — model training, scaling, evaluation
- joblib — model/scaler/column serialization
- Pillow (PIL) — logo image loading

### Tools
- Jupyter Notebook — data exploration, model training and evaluation (`main.ipynb`)
- Git / GitHub — version control

### AI / Machine Learning
- **RandomForestRegressor** (scikit-learn) — final deployed model, tuned via `GridSearchCV`
- **KNeighborsRegressor** and **LinearRegression** — baseline models compared against Random Forest
- **GridSearchCV** + **KFold** (5-fold) cross-validation — hyperparameter tuning
- **StandardScaler** — feature scaling

---

## 📁 Project Structure

```text
PaddyYield - Machine Learning/
├── app.py                                                              # Streamlit web application (main entry point)
├── main.ipynb                                                          # Data cleaning, feature selection, model training & evaluation
├── train_model.py                                                      # Minimal example script (not the production training pipeline)
├── paddydataset.csv                                                    # Raw dataset used for training
├── best_random_forest_model.pkl                                        # Trained Random Forest model (used by app.py)
├── robust_standard_scaler.pkl                                          # Fitted StandardScaler used to scale user input
├── feature_columns.pkl                                                 # Ordered list of feature columns expected by the model
├── requirements.txt                                                    # Python dependencies
├── logo_padi.jpg                                                       # Header/logo image used in the app
├── performance_metrics_comparison.png                                  # Model performance comparison chart
├── actual_vs_predicted_3_models_grid.png                               # Actual vs. predicted yield plots for all 3 models
├── feature_importance_all_45.png                                       # Feature importance chart (all 45 original features)
├── feature_importance_top12.png                                       # Feature importance chart (top 12 selected features)
├── Prediksi Hasil Panen Padi Menggunakan Pendekatan Machine Learning.docx  # Project report document
└── README.md
```

**Notable files:**
- `app.py` — the Streamlit application users interact with.
- `main.ipynb` — the actual ML pipeline: data cleaning, feature selection, encoding, scaling, hyperparameter tuning, model comparison, and export of the `.pkl` artifacts used by `app.py`.
- `train_model.py` — a small standalone example script using a dummy dataset; it is **not** the pipeline used to produce the deployed model.

---

## 🖱️ How to Use

1. Open the [live application](https://2aolml-l49mtt5tx7f4sj8heeu9kx.streamlit.app) (or run it locally — see below).
2. Fill in the numeric fields in each section:
   - **Luas Lahan Utama** — main field area (hectares) and seed quantity (kg)
   - **Area Pembibitan Awal** — nursery area and nursery land preparation
   - **Pengolahan Lahan Utama** — main field preparation and straw/residue management
   - **Pemupukan & Nutrisi Tanaman** — DAP, Urea, Potash, and micronutrient dosages
   - **Perlindungan Tanaman** — herbicide and pesticide amounts
3. Use a period (`.`) as the decimal separator (e.g. `62.28`).
4. Click **"Hitung Prediksi Hasil Panen"**.
5. Review the estimated total yield, the productivity ratio (Kg/hectare), the productivity tier, and the generated cultivation recommendations.

---

## 🚀 Installation & Setup

### Prerequisites
- Python 3.10+
- pip

### Steps

Clone the repository:

```bash
git clone https://github.com/nathanyaxavier/2_AOL_ML.git
cd "PaddyYield - Machine Learning"
```

Install dependencies:

```bash
pip install -r requirements.txt
```

> **Note:** `requirements.txt` currently lists `streamlit`, `numpy`, and `scikit-learn`. `app.py` also imports `pandas`, `joblib`, and `Pillow`, so make sure these are installed as well (e.g. `pip install pandas joblib pillow`) if they are not already present in your environment.

Run the application locally:

```bash
streamlit run app.py
```

The app will open in your browser, typically at `http://localhost:8501`.

No environment variables or API keys are required to run this project.

---

## ☁️ Deployment

The application is deployed on **Streamlit Community Cloud** and is publicly accessible at:

🔗 [https://2aolml-l49mtt5tx7f4sj8heeu9kx.streamlit.app](https://2aolml-l49mtt5tx7f4sj8heeu9kx.streamlit.app)

Streamlit Community Cloud builds the app directly from this repository's `app.py` entry point and installs the dependencies listed in `requirements.txt`. The serialized model artifacts (`best_random_forest_model.pkl`, `robust_standard_scaler.pkl`, `feature_columns.pkl`) are loaded directly from the repository at runtime via `joblib`.

`[Add information here]` — no additional deployment configuration files (e.g. `Dockerfile`, `Procfile`, or Streamlit `secrets.toml`) were found in the source code, so any further platform-specific settings used for the live deployment are not determinable from the repository alone.

---

## 👥 Team Members

| Name | NIM |
|------|-----|
| Angelina Jolie Candaya | 2802541644 |
| Maureen Calista Surjo | 2802536392 |
| Nathanya Xavier Napitupulu | 2802545850 |

---

## 📄 License

This project was developed for academic purposes.

