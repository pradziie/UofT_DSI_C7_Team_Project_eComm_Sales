# UofT DSI C7 Team Project eComm Sales
## ProfitLens: Visualizing E-Commerce Trends

Business proposal - "Our goal is to understand which products, regions, and discount strategies drive the highest profitability and how data-driven decisions can improve business outcomes"

E-Commerce dataset from Kaggle to study how different factors — like products, regions, and discounts — affect sales and profit. We want to find out which areas of the business make the most money and how companies can use data to make smarter decisions.

## Objectives 
Clean and organize the data for analysis. Find patterns between Sales, Profit, and Discounts. Identify which categories and regions are most profitable. Create easy-to-understand charts and graphs to share results. Build a model to predict future profit or sales

### Data cleaning temp notes:
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
