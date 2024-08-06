Exploratory Data Analysis (EDA) - Part 4
====================
**Written by: Syed Muhammad Awais Raza**  
[LinkedIn](https://www.linkedin.com/in/syed-muhammad-awais-raza-905317278/) | [Email](mailto:awaisraza5424@gmail.com) | [GitHub](https://github.com/awai1s)

## Feature Scaling, Normalization and Encoding 

***Table of Contents***
------------------------------------------

- [Exploratory Data Analysis (EDA) - Part 4](#exploratory-data-analysis-eda---part-4)
  - [Feature Scaling, Normalization and Encoding](#feature-scaling-normalization-and-encoding)
  - [***Table of Contents***](#table-of-contents)
  - [Overview](#overview)
  - [Data Pre-processing](#data-pre-processing)
  - [Feature Scaling](#feature-scaling)
    - [Why is Feature Scaling Important?](#why-is-feature-scaling-important)
    - [Features and Labels](#features-and-labels)
    - [Types of Feature Scaling Methods](#types-of-feature-scaling-methods)
      - [1. Min-Max Scaling](#1-min-max-scaling)
      - [2. Standard Scaling (Z-score Normalization)](#2-standard-scaling-z-score-normalization)
      - [3. Robust Scaling](#3-robust-scaling)
      - [4. Logarithmic Scaling](#4-logarithmic-scaling)
  - [Normalization](#normalization)
    - [1. **Normalization in Data Preprocessing:**](#1-normalization-in-data-preprocessing)
    - [2. **Normalization in Plotting:**](#2-normalization-in-plotting)
  - [Normalization vs. Scaling](#normalization-vs-scaling)
  - [Feature Encoding](#feature-encoding)
    - [Types of Feature Encoding Methods](#types-of-feature-encoding-methods)
      - [1. One-Hot Encoding](#1-one-hot-encoding)
      - [2. Label Encoding](#2-label-encoding)
      - [3. Ordinal Encoding](#3-ordinal-encoding)

---


## Overview

Feature scaling and encoding are crucial steps in data preprocessing. They ensure that your machine learning models work efficiently by transforming features into a format that algorithms can effectively process.

- **Feature Scaling**: Used for numerical variables to standardize or normalize the values.
- **Feature Encoding**: Used for categorical variables to convert them into numerical format.

## Data Pre-processing

Data pre-processing involves:
- **Detecting anomalies and outliers**
- **Understanding the structure of data**
- **Removing special characters**
- **Handling missing values**

## Feature Scaling

Feature scaling adjusts the range of numerical features to ensure that they contribute equally to the model. This prevents features with larger values from dominating those with smaller values.

### Why is Feature Scaling Important?

Feature scaling is essential because it helps:
- Algorithms converge faster
- Models perform better, especially for models like linear regression, logistic regression, and support vector machines

### Features and Labels

- **Features (X)**: Independent variables or predictors
- **Labels (y)**: Dependent variables or outcomes

### Types of Feature Scaling Methods

1. **Min-Max Scaling**
2. **Standard Scaling (Z-score Normalization)**
3. **Robust Scaling**
4. **Logarithmic Scaling**

#### 1. Min-Max Scaling

**Explanation**: Transforms the values to a range between 0 and 1.

**Python Code:**

```python
import pandas as pd
from sklearn.preprocessing import MinMaxScaler

# Sample data
data = {'values': [10, 20, 30, 40, 50]}
df = pd.DataFrame(data)

# Min-Max Scaling
scaler = MinMaxScaler()
df['values_scaled'] = scaler.fit_transform(df[['values']])
print(df)
```

#### 2. Standard Scaling (Z-score Normalization)

**Explanation**: Centers the data around 0 with a standard deviation of 1. Values typically range from -3 to 3.

**Python Code:**

```python
import pandas as pd
from sklearn.preprocessing import StandardScaler

# Sample data
data = {'values': [10, 20, 30, 40, 50]}
df = pd.DataFrame(data)

# Standard Scaling
scaler = StandardScaler()
df['values_scaled'] = scaler.fit_transform(df[['values']])
print(df)
```

#### 3. Robust Scaling

**Explanation**: Uses median and interquartile range (IQR) to scale, making it robust to outliers.

**Python Code:**

```python
import pandas as pd
from sklearn.preprocessing import RobustScaler

# Sample data
data = {'values': [10, 20, 30, 40, 50]}
df = pd.DataFrame(data)

# Robust Scaling
scaler = RobustScaler()
df['values_scaled'] = scaler.fit_transform(df[['values']])
print(df)
```

#### 4. Logarithmic Scaling


**Explanation**: Applies logarithm to transform skewed distributions.

**Python Code:**

```python
import numpy as np
import pandas as pd

# Sample data
data = {'values': [100000, 200000, 3000000, 4000000, 5000000]}
df = pd.DataFrame(data)

# Logarithmic Scaling
df['values_log'] = np.log(df['values'])
df['values_log2'] = np.log2(df['values'])
df['values_log10'] = np.log10(df['values'])
print(df)
```
## Normalization 
In data science, **normalization** often refers to adjusting the values of numerical features so that they fit within a common range or distribution, typically between 0 and 1. This process is crucial in ensuring that different features contribute equally to the analysis or model. 

However, the term "normalization" can have different meanings in different contexts:

### 1. **Normalization in Data Preprocessing:**
   - **Purpose**: Adjusts feature values to a common scale, typically between 0 and 1, to improve model performance and convergence.
   - **Example**: Min-Max Scaling is a common method of normalization in data preprocessing.

### 2. **Normalization in Plotting:**
   - **Purpose**: Refers to adjusting data points in a plot to make them comparable or to improve visual clarity.
   - **Example**: Scaling the y-axis of a plot to fit within a specific range for better visualization or comparison.

In the context of data preprocessing, normalization typically means transforming numerical data. In plotting and visualization, normalization refers to adjusting the scale of plots for better readability and comparison.


- **Feature Normalization**: Adjusts data values to fit within a specific range (e.g., 0 to 1).
- **Plot Normalization**: Adjusts the scale of plots to ensure that data points are presented clearly and comparably.



## Normalization vs. Scaling

**Normalization** refers to the process of adjusting the values in a dataset to a common scale, often between 0 and 1. **Scaling**, on the other hand, involves transforming numerical features to a specific range or distribution, such as standardizing to have a mean of 0 and a standard deviation of 1.

- **Normalization**: Typically used to ensure that all features have a common scale, often [0, 1].
- **Scaling**: Encompasses various methods (e.g., min-max, standard scaling) to adjust the distribution of features.

In summary, normalization and scaling are both vital in preprocessing to ensure that all features contribute equally to the learning algorithm and to improve model performance.

---


## Feature Encoding

Feature encoding is the process of converting categorical variables into numerical format so that machine learning algorithms can interpret them.

### Types of Feature Encoding Methods

1. **One-Hot Encoding**
2. **Label Encoding**
3. **Ordinal Encoding**

#### 1. One-Hot Encoding

**Explanation**: Converts categorical variables into binary vectors. Each category is represented by a single "hot" (1) value.

**Python Code:**

```python
import pandas as pd

# Sample data
data = {'Color': ['Red', 'Green', 'Blue', 'Red']}
df = pd.DataFrame(data)

# One-Hot Encoding
encoded_data = pd.get_dummies(df, columns=['Color'])
print(encoded_data)
```

#### 2. Label Encoding

**Explanation**: Converts each category to a unique integer. Suitable for categorical variables with an inherent order.

**Python Code:**

```python
from sklearn.preprocessing import LabelEncoder
import pandas as pd

# Sample data
data = {'Animal': ['Dog', 'Cat', 'Bird', 'Dog', 'Bird']}
df = pd.DataFrame(data)

# Label Encoding
label_encoder = LabelEncoder()
df['Animal_encoded'] = label_encoder.fit_transform(df['Animal'])
print(df)
```

#### 3. Ordinal Encoding

**Explanation**: Assigns a unique integer to each category based on a predefined order.

**Python Code:**

```python
from sklearn.preprocessing import OrdinalEncoder
import pandas as pd

# Sample data
data = {'Size': ['Small', 'Medium', 'Large', 'Medium']}
df = pd.DataFrame(data)

# Ordinal Encoding
ordinal_encoder = OrdinalEncoder(categories=[['Small', 'Medium', 'Large']])
df['Size_encoded'] = ordinal_encoder.fit_transform(df[['Size']])
print(df)
```


