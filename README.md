# 🦠 COVID-19 Data Analysis Pipeline: SQL ➔ Python ➔ Power BI

[![SQL Server](https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)](#)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](#)
[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](#)

An end-to-end data analysis project on the global impact of COVID-19: explore the data with **SQL Server**, clean it with **Python (Pandas)**, and present the results in an interactive **Power BI** dashboard.

---

## 📌 Overview

The project started as a SQL exploration exercise and grew into a full pipeline. It answers questions such as:

- How deadly was COVID-19 in each country (deaths vs. confirmed cases)?
- Which countries had the highest share of their population infected?
- How did vaccination progress over time relative to population size?

> **Note:** The SQL part follows the *COVID-19 Data Exploration* portfolio project by [Alex The Analyst](https://www.youtube.com/@AlexTheAnalyst). The Python cleaning step and the Power BI dashboard are my own extensions on top of it.

## 🛠️ Tech Stack

| Stage | Tools |
|---|---|
| Data exploration | Microsoft SQL Server (SSMS) |
| Data cleaning | Python: Pandas, NumPy, Pathlib, Jupyter Notebook |
| Visualization | Power BI Desktop |
| Version control | Git & GitHub |

## 📂 Repository Structure

```
COVID-19-Data-Exploration-SQL
├── Data/
│   ├── raw_data/              # Original Excel files from Our World in Data
│   └── clean_data/            # Cleaned CSV files exported by Python, used by Power BI
├── SQL_Exploration/
│   └── Covid_Data_Exploration.sql    # SQL queries for exploration and calculations
├── Python_Processing/
│   └── 01_Data_Cleaning.ipynb        # Missing values, duplicates, data types
├── PowerBI_Dashboard/
│   ├── Covid_Dashboard.pbix          # Interactive dashboard
│   └── Dashboard_Screenshot.png      # Preview image
├── requirements.txt
└── README.md
```

## 🔄 Pipeline

### 1. Exploration with SQL Server
- Imported two tables: `CovidDeaths` and `CovidVaccinations`.
- SQL techniques used: `JOIN`, `CTE`, temp tables, window functions (`PARTITION BY`), aggregate functions, and views.
- Core metrics calculated:
  - **Death rate:** total deaths ÷ total cases
  - **Infection rate:** total cases ÷ population
  - **Vaccination progress:** rolling count of people vaccinated vs. population

### 2. Cleaning with Python (Pandas)
- Standardized date columns to `datetime`.
- Enforced numeric types on count columns to avoid calculation errors.
- Handled null/NaN values: filled unrecorded daily cases and deaths with `0`.
- Removed duplicate rows.
- Exported cleaned CSV files to `Data/clean_data/`.

### 3. Visualization with Power BI
- Connected Power BI to the cleaned CSV files.
- Built an interactive dashboard to track the spread of the virus, find geographic hotspots, and follow mortality trends.

## 📊 Dashboard Preview
<img width="647" height="359" alt="image" src="https://github.com/user-attachments/assets/24891ccb-eb59-4b89-a732-b421102ea56b" />
<img width="614" height="368" alt="image" src="https://github.com/user-attachments/assets/656634e5-2abc-42f2-8428-3bbfd15e2eb1" />
<img width="652" height="365" alt="image" src="https://github.com/user-attachments/assets/b5581a5d-a130-48ec-a837-80cba92a3e05" />



## 💡 Key Findings

<!-- TODO: replace each [X] with real numbers from your queries/dashboard. Delete any finding you can't back with data. -->

1. **Infection rate:** [Country A], [Country B] and [Country C] had the highest share of population infected, at [X]%, [X]% and [X]%.
2. **Death rate:** The global death rate peaked at around [X]% in [month/year], then fell to [X]% by the end of the dataset.
3. **Vaccination:** By [date], [X]% of the population in [country/region] had received at least one dose, compared with [X]% in [country/region].
4. **Insight of your own:** [e.g. a comparison between continents, or the gap between case numbers and death rate in a specific country.]

## ▶️ How to Reproduce

1. **Get the data:** download the dataset from [Our World in Data](https://ourworldindata.org/covid-deaths) and place the files in `Data/raw_data/`.
2. **SQL:** import the data into SQL Server as `CovidDeaths` and `CovidVaccinations`, then run `SQL_Exploration/Covid_Data_Exploration.sql`.
3. **Python:**
   ```bash
   pip install -r requirements.txt
   jupyter notebook Python_Processing/01_Data_Cleaning.ipynb
   ```
4. **Power BI:** open `PowerBI_Dashboard/Covid_Dashboard.pbix` in Power BI Desktop and, if needed, point the data source to `Data/clean_data/`.

## ⚠️ Limitations

- The dataset covers **January 2020 – 2021**, so it does not reflect later variants or vaccination campaigns.
- Reported cases depend on each country's testing capacity, so death and infection rates are likely underestimated in some countries.
- Filling missing daily values with `0` is a simplifying assumption.

## 🔗 Data Source

- **Our World in Data:** [COVID-19 Dataset](https://ourworldindata.org/covid-deaths) (Excel/CSV)

## 👤 Author

**Nguyễn Văn Thương**: Data Science student, looking for a data-related internship.
GitHub: [@NguyenVanThuong2112](https://github.com/NguyenVanThuong2112)
<!-- TODO: add your email or LinkedIn here. -->
