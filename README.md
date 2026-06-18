# 🎬 YouTube Content Monetization Modeler

A machine learning project that predicts **YouTube ad revenue** from video performance and contextual features, deployed as an interactive Streamlit web application.

🔗 **[Live App → YouTube Ad Revenue Predictor](https://youtubecontentmonetizationmodeler-3ddh53xessm6tsi38xsy7u.streamlit.app)**


\---

## 📌 Problem Statement

As video creators and media companies increasingly rely on platforms like YouTube for income, predicting potential ad revenue becomes essential for business planning and content strategy. This project builds a **Lasso Regression model** that estimates YouTube ad revenue for individual videos based on performance and contextual features, deployed through a Streamlit web application.

\---

## 🌐 Live App

🔗 [YouTube Ad Revenue Predictor](https://youtubecontentmonetizationmodeler-3ddh53xessm6tsi38xsy7u.streamlit.app)

Enter video metrics (views, likes, watch time, category, country, device) and get an instant ad revenue estimate, along with visual insights on what drives revenue.

\---

## 📁 Project Structure

```
youtube-content-monetization-modeler/
|-- app.py                          # Streamlit web application
|-- notebook.ipynb                  # Full analysis: EDA, preprocessing, modelling
|-- best_model.pkl                  # Trained Lasso regression model
|-- scaler.pkl                      # Fitted StandardScaler
|-- encoders.pkl                    # Fitted LabelEncoders for categorical features
|-- requirements.txt                # Python dependencies
|-- youtube_ad_revenue_dataset.csv  # Dataset
|-- README.md                       # Project documentation
```

\---

## 📊 Dataset

|Property|Details|
|-|-|
|Name|YouTube Monetization Modeler|
|Source|Synthetic, created for learning purposes|
|Size|\~122,000 rows|
|Format|CSV|
|Target Variable|`ad\_revenue\_usd`|

**Features:**

|Column|Description|
|-|-|
|`video\_id`|Unique video identifier|
|`date`|Upload / report date|
|`views`|Total view count|
|`likes`|Total likes|
|`comments`|Total comments|
|`watch\_time\_minutes`|Total watch time in minutes|
|`video\_length\_minutes`|Duration of the video|
|`subscribers`|Channel subscriber count|
|`category`|Content category (Gaming, Music, Tech, etc.)|
|`device`|Primary viewing device|
|`country`|Viewer country|
|`ad\_revenue\_usd`|Ad revenue generated — **target variable**|

> Dataset included in this repository: `dataset.csv`


\---

## ⚙️ Methodology

### 1\. Exploratory Data Analysis (EDA)

* Univariate analysis: distributions of all numerical and categorical features
* Bivariate analysis: correlation heatmap, scatter plots, grouped boxplots
* Outlier detection using the IQR method across all key numerical columns

### 2\. Preprocessing

* Imputed \~5% missing values (median for numerical, mode for categorical)
* Removed \~2% duplicate records
* Applied IQR-based capping (Winsorization) to handle outliers without losing valid high-performing video data

### 3\. Feature Engineering

|Feature|Formula|
|-|-|
|`engagement\_rate`|`(likes + comments) / (views + 1)`|
|`watch\_ratio`|`watch\_time\_minutes / (video\_length\_minutes + 0.1)`|
|`likes\_per\_view`|`likes / (views + 1)`|
|`month`|Extracted from `date`|
|`day\_of\_week`|Extracted from `date`|

### 4\. Modelling

Five regression models were trained and compared:

|Model|R²|RMSE|MAE|
|-|-|-|-|
|**Lasso Regression** ✅|**0.9526**|**13.478**|**3.083**|
|Ridge Regression|0.9526|13.479|3.093|
|Linear Regression|0.9526|13.479|3.096|
|Gradient Boosting|0.9523|13.521|3.636|
|Random Forest|0.9504|13.786|3.575|

**Lasso Regression** was selected as the final model based on the lowest MAE (3.083). All linear models outperformed tree-based ensembles, confirming that the relationship between video performance metrics and ad revenue is predominantly linear — consistent with YouTube's CPM-based ad monetisation system.

\---

## 🔍 Key Insights

* **Views and watch time** are the strongest predictors of ad revenue, confirming that reach and audience retention are the primary monetisation drivers.
* **Engagement rate** (engineered feature) adds meaningful signal beyond raw view count — audience quality matters alongside quantity.
* **Category, device, and country** have relatively minor influence on revenue compared to engagement metrics.
* Lasso's L1 regularisation automatically eliminated low-signal features, providing built-in feature selection.

\---

## 🖥️ Streamlit App Features

**Tab 1 — 💰 Predict Revenue**

* Input form for all video performance metrics
* Instant revenue prediction using the trained Lasso model
* Expandable section showing engineered features used for the prediction

**Tab 2 — 📊 Visual Insights**

* Lasso coefficient chart showing which features drive revenue up or down
* Average revenue breakdowns by Category, Device, and Country

\---

## 🚀 Run Locally

**1. Clone the repository**

```bash
git clone https://github.com/akshayavk8/youtube-content-monetization-modeler.git
cd youtube-content-monetization-modeler
```

**2. Install dependencies**

```bash
pip install -r requirements.txt
```

**3. Run the app**

```bash
streamlit run app.py
```

\---

## 🛠️ Tech Stack

* **Language:** Python
* **Data manipulation:** Pandas, NumPy
* **Machine learning:** Scikit-learn (Lasso, Ridge, LinearRegression, RandomForest, GradientBoosting)
* **Visualisation:** Matplotlib, Seaborn, Plotly
* **Web app:** Streamlit
* **Model persistence:** Joblib
* **Development environment:** Google Colab

\---

## 👩‍💻 Author

**Akshayaa Vinod Kumar**  
Marine Biologist & Data Science Practitioner  
HCL GUVI — Data Science with ML & AI Certification

- 🔗 [LinkedIn](https://linkedin.com/in/akshayavinodkumar)
- 🐙 [GitHub](https://github.com/akshayavk8)

---

*This project was completed as part of the GUVI Data Science with ML & AI certification capstone.*
