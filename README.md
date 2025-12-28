<p align="left">
  <img src="Python-EU-Market-Analysis\assets\image-1.png" width="150" alt='python'/>
  <img src="Python-EU-Market-Analysis\assets\image-2.png" width="150" alt='seaborn'/>
  <img src="Python-EU-Market-Analysis\assets\image-3.png" width="150" alt='matplotlib'/>
</p>

# Python-EU-Market-Analysis
Python-EU-Market-Analysis is a data analysis project focused on exploring the data job market across the European Union using Python. The project leverages libraries such as pandas, seaborn, and matplotlib to clean data, uncover trends, and visualize insights about demand, skills, and salaries in the EU tech sector.

# Technologies & Tools Utilized:

- Python (NumPy, pandas, Matplotlib, Seaborn)

- Visual Studio Code

- Git & GitHub

# Data Cleanup:

To ensure the analysis was reliable, comparable across datasets, and suitable for visualization, several preprocessing steps were applied to the European job postings data. These transformations focused on filtering relevant records, normalizing data structures, and deriving analytical metrics needed for later insights.

### Import & Clean Up Data:

```py
# Load data & initial setup
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import ast

from datasets import load_dataset

# Load dataset
data = load_dataset('lukebarousse/data_jobs')
df = data['train'].to_pandas()

# Convert job posted date column to datetime
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])

# Convert skills column from string to list
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```
Because this analysis is centered specifically on the European market, the dataset first had to be geographically filtered. A predefined list of European countries was used to extract only the relevant job postings.

```py
# Filter Dataframe by EU countsry
eu_list = [
    "Albania", "Andorra", "Austria", "Belgium", "Belarus",
    "Bosnia and Herzegovina", "Bulgaria", "Croatia", "Montenegro",
    "Czech Republic", "Denmark", "Estonia", "Finland", "France",
    "Greece", "Spain", "Netherlands", "Ireland", "Iceland", "Kosovo",
    "Liechtenstein", "Lithuania", "Luxembourg", "Latvia",
    "North Macedonia", "Malta", "Moldova", "Monaco", "Germany",
    "Norway", "Poland", "Portugal", "Romania", "Russia",
    "San Marino", "Serbia", "Slovakia", "Slovenia", "Switzerland",
    "Sweden", "Turkey", "Ukraine", "Vatican City", "Hungary",
    "United Kingdom", "Italy"
]


df_eu = df.copy()
df_eu = df_eu[df_eu['job_location'].isin(eu_list)]
```
# Analysis:

Each Jupyter Notebook in this repository is designed with a clear analytical purpose. Every file answers one specific research question related to the European Data Analyst job market. By structuring the analysis into focused, question-driven
notebooks, the results become easier to interpret, compare, and reuse in future work.

## Research Focus: Market Dynamics & Key Players (01 - EDA.ipynb)

The primary objective of this specific analysis is to perform an Exploratory Data Analysis (EDA) to understand the current landscape of the European data job market. By leveraging the cleaned dataset, this section aims to answer critical questions regarding job distribution and employer dominance within the EU.

### Job Distribution by Country: 
Identifying which European nations offer the highest volume of opportunities for data professionals.

ZDJECIE


*Market Dominance: The bar chart reveals that a significant majority of job postings are concentrated in a few major economies (such as France, Germany, and the United Kingdom), which act as the primary engines for the data job market in Europe.

*Emerging Hubs: Beyond the top leaders, the chart shows substantial activity in countries like Poland, Spain, and the Netherlands, indicating a growing demand for data professionals in Central and Western Europe.

*Regional Fragmentation: While the top 5-10 countries represent the bulk of the volume, the "long tail" of the chart highlights that many other European nations have a much smaller, more fragmented job market.

Top Employers: Identifying the most active companies currently hiring in the European market to highlight key industry players.

Job Roles and Requirements: Evaluating the prevalence of different job titles (e.g., Data Analyst, Data Engineer) and the frequency of degree requirements in postings.
