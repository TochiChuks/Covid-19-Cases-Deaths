# Data Portfolio: Covid-19-Cases-Deaths (Hypothetical Case Study)

<img width="1165" height="637" alt="Screenshot 2025-08-25 133845" src="https://github.com/user-attachments/assets/59e8fc2a-541d-4904-b429-6ff6c0404fca" />

<img width="1163" height="641" alt="Screenshot 2025-08-22 170826" src="https://github.com/user-attachments/assets/df2b2f93-d1df-4282-8e08-05bf9f0a747b" />


# 1. Objective

As part of a Data Analyst assignment for a public health agency, I was tasked with building an end-to-end analytics pipeline to monitor and evaluate the impact of COVID-19 globally.

The agency needed a centralized reporting system that would:

- Track daily new cases and deaths worldwide.

- Identify countries with the highest cases, deaths, and case fatality rates (CFR).

- Compare COVID-19 trends across continents.

- Provide real-time insights via dashboards for decision-makers to allocate healthcare resources efficiently.

To achieve this, I used Python for data cleaning, SQL Server for structured transformations, and Power BI for interactive visualization, ensuring the agency had accurate, timely, and actionable insights.

# 2. Data Source

Dataset: https://catalog.ourworldindata.org/garden/covid/latest/cases_deaths/cases_deaths.csv

Source: Publicly available COVID-19 datasets (aligned with OWID/WHO structures).


Columns: date, country, new_cases, total_cases, new_deaths, total_deaths, population, etc.

Confirmed cases
| Variable | Description |
| total_cases | Total confirmed cases of COVID-19. Counts can include probable cases, where reported. |
| new_cases | New confirmed cases of COVID-19. Counts can include probable cases, where reported. In rare cases where our source reports a negative daily change due to a data correction, we set this metric to NA. |
| total_cases_per_million | Total confirmed cases of COVID-19 per 1,000,000 people. Counts can include probable cases, where reported. |
| new_cases_per_million | New confirmed cases of COVID-19 per 1,000,000 people. Counts can include probable cases, where reported. |

Confirmed deaths
| Variable | Description |
| total_deaths | Total deaths attributed to COVID-19. Counts can include probable deaths, where reported. |
| new_deaths | New deaths attributed to COVID-19. Counts can include probable deaths, where reported. In rare cases where our source reports a negative daily change due to a data correction, we set this metric to NA. |
| total_deaths_per_million | Total deaths attributed to COVID-19 per 1,000,000 people. Counts can include probable deaths, where reported. |
| new_deaths_per_million | New deaths attributed to COVID-19 per 1,000,000 people. Counts can include probable deaths, where reported. |


# 3. Stages

Data Exploration and Cleaning

Python

- Imported the COVID-19 dataset (cases & deaths) into Google Colab.

- Used Python (Pandas & Jupyter/Colab) to profile the dataset.

- Checked for missing values, duplicates, inconsistent country names, and outliers.

- Verified that “aggregates” (e.g., World, Asia, High-income countries) existed in the dataset.

- Cleaned data by removing irrelevant aggregates for country-level analysis, while retaining them for global-level insights.

Why it matters:

Prevents misleading insights (e.g., World appearing as a country).

Increases data reliability before analysis.


- Data Ingestion into SQL after cleaning with python in Google Colab.

- Created a structured schema (cases_deaths) with proper data types for dates, integers, and floats.

- Ensured large columns like total_deaths and total_cases were stored as BIGINT to avoid overflow errors.

Why it matters:

Establishes a single source of truth.

Ensures scalability for querying and connecting to Power BI.

<img width="866" height="483" alt="Screenshot 2025-08-25 160439" src="https://github.com/user-attachments/assets/177222f0-3129-425e-a1c7-485ac42fd07d" />

<img width="1198" height="184" alt="Screenshot 2025-08-25 160534" src="https://github.com/user-attachments/assets/cb23f2c0-7362-4770-8882-056e9cca2687" />

<img width="730" height="194" alt="Screenshot 2025-08-25 160607" src="https://github.com/user-attachments/assets/d5a01919-e7f6-4b05-9e3a-0df4badee94b" />

<img width="1782" height="389" alt="Screenshot 2025-08-25 160707" src="https://github.com/user-attachments/assets/5dc1e13f-e7dc-453c-a451-e84ae7f1e894" />


SQL

SQL Transformations & Creation of Analytical Views

- Created 7 SQL views to prepare analytics-ready data:

- Global totals (cases & deaths)

 <img width="714" height="408" alt="Screenshot 2025-08-25 161638" src="https://github.com/user-attachments/assets/5cfa55da-c2f6-49f0-9156-ab74ff1fd458" />
 
- Top 10 countries by total cases
  
<img width="714" height="408" alt="Screenshot 2025-08-25 161638" src="https://github.com/user-attachments/assets/96abb536-a34d-47a2-b8d7-7b8aee1499c0" />

- Top 10 countries by case fatality rate (CFR)
  
<img width="1048" height="686" alt="Screenshot 2025-08-25 161943" src="https://github.com/user-attachments/assets/71b356be-d7b7-4e99-9acc-19a7f0c2c990" />

- Daily global trend (cases & deaths)
  
<img width="606" height="539" alt="Screenshot 2025-08-25 162129" src="https://github.com/user-attachments/assets/c27bb624-df36-4a78-af11-08a4f065e36d" />
  
- Peak daily cases per country

<img width="1026" height="706" alt="Screenshot 2025-08-25 162240" src="https://github.com/user-attachments/assets/91c34234-9e29-42ab-b4a2-f6d6754b2d4b" />

- Highest cases per million (normalized by population)
  
<img width="1032" height="607" alt="Screenshot 2025-08-25 162419" src="https://github.com/user-attachments/assets/5eb74880-7e40-4a14-86d1-3788fc72d042" />

- Top 10 countries by total deaths

<img width="948" height="557" alt="Screenshot 2025-08-25 162540" src="https://github.com/user-attachments/assets/cb704f97-9ed2-4347-b3d2-7cd35ac562b8" />

- Excluded aggregate regions (e.g., World, Asia, EU) from country-level views.

Why it matters:

- Reduces Power BI complexity → all calculations are handled in SQL.

- Makes reports refresh faster since queries are optimized beforehand.


Power BI Connection and Visualization

- Connected Power BI directly to the SQL views.

- Built dashboards to visualize trends, comparisons, and rankings:

- Line charts: Daily global cases & deaths by year

- Bar charts: Top 10 countries by cases.

- Donut charts: Top countries by deaths.

- Map visualization: Spread of infections per million across countries.

- KPI cards: Global totals (cases, deaths, CFR).

Why it matters:

Provides decision-ready insights at a glance.

Allows non-technical users to interact with the data without writing SQL.



# 4. Insights, Findings, and Recommendations

Insights & Findings

Global Trends: Cases and deaths surged in specific waves (aligning with real-world pandemic peaks).

Country Leaders: Certain countries (e.g., US, India, Brazil) consistently appeared in the top 10 for cases and deaths.

Fatality Rates: Some smaller countries had disproportionately high CFRs due to limited testing and underreporting.

Regional Differences: Infection per million highlighted that some small-population countries had very high per-capita impact.

Peak Days: Each country had distinct “spikes,” aligning with reported outbreaks and policy changes.

Recommendations

Policy Simulation: Use this analysis to understand how waves evolved and test “what if” scenarios for future outbreaks.

Healthcare Planning: Countries with high CFRs could be studied further for healthcare capacity and testing coverage.

Public Awareness: Interactive dashboards can be shared with stakeholders to communicate risks more effectively.

Further Analysis: Integrating vaccination, hospital capacity, or mobility data could strengthen future insights.



