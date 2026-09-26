# Medical Appointment Data Analysis

## Project Overview

This project analyzes a medical appointment dataset to understand the factors associated with patients attending or missing their scheduled appointments.

The dataset contains information about patients such as age, gender, health conditions, scholarship status, SMS reminders, appointment dates, scheduling dates, and neighbourhood.

The main purpose of this project is to clean the data, explore different patterns through visualizations, and identify factors that may be related to appointment attendance.

---

## Objectives

The main objectives of this project are:

* Understand the structure and characteristics of the dataset.
* Clean and prepare the data for analysis.
* Analyze the overall appointment attendance rate.
* Explore the relationship between patient characteristics and attendance.
* Analyze the effect of SMS reminders on appointment attendance.
* Study the relationship between waiting time and missed appointments.
* Compare appointment attendance across different groups and neighbourhoods.
* Prepare the dataset for a future classification model.

---

## Dataset

The dataset contains information about medical appointments and whether patients attended their scheduled appointments.

Some important attributes include:

| Column         | Description                                      |
| -------------- | ------------------------------------------------ |
| Gender         | Gender of the patient                            |
| Age            | Age of the patient                               |
| Hypertension   | Whether the patient has hypertension             |
| Diabetes       | Whether the patient has diabetes                 |
| Scholarship    | Whether the patient received a scholarship       |
| SMS_received   | Whether the patient received an SMS reminder     |
| ScheduledDay   | Date and time when the appointment was scheduled |
| AppointmentDay | Date of the actual appointment                   |
| Neighbourhood  | Location of the appointment                      |
| No-show        | Original appointment attendance status           |

A new `show` variable was created during preprocessing to make the target easier to work with:

* `1` → Patient attended the appointment
* `0` → Patient did not attend the appointment

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

For calculating the waiting period, the date portions were compared rather than the time components so that same-day appointments were not incorrectly assigned a negative value.

---

## Exploratory Data Analysis

The analysis focuses on the following areas:

### Overall Appointment Attendance

The overall proportion of patients who attended and missed their appointments was calculated to understand the distribution of the target variable.

### Gender

The percentage of females missing their appointment is nearly two times the number of males. So females are more likely to miss their appointment.

### Scholarship

It seems that patients with scholarships are actually more likely to miss their appointment

### Hypertension

It seems that patients with hypertension are actually more likely to show up for their appointment.

### SMS Reminders

A strange finding here suggests that patients who received an SMS are more likely to miss their appointment.

### Waiting Time

It appears that the longer the period between the scheduling and appointment the more likely the patient won't show up.

### Age

There is no clear relation between the age and whether the patient shows up or not but younger patients are more likely to miss their appointments.

### Neighbourhood

Appointment attendance was also explored across different neighbourhoods to identify differences between locations.

---

## Key Observations

The exploratory analysis shows that appointment attendance is not identical across all groups.

Some variables show noticeable differences between patients who attended and those who missed their appointments. Waiting time, SMS reminder status, demographic characteristics, and location were among the factors explored.

However, these observations represent associations in the dataset. They should not be interpreted as proof that a particular factor directly causes a patient to miss an appointment.

---

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
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
Classification Model
   ↓
Appointment Prediction
```

---

## Future Scope

The next stage of this project is to build a classification model using the cleaned dataset.

A Logistic Regression model can be used to predict whether a patient is likely to attend or miss an appointment based on features such as:

* Gender
* Age
* Hypertension
* Diabetes
* Scholarship
* SMS received
* Waiting days

The model can then be evaluated using:

* Accuracy
* Precision
* Recall
* F1-score
* Confusion Matrix

An interactive input section can also be added so that a user can enter patient information and receive a predicted appointment outcome.

---

## Project Structure

```text
Medical-Appointment-Data-Analysis/
│
├── data/
│   └── noshowappointment.csv
│
├── notebooks/
│   └── Medical_Appointment_Data_Analysis.ipynb
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Conclusion

This project provided an opportunity to work with a real-world healthcare dataset and apply the complete exploratory data analysis workflow.

The analysis involved understanding the dataset, cleaning the data, creating useful features, visualizing appointment attendance, and investigating relationships between patient characteristics and missed appointments.

The cleaned dataset can now be used for the next phase of the project: developing a classification model to predict appointment attendance.
