<div align="center">

# 📊 RETAIL SALES & WEATHER INSIGHTS
### 🚀 End-to-End Data Analytics Pipeline: Cleaning, Feature Engineering & Advanced Exploratory Visualizations

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas" />
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy" />
  <img src="https://img.shields.io/badge/Matplotlib-Data%20Viz-Success?style=for-the-badge&color=3478F6" alt="Matplotlib" />
</p>

---

[💻 Main GitHub Portfolio](https://github.com/mhassan619) • [💼 LinkedIn Profile](https://www.linkedin.com/in/muhammad-hassan-python)

</div>

---

## 📋 Project Overview

This repository features a compact, reproducible **Data Analytics & Business Intelligence Engine**. It analyzes transactional retail behavior coupled with seasonal atmospheric weather matrices to determine outward impacts on corporate revenue. 

The project demonstrates a complete production-grade data lifecycle—handling asynchronous CSV streams, cleaning data distributions, executing conditional aggregations, and exporting high-resolution charts.

---

## 🛠️ Data Engineering & Analytical Flow

The Jupyter pipeline (`Retail_Sales_Weather_Project.ipynb`) executes the following operations step-by-step:

1. **🧹 Data Scrubbing & Typology Normalization:** 
   * Formats raw structural blocks into structured `datetime64` dimensions.
   * Isolates numerical data attributes and runs defensive `fillna()` routing rules (Mean/Median/Mode imputation) to prevent analytical bias.
2. **⚙️ Deep Feature Engineering:** 
   * Extracts localized timestamp dimensions (`Year`, `Month`, `DayOfWeek`, `WeekOfYear`).
   * Generates dynamic target metrics (`Revenue = Units_Sold * Price`).
3. **📈 Time-Series Resampling & Rolling Analytics:** 
   * Tracks daily and monthly operational income trends.
   * Computes a **7-Day Rolling Window Average** for `Units_Sold` to screen out seasonal spikes and trace actual customer demand patterns.
4. **🔬 Statistical Correlation & Trend Fitting:** 
   * Generates mathematical covariance matrices between volumes, price elasticities, and temperatures.
   * Injects a **Linear Polyfit Regression Line** ($y = mx + c$) to model exact sales movements relative to temperature changes.

---

## 📂 Project Structure & Visual Deliverables

```text
Retail_Sales_Weather_Project/
│
├── Retail_Sales_Weather_Project.ipynb  # Comprehensive Jupyter Analysis Pipeline
├── sales_weather.csv                  # Raw incoming transactional matrix
├── sales_weather_cleaned.csv          # Cleaned, engineered production-ready dataset
│
└── plots/                             # Publication-Quality Exported Charts (PNG)
    ├── monthly_revenue.png            # Aggregated monthly financial distributions
    ├── product_revenue.png            # Horizontal business performance rankings
    ├── daily_revenue_and_rolling.png # 7-day smoothed demand curve comparison
    ├── units_vs_temp.png              # Scatter trend plot with linear regression fit
    ├── correlation_heatmap.png        # Color-mapped feature interaction matrix
    └── boxplot_units_by_product.png   # Statistical density & quartile outlier metrics

```
## 🛠️ Technical Stack & Dependencies
 * **Data Manipulation:** Pandas (Vectorized logic, data alignment, type casting, and group-by aggregations)
 * **Mathematical Operations:** NumPy (Polynomial trend fitting array processing)
 * **Exploratory Visualizations:** Matplotlib (Heatmaps, subplots, line formatting, and high-DPI rendering)
 * **Environment Base:** Jupyter / VS Code (Notebook runtime parsing)
## 💻 Local Replication & Setup
Follow these commands to configure the analytics environment and replicate the visualizations locally:
 1. **Clone the Repository Space:**
```bash
   git clone [https://github.com/mhassan619/Projects.git](https://github.com/mhassan619/Projects.git)
   cd Projects  # Navigate to this project folder

```
 2. **Environment Activation & Dependency Loading:**
```bash
   # Recommended virtual setup
   python -m venv env
   source env/bin/activate  # Windows: env\Scripts\activate
   
   # Install required core packages
   pip install pandas matplotlib numpy nbformat notebook

```
 3. **Launch the Notebook Runtime:**
```bash
   jupyter notebook Retail_Sales_Weather_Project.ipynb

```
*Execute all blocks sequentially (Shift + Enter) to regenerate production datasets and plots.*
## 🎯 Generated Key Business Insights
 * **💡 Peak Driver:** **Eggs** yield the highest overall aggregated structural revenue.
 * **💡 Weather Influence:** Weather pattern profiling explicitly shows **Sunny Days** command a significantly higher mean profit margin compared to rainy/cloudy periods.
 * **💡 Temperature Correlation:** A localized positive linear covariance exists, proving transactional unit sales volume climbs gracefully alongside temperature increases.
<div align="center">
### 🌱 Turning Raw Data Arrays into Actionable Business Strategies.
📩 Data Operations Queries • 🌐 Connect Networks via LinkedIn
</div>
