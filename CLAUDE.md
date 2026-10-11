# Contoso PBI Report

## What it does and the problem it solves
This project is a Power BI report built on Microsoft's Contoso BI Demo Dataset (retail). The report gives management, sales/marketing and finance a unified view of retail operations: sales, profit and margin over time, by product category, store and region, and comparisons against budget.

The problem it solves: raw data is spread across many tables in a data warehouse and is hard to interpret. The report makes key figures accessible and interactive, so decision-makers can see trends and deviations without writing SQL.

## Tech stack and why
- **Data source: SQL Server, the `ContosoRetailDW` database** (restored from `ContosoRetailDW.bak`). This is the relational model of the Contoso dataset and is well suited for reporting.
- **Power BI Desktop** for the data model, measures and report design. It is the tool the dataset was made to demonstrate.
- **Power Query (M)** for data cleaning and transformation on load.
- **DAX** for all calculated measures (e.g. total sales, profit margin, YoY growth).
- **GitHub** for version control of documentation and exported report files/scripts.

## Architecture principles
- **Star schema:** fact tables (e.g. `FactSales`) in the center, with dimension tables (`DimDate`, `DimProduct`, `DimStore`, `DimGeography`) around them. Relationships are one-to-many with single filter direction unless otherwise justified.
- **Measures, not columns:** calculations are done as DAX measures, not calculated columns, unless necessary.
- **One measure does one thing:** build complex measures from simpler ones.
- **Measures live in their own table** (`_Measures`) and have clear, consistent names.
- **Transformations happen in Power Query**, not in visuals or DAX.
- **Load only what is needed:** remove unused columns and tables to keep the model small and fast.
- **Simple, readable design:** a few key messages per page, consistent colors and clear titles.
- **Document:** every measure and key assumption should have a short description.

## What the agent must NOT do
- Change, write to or replace the source database `ContosoRetailDW`. It is read-only reference data.
- Add external data sources or connections without asking first.
- Hardcode numbers in visuals or measures.
- Create calculated columns when a measure is enough.
- Delete or rename existing measures and tables without asking.
- Put passwords, connection credentials or sensitive information in the repo.
- Change the star schema structure or relationships without explaining why.
- Upload large files (e.g. the `.bak` or `.abf` files) to the repo.
