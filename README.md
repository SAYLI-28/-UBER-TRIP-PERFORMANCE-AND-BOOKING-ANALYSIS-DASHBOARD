# 🚗 Uber Trip Performance & Booking Analytics Dashboard

> An end-to-end **Power BI analytics solution** built on **103,700+ Uber trip records** — uncovering booking trends, revenue drivers, location demand, and operational inefficiencies to support data-driven business decisions.

📌 **Built for:** Data Analyst Portfolio | Remote Jobs | Business Intelligence Roles  
🛠️ **Tools:** Power BI Desktop · Advanced DAX · Power Query · Excel  
📁 **Dataset:** Kaggle — Uber Trip Data | Date Range: June 2024

---

## 🎯 Business Problem

Uber's operations teams need real-time visibility into:
- **Which time slots and days** drive peak booking demand?
- **Which locations** generate the highest trip volumes?
- **Which vehicle types and payment methods** dominate revenue?
- **What is the day vs night trip split** for smarter resource planning?

This dashboard answers all four — with interactive drill-through and dynamic KPI switching across 3 dashboards.

---

## 📊 Real Numbers From This Analysis

| KPI | Value |
|-----|-------|
| 🚕 Total Bookings | **103,700 trips** |
| 💰 Total Booking Value | **$1.6 Million** |
| 💵 Average Booking Value | **$15.0 per trip** |
| 📍 Total Trip Distance | **349,000 Miles** |
| 🛣️ Average Trip Distance | **3 Miles** |
| ⏱️ Average Trip Time | **16 Minutes** |
| 🏆 Most Frequent Pickup | **Penn Station / Madison Sq West** |
| 🏁 Most Frequent Drop-off | **Upper East Side North** |
| 🌙 Night vs Day Split | **60.5% Night** / 39.5% Day |
| 💳 Top Payment Method | **Uber Pay — 70.74%** of all transactions |
| 🚙 Most Booked Vehicle | **UberX — 38,744 bookings** |
| 📏 Farthest Single Trip | **144.1 Miles** (Lower East Side → Crown Heights North) |

---

## 🖥️ Dashboard Screenshots

### Dashboard 1 — Overview Analysis
*KPI cards, payment breakdown, location intelligence, vehicle type grid*

![Overview Dashboard](UBER%20DASHBOARD%20OVERVIEW.png)

---

### Dashboard 2 — Time Analysis
*Pickup time area chart, day-name line chart, Hour × Day booking heatmap*

![Time Analysis Dashboard](UBER%20TRIP%20TIME%20ANALYSIS%20DASHBOARD.png)

---

### Dashboard 3 — Trip Details (Drill-Through)
*Granular trip-level records — Trip ID, vehicle, payment, distance, location, booking value*

![Trip Details Dashboard](UBER%20TRIP%20DETAILS%20DASHBOARD.png)

---

## 🔢 Key DAX Measures Built

```DAX
-- Total Revenue (Fare + Surge Fee combined)
Total Booking Value = 
    SUM('Trip Details'[fare_amount]) + SUM('Trip Details'[Surge Fee])

-- Average Revenue Per Trip
Avg Booking Value = 
    DIVIDE([Total Booking Value], [Total Bookings], BLANK())

-- Average Trip Duration in Minutes
Avg Trip Time = 
    AVERAGEX('Trip Details', 
        DATEDIFF('Trip Details'[Pickup Time], 
                 'Trip Details'[Drop Off Time], MINUTE))

-- Most Frequent Pickup using TOPN
Most Frequent Pickup Point = 
    VAR Pickpoint = TOPN(1, SUMMARIZE('Trip Details', 
                         'Location Table'[Location]), [Count], DESC)
    RETURN MAXX(Pickpoint, 'Location Table'[Location])

-- Dynamic KPI title updates all visuals simultaneously
Title For Pickup Time = 
    SELECTEDVALUE('Dynamic Measures'[Dynamic Title]) & " By Pickup Time"
```

> 💡 A **Disconnected Table** powers a measure selector — one slicer dynamically switches ALL charts between Total Bookings / Total Booking Value / Total Trip Distance simultaneously.

---

## 📐 Data Model

```
Trip Details (Fact Table)
├── Trip ID, Pickup Time, Drop Off Time
├── fare_amount, Surge Fee
├── trip_distance, passenger_count
├── Vehicle (UberX, Uber Black, Uber Comfort, Uber Green, UberXL)
├── Payment_type (Uber Pay, Cash, Amazon Pay, Google Pay)
├── Trip (Day / Night)
├── PULocationID → Location Table [active relationship]
└── DOLocationID → Location Table [inactive — USERELATIONSHIP in DAX]

Location Table      →  LocationID, Location, City
Calendar Table      →  Date, Day Name, Day Num
Dynamic Measures    →  Disconnected slicer table for KPI switching
```

---

## ✨ Advanced Features Implemented

| Feature | What It Does |
|---------|-------------|
| 🔄 Dynamic Measure Selector | One slicer updates ALL visuals — Bookings / Revenue / Distance |
| 🔍 Drill-Through | Right-click any data point → jump to granular Trip Details tab |
| 📍 Inactive Relationship | Drop-off location via `USERELATIONSHIP` in DAX |
| 🌙 Day/Night Segmentation | 60.5% night vs 39.5% day demand insight |
| 🗺️ Location Intelligence | TOPN DAX for most frequent pickup & drop-off |
| 📊 Hour × Day Heatmap | Exact peak booking hours per weekday |
| 🔖 Bookmarks | Info panel + Clear Filters reset button |
| ⬇️ Export Button | Download raw data directly from dashboard |
| 🎨 Conditional Formatting | Highlights high/low values in vehicle KPI grid |

---

## 💡 Business Insights & Recommendations

1. **Night trips dominate at 60.5%** — driver supply and surge pricing should be weighted toward evening/night for revenue maximisation
2. **Uber Pay leads at 70.74%** — cashless infrastructure is working; incentivise remaining 29% to shift digital
3. **UberX highest volume (38,744) but avg value flat at $15** across all vehicle types — premium upselling strategy needs a rethink
4. **Penn Station is the #1 pickup zone** — concentrating driver availability here during peak hours directly increases booking capture rate
5. **144.1 mile farthest trip signals long-haul demand** — a dedicated long-distance pricing tier could unlock additional revenue segment

---

## 🛠️ Tech Stack

| Tool | Usage |
|------|-------|
| Power BI Desktop | Dashboard development |
| Power Query (M) | Data cleaning & transformation |
| DAX | 13+ measures — dynamic, TOPN, USERELATIONSHIP, AVERAGEX |
| Excel / CSV | Raw data source |
| Kaggle | Dataset source |

---

## 🚀 How to Open This Project

1. Download the `.pbit` file from this repo
2. Open **Power BI Desktop** (free from Microsoft)
3. Connect to your local CSV data source when prompted
4. All measures, relationships, and dashboards load automatically

> 💡 No Power BI? The dashboard screenshots above show the full analysis.

---

## 👩‍💻 About

Built by **Sayli Markandey** — Junior Data Analyst  
📧 saylimarkandey@gmail.com  
🐙 [github.com/SAYLI-28](https://github.com/SAYLI-28)

*Open to remote Data Analyst opportunities globally.*

---

⭐ If this project was useful, consider starring the repo!
