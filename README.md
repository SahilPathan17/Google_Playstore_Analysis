# Google_Playstore_Analysis


<br>
<p>


This project aims to analyze data from the Google Playstore to uncover patterns and insights about various applications. The analysis involves cleaning and processing the data, handling missing values, and performing exploratory data analysis (EDA).

---

## Project Overview

The Google Playstore Analysis project involves several key steps:

1. **Data Loading and Initial Exploration**:
    - The dataset is loaded using `pandas` and the first few rows are displayed to understand its structure.
    - Duplicate entries are identified and removed to ensure data quality.

2. **Handling Missing Values**:
    - The dataset is checked for missing values, and appropriate measures are taken to handle them. For instance, the `Rating`, `Type`, and `Current Ver` columns' missing values are filled with their respective mode values.

3. **Data Cleaning and Transformation**:
    - The `Reviews` and `Installs` columns are converted to numeric values, handling non-numeric entries with the `errors='coerce'` parameter to avoid errors during conversion.
    - The `Price` column is cleaned by removing the dollar sign and converting it to a float.
    - The `Current Ver` and `Android Ver` columns are stripped of any leading or trailing whitespace and converted to numeric values where applicable.

4. **Exploratory Data Analysis (EDA)**:
    - Visualizations are created using `matplotlib` and `seaborn` to understand the distribution of ratings and the relationship between ratings and app categories.
    - Count plots and bar plots provide insights into which categories have the highest ratings and how ratings are distributed across different categories.

## Code Breakdown

### Data Loading and Initial Cleaning
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('/content/googleplaystore.csv')
df.drop_duplicates(inplace=True)
```

### Handling Missing Values
```python
df['Rating'].fillna(df['Rating'].mode()[0], inplace=True)
df['Type'].fillna(df['Type'].mode()[0], inplace=True)
df['Current Ver'].fillna(df['Current Ver'].mode()[0], inplace=True)
```

### Data Transformation
```python
df['Reviews'] = pd.to_numeric(df['Reviews'], errors="coerce")
df['Installs'] = df['Installs'].str.replace(',', '').str.replace('+', '').astype(float)
df['Price'] = df['Price'].str.replace("$", "").astype(float)
df['Current Ver'] = pd.to_numeric(df['Current Ver'].str.strip(), errors='coerce')
df['Android Ver'] = pd.to_numeric(df['Android Ver'].str.strip(), errors='coerce')
```

### Exploratory Data Analysis
```python
plt.figure(figsize=(10, 10))
sns.countplot(x=df.Rating)

plt.figure(figsize=(10, 10))
sns.barplot(x=df.Rating, y=df.Category)
```

## Conclusion

This analysis of the Google Playstore dataset provides insights into how various factors like reviews, installs, price, and app versions correlate with app ratings. The visualizations help identify patterns and trends that can be useful for developers and marketers to optimize their apps.

## Future Work

- Further analysis can be conducted to understand the impact of other factors such as app size and content rating.
- Machine learning models can be developed to predict app ratings based on the features available in the dataset.

---

</p>
