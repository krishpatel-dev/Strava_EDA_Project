# Strava Fitness & Health Data: Exploratory Data Analysis (EDA)

![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-3776AB?style=for-the-badge)
![Plotly](https://img.shields.io/badge/Plotly-Interactive%20Charts-3F4F75?style=for-the-badge&logo=plotly&logoColor=white)

---

## Project Overview

**Strava, Inc.** is a leading fitness tracking and social networking platform headquartered in San Francisco, California. Millions of runners, cyclists, and athletes globally rely on Strava to track workouts using GPS data, analyze performance metrics, and engage with a vibrant athletic community.

This project performs an extensive **Exploratory Data Analysis (EDA)** on multi-dimensional user fitness, activity intensity, calorie burn, heart rate, weight, and sleep datasets. By merging daily, hourly, and minute-level fitness tracking telemetry, the analysis uncovers key behavioral patterns, activity trends, correlation dynamics, and actionable business strategies to boost user retention and premium subscription adoption.

---

## Business Objectives

1. **User Activity & Behavioral Pattern Analysis:** Understand how users distribute daily steps, active distance, and intensity levels across different workout routines.
2. **Passive vs. Active Tracking Gap Identification:** Analyze friction points where users record passive daily steps but fail to log active manual workouts on the app.
3. **Subscription Growth & Monetization:** Discover data-driven opportunities to convert free users into paid Strava Subscription (Summit) members.
4. **Health & Recovery Feature Expansion:** Evaluate underutilized features like sleep monitoring and weight logs to enhance holistic health tracking.

---

## Dataset Architecture & Data Pipeline

The project integrates **18 multi-granular fitness tracking datasets** collected from wearable sensors and smart devices:

### Summary of Key Datasets

| Dataset File | Primary Metrics | Granularity |
| :--- | :--- | :--- |
| dailyActivity_merged.csv | Total Steps, Distance, Active Minutes, Calories | Daily |
| dailyCalories_merged.csv | Energy Expenditure (kcal) | Daily |
| dailyIntensities_merged.csv | Very / Fairly / Lightly Active / Sedentary Minutes | Daily |
| dailySteps_merged.csv | Total Step Count | Daily |
| sleepDay_merged.csv | Total Sleep Records, Total Minutes Asleep, Time in Bed | Daily |
| weightLogInfo_merged.csv | Weight (kg/lbs), BMI, Manual vs. Sync Log Flag | Periodic |
| heartrate_seconds_merged.csv | Heart Rate (BPM) telemetry | Seconds |
| hourlySteps_merged.csv / hourlyCalories_merged.csv | Hourly Step & Calorie Trends | Hourly |
| minuteStepsNarrow_merged.csv / minuteMETsNarrow_merged.csv | High-Resolution Activity & METs Telemetry | Minute |

### Data Merging Pipeline
The primary analytical dataset (md) is created by executing an **outer merge pipeline** across Id and timestamp dimensions (ActivityDate, ActivityDay, SleepDay, Date), synthesizing daily activity, intensities, steps, calories, sleep logs, and weight metrics into a unified dataframe.

---

## Key Analytical Insights

```text
                   Correlation Highlights Across Fitness Metrics
   +-----------------------------------------------+----------------+
   | Metric Pair                                   | Pearson (r)    |
   +-----------------------------------------------+----------------+
   | Total Distance  <->  Total Steps              |  0.98 (Strong) |
   | Moderately Active Distance <-> Fairly Active  |  0.97 (Strong) |
   | Very Active Distance  <->  Very Active Min    |  0.88 (Strong) |
   +-----------------------------------------------+----------------+
```

1. **Step Count & Distance Thresholds:**
   - Most active users cluster around **8,000 to 14,000 steps** daily.
   - Average active distance covered by regular users sits between **5 km and 10 km**.

2. **The Passive-Active Logging Disconnect:**
   - High step counts are logged automatically via background phone sensors, but LoggedActivitiesDistance (manual workout logging) remains close to zero for a majority of users. Users leave the app running passively rather than starting explicit workout sessions.

3. **Sleep Telemetry Under-Indexing:**
   - Sleep tracking dataset records only **33 complete sleep logs**, indicating low user adoption of sleep and recovery monitoring features compared to step tracking.

4. **Basal Metabolic Rate (BMR) & Calorie Distribution:**
   - Even when users record 0 steps, baseline daily calorie expenditure centers between **1,496 kcal and 1,982 kcal**, accurately capturing baseline human BMR.

---

## Strategic Business Recommendations

1. **Automated Active Workout Detection & Prompts:**
   - Implement smart background detection (e.g., *'Looks like you completed a 5km run! Tap to log on Strava'*) to bridge the gap between passive step counts and active workout logs.

2. **Milestone-Based Premium Subscription Rewards:**
   - Offer 7-day free trial passes or discounts on **Strava Premium** when users achieve consistency milestones (e.g., maintaining a 10,000-step streak or 10 km distance streak for 7 consecutive days).

3. **Gamified Community Challenges & Badges:**
   - Introduce monthly distance milestone challenges (e.g., *'Break the 10km Distance Barrier'*) to nudge users currently plateauing at the 5-6 km threshold.

4. **Integrated Sleep & Recovery Score:**
   - Build a unified **Daily Recovery Index** combining sleep duration with daily METs/intensity to encourage daily morning app opens and increase sleep log logging.

---

## Repository Structure

```text
Strava Health Project/
├── Strava_EDA_Project.ipynb          # Comprehensive Jupyter notebook with full EDA & visualizations
├── .gitignore                        # Custom Git ignore file tailored for Python & Data Science
├── README.md                         # Detailed project documentation
├── dailyActivity_merged.csv          # Daily activity summary dataset
├── dailyCalories_merged.csv          # Daily calorie expenditure dataset
├── dailyIntensities_merged.csv       # Daily activity intensity breakdown dataset
├── dailySteps_merged.csv             # Daily step totals dataset
├── sleepDay_merged.csv               # Sleep records and duration dataset
├── weightLogInfo_merged.csv          # Weight and BMI log dataset
└── [High-Resolution Datasets]        # Minute/Hourly/Second-level steps, calories, heart rate CSVs
```

---

## Installation & Setup Guide

### Prerequisites
- **Python 3.8+**
- **Jupyter Notebook** or **JupyterLab** / **VS Code**

### 1. Clone the Repository
```bash
git clone https://github.com/krishpatel-dev/Strava_EDA_Project.git
cd Strava_EDA_Project
```

### 2. Create and Activate Virtual Environment
```bash
# On Windows
python -m venv venv
.\venv\Scripts\activate

# On macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Required Dependencies
```bash
pip install pandas numpy matplotlib seaborn plotly scikit-learn missingno wordcloud statsmodels geopandas
```

### 4. Launch Jupyter Notebook
```bash
jupyter notebook Strava_EDA_Project.ipynb
```

