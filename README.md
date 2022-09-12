# Merchant-Transaction-Analysis
Exploratory and churn rate analysis for merchants based on Transactional data.

### 1.	Explore.   
•	The dataset contains 3 columns: time, merchant_id and amount_usd_in_cents.  
•	The data starts from Jan, 2033 and ends on Dec, 2034.  
•	There are no null values in the given dataset.  
•	Trend of total transaction amount across merchants on a daily chart.  

<img width="1020" alt="image" src="https://user-images.githubusercontent.com/21052254/189581668-9ddb3246-1535-4845-9888-f4aa9a4f7c5c.png">

•	Trend of number of transactions across merchants on a daily chart.   

<img width="1020" alt="image" src="https://user-images.githubusercontent.com/21052254/189581701-b4afcb0e-8da3-4f13-8c94-304850636dfa.png">


There is a linear increase in the number of transactions that are being executed.

#### Probable reasons for the increasing trend:     
a)	New merchants being added.  
b)	Existing merchants doing bigger transactions.  
c)	Lowering churn rate with increase in new merchants.  

The spikes in the chart may be attributed to discount weekends, holiday season, etc.  

### Problem Statement     
#### 1.	Understand payment activity of the merchants. Tag merchants with attributes based on the data available.      
Merchants Attributes Engineered:   
a)	Store Operational timings     
b)	Median of amount per transaction for a merchant.   
c)	Number of transactions for a merchant    
d)	Quarter wise number of transactions.   
e)	Quarter wise amount of transaction.  
f)	Weekday Sales amount.    
g)	Weekend Sales amount. 


> Store Operational Timings:  
*	The stores are tagged as all_day, day, night which represents when the transactions have taken place for the merchant.   
*	Day timings considered are from 6AM to 6PM.   
*	All day stores might be online merchants, gas stations or medical stores. 
*	Morning only store might be vegetable vendors, breakfast places, etc.  
*	Night store might be dinner restaurants, bars etc.  

>	Median of amount per transaction for a merchant.   
*	This metric gives an idea of how huge per transactions are normally. Electronics shops would normally have bigger amount values than grocery stores.    

>	Number of transactions for a merchant. 
*	This metric gives an idea of how many transactions were done for the merchant in the 2 years. Electronics shops would normally have lesser number of transactions than grocery stores.  


> Quarter wise number of transactions and amount of transaction. 
*	The seasonality of the business can be estimated from these columns. Some merchants would have very high business sales during the holiday season (December), whereas other might have high sales during summer.  
*	There are many businesses that have almost equal sales throughout each quarter every year.  

> Weekday and Weekend Sales. 
*	These columns show if the merchant is open during the weekend, weekday or throughout the week.  
*	Weekend sales for some businesses might be more than weekday sales or vice versa.  

The Merchant Attribute Value:  
<img width="1020" alt="image" src="https://user-images.githubusercontent.com/21052254/189581570-9a5d604a-6da2-49d5-a2de-ebe43f2bcff2.png">


## 2.	Identifying and predicting Churn. 

a)	Churn Definition used in this analysis. 
-	The merchants that were part of the transactions in a period are not in the next period. Then the percentage of those merchants irrespective of newly added merchants form the churn rate.  
-	In this analysis Quarterly and Monthly time period being used.  

b)	Identifying merchants that have churned (same method for monthly and quarterly). 
-	Groupby the time frame (month, quarter along with year) and fetch a set of merchants part of that period.  
-	Create a merchant lag variable of 1.     
-	Use the lag variable and minus the current merchant set values. This would give us the merchants that were part of the previous period but did not continue (Churn).   
-	Churn Rate = Difference in Merchants from above step / Total Merchants in lag column (previous period) * 100. 
-	The column difference column of the merchants has the set of all merchants that have churned.  

 <img width="1020" alt="image" src="https://user-images.githubusercontent.com/21052254/189581848-fd784fe9-1cc8-4ac4-a89c-05fe21ffa3f7.png">

<img width="1020" alt="image" src="https://user-images.githubusercontent.com/21052254/189581854-1c71864e-93ae-4267-a7c1-4ab25e72dfee.png">

The graphs above show the count of new merchants and the churn rate over the quarters and months. The churn rate is exponential decreasing and would most probably be stabilizing in the coming period. Predicting the churn rate and the new merchant acquisition becomes easy once we see the trajectory in the graph.  


c)	Predicting active merchants that would churn. 
-	Build a model with a small part of data with balanced class size to predict churn.  
-	On testing the model used (Random Forest) gave a F1 Score of 91%.  
-	We can go ahead and use the same model on the active merchants and see which might churn.  

### Possible Future Work.   
•	Use clustering algorithms like the KMeans on the attributes to categories the merchants in buckets. Find the best k value using the knee graph.     
•	Use another modeling technique to model churn merchants that might perform better.     
•	Explore the combined dataset and not based on merchants, to get other insights.  
•	Calculate churn based on revenue from the merchants.  
•	Going a step forward and providing dynamic commission charge as a company to reduce churn and increase profitability.  

