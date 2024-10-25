# task-1
# Import necessary libraries
import pandas as pd

# Load data from a CSV file
data = pd.read_csv('sales_data.csv')

# Display the first few rows of the data
print("Initial Data:\n", data.head())

# 1. Data Cleaning
# Remove rows with missing values
data.dropna(inplace=True)

# Convert data types if necessary
data['Date'] = pd.to_datetime(data['Date'])  # Convert 'Date' column to datetime
data['Sales'] = data['Sales'].astype(float)  # Convert 'Sales' column to float

# 2. Filtering Data
# Filter for sales data after January 1, 2023
filtered_data = data[data['Date'] > '2023-01-01']

# 3. Aggregating Data
# Group by 'Product' and calculate total sales
total_sales_per_product = filtered_data.groupby('Product')['Sales'].sum()

# 4. Adding a New Column
# Add a column for cumulative sales
filtered_data['Cumulative_Sales'] = filtered_data['Sales'].cumsum()

# 5. Sorting Data
# Sort data by 'Date' and 'Sales' in descending order
sorted_data = filtered_data.sort_values(by=['Date', 'Sales'], ascending=[True, False])

# Display processed data
print("Filtered and Processed Data:\n", sorted_data.head())
print("Total Sales Per Product:\n", total_sales_per_product)
# Output
Sample Data (sales_data.csv):

Date	Product	Sales
2023-01-05	ProductA	200
2023-02-10	ProductB	150
2023-01-15	ProductA	300
2023-03-12	ProductC	250
2023-02-20	ProductB	100
2022-12-25	ProductC	200
2023-01-28	ProductA	150
2023-04-01	ProductC	300
Expected Output:

plaintext
Copy code
Initial Data:
          Date   Product  Sales
0  2023-01-05  ProductA    200
1  2023-02-10  ProductB    150
2  2023-01-15  ProductA    300
3  2023-03-12  ProductC    250
4  2023-02-20  ProductB    100

Filtered and Processed Data:
         Date   Product  Sales  Cumulative_Sales
0 2023-01-05  ProductA    200               200
2 2023-01-15  ProductA    300               500
6 2023-01-28  ProductA    150               650
1 2023-02-10  ProductB    150               800
4 2023-02-20  ProductB    100               900

Total Sales Per Product:
Product
ProductA    650
ProductB    250
ProductC    550
Name: Sales, dtype: float64
