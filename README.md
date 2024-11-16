# Cardiovascular Disease Risk Prediction Using Logistic Regression
![alt text](images/image.png)

*Image Source: [Google Images](https://images.app.goo.gl/RcmNZLhfTAZMNHfJ9)*

A logistic regression model to predict the likelihood of an individual developing cardiovascular disease (CVD) in the next 10 years. This project focuses on preprocessing, class imbalance handling, hyperparameter tuning, and evaluating model performance using real-world health data.

## Table of Contents

<ol>
<li><a href="#Overview"><b> Overview </a></b></li>
<li><a href="#Datasets"><b> Datasets </a></b></li>
<li><a href="#EDA"><b> Exploratory Data Analysis </a></b></li>
<li><a href="#featureengineering"><b> Feature Engineering </a></b></li>
<li><a href="#summary"><b> Summary Till Now </a></b></li>
<li><a href="#tuning"><b> Model Tuning </a></b></li>
<li><a href="#finalization"><b> Model Finalization </a></b></li>
<li><a href="#saveload"><b> Saving & Loading the Model </a></b></li>
<li><a href="#conclusion"><b> Conclusion </a></b></li>
</ol>




<h2 id="Overview">1. Overview</h2>
 WHO (World Health Organization) estimates that out of 5 deaths, 4 of them are realted to the cardiovascular disease(CVD), so the goal of this project is to use Logistic Regression to determine the propoertion of patients who are at a high risk of CVD. 

 This project focuses on preprocessing, class imbalance handling, hyperparameter tuning, and evaluating model performance using real-world health data.

<h2 id="Datasets">2. Dataset</h2>
The dataset has a total of:<br>
 - Rows:  4240 <br>
 - Features:  16

 Target Column: TenYearCHD (1 = Risk of CVD, 0 = No Risk)

#### 2.1 Features used:
- Demographic: male, age
- Health: currentSmoker, cigsPerDay, BPMeds, prevalentStroke, prevalentHyp, diabetes
- Measurements: totChol, sysBP, diaBP, BMI, heartRate, glucose

#### 2.2 Data Cleaning:
- Irrelevant column 'education' has been dropped.
- There were missing values too, here we have dropped it else we could have used imputation or other methods to fill up those missing values but for the shake of this project, we dropped it.

![alt text](images/image-1.png)

<h2 id="EDA">3. Exploratory Data Analysis</h2>

#### 3.1 Univariate Analysis:
a. Histogram:

To visualize the distribution of a single variable and identify its range, skewness, and presence of outliers.
![alt text](images/image-2.png)

b. Density Plot:

To show the probability distribution of a variable and provide insights into its shape and central tendencies.
![alt text](images/image-3.png)

c. Box Plot:

To highlight the spread and variability of a variable, including its median, quartiles, and outliers.
![alt text](images/image-4.png)

#### 3.2 Multivariate Analysis:
a. Heatmap:

To identify relationships between numerical variables and detect multicollinearity in the data.
![alt text](images/image-5.png)

#### 3.3 Checking Class Imbalance:
When working with classification task, it is important to check if the class or the count of the classes of the target feature is balanced or not. For that we can just simple target that column and count the values.
![alt text](images/image-6.png)

<b> There is a clear case of class imabalance here. </b>

So, now we will use a technique called <b>Resampling </b> and keep it separately and later on test our model on the original imabalanced data and this newly oversampled data and compare the results.

#### 3.4 Handling Class Imbalance:
![alt text](images/image-7.png)

so, the countplot below shows the count of the classes on the original and oversampled data.
![alt text](images/image-8.png)

<br>

![alt text](images/image-9.png)


<h2 id="featureengineering">4. Feature Engineering </h2>

Here, first we will use the original dataset and then use the oversampled dataset.

<h3> 4.1 On the original dataset</h3>
1. First we will split the data into training and testing data so that we can use training data to build the model and test data to find the generalization of the model. <br>

![alt text](images/image-11.png)
2. We will use a <b>Pipeleine</b> so that it can automate the sequence of preprocessing steps and model training, ensuring consistency and reducing the risk of errors. <br>
<br>
<b>NOTE: </b>Here, we have only used 7 as the value for K in SelectKBest just for the testing purpose, later on when optimizing the hyperparameter, we will use differen variations.

![alt text](images/image-10.png)

Then we will fit the pipeline on X_train and y_train data. This is the split that we did in the first step on the original oversampled dataset.

Once the model is trained, we will predict on the X_test data and compare the results. <br>
<br>
Since we are working with imbalanced dataset, accuracy alone cannot be used as the decision metrics on the generalization. Below is the result of the training and testing data:<br>

![alt text](images/image-12.png)

As we can see the accuracy on the training and testing data is quite high but it is not useful, we are looking at F1-Score, which is the generalization of Precision and Recall and are commonly used metrics for imbalanced dataset.

<h3> 4.2 On the oversampled dataset</h3>
- Similarly, we repeat the same process on the oversampled dataset. We will split the oversampled data in training and testing data and fit the model on the training data.

![alt text](images/image-13.png)

The metrics on the oversampled data:

![alt text](images/image-14.png)

Although the accuracy is low in the oversampled dataset, the F1-score is better than that of the original dataset.
But still, we will tune hyperparameter for both, the original and the oversampled dataset, then compare the metrics and only select the final hyperparameters and select the dataset that we want to finalize 
to train our final model.

<h2 id="summary">5. Summary Till Now </h2>

- We tried out with both the orignal and oversampled data, but the original data is outperformed.


- Accuracy alone cannot be used to determine the quality of the model.


- Now, we could try other ensemble models but since we are just focusing on Logistic Regression, we will further proceed 
with GridSeachCV, where we will optimize our model to find the best hyper-parameter.


<h2 id="tuning">6. Model Tuning</h2>

To find the best hyperparameters, we will use <b>GridSeachCV</b>.

We will use these parameter grid:

![alt text](images/image15.png)


#### 6.1 Fit the gird search on the original dataset:

![alt text](image.png)

<b> Print the best hyperparameters: </b>

![alt text](image-1.png)

<b> Print the metrics: </b>

![alt text](image-2.png)

![alt text](image-3.png)

There is no any improvement on the F1-score.

#### 6.2 Fit the gird search on the oversampled dataset:

Here, also we will repeat the same process as above but on the oversampled dataset.

![alt text](image-4.png)

<b> Print the best hyperparameters: </b>

![alt text](image-5.png)


<b> Print the metrics: </b>

![alt text](image-6.png)

![alt text](image-7.png)

The metrics shows, using the oversampled data, we got better results.

<h2 id="finalization">7. Model Finalization </h2>

So, we are done with finding the best hyperparameters and we also saw that oversampling the data was the best idea as this was imbalanced dataset, using metrics like Accuracy alone is not an effective way to finalize the model. So, we had to compare other metrics like precision, recall, and F1-score.

#### 7.1 Selecting the best estimators:
![alt text](image-8.png)


#### 7.2 Fitting entire dataset on the final model:
![alt text](image-9.png)



<h2 id="saveload"> 8. Saving & Loading the Model:</h2>

We can use <b>joblib</b> to dump(save) and load the saved model for future predicitons.

#### 8.1 Save the model:

![alt text](image-10.png)

#### 8.2 Load the model:
![alt text](image-11.png)

#### 8.3 Make Predictions:
![alt text](image-12.png)



<h2 id="conclusion">9. Conclusion </h2>

Working with an imbalanced dataset is a challenging task, particularly in sensitive domains 
like healthcare, where misclassifications can have significant consequences. Relying solely 
on accuracy as a metric can be misleading, as it does not adequately capture the performance 
of models on minority classes. Therefore, metrics like Precision, Recall, F1-score, and Area 
Under the Precision-Recall Curve (PR-AUC) are more appropriate for evaluating model generalization 
in such scenarios.

In this project, I implemented a sampling technique to address class imbalance, but it’s 
worth noting that several other methods, such as SMOTE, cost-sensitive learning, and ensemble 
methods, could also be explored. Additionally, this project demonstrates the use of Logistic 
Regression, one of the most popular algorithms for binary classification. However, experimenting 
with other classification algorithms, such as Random Forest, Support Vector Machines, or Gradient 
Boosting methods, could potentially yield even better results.


