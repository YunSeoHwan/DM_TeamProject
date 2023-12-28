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
