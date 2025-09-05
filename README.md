# GTC ML Project 1: Hotel Bookings Analysis & Prediction 🏨✈️

This project involves a comprehensive analysis of a hotel bookings dataset to understand factors influencing booking cancellations and to build a predictive model.

## 📊 Data Loading & Exploration

The project starts with loading the hotel bookings dataset from Kaggle.

*   Used the Kaggle API to download the dataset 📦.
*   Loaded the data into a pandas DataFrame for initial inspection and analysis.

## 🔍 Exploratory Data Analysis (EDA)

A thorough EDA was conducted to understand the dataset's structure, identify missing values, duplicates, and outliers, and explore correlations between features.

*   Applied descriptive statistics (`.info()`, `.describe()`) to summarize the data 📈.
*   Checked dataset shape and unique values.
*   Identified columns with missing values and their percentages 📊.
*   Visualized missing values using `missingno` library matrix and bar plots.
*   Checked for duplicate rows (None found 👍).
*   Visualized correlations between numerical features using a heatmap 🔥.
*   Identified and visualized outliers in various numerical columns using box plots 🎯.

## ⚡ Data Cleaning

Addressed missing values and outliers to prepare the data for modeling.

*   Dropped unnecessary columns (`index`, `reservation_status`, `reservation_status_date`) as they are not useful for prediction.
*   Handled missing values:
    *   Filled `company` and `agent` missing values with a new category 'Unknown' ❓.
    *   Filled `country` and `children` missing values with the mode (most frequent value) to address the small number of missing entries.
*   Handled outliers:
    *   Capped the upper values of `adr` at 1000.
    *   Capped the upper values of `lead_time` at the 99th percentile to reduce the impact of extreme values while retaining most of the data.

## 🏢 Feature Engineering & Preprocessing

Created new features and encoded categorical variables to make the data suitable for machine learning algorithms.

*   Created new features:
    *   `total_guests` = sum of `adults`, `children`, and `babies` 👨‍👩‍👧‍👦.
    *   `total_nights` = sum of `stays_in_weekend_nights` and `stays_in_week_nights` 🌙.
    *   `is_family` = a boolean flag indicating if the booking includes children or babies ❤️.
*   Encoded categorical variables:
    *   Applied **Frequency Encoding** to high-cardinality columns (`country`, `agent`, `company`) to represent categories by their occurrence frequency.
    *   Applied **One-Hot Encoding** using scikit-learn's `OneHotEncoder` to low-cardinality categorical columns (`hotel`, `arrival_date_month`, `meal`, `market_segment`, `distribution_channel`, `reserved_room_type`, `assigned_room_type`, `deposit_type`, `customer_type`) to convert them into a numerical format suitable for modeling.
    *   Converted boolean columns (`is_canceled`, `is_repeated_guest`, `is_family`) to integers (0 or 1).

## ✂️ Data Splitting

Split the cleaned and preprocessed dataset into training and testing sets for model development and evaluation.

*   Defined features (`X`) as all columns except the target variable.
*   Defined the target variable (`y`) as `'is_canceled'`.
*   Used `train_test_split` from scikit-learn to split the data with a test size of 20% and a `random_state` of 42 for reproducibility.
*   Saved the training and testing sets (`X_train`, `X_test`, `y_train`, `y_test`) to separate CSV files for easy loading and use in subsequent modeling steps 💾.

## 🌟 Key Findings & Conclusion

Based on the exploratory data analysis and preprocessing:

*   The dataset provided a good foundation for analyzing hotel booking cancellations.
*   Missing data in `company` and `agent` were significant and required careful handling.
*   Outliers were present in several numerical features, indicating the need for appropriate strategies (capping in this case) to mitigate their impact on modeling.
*   Correlations between features like `previous_cancellations` and `is_canceled`, and negative correlations between `required_car_parking_spaces`, `total_of_special_requests`, and `is_canceled` are important insights for feature selection and model interpretation.
*   Feature engineering created potentially useful new features (`total_guests`, `total_nights`, `is_family`) that capture important aspects of the bookings.
*   The data is now cleaned, preprocessed, and split, ready for training machine learning models to predict hotel booking cancellations. The next steps would involve model selection, training, evaluation, and potentially hyperparameter tuning to build an effective predictive model.

This project provides a solid base for understanding hotel booking patterns and predicting cancellations, which can be valuable for hotel management and revenue optimization.
