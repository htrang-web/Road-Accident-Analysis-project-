# UK Road Accident Analysis | Power BI

An interactive Power BI project analyzing UK road accident data from
2021–2022 to identify patterns in accident frequency, severity, time,
location, road conditions, weather, lighting, and vehicle types.

The project focuses on transforming raw accident data into meaningful
insights through data cleaning, data modeling, DAX measures, and
interactive dashboard design.

---

## 📌 Project Overview

Road accidents are influenced by multiple factors, including time,
location, road characteristics, weather, lighting conditions, and
vehicle types.

This project analyzes **307,973 recorded accidents** across the UK
during 2021–2022 to identify recurring patterns and factors associated
with accident frequency and severity.

The analysis is designed to support data-driven understanding of
road accident patterns and provide insights that could help inform
traffic safety planning.

---

## 🎯 Project Objectives

The main objectives of this project are to:

- Analyze changes in accident volume and severity over time.
- Identify the time periods when accidents occur most frequently.
- Examine accident patterns across different locations.
- Analyze the relationship between accidents and road conditions,
  weather, and lighting.
- Identify vehicle types most frequently involved in accidents.
- Compare accident patterns between urban and rural areas.
- Build interactive dashboards to support data exploration and reporting.

### Key Business Questions

- How did accident volume and severity change between 2021 and 2022?
- When do road accidents occur most frequently?
- Which road, weather, and lighting conditions are associated with
  higher accident volumes?
- Which vehicle types are most frequently involved in accidents?
- Which regions record the highest number of accidents?
- How do accident patterns differ between urban and rural areas?

---

## 🛠️ Tools & Technologies

- **Power BI** – Data modeling, visualization, dashboard development
- **Power Query** – Data cleaning and transformation
- **DAX** – KPI calculations and time-intelligence measures
- **Data Modeling** – Relationship design and calendar dimension
- **GitHub** – Project documentation and portfolio presentation

---

## 📊 Dataset

The dataset contains UK road accident records from **2021–2022**.

### Dataset Coverage

- **307,973 recorded accidents**
- **24 months**
- **422 Local Authorities**
- **51 Police Forces**

The dataset contains information covering:

- Accident date and time
- Accident severity
- Number of casualties
- Number of vehicles
- Geographic information
- Road characteristics
- Weather conditions
- Lighting conditions
- Road surface conditions
- Vehicle types
- Urban / rural classification

### Key Data Categories

| Category | Examples |
|---|---|
| Time | Date, Year, Month, Hour, Day of Week |
| Accident | Accident Index, Severity, Casualties, Vehicles |
| Road | Road Type, Speed Limit, Junction |
| Environment | Weather, Lighting, Road Surface |
| Vehicle | Vehicle Type |
| Geography | District, Police Force, Urban/Rural |

---

## 🧹 Data Preparation & Modeling

### Data Preparation

Data preparation was performed using **Power Query** to improve
data quality and prepare the dataset for analysis.

Key preparation steps included:

- Reviewing data types and column consistency.
- Handling missing and invalid values where appropriate.
- Creating analysis-ready time attributes.
- Creating derived fields such as:
  - Year
  - Month
  - Hour
  - Day of Week
  - Weekend indicator
- Preparing categorical fields for dashboard filtering.

### Data Modeling

The project uses a simple analytical model consisting of:

- `Data` – main accident fact table
- `Calendar` – date dimension table

The `Calendar` table is connected to the accident data through the
accident date to support time-based analysis and time-intelligence
calculations.

### Data Model

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4eee8eb5-d137-46f8-a23b-262c64f81939" />

---

## 📐 DAX Measures

Several DAX measures were created to support KPI cards,
comparisons, and time-based analysis.

### Total Accidents

```DAX
Total Accidents =
DISTINCTCOUNT(Data[Accident_Index])
```

### Total Casualties

```DAX
Total Casualties =
SUM(Data[Number_of_Casualties])
```

### Total Fatalities

```DAX
Total Fatalities =
CALCULATE(
    [Total Casualties],
    Data[Accident_Severity] = "Fatal"
)
```

### Average Vehicles per Accident

```DAX
Avg Vehicles per Accident =
DIVIDE(
    SUM(Data[Number_of_Vehicles]),
    [Total Accidents]
)
```

### YoY Change %

```DAX
YoY Change % =
VAR CurrentYear =
    [Total Accidents]

VAR PreviousYear =
    CALCULATE(
        [Total Accidents],
        SAMEPERIODLASTYEAR('Calendar'[Date])
    )

RETURN
    DIVIDE(
        CurrentYear - PreviousYear,
        PreviousYear
    )
```

---

# 📈 Key Insights

## 1. Overall Accident & Severity Patterns

- Accident volume decreased in 2022 compared with 2021.
- The majority of casualties were classified as **slight severity**.
- Rural areas accounted for a disproportionately high share of
  casualties compared with urban areas.

The rural–urban difference suggests that factors such as speed limits,
road characteristics, and other environmental conditions could be
further investigated.

---

## 2. Time Patterns

- **Friday** recorded the highest number of accidents among the days
  of the week.
- **17:00** was identified as the peak accident hour.
- **Weekdays accounted for approximately 75.61% of recorded accidents.**
- Accident volume shows clear variation across different hours and
  days of the week.

These patterns indicate that accident frequency is strongly related
to daily travel and commuting patterns.

---

## 3. Weather & Road Conditions

- **Clear weather** accounted for the largest number of recorded
  accidents.
- **Dry road surfaces** represented the majority of accident records.
- Poor weather conditions do not necessarily correspond to the
  highest accident volume because clear and dry conditions represent
  a much larger share of total driving conditions.

This highlights the importance of interpreting accident counts
relative to the underlying exposure rather than assuming that the
most frequent condition is necessarily the most dangerous.

---

## 4. Vehicle Patterns

- **Cars** were involved in approximately **245K accidents**, making
  them the dominant vehicle type in the dataset.
- Other vehicle categories accounted for substantially smaller
  proportions of total accident involvement.

The results provide a useful overview of which vehicle categories
contribute most to overall accident volume.

---

## 5. Geographic Patterns

- Accident volumes vary considerably across local authorities.
- **Birmingham** recorded the highest accident count among the
  analyzed districts.
- Urban and rural areas show different patterns in accident volume
  and casualty distribution.

These differences suggest that location-specific characteristics
should be considered when analyzing road safety.

---

# 📊 Dashboard

The project consists of multiple interactive dashboards designed
to provide different levels of analysis.

## Dashboard 1 — Overview

Provides a high-level view of:

- Total accidents
- Total casualties
- Total fatalities
- Accident severity
- Overall accident trends

<img width="1252" height="699" alt="image" src="https://github.com/user-attachments/assets/063d9ebd-2f08-455a-9b35-5ced88565e3f" />

---

## Dashboard 2 — Time Analysis

Analyzes accident patterns by:

- Year
- Month
- Day of Week
- Hour
- Weekday vs Weekend

<img width="1256" height="716" alt="image" src="https://github.com/user-attachments/assets/1a2a0751-700f-4743-8e73-75980fedae31" />

---

## Dashboard 3 — Weather & Road Conditions

Examines accident patterns across:

- Weather conditions
- Road surface conditions
- Lighting conditions
- Road types
- Speed limits

<img width="1253" height="702" alt="image" src="https://github.com/user-attachments/assets/db24991d-978f-461d-a46f-0bfdfa55c85b" />

---

## Dashboard 4 — Vehicle and Geographic Analysis

Analyzes accident involvement by:

- Vehicle type
- Number of vehicles
- Accident severity
- Local authority
- Police force
- Urban / rural classification
- Geographic location

<img width="1256" height="714" alt="image" src="https://github.com/user-attachments/assets/8585b209-ae8c-4cb0-b7a6-eb9bd4954c8c" />

---

# 💡 Key Takeaways

The analysis highlights several important patterns:

1. Accident frequency varies significantly by time and location.
2. Weekday and commuting-hour patterns account for a large proportion
   of accident records.
3. Cars represent the dominant vehicle category in the dataset.
4. Clear weather and dry roads account for the largest number of
   accident records.
5. Rural areas show a disproportionately high share of casualties,
   suggesting opportunities for further investigation into severity-
   related factors.
6. Accident volume alone should not be interpreted as accident risk;
   severity and contextual factors should also be considered.

---

# 🎯 Skills Demonstrated

- Business problem identification
- Data cleaning and transformation
- Data modeling
- Star-schema concepts
- DAX and time-intelligence calculations
- KPI development
- Exploratory data analysis
- Data visualization
- Interactive dashboard development
- Insight generation
- Data storytelling
- Analytical reporting

---

# 📌 Conclusion

This project demonstrates an end-to-end Power BI workflow, from
data preparation and modeling to analytical calculations,
visualization, and insight generation.

Rather than focusing only on dashboard design, the project emphasizes
using data to identify patterns, answer business questions, and
communicate actionable findings.
