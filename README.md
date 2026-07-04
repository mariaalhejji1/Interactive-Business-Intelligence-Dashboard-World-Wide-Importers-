# Worldwide Importers: Sales and Economic Performance Analysis

An interactive Business Intelligence solution built in Power BI utilizing the Worldwide Importers dataset sourced from Kaggle. This project transforms over 26,397 raw transactional records into an enterprise-grade decision-support system, moving from historical descriptive reporting to dynamic predictive forecasting.

## Project Overview and Problem Statement
Modern wholesale organizations generate massive daily transaction volumes. Without proper Business Intelligence frameworks, converting this multi-dimensional data into strategic insights is highly challenging. Relying on static spreadsheets limits a company's ability to identify seasonal shifts, geographic profitability, and product line margins.

This project addresses these challenges by establishing a unified data model that provides interactive descriptive charts, automated tier-based regional classifications, and strategic What-If simulation sliders for real-time risk evaluation and economic forecasting.

## Tech Stack and Key Features
* BI Platform: Power BI Desktop
* ETL and Data Preprocessing: Power Query
* Data Modeling: Relational Star Schema
* Analytical Calculations: Advanced DAX (Data Analysis Expressions)
* Analytics Scope: Descriptive, Predictive, and Prescriptive Analytics

## Dashboard Insights and Layout

The dashboard features a curated Sage Green and Corporate White color palette designed for executive accessibility, accompanied by a fixed left-hand filtering sidebar for granular data slicing.

### Page 1: Descriptive Analytics and Operational Performance
Focuses on historical trends, key performance tracking, and granular profitability distribution.
* Executive KPI Scorecard: Displays core health metrics including Total Sales ($19.88M) and an aggregate Profitability Margin of 49.92%.
* Sales Performance Trend: An area chart outlining revenue fluctuations over multiple fiscal periods to detect seasonality.
* Regional Performance Matrix: A tabular view using advanced DAX to categorize states into dynamic performance tiers such as Exceptional, Excellent, Average, and Poor.

Dashboard Preview - Page 1:
<img width="1432" height="793" alt="The Dashbord Page1" src="https://github.com/user-attachments/assets/32ef0273-6d60-4f67-850f-75be5ed437c7" />

### Page 2: Predictive Forecasting and Economic Sensitivity (What-If Analysis)
Enables decision-makers to run real-time corporate forecasting scenarios.
* Strategic Growth and Currency Sliders: Parameterized inputs allowing users to adjust expected growth rates and simulate international currency impact fluctuations.
* Variance Gap Analysis: Dynamic measures calculating the exact delta between actual profits and simulated targets.
* Segmental and Logistics Analysis: Columns and donut charts tracking profit margins across individual Buying Groups and delivery efficiencies based on Package Types including Carton, Case, and Packet.

Dashboard Preview - Page 2:
<img width="1424" height="795" alt="The Dashbord Page2" src="https://github.com/user-attachments/assets/2e958538-25eb-4990-a892-a41c04ffc6b9" />

## Data Engineering and ETL Pipeline (Power Query)
Before modeling, raw tables underwent strict data-cleaning treatments via Power Query Editor:
1. Irrelevant Column Removal: Dropped technical audit fields (Valid From, Valid To, Lineage Key) and uniform or empty rows (Sales Territory, empty Photo attributes) to minimize model size.
2. Data Type Correction: Converted surrogate keys to integers to guarantee primary and foreign key synchronization, and cast financial values (Unit Price, Tax Amount, Profit) to decimals for calculation accuracy.
3. Missing Value Imputation: Replaced invalid placeholders such as ? and - in critical fields like Credit Limit with structured default business thresholds.

## Data Architecture (Star Schema)
The architecture follows a robust Star Schema centered around FactSale, handling over 26,000 records and distributing filters seamlessly through One-to-Many (1:*) single-directional relationships to the following dimensions:
* DimCustomer and DimStockItem: Slicing by demographics and product catalogs.
* DimDate: Enabling time-intelligence filters.
* DimCity and DimEmployee: Driving regional accountability and sales representative metrics.
* CurrencyRates: An API-driven live infrastructure for real-time exchange conversions.

## Advanced DAX Measures Implemented
The analytical core relies on fully customized DAX measures. Key examples include:

* Dynamic Sales Financial Conversion:
    ```dax
    Sales Converted = SUM(FactSale[Total Including Tax]) * SELECTEDVALUE(CurrencyRates[ExchangeRate], 1)
    ```
* Predictive Profit Simulation (What-If):
    ```dax
    Predicted Profit = [Total Profit Converted] * (1 + 'Expected Growth %'[Expected Growth % Value])
    ```
* Prescriptive Performance Tiering:
    ```dax
    Sales Performance = 
    SWITCH(
        TRUE(),
        [Total Sales] >= 5000000, "Exceptional Performance",
        [Total Sales] >= 2000000, "Excellent Performance",
        [Total Sales] >= 500000, "Average Performance",
        "Poor Performance"
    )
    ```

## Project Impact and Strategic Takeaways
* Identified Core Revenue Drivers: Recognized California and Washington as primary business hubs, allowing optimization of geographic resource allocation.
* Risk Mitigation: Enabled financial departments to model sudden economic devaluations or supply chain disruptions instantly using currency sensitivity logic.
* Inventory and Logistics Optimization: Highlighted shipping trends across specific package types, linking lower-margin products with higher transport costs to suggest operational improvements.
