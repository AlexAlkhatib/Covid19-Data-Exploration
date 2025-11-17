# 🦠 **Covid-19 Data Exploration — Analyse SQL avancée**

Ce projet est une exploration approfondie des données Covid-19 grâce à SQL.
Il met en œuvre des techniques avancées pour analyser les contaminations, les décès, les taux de vaccination et comparer les impacts entre pays et continents.

Réalisé dans un **cadre personnel d’apprentissage**, ce projet démontre une solide maîtrise du SQL moderne, des jointures complexes, de la manipulation de données massives et de l’analyse statistique.


## 🎯 **Objectifs du projet**

* Explorer et analyser des datasets Covid-19 (infections, décès, vaccination)
* Construire des requêtes SQL avancées pour extraire des insights significatifs
* Comprendre les dynamiques de contamination à travers le monde
* Préparer des données pour des visualisations ou dashboards BI
* Manipuler efficacement des millions de lignes (selon dataset utilisé)


## 🧰 **Compétences SQL utilisées**

Ce projet démontre la maîtrise de nombreuses techniques SQL professionnelles :

### 🔹 Requêtes avancées

* **JOINS**
* **Common Table Expressions (CTE)**
* **Temp Tables (tables temporaires)**
* **Window Functions** (`OVER`, `PARTITION BY`)
* **Aggregate Functions** (`SUM`, `MAX`, `AVG`, etc.)
* **Création de Views** pour analyses ultérieures
* **Conversions de types** (`CAST`, `CONVERT`)
* Filtrage optimisé (`WHERE`, `LIKE`, `GROUP BY`, `ORDER BY`)

### 🔹 Analyse statistique SQL

* Taux de mortalité
* % de population infectée
* Comptage des décès par pays et continent
* Progression des vaccinations (rolling sum)
* Analyse globale consolidée


## 📊 **Types d’analyses effectuées**

### 📌 1. Infection & Mortalité

* Taux de mortalité par pays : `(total_deaths / total_cases) * 100`
* % de population infectée
* Pays les plus touchés selon le ratio infections/population
* Classement mondial des décès

### 📌 2. Analyse par continent

* Continent avec le plus grand nombre de décès
* Comparaisons géographiques larges

### 📌 3. Analyse globale

* Cas totaux et décès totaux dans le monde
* Taux de mortalité global

### 📌 4. Vaccinations

* Jointure des datasets **CovidDeaths** et **CovidVaccinations**
* Calcul du nombre cumulé de personnes vaccinées (rolling total)
* % de la population vaccinée
* Création d’une **vue SQL** pour futuros tableaux de bord BI


## 📂 **Structure du projet**

```
Covid-Data-Exploration/
 ├── CovidDeaths.csv
 ├── CovidVaccinations.csv
 ├── covid_data_exploration.sql   # fichier SQL principal (ton code)
 ├── README.md
 └── ressources/                  # éventuellement, données supplémentaires
```


## 🚀 **Exemples de requêtes avancées utilisées**

### 🔸 Pourcentage de la population vaccinée (rolling sum + CTE)

```sql
With PopvsVac (Continent, Location, Date, Population, New_Vaccinations, RollingPeopleVaccinated) as
(
    Select dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations,
        SUM(CONVERT(int,vac.new_vaccinations)) OVER 
        (Partition by dea.Location Order by dea.location, dea.Date) as RollingPeopleVaccinated
    From PortfolioProject..CovidDeaths dea
    Join PortfolioProject..CovidVaccinations vac
        On dea.location = vac.location
        and dea.date = vac.date
    Where dea.continent is not null
)
Select *, (RollingPeopleVaccinated/Population)*100
From PopvsVac;
```

### 🔸 Vue SQL pour dashboards BI

```sql
Create View PercentPopulationVaccinated as
Select dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations,
    SUM(CONVERT(int,vac.new_vaccinations)) OVER 
    (Partition by dea.Location Order by dea.location, dea.Date) as RollingPeopleVaccinated
From PortfolioProject..CovidDeaths dea
Join PortfolioProject..CovidVaccinations vac
    On dea.location = vac.location
    and dea.date = vac.date
Where dea.continent is not null;
```


## 🧠 **Compétences démontrées**

✔ Analyse SQL avancée
✔ Manipulation de données volumineuses
✔ Création de modèles analytiques (mortalité, infection, vaccination)
✔ Nettoyage / préparation de données
✔ Utilisation de CTE, views, tables temporaires
✔ Jointures complexes et window functions
✔ Préparation de données pour dashboards (Power BI, Tableau, Excel…)


## 🔧 **Pistes d’amélioration**

* Création d'un dashboard Power BI / Tableau basé sur les views SQL
* Optimisation des performances (indexation sur location/date)
* Ajout d’une analyse temporelle avancée (saisonnalité, pics épidémiques)
* Export des résultats en CSV / Excel
* Machine Learning (prévision de cas futurs)


## 👤 À propos

Développeur et analyste passionné par les données, j’ai réalisé ce projet pour perfectionner mes compétences SQL avancées et produire des analyses exploitables sur un dataset mondial complexe.

GitHub : **[https://github.com/AlexAlkhatib](https://github.com/AlexAlkhatib)**


## 📄 Licence
MIT License
Copyright (c) 2025 Alex Alkhatib
