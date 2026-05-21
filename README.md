# 📊 HR Analytics — Dashboard Power BI & KPIs DAX

> **Projet universitaire BI** · Master Audit, Contrôle & Business Intelligence  
> Tafilalt Business School — Faculté Polydisciplinaire Errachidia · 2025–2026  
> Encadré par : **Mr. Farhaoui Youssef**

---

## 🎯 Objectif du projet

Concevoir un **tableau de bord interactif Power BI** pour analyser les performances des ressources humaines d'une organisation, identifier les leviers de productivité et détecter les risques de turnover — en s'appuyant sur une modélisation en étoile et des KPIs calculés en DAX.

---

## 📌 Résultats clés

| Indicateur | Valeur |
|---|---|
| 👥 Employés analysés | **500** |
| 💰 Masse salariale totale | **52 M** |
| 💵 Salaire moyen | **103 680** |
| ⭐ Performance moyenne | **3,26 / 5** |
| ⚠️ Taux d'attrition | **11 %** |
| 🚨 Employés à risque de départ | **55** |
| 📁 Projets traités / employé | **8,07** |
| ⏱️ Heures supplémentaires / mois | **20,04 h** |

---

## 🏗️ Architecture des données — Star Schema

```
                    ┌─────────────────┐
                    │  Dim_Employee   │
                    │  - EmployeeID   │
                    │  - Name, Gender │
                    │  - Age, Education│
                    └────────┬────────┘
                             │
   ┌─────────────┐  ┌────────▼──────────────┐  ┌──────────────────┐
   │  Dim_Time   │  │  Fact_EmployeePerf    │  │  Dim_Location    │
   │  - JoiningDate│◄─┤  - MonthlyS alary   ├──►│  - Country       │
   │  - LastLeave │  │  - PerformanceRating │  │  - CountryCode   │
   │  - YearsAtCo │  │  - ProjectsHandled  │  └──────────────────┘
   └─────────────┘  │  - OvertimeHours     │
                    │  - TrainingHours     │  ┌──────────────────┐
                    │  - AttritionRisk     ├──►│  Dim_Organization│
                    │  - CustomerSatisf.  │  │  - Department    │
                    └───────────────────────┘  │  - JobRole       │
                                               └──────────────────┘
```

**Source des données :** [Dataset RH — Kaggle](https://www.kaggle.com)

---

## 📐 KPIs calculés en DAX

```dax
-- 1. Nombre total d'employés
Nombre des employees = COUNTROWS(Fact_EmployeePerformance)

-- 2. Masse salariale totale
Total Payroll = SUM(Fact_EmployeePerformance[MonthlySalary])

-- 3. Salaire moyen
Salaire moyen = 
    CALCULATE(
        AVERAGE(Fact_EmployeePerformance[MonthlySalary]),
        NOT(ISBLANK(Fact_EmployeePerformance[MonthlySalary]))
    )

-- 4. Performance moyenne
Performance moyenne = AVERAGE(Fact_EmployeePerformance[PerformanceRating])

-- 5. Taux d'attrition
Taux d'attrition = 
    DIVIDE(
        CALCULATE(
            COUNTROWS(Fact_EmployeePerformance),
            Fact_EmployeePerformance[AttritionRisk] = "Yes"
        ),
        COUNTROWS(Fact_EmployeePerformance),
        0
    )
```

---

## 📊 Dashboard Power BI — 3 pages interactives

### Page 1 — Vue d'ensemble (Overview)
- Effectif total · Masse salariale · Salaire moyen · Taux d'attrition
- Répartition par département, pays et genre
- Distribution des salaires mensuels par pays
- Répartition par ancienneté

### Page 2 — Performance des employés
- Performance moyenne par département *(Marketing & HR en tête)*
- Impact des heures de formation sur la performance
- Performance par niveau d'éducation et ancienneté
- Moyenne des projets traités par poste

### Page 3 — Turnover / Attrition
- 55 employés à risque (taux global : 11%)
- Département **Sales** : zone à risque prioritaire
- Corrélation heures supplémentaires × attrition
- Analyse salaire vs décision de départ par département

---

## 🎯 Recommandations managériales

1. **Renforcer les programmes de formation** — corrélation positive formation/performance démontrée
2. **Réduire les heures supplémentaires dans le département Sales** — principal facteur de départ identifié
3. **Stratégies de rétention ciblées** sur les 3 premières années d'ancienneté
4. **Plans de carrière et reconnaissance** pour réduire le taux d'attrition de 11%

---

## 🛠️ Stack technique

| Outil | Usage |
|---|---|
| **Power BI** | Modélisation, calculs DAX, dashboards interactifs |
| **Power Query** | Transformation et nettoyage des données |
| **DAX** | Calcul des KPIs (COUNTROWS, SUM, AVERAGE, DIVIDE, CALCULATE) |
| **Star Schema** | Architecture de la base de données analytique |
| **LaTeX** | Rédaction du rapport académique |

---

## 📁 Structure du repo

```
HR-Analytics-PowerBI-Dashboard/
│
├── README.md
├── report/
│   └── Analyse_RH_Rapport.pdf
├── dashboard/
│   ├── page1_overview.png
│   ├── page2_performance.png
│   └── page3_attrition.png
└── dax/
    └── kpi_formulas.md
```

---

## 🔗 Liens utiles

- 🌐 [LinkedIn — Manar Abdellaoui](https://www.linkedin.com/in/manarabdellaoui)
- 💻 [GitHub — manar09-abd](https://github.com/manar09-abd)

---

*Master Audit, Contrôle & Business Intelligence · Tafilalt Business School · FP Errachidia · 2025–2026*
