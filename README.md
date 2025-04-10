# Practical Application 17 - Comparing Classifiers

### Overview

   In this practical application, your goal is to compare the performance of the classifiers we encountered in this section, namely K Nearest Neighbor, Logistic Regression, Decision Trees, and Support Vector Machines. We will utilize a dataset related to marketing bank products over the telephone.
   

### Business Obbjective

The business objective consist of leveraging the dataset supplied by a portuguese bank regarding past direct marketing campaign. Using this dataset of 17 campaigns and over 79,354 contacts, the goal is to create a model capable of predicting the success of marketing campaign. The success in this case is to predict the number of people who will probably purchase the product (a long-term deposit with good interest rates) which will then be targetted through furture marketing campaigns.

To do so, we will compare the classification methods of:
	
K-nearest neighbors (KNN)
Logistic Regression (LR)
Decision Trees (DT)
Support Verctor Machines (SVM)

### Model Evaluation

Before beginning our exploration of various models, it is important to define the criteria used to evaluate each model. 

In reference to 'Using Data Mining for Bank Direct Marketing: An Application of the CRISP-DM Methodology' by Moro, S. & Laureano, M.S. the AUC_ROC offers a great way to track the performance of our model in our business context. The AUC plots the False Positive Rate (FPR) versus the True Positive Rate (TPR). This measure will show the number of clients the model miss-identified as potential buyers of the product (false positives) while at the same time enabling the data scientist to maximize the real buyers of the product (true positives). In the business context, such approach makes sense as you are looking to limit the resources spent on non-buyers hence you are hoping to have a low FPR (false positive ratio) to maximize your campaigns profitability.

In addition, we will track the Accuracy, F1, Precision and Recall to better understand the overall performance of each model. To understand the cost behind each model, we will also collect the run time of each model to better track the tradeoff of accuracy vs time.

### Findings and Conclusions

The overall business objective for this ML exercise was to build classification model that would help our client, the Portuguese bank, better predict which of its targetted customers are likely to purchase investment products being promoted within the bank's many marketing campaigns. In order to accruately measure the mdoels' results in the context of the chosen business objective, the AUC_ROC curve was used as the primary metric because the AUC plots fales positive rate against the true positive rate^1. The AUC metric will show the number of customers which were classified as potential purchasers and which in turn did purchase the investment product (True Positives) versus the number of customers that were also classified as potential purchasers who did not end up purchasing the investment product (False Positives). This approach will enable us to focus on minimizing False Positives which in turn would waste less of the bank's resources and time in regards to the execution of its marketing campaigns.

Additionally, it is important to recognize that the dataset is not balanced with regards to the two classes (values within the "y" column). There are many more "No" or '0' than "Yes" or '1'. This imbalance requires the use of a metric which combines both "precision" and "recall" hince the inclusion of F1 as a metric to measure performance according to class.

Model comparison with regards to chosen metrics and performance:

Assuming all customers would not purchase the investment product specified in the campaign the baseline model showed a 87% accuracy for "No" and a ROC_AUC of .5. Models subsequently used should provide better accuracy than 13% and a ROC_AUC higher than .5.

##	Simple Logistic Regression
The confusion matrix showed for the simple logistic model showed the same results as the baseline model classifying all predictions as "no", hence this model can be discarded.

##	Logistic Regression with GridSearch
The logistic regression model with grid search on hyperparameters showed a slightly higher ROC_AUC score than simple Logistic Regression without grid search. The accuracy score was much lower than the simple Logistic Regression model however, its confusion matrix shows a clear pattern with regards to prediction and it showed the best F1 score out of all of the models tested. Furthermore, the logistic regression model with grid search also had the shortest fit time so training it does not require an abundance of resources.

##	KNN with GridSearch
The KNN with GridSearch of hyperparameters did not yield good results. First, the ROC_AUC score was below the threshold set by the baseline model. Second, it took some time to train the model which demonstrated its inefficiency.

##	SVM with GridSearch
SVM with GridSearch of hyperparameters was training on a subset of the orginal dataset which consisted of 5000 random samples. This was the most inefficient model as it took the longest to train. Also, its ROC_AUC score was below the threshold set by the baseline model.

##	Decision Tree with GridSearch
The decision tree with GridSearch had a slightly better ROC_AUC score than the logistic regression model with GridSearch however, its F1 score was really low. Furthermore, it took more time to train then the logistic regression model with GridSearch.

##	Conclusion
The best model to use to acheive the stated business objective would be the Logistic Regression model with Ridge Regression (l2). This model shows the highest F1 score and can be trained with few resources.

