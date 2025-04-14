# E-commerce Customer Segmentation: RFM Analysis

## Technical Documentation

### Overview
This project used the RFM (Recency, Frequency, Monetary) Analysis to analyze customer from a online retail store. The project aims to identify and analyze different customer segments to inform targeted marketing strategies. Customers are grouped into segments based on their RFM score. Below is the mapping table used:

| Segment              | RFM Score                                                                                              |
|----------------------|--------------------------------------------------------------------------------------------------------|
| Champions            | 555, 554, 544, 545, 454, 455, 445                                                                       |
| Loyal                | 543, 444, 435, 355, 354, 345, 344, 335                                                                 |
| Potential Loyalist   | 553, 551, 552, 541, 542, 533, 532, 531, 452, 451, 442, 441, 431, 453, 433, 432, 423, 353, 352, 351, 342, 341, 333, 323 |
| New Customers        | 512, 511, 422, 421, 412, 411, 311                                                                       |
| Promising            | 525, 524, 523, 522, 521, 515, 514, 513, 425, 424, 413, 414, 415, 315, 314, 313                         |
| Need Attention       | 535, 534, 443, 434, 343, 334, 325, 324                                                                  |
| About To Sleep       | 331, 321, 312, 221, 213, 231, 241, 251                                                                  |
| At Risk              | 255, 254, 245, 244, 253, 252, 243, 242, 235, 234, 225, 224, 153, 152, 145, 143, 142, 135, 134, 133, 125, 124 |
| Cannot Lose Them     | 155, 154, 144, 214, 215, 115, 114, 113                                                                  |
| Hibernating Customers| 332, 322, 233, 232, 223, 222, 132, 123, 122, 212, 211                                                  |
| Lost Customers       | 111, 112, 121, 131, 141, 151                                                                            |

These segments can be used to guide business decisions, such as:
- Retargeting lost or at-risk customers
- Rewarding champions and loyal buyers
- Engaging promising or new customers to build loyalty

## Dataset Overview
- **Source:** Transactional records from an online retail store
- **Size:** 541,909 records with 8 columns
- **Time Period:** 2010-12-01 to 2011-12-9

## Data Dictionary
| Field       | Description                                                                 | Data Type       |
|-------------|-----------------------------------------------------------------------------|-----------------|
| InvoiceNo   | Invoice number. A 6-digit code uniquely assigned to each transaction. If the code starts with 'C', it indicates a cancellation. | Object          |
| StockCode   | Product (item) code. A 5-digit code uniquely assigned to each product.      | Object          |
| Description | Product (item) name.                                                        | Object          |
| Quantity    | Quantity of each product per transaction.                                   | int64           |
| InvoiceDate | Date and time when the transaction was generated.                           | datetime64[ns]  |
| UnitPrice   | Price per unit in sterling.                                                 | float64         |
| CustomerID  | Customer number. A 5-digit code uniquely identifying each customer.         | float64         |
| Country     | Name of the country where the customer resides.                             | Object          |

## Data Preprocessing Steps

### Data Loading and Exploration
- Loaded data from an Excel file.
- Explored structure, datatypes, and summary statistics.
- Found:
  - 1,454 missing values in `Description`
  - 135,080 missing values in `CustomerID`
  - 5,268 duplicate records

### Data Cleaning
- Removed rows with missing `CustomerID`
- Removed duplicate entries
- Removed transactions with negative `Quantity` or `UnitPrice` (e.g., cancellations or balance adjustments)
- Converted `CustomerID` to integer type
- Resulted in **301,020** clean records

## RFM Methodology Implementation

### Recency Calculation
- Set reference date to **2011-12-31**
- Measured days between the reference date and each customer’s most recent purchase
- Lower values = more recent activity

### Frequency Calculation
- Counted unique invoices per customer
- Higher values = more frequent purchases

### Monetary Calculation
- Summed total spending per customer
- Higher values = higher overall value

### RFM Scoring
- Each metric divided into quintiles (1 to 5)
- **Recency:** 5 = most recent, 1 = least recent
- **Frequency & Monetary:** 5 = most frequent/highest spenders, 1 = least
- RFM scores combined into 3-digit values (e.g., 555 = top tier)

