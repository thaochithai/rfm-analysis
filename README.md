# E-commerce Customer Segmentation with RFM Analysis
![E-com RFM](https://img.shields.io/badge/Ecommerce-FRM_Customer_Segmentation-green)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

## 📊 Project Overview
This project applies RFM (Recency, Frequency, Monetary) analysis to segment customers of a UK-based online retail store that sells all-occasion gifts. By categorizing customers based on their purchasing behavior, I aim to deliver actionable insights that enable targeted marketing strategies and optimize customer engagement.

### Key Objectives:
- Segment customers based on their purchasing patterns
- Identify high-value customer groups and growth opportunities
- Provide actionable recommendations for each segment
- Optimize marketing strategy

## 💼 Business Context
Understanding different customer segments allows businesses to:
- Target marketing efforts more effectively
- Develop personalized communication strategies
- Optimize resource allocation
- Increase customer retention and lifetime value

## 📋 Dataset Information
- **Source:** Online retail transaction records
- **Size:** 541,909 records with 8 columns
- **Time Period:** December 2010 to December 2011
- **Fields:** Customer purchases, including invoice details, products, quantities, prices, and customer information

### Data Dictionary
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

## 🔍 Methodology
The project follows these key steps:

### 1. Data Exploration & Preprocessing
- Explored structure, datatypes, and summary statistics
  - 1,454 missing values in `Description`
  - 135,080 missing values in `CustomerID`
  - 5,268 duplicate records

**Data Preprocessing:**
- Removed rows with missing `CustomerID`
- Removed duplicate entries
- Negative values in `Quantity` indicate cancelled orders (removed), while negative values in `UnitPrice` represent balance adjustments (removed)
- Converted `CustomerID` to integer type
- Resulted in **301,020** clean records

### 2. RFM Calculation
- **Recency:** Days since last purchase (as of December 31, 2011)
- **Frequency:** Number of unique purchases
- **Monetary:** Total customer spend

### 3. Customer Segmentation
- Scored each RFM dimension on a scale of 1 to 5
- Combined R, F, M scores into a 3-digit composite RFM score
- Mapped scores to customer segments using predefined rules:

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

### 4. Analysis & Visualization
- Analyzed segment distribution and value contribution
- Created visualizations to understand segment characteristics
- Calculated key metrics like Average Basket Size (ABS) per segment

## 🌟 Key Findings

### Customer Segmentation
The analysis identified 11 distinct customer segments:
<p align="center">
  <img src="https://github.com/user-attachments/assets/cf55a502-1d2d-439e-b737-86e018caf0dc" width=750px />
</p>


### Customer Behavior Patterns
- Nearly half of customers made purchases within the last 50 days
- Typical purchase frequency is between 10-25 orders
- Strong correlation between frequency and monetary value

<p align="center">
  <img src="https://github.com/user-attachments/assets/42939494-41fe-4fa9-b3ad-c18782468bb5" width="90%" />
  <img src="https://github.com/user-attachments/assets/caf051c8-f1dd-4149-bda7-717ebc3a9a37" width="45%" />
</p>

### Average Basket Size (ABS) per Segment
Average ABS across all segments is **£1,479.80**.
"At Risk" and "Need Attention" segments have relatively high ABS, just below the average — these are valuable opportunities to nurture.

| Segment               | Customer Count | Monetary Value | Avg. ABS (£) |
|-----------------------|----------------|----------------|------------------|
| Champions             | 837            | 4,007,874      | 4,788.38         |
| Loyal                 | 409            | 697,600        | 1,705.62         |
| Cannot Lose Them      | 101            | 169,279        | 1,676.03         |
| Need Attention        | 278            | 363,736        | 1,308.40         |
| At Risk               | 425            | 544,726        | 1,281.71         |
| Promising             | 134            | 85,762         | 640.01           |
| Potential Loyalist    | 427            | 157,627        | 369.15           |
| Hibernating Customers | 662            | 186,213        | 281.29           |
| About To Sleep        | 298            | 55,387         | 185.86           |
| New Customers         | 267            | 38,547         | 144.37           |
| Lost Customers        | 466            | 62,331         | 133.76           |

## 💡 Strategic Recommendations

### High-Value Segments
Champions: These customers purchase frequently and recently, with the highest average monetary value.
→ Strategy: Leverage this segment with premium product offerings and high Average Basket Size (ABS) SKUs. Ensure strong retention with exclusive perks or early access to new collections.

#### Loyal Customers: This group shows consistent purchasing behavior with strong potential for long-term value.
→ Strategy: Maintain engagement through personalized offers, loyalty points, and feedback loops to reinforce loyalty and prevent churn.

#### At Risk: Customers here have shown moderate value but are slipping in recency. This could be due to one-off or declining purchases.
→ Strategy: Re-engage with recurring promotions, personalized win-back campaigns, or reminders based on their past preferences to boost frequency and recency.

### Growth & Potential Segments
Potential Loyalists / New Customers / Promising: These segments reflect new or infrequent buyers with lower monetary contribution.

→ Strategy:
 - For new buyers: Offer first-time incentives like welcome vouchers, free shipping, or starter bundles to increase basket size and conversion.
 - For potential loyalists: Introduce tiered loyalty programs, early loyalty discounts, or referral bonuses to nudge them into higher engagement and spending.

### Key Opportunity
While Champions and Loyal Customers are top-performing groups in terms of value, many segments represent large customer bases with low monetary value.
→ Strategy: Focus on increasing Average Basket Size and Order Value through better cross-sell/upsell tactics, bundling offers, and value-based promotions.
