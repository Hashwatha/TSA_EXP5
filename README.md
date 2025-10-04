# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 
## AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.
## ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

## PROGRAM:
```
# Import necessary modules
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Step 1: Load dataset (without parse_dates first)
data = pd.read_csv("cardekho.csv")

print("Dataset Head:")
print(data.head())
print("\nDataset Columns:")
print(data.columns)

# Step 2: If 'year' column exists, convert it to datetime
# (change 'year' to the actual column name if different)
if 'year' in data.columns:
    data['sale_date'] = pd.to_datetime(data['year'], format='%Y')
    data.set_index('sale_date', inplace=True)
else:
    raise ValueError("Dataset does not have a 'year' column. Please check column names.")

# Step 3: Resample to yearly frequency (since we only have year info)
# If you later have monthly data, replace 'YS' with 'MS'
data_yearly = data['selling_price'].resample('YS').sum()

print("\nYearly Resampled Data Head:")
print(data_yearly.head())

# Step 4: Perform seasonal decomposition (period=5 is common for yearly car sales, adjust if needed)
decomposition = seasonal_decompose(data_yearly, model='additive', period=5)

# Step 5: Plot the decomposition
plt.figure(figsize=(10, 12))

# Original Data
plt.subplot(411)
plt.plot(data_yearly, label='Yearly Car Sales')
plt.legend(loc='upper left')
plt.title('Yearly Car Sales')

# Trend Plot
plt.subplot(412)
plt.plot(decomposition.trend, label='Trend', color='orange')
plt.legend(loc='upper left')
plt.title('Trend')

# Seasonal Plot
plt.subplot(413)
plt.plot(decomposition.seasonal, label='Seasonal', color='green')
plt.legend(loc='upper left')
plt.title('Seasonality')

# Residual Plot
plt.subplot(414)
plt.plot(decomposition.resid, label='Residual', color='red')
plt.legend(loc='upper left')
plt.title('Residuals')

plt.tight_layout()
plt.show()

```

## OUTPUT:
### FIRST FIVE ROWS:

<img width="831" height="630" alt="image" src="https://github.com/user-attachments/assets/712b0581-7be5-44b1-93cb-404095f3a53f" />

### PLOTTING THE DATA:

<img width="1011" height="280" alt="image" src="https://github.com/user-attachments/assets/9afbfd70-15bd-43c7-8e57-e8edb553de01" />

### SEASONAL PLOT REPRESENTATION :

<img width="1223" height="370" alt="image" src="https://github.com/user-attachments/assets/8216e1b2-eb60-43d5-9ce0-cfacae1a3816" />

### TREND PLOT REPRESENTATION :

<img width="1207" height="362" alt="image" src="https://github.com/user-attachments/assets/53cb914a-b054-40cb-a216-1201d774cb10" />

### OVERAL REPRESENTATION:

<img width="1262" height="373" alt="image" src="https://github.com/user-attachments/assets/bd160751-3c20-48dc-a72e-fd7fc1de22ae" />

## RESULT:

Thus we have created the python code for the time series analysis and decomposition for car sales data.

### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
