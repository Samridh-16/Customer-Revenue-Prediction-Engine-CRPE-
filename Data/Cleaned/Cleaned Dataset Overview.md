# Cleaned Online Retail Dataset
 
## Overview
 
This folder contains the cleaned transaction-level dataset used in the **Customer Purchase Probability & Revenue Forecasting Engine** project.
 
The dataset is derived from the UCI Online Retail dataset and has been prepared for customer-level analysis, feature engineering, purchase-probability modeling, and revenue prediction.
 
The original transaction data contains records of purchases made by customers of a UK-based online retail business. The cleaned version focuses on valid, identifiable customer purchases and provides a consistent transaction-level structure for downstream analysis.
 
---
 
## Dataset Summary
 
| Attribute           | Details                                            |
| ------------------- | -------------------------------------------------- |
| Dataset type        | Transaction-level retail data                      |
| Source              | UCI Online Retail Dataset                          |
| Cleaned records     | 397,884 transactions                               |
| Columns             | 9                                                  |
| Granularity         | One row per transaction line                       |
| Customer identifier | `CustomerID`                                       |
| Main use            | Customer behavior analysis and predictive modeling |
 
---
 
## Cleaning Process
 
The raw transaction data was processed before being used for modeling.
 
### 1. Customer identification
 
Transactions without a valid `CustomerID` were removed.
 
This ensures that each retained transaction can be associated with a specific customer and allows the data to be aggregated into customer-level behavioral features.
 
### 2. Invalid and return transactions
 
Transactions with:
 
* `Quantity <= 0`
* `UnitPrice <= 0`
were removed from the modeling dataset.
 
This excludes return/cancellation records and transactions that do not represent positive-value purchases.
 
### 3. Revenue calculation
 
A new `Revenue` column was created using:
 
`Revenue = Quantity × UnitPrice`
 
This provides the monetary value of each transaction line and is later aggregated to calculate customer-level revenue.
 
---
 
## Column Description
 
The cleaned dataset contains the following fields:
 
| Column        | Description                                              |
| ------------- | -------------------------------------------------------- |
| `InvoiceNo`   | Unique invoice or transaction identifier                 |
| `StockCode`   | Product or stock identifier                              |
| `Description` | Product description                                      |
| `Quantity`    | Number of units purchased                                |
| `InvoiceDate` | Date and time of the transaction                         |
| `UnitPrice`   | Price per unit                                           |
| `CustomerID`  | Unique identifier for the customer                       |
| `Country`     | Customer's country                                       |
| `Revenue`     | Transaction revenue calculated as `Quantity × UnitPrice` |
 
---
 
## Example Structure
 
A typical record in the cleaned dataset follows this structure:
 
```text
InvoiceNo | StockCode | Description | Quantity | InvoiceDate | UnitPrice | CustomerID | Country | Revenue
```
 
For example, conceptually:
 
```text
536365 | 85123A | WHITE HANGING HEART T-LIGHT HOLDER | 6 | 2010-12-01 08:26 | 2.55 | 17850 | United Kingdom | 15.30
```
 
The actual dataset contains **397,884 cleaned transaction records**.
 
---
 
## Data Granularity
 
This is a **transaction-line-level dataset**, not a customer-level dataset.
 
A customer may therefore appear in multiple rows because a customer can:
 
* place multiple orders,
* purchase multiple products within an order,
* make purchases on different dates.
The dataset is subsequently aggregated into customer-level features during the feature-engineering stage.
 
---
 
## Relationship to the Modeling Pipeline
 
The cleaned dataset is the foundation of the project's modeling pipeline:
 
```text
Cleaned Transaction Data
          ↓
Customer-Level Aggregation
          ↓
RFM Features
          ↓
Additional Behavioral Features
          ↓
30-Day Purchase Target
          ↓
30-Day Revenue Target
          ↓
Machine Learning Models
          ↓
Expected Revenue
          ↓
Customer Prioritization
```
 
The next stage of the project converts these transaction-level records into customer-level features such as:
 
* Recency
* Frequency
* Monetary value
* Customer lifespan
* Average order value
* Purchase rate
These features are then used to predict future customer purchasing behavior and revenue.
 
---
 
## Why the Cleaned Dataset Is Not Included Directly
 
The processed transaction-level CSV is larger than GitHub's standard web-upload file limit.
 
Rather than storing a large derived file in the repository, the cleaning process is documented in:
 
`01_data_exploration.ipynb`
 
The cleaned dataset can therefore be reproduced by running the preprocessing workflow on the original UCI Online Retail data.
 
Customer-level datasets used in the modeling stage are provided separately where applicable.
 
---
 
## Reproducibility
 
To reproduce this dataset:
 
1. Obtain the original UCI Online Retail dataset.
2. Load the transaction data using the workflow in `01_data_exploration.ipynb`.
3. Remove records without `CustomerID`.
4. Retain transactions where `Quantity > 0` and `UnitPrice > 0`.
5. Calculate `Revenue` as `Quantity × UnitPrice`.
6. Save the resulting transaction-level dataset as the cleaned dataset.
The notebook contains the actual preprocessing workflow used in this project.
 
---
 
## Role in the Project
 
This cleaned dataset serves as the bridge between the **raw retail transaction data** and the project's **customer-level predictive modeling**.
 
It provides a consistent foundation for analyzing purchasing behavior and ultimately supports the project's objective of estimating:
 
1. the probability that a customer will make a purchase within the next 30 days, and
2. the revenue that the customer may generate during that period.
The resulting predictions are combined into an **Expected Revenue** score for simulated customer prioritization.
 
