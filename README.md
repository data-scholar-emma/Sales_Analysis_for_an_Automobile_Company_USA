# Sales_Analysis_for_an_Automobile_Company_USA
A Data Science Project that Analysed  the sales performance of an Automobile company Based in the United States. The company’s sales transaction data generated over the past years was used for this  analysis.

## PROBLEM STATEMENT:  
What are the Top Most-Profitable 5 States for the Bike Product Category in the United States ?

## DATA PRE-PROCESSING 
#### DATA LOADING 
```Python
##  importing all the necessary python packages


# solution 

import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt

print("The packages have been successfully imported")

```


```Python
# reading the sales data into a pandas dataframe

bikes_df = pd.read_csv("C:/Users/HP/Downloads/dowlnoad 2/bikes.csv")
bikes_df.head()    

```

####  Data Modification
```Python
# (1). Adding the following 3 columns to your pansdas Dataframe:  bikes_df







# TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)


bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 





# SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)


bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 



# Profit : To be obtained by (SalesRevenue - TotalCostPrice)



bikes_df["Profit"] = bikes_df["SalesRevenue"] - bikes_df["TotalCostPrice"]


bikes_df.head()
```

## DATA ANALYSIS 
#### DATA FILTERING 

```Python
# Filtering out only the data relevant to solving the problem statement

is_usa = bikes_df["CustomerCountry"] == "United States"

is_bike = bikes_df["ProductCategory"] == "Bikes"

bike_in_the_US = bikes_df[ (is_usa) & (is_bike) ]

bike_in_the_US.head()

```

#### DATA AGGREGATION

```Python
# aggregating the total profit by states in the United States for bikes sales  

total_profits_by_states = bike_in_the_US.pivot_table(values = "Profit", index = "CustomerState", aggfunc = np.sum )

total_profits_by_states
```

#### DATA SORTING 
```Python
# Sorting the aggregated data 
# in order to rank the states according to top most-profitable states

total_profits_by_states.sort_values("Profit", ascending = False)

```

#### RESULT 
```Pthon
# The Top Most-Profitable 5 States for the Bike Product Category 

# in the United States ?

top_5_most_profitable_states_USA = total_profits_by_states.sort_values("Profit", ascending = False).head()

top_5_most_profitable_states_USA
```


## DATA VISUALIZATION 

```Python
# visualizing the result 

top_5_most_profitable_states_USA.plot(kind = "bar")


# adding a title and label to the plot 

plt.title("The Top 5 Most Profitable States for Bike Product in the US ")

plt.ylabel("Total Profit in Million Dollars")

plt.xlabel("States")

# showing the plot

plt.show()


```

