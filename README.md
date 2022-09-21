# capstone-project
DABC Capstone Team Project

## Rationale and Data Source
*AUTHOR FOR THIS SECTION: Tyler Hendricks

Selected Topic: Suicide Risk in Adolescents

Rationale for Selection:

Several members of the team have an interest in the healthcare industry and so it was initially determined that the project would focus on a topic associated with healthcare. After narrowing down possible topics, suicide risks in adolescents was selected because this is a current challenge that the state of Utah faces. Utah has seen its adolescent suicide rate triple since the year 2000. It is thought that machine learning and artificial intelligence can assist in helping clinicians identify which adolescents are at risk. The goal of this project will be to create such a model. 

Data Source:

The data for this project was sourced from the YRBSS (Youth Risk Behavior Surveillance System) survey. The data was collected in 2019 and covers a range of risky behaviors in US adolescents. The survey was designed to determine the relationshp between the prevalance of risk behaviors and can be used to examine the co-occurence of health issues. [Click here](https://github.com/tylerah/capstone-project/blob/main/data/2019_National_YRBS_Data_Users_Guide.pdf) to access the published user's guide for the data set. For more information on the YRBSS, please visit the following website published by the CDC: www.cdc.gov/yrbss

Potential Answers:

It is expected that by using a machine learning model, risk factors that correlate with adolescent suicide risk can be identified. Specifically, correlations between attempted suicide and frequent risk factors will be examined in order to determine the behaviors that are most closely associated with suicide risk.


## Machine Learning Model
*AUTHOR FOR THIS SECTION: Isaac Jorgensen*

The project's mission is to be able to predict suicide risk from survey data taken from the CDC (YRBSS) for youth in high school. As such, the target variable will be a boolean (0, 1) classification with 0 indicating no suicide risk and 1 inidicating that there is. It was decided to use a random forest ensemble learning model because the nature of the project aligns with the ways random forest excels: resistant to overfitting, naturally ranks feature importance, and handles outliers well. 
Because mental health is such an important aspect of an individuals life and can have devastating affects if left unattended, it's important for this model to have a higher sensitivity score than precision. If a false negative is returned, the worst thing that could happen is more people are helping monitor their health.

This project will use the sklearn library's RandomForestClassifier, train_test_split, StandardScaler, confusion_matrix, and classification_report to help analyze and interpret the results.

The following is a loose step-by-step plan of how the model will be implemented:
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
