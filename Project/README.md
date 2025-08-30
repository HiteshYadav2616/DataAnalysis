# Overview  
This project explores **Data Analyst job postings in the United States**, focusing on:  
- The most in-demand skills  
- Skill trends over time  
- Salary distribution across roles  
- Highest-paying vs most-demanded skills  
- The most **optimal skills** (balance between demand and salary)  

The analysis provides **data-driven insights** for anyone looking to grow in a Data Analytics career.  

---

## Key Questions Answered  
1. What are the top demanded skills for the **Top 3 most popular data roles**?  
2. How are **in-demand skills trending** for Data Analysts?  
3. How well do **jobs and skills pay** for Data Analysts?  
4. What is the **most optimal skill** to learn (high demand + high salary)?  

---

## Tools I Used  
- **Python** → Core programming language  
- **Pandas** → Data manipulation & cleaning  
- **Seaborn & Matplotlib** → Data visualization  
- **Jupyter Notebook** → Interactive analysis environment  
- **AdjustText** → Annotating scatter plots  

---

## Data Preparation & Cleanup  
Before running analysis, the dataset was **imported, cleaned, and transformed**:  
- Imported raw CSV files into **Pandas DataFrames**  
- Removed **duplicates** and **null values**  
- Converted salary values to **numerical format (USD)**  
- Standardized skill names (e.g., merged `sql server` / `SQL`)  
- Created aggregated datasets:  
  - **Skill demand (% of job postings)**  
  - **Median salaries by role & skill**  
  - **Skill categories (programming, BI tools, databases, etc.)**  

---

# The Analysis

## 1. What are the most top demanded skills for the Top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for those top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here:
[Open skill_demand.ipynb](skill_demand.ipynb)

## Visulize data

```python
fig, ax = plt.subplots(3, 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skill_percent[df_skill_percent['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
    ax[i].legend().remove()
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].set_xlim(0, 75)

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v+1, n, f'{v:.0f}%', va='center')
        
ax[len(job_titles)-1].set_xlabel('skill percent')
plt.tight_layout()
plt.show() 
```

### Results

![Visulaization of Top Skills of Data Nerds](images\skill_deamand_plot.png)

### Key Insights from Visualization

- **SQL dominates** across all roles (51–72%), making it the most in-demand skill.  
- **Python** is highly valued, especially in technical roles (65–72%).  
- **Excel (41%)** and **Tableau (28%)** remain important for data analysis and BI-focused jobs.  
- **Cloud skills** like **AWS (43–52%)** and **Azure (32–37%)** are increasingly required, reflecting rising demand for cloud expertise.  
- **Big Data tools** such as **Spark (32–42%)** are critical in engineering-heavy roles.  
- **SAS (19%)** has relatively lower demand, indicating a shift toward open-source and modern tools.  

**Takeaway:** Mastery of **SQL + Python** is essential, while **cloud (AWS/Azure)** and **big data (Spark)** provide a competitive edge.



## 2. How are in-demand skills trending for Data Analysts?

### Visulize Data

```python

df_perc_plot = df_perc.iloc[:,:5]
sns.lineplot(data=df_perc_plot, dashes=False, palette='tab10')
plt.title("Trending Top Skills for the Data Analysis in the US")
plt.ylabel("Likelihood in job posting")
plt.xlabel('2023')
plt.legend().remove()
sns.despine()
from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))
for i in range(5):
    plt.text(11.2, df_perc_plot.iloc[-1, i], df_perc_plot.columns[i])

plt.tight_layout()
plt.show()
```

View my notebook with detail steps here:
[trending_skills.ipynb](trending_skills.ipynb)

### Results

![Trending Top Skills for Data Analysts in the US](images\trending_skills_plot.png)

*Bar graph visualizing the trending top skills for data analysts in the US in 2023.*

### Findings & Conclusion

#### Skill Demand in US Job Postings (2023)
- **SQL** → Most in-demand skill (~45–55% of postings).  
- **Excel** → Strong second (~34–43%), still highly relevant.  
- **Python & Tableau** → Mid-tier (~26–31%), stable across the year.  
- **SAS** → Lowest demand (~17–21%), reflecting industry decline.  

#### Skill Trends Over Time
- **SQL** stayed dominant but dipped slightly by year-end.  
- **Excel** followed a similar downward trend in late 2023.  
- **Python & Tableau** remained steady, occasionally overlapping in demand.  
- **SAS** fluctuated at the bottom without any growth trend.  

#### Conclusion
- **SQL + Excel** → Core skills every data analyst should master.  
- **Python + Tableau** → Essential for analysis and visualization.  
- **SAS** → Declining usage; optional for niche cases.  

**Takeaway:** Focus learning on **SQL & Excel**, strengthen with **Python & Tableau**, and consider cloud/big data tools for future-proofing.



## 3. How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Nerds

#### Visualize Data

```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)
sns.set_theme(style='ticks')

plt.title('Salary Distribution in the United States')
plt.xlabel('Yearly Salary (USD)')
plt.ylabel('')
plt.xlim(0, 600000)
from matplotlib.ticker import FuncFormatter
plt.gca().xaxis.set_major_formatter(FuncFormatter(lambda x, pos: f'${int(x/1000)}K'))
plt.show()
```

View my notebook with detail steps here:
[Salary_Analysis.ipynb](Salary_analysis.ipynb)

#### Results

![Salary Distribution of Data jobs in the US](images\salary_analysis_plot.png)

#### Summary
This visualization highlights the salary distribution of top data-related roles in the U.S. Senior roles consistently command higher salaries, while junior positions show comparatively lower medians. Wide ranges and outliers reflect market diversity across industries, locations, and levels of expertise.

#### Insights
- **Senior roles earn higher salaries** than junior roles (e.g., Senior Data Scientist vs. Data Scientist).  
- **Median salaries** for senior positions are significantly above **$150K**.  
- **Data Scientists and Data Engineers** (both junior and senior) show **wide salary ranges** with many outliers.  
- **Data Analysts** (junior and senior) have **lower median salaries** compared to engineering and science roles.  
- **High variability & outliers** suggest salaries differ greatly by **company, location, and experience**.  


#### Key Takeaway
Senior data roles are more lucrative, but salaries vary widely across the industry depending on skills, location, and company.  

### Highest Paid and most Demanded Skills in Data Analysts

#### Visualize Data

```python
fig,ax = plt.subplots(2, 1)

sns.set_theme(style='ticks')

sns.barplot(data=df_DA_US_top_pay, x='median', y=df_DA_US_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')
ax[0].legend().remove()

ax[0].set_xlabel('')
ax[0].set_ylabel('')
ax[0].set_title('Top 10 highest paid Skills for Data Analysts')
ax[0].xaxis.set_major_formatter(FuncFormatter(lambda x, pos: f'${int(x/1000)}K'))


sns.barplot(data=df_DA_US_skills, x='median', y=df_DA_US_skills.index, hue='count', ax=ax[1], palette='dark:b_r')
ax[1].legend().remove()

ax[1].set_xlabel('Median Salary (USD)')
ax[1].set_ylabel('')
ax[1].set_xlim(0, 200000)
ax[1].set_title('Top 10 most In-demand skills for Data Analysts')
ax[1].xaxis.set_major_formatter(FuncFormatter(lambda x, pos: f'${int(x/1000)}K'))

plt.tight_layout()
plt.show()
```
View my notebook with detail steps here:
[Salary_Analysis.ipynb](Salary_analysis.ipynb)

#### Results
Here's the breakdown of the highest-paid skills and in-demand skills for data analysts in the US:

![The Highest paid & most In-Demand Skills for Data Analysts in the US](images\salary_analysis_plot2.png)
*Two seperate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US.*


#### Summary
This visualization compares the **highest-paid skills** and the **most in-demand skills** for Data Analysts in the U.S. It highlights the salary gap between niche, high-paying technical skills and widely used, business-focused tools.

#### Insights
- **Top Paid Skills**:
  - Advanced/technical tools like **dplyr, bitbucket, gitlab, solidity, hugging face** lead to **higher salaries (>$170K median)**.  
  - Skills such as **ansible, mxnet, cassandra, vmware** also offer lucrative pay around **$140K–$160K**.  
  - These skills are specialized and often overlap with **data engineering, machine learning, or DevOps** roles.  

- **Most In-demand Skills**:
  - **Python, Tableau, R, SQL, Power BI, Excel** are the **most commonly required skills** in the job market.  
  - However, their **median salaries are lower (~$80K–$95K)** compared to niche technical skills.  
  - These are core **business intelligence and data analysis tools**, essential for entry to mid-level roles.  

#### Key Takeaway
- There is a **trade-off between demand and salary**:  
  - Widely used tools (Python, Excel, SQL) are essential and in-demand but not the highest paying.  
  - Niche technical skills (GitLab, Hugging Face, Solidity) are less in-demand but **significantly boost earning potential**.  

#### Conclusion
To maximize career growth:  
- **Start with in-demand skills** (Python, SQL, Tableau, Excel) to enter the field.  
- **Progress into niche technical tools** (machine learning frameworks, cloud/DevOps tools, specialized libraries) to command **higher salaries** and stand out in senior roles.

## 4. What is the most optimal skill to learn for Data Analysts?

#### Visualize Data

```python
from adjustText import adjust_text

sns.set_theme(style='ticks')
texts=[]
sns.scatterplot(data=df_plot, x='skill_percent', y='median_salary', hue='technology')
sns.despine()

for i, txt in enumerate(df_plot['skills']):
    texts.append(plt.text(df_plot['skill_percent'].iloc[i], df_plot['median_salary'].iloc[i], "" + txt))

adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray'))

plt.title("Most Optimal Skills for Data Analysts in the US")
plt.xlabel('Percent of Data Analyst Jobs')
plt.ylabel('Median Salary (USD)')
plt.legend(title='Technology')

from matplotlib.ticker import FuncFormatter 
from matplotlib.ticker import PercentFormatter
plt.gca().yaxis.set_major_formatter(FuncFormatter(lambda x, pos: f'${int(x/1000)}K'))
plt.gca().xaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.tight_layout()
plt.show()
```

View my notebook with detail steps here:
[Optimal_skills.ipynb](Optimal_skills.ipynb)

#### Results

![Most Optimal Skills for Data Analysts in the US](images\optimal_skills_plot2.png)
*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US*

#### Key Insights
- **SQL** is the most in-demand skill (required in ~60% of jobs).  
- **Python** provides the highest salary boost (~$98K).  
- **Tableau** balances demand (~30%) and high salary (~$94K).  
- **Excel** is widely expected (~40% of jobs) but adds modest salary value.  
- **SAS** and **Power BI** are niche, paying well but less frequently required.  
- **Word & PowerPoint** add little value in analytics hiring.  

---

#### Takeaways
- **SQL is essential** → It gets you the job.  
- **Python increases salary** → Strong career growth tool.  
- **Tableau/Power BI are great add-ons** → Competitive visualization skills.  
- **SAS is industry-specific** → Useful in finance/healthcare roles.  
- **Word/PowerPoint aren’t differentiators** → Don’t highlight them on resumes. 

---

# What I Learned
Through this project, I gained hands-on experience in:  
- **Data cleaning & wrangling** using Pandas  
- Working with **nested / stringified dictionaries** (e.g., job skills columns)  
- Visualizing insights using **Seaborn & Matplotlib**  
- Formatting axes and improving readability with **custom formatters**  
- Using **AdjustText** to label scatter plots without overlaps  
- Understanding the relationship between **demand vs. salary** in job skills  

---

## Key Insights  
- **SQL** is the single most in-demand skill for Data Analysts.  
- **Python** and **Excel** are both highly demanded and offer strong salaries.  
- **Tableau** and **Power BI** dominate the **BI tool category**, showing clear employer preference.  
- Niche skills like **SAS** or **Scala** offer higher salaries but appear in fewer job postings.  
- The “most optimal skills” are those that combine **widespread demand with above-average salaries**, making them smart choices for career growth.  

---

## Challenges I Faced  
- **Data inconsistencies** – some skills were spelled differently (`sql` vs. `SQL Server`).  
- **Nested dictionaries in CSV** – job skills data required `ast.literal_eval` to parse.  
- **Complex visualizations** – scatter plots with many overlapping labels needed fine-tuning with `adjustText`.  
- **Handling missing values** – had to drop or impute depending on context.  
- **Balancing insights vs. complexity** – too much detail made visuals cluttered, so simplification was necessary.  

---

## Conclusion  
This project provided a **data-driven perspective** on Data Analyst careers in the US.  
Key takeaways:  
- Learning **SQL + Python + a BI tool (Tableau/Power BI)** provides the best career opportunities.  
- Certain niche tools can boost salaries but may not be worth the effort for beginners.  
- Data-driven skill planning can help job seekers **focus on high-demand and high-paying skills**, ensuring long-term career growth.  
