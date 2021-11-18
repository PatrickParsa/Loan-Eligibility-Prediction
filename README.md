# Loan-Eligibility-Prediction
Loan eligibility prediction with logistic regression and KNN

## Introduction

The purpose of this project was to build a classification model that minimizes credit risk (the risk of loss resulting from the failure of a borrower to repay the principal and interest owed to the lender). We wanted our model to accomplish this by using customer data to accurately predict whether an application should be approved or not. 


Following the Data Science approach of OSEMN, as outlined and detailed below, we were able to determine a final model that accomplishes our objective while also identifying the key factors that play the biggest part in the decision. 

## Technologies used: 

* Pandas 
* Numpy
* Matplotlib
* Seaborn
* Sklearn


## The Data Science Process: OSEMN

### Obtain

The data used for this project was obtained from [Kaggle](https://www.kaggle.com/ninzaami/loan-predication)

The **data dictionary** is as follows: 

* **Loan_ID**: Unique Loan ID
* **Gender**: Gender of the applicant - Male/Female
* **Married**: Whether the applicant is married or not (Yes/No)
* **Dependents**: Number of dependents of the applicant
* **Education**: Applicant's education (Graduate/Not Graduate)
* **Self_Employed**: Whether the applicant is self-employed (Yes/No)
* **ApplicantIncome**: The income of the applicant ($)
* **CoapplicantIncome**: The co-applicant's income in case of a joint loan and 0 otherwise ($)
* **LoanAmount**: Loan amount (dollars in thousands)
* **Loan_Amount_Term**: Term of loan in months
* **Credit_History**: Whether the applicant's credit history meets required guidelines
* **Property_Area**: The area the property pertaining to the loan belongs to - * Urban/Semi-Urban/Rural
* **Loan_Status**: Loan approved (1 - Yes, 0 - No)

### Scrub

The dataset contained missing values for the loan amount for which we dealt with using the median, this is because we noticed that the distribution is highly skewed with a lot of outliers. We also did some feature engineering and alterations such as adding a column of the total income (applicant + co-applicant income), as well as converting the scale of loan term from months to years. Finally, we encoded the loan status column to make it eligible for modeling. 

### Explore

In this phase, we started off with separating the numerical columns from the categorical ones in order to quickly eyeball the summary statistics of the former as well as checking the percentages for each category for the latter. This gave us a quick idea of how the spread of the data, by showing us for example that over 80% of the applicants were male. 

We then undertook bivariate analysis to check the relationships between variables to see if we can find correlations. For example, the following graph shows how the loan amount is positively correlated with the total income which imlpies that the loan amount for higher-income applicants is progressively higher. 

<img width="562" alt="Screen Shot 2021-11-17 at 5 18 34 PM" src="https://user-images.githubusercontent.com/88220704/142333409-9eda8137-5fa0-473c-a987-51e80148d1b1.png">

We then saw however, that total income may not be a good indicator of an applicant's loan eligibility. The following graph shows no major difference between the income of those customers who are eligible and those who are not. 

<img width="426" alt="Screen Shot 2021-11-17 at 5 21 21 PM" src="https://user-images.githubusercontent.com/88220704/142333683-3b496717-d6db-40bb-bebf-6e0b08c3dce0.png">

The same analysis was done with the property area, education levels of the applicants, and their credit history. Credit history showed a stark difference in loan approval between those who met the credit history requirements and those that did not as shown in the following graph. 

<img width="418" alt="Screen Shot 2021-11-17 at 5 23 48 PM" src="https://user-images.githubusercontent.com/88220704/142333916-287cbe08-af68-45ed-bb8b-70ae9740da7b.png">


## Model

### Evaluation Criterion

Before training models, it is important to figure out which performance metric we care most about.  Since we want to minimize financial loss to the company,we want to avoid granting eligiblity to customers that are not eligible and therefore we want to minimize the number of false negatives which means that **recall** is the evaluation criterion that we want to focus on. 

The following classification Algorithms were used: 

* Logistic Regression
* K-Nearest Neighbors (KNN)
* Decision Tree with hyperparameter tuning
* Random Forest with hyperparameter tuning

We used a confusion matrix for each of the models to evaluate the performance, with specific focus on the recall score for the ineligible class (class 0). The below example shows the confusion matrix for the logistic regression after accounting for the optimal threshold obtained from the precision-recall curve. 

<img width="504" alt="Screen Shot 2021-11-17 at 6 20 55 PM" src="https://user-images.githubusercontent.com/88220704/142339635-294e5371-c5d5-41c1-af68-7d4cd2eb20e1.png">

For each of these models we also identified the importance of the variables. The below graph shows the feature importances of the random forest. 

<img width="569" alt="Screen Shot 2021-11-17 at 6 27 56 PM" src="https://user-images.githubusercontent.com/88220704/142340355-3db63db4-fe51-42dc-b74d-1e7791557394.png">



## iNterpret

The various algorithms use their own sophisticated ways to identify whether or not an applicant should be eligible for a loan. They identify the most important variables for the decision and make their predictions based on them. 

For example, logistic regression uses an equation as the representation and models the probability of the default class (e.g. the first class). After obtaining the appropriate coefficients, making the predictions comes with simply plugging in the numbers into the logistic regression equation and calculating a result. 

Following this process, we evaulated these models using the confusion matrix to see how many customers were correctly classified. We paid specific attention to the ineligible customers being predicted a loan approval, because this is the metric we want to minimize so that we avoid financial loss. 

## Conclusion

Following the training of these various models, our best model was logistic regression as it provided the highest recall score (66%) for our ineligible applicant class. There is still definitely room for improvement and we will try other algorithms such as xgboost to improve this performance. 

We also concluded that the most important by far for this model was the credit history. Other features that played a part were: 
* The property area being suburban or not
* Whether or not they were married

<img width="291" alt="Screen Shot 2021-11-17 at 6 42 28 PM" src="https://user-images.githubusercontent.com/88220704/142341920-610b57f9-d6e1-4c59-bfa1-f7e255fd0211.png">



# Changes 

* Added: Decision Tree and Random Forest modeling

# Next steps

* Other algorithms such as adaboost and xgboost. 
