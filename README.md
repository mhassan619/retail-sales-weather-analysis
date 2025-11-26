"""
This script creates two GitHub-ready files for the "Retail Sales & Weather Insights" project:

1) `Retail_Sales_Weather_Project.ipynb` - a Jupyter notebook ready to upload to GitHub.
2) `README.md` - a project README suitable for the repo front page.

Run this script in your local machine (or copy/paste cells into a new notebook). It will write both files to the current directory.

Files produced contain: dataset creation (if you don't have CSV), full analysis (Pandas), Matplotlib plots saved to ./plots, and final insights.

NOTE: This is a generator script. After running it, open the produced `.ipynb` in Jupyter/VS Code to run cells interactively.
"""

import json
import nbformat
from nbformat.v4 import new_notebook, new_code_cell, new_markdown_cell

# README content (markdown)
README = r"""
# Retail Sales & Weather Insights

**Description**

This is a compact, reproducible project that demonstrates how to use **Pandas** for data cleaning and analysis and **Matplotlib** for publication-quality visualizations. The dataset contains daily retail transactions combined with weather information so you can explore seasonal trends, product performance, customer behavior, and weather impact on sales.

**What you'll find in this repo**

- `Retail_Sales_Weather_Project.ipynb` — Jupyter notebook with step-by-step analysis and plots.
- `sales_weather_cleaned.csv` — cleaned dataset produced by the notebook (created when you run the notebook).
- `plots/` — folder where the notebook saves PNGs of the main charts (monthly revenue, product revenue, time-series with rolling average, scatter fit, correlation heatmap, boxplots).

**Skills demonstrated**

- Data cleaning & type conversion (datetime, numeric)
- Feature engineering (Revenue, Year, Month, DayOfWeek, WeekOfYear)
- Aggregations & GroupBy (yearly/monthly/product/customer)
- Time-series resampling and rolling windows
- Correlation analysis and weather impact
- Publication-quality plotting with Matplotlib

**How to run**

1. Clone the repo or download files to your local machine.
2. Create and activate a Python environment (recommended: conda).

```bash
conda create -n ml python=3.10 -y
conda activate ml
pip install pandas matplotlib numpy nbformat
```

3. Open `Retail_Sales_Weather_Project.ipynb` in Jupyter Notebook / VS Code and run all cells.

**Output**

- `sales_weather_cleaned.csv` generated in the notebook.
- PNG files saved under `plots/`.
- A printed list of short insights (ready to include in LinkedIn post).

**License**: MIT

"""

# Notebook cells
cells = []

# 1: Title markdown
cells.append(new_markdown_cell("""# Retail Sales & Weather Insights\n\n**Pandas + Matplotlib project**\n\nThis notebook runs a complete analysis: data creation (or load), cleaning, feature engineering, EDA, time-series aggregation, visualization, and final insights. Run each cell sequentially (Shift+Enter)."""))

# 2: Dataset creation / load markdown
cells.append(new_markdown_cell("""## 1. Load or create dataset\n\nIf you already have `sales_weather.csv`, replace the creation cell and use `pd.read_csv('sales_weather.csv')`. Otherwise the cell below creates the example dataset used in this project."""))

# 3: Code cell: create dataframe and save csv
create_data_code = r"""
import pandas as pd
from io import StringIO

csv_text = '''Date,Store,Product,CustomerID,Region,Units_Sold,Price,Weather,Temperature
2021-01-05,Store_A,Bread,1001,North,20,2.5,Sunny,15
2021-01-06,Store_A,Milk,1002,North,12,1.8,Cloudy,12
2021-01-07,Store_A,Eggs,1003,North,30,3.2,Sunny,16
2021-01-12,Store_A,Bread,1004,North,18,2.5,Sunny,17
2021-01-15,Store_A,Milk,1001,North,10,1.8,Rainy,11
2021-02-03,Store_A,Eggs,1005,North,35,3.2,Sunny,18
2021-02-10,Store_A,Bread,1002,North,25,2.7,Sunny,19
2021-02-12,Store_A,Milk,1006,North,15,1.9,Cloudy,14
2021-03-01,Store_A,Eggs,1003,North,40,3.5,Sunny,20
2021-03-10,Store_A,Bread,1007,North,22,2.8,Rainy,13
2021-03-15,Store_A,Milk,1008,North,18,2.0,Cloudy,15
2021-04-02,Store_A,Eggs,1009,North,45,3.6,Sunny,21
2021-04-10,Store_A,Bread,1010,North,28,3.0,Sunny,22
2021-04-15,Store_A,Milk,1003,North,20,2.1,Cloudy,16
2021-05-01,Store_A,Eggs,1001,North,50,3.8,Sunny,25
2021-05-05,Store_A,Bread,1005,North,30,3.0,Sunny,24
2021-05-09,Store_A,Milk,1011,North,22,2.2,Rainy,18
2021-06-01,Store_A,Eggs,1012,North,55,4.0,Sunny,27
2021-06-07,Store_A,Bread,1013,North,32,3.2,Cloudy,23
2021-06-12,Store_A,Milk,1007,North,25,2.3,Sunny,26
2021-07-01,Store_A,Eggs,1002,North,60,4.2,Sunny,30
2021-07-05,Store_A,Bread,1004,North,35,3.5,Sunny,29
2021-07-08,Store_A,Milk,1014,North,28,2.5,Cloudy,24
2021-08-01,Store_A,Eggs,1015,North,65,4.5,Sunny,31
2021-08-10,Store_A,Bread,1001,North,40,3.6,Rainy,20
2021-08-15,Store_A,Milk,1016,North,30,2.6,Sunny,28
2021-09-01,Store_A,Eggs,1003,North,70,4.6,Sunny,32
2021-09-07,Store_A,Bread,1008,North,38,3.7,Cloudy,25
2021-09-12,Store_A,Milk,1012,North,35,2.8,Sunny,27
2021-10-01,Store_A,Eggs,1010,North,72,4.8,Sunny,29
'''

# load into dataframe
df = pd.read_csv(StringIO(csv_text))
# save a copy
df.to_csv('sales_weather.csv', index=False)
print('Created sales_weather.csv with', df.shape[0], 'rows')
df.head()
"""
cells.append(new_code_cell(create_data_code))

# 4: Data cleaning markdown
cells.append(new_markdown_cell('''## 2. Cleaning & Type Conversion
Convert the Date column, ensure numeric columns are numeric, check/fill missing values.'''))

# 5: Code cell cleaning
clean_code = r"""
# convert and coerce types
df['Date'] = pd.to_datetime(df['Date'])
df['Units_Sold'] = pd.to_numeric(df['Units_Sold'], errors='coerce')
df['Price'] = pd.to_numeric(df['Price'], errors='coerce')
df['Temperature'] = pd.to_numeric(df['Temperature'], errors='coerce')

# missing values (this sample has none, but keep practice)
print('Missing values before fill:')
print(df.isnull().sum())

# fill rules
df['Units_Sold'].fillna(df['Units_Sold'].mean(), inplace=True)
df['Price'].fillna(df['Price'].median(), inplace=True)
df['Weather'].fillna(df['Weather'].mode()[0], inplace=True)
df['Temperature'].fillna(df['Temperature'].mean(), inplace=True)

print('\nMissing values after fill:')
print(df.isnull().sum())

# basic info
print('\nData types:')
print(df.dtypes)
"""
cells.append(new_code_cell(clean_code))

# 6: Feature engineering markdown
cells.append(new_markdown_cell('''## 3. Feature Engineering
Create Year, Month, DayOfWeek, WeekOfYear and Revenue columns.'''))

# 7: Feature engineering code
feat_code = r"""
df['Year'] = df['Date'].dt.year
df['Month'] = df['Date'].dt.month
df['DayOfWeek'] = df['Date'].dt.day_name()
df['WeekOfYear'] = df['Date'].dt.isocalendar().week
df['Revenue'] = df['Units_Sold'] * df['Price']

print(df[['Date','Product','Units_Sold','Price','Revenue']].head())
"""
cells.append(new_code_cell(feat_code))

# 8: EDA markdown
cells.append(new_markdown_cell('''## 4. Exploratory Data Analysis
Yearly/monthly aggregates, product & customer analysis, weather impact and correlation.'''))

# 9: EDA code
eda_code = r"""
# Aggregates
yearly_revenue = df.groupby('Year')['Revenue'].sum().sort_index()
monthly_revenue = df.groupby(['Year','Month'])['Revenue'].sum()
product_revenue = df.groupby('Product')['Revenue'].sum().sort_values(ascending=False)
top_customers = df.groupby('CustomerID')['Revenue'].sum().sort_values(ascending=False).head(5)
weather_revenue = df.groupby('Weather')['Revenue'].mean()
corr = df[['Units_Sold','Price','Temperature','Revenue']].corr()

print('Yearly revenue:\n', yearly_revenue)
print('\nTop products:\n', product_revenue)
print('\nTop customers:\n', top_customers)
print('\nAvg revenue by weather:\n', weather_revenue)
print('\nCorrelation matrix:\n', corr)
"""
cells.append(new_code_cell(eda_code))

# 10: Time series markdown
cells.append(new_markdown_cell('''## 5. Time-series & Rolling
Resample to monthly and calculate a 7-day rolling average for Units_Sold.'''))

# 11: Time-series code
ts_code = r"""
ts = df.set_index('Date').sort_index()
daily_revenue = ts['Revenue'].resample('D').sum()
monthly_revenue_ts = ts['Revenue'].resample('M').sum()
rolling_7 = ts['Units_Sold'].rolling(window=7, min_periods=1).mean()

print('Monthly revenue (time-series):\n', monthly_revenue_ts)
print('\nSample rolling 7-day Units_Sold:\n', rolling_7.head(10))
"""
cells.append(new_code_cell(ts_code))

# 12: Plotting markdown
cells.append(new_markdown_cell('''## 6. Visualizations (Matplotlib)
Plots are saved in `plots/`. Each plot cell also displays the figure inline.'''))

# 13: Plotting code cell (multiple plots)
plot_code = r"""
import matplotlib.pyplot as plt
import numpy as np
import os
os.makedirs('plots', exist_ok=True)

# Plot A: Monthly revenue bar chart
plt.figure(figsize=(8,5))
monthly_revenue_ts.plot(kind='bar')
plt.title('Monthly Revenue')
plt.xlabel('Month')
plt.ylabel('Revenue')
plt.tight_layout()
plt.savefig('plots/monthly_revenue.png', dpi=300)
plt.show()

# Plot B: Product revenue (horizontal bar)
plt.figure(figsize=(8,4))
product_revenue.plot(kind='barh')
plt.title('Product Revenue (total)')
plt.xlabel('Revenue')
plt.tight_layout()
plt.savefig('plots/product_revenue.png', dpi=300)
plt.show()

# Plot C: Time series daily revenue (line) + 7-day rolling Units_Sold
plt.figure(figsize=(10,5))
plt.plot(daily_revenue.index, daily_revenue.values, label='Daily Revenue', marker='o')
plt.plot(rolling_7.index, rolling_7.values, label='7-day avg Units_Sold', linestyle='--')
plt.legend()
plt.title('Daily Revenue and 7-day avg Units_sold')
plt.xlabel('Date')
plt.ylabel('Value')
plt.tight_layout()
plt.savefig('plots/daily_revenue_and_rolling.png', dpi=300)
plt.show()

# Plot D: Scatter Units_Sold vs Temperature + simple linear fit
plt.figure(figsize=(7,5))
x = df['Temperature']
y = df['Units_Sold']
plt.scatter(x, y, alpha=0.7)
# linear fit
m, b = np.polyfit(x, y, 1)
plt.plot(x, m*x + b, color='red', linewidth=2, label=f'fit: y={m:.2f}x+{b:.2f}')
plt.title('Units_Sold vs Temperature')
plt.xlabel('Temperature')
plt.ylabel('Units_Sold')
plt.legend()
plt.tight_layout()
plt.savefig('plots/units_vs_temp.png', dpi=300)
plt.show()

# Plot E: Correlation heatmap
plt.figure(figsize=(5,4))
plt.imshow(corr, cmap='coolwarm', interpolation='nearest')
plt.colorbar()
plt.xticks(range(len(corr.columns)), corr.columns)
plt.yticks(range(len(corr.columns)), corr.columns)
plt.title('Correlation Matrix')
plt.tight_layout()
plt.savefig('plots/correlation_heatmap.png', dpi=300)
plt.show()

# Plot F: Boxplot Units_Sold by Product
plt.figure(figsize=(7,5))
products = df['Product'].unique()
data_to_plot = [df[df['Product']==p]['Units_Sold'] for p in products]
plt.boxplot(data_to_plot, labels=products)
plt.title('Units_Sold distribution by Product')
plt.xlabel('Product')
plt.ylabel('Units_Sold')
plt.tight_layout()
plt.savefig('plots/boxplot_units_by_product.png', dpi=300)
plt.show()

print('Plots saved to ./plots')
"""
cells.append(new_code_cell(plot_code))

# 14: Insights markdown
cells.append(new_markdown_cell('''## 7. Insights (example)

- **Top product by revenue:** Eggs
- **Top customer by revenue:** CustomerID shown in top_customers
- **Weather impact:** Sunny days show higher average revenue
- **Temperature correlation:** small positive correlation with Units_Sold

Use these bullet points as a starting point for a LinkedIn post.
'''))

# 15: Save cleaned CSV cell
cells.append(new_code_cell("""# Save cleaned dataframe (already saved earlier but safe to save again)
df.to_csv('sales_weather_cleaned.csv', index=False)
print('Saved sales_weather_cleaned.csv')
"""))

# Build the notebook object
nb = new_notebook(cells=cells, metadata={"kernelspec": {"name": "python3", "display_name": "Python 3"}, "language_info": {"name": "python"}})

# Write notebook to file
nb_filename = 'Retail_Sales_Weather_Project.ipynb'
with open(nb_filename, 'w', encoding='utf-8') as f:
    nbformat.write(nb, f)

# Write README
with open('README.md', 'w', encoding='utf-8') as f:
    f.write(README)

print(f'Created {nb_filename} and README.md in the current directory.')