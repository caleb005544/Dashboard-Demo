Manage Your Personal Finance with a Power BI Dashboard

Track your spending habits, increase your savings, and monitor your investment portfolio

A practice project inspired by this YouTube tutorial (https://www.youtube.com/watch?v=RGkxrQcgtrg)
, expanded with my own ideas, data model tweaks, and visualization enhancements.

Why this dashboard?

Track your spending habits: Daily and monthly views surface trends, spikes, and categories driving expenses.

Increase your savings: Clear KPIs, variance vs. prior month, and contribution-to-total help identify levers to save more.

Track your investment portfolio: Dedicated visuals to follow balances and performance alongside cash accounts for a full net-worth snapshot.

🚀 What this repo contains

Power BI Desktop (.pbix) file

Sample daily-balance CSV (two accounts)

🎯 Objectives

Recreate core concepts from the referenced tutorial

Practice data modeling, DAX, and UX polish

Add new features (rolling 12M view, arrow indicators, sparklines, contribution %)

✨ Key Features

Date dimension with Year/Quarter/Month/ISO Week, Month sort keys, Weekend flag

Last 12 months rolling window (measure-based visual filter)

Month-over-Month (PM) comparisons, variance, and growth %

Contribution-to-Total using ALL/ALLSELECTED variants

Conditional formatting (▲▼ arrows via UNICHAR, measure-driven colors)

In-cell sparklines using SVG generated from DAX (no custom visual)

Locale-safe date parsing for dd/mm/yyyy sources (Power Query “Using Locale…”)

🧱 Data Model

Calendar (marked as Date table)

Columns: Date, Year, Month, Monthnum, Day, Weekday, DayOfWeekNum, ISO Week, Quarter, Weekend/Weekday

DailyBalance (fact)


🧮 DAX Highlights (snippets)

-- Core
Total Amount = 
SUM ( DailyBalance[Account Balance - Personal Checking] ) +
SUM ( DailyBalance[Account Balance - Savings Account] )

-- Previous Month comparison (full-month)
Total Amount PM =
CALCULATE ( [Total Amount], PREVIOUSMONTH ( 'Calendar'[Date] ) )

Variance = [Total Amount] - [Total Amount PM]

Growth % =
DIVIDE ( [Variance], [Total Amount PM] )

-- Share of page/grand total (pick one)
% of Page Total =
DIVIDE ( [Total Amount], CALCULATE ( [Total Amount], REMOVEFILTERS ( 'Calendar' ) ) )

% of Grand Total =
DIVIDE ( [Total Amount], CALCULATE ( [Total Amount], ALL ( DailyBalance ) ) )

-- Rolling last 12 months flag (use as Visual-level filter = 1)
Show Last 12M :=
VAR lastDate  = CALCULATE ( MAX ( 'Calendar'[Date] ), ALL ( 'Calendar'[Date] ) )
VAR startDate = EOMONTH ( lastDate, -12 ) + 1
VAR curDate   = MAX ( 'Calendar'[Date] )
RETURN IF ( curDate >= startDate && curDate <= lastDate, 1, 0 )

-- Arrow display for Growth %
Growth % Arrow :=
VAR up   = UNICHAR(9650)   -- ▲
VAR down = UNICHAR(9660)   -- ▼
VAR g    = [Growth %]
RETURN
IF ( ISBLANK ( g ), BLANK(),
     IF ( g >= 0, "+ " & FORMAT(g,"0.0%") & " " & up,
                 FORMAT(g,"0.0%") & " " & down ) )


🙌 Credits

Tutorial inspiration: the video by How to Power BI — https://www.youtube.com/watch?v=RGkxrQcgtrg

Additional DAX patterns, formatting ideas, and enhancements were created by me for learning/demo purposes.

📄 License / Use

This repo is for learning & demonstration.

Date, Account Balance - Personal Checking, Account Balance - Savings Account

Relationship: Calendar[Date] → DailyBalance[Date] (single direction).
