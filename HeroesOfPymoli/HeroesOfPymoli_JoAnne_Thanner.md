Jo Anne Thanner
### Heroes Of Pymoli Data Analysis
* Of the 1163 active players, the vast majority are male (84%). There also exists, a smaller, but notable proportion of female players (14%).

* Our peak age demographic falls between 20-24 (44.8%) with secondary groups falling between 15-19 (18.60%) and 25-29 (13.4%).  
-----

As a first task, the company would like you to generate a report that breaks down the game's purchasing data into meaningful insights.

* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.

There are 576 unique players total.

There are 780 unique items with the average price being $3.05 for each item.

There were a total of 780 purchases with a total revenue of roughly a little over $2300.

There are 484 male and 81 female unique players. 

The above gender count is a ratio of 84% men and 14% women with 2% undisclosed. 

Females spent more per item than men did, but men made more purchases.

The Other category spent the most per purchase.

The age group with the largest amount of players is 20-24, and the lowest number of players is over 40.

Players over the age of 40 purchased the most items.

The top 5 spenders bought less than $5 per item with less than $20 purchase value.

The most popular item is Despair, Favor of Due Dilligence.



```python
# Dependencies
import pandas as pd
import numpy as np

# Raw data file
file_to_load = "Resources/purchase_data.csv"

# Read purchasing file and store into pandas data frame
purchase_data = pd.read_csv(file_to_load)
purchase_data.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>



## Player Count

* Display the total number of players



```python
players = purchase_data.groupby("SN")["SN"].nunique()
players= pd.DataFrame({"Total Players": players})
players
players.count()

# There are 576 unique players total
```




    Total Players    576
    dtype: int64



# Purchasing Analysis (Total)

* Run basic calculations to obtain number of unique items, average price, etc.


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame



```python
unique_items = purchase_data['Item Name'].count()
avg_price = purchase_data['Price'].mean()
purchases = purchase_data['Price'].count()
revenue = purchase_data['Price'].sum()

purchase_analysis = {
    'Unique Items': [purchase_data['Item Name'].count()],
    'Average Price': [purchase_data['Price'].mean()],
    'Total Purchases': [purchase_data['Price'].count()],
    'Total Revenue': [purchase_data['Price'].sum()]
}

purchase_analysis = pd.DataFrame(purchase_analysis)
purchase_analysis

# There are 780 unique items with the average price being $3.05 for each item.
# There were a total of 780 purchases with a total revenue of roughly a little over $2300.
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unique Items</th>
      <th>Average Price</th>
      <th>Total Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>780</td>
      <td>3.050987</td>
      <td>780</td>
      <td>2379.77</td>
    </tr>
  </tbody>
</table>
</div>



## Gender Demographics

* Percentage and Count of Male Players


* Percentage and Count of Female Players


* Percentage and Count of Other / Non-Disclosed





```python
# Gender Count
gender_count= purchase_data.groupby("Gender")["SN"].nunique()
gender_count.head()

# There are 484 male and 81 female unique players. 
```




    Gender
    Female                    81
    Male                     484
    Other / Non-Disclosed     11
    Name: SN, dtype: int64




```python
# Gender Percentage
gender_percentage = gender_count/573
gender_percentage.round(2)

# The above gender count is a ratio of 84% men and 14% women with 2% undisclosed. 
```




    Gender
    Female                   0.14
    Male                     0.84
    Other / Non-Disclosed    0.02
    Name: SN, dtype: float64




```python
#Gender Demographics
gender_demographics = pd.DataFrame({"Gender Count": gender_count,"Gender Percentage":gender_percentage})
gender_demographics
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender Count</th>
      <th>Gender Percentage</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>81</td>
      <td>0.141361</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>484</td>
      <td>0.844677</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>0.019197</td>
    </tr>
  </tbody>
</table>
</div>




## Purchasing Analysis (Gender)

* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. by gender




* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
# PURCHASING ANALYSIS (GENDER)

# Calculate purchase count by gender
all_gender_df = purchase_data.groupby('Gender')

player_count = all_gender_df['SN'].count()
player_count_df = pd.DataFrame(player_count)

# Calculate average purchase price by gender
average_price = all_gender_df['Price'].mean()
average_price_df = pd.DataFrame(average_price)

# Calculate total purchase price by gender
total_gender_purchase = all_gender_df['Price'].sum()

# Calculate average price per person (total per category / total count per category)
avg_price_person =(all_gender_df["Price"].sum()/all_gender_df["Age"].count())
average_price_person = total_gender_purchase / player_count

# Add 'Average Purchase Price' to table
player_count_df['Average Purchase Price'] = average_price
gender_purchase_df = pd.DataFrame(player_count_df)
gender_purchase_df

# Rename 'SN' column to 'Purchase Count'
new_gender_purchase_df = gender_purchase_df.rename(columns={
    'SN': 'Purchase Count',
})

# Add 'Total Purchase Price' to table
new_gender_purchase_df['Total Purchase Price'] = total_gender_purchase
new_gender_purchase2_df = pd.DataFrame(new_gender_purchase_df)

# Add 'Average Price person' to table
new_gender_purchase2_df['Average Price Per Person'] = average_price_person
total_gender_purchase_df = pd.DataFrame(new_gender_purchase2_df)
total_gender_purchase_df

# Females spent more per item than men did, but men made more purchases.
# The Other category spent the most per purchase.
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Price</th>
      <th>Average Price Per Person</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>113</td>
      <td>3.203009</td>
      <td>361.94</td>
      <td>3.203009</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>652</td>
      <td>3.017853</td>
      <td>1967.64</td>
      <td>3.017853</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>15</td>
      <td>3.346000</td>
      <td>50.19</td>
      <td>3.346000</td>
    </tr>
  </tbody>
</table>
</div>



## Age Demographics

* Establish bins for ages


* Categorize the existing players using the age bins. Hint: use pd.cut()


* Calculate the numbers and percentages by age group


* Create a summary data frame to hold the results


* Optional: round the percentage column to two decimal points


* Display Age Demographics Table



```python
# Establish bins for ages
age_bins = [0, 9.90, 14.90, 19.90, 24.90, 29.90, 34.90, 39.90, 99999]
group_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

# Age groups 
purchase_data['Total Count'] = pd.cut(purchase_data['Age'],
                                     age_bins, labels=group_names)

age_groups = purchase_data.groupby('Total Count')
age_groups_df = age_groups.count()

# Total'Age' column
age_df = age_groups_df[['Age']]
age_df

# The age group with the largest amount of players is 20-24, and the lowest number of
# players is over 40.
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
    </tr>
    <tr>
      <th>Total Count</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>23</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>28</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age


* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
# Bins for different ages
age_bins2 = [0, 10, 15, 20, 25, 30, 35, 40, 100]
group_names2 = ['<10', '10-14', '15-19', '20-24', '25-29', '30-34', '35-39', '40+']

# Age groups
purchase_data['Total Count'] = pd.cut(purchase_data['Item ID'],
                                     age_bins2, labels=group_names2)
age_groups2 = purchase_data.groupby('Total Count')
age_groups2_df = age_groups2.count()
age_purchase = age_groups2_df['Item ID']
age_purchase

age2_df = age_groups2_df[['Item ID']]
age2_df

# Players over the age of 40 purchased the most items.
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Total Count</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>44</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>22</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>23</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>23</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>12</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>22</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>23</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>252</td>
    </tr>
  </tbody>
</table>
</div>



## Top Spenders

* Run basic calculations to obtain the results in the table below


* Create a summary data frame to hold the results


* Sort the total purchase value column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Total Purchase Count
count_per_SN = purchase_data.groupby('SN')['Price'].count()
count_per_SN_df = pd.DataFrame(count_per_SN)

# Total Purchase Price
unique_SN_df = purchase_data.groupby('SN')['Price'].sum()

# Average Purchase Price
avg_price_per_SN = purchase_data.groupby('SN')['Price'].mean()

# Add 'Average Purchase Price'
count_per_SN_df['Average Purchase Price'] = avg_price_per_SN

# Add 'Total Purchase Value'
count_per_SN_df['Total Purchase Value'] = unique_SN_df
count_per_SN_df

# Rename 'Price' to 'Purchase Count'
updated_count_per_SN_df = count_per_SN_df.rename(columns={
    'Price': 'Purchase Count',
})

# Sort 'Price' from highest to lowest
sorted_SN_df = updated_count_per_SN_df.sort_values(by=['Total Purchase Value'], ascending=False)
sorted_SN_df

# Show top 5 spenders only
sorted_SN_df.head(5)

# The top 5 spenders bought less than $5 per item with less than $20 purchase value.
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Lisosia93</th>
      <td>5</td>
      <td>3.792000</td>
      <td>18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>3.862500</td>
      <td>15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>4.610000</td>
      <td>13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>3.405000</td>
      <td>13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>4.366667</td>
      <td>13.10</td>
    </tr>
  </tbody>
</table>
</div>



## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns


* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value


* Create a summary data frame to hold the results


* Sort the purchase count column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Total Purchase Count
count_per_item = purchase_data.groupby('Item ID')['Price'].count()
count_per_item_df = pd.DataFrame(count_per_item)

# Total Purchase Price
unique_item_df = purchase_data.groupby('Item ID')['Price'].sum()

# Add Item Name
item_name_df = purchase_data.iloc[:, 5]
count_per_item_df['Item Name'] = item_name_df

# Add Item Price
item_price_df = purchase_data.iloc[:, 6]
count_per_item_df['Item Price'] = item_price_df

# Add Total Purchase Value
count_per_item_df['Total Purchase Value'] = unique_item_df
count_per_item_df

# Rename 'Price' to 'Purchase Count'
updated_count_per_item_df = count_per_item_df.rename(columns={
    'Price': 'Purchase Count',
})

# Rearrange columns
organized_items_df = updated_count_per_item_df[['Item Name', 'Purchase Count', 'Item Price', 'Total Purchase Value']]

# Sort 'Purchase Count' from highest to lowest
sorted_items_df = organized_items_df.sort_values(by=['Purchase Count'], ascending=False)

# Show top 5 popular items only
sorted_items_df.head()

# The most popular item is Despair, Favor of Due Dilligence
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <td>Despair, Favor of Due Diligence</td>
      <td>12</td>
      <td>4.60</td>
      <td>50.76</td>
    </tr>
    <tr>
      <th>145</th>
      <td>Hopeless Ebon Dualblade</td>
      <td>9</td>
      <td>1.33</td>
      <td>41.22</td>
    </tr>
    <tr>
      <th>108</th>
      <td>Malificent Bag</td>
      <td>9</td>
      <td>1.75</td>
      <td>31.77</td>
    </tr>
    <tr>
      <th>82</th>
      <td>Azurewrath</td>
      <td>9</td>
      <td>4.40</td>
      <td>44.10</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Blazefury, Protector of Delusions</td>
      <td>8</td>
      <td>4.64</td>
      <td>8.16</td>
    </tr>
  </tbody>
</table>
</div>



## Most Profitable Items

* Sort the above table by total purchase value in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the data frame




```python
# Total Purchase Count
count_per_item2 = purchase_data.groupby('Item ID')['Price'].count()
count_per_item2_df = pd.DataFrame(count_per_item2)

# Total Purchase Price
unique_item2_df = purchase_data.groupby('Item ID')['Price'].sum()

# Add Item Name
item_name2_df = purchase_data.iloc[:, 5]
count_per_item2_df['Item Name'] = item_name2_df

# Add Item Price
item_price2_df = purchase_data.iloc[:, 6]
count_per_item2_df['Item Price'] = item_price2_df

# Add Total Purchase Value
count_per_item2_df['Total Purchase Value'] = unique_item2_df
count_per_item2_df

# Rename 'Price' to 'Purchase Count'
updated_count_per_item2_df = count_per_item2_df.rename(columns={
    'Price': 'Purchase Count',
})

# Rearrange columns
organized_items2_df = updated_count_per_item2_df[['Item Name', 'Purchase Count', 'Item Price', 'Total Purchase Value']]

# Sort 'Purchase Count' from highest to lowest
sorted_items2_df = organized_items2_df.sort_values(by=['Total Purchase Value'], ascending=False)

# Show top 5 popular items only
sorted_items2_df.head()

# The most profitable item was also Despair, Favor of Due Dilligence
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>178</th>
      <td>Despair, Favor of Due Diligence</td>
      <td>12</td>
      <td>4.60</td>
      <td>50.76</td>
    </tr>
    <tr>
      <th>82</th>
      <td>Azurewrath</td>
      <td>9</td>
      <td>4.40</td>
      <td>44.10</td>
    </tr>
    <tr>
      <th>145</th>
      <td>Hopeless Ebon Dualblade</td>
      <td>9</td>
      <td>1.33</td>
      <td>41.22</td>
    </tr>
    <tr>
      <th>92</th>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>8</td>
      <td>3.94</td>
      <td>39.04</td>
    </tr>
    <tr>
      <th>103</th>
      <td>Thorn, Satchel of Dark Souls</td>
      <td>8</td>
      <td>1.33</td>
      <td>34.80</td>
    </tr>
  </tbody>
</table>
</div>


