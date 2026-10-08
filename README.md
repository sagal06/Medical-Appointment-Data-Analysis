# Medical Appointment Data Analysis

## Project Overview

This project analyzes a medical appointment dataset to understand the factors associated with patients attending or missing their scheduled appointments.

The dataset contains information about patients such as age, gender, health conditions, scholarship status, SMS reminders, appointment dates, scheduling dates, and neighbourhood.

The main purpose of this project is to clean the data, explore different patterns through visualizations, and build a classification model to predict whether a patient is likely to miss an appointment.

---

## Objectives

The main objectives of this project are:

* Understand the structure and characteristics of the dataset.
* Clean and prepare the data for analysis.
* Analyze the overall appointment attendance rate.
* Explore the relationship between patient characteristics and attendance.
* Analyze the relationship between SMS reminders and appointment attendance.
* Study the relationship between waiting time and missed appointments.
* Compare appointment attendance across different groups and neighbourhoods.
* Build a classification model to predict appointment no-shows.
* Evaluate and interpret the performance of the classification model.

---

## Dataset

The dataset contains information about medical appointments and whether patients attended their scheduled appointments.

Some important attributes include:

| Column | Description |
|---|---|
| Gender | Gender of the patient |
| Age | Age of the patient |
| Hypertension | Whether the patient has hypertension |
| Diabetes | Whether the patient has diabetes |
| Scholarship | Whether the patient received a scholarship |
| SMS_received | Whether the patient received an SMS reminder |
| ScheduledDay | Date and time when the appointment was scheduled |
| AppointmentDay | Date of the actual appointment |
| Neighbourhood | Location of the appointment |
| No-show | Original appointment attendance status |

A new `show` variable was created during preprocessing to make the target easier to work with:

* `1` → Patient attended the appointment
* `0` → Patient did not attend the appointment

For the classification model, this was converted into a `no_show` target:

* `1` → Patient missed the appointment
* `0` → Patient attended the appointment

---

## Data Cleaning and Preprocessing

The following preprocessing steps were performed:

* Loaded the dataset using Pandas.
* Inspected the rows, columns, data types, and summary statistics.
* Checked for missing values.
* Checked for duplicate records.
* Removed unnecessary identifier columns.
* Standardized column names.
* Converted appointment and scheduling columns to datetime format.
* Calculated the number of days between scheduling and appointment dates.
* Created a binary `show` variable for appointment attendance.
* Removed invalid records with negative age or negative waiting time before modelling.

For calculating the waiting period, the date portions were compared rather than the time components so that same-day appointments were not incorrectly assigned a negative value.

---

## Exploratory Data Analysis

The analysis focuses on the following areas:

### Overall Appointment Attendance

The overall proportion of patients who attended and missed their appointments was calculated to understand the distribution of the target variable.

### Gender

Appointment attendance was compared between male and female patients.

The analysis uses proportions rather than only raw counts so that differences in the number of male and female patients do not give a misleading impression.

### Scholarship

The attendance rate was compared between patients with and without a scholarship.

### Hypertension

The appointment attendance of patients with and without hypertension was explored.

### SMS Reminders

The relationship between receiving an SMS reminder and appointment attendance was analyzed.

A difference between the two groups does not necessarily mean that SMS reminders cause patients to attend or miss appointments. Other factors may influence whether a reminder is sent.

### Waiting Time

The difference between the scheduled date and appointment date was calculated as `day_diff`.

The analysis examines whether longer waiting periods are associated with a higher proportion of missed appointments.

### Age

Age distributions were compared to look for patterns between patients who attended and those who missed their appointments.

### Neighbourhood

Appointment attendance was also explored across different neighbourhoods to identify differences between locations.

---

## Key Observations

The exploratory analysis shows that appointment attendance is not identical across all groups.

Some variables show noticeable differences between patients who attended and those who missed their appointments. Waiting time, SMS reminder status, demographic characteristics, and location were among the factors explored.

However, these observations represent associations in the dataset. They should not be interpreted as proof that a particular factor directly causes a patient to miss an appointment.

---

## Classification Model

A **Logistic Regression** model was developed to predict whether a patient is likely to miss a medical appointment.

The model uses patient information and appointment-related features to classify each record into two classes:

* `0` → Show
* `1` → No-show

### Features Used

The model uses the following features:

**Numerical features:**

* Age
* Waiting time (`day_diff`)

**Binary features:**

* Scholarship
* Hypertension
* Diabetes
* Alcoholism
* Handicap
* SMS received

**Categorical features:**

* Gender
* Neighbourhood

The original attendance variable was converted to `no_show` so that the model specifically focuses on identifying patients who may miss their appointments.

---

## Model Preparation

Before training the model:

* Invalid records with negative age or waiting time were removed.
* The dataset was divided into training and testing sets.
* 80% of the data was used for training.
* 20% of the data was used for testing.
* Stratified splitting was used to maintain the proportion of show and no-show cases.
* Numerical features were standardized using `StandardScaler`.
* Categorical features were converted into numerical form using `OneHotEncoder`.
* Binary features were passed through without additional encoding.

A machine-learning pipeline was used to combine preprocessing and Logistic Regression into one workflow.

Because no-show cases represent a smaller class in the dataset, `class_weight='balanced'` was used to give additional importance to the no-show class.

---

## Model Evaluation

The trained Logistic Regression model was evaluated on the test dataset.

The following evaluation methods were used:

### Classification Report

The classification report provides:

* Precision
* Recall
* F1-score
* Support

These metrics help evaluate how well the model identifies both patients who attend and patients who miss their appointments.

### Confusion Matrix

The confusion matrix shows the number of:

* Correctly predicted show cases
* Incorrectly predicted no-show cases
* Incorrectly predicted show cases
* Correctly predicted no-show cases

This helps understand where the model makes correct and incorrect predictions.

### ROC AUC

ROC AUC was used to measure how well the model distinguishes between patients who attend and patients who miss their appointments.

A higher ROC AUC indicates better separation between the two classes.

### ROC Curve

A ROC curve was also generated to visualize the classification performance of the model across different probability thresholds.

---

## Cross-Validation

Five-fold stratified cross-validation was performed to check whether the model's performance remains reasonably consistent across different subsets of the dataset.

`StratifiedKFold` was used so that each fold maintains a similar distribution of show and no-show cases.

ROC AUC was calculated for each fold, followed by the mean ROC AUC.

This provides an additional check on the stability of the model rather than relying only on one train-test split.

---

## Model Interpretation

The Logistic Regression coefficients were converted into **odds ratios** to make the model easier to interpret.

The odds ratio helps show how each feature is associated with the odds of a patient being classified as a no-show.

* Odds ratio greater than `1` → higher odds of no-show.
* Odds ratio less than `1` → lower odds of no-show.
* Odds ratio close to `1` → smaller change in the odds.

A bar chart was created to visualize the odds ratios for the main features.

These values represent associations learned by the model and should not be interpreted as proof of direct causation.

---

## Prediction for a New Patient

The trained model can also be used to estimate the probability that a new patient will miss an appointment.

For example, information such as:

* Age
* Waiting time
* Scholarship status
* Hypertension
* Diabetes
* Alcoholism
* Handicap
* SMS received
* Gender
* Neighbourhood

can be provided as input.

The model then produces a probability of no-show.

For example:

Probability of no-show: 0.67

---

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* Jupyter Notebook

---


## Project Workflow

```text
Dataset
   ↓
Data Inspection
   ↓
Data Cleaning
   ↓
Date Processing
   ↓
Feature Creation
   ↓
Exploratory Data Analysis
   ↓
Visualization
   ↓
Key Observations
   ↓
Prepare Data for Modelling
   ↓
Logistic Regression Model
   ↓
Model Evaluation
   ↓
Cross-Validation
   ↓
Model Interpretation
   ↓
New Patient Prediction
```
---
## Conclusion

This project provided an opportunity to work with a real-world healthcare dataset and apply a complete data analysis and machine-learning workflow.

The analysis involved understanding the dataset, cleaning the data, creating useful features, visualizing appointment attendance, and investigating relationships between patient characteristics and missed appointments.

A Logistic Regression classification model was developed to predict whether a patient is likely to miss an appointment. The model was evaluated using a classification report, confusion matrix, ROC AUC, ROC curve, and five-fold cross-validation.

The model was also interpreted using odds ratios to understand how different features are associated with the odds of a patient being classified as a no-show.

Finally, the trained model can be used to estimate the probability of a no-show for a new patient based on their demographic, health, and appointment-related information.


