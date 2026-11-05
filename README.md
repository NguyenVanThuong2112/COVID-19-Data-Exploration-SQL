# COVID-19 Data Exploration in SQL

## 📌 Project Overview
This project explores global COVID-19 data to uncover trends in infection rates, mortality rates, and vaccination progress across different countries and continents. 

## 🛠️ Skills & Technologies Used
* **Database:** Microsoft SQL Server (SSMS) / MySQL
* **SQL Concepts:** Joins, CTEs, Windows Functions, Aggregate Functions, Data Type Conversions, Creating Views.
* **Dataset:** Our World in Data (Covid-19 dataset)

## 🔍 Key Questions Answered
1. **Global Impact:** What is the overall death percentage of reported COVID-19 cases globally?
2. **Infection Rates:** Which countries have the highest infection rates relative to their total population?
3. **Mortality Rates:** Which countries and continents suffered the highest total death counts?
4. **Vaccination Progress:** How can we track the rolling number of vaccinations and calculate the percentage of vaccinated individuals per country over time?

## 💻 Sample Code (Using CTE & Window Functions)
To calculate the rolling count of vaccinated people, I utilized `JOIN` to combine infection and vaccination tables, applying `OVER (PARTITION BY...)` to calculate cumulative sums:

```sql
WITH PopvsVac (Continent, Location, Date, Population, New_Vaccinations, RollingPeopleVaccinated)
AS
(
SELECT dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations
, SUM(CAST(vac.new_vaccinations AS INT)) OVER (PARTITION BY dea.Location ORDER BY dea.location, dea.Date) AS RollingPeopleVaccinated
FROM PortfolioProject..CovidDeaths dea
JOIN PortfolioProject..CovidVaccinations vac
	ON dea.location = vac.location
	AND dea.date = vac.date
WHERE dea.continent IS NOT NULL 
)
SELECT *, (RollingPeopleVaccinated/Population)*100 AS PercentVaccinated
FROM PopvsVac;	
