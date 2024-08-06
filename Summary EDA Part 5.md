# Exploratory Data Analysis (EDA) - Summary

**Written by: Syed Muhammad Awais Raza**  
[LinkedIn](https://www.linkedin.com/in/syed-muhammad-awais-raza-905317278/) |  [Email](mailto:awaisraza5424@gmail.com) | [GitHub](https://github.com/awai1s)

---

## Table of Contents
1. [Introduction](#introduction)
2. [Basics of Pandas](#basics-of-pandas)
3. [Handling Missing Values](#handling-missing-values)
4. [Detecting and Handling Outliers](#detecting-and-handling-outliers)
5. [Feature Scaling](#feature-scaling)
6. [Feature Encoding](#feature-encoding)

---

## Introduction

Exploratory Data Analysis (EDA) is the process of analyzing datasets to summarize their main characteristics, often using visual methods. It is a crucial step in data preprocessing and helps in understanding the data, identifying patterns, and preparing it for modeling. This guide will cover the basics of Pandas, handling missing values, detecting and handling outliers, feature scaling, and feature encoding.

---

## Basics of Pandas

Pandas is a powerful Python library used for data manipulation and analysis. It provides data structures and functions needed to manipulate structured data seamlessly.

### Key Concepts
- **DataFrame**: A 2-dimensional labeled data structure with columns of potentially different types.
- **Series**: A 1-dimensional labeled array capable of holding any data type.

### Example
```python
import pandas as pd

# Creating a DataFrame
data = {'Name': ['John', 'Anna', 'Peter', 'Linda'],
        'Age': [28, 24, 35, 32],
        'City': ['New York', 'Paris', 'Berlin', 'London']}
df = pd.DataFrame(data)
print(df)
```

---

## Handling Missing Values

Missing values can significantly affect the performance of a model. Pandas provides several methods to handle missing data.

### Methods to Handle Missing Values
1. **Drop missing values**
2. **Fill missing values**

### Example
```python
# Drop missing values
df.dropna()

# Fill missing values with a specific value
df.fillna(0)

# Fill missing values with the mean of the column
df['Age'].fillna(df['Age'].mean(), inplace=True)
```

---

## Detecting and Handling Outliers

Outliers can skew and mislead the training process of machine learning algorithms. Identifying and handling outliers is crucial for accurate data analysis.

### Methods to Detect Outliers
1. **Box Plot**
2. **Z-Score**
3. **IQR (Interquartile Range)**

### Example
```python
import numpy as np
import matplotlib.pyplot as plt

# Box Plot
plt.boxplot(df['Age'])
plt.show()

# Z-Score
df['zscore'] = (df['Age'] - df['Age'].mean()) / df['Age'].std()
outliers = df[df['zscore'].abs() > 3]

# IQR
Q1 = df['Age'].quantile(0.25)
Q3 = df['Age'].quantile(0.75)
IQR = Q3 - Q1
outliers = df[(df['Age'] < (Q1 - 1.5 * IQR)) | (df['Age'] > (Q3 + 1.5 * IQR))]
```

---

## Feature Scaling

Feature scaling is used to normalize the range of independent variables or features of data. It ensures that the algorithm works efficiently and correctly.

### Methods of Feature Scaling
1. **Min-Max Scaling**
2. **Standard Scaling (Z-score Normalization)**
3. **Robust Scaling**
4. **Logarithmic Scaling**

### Example
```python
from sklearn.preprocessing import MinMaxScaler, StandardScaler, RobustScaler
import numpy as np

# Min-Max Scaling
scaler = MinMaxScaler()
df['Age_MinMax'] = scaler.fit_transform(df[['Age']])

# Standard Scaling
scaler = StandardScaler()
df['Age_Standard'] = scaler.fit_transform(df[['Age']])

# Robust Scaling
scaler = RobustScaler()
df['Age_Robust'] = scaler.fit_transform(df[['Age']])
```

---

## Feature Encoding

Feature encoding is used to convert categorical variables into numerical values so that machine learning algorithms can process them.

### Methods of Feature Encoding
1. **One-Hot Encoding**
2. **Label Encoding**
3. **Ordinal Encoding**

### Example
```python
# One-Hot Encoding
df = pd.get_dummies(df, columns=['City'])

# Label Encoding
from sklearn.preprocessing import LabelEncoder
encoder = LabelEncoder()
df['Name_encoded'] = encoder.fit_transform(df['Name'])

# Ordinal Encoding
from sklearn.preprocessing import OrdinalEncoder
ordinal_encoder = OrdinalEncoder()
df['City_ordinal'] = ordinal_encoder.fit_transform(df[['City']])
```

---
]