# E-commerce Customer Segmentation: RFM Analysis

## Technical Documentation

### Overview
This document provides detailed technical information for the RFM (Recency, Frequency, Monetary) Analysis project performed on e-commerce retail data. The project aims to identify and analyze different customer segments to inform targeted marketing strategies.

## Data Source

- **Dataset:** E-commerce retail dataset
- **Source:** Transactional records from an online retail store
- **Size:** 541,909 records with 8 columns
- **Time Period:** 2010-12-01 to 2011-12-09

## Data Dictionary

| Field       | Description                                                | Data Type       |
|-------------|------------------------------------------------------------|-----------------|
| InvoiceNo   | Unique invoice number                                      | Object          |
| StockCode   | Product code                                               | Object          |
| Description | Product description                                        | Object          |
| Quantity    | Number of products purchased in the transaction            | int64           |
| InvoiceDate | Date and time of the transaction                           | datetime64[ns]  |
| UnitPrice   | Price per unit                                             | float64         |
| CustomerID  | Unique customer identifier                                 | float64         |
| Country     | Country where the customer resides                         | Object          |

## Data Preprocessing Steps

### Data Loading and Exploration
- Loaded data from an Excel file.
- Examined data structure, datatypes, and summary statistics.
- Identified 1,454 missing values in `Description`.
- Found 135,080 missing values in `CustomerID`.
- Detected 5,268 duplicate records.

### Data Cleaning
- Removed rows with missing `CustomerID` values.
- Removed duplicate records.
- Eliminated transactions with negative quantities (representing cancelled orders).
- Eliminated transactions with negative unit prices (representing balance adjustments).
- Converted `CustomerID` to integer type.
- Resulted in **301,020** clean records for further analysis.

## RFM Methodology Implementation

### Recency Calculation
- Set the reference date as **2011-12-31**.
- Computed the number of days between the reference date and the customer's most recent purchase.
- Lower values indicate more recent activity.

### Frequency Calculation
- Counted the unique number of invoices per customer.
- Higher values indicate more frequent purchases.

### Monetary Calculation
- Calculated the total spending per customer.
- Higher values indicate higher spending.

### RFM Scoring
- Divided each RFM metric into quintiles (scores from 1 to 5).
- For **Recency**, a score of 5 represents the most recent activity, while 1 represents the least recent.
- For **Frequency** and **Monetary**, a score of 5 indicates the highest number and spending respectively, and 1 indicates the lowest.
- Combined the individual R, F, and M scores into a 3-digit composite RFM score.

## Customer Segmentation
- Mapped the composite RFM scores to predefined customer segments.
- Created categorical segments such as "Champions," "Loyal Customers," "At Risk," etc., based on the RFM scores.
