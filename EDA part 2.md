Exploratory Data Analysis (EDA) - Part 2
====================
**Written by: Syed Muhammad Awais Raza**  
[LinkedIn](https://www.linkedin.com/in/syed-muhammad-awais-raza-905317278/) | [Email](mailto:awaisraza5424@gmail.com) | [GitHub](https://github.com/awai1s)
## Exploring Pandas Library and Handling missing values
***Table of Contents***
- [Exploratory Data Analysis (EDA) - Part 2](#exploratory-data-analysis-eda---part-2)
  - [Exploring Pandas Library and Handling missing values](#exploring-pandas-library-and-handling-missing-values)
    - [Basic Functions of Pandas for Exploring Data](#basic-functions-of-pandas-for-exploring-data)
      - [1. Loading Data](#1-loading-data)
        - [Example: Reading a CSV File](#example-reading-a-csv-file)
      - [2. Viewing Data](#2-viewing-data)
        - [`head()`](#head)
        - [`tail()`](#tail)
        - [`sample()`](#sample)
      - [3. DataFrame Information](#3-dataframe-information)
        - [`info()`](#info)
        - [`describe()`](#describe)
        - [`shape`](#shape)
        - [`columns`](#columns)
      - [4. Data Selection](#4-data-selection)
        - [Selecting Columns](#selecting-columns)
        - [Selecting Rows](#selecting-rows)
          - [Using Index](#using-index)
          - [Using Conditions](#using-conditions)
        - [Selecting Specific Rows and Columns](#selecting-specific-rows-and-columns)
    - [What are Missing Values?](#what-are-missing-values)
    - [Nicknames for Missing Values](#nicknames-for-missing-values)
    - [Why Is Handling Missing Values Important?](#why-is-handling-missing-values-important)
    - [Deciding Whether to Remove a Column with Missing Values](#deciding-whether-to-remove-a-column-with-missing-values)
    - [Detailed Methods for Handling Missing Values](#detailed-methods-for-handling-missing-values)
      - [1. Re-acquire Data from the Source\*\*](#1-re-acquire-data-from-the-source)
      - [2. Remove Rows with Missing Values](#2-remove-rows-with-missing-values)
      - [3. Remove Columns with Missing Values](#3-remove-columns-with-missing-values)
      - [4. Fill Missing Values with a Specific Value](#4-fill-missing-values-with-a-specific-value)
      - [5. Fill Missing Values with Mean, Median, or Mode](#5-fill-missing-values-with-mean-median-or-mode)
      - [6. Forward Fill (Fill with Previous Value)](#6-forward-fill-fill-with-previous-value)
      - [7. Backward Fill (Fill with Next Value)](#7-backward-fill-fill-with-next-value)
      - [8. Interpolation](#8-interpolation)
      - [9. Using K-Nearest Neighbors (KNN) Imputation](#9-using-k-nearest-neighbors-knn-imputation)
      - [10. Drop Columns with a High Percentage of Missing Values](#10-drop-columns-with-a-high-percentage-of-missing-values)
    - [Consequences of Not Handling Missing Values](#consequences-of-not-handling-missing-values)
### Basic Functions of Pandas for Exploring Data

Pandas is a powerful library in Python for data manipulation and analysis. Here are some fundamental functions to help you explore and understand your data.

#### 1. Loading Data

Before you can explore data, you need to load it into a DataFrame. Pandas provides functions to read data from various file formats.

##### Example: Reading a CSV File
```python
import pandas as pd

# Load data from a CSV file
df = pd.read_csv('data.csv')
print(df.head())
```

#### 2. Viewing Data

Once your data is loaded, you can view it using various functions to get an overview.

##### `head()`

Displays the first few rows of the DataFrame.

```python
# Display the first 5 rows
print(df.head())
```

##### `tail()`

Displays the last few rows of the DataFrame.

```python
# Display the last 5 rows
print(df.tail())
```

##### `sample()`

Returns a random sample of rows from the DataFrame.

```python
# Sample 3 random rows
print(df.sample(3))
```

#### 3. DataFrame Information

To get an overview of the DataFrame structure and data types, use the following methods.

##### `info()`

Provides a concise summary of the DataFrame including the index dtype, columns, non-null values, and memory usage.

```python
# Get a summary of the DataFrame
print(df.info())
```

##### `describe()`

Generates descriptive statistics of the numerical columns, such as count, mean, standard deviation, min, and max.

```python
# Get descriptive statistics
print(df.describe())
```

##### `shape`

Returns the dimensions of the DataFrame (number of rows and columns).

```python
# Get the dimensions of the DataFrame
print(df.shape)
```

##### `columns`

Lists the column names of the DataFrame.

```python
# List the column names
print(df.columns)
```

#### 4. Data Selection

You can select and filter data in various ways.

##### Selecting Columns

You can select one or more columns by their names.

```python
# Select a single column
print(df['column_name'])

# Select multiple columns
print(df[['column1', 'column2']])
```

##### Selecting Rows

You can select rows based on their index or conditions.

###### Using Index

```python
# Select the row at index 2
print(df.iloc[2])
```

###### Using Conditions

```python
# Select rows where the value in 'column_name' is greater than 50
print(df[df['column_name'] > 50])
```

##### Selecting Specific Rows and Columns

You can select specific rows and columns using `.loc[]` or `.iloc[]`.

```python
# Select specific rows and columns
print(df.loc[0:5, ['column1', 'column2']])
```
### What are Missing Values?

Missing values in a dataset refer to the absence of data for one or more entries. In simpler terms, they are the gaps where data is supposed to be, but isn't. This can happen for various reasons, such as errors in data collection, data corruption, or intentional omissions.
### Nicknames for Missing Values
Missing values also have various names depending on the context and domain. Here are some common terms used in data science and statistics:

- **NA (Not Available)**
- **NaN (Not a Number)**: Commonly used in programming languages like Python (pandas library).
- **Null**: Used in database management systems like SQL.
- **Undefined**
- **Blank or Empty**
- **Placeholder Values**: Default values set to recognize missing data (e.g., -1 or 999 in an age field).
- **Sentinel Values**: Specific values representing certain conditions.
- **Dummy Data**: Used for placeholder or testing purposes.
- **Missing Data**: A common term used in research papers.

Recognizing and handling these different types of missing values is essential during data analysis or preprocessing.

### Why Is Handling Missing Values Important? 

1. **Impact on Model Accuracy**: Missing values can reduce the accuracy and performance of machine learning models.
2. **Data Quality Concerns**: Missing values weaken data quality, leading to incorrect analyses and decisions.
3. **Increased Model Training Time**: Handling missing values can increase model training time, wasting resources and time.

### Deciding Whether to Remove a Column with Missing Values

Consider the following factors:

1. **Quantity of Data**: If a specific column has a high percentage of missing values (e.g., 70% or 80%), it may be better to remove it.
2. **Importance of the Column**: If the column is crucial for your analysis or model, avoid removing it. Instead, consider imputation techniques.
3. **Nature of Data**: Sometimes missing values indicate something (e.g., a survey question left unanswered due to discomfort).
4. **Model Sensitivity**: Some machine learning models can handle missing values, while others cannot.
5. **Type of Data**: Numeric data can be imputed using mean, median, or mode. Categorical data can be imputed using mode or a specific category.

Generally, if a column has more than 50% missing data, consider whether it's better to remove it. However, this isn't a hard and fast rule. Each dataset is unique, and decisions should be made in context.

### Detailed Methods for Handling Missing Values 
Certainly, here are some methods for handling missing values using pandas in Python with code examples:

#### 1. Re-acquire Data from the Source**

If possible, re-acquire the data to fill in missing values. This step is often manual and depends on the data source, so it doesn't have a specific code example.

#### 2. Remove Rows with Missing Values

To remove rows with any missing values:
```python
import pandas as pd

# Sample DataFrame
data = {'A': [1, 2, None, 4], 'B': [5, None, None, 8], 'C': [9, 10, 11, 12]}
df = pd.DataFrame(data)

# Remove rows with any missing values
df_cleaned = df.dropna()
print(df_cleaned)
```

#### 3. Remove Columns with Missing Values

To remove columns with any missing values:
```python
# Remove columns with any missing values
df_cleaned = df.dropna(axis=1)
print(df_cleaned)
```

#### 4. Fill Missing Values with a Specific Value

To fill missing values with a specific value (e.g., 0):
```python
# Fill missing values with 0
df_filled = df.fillna(0)
print(df_filled)
```

#### 5. Fill Missing Values with Mean, Median, or Mode

To fill missing values with the mean:
```python
# Fill missing values with mean of the column
df_filled_mean = df.fillna(df.mean())
print(df_filled_mean)
```

To fill missing values with the median:
```python
# Fill missing values with median of the column
df_filled_median = df.fillna(df.median())
print(df_filled_median)
```

To fill missing values with the mode:
```python
# Fill missing values with mode of the column
df_filled_mode = df.fillna(df.mode().iloc[0])
print(df_filled_mode)
```

#### 6. Forward Fill (Fill with Previous Value)

To fill missing values with the previous value in the column:
```python
# Forward fill
df_filled_ffill = df.ffill()
print(df_filled_ffill)
```

#### 7. Backward Fill (Fill with Next Value)

To fill missing values with the next value in the column:
```python
# Backward fill
df_filled_bfill = df.bfill()
print(df_filled_bfill)
```

#### 8. Interpolation

To fill missing values using interpolation:
```python
# Interpolation
df_interpolated = df.interpolate()
print(df_interpolated)
```

#### 9. Using K-Nearest Neighbors (KNN) Imputation

To fill missing values using KNN imputation (requires `sklearn`):
```python
from sklearn.impute import KNNImputer

# Sample DataFrame with missing values
data = {'A': [1, 2, None, 4], 'B': [5, None, 7, 8], 'C': [9, 10, 11, None]}
df = pd.DataFrame(data)

# Initialize KNN Imputer
imputer = KNNImputer(n_neighbors=2)

# Impute missing values
df_imputed = pd.DataFrame(imputer.fit_transform(df), columns=df.columns)
print(df_imputed)
```

#### 10. Drop Columns with a High Percentage of Missing Values

To drop columns with more than 50% missing values:
```python
# Drop columns with more than 50% missing values
threshold = len(df) * 0.5
df_cleaned = df.dropna(thresh=threshold, axis=1)
print(df_cleaned)
```

These methods and examples cover a range of techniques for handling missing values in pandas. Depending on the context and specific dataset, you might choose one or a combination of these methods.
### Consequences of Not Handling Missing Values 

If we ignore missing values, several issues can arise:

1. **Reduced Model Accuracy**:  Models may perform poorly due to incomplete information.
2. **Incorrect Analysis**:  Leads to wrong conclusions and decisions.
3. **Model Confusion**:  Some models can't handle missing values, leading to training failures or incorrect predictions.
4. **Bias in Model**: Missing values can introduce bias.
5. **Incorrect Data Interpretation**: Leads to incomplete or incorrect data interpretation.
6. **Storage Issues**:  Some systems can't store missing values.
7. **Data Integration Issues**:  Problems integrating data from different sources.
8. **Incorrect Feature Selection**: Important features may be ignored.
9. **Incorrect Experimental Results**: Especially in science or research projects.
10. **Extra Work and Stress**: Data scientists have to put in extra work to identify and handle missing values.



























