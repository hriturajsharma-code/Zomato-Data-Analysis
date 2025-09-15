![Zomato logo](https://github.com/hriturajsharma-code/Zomato-Data-Analysis/blob/d59e82953b645b287f4ff667af07831bc10149fc/Zomato%20logo.png)


# Zomato-Data-Analysis
This project utilizes Python for a comprehensive analysis of the Zomato dataset, aiming to extract valuable insights and address key business questions.

## Project Objectives
The primary goal is to analyze the Zomato dataset to understand customer behavior and restaurant performance, thereby providing actionable insights for service and marketing improvements.

## Business Problems
The analysis addresses the following business questions:

1) What type of restaurant do the majority of customers order from?

2) How many votes has each type of restaurant received from customers?

3) What are the ratings that the majority of restaurants have received?

4) Zomato has observed that most couples order most of their food online. What is their average spending on each order?

5) Which mode (online or offline) has received the maximum rating?

6) Which type of restaurant received more offline orders, so that Zomato can provide those customers with some good offers?
## Solutions
### Step 1 : import necessary python libraries
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```
### Step 2: Create the data frame.

```python
dataframe = pd.read_csv("Zomato data .csv")
print(dataframe.head())
dataframe = pd.read_csv("Zomato data .csv")
dataframe
```
### Step 3: Let's convert the data type of the "rate" column to float and remove the denominator.
```python
def handleRate(value):
    value = str(value).split('/')
    value = value[0]
    return float(value)
dataframe['rate'] = dataframe['rate'].apply(handleRate)
print(dataframe.head())
```
### Step 4 : Identify if the data set have any null values
```python
dataframe.info()
```
## Charts
### 1) What type of restaurant do the majority of customers order from?
```python
sns.countplot(x=dataframe['listed_in(type)'])
plt.xlabel("Type of restaurant")
```
![countplot](https://github.com/hriturajsharma-code/Zomato-Data-Analysis/blob/a4bc00fa52fb0896d45caed17859888340442690/Chart1.png)

## Chart Insights :
The majority of the resturants fall into the dining category.

### 2) How many votes has each type of restaurant received from customers?
```python
grouped_data = dataframe.groupby('listed_in(type)')['votes'].sum()
result = pd.DataFrame({'votes': grouped_data})
plt.plot(result, c="green", marker="o")
plt.xlabel("Type of restaurant", c="red", size=20)
plt.ylabel("Votes", c="red", size=20)
```
![votes](https://github.com/hriturajsharma-code/Zomato-Data-Analysis/blob/a4bc00fa52fb0896d45caed17859888340442690/chart2.png)

## Chart Insights :
The majority of votes have received from the customers in dining category.

### 3) What are the ratings that the majority of restaurants have received?
```python
plt.hist(dataframe['rate'], bins=5)
plt.title("Ratings Distribution")
plt.show()
```
![histplot](https://github.com/hriturajsharma-code/Zomato-Data-Analysis/blob/a4bc00fa52fb0896d45caed17859888340442690/chart3.png)

## Chart Insights :
The majority of resturants received ratings from 3.5 to 4

### 4) Zomato has observed that most couples order most of their food online. What is their average spending on each order?
```python
Couple_data=dataframe[‘approx_cost(for two people)’]
Sns.countplot(x=couple_data)
```
![couple](https://github.com/hriturajsharma-code/Zomato-Data-Analysis/blob/a4bc00fa52fb0896d45caed17859888340442690/chart4.png)
 
## Chart Insights :
The majority of couples prefer resturants with an approximate cost of 300 rupees.Whether online orders receive higher ratings than offline orders.

### 5) Which mode (online or offline) has received the maximum rating?
```python
plt.figure(figsize=(6,6))
sns.boxplot(x='online_order', y='rate', data=dataframe)
```
![boxplot](https://github.com/hriturajsharma-code/Zomato-Data-Analysis/blob/a4bc00fa52fb0896d45caed17859888340442690/chart5.png)
## Chart Insights :
Offline orders received lower ratings in comparison to online orders, which obtained excellent ratings

### 6) Which type of restaurant received more offline orders, so that Zomato can provide those customers with some good offers?
```python
pivot_table = dataframe.pivot_table(index='listed_in(type)', columns='online_order', aggfunc='size')
sns.heatmap(pivot_table, annot=True, cmap="YlGnBu", fmt='d')
plt.title("Heatmap")
plt.xlabel("Online Order")
plt.ylabel("Listed In (Type)")
plt.show()
```
![heatmap](https://github.com/hriturajsharma-code/Zomato-Data-Analysis/blob/a4bc00fa52fb0896d45caed17859888340442690/chart6.png)
## Chart Insights :
Dining resturants primarily accept offline orders,whereas cafe primarily receive online orders. THis suggests that clients prefer to place orders in person at restaurants, but prefer online ordering at cafes.

# Conclusion

The analysis reveals important patterns in customer behavior on Zomato. Dining restaurants lead in popularity, receiving the most orders, votes, and offline engagement, while online orders are generally rated higher. Couples show a preference for affordable dining options, and cafes are more popular for online orders. Overall, both online and offline modes play significant roles, but customer satisfaction trends lean more toward online ordering.

## Key Insights:
 
- Dining restaurants dominate in orders and votes.  
- Most ratings fall in the **3.5–4** range, reflecting good satisfaction.  
- Couples prefer restaurants with an average spend of **₹300**.  
- Online orders receive **higher ratings** than offline ones.  
- **Dining = more offline orders**, **Cafes = more online orders**.  

















