Exploratory Data Analysis (EDA) - Part 3
====================
**Written by: Syed Muhammad Awais Raza**  
[LinkedIn](https://www.linkedin.com/in/syed-muhammad-awais-raza-905317278/) | [Email](mailto:awaisraza5424@gmail.com) | [GitHub](https://github.com/awai1s)
## Exploring Pandas Library and Handling Outliers in Data

***Table of Contents***
------------------------------------------

- [Exploratory Data Analysis (EDA) - Part 3](#exploratory-data-analysis-eda---part-3)
  - [Exploring Pandas Library and Handling Outliers in Data](#exploring-pandas-library-and-handling-outliers-in-data)
  - [***Table of Contents***](#table-of-contents)
  - [What are Outliers?](#what-are-outliers)
  - [Characteristics of Outliers](#characteristics-of-outliers)
  - [Main Types of Outliers](#main-types-of-outliers)
    - [1. Global Variable Outliers](#1-global-variable-outliers)
    - [2. Contextual Outliers](#2-contextual-outliers)
    - [3. Collective Outliers](#3-collective-outliers)
  - [Other Types of Outliers](#other-types-of-outliers)
    - [a. Univariate Outliers](#a-univariate-outliers)
    - [b. Multivariate Outliers](#b-multivariate-outliers)
  - [Identifying Outliers](#identifying-outliers)
    - [1. Visual Methods](#1-visual-methods)
    - [2. IQR (Interquartile Range) Method](#2-iqr-interquartile-range-method)
    - [3. Z-Score Method](#3-z-score-method)
  - [Handling Outliers](#handling-outliers)
    - [1. Remove Them](#1-remove-them)
    - [2. Transform Them](#2-transform-them)
    - [3. Impute Them](#3-impute-them)
  - [Importance of Handling Outliers](#importance-of-handling-outliers)

---
## What are Outliers?

Outliers are data points that significantly differ from other `data points` in a dataset. They can be unusually high or low compared to the majority of the data. Outliers can arise due to various reasons such as measurement errors, data entry mistakes, natural variability, or genuine extreme values.
## Characteristics of Outliers
Unusual values: Outliers are values that are far away from the mean or median of the dataset.
Inconsistent with the rest of the data: Outliers do not follow the same pattern or trend as the rest of the data.
Can affect statistical analysis: Outliers can significantly impact the results of statistical analysis, such as skewing the mean or affecting the accuracy of predictions.
## Main Types of Outliers

Outliers can be categorized based on their nature and the context in which they appear. Understanding these types helps in accurate identification and handling.

### 1. Global Variable Outliers

Global variable outliers are data points that fall outside the expected range of values for a given dataset. These outliers are identified based on the overall distribution of the data.

**Example:**

If a city’s temperature range is expected to be between 2°C and 40°C, a temperature reading of 100°C would be considered a global variable outlier, as it is far outside the plausible range for that location.

### 2. Contextual Outliers

Contextual outliers are values that are unusual within a specific subset or context of the data. They are identified based on the local patterns or constraints of the dataset.

**Example:**

In a dataset where the temperature typically ranges from 2°C to 35°C, a temperature of 40°C could be a contextual outlier. Although it is not globally extreme, it deviates from the expected range for that particular context.

### 3. Collective Outliers

Collective outliers occur when a group of data points deviates significantly from the norm. This type often results from issues in data collection or sampling.

**Example:**

If data is collected from one person who provides unusual responses, it might affect the nearby values in the dataset, causing them to be considered outliers as well. Identifying these requires understanding the data collection process and sources.

## Other Types of Outliers

Outliers can also be classified based on the number of variables they affect:

### a. Univariate Outliers

Univariate outliers are identified by analyzing a single variable within the dataset. These outliers are detected by examining the distribution of that variable alone.

**Example:**
```python
import pandas as pd

# Example DataFrame
data = {'age': [25, 30, 28, 29, 100]}
df = pd.DataFrame(data)

# Summary statistics
print(df['age'].describe())
```

### b. Multivariate Outliers

Multivariate outliers are identified by considering multiple variables simultaneously. These outliers are detected by examining relationships between variables.

**Example:**
```python
# Example DataFrame
data = {'age': [25, 30, 28, 29, 100], 'height': [150, 160, 155, 158, 200]}
df = pd.DataFrame(data)

# Summary statistics
print(df.describe())
```

## Identifying Outliers

Several methods can be used to identify outliers in a dataset. Each method has its strengths and is suitable for different types of data.

### 1. Visual Methods

Visual methods involve plotting the data to visually detect outliers. Common plots include:

- **Boxplots**: Show the distribution of data and highlight outliers as points beyond the "whiskers."
- **Histograms**: Display the frequency distribution and help identify unusual spikes or gaps.
- **Scatter Plots**: Useful for identifying outliers in bivariate data, where outliers may appear as points distant from the general pattern.

**Example with Boxplot:**
```python
import seaborn as sns
import matplotlib.pyplot as plt

# Example DataFrame
data = {'age': [25, 30, 28, 29, 100]}
df = pd.DataFrame(data)

# Boxplot
sns.boxplot(x=df['age'])
plt.show()
```

### 2. IQR (Interquartile Range) Method

The IQR method calculates the range between the first quartile (Q1) and the third quartile (Q3) of the data. Outliers are defined as values falling outside 1.5 times the IQR above Q3 or below Q1.

**Steps to Identify Outliers:**

1. **Calculate Q1 and Q3**: Determine the first and third quartiles.
2. **Compute IQR**: Calculate the difference between Q3 and Q1.
3. **Define Outlier Thresholds**:
   - **Upper Bound**: Q3 + 1.5 * IQR
   - **Lower Bound**: Q1 - 1.5 * IQR
4. **Identify Outliers**: Values outside these bounds are considered outliers.

**Example:**
```python
# Calculate the IQR for the 'age' column
Q1 = df['age'].quantile(0.25)
Q3 = df['age'].quantile(0.75)
IQR = Q3 - Q1

# Define bounds for the outliers
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

# Identify outliers
outliers = df[(df['age'] < lower_bound) | (df['age'] > upper_bound)]
print(outliers)
```

### 3. Z-Score Method

The Z-score method calculates how many standard deviations away from the mean a data point is. Typically, Z-scores beyond ±3 are considered outliers.

**Z-Score Interpretation:**
- **Z = 0**: No deviation.
- **Z = ±1**: Slight deviation.
- **Z = ±2**: Moderate deviation.
- **Z = ±3**: Extreme deviation.

**Example:**
```python
from scipy import stats

# Calculate Z-scores
df['z_score'] = stats.zscore(df['age'])

# Identify outliers
outliers = df[(df['z_score'] < -3) | (df['z_score'] > 3)]
print(outliers)
```

## Handling Outliers

Once outliers are identified, various strategies can be applied to handle them effectively.

### 1. Remove Them

Removing outliers involves filtering the data to exclude values that fall outside the defined bounds. This method simplifies data analysis and model training.

**Example:**
```python
# Remove outliers based on IQR
df_no_outliers = df[(df['age'] >= lower_bound) & (df['age'] <= upper_bound)]
print(df_no_outliers)
```

### 2. Transform Them

Transformations can be applied to reduce the impact of outliers. Common transformations include logarithmic transformations, square root transformations, and Box-Cox transformations.

**Example of Log Transformation:**
```python
import numpy as np

# Apply log transformation
df['age_log'] = np.log(df['age'] + 1)  # Adding 1 to avoid log(0)
print(df)
```

### 3. Impute Them

Imputation involves replacing outliers with statistical measures like the mean or median. This approach maintains the dataset size while reducing the impact of outliers.

**Example of Imputation with Median:**
```python
# Impute outliers with the median
median_age = df['age'].median()
df_imputed = df.copy()
df_imputed.loc[df['age'] > upper_bound, 'age'] = median_age
print(df_imputed)
```

## Importance of Handling Outliers

Handling outliers is crucial for several reasons:

1. **Data Accuracy**: Outliers can skew statistical analyses and affect measures like mean, variance, and correlation. By handling them, you ensure that these statistics more accurately reflect the dataset.

2. **Model Performance**: Many machine learning algorithms are sensitive to outliers, which can lead to overfitting or poor model performance. Addressing outliers helps in building more robust and reliable models.

3. **Data Integrity**: Outliers might indicate errors or anomalies in data collection. Identifying and addressing these helps maintain the integrity and quality of the dataset.

4. **Improved Insights**: Properly managing outliers ensures that the insights and conclusions drawn from the data are valid and meaningful.

5. **Compliance and Standards**: In some industries, managing outliers is necessary to comply with regulatory standards and ensure the validity of analyses used for decision-making.