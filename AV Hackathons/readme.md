## Loan Delinquency Prediction

**Problem Statement**

	Given the details of the bank customers we have to predict whether the customer will pay off the loan or not. The given data includes source of the loan, the date of loan sanction, number of borrowers, loan to value ratio, type of loan etc along with the loan delinquency status for 12 months from date of loan sanctioned. We have to predict if the customer will pay off the loan or not for the 13th month.

**Exploratory Data Analysis**	

	By plotting a count plot of the target variable, it can be seen that the data is highly imbalanced, and it will be hard for the model to predict the target '1' which is what we are looking for. In real scenario we should collect more data to balance the target variable distribution, so the model has enough data to train on both the classification and won't be biased. In these cases, resampling techniques can be used to train the model well on different classification and increase the accuracy of the model.
	
	By quickly plotting a scatterplot of the ‘unpaid_principal_bal’ we can easily see how it is distributed and spot any outliers. Other ways to spot outliers would be to calculate Z-score or Standard Deviation among other methods and find if a particular data point is deviating too much from the distribution.

	From the plot we can see the data is distributed evenly until around 620000 but then start to deviate too much from data range. Let's consider anything above 790000 as outliers. Similarly, by checking the other end of the range we don't see any extreme deviation from other data points so this okay.

**Feature Engineering**

	The categorical features such as 'source', 'financial_institution', 'loan_purpose' are converted using One Hot encoding.
  
	Initially I have converted the date features 'origination_date', 'first_payment_date' to datetime format and split them into separate months and days columns. Since I saw no significant improvement later in the model with and without the date features, I removed the date features in my final submission.
  
	The various columns in the data have spread across different range and in different magnitude and this may affect the performance of the final model as the feature with higher magnitude will have more impact on the model performance. Hence, I have used Standard scaler to standardise the entire data except the target variable.
  
**Training the model**

	I have used train_test_split to split the train set into train and test data to train the model and find the best parameters that gives the better F1 score since that is what we are using to score the performance of the model.
  
	Used GridSearchCV  to determine the best parameters for the Logistic Regression, Random Forest, Decision Tree, KNN.
  
	Used the parameters obtained from GridSearchCV to create different models and calculated the F1 score.
  
	Using K-fold Cross Validation with n=3 to validate how good the model performs and was evaluated using F1 score. The CV score was consistently better than the actual score obtained for different models meaning the model was performing good.
  
 	Used Precision-Recall curve to determine how the model performs as unlike AUC-ROC curve reviewing both precision and recall is useful in cases where there is an imbalance in the observations between the two classes. Specifically, there are many examples of no event (class 0) and only a few examples of an event (class 1).The reason for this is that typically the large number of class 0 examples means we are less interested in the skill of the model at predicting class 0 correctly, e.g. high true negatives.

**Testing**

	Logistic Regression gave the best F1 score out of all other model hence used that model to predict the test data and the final predictions submitted was that of Logistic Regression.
  
**Further Scope**

	The data could have been trained with other algorithms such as XGBoost which is known to give better results than other algorithms to further increase the model performance. It might have been possible to get a better F1 score from XGBoost but was unable to test due to time restrictions.

