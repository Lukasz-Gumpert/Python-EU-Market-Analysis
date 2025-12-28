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

# Analysis:

## 1. Data Cleanup:

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
