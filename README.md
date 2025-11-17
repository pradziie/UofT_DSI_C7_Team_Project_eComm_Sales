# UofT DSI C7 Team Project eComm Sales
## ProfitLens: Visualizing E-Commerce Trends
<img width="200" height="200" alt="profitLensLogo3" src="https://github.com/user-attachments/assets/fddb7c29-38b7-492e-8d77-59920b1b5698" />

# Project Overview
 - [Purpose and Overview](#purpose-and-overview)
 - [Methodology](#methodology)
 - [Project Scope](#project-scope)
 - [Responsibilities](#Responsibilities)
 - [Repository Structure & Reproducibility](#Repository-Structure-&-Reproducibility)
 - [Understanding the Data](#understanding-the-data)
 - [Data Cleaning](#data-cleaning)
 - [Data Analysis and Recommendations](#data-analysis-and-recommendations)
 - [Conclusion](#conclusion)
 - [Team Videos](#team-videos)
 - [Bonus: UofT color themes for Power BI and Excel](#bonus-uoft-color-themes-for-power-bi-and-excel)
 - [Credits and Source](#credits)
   
# Purpose and Overview 

Our goal is to understand which products, regions, and discount strategies drive the highest profitability and how data-driven decisions can improve business outcomes. Many e-commerce sellers have rich order data but limited visibility into which product categories, regions, and discount strategies drive the most revenue and potential profit. ProfitLens focuses on turning historical Amazon order data into clear, action-oriented insights that can guide pricing, inventory, and fulfillment decisions.

E-Commerce dataset from Kaggle to study how different factors — like products, regions, and MRP — affect sales and profit. We want to find out which areas of the business make the most money and how companies can use data to make smarter decisions.

---
# Methodology
## Steps taken:
-Data Cleaning: Addressed missing values, corrected inconsistencies, and prepared the dataset for analysis.\
-Exploratory Analysis: Examined data patterns, distributions, and correlations to uncover key relationships.\
-Regression Modeling and Validation: Applied Linear Regression and Random Forest Regressor to analyze factors influencing product popularity and sales performance. Built training and test sets, evaluated model accuracy using metrics such as RMSE and R², and used the insights to understand which products should be prioritized for stocking.\
-Visualization: Developed clear visualizations to communicate insights and model outcomes.\
-Conclusion: Summarized findings, model results, and actionable insights derived from the analysis.

 ## Technical Stack:
 - Python
 - Power BI

 ### Project Management tool used
[GitHub Project](https://github.com/projects)

 ### Libraries Used:
 - Numpy: matrix operations
 - Pandas: data analysis
 - Matplotlib: creating graphs and plots
 - Plotly: creating graphs and plots
 - Seaborn: enhancing matplotlib plots
 - SKLearn: RandomForestRegressor and LinearRegression
   
## Project Scope

**Dataset selection:** We use the public **“Amazon Sale Report”** dataset from Kaggle. It contains order-level information including product category, quantity, amount, order status, fulfillment type, dates, and shipping details (city, state, postal code). This dataset is stored under `data/raw/Amazon Sale Report.csv`, with a cleaned version exported to `data/processed/Amazon_Sale_Report_Cleaned.csv` from the main analysis notebook in `src/Amazon Sale Report.ipynb`.

## Stakeholders
- Business Leadership / Executives - Make strategic decisions based on visualizations.
- Sales & Marketing Teams - Use the insights to decide which promotions to run, and align inventory with demand.
- Operations / Inventory / Supply Chain - Use demand forecasts to optimize stock levels, avoid overstocking low-margin SKUs, and reduce holding costs.

  
**Main questions / research focus:**
- Which product categories contribute the most to overall sales (and proxy profit)?
- Which cities/states and fulfillment channels (Amazon vs Merchant) drive the highest sales volumes?
- How do order status and discount-related variables relate to sales performance?
- What are the key time-based trends in sales, and can simple regression-type relationships help explain popularity of the product?

**Proposed methods / approach:**
- Systematic **data cleaning and feature engineering** in `src/Amazon Sale Report.ipynb` (handling missing values, standardizing text, deriving year/month features, and exporting a cleaned dataset).
- **Exploratory data analysis (EDA)** using bar charts, treemaps, donut charts, and time series plots to explore category, region, fulfillment, and status breakdowns.
- **Correlation and simple regression-style analysis** (in `experiments/Regression_Project_Amazon_Sales - 1.ipynb`) to examine relationships between numeric features such as `Amount`, `Qty`, and `Discount`.
- Visual design aligned with UofT-inspired colour palettes to ensure plots are clear and presentation-ready.

### Responsibilities
- Vikrama: business proposal, naming, data cleaning, experiments, code review
- Iryna: dataset selection, data exploration, KPI development, setting business goals, linear and random forest regression experiments
- Paul: repo management, project tracking, data exploration and cleaning, slides, vizualization, presentation management

# Repository Structure & Reproducibility

The repository follows the recommended teaching structure from the Team Project guidelines, with a few project-specific additions (some duplication was needed for backups and reproducibility):

```
├── .copilot-tasks/
├── .git/
├── .gitignore
├── README.md
├── data/
│   ├── design/
│   │   └── logos/
│   ├── processed/
│   │   └── Amazon_Sale_Report_Cleaned.csv
│   ├── raw/
│   │   ├── Amazon Sale Report.csv
│   │   ├── Amazon Sale Report.ipynb
│   │   ├── Cloud Warehouse Compersion Chart.csv
│   │   ├── Expense IIGF.csv
│   │   ├── International sale Report.csv
│   │   ├── May-2022.csv
│   │   ├── P  L March 2021.csv
│   │   ├── Sale Report.csv
│   │   ├── monthly_sales_trend.csv
│   │   ├── sales_by_category.csv
│   │   ├── sales_by_city.csv
│   │   ├── sales_by_fulfillment.csv
│   │   └── status_vs_sales.csv
│   └── temp/
├── experiments/
│   ├── Amazon Sale Report.ipynb
│   ├── Regression_Project_Amazon_Sales - 1.ipynb
│   ├── Test-File-1.ipynb
│   └── outputs/
├── materials/
│   └── presentations/
├── models/
├── reports/
├── src/
│   ├── Amazon Sale Report.ipynb
│   ├── Regression_Project_Amazon_Sales - 1.ipynb
│   ├── Amazon-Sales_Report-Power-BI.pbix
│   └── data/
│       └── processed/
│           └── Amazon_Sale_Report_Cleaned.csv
└── temp/
```

To reproduce the analysis:
1. Create and activate a Python environment with `pandas`, `numpy`, `matplotlib`, `seaborn`, and `plotly` installed.
2. Place the raw Kaggle file as `data/raw/Amazon Sale Report.csv` (or use the provided copy in this repo).
3. Run the notebook `src/Amazon Sale Report.ipynb` from the project root. The notebook loads the raw file using **relative paths** via `pathlib`, performs cleaning, and exports `data/processed/Amazon_Sale_Report_Cleaned.csv`.
4. Optional: Open `experiments/Regression_Project_Amazon_Sales - 1.ipynb` to explore additional regression-focused experiments.

 # Understanding the Data
 ### Parameters (main ones)
- price
- product quantity
- state
- product type
- date
- amount
# Data Cleaning
- Removed technical or redundant columns such as `index` and `Unnamed: 22`.
- Standardized column names and cleaned text fields (`Category`, `ship-state`, `Status`, etc.) by trimming whitespace and converting to lowercase to avoid duplicates.
- Converted `Date` to a proper datetime type and derived additional features such as `Year`, `Month`, and `Year-Month` for trend analysis.
- Ensured `Amount` is numeric and dropped rows with missing `Amount` (since sales amount is central to all analyses).
- Cleaned `ship-postal-code` to an integer-like type using pandas nullable integers, and filled key text fields (e.g., `Courier Status`, `ship-city`, `ship-state`, `fulfilled-by`) with "Unknown" when missing.

These transformations are implemented in the `src/Amazon Sale Report.ipynb` notebook and exported as `Amazon_Sale_Report_Cleaned.csv` under `data/processed/`.

# Data Analysis And Recommendations

Based on this pie chart, the recommendation is to introduce targeted promotions designed to increase repeat purchases.


<img width="572" height="599" alt="image" src="https://github.com/user-attachments/assets/77395e60-4d70-4730-a556-07196e5ddb40" />

### Repeat Purchases can be increased through:
1. Personalized Promotions - Customers respond better when offers feel relevant.
Examples:
- Discounts based on previous purchases
- “We miss you” promo after 30 days of no activity
- Bundle discounts on frequently bought-together items
- Personalized emails with product recommendations
  
2. Loyalty or Rewards Program - Make customers feel rewarded for coming back.
- Points for every purchase
- Tier levels (Silver, Gold, Platinum)
- Birthday or anniversary rewards
  
3. Post-Purchase Follow-Up - Customers often buy again if they feel supported.
- Send order follow-up email with product care tips
- Ask for a review (and give a small incentive)
- Suggest complementary products
  
4. Create Urgency or Exclusivity - People buy again when they feel they might miss out.
- Limited-time deals
- Members-only sales
- New product drops with early access
  
#  Applied Linear Regression and Random Forest Regressor to analyze factors influencing product popularity
In the regression-focused notebook (`experiments/Regression_Project_Amazon_Sales - 1.ipynb`), we begin exploring simple regression-style relationships between these numeric variables to better understand drivers of sales.
### SKU-Level Linear Regression: What Sells Most
This version aggregates all orders by SKU to get each product’s total quantity sold and average amount.
Then it fits a linear regression model to see which attributes drive higher total sales.
Overall model
RMSE: 19.35 - SKU-level sales vary a lot; some SKUs sell hundreds while most sell few - normal.
R²: 0.0455 - Product attributes explain only 4.5% of variation in sales. But the coefficients still show clear patterns of what sells more.
Because it explains only for 4.5% of variation in sales, Sku-Level REgression was tested (Random Forest REgressor). 

### Random Forest Regressor gave the following results:

RMSE: 2.55 -  on average, the model's predicted SKU counts are off by about 2.5 units, meaning predictions are reliable.
R²: 0.9835 - the model explains 98.35% of the variance in SKU demand/popularity.
The SKU’s performance is driven heavily by overall spending behavior, not by product attributes like size, category, or fulfillment type.

### Recomendation based on RFR model:
1. Pricing & Inventory.
Focus on TotalAmount/price points: Since sales are highly driven by the total value of SKUs, consider adjusting inventory and promotions around high-value items.
- Stock high-selling SKUs heavily:
- Western Dresses (L/M/S)
- Sets (S/M/XL)
- Kurta (L/S)
Ensuring these SKUs are always in stock can maximize revenue.

2. Product & Category Strategy.
- Promote top categories: Western Dresses and Sets are consistently top-sellers.
- Consider expanding variants in the top-selling sizes (L and M) to capture more demand.
- Lower emphasis on less influential categories until there is data showing potential growth.

# Model Performance Summary:
Both models identify the same top-selling SKUs and use the same features, but the quality of insights is very different. Random Forest produces accurate predictions and meaningful feature importance, while Linear Regression provides weak predictions and unstable, contradictory coefficients.

### Results of RFR are also supported by 
Sales by Category bar chart:

<img width="714" height="528" alt="image" src="https://github.com/user-attachments/assets/c7002c46-9e9f-4a2b-b0b8-b70a6dc3325b" />
### More Recommendations

Top 10 Cities by Sales suggests which cities are important for stocking:

<img width="895" height="479" alt="image" src="https://github.com/user-attachments/assets/6f43e01e-04b3-4861-844f-4fa645a6dbbf" />

Recommendations based on Orders by Fulfilment chart.\
<img width="406" height="269" alt="image" src="https://github.com/user-attachments/assets/7f7fb80c-c68f-4019-8f46-a9850971229c" />

1. Increase Amazon-Fulfilled (FBA) Inventory
Since 70% of our demand naturally prefers FBA, we should ensure:
- FBA inventory is never out of stock
- High-velocity SKUs (your top sellers) always have FBA coverage
- Reduce long-term storage fees by trimming slow-moving FBA items, but keep fast movers stocked

2. Improve FBM Performance for Cost Efficiency
Since we still have 31% FBM, optimize it rather than eliminating it.
- Ensure fast dispatch times
- Maintain accurate stock to avoid cancellations
- Improve packaging/handling time
- Use regional carriers with cheaper rates
 

### Extra Visualizations
Using the main and experiments notebooks, we built several visualizations to answer our core questions:

- **Sales by Category:** Horizontal bar charts highlight the top 10 categories by sales, with the highest-performing category accentuated (e.g., gold highlight). This makes it easy to see which product lines drive the most revenue.
- **Sales by City / Region:** Bar and lollipop charts show the top cities by sales, revealing geographic hotspots where marketing or inventory efforts could be prioritized.
- **Sales by Fulfilment Type:** Bar charts contrast Amazon-fulfilled vs merchant-fulfilled orders, showing which fulfillment strategy is associated with higher sales volume.
- **Order Status Breakdown:** A donut chart summarises the distribution of order statuses (e.g., Shipped, Cancelled, Pending) and aggregates smaller segments into an "Others" category to keep the story readable.
- **Time Series of Monthly Sales:** Line and area plots of monthly sales (with a 3‑month moving average) highlight seasonality, growth/decline periods, and peak months.
- **Correlation Heatmaps:** Numeric correlations between `Amount`, `Qty`, and `Discount` are visualized via heatmaps, providing a quick view of how quantity and discount levels relate to sales.

#### Power BI dashboard.
<img width="2817" height="1566" alt="PBI" src="https://github.com/user-attachments/assets/5dc10947-19b8-4274-96d6-d5303dd77402" />

#### Other visualization examples
<img width="989" height="600" alt="saleStatus" src="https://github.com/user-attachments/assets/828ad922-3bbc-4264-bfc1-fd76cef5c2f2" />

### Regression analysis
In the regression-focused notebook (`experiments/Regression_Project_Amazon_Sales - 1.ipynb`), we begin exploring simple regression-style relationships between these numeric variables to better understand drivers of sales.

# Conclusion

Based on the current state of analysis (subject to refinement as the project continues):
- A small number of **top product categories** account for a large share of total sales, suggesting an opportunity to double down on high-performing lines while reviewing the long tail of low-selling categories.
- Certain **cities/states appear as clear leaders** in sales volume, indicating priority regions for targeted campaigns, better stock allocation, or localized offers.
- The **order status breakdown** reveals the proportion of cancelled or pending orders, which may hint at operational bottlenecks (e.g., logistics or inventory issues) that reduce realized revenue.
- Correlation analysis shows how **quantity and discounts** are related to `Amount`, offering an early view on how discounting might boost volume and revenue (to be validated with deeper regression modelling).
- Time-series plots show **peak months** where sales spike, which can inform seasonal planning and promotional calendars.
Our recommendation for the business stakeholders is to make use of the Random Forest Regression model as a decision-support tool but not yet a fully autonomous system. Continuous improvement is needed in expanding dataset and cross-department data collaboration to enrich model inputs and model maturity.

## Presentation links
[placeholder for team presentation]

Individual team member video links:

####[Iryna](https://drive.google.com/file/d/1LB2xYGn2IAvMGN7PT1Lnmuflfl_v5SPW/view?usp=sharing)

####[Vikrama]( https://youtu.be/Xg_bB7GBvIo )

####[Paul](https://youtu.be/wv9CWg1ii7A)

## Bonus: UofT color themes for Power BI and Excel

[UofT Excel color theme](https://github.com/pradziie/UofT_DSI_C7_Team_Project_eComm_Sales/blob/main/data/design/color%20themes/Excel_UofT_colors_2025.xml)
(save it under C:\Users\<YourUser>\AppData\Roaming\Microsoft\Templates\Document Themes\Theme Colors\)

[UofT Power BI color theme](https://github.com/pradziie/UofT_DSI_C7_Team_Project_eComm_Sales/blob/main/data/design/color%20themes/UofT%20Power%20BI%20Color%20Theme.json)
(save and import it in Power BI Desktop via View → Themes → Browse for themes)


## Credits and Source
  
The data was sourced from Kaggle.\
[E-commerce-sales](https://www.kaggle.com/datasets/thedevastator/unlock-profits-with-e-commerce-sales-data)

## Future versions:

- Extend the ProfitLens README with final metrics, concrete business recommendations, and links to the main visualizations and any productionized artefacts (reports, dashboards, or saved models in `models/`).
- Ensure fully reproducible setup instructions (environment file or `requirements.txt`) and, if time permits, a lightweight script or notebook entry-point for regenerating all figures from the cleaned dataset.
