# Project Title
This project was conducted during the Data Mining class in the second semester of 2023.
<br><br>

# Project Background 
Medical attrition refers to the voluntary or involuntary departure of healthcare professionals from their workplaces, such as hospitals. This kind of attrition can have a significant impact on medical facilities.
A sudden loss of staff can lead to a shortage of manpower, possibly worsening the working conditions for the remaining medical staff. Ultimately, the quality of the healthcare services provided can deteriorate. <br>
Furthermore, from the managerial perspective of healthcare facilities, sudden staff turnover can pose a significant risk to hospital operations. Given the substantial cost required to train nursing staff, predicting and preventing staff attrition is crucial.<br><br>
For these reasons, predicting staff turnover in hospitals is an incredibly important issue. Therefore, we have aimed to construct a classification model with high interpretability to make more accurate predictions and to identify specific causes of staff attrition. Furthermore, we seek to propose ways in which the model can be utilized.
<br><br>

# Project Process  

## Stack
### Language & Library
<div>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Numpy-013243?style=flat&logo=Numpy&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-150458?style=flat&logo=Pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/Scikit learn-F7931E?style=flat&logo=Scikitlearn&logoColor=white"/>
</div>

### Model
<div>
  <img src="https://img.shields.io/badge/Statsmodels-000000?style=flat&logo=&logoColor=white"/>
  <img src="https://img.shields.io/badge/LogisticRegression-000000?style=flat&logo=&logoColor=white"/>
  <img src="https://img.shields.io/badge/SVM-000000?style=flat&logo=&logoColor=white"/>
  <img src="https://img.shields.io/badge/Naive bayes-000000?style=flat&logo=&logoColor=white"/>
</div>
<br><br>

## Pipeline
### Dataset
In this project, the data utilized was a dataset on [**Employee Attrition**](https://www.kaggle.com/datasets/jpmiller/employee-attrition-for-healthcare/data) for healthcare.

### Preprocessing
#### **Categorical**
- There were a total of 9 categorical features, and among them, the 'Over18' variable, which had the same value for all samples, was removed.
- Excluding 'Over18', the remaining 8 categorical variables each had varying cardinalities. Thus, to experimentally determine the optimal encoding method, we divided them into a total of 4 cases, as shown in the figure below.<br><br>
![image](https://github.com/YunSeoHwan/DM_TeamProject/assets/48356954/827a0c7c-3798-42c7-94e3-d09cd457fd44)<br>
- To assess the performance of each encoding, we conducted experiments comparing metrics using the least variant baseline model, logistic regression.
- To empirically determine the appropriate preprocessing method, we applied standard, MinMax, and Robust scaling to each of the 4 previously encoded cases.
- We carried out comparative experiments using the baseline logistic regression model, evaluating accuracy, recall, and F1 score, along with 5-fold cross-validation.
- Ultimately, we selected the dataset that applied the Standard scaler to Case 4.
<br><br>

#### **Numerical**
- There were a total of 26 numerical variables, out of which 'EmployeeID' and 'StandardHours', which had the same value for all samples, were removed.
- We identified a class imbalance issue and compared metrics with and without the use of three oversampling algorithms: Random Oversampling, SMOTE, and ADASYN (following the same procedure as the encoding method).
- The oversampling results showed a decrease in accuracy compared to the original model, and there was no significant difference in the F1 score, considering that the imbalance issue could be reduced (hence, we proceeded without applying oversampling).
- Therefore, the final dataset was configured as shown in the figure below, reflecting the aforementioned results<br><br>
![image](https://github.com/YunSeoHwan/DM_TeamProject/assets/48356954/a32a0360-c179-49b6-a08e-23f0061ef78b)

### Modeling
#### Cross Validation between models
To compare the baseline performance among models, we conducted a performance comparison using logistic regression as a base, including three shrinkage methods, SVM, and Naive Bayes, totaling six models. We verified the average performance using 5-fold cross-validation, where logistic regression generally showed superior performance. SVM yielded lower performance due to its sensitivity to hyperparameters, prompting us to proceed with hyperparameter tuning to assess its performance. <br><br>
![image](https://github.com/YunSeoHwan/DM_TeamProject/assets/48356954/309ebb35-5b9f-4421-8063-5b9136123095)
<br><br>

#### Feature Selection
Prior to hyperparameter tuning, we performed feature selection to reduce computational load. To check for multicollinearity, we considered the Variance Inflation Factor (VIF) and Confidence Interval (CI), selecting features with a VIF exceeding 8 and CI over 30, and monitored p-values through cross-validation. Subsequently, we removed 12 variables in total and, upon comparing model performance, observed improvements in recall and F1 score.<br><br>
![image](https://github.com/YunSeoHwan/DM_TeamProject/assets/48356954/ab0388e3-ae01-467e-91e8-8407ddebd0d1)<br><br>

#### Before Hyperparameter Tuning
We re-evaluated the performance of the models based on the feature selection. Default hyperparameters were used. The results are as illustrated in the figure below. <br><br>
![image](https://github.com/YunSeoHwan/DM_TeamProject/assets/48356954/78f5840c-6fb1-49a6-814d-9c534738691a)
<br><br>

#### After Hyperparameter Tuning
After conducting hyperparameter tuning, we evaluated the performance of the six models, and considering the number of false negatives and false positives, we selected ElasticNet as the final model.
We used Bayesian optimization from Scikit-learn's optimization tools.
<br><br>
![image](https://github.com/YunSeoHwan/DM_TeamProject/assets/48356954/494730a5-d8d0-4826-86b4-6d1efe9e96ee)
<br><br>

### Role
#### [**YunSeoHwan**](https://github.com/YunSeoHwan) : EDA, Preprocessing, Modeling, Interpretation<br>
#### KimJuHyuk: EDA, Preprocessing, Modeling, Interpretation
#### SongJunhyun : EDA, Preprocessing, Modeling, Interpretation
#### OhSeungjun : EDA, Preprocessing, Modeling, Interpretation <br>

# Result & Suggestion
## Performance of final model according to threshold
We adjusted the threshold of the final model to fit specific situations. While the default threshold is 0.5, if we aim to predict attrition more conservatively, we could set a lower threshold, like 0.15, to increase recall. Conversely, if we consider the overall prediction performance for attrition, we might adjust the threshold to a level like 0.35. <br><br>
![image](https://github.com/YunSeoHwan/DM_TeamProject/assets/48356954/0d563b77-a7e1-471a-a8b5-93239ba08bc6)
<br><br>

We applied PCA to the selected features with varying numbers of principal components to evaluate performance. We identified points where recall and F1 score were generally favorable, and with 27 principal components, the performance was as depicted in the figure below. <br><br>
![image](https://github.com/YunSeoHwan/DM_TeamProject/assets/48356954/233c60c9-af88-438a-b0c3-4e46af598ded)
<br><br>

## Analyzing the coefficient of a variable
we examined the coefficients of the final model. The coefficients represent the change in the log-odds for a one-unit increase in the corresponding X variable. For instance, when age increases by one unit, the log-odds of attrition decrease by about -1.
Intuitively, one might think that lower job intensity or higher wages would reduce the probability of attrition.
Variables such as OverTime, which indicates the amount of overtime work, and BusinessTravel, which reflects the frequency of business trips, show intuitive results where an increase in these variables leads to higher attrition rates.
Conversely, wage-related variables like MonthlyIncome and Hourly Rate were eliminated during the feature selection process, suggesting that salary may not have a significant impact on predicting staff turnover.
The coefficients for YearsInCurrentRole, TotalWorkingYears, and JobLevel suggest that an increase in tenure corresponds to a lower probability of attrition. Therefore, it indicates that more attention may be needed in managing newer employees with less tenure to prevent staff turnover. <br><br>
![image](https://github.com/YunSeoHwan/DM_TeamProject/assets/48356954/20b8f7cb-a593-412c-93c0-7cd38db29122) <br><br>

## Calculate confidence intervals
We aimed to provide insights into what percentage of the total workforce might leave by calculating a confidence interval for the attrition rate. Viewing the training data as a sample drawn from the entire population, we used the attrition rate from the training data as the sample proportion to estimate the interval for the population proportion.
The results of estimating a 95% confidence interval indicated that the upper limit of the attrition rate was 0.14, and the lower limit was 0.10.
This means that, based on a 95% confidence interval, we can expect that 10 to 14 out of every 100 employees may leave.<br><br>
![image](https://github.com/YunSeoHwan/DM_TeamProject/assets/48356954/47052db2-9805-4717-916d-a8e111cc3aee) <br><br>
The scatter plot below shows the results of projecting the training/test data into two dimensions using PCA. When considering the test data as unseen data unknown to us, we can observe that the distribution of the training data is similar to that of the unseen data.
Furthermore, the attrition rate of the unseen data is 0.119, which falls within the previously calculated 95% confidence interval.
This information can be utilized to reduce managerial risks in healthcare facilities. For example, knowing that 10 to 14 out of every 100 employees might leave, a hiring manager could conservatively plan to recruit 120 people when 100 are needed.
This approach is particularly beneficial in high-stakes areas like intensive care units, where the cost of attrition can exceed the cost of additional hiring. Through conservative hiring practices, it is possible to prevent a decline in the quality of medical services due to staff attrition. <br><br>![image](https://github.com/YunSeoHwan/DM_TeamProject/assets/48356954/a639d7fa-4b8b-4e11-a938-d550f5353d5d) <br><br>
