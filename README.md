<p align="left">
  <img src="Python-EU-Market-Analysis\assets\image-1.png" width="150" alt='python'/>
  <img src="Python-EU-Market-Analysis\assets\image-2.png" width="150" alt='seaborn'/>
  <img src="Python-EU-Market-Analysis\assets\image-3.png" width="150" alt='matplotlib'/>
</p>

# Python-EU-Market-Analysis
Python-Europe-Market-Analysis is a data analysis project focused on exploring the data job market across the Europe using Python. The project leverages libraries such as pandas, seaborn, and matplotlib to clean data, uncover trends, and visualize insights about demand, skills, and salaries in the EU tech sector.

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

## Market Dynamics & Key Players (01 - EDA.ipynb)

The primary objective of this specific analysis is to perform an Exploratory Data Analysis (EDA) to understand the current landscape of the European data job market. By leveraging the cleaned dataset, this section aims to answer critical questions regarding job distribution and employer dominance within the EU.

### Job Distribution by Country: 
Identifying which European nations offer the highest volume of opportunities for data professionals.

<img src="Python-EU-Market-Analysis\assets\01_Top_10_eu_countries.png" alt='European countries with most data job postings'>

* Market Leadership: The UK, France, and Italy dominate the European market, with the UK leading significantly at nearly 2,000 job postings.

* Regional Demand Disparity: There is a sharp decline in volume after the top three, with mid-tier markets like Spain and Germany offering roughly 50-60% fewer opportunities.

* Tech Hub Density: While smaller nations like Luxembourg and the Netherlands have lower absolute counts (~500), they show high demand relative to their market size.

## Benefits and Requirements
Next, I explored key job requirements and benefits for Data Analyst roles using pie chart visualizations to identify industry standards.

<img src="Python-EU-Market-Analysis\assets\02_Requirement_exploration.png" alt='Requirements exploration.png'>

* Dominance of Remote Work: Remote flexibility is nearly universal in the field, with 91.1% of job postings confirming that remote work is possible.

* Education Requirements: A university degree remains a significant barrier to entry, as it is required by 69.4% of employers.

* Standardized Benefits: Health insurance is a highly consistent offering across the market, included in 89.0% of the analyzed job descriptions.

### Top Employers: 
Lastly identifying the most active companies currently hiring in the European market to highlight key industry players.

<img src="Python-EU-Market-Analysis\assets\03_Top_10_companies.png" alt='Top 10 companies'>

* Dominance of "Confidenziale": The largest share of postings comes from "Confidenziale" (over 500 listings), which typically represents confidential recruitment agencies masking client identities.

* Recruitment Agency Presence: Professional staffing firms like JobLeads GmbH, Hays, and Randstad feature prominently, indicating that a significant portion of the market is managed by third-party recruiters.

* Key Corporate Employers: Major industry players such as Allegro, Banco Santander, and SAFRAN emerge as the top direct corporate employers actively seeking data talent.

## Technical Skill Requirements (02 - Skills_Count.ipynb)

Next, I analyzed the most frequently requested skills for three core data roles to identify the essential technical competencies in the current market.

<img src="Python-EU-Market-Analysis\assets\04_Skill_requested.png" alt='Most requested skills'>

* Universal Importance of SQL and Python: SQL is a foundational requirement across all roles, peaking at 56% for Data Engineers, while Python is the most critical skill for Data Scientists at 60%.

* Distinct Analyst Toolkit: For Data Analysts, the stack is uniquely characterized by a blend of SQL (43%) and visualization or spreadsheet tools like Excel (30%) and Power BI (23%).

* Cloud and Infrastructure Focus: Data Engineering roles show a much higher demand for cloud platforms and big data tools, specifically Azure (35%), AWS (28%), and Spark (27%).

## Technical Skill Trends in European markekt (03 - skill_trend.ipynb)

Technical Skill Requirements:

In this part I analyzed the most frequently requested skills for three core data roles to identify the essential technical competencies in the current market.

<img src="Python-EU-Market-Analysis\assets\05_skill_trend.png" alt='Skill trends'>

* Universal Importance of SQL and Python: SQL remains the industry standard database language and is a foundational requirement across all data roles, while Python is highly sought-after for its flexibility in data cleaning and advanced analysis.

* Distinct Analyst Toolkit: For Data Analysts, the technical stack is uniquely characterized by a blend of SQL for data retrieval and visualization or spreadsheet tools like Excel and Power BI for reporting.

* Infrastructure and Advanced Analytics: Data Engineering and Scientist roles show a higher demand for specialized skills such as Cloud platforms (AWS/Azure) and Machine Learning, which are increasingly identified as key components for high-impact data professional toolkits.

## Salary Distribution Analysis:

Finally, I analyzed the yearly salary distribution across different data roles in Europe to understand the earning potential within each specialization.

<img src="Python-EU-Market-Analysis\assets\06_data_salary_distribution" alt='Salary distribution'>

* Highest Median Salary: Data Engineers command the highest median yearly salary in Europe, followed closely by Data Scientists, both of which significantly outperform the Data Analyst role.

* Significant Salary Variance: Data Scientists exhibit the widest range of salary distribution, indicating a high level of variability based on experience, seniority, or specific industry sectors.

* Market Outliers: While Data Analysts generally have a lower median salary, the presence of extreme outliers (up to $400k) suggests that specialized or high-level positions in this field can still reach top-tier compensation.

