# UK Road Accident Analysis | Power BI

An interactive Power BI project analyzing UK road accident data from 2021–2022 to identify patterns in accident frequency, severity, timing, location, road conditions, weather, lighting, and vehicle types.

---

## Project Overview

Road accidents are shaped by multiple factors — time, location, road characteristics, weather, lighting, and vehicle type. This project analyzes 307,973 recorded accidents across the UK during 2021–2022 to find recurring patterns and the factors most associated with accident frequency and severity, turning raw accident data into insights through data cleaning, modeling, DAX, and dashboard design.

## Project Objectives

- Track changes in accident volume and severity over time.
- Identify the time periods when accidents occur most frequently.
- Examine accident patterns across different locations.
- Analyze the relationship between accidents and road conditions, weather, and lighting.
- Identify the vehicle types most frequently involved in accidents.
- Compare accident patterns between urban and rural areas.

### Key Business Questions

- How did accident volume and severity change between 2021 and 2022?
- When do road accidents occur most frequently?
- Which road, weather, and lighting conditions are associated with higher accident volumes?
- Which vehicle types are most frequently involved in accidents?
- Which regions record the highest number of accidents?
- How do accident patterns differ between urban and rural areas?

---

## Tools & Technologies

- **Power BI** – data modeling, visualization, dashboard development
- **Power Query** – data cleaning and transformation
- **DAX** – KPI calculations and time-intelligence measures
- **Data modeling** – relationship design and calendar dimension

---

## Dataset

The dataset contains UK road accident records from 2021–2022.

- 307,973 recorded accidents
- 24 months
- 422 local authorities
- 51 police forces

Fields cover accident date and time, severity, number of casualties and vehicles, geographic information, road characteristics, weather, lighting, road surface conditions, vehicle types, and urban/rural classification.

| Category | Examples |
|---|---|
| Time | Date, Year, Month, Hour, Day of Week |
| Accident | Accident Index, Severity, Casualties, Vehicles |
| Road | Road Type, Speed Limit, Junction |
| Environment | Weather, Lighting, Road Surface |
| Vehicle | Vehicle Type |
| Geography | District, Police Force, Urban/Rural |

---

## Data Preparation & Modeling

Data preparation was done in Power Query:

- Reviewed data types and column consistency.
- Handled missing and invalid values where appropriate.
- Derived time attributes: Year, Month, Hour, Day of Week, and a weekend indicator.
- Prepared categorical fields for dashboard filtering.

The model is a simple star schema: `Data` (the accident fact table) related to `Calendar` (a date dimension) on accident date, supporting time-intelligence calculations like year-over-year comparisons.

<img width="1001" height="678" alt="Data model" src="https://github.com/user-attachments/assets/476b28e8-6b23-4421-af46-f4c628a3d75c" />

---

## DAX Measures

```DAX
Total Accidents = DISTINCTCOUNT(Data[Accident_Index])

Total Casualties = SUM(Data[Number_of_Casualties])

Total Fatalities = 
CALCULATE([Total Casualties], Data[Accident_Severity] = "Fatal")

Avg Vehicles per Accident = 
DIVIDE(SUM(Data[Number_of_Vehicles]), [Total Accidents])

YoY Change % = 
VAR CurrentYear = [Total Accidents]
VAR PreviousYear = 
    CALCULATE([Total Accidents], SAMEPERIODLASTYEAR('Calendar'[Date]))
RETURN 
    DIVIDE(CurrentYear - PreviousYear, PreviousYear)
```

---

## Key Insights

### Overall Accident & Severity Patterns

Accident volume fell in 2022 compared with 2021, and most casualties were classified as slight severity. Rural areas accounted for a disproportionately high share of casualties relative to urban areas — worth a closer look at speed limits, road characteristics, and other environmental factors specific to rural roads.

### Time Patterns

Friday recorded the highest number of accidents among the days of the week, and 17:00 was the peak accident hour. Weekdays accounted for roughly 75.61% of all recorded accidents — a pattern that tracks closely with daily commuting traffic.

### Weather & Road Conditions

Clear weather and dry road surfaces accounted for the largest share of recorded accidents — not because these conditions are more dangerous, but because they represent the vast majority of actual driving conditions. Raw accident counts by condition reflect exposure as much as risk, so they shouldn't be read as a direct measure of danger per trip.

### Vehicle Patterns

Cars were involved in roughly 245K accidents, by far the dominant vehicle type in the dataset, with all other vehicle categories accounting for a much smaller share of total involvement.

### Geographic Patterns

Accident volume varies considerably across local authorities, with Birmingham recording the highest count among the districts analyzed. Urban and rural areas also differ in how accident volume and casualty severity are distributed, reinforcing that location-specific factors matter for road safety analysis.

---

## Dashboard

### Dashboard 1 — Overview
Total accidents, casualties, fatalities, severity breakdown, and overall trend.

<img width="1252" height="699" alt="Dashboard 1 Overview" src="https://github.com/user-attachments/assets/063d9ebd-2f08-455a-9b35-5ced88565e3f" />

### Dashboard 2 — Time Analysis
Accidents by year, month, day of week, hour, and weekday vs. weekend.

<img width="1256" height="716" alt="Dashboard 2 Time Analysis" src="https://github.com/user-attachments/assets/1a2a0751-700f-4743-8e73-75980fedae31" />

### Dashboard 3 — Weather & Road Conditions
Weather, road surface, lighting, road type, and speed limit.

<img width="1253" height="702" alt="Dashboard 3 Weather and Road Conditions" src="https://github.com/user-attachments/assets/db24991d-978f-461d-a46f-0bfdfa55c85b" />

### Dashboard 4 — Vehicle and Geographic Analysis
Vehicle type, number of vehicles, severity, local authority, police force, and urban/rural classification.

<img width="1256" height="714" alt="Dashboard 4 Vehicle and Geographic Analysis" src="https://github.com/user-attachments/assets/8585b209-ae8c-4cb0-b7a6-eb9bd4954c8c" />

---

## Takeaways

Accident frequency varies significantly by time and location, with weekday commuting hours accounting for a large share of records. Cars dominate the vehicle-type breakdown, and clear/dry conditions account for the most accidents simply because they're the most common driving conditions — not necessarily the riskiest. Rural areas carry a disproportionate share of casualty severity, which is worth investigating further. Overall, accident volume on its own isn't a reliable proxy for risk — severity and context need to be read together.
