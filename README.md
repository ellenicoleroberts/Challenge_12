<img src= "images/default.png" width="930" height="330">

## __Credit Risk Analysis Report__

### __Overview of the Analysis__

Credit risk poses a classification problem that’s inherently imbalanced because healthy loans vastly outnumber risky loans. 

Using a dataset of historical lending activity from a peer-to-peer lending services company, the included notebook in this repo (credit_risk_resampling.ipynb) uses various techniques to train and evaluate models with imbalanced classes to identify the creditworthiness of borrowers. Using various borrower metrics, including the size of the loan, the interest rate, the borrower's income, the debt-to-income ratio, the borrower's number of accounts, any derogatory marks, and total debt-loan status, the notebook identifies the *best* model to predict which loans are at a high-risk of defaulting.

This analysis compares the performance of the two different machine learning approaches used: (1) using a logistic regression model with original data, and (2) using a logistic regression model with oversampled data. The performance is determined by way of accuracy, precision, and recall, each being a metric of how well the model predicts the target variable, 'y' (which is whether a loan will remain healthy or be at a high-risk of default).

The first part of this notebook imports the data via the lending_data.csv file from the Resources folder, and then splits this data into training and testing sets. For reference, a value of '0' in the “loan_status” column means that the loan is healthy while a value of '1' means that the loan has a high risk of defaulting.

A logistic regression model is instantiated and fitted with the original data. Predictions are made for the testing data and saved. The model's performance is then evaluated by way of an accuracy score, a confusion matrix, and a classification report.

Next, another logistic regression model is instantiated and fitted but this time with resampled training data. Resampled data, obtained using the RandomOverSampler module from the imbalanced-learn library, is used as a way to correct for the small number of high-risk loan labels. Note, `value_counts` was used initially to show the extent of the imbalance between the healthy-loans class and loans-at-high-risk class, and later again used after the training data was resampled. As expected, after resampling, the two classes were perfectly balanced with equal numbers in each class.

Using this model fit on the resampled training data, predictions are made for the testing data and saved. The model's performance is then evaluated by way of an accuracy score, a confusion matrix, and a classification report.

### __Results__

Listed here are the balanced accuracy scores and the precision and recall scores of both machine learning models:

* **Logistic Regression model using original data**:
  * Accuracy: .95
  * Precision: 1.00 (class '0'), .85 (class '1')
  * Recall: .99 (class '0'), .91 (class '1')
  
* **Logistic Regression model using resampled data**:
  * Accuracy: .99
  * Precision: 1.00 (class '0'), .84 (class '1')
  * Recall: .99 (class '0'), .99 (class '1')

### __Summary__

Overall, the logistic regression model fit with oversampled data is superior to the logistic regression model fit with original data. First, the accuracy score is higher for the resampled data than it was for the original data (0.95 vs 0.99), meaning that the model using resampled data was better at detecting true positives and true negatives.

Regarding precision, the logistic regression model fit with oversampled data predicts the '0' (healthy loan) label very well with a perfect score of 1.00; regarding the '1' (high-risk loan) label, it does not do as well with a precision rating of .84. This is one percentage point below the precision score for the '1' class (.85) of the model trained on the original data, meaning that the model using the original data was slightly better at detecting the users that were actually going to be at high risk of defaulting.

Sacrificing a little precision however is not a bad trade-off when you consider the improved recall score for the resampled data for the '1' label: .99 versus .91. So, there was a considerable improvement in the '1' label's recall score when using resampled data, meaning that the resampled data correctly clasified a higher percentage of the truly at-high-risk borrowers. Regarding the '0' label's recall score, it was excellent at .99 for both original and resampled data.

All in, the model using resampled data was better at detecting borrowers who are likely to default than the model generated using the original, imbalanced dataset. We recommend using the logistic regression model with the resampled data.

---

## __Technologies__

This application leverages python 3.7 with the following packages that require additional installation:

* pandas: an open-source library that offers easy-to-use data analysis tools for Python.
* pathlib: for creation of file paths allowing the application to interact with a computer's filesystem.
* sklearn: a Python library for machine learning and statistical modeling including tools for classification, regression, clustering and dimensionality reduction.

---

## __Installation Guide__

Begin by cloning the GitHub repo (the same repo that this README.md file is contained within) into your terminal. 

Then activate the correct environment by inputting the following command into your terminal:

`conda activate dev`

Within this environment, next install the above listed dependencies. To do so, in your terminal while in this same repo, enter `pip install -r requirements.txt`.

---

## __Contributors__

Nicole Roberts,
elle.nicole.roberts@gmail.com

---

## __License__

[BSD 3](https://choosealicense.com/licenses/bsd-3-clause-clear/): BSD 3-clause is a permissive licence, allowing nearly unlimited freedom with the software as long as BSD copyright and license notice is included.