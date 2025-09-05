Manage Your Personal Finance with a Power BI Dashboard

Track your spending habits, increase your savings, and monitor your investment portfolio — all in one place.

Practice project inspired by this YouTube tutorial
, expanded with my own ideas, data model tweaks, and visualization enhancements.

Why this dashboard

Track spending habits: Daily and monthly views surface trends, spikes, and categories driving expenses.

Increase savings: Clear KPIs, variance vs. prior month, and contribution-to-total highlight opportunities to save more.

Monitor investments: Dedicated visuals track balances and performance alongside cash accounts for a full net-worth snapshot.

🚀 What this repo contains

Power BI Desktop (.pbix) file

Sample daily-balance CSV (two accounts)

🎯 Objectives

Recreate core concepts from the referenced tutorial

Practice data modeling, DAX, and UX polish

Add new features (rolling 12M view, arrow indicators, sparklines, contribution %)

✨ Key Features

Date dimension with Year / Quarter / Month / ISO Week, Month sort keys, Weekend flag

Rolling last 12 months (measure-based visual filter)

Month-over-Month (PM) comparisons, variance, and growth %

Contribution-to-total using ALL / ALLSELECTED variants

Conditional formatting (▲▼ via UNICHAR, measure-driven colors)

In-cell sparklines using SVG generated from DAX (no custom visual)

Locale-safe date parsing for dd/mm/yyyy sources (Power Query “Using Locale…”)

🛠️ Getting Started

Open the .pbix in Power BI Desktop.

If source dates are dd/mm/yyyy: Power Query → select date column → Data type → Using Locale… → Type: Date; Locale: English (United Kingdom) (or your D/M/Y locale).

In Model view:

Mark Calendar as Date table (Column = Date).

Set Month → Sort by Monthnum; Weekday → Sort by DayOfWeekNum.

For the sparkline measure: select it → Data category = Image URL.

📊 How to Use

Slicers: Account, Date (or force Last 12M via [Show Last 12M] = 1).

Cards: Total, PM, Variance, Growth %.

Line chart: daily balances with continuous X-axis and Show items with no data = On.

Matrix: category/segment + Contribution % + Sparkline.

📁 Suggested Repo Structure
/data
  daily_balance_sample.csv
/models
  finance_dashboard.pbix
/docs
  screenshots/
  measures.md
README.md

🖼️ Screenshots / Demo

(Add a few PNGs or a short GIF showing: KPIs & line chart, matrix with sparkline/arrows, and the Last 12M behavior.)

🙌 Credits

Tutorial inspiration: How to Power BI — https://www.youtube.com/watch?v=RGkxrQcgtrg

Additional DAX patterns, formatting ideas, and enhancements were created by me for learning/demo purposes.

📄 License / Use

This repo is for learning & demonstration. Replace sample data with your own before using in production.
