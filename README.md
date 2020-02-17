> Team Name           : KOS <br />
> Kaggle Username     : ds1092 <br />
> Kaggle Display Name : ds1092 <br />

# **1. Introduction**
Banks often over-issue credit cards to applicants without properly assessing their ability to repay. This leads most cardholders to overuse their credit cards for consumption irrespective of their repayment ability. This scenario will lead to heavily accumulated credit card debts. This kind of crisis will ruin the consumer finance confidence and it is a big challenge for both banks and cardholders. The task is to crack the above scenario and predict whether the next month payment of a particular customer is a default payment or not depending on Credit Card Limit, Gender, Age, Education Status, Marital Status, Repayment Status, Due amount and Paid amount.
# **2. Approach Used**
Our approach to the best model can be divided into 3 main steps.
1. **Organizing Data** – Analysis of the problem statement and the dataset revealed that it needed the following pre-processing steps. Since there were no null entries, the following steps were adequate in pre-processing.
* Encoding Non-numerical data: We encoded the Categorical (Marital Status, Gender) and Ordinal (Balance Limit, Education, Age) for training and visualization convenience.
* Normalizing Data: We normalized the large values in the dataset in order to make all the features for a same scale and to suppress unnecessary interference in mathematical models such as regressions. We used Z-score and min-max normalization.
2. **Visualizing the data using plots and tables** – We used plots and tables to identify important statistics about the data and their relationships. Among them are the correlation matrix, distributions of the data, descriptive tables about the feature columns etc.

![Picture2](https://user-images.githubusercontent.com/33924326/74664801-706f3e80-51c4-11ea-8410-ce998688a4e3.png)

3. **Exploring Data relationships and Feature engineering** – Using the correlations obtained between the features and the next month credit card default status, we found PAY_X values are significant. Likewise, we added and removed some features in order to improve the mean F1 score (or the validation accuracy). We used engineered features based on the original features and the techniques we used will be discussed in the next section.

# **3. Feature Engineering**
This was a critical step in addressing the problem at hand. Using the basic machine learning models and trying out different combination of original features, we realized that certain features were needed to be created, certain original features were needed to be removed or changed. The following are some of the engineered features we used with different models we trained.
* Difference between total paid and total – This represents how much a client owes to the bank at the end of 6 months period and indicates the client’s attitude towards settling the credit he or she owes. This improved the accuracy significantly.
* Removal of several original features – Based on results obtained with different combinations of original features and their correlation to next month default status we removed several features such as Marital Status, Education Level and DUE_AMT_X
* Closeness column to check how far the bill is from the allowed limit – We defined the closeness by subtracting the DUE_AMT_X from Balance_Limit_V1 and dividing it by Balance_Limit_V1.
* We defined another closeness column where the closeness was defined by subtracting the difference between the mean of paid amount and due amount from Balace_Limit_V1.
* Status of a client - We put this feature to check whether a certain ID is still a client or not. If a certain entry has 0s for PAY_X, DUE_AMT_X and PAID_AMT_X that client is no longer a client in the company. This has a relatively high correlation with NEXT_MONTH_DEFAULT.
* We considered the Balance_Limit_V1 as a categorical feature and a continuous numerical feature in models.
* We also categorized the PAY_X columns to two categories based on prior and delayed payments based on the PAY_X value.

# **4. Final Model**
We initially approached the problem using all the pre-processed original features. We used the basic machine learning models such as Decision Tree Classifier, K-Neighbour Classifier and Naïve Bayes Classifier. We split the dataset to 5 folds and trained these models and obtained a maximum accuracy around 80.8%. We used it as out base score to be improved by other means.
We then engineered some features as mentioned in the previous section and based on the Pearson Correlation we selected the most important features for training. We moved to Gradient Boosting Decision Tree algorithms where we tried LightGBM, CATBoost and XGBoost algorithms. We used 80% of the data to train the models and the remaining to validate them. With LightGBM we achieved a maximum validation score of 81.772% and 83.152% with CATBoost(sub3.csv). We also tried Dense Neural Network with 13 layers and dropout layers. We used Adam optimizer with a learning rate of 0.0001 to be decayed during the training. The model achieved an accuracy of 81.81% on validation(sub9.csv). As the final model, we selected the model based on XGBoost Algorithm, which is an ensemble learning method which fit the data to multiple tree structures sequentially and boost significant features and dropping less significant features circularly. We used Grid Search algorithm to optimize the hyperparameters including learning rate, maximum depth of a tree and L1 regularization term on weights. We achieved an accuracy on the validation set of 82.896% and 82.466% on the test set(subtest1.csv).

|Model      |Accuracy   |Precision  |Recall     |F1 Score  |ROC       |
|-----------|-----------|-----------|-----------|----------|----------|
|XG Boost   |0.828958   |0.711957   |0.372512   |0.48911   |0.665028  |

# **5. Business Insights**
The main business problem we are trying to capture through this is to identify the clients who are likely to default the credit card payments which would ultimately result in loss of key clients as well as profit for the credit offering institutes specifically the banks.

Even though there is no strong correlation between the _Gender, Education Level_ and the _Default of Credit card payment_, we saw that a higher proportion of High Schoolers and Graduates default in credit payment. Lack of analysis on the category Others under the Educational Level would cause a great loss for the banks as a significant portion of that category can be seen defaulting the credit card payment. The collected data do not have the status of the employment which is one crucial factor in deciding whether the client is capable of paying the credit amounts used each month.
We interpreted the PAY_X values as how the clients have made the due payments for the credit they have used. We saw that most of the defaulted clients tend to have prolonged payment periods where they take more than 1 months to settle their credit limit.

Based on the above specifications we analyzed with the provided dataset the following are some of the actions that we would like to suggest.

We suggest that the banks to sub categorize and analyze the _Other_ category under the _Educational Level_ so that better analysis can be made. We also suggest following a system that reflects the client’s ability to pay when providing the credit limits. It is our view that providing a monthly limit of 100K for especially High Schoolers bears a greater risk of defaulting the credit card payments. Banks should analyze the client's employment status and update them on quarterly or yearly basis. We also suggest to closely monitor the important customers through follow-ups when the clients fall due more than 1 month and gain a mutual solution. This can be done for less important customers like High Schoolers as well but the befits of doing so should outweigh the cost of doing it.

This would be our business insight on the problem of credit card payment defaults based on the given data.
