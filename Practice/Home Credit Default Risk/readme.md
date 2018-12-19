# Home Credit Default Risk

## Introduction
In this notebook, we will look at the [Kaggle Home Credit Default Risk](https://www.kaggle.com/c/home-credit-default-risk "Kaggle Home Credit Default Risk")  machine learning competition.

The objective is to use historical loan application data to predict whether or not an applicant will be able to repay a loan. This is a standard supervised classification task:

* Supervised: The labels are included in the training data and the goal is to train a model to learn to predict the labels from the features
* Classification: The label is a binary variable, 0 (will repay loan on time), 1 (will have difficulty repaying loan)

## Data
The data is provided by Home Credit, a service dedicated to provided lines of credit (loans) to the unbanked population. Predicting whether or not a client will repay a loan or have difficulty is a critical business need, and Home Credit hosted this competition on Kaggle to see what sort of models the machine learning community can develop to help them in this task.

There are 7 different sources of data:

* application_train/application_test: the main training and testing data with information about each loan application at Home Credit. Every loan has its own row and is identified by the feature SK_ID_CURR. The training application data comes with the TARGET indicating 0: the loan was repaid or 1: the loan was not repaid.
* bureau: data concerning client's previous credits from other financial institutions. Each previous credit has its own row in bureau, but one loan in the application data can have multiple previous credits.
* bureau_balance: monthly data about the previous credits in bureau. Each row is one month of a previous credit, and a single previous credit can have multiple rows, one for each month of the credit length.
* previous_application: previous applications for loans at Home Credit of clients who have loans in the application data. Each current loan in the application data can have multiple previous loans. Each previous application has one row and is identified by the feature SK_ID_PREV.
* POS_CASH_BALANCE: monthly data about previous point of sale or cash loans clients have had with Home Credit. Each row is one month of a previous point of sale or cash loan, and a single previous loan can have many rows.
* credit_card_balance: monthly data about previous credit cards clients have had with Home Credit. Each row is one month of a credit card balance, and a single credit card can have many rows.
* installments_payment: payment history for previous loans at Home Credit. There is one row for every made payment and one row for every missed payment.

To fully understand the data, refer to the [column descriptions](https://github.com/MAKAnalytics/Kaggle/blob/master/Practice/Home%20Credit%20Default%20Risk/data/HomeCredit_columns_description.csv) provided.

In this notebook, we will focus on the application train and test data files only. This is to simplifier the model building process and to establish a baseline. In actual competition, all data files and their relationship to each other would need to be considered. 

## Evaluation
Submissions are evaluated on area under the ROC curve between the predicted probability and the observed target.

## The ROC curve
The Reciever Operating Characteristic (ROC) curve graphs the true positive rate versus the false positive rate: 

![alt text][logo]

[logo]: https://github.com/MAKAnalytics/Kaggle/blob/master/Practice/Home%20Credit%20Default%20Risk/images/roc_curve.jpg "ROC curve"

Each curve of the graph represents a single model. Each shows the true positive and false positive rate for every probability threashold of a binary classifier.

In the above graph, we see four models corresponding to the blue, red, green, and orange curves. Graphs that are closest to the top-right are best. Therefore, the orange curve is best followed by green, red, and blue. The grey diagonal line is a model that is no better than random guessing.

## The AUC
The Area Under the Curve (AUC) is the area under the ROC curve. This metric is between 0 and 1 with a better model scoring higher. A model that simply guesses at random will have an ROC AUC of 0.5.

