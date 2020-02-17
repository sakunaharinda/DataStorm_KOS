# Data Storm 1.0 

> Team Name               : KOS <br />
> Kaggle Username         : ds1092 <br />
> Kaggle Display Name     : ds1092 <br />
# **1. Introduction**
Banks often over-issue credit cards to applicants without properly assessing their ability to repay. This leads most cardholders to overuse their credit cards for consumption irrespective of their repayment ability. This scenario will lead to heavily accumulated credit card debts. This kind of crisis will ruin the consumer finance confidence and it is a big challenge for both banks and cardholders. The task is to crack the above scenario and predict whether the next month payment of a particular customer is a default payment or not depending on Credit Card Limit, Gender, Age, Education Status, Marital Status, Repayment Status, Due amount and Paid amount.
# **2. Approach Used**
Our approach to the best model can be divided into 3 main steps.
1. **Organizing Data** – Analysis of the problem statement and the dataset revealed that it needed the following pre-processing steps. Since there were no null entries, the following steps were adequate in pre-processing.
* Encoding Non-numerical data: We encoded the Categorical (Marital Status, Gender) and Ordinal (Balance Limit, Education, Age) for training and visualization convenience.
* Normalizing Data: We normalized the large values in the dataset in order to make all the features for a same scale and to suppress unnecessary interference in mathematical models such as regressions. We used Z-score and min-max normalization.
