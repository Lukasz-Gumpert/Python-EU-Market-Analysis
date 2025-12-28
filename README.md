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

## Market Dynamics & Key Players:

The primary objective of this specific analysis is to perform an Exploratory Data Analysis (EDA) to understand the current landscape of the European data job market. By leveraging the cleaned dataset, this section aims to answer critical questions regarding job distribution and employer dominance within the EU.

### Job Distribution by Country: 
Identifying which European nations offer the highest volume of opportunities for data professionals.

```py
df_top_countries = df_eu['job_location'].value_counts().sort_values(ascending=False).head(10).reset_index()
df_top_countries.columns = ['country', 'count']

sns.set_theme(style='ticks')
sns.barplot(data=df_top_countries,x='count',y='country', hue='count', palette='flare')

plt.title('Top 10 EU job posting countries for Data Analyst role')
plt.xlabel('')
plt.ylabel('Country name')
```

<img src="Python-EU-Market-Analysis\assets\01_Top_10_eu_countries.png" alt='European countries with most data job postings'>

* Market Leadership: The UK, France, and Italy dominate the European market, with the UK leading significantly at nearly 2,000 job postings.

* Regional Demand Disparity: There is a sharp decline in volume after the top three, with mid-tier markets like Spain and Germany offering roughly 50-60% fewer opportunities.

* Tech Hub Density: While smaller nations like Luxembourg and the Netherlands have lower absolute counts (~500), they show high demand relative to their market size.

## Benefits and Requirements:
Next, I explored key job requirements and benefits for Data Analyst roles using pie chart visualizations to identify industry standards.

```py
dict_column = {
    'job_work_from_home': 'Remote job possible?',
    'job_no_degree_mention': 'Is degree required?',
    'job_health_insurance': 'Health insurance benefits'
}

colors = sns.color_palette('flare')

fig,ax = plt.subplots(1,3,figsize=(15,10))

for i, (column, title) in enumerate(dict_column.items()):
    ax[i].pie(df[column].value_counts(),
        labels=[True,False],
        autopct='%1.1F%%',
        startangle=90,
        colors=colors,
)
    ax[i].set_title(title,fontsize=14)
```

<img src="Python-EU-Market-Analysis\assets\02_Requirement_exploration.png" alt='Requirements exploration.png'>

* Dominance of Remote Work: Remote flexibility is nearly universal in the field, with 91.1% of job postings confirming that remote work is possible.

* Education Requirements: A university degree remains a significant barrier to entry, as it is required by 69.4% of employers.

* Standardized Benefits: Health insurance is a highly consistent offering across the market, included in 89.0% of the analyzed job descriptions.

### Top Employers: 
Lastly identifying the most active companies currently hiring in the European market to highlight key industry players.

```py
df_top_companies = df_eu['company_name'].value_counts().sort_values(ascending=False).head(10).reset_index()
df_top_companies.columns = ['company', 'count']

sns.set_theme(style='ticks')
sns.barplot(data=df_top_companies,x='count',y='company', hue='count', palette='flare')

plt.title('Top 10 EU companies hiring Data Analysts')
plt.xlabel('')
plt.ylabel('Company name')
```

<img src="Python-EU-Market-Analysis\assets\03_Top_10_companies.png" alt='Top 10 companies'>

* Dominance of "Confidenziale": The largest share of postings comes from "Confidenziale" (over 500 listings), which typically represents confidential recruitment agencies masking client identities.

* Recruitment Agency Presence: Professional staffing firms like JobLeads GmbH, Hays, and Randstad feature prominently, indicating that a significant portion of the market is managed by third-party recruiters.

* Key Corporate Employers: Major industry players such as Allegro, Banco Santander, and SAFRAN emerge as the top direct corporate employers actively seeking data talent.

## Technical Skill Requirements:

Next, I analyzed the most frequently requested skills for three core data roles to identify the essential technical competencies in the current market.

```py
# Set plot size, structure and theme
fig,ax = plt.subplots(3,1,figsize=(10,7))
sns.set_theme(style='ticks')

# Create bar charts showing the top 5 skills by demand percentage for each job title
for i,job_title in enumerate(data_list):

    # Filter top 5 skills for the current job title
    df_plot = df_skill_perc[df_skill_perc['job_title_short'] == job_title].head(5)

    # Plot skill demand percentage
    sns.barplot(data=df_plot,
                x='percentage',
                y='job_skills',
                ax=ax[i],
                hue='skill_count',
                palette='flare')
```
<img src="Python-EU-Market-Analysis\assets\04_Skill_requested.png" alt='Most requested skills'>

* Universal Importance of SQL and Python: SQL is a foundational requirement across all roles, peaking at 56% for Data Engineers, while Python is the most critical skill for Data Scientists at 60%.

* Distinct Analyst Toolkit: For Data Analysts, the stack is uniquely characterized by a blend of SQL (43%) and visualization or spreadsheet tools like Excel (30%) and Power BI (23%).

* Cloud and Infrastructure Focus: Data Engineering roles show a much higher demand for cloud platforms and big data tools, specifically Azure (35%), AWS (28%), and Spark (27%).

## Technical Skill Trends in European market:

In this part I analyzed the most frequently requested skills for three core data roles to identify the essential technical competencies in the current market.

```py
from matplotlib.ticker import PercentFormatter

# Plot percentage trends for top skills
sns.lineplot(
    data=df_percents_top10,
    dashes=False,
    palette='tab10'
)
# Apply theme and remove top/right spines
sns.set_theme(style='ticks')
sns.despine()

# Add chart title, remove legend, label x-axis
plt.title('Top skill trends in European Data Analyst market')
plt.legend().remove()
plt.xlabel('2023')

# Format y-axis to display values as percentages
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=False))

# Add end-of-line labels for better readability
for i in range(5):
    plt.text(11.5, df_percents_top10.iloc[-1,i], df_percents.columns[i])
```

<img src="Python-EU-Market-Analysis\assets\05_skill_trend.png" alt='Skill trends'>

* Universal Importance of SQL and Python: SQL remains the industry standard database language and is a foundational requirement across all data roles, while Python is highly sought-after for its flexibility in data cleaning and advanced analysis.

* Distinct Analyst Toolkit: For Data Analysts, the technical stack is uniquely characterized by a blend of SQL for data retrieval and visualization or spreadsheet tools like Excel and Power BI for reporting.

* Infrastructure and Advanced Analytics: Data Engineering and Scientist roles show a higher demand for specialized skills such as Cloud platforms (AWS/Azure) and Machine Learning, which are increasingly identified as key components for high-impact data professional toolkits.

## Salary Distribution Analysis:

This part focuses on yearly salary distribution across different data roles in Europe to understand the earning potential within each specialization. Additionaly, relationships between specific technical skills and their impact on compensation was added.

```py
# Create boxplot of EU salary distribution
sns.boxplot(data=df_eu_top,x='salary_year_avg',y='job_title_short',order=titles_order)
sns.set_theme(style="ticks")

# Add chart title, edit labels, xlim,
plt.title('Data salary distribution in Europe')
plt.ylabel('')
plt.xlabel('Salary yearly in USD')

# Limit x-axis range to focus on relevant salary values
plt.xlim(0,420000)

# Format x-axis ticks as "$XXK" for readability
ticks = plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks)

plt.show()
```

<img src="Python-EU-Market-Analysis\assets\06_data_salary_distribution.png" alt='Salary distribution'>

* Highest Median Salary: Data Engineers command the highest median yearly salary in Europe, followed closely by Data Scientists, both of which significantly outperform the Data Analyst role.

* Significant Salary Variance: Data Scientists exhibit the widest range of salary distribution, indicating a high level of variability based on experience, seniority, or specific industry sectors.

* Market Outliers: While Data Analysts generally have a lower median salary, the presence of extreme outliers (up to $400k) suggests that specialized or high-level positions in this field can still reach top-tier compensation.

```py
# Plot salary distribution for each skill
fig,ax = plt.subplots(2,1)

sns.barplot(data=df_da_top_pay,
            x='median',
            y=df_da_top_pay.index, hue='median', 
            ax=ax[0],
            palette='light:b'
)

ax[0].set_title('Top 10 highest paid skills for Data Analyst')
ax[0].legend().remove()
ax[0].set_xlabel('')
ax[0].set_ylabel('')
ax[0].xaxis.set_major_formatter(lambda x, pos: f'${int(x/1000)}K')

sns.barplot(data=df_da_top_skill,
            x='median',
            y=df_da_top_skill.index, 
            hue='median', 
            ax=ax[1],
            palette='light:b'
)

ax[1].set_title('Top 10 most in-demand skills for Data Analyst')
ax[1].legend().remove()
ax[1].set_xlabel('')
ax[1].set_ylabel('')
ax[1].set_xlim(ax[0].get_xlim())
ax[1].xaxis.set_major_formatter(lambda x, pos: f'${int(x/1000)}K')

plt.tight_layout()
plt.show()
```

<img src="Python-EU-Market-Analysis\assets\07_salary_comparison.png" alt='Salary comparison'>

* Highest Paying Niche Skills: Specialized tools like svn lead the market with salaries reaching $400k, followed by deep learning frameworks such as pytorch and tensorflow which average around $175k.

* Most In-Demand Skill Value: While looker is the most in-demand skill, it commands a median salary of approximately $110k, which is significantly lower than the top niche technical skills.

* Core Technical Baseline: Standard analyst tools like SQL, Python, and Tableau show a consistent market value between $90k and $100k, establishing a strong earning baseline for the profession.

## Final Strategic Summary: Optimal Skills & Salary Analysis:

To conclude my research, I have integrated all previously collected data to identify the most strategic technical skills based on their market demand and salary potential.

```py
from adjustText import adjust_text
from matplotlib.ticker import PercentFormatter

# Scatterplot relating skill popularity vs. salary, colored by technology category
sns.scatterplot(
    data=df_final,
    x='skill_percent',
    y='median_salary',
    hue='Technology'
)

# Add skill labels to points
texts = []

for i,val in enumerate(df_eu_top_skills.index):
    texts.append(
        plt.text(
            df_eu_top_skills['skill_percent'].iloc[i],
            df_eu_top_skills['median_salary'][i],
            val)
            )

# Automatically adjust label positions and draw arrows
adjust_text(texts, arrowproprops=dict(arrowstyl='->',color='gray',lw=3))

ax = plt.gca() 
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos:  f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))


# Apply theme, labels, layout
sns.despine()
sns.set_theme(style='ticks')
plt.xlabel('Percent of Data Analyst Jobs')
plt.ylabel('Medium Yearly Salary')
plt.title('Most optimal skills in EU job offers ')
plt.tight_layout()
plt.show()
```

<img src="Python-EU-Market-Analysis\assets\08_optimal_skills.png" alt='Optimal skills'>

* Optimal High-Value Skills: Python and Tableau represent the "sweet spot" in the market, offering high median salaries (above $100k) while remaining in high demand among approximately 25-35% of job postings.

* Essential Foundations vs. Niche Earnings: While SQL is the most widely required skill (42% of jobs), it commands a more moderate baseline salary of $90k; conversely, niche tools like Looker offer the highest median pay ($112k) despite appearing in fewer than 10% of offers.

* Strategic Specialization: For those seeking the highest possible compensation, specialized engineering and cloud skills like SVN, PyTorch, and TensorFlow can push salaries toward the $175k–$400k range, though they are less frequent in general analyst roles.
