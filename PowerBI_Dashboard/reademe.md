COVID-19 Global Analysis Dashboard (Power BI)

An interactive Power BI dashboard that explores the global progression of COVID-19 between 1 Jan 2020 and 30 Apr 2021: cases, deaths, country comparisons, testing and vaccination.


Objectives
Show how the pandemic progressed globally over time.
Compare countries by total burden and by population size (per million).
Separate cumulative metrics from daily metrics, and doses from people vaccinated.
Explore testing and vaccination where the data is sufficient, without implying causation.
Data source
File: CovidDeaths_Cleaned.csv is the only data source (no external data).
Size: 80,960 rows x 48 columns, 209 countries and territories, 6 continents.
Period: 1 Jan 2020 to 30 Apr 2021.
Exploration: Covid_Exploration.sql (SQL Server) was used for initial exploration only and is not loaded into the model.

Data model
Table	Role	Notes
Covid	Fact table	One row per country per day
DimCountry	Dimension	One row per country (209): continent, population, density, median age, GDP, HDI
DimDate	Date table	Calendar from first to last date, marked as date table
_Measures	Measures	All DAX measures

Relationships: DimCountry[Country] 1 to many Covid[location], and DimDate[Date] 1 to many Covid[date] (single direction).

Data preparation (Power Query)
date converted to a Date type.
In total_tests, new_tests, total_vaccinations, people_vaccinated, people_fully_vaccinated, new_vaccinations, icu_patients and hosp_patients, a value of 0 means "not reported", so 0 was converted to null.
Cumulative testing and vaccination columns were forward-filled within each country (last reported value carried forward). Daily (new_*) columns were not filled.
DimCountry was built from Covid by keeping the static columns and removing duplicate countries.
Key DAX logic
Cumulative totals (cases, deaths, vaccinations, tests) take each country's latest value on or before the selected end date, then add up across countries. Cumulative values are never summed across dates.
Daily metrics (New Cases, New Deaths) are summed, with 7-day averages calculated from them.
Ratios use DIVIDE(): CFR %, Cases per Million, Deaths per Million, % Population Vaccinated, Tests per Thousand.
Total Vaccinations (doses), People Vaccinated (at least one dose) and People Fully Vaccinated are separate measures and are never used interchangeably.
Dashboard pages
Page	Question answered	Main visuals
Global Overview	What is the global situation?	KPI cards (cases, deaths, CFR, vaccinations), cumulative cases and deaths over time, map, Top 10 by cases and deaths
Trend Analysis	How did the pandemic evolve?	Daily new cases and deaths with 7-day average, cumulative area charts, monthly cases vs deaths, peak cards
Country Comparison	Which countries were hit hardest relative to size?	Top 10 by total and per million (population of at least 1M), density vs cases per million (log scale), comparison table (at least 10,000 cases)
Testing & Vaccination	How far did testing and vaccination progress?	Doses, people vaccinated and fully vaccinated cards, cumulative doses, Top 15 vaccinated %, tests per 1,000 (one unit at a time), average positive rate, vaccination vs deaths per million

Hidden pages: Country Detail (drill-through target) and Tip Country (tooltip page).

Interactivity
Slicers for Date, Country and Continent on each page (selections are set per page). The Testing & Vaccination page has no Date slicer and adds a test-unit slicer that only affects the tests chart.
Cross-filtering between visuals, with selected visuals isolated from each other where needed.
Drill-through from a country to the Country Detail page.
Tooltip page for country details on hover.
Dynamic chart titles that show the selected country or continent.
Key findings (to 30 Apr 2021)
Global totals: 151,398,759 confirmed cases and 3,180,223 deaths (CFR about 2.10%).
The United States leads both cases (32.3M) and deaths (576,232). India (19.2M) and Brazil (14.7M) follow on cases.
Europe has the highest continental death toll (1,016,750).
Monthly new cases grew from about 0.79M (Mar 2020) to 12.1M (Oct 2020), 19.3M (Dec 2020) and 22.5M (Apr 2021). Monthly deaths peaked in Jan 2021 (about 411,000).
Deaths per new case fell from about 8.0% (Apr 2020) to about 1.5% (Oct 2020), then rose again to about 2.7% (Feb 2021). The data cannot explain why.
Among countries with at least 1M people, Czechia has the most cases per million (about 152,300) and Hungary the most deaths per million (about 2,850).
Population density shows almost no relationship with cases per million. These are descriptive associations, not proof of cause.
Data notes and limitations
Totals use cumulative columns. Summing new_cases gives 150,574,977 instead of 151,398,759 because Turkey's cumulative total jumped by 823,225 on 10 Dec 2020 (a reporting change) while its daily new cases show 0.
Negative daily values (61 rows for new cases, 80 for new deaths) are reporting adjustments and were kept so totals reconcile.
No recovered-cases column exists, so recoveries are not shown. ICU and hospital columns are mostly empty and were not used.
Test units differ between countries (tests performed, people tested, samples tested, units unclear), so the tests chart shows one unit at a time.
CFR is deaths divided by confirmed cases, so it depends on testing and reporting. CFR rankings only include countries with at least 10,000 cases.
Small populations distort per-million rankings, so these charts only include countries with at least 1M people. Some small territories report vaccination above 100% of population.
Vaccination data starts on 14 Dec 2020. Values are each country's latest report, so countries that stopped reporting keep their last value.
The dataset ends on 30 Apr 2021, so the latest peak in cases sits at the edge of the data.
Reference values for validation
Check	Expected value
Rows in Covid / countries in DimCountry	80,960 / 209
Total cases / deaths (full period)	151,398,759 / 3,180,223
Global CFR	about 2.10%
Peak daily new cases	905,992 on 28 Apr 2021
Peak daily new deaths	17,906 on 20 Jan 2021
Total vaccinations / people vaccinated / fully vaccinated	1,133,780,425 / 594,874,734 / 267,809,495
How to open
Open Covid_Dashboard.pbix in Power BI Desktop.
If the data source path differs on your machine, go to Home > Transform data > Source and point it to CovidDeaths_Cleaned.csv, then Close & Apply.
Tools

Power BI Desktop, Power Query (M), DAX, SQL Server (exploration).

Author
