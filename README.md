# capstone-project
DABC Capstone Team Project

## Machine Learning Model
AUTHOR: Isaac Jorgensen
Which model did you choose and why?
How are you training your model?
What is the model's accuracy?
How does this model work?

The project's mission is to be able to predict suicide risk from survey data -- taken from this place. As such, the target variable will be a boolean (0, 1) classification with 0 indicating no suicide risk and 1 inidicating that there is. It was decided to use a random forest ensemble learning model because the nature of the project aligns with the ways random forest excels: resistant to overfitting, naturally ranks feature importance, and handles outliers well. 
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
    * Create creation metrics
    * Analyze and interpet accuracy, precision, and sensitivity
* Make conclusions
    * Does this model perform optimally? (at least above 75%, optimally at or above 95%)
    * If not, can we improve its performance?
        * Bagging and Boosting
        * Feature Importance
        * Sampling differences (SMOTE, SMOTEEN, oversampling, undersampling)
    * If necessary, use another machine learning model (like Logistical Regression)