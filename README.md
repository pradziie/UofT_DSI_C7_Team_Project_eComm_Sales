# UofT DSI C7 Team Project eComm Sales
## ProfitLens: Visualizing E-Commerce Trends
<img width="200" height="200" alt="profitLensLogo3" src="https://github.com/user-attachments/assets/fddb7c29-38b7-492e-8d77-59920b1b5698" />

Business proposal - "Our goal is to understand which products, regions, and discount strategies drive the highest profitability and how data-driven decisions can improve business outcomes"

E-Commerce dataset from Kaggle to study how different factors — like products, regions, and discounts — affect sales and profit. We want to find out which areas of the business make the most money and how companies can use data to make smarter decisions.

## Objectives 
Clean and organize the data for analysis. Find patterns between Sales, Profit, and Discounts. Identify which categories and regions are most profitable. Create easy-to-understand charts and graphs to share results. Build a model to predict future profit or sales.

---

## Project Overview (Proposal)

**Business motivation:** Many e-commerce sellers have rich order data but limited visibility into which product categories, regions, and discount strategies drive the most revenue and potential profit. ProfitLens focuses on turning historical Amazon order data into clear, action-oriented insights that can guide pricing, inventory, and fulfillment decisions.

**Dataset selection:** We use the public **“Amazon Sale Report”** dataset from Kaggle. It contains order-level information including product category, quantity, amount, order status, fulfillment type, dates, and shipping details (city, state, postal code). This dataset is stored under `data/raw/Amazon Sale Report.csv`, with a cleaned version exported to `data/processed/Amazon_Sale_Report_Cleaned.csv` from the main analysis notebook in `src/Amazon Sale Report.ipynb`.

**Main questions / research focus:**
- Which product categories contribute the most to overall sales (and proxy profit)?
- Which cities/states and fulfillment channels (Amazon vs Merchant) drive the highest sales volumes?
- How do order status and discount-related variables relate to sales performance?
- What are the key time-based trends in sales, and can simple regression-type relationships help explain variation in revenue?

**Proposed methods / approach:**
- Systematic **data cleaning and feature engineering** in `src/Amazon Sale Report.ipynb` (handling missing values, standardizing text, deriving year/month features, and exporting a cleaned dataset).
- **Exploratory data analysis (EDA)** using bar charts, treemaps, donut charts, and time series plots to explore category, region, fulfillment, and status breakdowns.
- **Correlation and simple regression-style analysis** (in `experiments/Regression_Project_Amazon_Sales - 1.ipynb`) to examine relationships between numeric features such as `Amount`, `Qty`, and `Discount`.
- Visual design aligned with UofT-inspired colour palettes to ensure plots are clear and presentation-ready.

### Responsibilities
- Vikrama: business proposal, naming, data cleaning, experiments, code review
- Iryna: dataset selection, data exploration, KPI development, setting business goals
- Paul: repo management, project tracking, data exploration and cleaning, slides, vizualization, presentation management

### Repository Structure & Reproducibility

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

### Project plan:
Deliverable – End of Week 1 (Project Proposal)

• Business motivation: Explain the problem or opportunity your project addresses and why it matters from a business perspective.

• Dataset selection: Identify which dataset you chose, its source, and the key variables you’ll analyze.

• Project objective / research question: State the main question or hypothesis your analysis or model will answer.

• Proposed methods / approach: Briefly outline how you plan to explore the data (e.g., visualization, regression, classification, etc.).

• Roles and responsibilities: Indicate who is doing what within the team.

• Risks and unknowns: Note any challenges, assumptions, or potential limitations you’ve identified.

• Initial repository structure: Your GitHub repo should follow the suggested folder layout (data/, src/, reports/, etc.) and include a clean .gitignore.

### Project Management tool used
[GitHub Project](https://github.com/projects)

### Risks/Unknowns
* No clear way to calculate profit margins given the datasets
* Lack of cost/BOM data for further analysis
* Time constraints

### Parameters (main ones)
- price
- product quantity
- state
- product type
- date

### Data cleaning temp notes (may be deleted with day one project delivery update):
1. Remove unnecessary columns
The column “index” is just numbering — you can delete it.
“promotion-ids” may contain long text; you can either keep it for later or remove it if not needed for profit analysis.
2. Fix missing values
Some columns have missing entries:
Courier Status, currency, Amount, ship-city, ship-state, fulfilled-by
You can:
Fill missing text fields with "Unknown"
Drop rows with missing Amount (since sales amount is essential)
3. Convert data types
Date should be changed from text to date format (for time-based analysis).
ship-postal-code should be made an integer (it’s currently stored as float).
Columns like Amount should be numeric (already fine)
4. Handle inconsistent text formats
Convert all text columns like Category, ship-state, Status to lowercase to avoid duplicates like “Shipped” vs “shipped”.
Remove extra spaces.
5. Check for duplicate records
Sometimes the same Order ID might appear twice (especially with status changes).
 Keep only the most recent or relevant status.
6. Clean or group categorical values
Combine similar order statuses like "Shipped - Delivered to Buyer" and "Shipped" into one.
Group fulfillment types (e.g., Amazon, Merchant) for consistency.
7. Currency consistency
If the dataset contains multiple currencies, convert them all to one (e.g., INR).
If it’s all INR, confirm and keep the column clean.
8. Optional: Add derived columns
Once clean, you can add:
Profit Margin = Amount / Qty
Month / Year extracted from Date for trend analysis.
After data cleaning, your dataset will be ready to:
Analyze sales by category, city, or fulfillment type
Compare status vs. profit trends
Find seasonal sales patterns
Build visualizations for profitability insights
THIS WE CAN INCLUDE FOR - Data Cleaning Tasks IN README FILE

### Preliminary data analysis ideas:

What to Explore Exploratory Data Analysis (EDA Ideas)
Once cleaned, you can analyze patterns like:

**Product Insights**
Which categories (e.g., kurta, top, dress) sell the most?
Which category brings the highest revenue?

**Regional Insights**
Which states or cities have the most orders?
Are certain regions more profitable?

**Order Performance**
Compare Amazon-fulfilled vs Merchant-fulfilled orders.
Find how many were cancelled, shipped, or pending.

**Sales & Discount Patterns**
How does quantity relate to total amount?
Check if discounts or promotions affect sales volume.

**Time-based Trends**
Which months or days have the most orders or sales?
Detect seasonal spikes in sales (for example, festivals or holidays).
Once the data is clean, you can create charts like:
Bar Chart: Sales by category
Pie Chart: Order status breakdown
Line Chart: Monthly sales trends
Heatmap: Correlation between sales amount, quantity, and discounts

---

## Methods & Key Findings (Current Status)

### Data Cleaning & Feature Engineering
- Removed technical or redundant columns such as `index` and `Unnamed: 22`.
- Standardized column names and cleaned text fields (`Category`, `ship-state`, `Status`, etc.) by trimming whitespace and converting to lowercase to avoid duplicates.
- Converted `Date` to a proper datetime type and derived additional features such as `Year`, `Month`, and `Year-Month` for trend analysis.
- Ensured `Amount` is numeric and dropped rows with missing `Amount` (since sales amount is central to all analyses).
- Cleaned `ship-postal-code` to an integer-like type using pandas nullable integers, and filled key text fields (e.g., `Courier Status`, `ship-city`, `ship-state`, `fulfilled-by`) with "Unknown" when missing.

These transformations are implemented in the `src/Amazon Sale Report.ipynb` notebook and exported as `Amazon_Sale_Report_Cleaned.csv` under `data/processed/`.

### Exploratory Visualizations
Using the main and experiments notebooks, we built several visualizations to answer our core questions:

- **Sales by Category:** Horizontal bar charts highlight the top 10 categories by sales, with the highest-performing category accentuated (e.g., gold highlight). This makes it easy to see which product lines drive the most revenue.
- **Sales by City / Region:** Bar and lollipop charts show the top cities by sales, revealing geographic hotspots where marketing or inventory efforts could be prioritized.
- **Sales by Fulfilment Type:** Bar charts contrast Amazon-fulfilled vs merchant-fulfilled orders, showing which fulfillment strategy is associated with higher sales volume.
- **Order Status Breakdown:** A donut chart summarises the distribution of order statuses (e.g., Shipped, Cancelled, Pending) and aggregates smaller segments into an "Others" category to keep the story readable.
- **Time Series of Monthly Sales:** Line and area plots of monthly sales (with a 3‑month moving average) highlight seasonality, growth/decline periods, and peak months.
- **Correlation Heatmaps:** Numeric correlations between `Amount`, `Qty`, and `Discount` are visualized via heatmaps, providing a quick view of how quantity and discount levels relate to sales.

#### Power BI dashboard - early version
<img width="2817" height="1566" alt="PBI" src="https://github.com/user-attachments/assets/5dc10947-19b8-4274-96d6-d5303dd77402" />

#### Other visualization examples
<img width="989" height="600" alt="saleStatus" src="https://github.com/user-attachments/assets/828ad922-3bbc-4264-bfc1-fd76cef5c2f2" />

### Regression analysis
In the regression-focused notebook (`experiments/Regression_Project_Amazon_Sales - 1.ipynb`), we begin exploring simple regression-style relationships between these numeric variables to better understand drivers of sales.

### Early Business Insights

Based on the current state of analysis (subject to refinement as the project continues):
- A small number of **top product categories** account for a large share of total sales, suggesting an opportunity to double down on high-performing lines while reviewing the long tail of low-selling categories.
- Certain **cities/states appear as clear leaders** in sales volume, indicating priority regions for targeted campaigns, better stock allocation, or localized offers.
- The **order status breakdown** reveals the proportion of cancelled or pending orders, which may hint at operational bottlenecks (e.g., logistics or inventory issues) that reduce realized revenue.
- Correlation analysis shows how **quantity and discounts** are related to `Amount`, offering an early view on how discounting might boost volume and revenue (to be validated with deeper regression modelling).
- Time-series plots show **peak months** where sales spike, which can inform seasonal planning and promotional calendars.

These insights will be refined as we iterate on the regression experiments and potentially incorporate more advanced modelling.

### Presentation link
[placeholder]

Individual team member video links:
[Iryna]()
[Vikrama]()
[Paul]()

## Bonus: UofT color themes for Power BI and Excel

[UofT Excel color theme](https://github.com/pradziie/UofT_DSI_C7_Team_Project_eComm_Sales/blob/main/data/design/color%20themes/Excel_UofT_colors_2025.xml)
(save it under C:\Users\<YourUser>\AppData\Roaming\Microsoft\Templates\Document Themes\Theme Colors\)

[UofT Power BI color theme](https://github.com/pradziie/UofT_DSI_C7_Team_Project_eComm_Sales/blob/main/data/design/color%20themes/UofT%20Power%20BI%20Color%20Theme.json)
(save and import it in Power BI Desktop via View → Themes → Browse for themes)

---

## Future versions:

- Extend the ProfitLens README with final metrics, concrete business recommendations, and links to the main visualizations and any productionized artefacts (reports, dashboards, or saved models in `models/`).
- Ensure fully reproducible setup instructions (environment file or `requirements.txt`) and, if time permits, a lightweight script or notebook entry-point for regenerating all figures from the cleaned dataset.
