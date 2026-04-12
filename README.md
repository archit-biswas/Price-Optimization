
# Price Optimization using Python

## Project Overview

This project demonstrates a price optimization strategy using Python, leveraging data analysis and modeling to determine effective pricing for products or services. The goal is to maximize profitability and market share by considering factors such as market demand, competition, costs, and customer behavior.

## Dataset

The analysis uses a dataset containing the following key columns:

*   `Fiscal_Week_ID`: Identifier for the fiscal week.
*   `Store_ID`: Unique identifier for each store.
*   `Item_ID`: Unique identifier for each product item.
*   `Price`: The store's selling price for the item.
*   `Item_Quantity`: The quantity of the item sold.
*   `Sales_Amount_No_Discount`: Sales amount before any discounts.
*   `Sales_Amount`: Sales amount after applying discounts.
*   `Competition_Price`: The price of the same item offered by competitors.

## Methodology

The project follows a structured approach to price optimization:

1.  **Data Loading and Initial Exploration**: 
    *   Loaded the `Competition_Data.csv` dataset into a Pandas DataFrame.
    *   Inspected the data structure and types using `df.head()` and `df.info()` to ensure data quality and identify potential issues.

2.  **Price Distribution Analysis**: 
    *   Visualized the price distributions for our store and the competition using histograms to understand market positioning.
    *   *Observation*: Competition generally had higher prices with specific peaks, while our store's prices were more evenly distributed.

3.  **Price vs. Sales Amount Relationship**: 
    *   Used scatter plots to examine the relationship between price and sales amount for both our store and the competition.
    *   *Observation*: Our store showed varied performance without a clear trend, while the competition showed denser clustering of higher sales amounts.

4.  **Price Changes Over Time**: 
    *   Converted `Fiscal_Week_ID` to datetime objects.
    *   Plotted the average price trends over time for both our store and the competition.
    *   *Observation*: Competition maintained higher and more stable average prices, whereas our store experienced more fluctuations.

5.  **Price Elasticity of Demand Calculation**: 
    *   Calculated price elasticity of demand (`elasticity = (qty_change / price_change)`) to understand how sensitive demand is to price changes.
    *   Plotted elasticity over time, revealing significant variability.
    *   *Observation*: Demand response to price changes was inconsistent, suggesting other factors (promotions, seasonality) influence sales.

6.  **Total Sales Comparison**: 
    *   Compared total sales amounts between our store and the competition.
    *   *Observation*: Competition significantly outperformed our store in total sales, highlighting the need for optimization.

7.  **Sales by Price Bracket Analysis**: 
    *   Segmented sales into various price brackets (e.g., 0-50, 51-100, etc.).
    *   Compared sales performance within each bracket for our store and the competition.
    *   *Observation*: Competition consistently outperformed our store across most price brackets, especially in lower-to-mid ranges.

8.  **Dynamic Pricing Model Development**: 
    *   Segmented items based on average price into 'Low', 'Medium', and 'High' categories.
    *   Calculated average price elasticity for each segment.
    *   Defined dynamic pricing rules: 
        *   **Medium Segment (Elasticity ~0.15)**: Increased price by 5% due to relatively inelastic demand.
        *   **High Segment (Elasticity ~0.15)**: Decreased price by 10% to test the impact, assuming some price sensitivity despite low elasticity.

9.  **Dynamic Pricing Simulation**: 
    *   Applied the dynamic pricing rules to a copy of the dataset.
    *   Calculated new sales amounts based on the dynamic prices.
    *   Compared total sales amounts between the existing and dynamic pricing strategies.

## Key Findings & Results

*   **Competition's Superiority**: The competition consistently demonstrated higher average prices, more stable pricing strategies, and significantly greater total sales across most price brackets compared to our store.
*   **Inconsistent Demand Response**: Our store's price elasticity of demand showed high variability, indicating that sales are influenced by multiple factors beyond just price.
*   **Dynamic Pricing Effectiveness**: The simulation of the dynamic pricing model, with targeted price adjustments based on segment elasticity, showed a **substantial increase in total sales amount** (from approximately 1.14e+08 to 6.22e+08), demonstrating its potential to significantly boost revenue.

## Future Improvements

*   **Incorporate more features**: Integrate additional features such as promotions, seasonality, and inventory levels into the pricing model for more accurate predictions.
*   **Advanced Elasticity Modeling**: Implement more sophisticated models for calculating price elasticity, such as regression analysis, to capture non-linear relationships and interactions between variables.
*   **Machine Learning Models**: Explore machine learning algorithms (e.g., Random Forests, Gradient Boosting) for dynamic pricing that can learn complex patterns and adapt to changing market conditions.
*   **A/B Testing**: Design and implement A/B tests to validate the effectiveness of dynamic pricing strategies in a real-world scenario.
*   **Cost Analysis**: Incorporate cost data to ensure that price adjustments not only maximize revenue but also maintain healthy profit margins.
*   **Real-time Data Integration**: Develop a system for real-time data ingestion and price adjustments to respond quickly to market changes.

## How to Run the Notebook

To run this analysis and simulation, follow these steps:

1.  **Clone the Repository (if applicable)**:
    ```bash
    git clone <repository_url>
    cd <project_directory>
    ```

2.  **Ensure Data Availability**: Make sure the `Competition_Data.csv` file is accessible at the specified path (e.g., `/content/drive/MyDrive/Colab Notebooks/Price Optimization Project/Competition_Data.csv`). Adjust the path in the code if your file location is different.

3.  **Install Dependencies**: The project primarily uses `pandas` and `matplotlib`. Ensure you have these libraries installed:
    ```bash
    pip install pandas matplotlib
    ```
    (These are typically pre-installed in Google Colab environments.)

4.  **Open in Google Colab**: Upload the `.ipynb` file to Google Colab or open it directly if it's hosted there.

5.  **Run Cells**: Execute the cells sequentially from top to bottom. The notebook is designed to run in order.

## Technologies Used

*   Python 3
*   Pandas (for data manipulation and analysis)
*   Matplotlib (for data visualization)

## Conclusion

This project successfully outlines a data-driven approach to price optimization. By understanding competitive landscapes, demand elasticity, and the impact of price on sales, it's possible to implement dynamic pricing strategies that lead to significant revenue improvements. The simulation demonstrated the power of tailored pricing adjustments in maximizing sales performance.
```
