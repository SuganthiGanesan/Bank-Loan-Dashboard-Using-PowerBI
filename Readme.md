# 🏦 BANK LOAN REPORT | SUMMARY DASHBOARD

![Dashboard Screenshot](bank.png)

This repository contains a comprehensive **Bank Loan Management Dashboard** built in Power BI to analyze and monitor loan portfolio performance. The dashboard provides critical insights into loan applications, funded amounts, repayments, and risk metrics to support data-driven lending decisions.

## 📊 KEY PERFORMANCE INDICATORS (KPIs)

### Portfolio Summary

| Metric | Total | MTD | MoM Change |
|--------|-------|-----|------------|
| **Total Loan Applications** | 38.6K | 4.3K | ▲ 6.9% |
| **Total Funded Amount** | $435.8M | $54.0M | ▲ 13.0% |
| **Total Amount Received** | $473.1M | $58.1M | ▲ 15.8% |
| **Avg Interest Rate** | 12.0% | 3.5% | ▲ 13.7% |
| **Avg DTI** | 13.3% | - | - |

### Loan Quality Overview

| Category | Applications | Funded Amount | Received Amount |
|----------|--------------|---------------|-----------------|
| **GOOD LOAN ISSUED** | 33K (86.2%) | $370.2M | $435.8M |
| **BAD LOAN ISSUED** | 5K (13.8%) | $65.5M | $37.3M |

## 📈 LOAN STATUS BREAKDOWN

| Loan Status | Total Loan Applications | Total Funded Amount | Total Amount Received | MTD Funded Amount | MTD Amount Received | Avg Interest | Avg DTI |
|-------------|------------------------|---------------------|----------------------|-------------------|---------------------|--------------|---------|
| **Fully Paid** | 32,145 | $351,358,350 | $411,586,256 | $41,302,025 | $47,815,851 | 11.64% | 13.17% |
| **Charged Off** | 5,333 | $65,532,225 | $37,284,763 | $8,732,775 | $5,324,211 | 13.88% | 14.00% |
| **Current** | 1,098 | $18,866,500 | $24,199,914 | $3,946,625 | $4,934,318 | 15.10% | 14.72% |
| **GRAND TOTAL** | **38,576** | **$435,757,075** | **$473,070,933** | **$53,981,425** | **$58,074,380** | **12.05%** | **13.33%** |

## 🔍 KEY INSIGHTS

### Portfolio Health
- ✅ **Strong Repayment Performance:** $473.1M received against $435.8M funded (108.5% recovery rate)
- ✅ **Good Loan Ratio:** 86.2% of applications are performing well (Fully Paid + Current)
- ⚠️ **Charge-Off Rate:** 13.8% of applications charged off, representing $65.5M in risky lending

### Risk Analysis
- 📉 **Higher Risk Loans:** Charged-off loans have higher avg interest (13.88%) and DTI (14.00%)
- 📈 **Current Loans:** Highest interest rates (15.10%) indicating recent higher-risk lending
- 💰 **Profitability:** Interest income contributes significantly to amount received

### Monthly Performance
- 📊 **Strong Growth:** MTD applications (+6.9%), funding (+13.0%), and receipts (+15.8%)
- 💹 **Increasing Yields:** MTD interest rates show positive momentum

## 🛠️ TECHNICAL IMPLEMENTATION

### Power BI Features Used

| Feature | Description |
|---------|-------------|
| **DAX Measures** | Time intelligence (MTD, MoM), KPI calculations |
| **Page Navigation** | Summary, Overview, Details pages |
| **Drill-Through** | Loan-grade and status detailed analysis |
| **Conditional Formatting** | Color-coded loan status and trends |
| **Tooltips** | Hover-based detailed metrics |
| **Bookmarks** | Toggle between different views |

### Key DAX Measures

```dax
// Total Loan Applications
Total Applications = COUNT(Loans[LoanID])

// MTD Applications
MTD Applications = TOTALMTD(COUNT(Loans[LoanID]), 'Date'[Date])

// MoM Change %
MoM Change = 
VAR CurrentMonth = [MTD Applications]
VAR PreviousMonth = CALCULATE([MTD Applications], DATEADD('Date'[Date], -1, MONTH))
RETURN
DIVIDE(CurrentMonth - PreviousMonth, PreviousMonth, 0)

// Good Loan Percentage
Good Loan % = 
DIVIDE(
    CALCULATE(COUNT(Loans[LoanID]), Loans[Status] IN {"Fully Paid", "Current"}),
    COUNT(Loans[LoanID]),
    0
)

// Recovery Rate
Recovery Rate = DIVIDE([Total Amount Received], [Total Funded Amount], 0)

📁 DATA MODEL
┌─────────────────┐     ┌─────────────────┐
│     Loans       │─────│      Date       │
│  (Fact Table)   │     │  (Dimension)    │
│ - Loan ID       │     │ - Date          │
│ - Amount        │     │ - Month         │
│ - Status        │     │ - Year          │
│ - Interest Rate │     └─────────────────┘
│ - DTI           │              │
│ - Grade         │              │
└─────────────────┘              │
         │                       │
         │                 ┌─────▼─────┐
         │                 │  Filters  │
         │                 └───────────┘
    ┌────▼────┐
    │ Borrower│
    │(Dim)    │
    └─────────┘

🎯 PROJECT OBJECTIVES
Objective	Description
📊 Portfolio Monitoring	Track loan applications, funding, and repayments
⚖️ Risk Assessment	Monitor charge-off rates and risky segments
📈 Trend Analysis	Identify monthly and month-over-month patterns
💰 Profitability Analysis	Track interest income and recovery rates
