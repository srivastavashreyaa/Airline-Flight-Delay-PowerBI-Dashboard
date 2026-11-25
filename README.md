# Airline Flight Delay & Airport Performance Analytics (Power BI)

An interactive Power BI dashboard that analyzes U.S. domestic airline and airport performance using about 5.8 million flight records from 2015.

![Dashboard](screenshots/dashboard.png)

## Problem

Airlines produce huge amounts of flight data, but it usually sits in raw files. That makes simple questions hard to answer: Which airlines are most reliable? When and where do delays spike? What actually causes them? This dashboard turns the raw data into clear, interactive insights.

## Dataset

[2015 Flight Delays and Cancellations](https://www.kaggle.com/datasets/usdot/flight-delays) (U.S. Department of Transportation, via Kaggle)

| Table | Contents |
|---|---|
| `flights.csv` | ~5.8 million flight records with delays, cancellations and delay causes |
| `airlines.csv` | Airline IATA codes and names |
| `airports.csv` | Airport codes, city, state and coordinates |

The dataset is not included in this repo because of its size. Download it from the link above.

## Tools

Power BI Desktop, Power Query, DAX, data modeling (star schema)

## How it was built

1. **Data cleaning (Power Query):** loaded all three CSV files and fixed header detection and data types.
2. **Data model:** built a star schema with `flights` as the fact table and `airlines` and `airports` as dimensions.
   - `flights[AIRLINE]` → `airlines[IATA_CODE]` (active)
   - `flights[ORIGIN_AIRPORT]` → `airports[IATA_CODE]` (active)
   - `flights[DESTINATION_AIRPORT]` → `airports[IATA_CODE]` (inactive, used with `USERELATIONSHIP` for role-playing analysis)
3. **12 DAX measures:** Total Flights, On-Time Flights, On-Time Performance %, Avg Arrival Delay, Avg Departure Delay, Cancelled Flights, Cancellation Rate %, plus five delay-cause measures (Air System, Security, Airline, Late Aircraft, Weather). Key functions: `COUNTROWS`, `CALCULATE`, `DIVIDE`, `SUM`, `AVERAGE`.
4. **Visuals:** KPI cards, an airline comparison bar chart, a monthly delay trend line, a geographic airport map, a delay-cause donut chart, and Airline and Month slicers.

## Key insights

| Metric | Value |
|---|---|
| On-time performance | 82.4% |
| Average arrival delay | 4.41 minutes |
| Cancellation rate | 1.5% |

- **Late-arriving aircraft is the top delay cause** (~39.8% of delay minutes), followed by airline operations (~32.2%) and the air system (~22.9%).
- **On-time performance differs by about 14 percentage points** between the best and weakest airlines, with Frontier (F9) the lowest.
- **Delays peak around June and February.**

## How to open

1. Download the dataset from Kaggle.
2. Open `Airline_Flight_Delay_Dashboard.pbit` in Power BI Desktop.
3. If it asks for the data files, go to **Transform data → Data source settings** and point each source to your downloaded CSV files, then click **Refresh**.

## Team

Shreya Srivastava, Yash Chauhan, Tanishka Jain
Business Intelligence and Analytics (21CSE421T), SRM Institute of Science and Technology
Faculty guide: Dr. Kavitha P M
