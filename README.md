# Human Resources Data Visualization
This is my 2nd project for my Data Visualization Class. For this project we were tasked with the following:
1. Select a dataset of our choosing (Human Resources)
2. Chop the dataset using pandas or any other method in python
3. Clean the dataset and drop missing values if needed
4. Create two types of visualization minimum
5. Create an excellent readme file
6. Push to Github and Kaggle

## About the Readme
This readme is to be used as a more straight forward walkthrough of the project that was created.
In this readme you will find the following:
1. Human Resources Data Visualization
2. About the Readme
3. About the Dataset
4. How to Run the Code
5. Importing the Data
6. Cleaning the Data
7. General Data Visualization
8. The Heatmap
9. Summary

## About the Dataset
![picture alt](http://ci.alamogordo.nm.us/Assets/COA+Documents+$!26+Images/Human+Recources/HR.jpg)

Human Resources typically focuses on providing tools and enforcing laws that protect employees as well as help keep their overall
satisfaction high.  This dataset focuses on employee turnover and the factors that lead to emplyees leaving the company.
This dataset contains the following 10 features that were examined with roughly 15,000 employees:
1. Satisfaction Level
2. Last Evaluation
3. Number of Projects
4. Average Monthly Hours
5. Time Spent at the Company
6. Whether They have had a Work Related Accident
7. Whether They have has a Promotion within the Last 5 Years
8. Departments (Ex: Sales)
9. Salary
10. Turnover

You can get this dataset by creating an account on Kaggle and following this link:
https://www.kaggle.com/ludobenistant/hr-analytics

## How to Run the Code
To run the code you should use anaconda3 or jupyter notebook with python 3. 
You will also need numpy, pandas, matplotlib, and seaborn libraries in python.

## Importing the Data
After you have the previously mentioned libraries in python 3, it is now time to start importing the libraries and the data.
To import the libraries enter the following code:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import matplotlib as matplot
import seaborn as sns
%matplotlib inline
```
Note: If any of the libraries fail to load please try reintstalling the libraries in order to continue.

Next we are going to import the data and put it into a dataframe called HR_DF.  To do this we run the following code:
```python
HR_DF = pd.read_csv('../input/HR_comma_sep.csv')
```

## Cleaning the Data
The Human Resources dataset that we are using is a very clean dataset and actually requires very little editing.  When
looking at the data, we notice that the features in the table has some spelling errors and are jsut difficult to read.  We can edit
and view the new table by entering the following code:
```python
HR_DF = HR_DF.rename(columns={'satisfaction_level': 'satisfaction',
                             'last_evaluation': 'evaluation',
                             'number_project': 'projectCount',
                             'average_montly_hours': 'AVG_MonthlyHours',
                             'time_spend_company': 'yearsAtCompany',
                             'Work_accident': 'workAccident',
                             'promotion_last_5years': 'promotion',
                             'sales': 'department',
                             'left': 'turnover'
                             })
 HR_DF.head()
 ```
 
 ## General Data Visualization
 Now that the data is how we want it we can finally visualize the data.  To do some general graphs we can enter the following code:
 ```python
 fig, axs = plt.subplots(ncols=2,figsize=(12,6))
x = sns.countplot(HR_DF['department'], ax=axs[0])
plt.setp(x.get_xticklabels(), rotation=45)
y = sns.countplot(HR_DF['salary'], ax=axs[1])
plt.tight_layout()
plt.show()
```
![picture alt](https://raw.githubusercontent.com/ainnes84/Human-Resources-Data-Visualization/master/Department_Salary.jpg)

We can conclude from the above two histograms the following things:
* The sales department has the highest number of employees
* The majority of employees in this dataset have a low to medium salary

More code:
```python
fig, axs = plt.subplots(ncols=3,figsize=(12,6))
sns.countplot(HR_DF["workAccident"], ax=axs[0])
sns.countplot(HR_DF["promotion"], ax=axs[1])
sns.countplot(HR_DF["turnover"], ax=axs[2])
plt.tight_layout()
plt.show()
```
![picture alt](https://raw.githubusercontent.com/ainnes84/Human-Resources-Data-Visualization/master/Images/Accident_Promotion_Turnover.png)

The previous histograms show the following:
* The majority of workers have not had a work related accident
* Very few have recieved a promotion within the past 5 years
* The average turnover for the company is roughly 25%

Next Group:
```python
fig, axs = plt.subplots(ncols=3,figsize=(12,6))
sns.distplot(HR_DF["satisfaction"], ax=axs[0])
sns.distplot(HR_DF["evaluation"], ax=axs[1])
sns.distplot(HR_DF["AVG_MonthlyHours"], ax=axs[2])
plt.tight_layout()
plt.show()
```
![picture alt](https://raw.githubusercontent.com/ainnes84/Human-Resources-Data-Visualization/master/Images/Satisfaction_Evaluation_MonthlyHours.png)

Final Chunk:
```python
fig, axs = plt.subplots(ncols=2,figsize=(12,6))
axs[0].hist(HR_DF["projectCount"],bins=6)
axs[0].set_xlabel("Number of Projects")
axs[0].set_ylabel("Number of Employees")
axs[1].hist(HR_DF["yearsAtCompany"],bins=6,color='r')
axs[1].set_xlabel("Years at the Company")
axs[1].set_ylabel("Number of Employees")
plt.tight_layout()
plt.show()
```
![picture alt](https://raw.githubusercontent.com/ainnes84/Human-Resources-Data-Visualization/master/Images/ProjectCount_Years.png)

## The Heatmap
Below is a heatmap and correlation matrix showing different factors and how relavant they are to each other. Some key findings include:

* Satisfaction vs. Turnover: -0.388375
  * Since this is a negative relationship, these two are highly correlated. This could mean the least satisfied employees are more likely to leave.
* AVG_MonthlyHours vs. projectCount: 0.417211
  * A positive relationship that is moderately correlated. Most likely due to more projects = more hours spent working. Which leads us to our next one:
* projectCount vs evaluation: 0.349333
  * Another positive relationship that is moderately correlated. Most likely due to employees who work on more projects are evaluated more than those who do not.
 
 To show the heatmap we enter the following code:
 ```python
 correlation = HR_DF.corr()
plt.figure(figsize=(10,10))
sns.heatmap(correlation, vmax=1, square=True, annot=True, cmap='cubehelix')

plt.title('Correlation Between Features')

correlation
```
![picture alt](https://raw.githubusercontent.com/ainnes84/Human-Resources-Data-Visualization/master/Images/Heatmap.png)

## Summary
Based on the data interpreted in this dataset, we can conlude the following:

* The least satisfied employees within the company are more likely to have a higher turnover rate.
* Highest indicator of employee turnover.
* Higher project count leads to more hours worked. However, employees are more likely to leave when they are overworked or underworked.
* The majority of employees have a low to medium salary. This also happens to be where the bulk of employee turnover lies.

### Author
Andrew Innes
Contact @: ainnes84@live.com
