# capstone-project
DABC Capstone Team Project

## Overview of Project

**Selected Topic: Suicide Risk in Adolescents**
 
The purpose of this project was to build a machine learning model capable of accurately predicting youth suicide risk using data from a health questionnaire. The questionnaire used in this project was the YRBSS, which is administered yearly to American high school students. There are over 90 questions, including demographics, smoking/drug use, seat belt use, nutrition, mental health, bullying, and more, which were used to train the model. A random forest model was ultimately created, which had over 99% accuracy in classifying training data into students who would attempt suicide or not. 

Data was downloaded from the CDC website and converted into a csv. It was then stored in an S3 bucket on AWS, and put into a postgres database (also on AWS) using python and pandas. Data was preprocessed with python and pandas by interpolating missing data, encoding some variables, and scaling the data. Data was then put in the machine learning model. Data was also imported into tableau, where a dashboard was created for the project. 


## Rationale and Data Source

**Rationale for Topic Selection:**

Several members of the team have an interest in the healthcare industry and so it was initially determined that the project would focus on a topic associated with healthcare. After narrowing down possible topics, suicide risks in adolescents was selected because this is a current challenge that the state of Utah faces. Utah has seen its adolescent suicide rate triple since the year 2000, and suicide is the leading cause of death for Utahns ages 14-18. 

The project also has a broader application. The machine learning model could help identify which adolescents are at risk of dying by suicide if future data was ran through the model. Also, risk factors that help predict adolescent suicide attempts were identified. Information from this project could be helpful in suicide prevention efforts

**Data Source:**

The data for this project was sourced from the YRBSS (Youth Risk Behavior Surveillance System) survey. The data was collected in 2019 and covers a range of risky behaviors in US adolescents. The survey was designed to determine the relationship between the prevalence of risk behaviors and can be used to examine the co-occurrence of health issues. [Click here](https://github.com/tylerah/capstone-project/blob/main/data/2019_National_YRBS_Data_Users_Guide.pdf) to access the published user's guide for the data set. For more information on the YRBSS, please visit the following website published by the CDC: www.cdc.gov/yrbss


## Machine Learning Model

**Planning:**

The project's mission is to be able to predict suicide risk from survey data taken from the CDC (YRBSS) for youth in high school. As such, the target variable is a boolean (0, 1) classification with 0 indicating no suicide risk and 1 indicating that there is. It was decided to use a random forest ensemble learning model because the nature of the project aligns with the ways random forest excels: resistant to overfitting, naturally ranks feature importance, and handles outliers well. 
Because mental health is such an important aspect of an individuals life and can have devastating effects if left unattended, it was important for this model to have a higher sensitivity score than precision. If a false negative is returned, the worst thing that could happen is more people are helping monitor their health.

This project used the sklearn library's RandomForestClassifier, train_test_split, StandardScaler, confusion_matrix, and classification_report to help analyze and interpret the results.

The following is a loose step-by-step plan of how the model was implemented:
* Pre-process dataset
    * Handle null values with interpolation
    * Encode categorical values
    * Split data into training and testing sets
        * Separate target variable from features
        * Use train_test_split to create groups
    * Scale the new dataset groups
        * Use StandardScaler instance
* Fit the random forest model
    * Create instance of RandomForestClassifier
        * estimators = 128
        * random_state = 78
    * Fit model with x and y training datasets
* Make predictions
* Evaluate performance
    * Create summary metrics
    * Analyze and interpet accuracy, precision, and sensitivity
* Make conclusions
    * Does this model perform optimally? (at least above 75%, optimally at or above 95%)
    * If not, can we improve its performance?
        * Bagging and Boosting
        * Feature Importance
        * Sampling differences (SMOTE, SMOTEEN, oversampling, undersampling)
    * If necessary, use another machine learning model (like Logistical Regression)

**Execution:**

After interpolating the data, splitting into the training and testing groups (through train_test_split), scaling it, and passing it through the RandomForestClassifier, the model returned the following values:
    * recall: 1.0
    * precision: 0.9
    * accuracy: 0.91
Luckily, the model performed exceptionally well in the first pass and the first model choice the team selected for the project. A high recall score indicates that most, if not all, youth who attempted suicide were able to be identified as such through the model. And luckily, there weren't many false positives recorded, either! While having a few false positives was acceptable for the use-case of this model, it is encouraging to see such strong performance.


## Tableau Dashboard

### Link to Dashboard
https://public.tableau.com/app/profile/tyler.hendricks/viz/DABCCapstoneProject-SuicideRiskinAdolescents/Dashboard-SuicideinAdolescence?publish=yes

### Link to Google Slideshow
https://docs.google.com/presentation/d/10kaRYGAx5FV9UMT_6x0MvqeqaaQCGQL8VoUxayhrCW4/edit#slide=id.g87a89564d6d86dd_35

### Explanation
Initial charts were just the overall count of suicide ideation / attempts. However, these charts are misleading in some cases due to the sample including many more white individuals than other races. As such, a second wave of charts were generated in order to show the percentage of each race that considered, planned, and attempted suicide. This breakdown provides a more meaningful context. 

Examples included here:

![screenshot_tableau_black](https://user-images.githubusercontent.com/104606662/193771890-2a40e3ef-2be1-4376-9450-205271bb30d7.png)

![screenshot_tableau_white](https://user-images.githubusercontent.com/104606662/193771916-da8f969f-fb39-43f0-9a69-73708b016f62.png)

While constructing graphs for a breakdown by sexual orientation, it was observed that the numbers do not match what is expected from national data (some sources indicate that LGBTQ suicide rates are well about 20%. This doesn't track with the data in this sample and is potentially an area for improvement. Excel was used to verify that the numbers produced in Tableau were correct even though they don't match other national data sources. While other breakdowns (race & gender) track with what is expected, the difference seen in sexual orientation raises questions to the accuracy of this particular data source. Further scrutiny is warranted. 

## Database & Data Storage

Data was first divided into two tables: demographics, and responses to survey questions. Data was stored as two csvs in an AWS S3 bucket. An AWS postgres RDS was also set up to house the data. Code in a jupyter notebook was written to:
1. Pull data into a pandas dataframe from the S3 bucket
2. Put the pandas dataframe into the postgres database
3. Pull data from the database back into a pandas dataframe
4. Pull a joined table in from the database, to demonstrate the capabilities of manipulating and joining data in pgAdmin
