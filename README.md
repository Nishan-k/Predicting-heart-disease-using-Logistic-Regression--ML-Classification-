# Cardiovascular Disease Risk Prediction Using Logistic Regression
![alt text](image.png)

*Image Source: [Google Images](https://images.app.goo.gl/RcmNZLhfTAZMNHfJ9)*

A logistic regression model to predict the likelihood of an individual developing cardiovascular disease (CVD) in the next 10 years. This project focuses on preprocessing, class imbalance handling, hyperparameter tuning, and evaluating model performance using real-world health data.

## Table of Contents
1.  [Overview](#overview)
2.  [Dataset](#dataset)
3.  [Exploratory Data Analysis](#eda)
4.  [Results](#results)
5.  [Conclusion](#conclusion)



## 1. Overview
 WHO (World Health Organization) estimates that out of 5 deaths, 4 of them are realted to the cardiovascular disease(CVD), so the goal of this project is to use Logistic Regression to determine the propoertion of patients who are at a high risk of CVD. 

 This project focuses on preprocessing, class imbalance handling, hyperparameter tuning, and evaluating model performance using real-world health data.

## 2. Dataset
The dataset has a total of:
 - Rows: 4240
 - Features: 16

 Target Column: TenYearCHD (1 = Risk of CVD, 0 = No Risk)

#### 2.1 Features used:
- Demographic: male, age
- Health: currentSmoker, cigsPerDay, BPMeds, prevalentStroke, prevalentHyp, diabetes
- Measurements: totChol, sysBP, diaBP, BMI, heartRate, glucose

#### 2.2 Data Cleaning:
- Irrelevant column 'education' has been dropped.
- There were missing values too, here we have dropped it else we could have used imputation or other methods to fill up those missing values but for the shake of this project, we dropped it.

![alt text](image-1.png)


## 3. Exploratory Data Analysis:
