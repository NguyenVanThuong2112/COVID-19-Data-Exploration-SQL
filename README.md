# 🦠 COVID-19 Data Analysis Pipeline: SQL ➔ Python ➔ Power BI

[![SQL Server](https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)](#)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](#)
[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](#)

An end-to-end analysis of the global COVID-19 pandemic (1 Jan 2020 – 30 Apr 2021): explore the data with **SQL Server**, clean it with **Python (Pandas)**, and present the results in a **4-page interactive Power BI dashboard**.

> **Note:** The SQL exploration follows the *COVID-19 Data Exploration* portfolio project by [Alex The Analyst](https://www.youtube.com/@AlexTheAnalyst). The Python cleaning pipeline and the Power BI dashboard are my own extensions on top of it.

## 📊 Dashboard Preview

The dashboard has four pages. All pages can be filtered by date range, country and continent.

### 1. Global Analysis
Headline KPIs, cumulative cases and deaths, a world map, and the top 10 countries.

<img width="647" height="360" alt="Screenshot 2026-11-18 180806" src="https://github.com/user-attachments/assets/ff82fe73-159e-4597-ab8e-371682ae21cc" />


### 2. Trend Analysis
Peak days, daily new cases and deaths with a 7-day average, and monthly cases vs. deaths.

<img width="632" height="358" alt="Screenshot 2026-11-18 180814" src="https://github.com/user-attachments/assets/ff89debf-66f3-4147-8660-c48e4960f581" />

### 3. Country Comparison
Absolute vs. population-adjusted rankings, population density vs. cases per million, and a comparison table.

<img width="644" height="359" alt="Screenshot 2026-11-18 180821" src="https://github.com/user-attachments/assets/1e6e19b0-b095-4499-a2bf-e633c0d49f92" />


### 4. Testing & Vaccination
Vaccine doses, people vaccinated, tests per 1,000 people, positive rates, and vaccination coverage vs. deaths per million.

<img width="650" height="357" alt="Screenshot 2026-11-18 180843" src="https://github.com/user-attachments/assets/34748c16-1c48-499f-804c-0371da60bc95" />


## 💡 Key Findings

All figures cover 1 Jan 2020 – 30 Apr 2021 (the end of the dataset).

**Overall**
- **151.40M** confirmed cases and **3.18M** deaths worldwide, a crude case fatality rate (CFR) of **2.10%**.
- **1 billion** vaccine doses administered; **595M** people had at least one dose and **268M** were fully vaccinated.

**Absolute numbers vs. population-adjusted numbers**
- By total cases: United States (32M), India (19M), Brazil (15M), France (6M). By total deaths: United States (0.58M), Brazil (0.40M), Mexico (0.22M), India (0.21M).
- Adjusting for population changes the picture. Among countries with at least 1M people, the highest cases per million were in **Czechia (~152,300), Slovenia (~115,600) and Bahrain (~104,000)**. India has the second-highest number of cases but only about 13,900 cases per million, compared with about 97,700 in the United States.
- Highest deaths per million: **Hungary (~2,850), Czechia (~2,730), Bosnia and Herzegovina (~2,610)**.
- **Mexico** has the highest CFR (**9.25%**) among countries with at least 10,000 cases. CFR uses confirmed cases only, so it depends on how much testing a country does.

**Trends over time**
- Monthly new cases rose from about 0.79M (Mar 2020) to 12.1M (Oct 2020), 19.3M (Dec 2020) and 22.5M (Apr 2021).
- Daily deaths peaked at **17.91K on 20 Jan 2021**, and monthly deaths peaked in January 2021 (about 411,000).
- The peak of daily cases (**905.99K on 28 Apr 2021**) sits at the very end of the dataset, so it may not be the true peak.
- Deaths per new case fell from about 8.0% (Apr 2020) to about 1.5% (Oct 2020), rose to about 2.7% in Feb 2021 and was about 1.6% in Apr 2021. This describes the numbers only; the data cannot explain why.

**Vaccination and context**
- Highest share of the population with at least one dose (countries with ≥1M people): Israel (62.44%), United Arab Emirates (51.38%), United Kingdom (50.40%), United States (43.77%).
- Population density shows almost no relationship with cases per million (rank correlation of about 0.1), while median age (about 0.65) and HDI (about 0.71) are more strongly associated. These are descriptive associations, not proof of cause.
- A positive link between vaccination coverage and deaths per million does **not** mean vaccines increase deaths: outbreaks and vaccine rollouts happened at different times in each country, and the data ends in April 2021.

## 🛠️ Tech Stack

| Stage | Tools |
|---|---|
| Data exploration | Microsoft SQL Server (SSMS) |
| Data cleaning | Python: Pandas, NumPy, Pathlib, Jupyter Notebook |
| Visualization | Power BI Desktop |
| Version control | Git & GitHub |

## 🔄 Pipeline

### 1. Exploration with SQL Server
- Imported two tables: `CovidDeaths` and `CovidVaccinations`.
- SQL techniques: `JOIN`, `CTE`, temp tables, window functions (`PARTITION BY`) and aggregate functions.
- Core metrics:
  - **Death rate:** total deaths ÷ total cases
  - **Infection rate:** total cases ÷ population
  - **Vaccination progress:** rolling count of people vaccinated vs. population

### 2. Cleaning with Python (Pandas)
- Standardized date columns to `datetime`.
- Enforced numeric types on count columns to avoid calculation errors.
- Handled null/NaN values: filled unrecorded daily cases and deaths with `0`.
- Checked for and removed duplicate rows.
- Exported cleaned CSV files to `Data/clean_data/`.

### 3. Visualization with Power BI
- Connected Power BI to the cleaned CSV files.
- Built four dashboard pages (Global Analysis, Trend Analysis, Country Comparison, Testing & Vaccination) with slicers for date, country and continent.
- Added short "key insights" notes on the pages, written to describe the data without claiming causes.

## 📂 Repository Structure

```
COVID-19-Data-Exploration-SQL/
├── Data/
│   ├── raw_data/              # Original Excel files from Our World in Data
│   └── clean_data/            # Cleaned CSV files exported by Python, used by Power BI
├── SQL_Exploration/
│   └── Covid_Data_Exploration.sql    # SQL queries for exploration and calculations
├── Python_Processing/
│   └── 01_Data_Cleaning.ipynb        # Missing values, duplicates, data types
├── PowerBI_Dashboard/
│   ├── Covid_Dashboard.pbix          # Interactive dashboard
│   └── screenshots/                  # Preview image of each dashboard page
├── requirements.txt
└── README.md
```

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

- The data ends on **30 Apr 2021**, so it does not cover later waves, variants or vaccination campaigns. The April 2021 peak in daily cases sits at the edge of the dataset.
- Reported cases depend on each country's testing capacity and reporting rules, so CFR and infection rates are not directly comparable across countries.
- Dips in the daily series reflect reporting adjustments (negative daily values are kept, not removed).
- **Turkey, 10 Dec 2020:** cumulative cases jump by 823,225 because of a change in reporting, and daily new cases show 0 on that day.
- Filling missing daily values with `0` is a simplifying assumption.
- The relationships shown are descriptive and do not establish cause and effect.

## 🔗 Data Source

- **Our World in Data:** [COVID-19 Dataset](https://ourworldindata.org/covid-deaths) (Excel/CSV)

## 👤 Author

**Nguyễn Văn Thương** · [@NguyenVanThuong2112](https://github.com/NguyenVanThuong2112)
