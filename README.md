# Task-5
# Titanic Dataset: Exploratory Data Analysis (EDA)

## 🚢 Project Overview

This repository contains an **Exploratory Data Analysis (EDA)** of the **Titanic dataset**, which provides insights into the passengers aboard the ill-fated ship. By analyzing various features such as **age**, **passenger class**, **fare**, and **survival status**, we uncover patterns and relationships that may help us understand the factors contributing to survival aboard the Titanic.

## 📂 Dataset Overview

The **Titanic dataset** contains passenger information, including whether they survived or not. Here are the key columns in the dataset:

- **PassengerId**: Unique identifier for each passenger.
- **Survived**: Survival status (0 = No, 1 = Yes).
- **Pclass**: Passenger class (1, 2, or 3).
- **Name**: Full name of the passenger.
- **Sex**: Gender of the passenger.
- **Age**: Age of the passenger in years.
- **SibSp**: Number of siblings or spouses aboard.
- **Parch**: Number of parents or children aboard.
- **Ticket**: Ticket number.
- **Fare**: Amount of money paid for the ticket.
- **Cabin**: Cabin number.
- **Embarked**: Port of embarkation (C = Cherbourg, Q = Queenstown, S = Southampton).

## 📚 Libraries Used

This analysis leverages the following Python libraries:

- **pandas**: For data manipulation and analysis.
- **matplotlib**: For creating basic plots and visualizations.
- **seaborn**: For advanced statistical plotting and visualization (e.g., pairplots, correlation heatmaps).

## 🔍 EDA Breakdown

### 1. **Initial Data Exploration**
To understand the dataset, we begin by reviewing its structure, data types, and the presence of missing values.

```python
print("Basic Information:")
print(df.info())

print("\nStatistical Summary:")
print(df.describe())

print("\nMissing Values:")
print(df.isnull().sum())
```

### 2. **Visualizing Numerical Features**

#### 2.1 **Histograms**
Histograms provide a snapshot of the distribution of numerical features, which helps us understand how data is spread across different ranges.

- **Survived**: A binary distribution, with approximately 60% of passengers not surviving (0) and 40% surviving (1).
- **Age**: The age distribution is right-skewed, with a significant concentration of passengers between 20-30 years of age.
- **Fare**: The fare distribution is highly right-skewed, with many passengers paying lower fares, but some paying significantly higher fares (up to $500).

```python
df.hist(figsize=(12, 8), bins=25, color='skyblue', edgecolor='black')
plt.suptitle('Histograms of Numerical Features', fontsize=14)
plt.show()
```

#### 2.2 **Boxplots**
Boxplots help identify outliers in numerical features. Key insights:

- **Fare**: Contains extreme outliers with fares above $200, indicating some passengers paid significantly higher than others.
- **SibSp and Parch**: Most passengers had few or no family members aboard, but a few had a higher number of siblings, spouses, or parents.

```python
plt.figure(figsize=(12, 6))
for i, col in enumerate(numeric_cols, 1):
    plt.subplot(2, (len(numeric_cols) + 1) // 2, i)
    sns.boxplot(y=df[col], color='lightgreen')
    plt.title(f'Boxplot of {col}', fontsize=10)
plt.tight_layout()
plt.show()
```

#### 2.3 **Scatterplot: Age vs Fare**
This scatterplot visualizes the relationship between **Age** and **Fare**. We observe that the fare distribution doesn't show a clear pattern with age, but both **Age** and **Fare** span a wide range of values.

```python
sns.scatterplot(x='Age', y='Fare', data=df, hue='Sex')
plt.title('Scatterplot: Age vs Fare', fontsize=14)
plt.show()
```

#### 2.4 **Pairplot**
Pairplots are used to visualize the relationships between multiple numerical variables at once. By plotting **Age**, **Fare**, **SibSp**, and **Parch**, we can visually inspect correlations and potential clusters.

```python
sns.pairplot(df[['Age', 'Fare', 'SibSp', 'Parch']].dropna(), height=2.2)
plt.suptitle('Pairplot of Selected Features', y=1.02, fontsize=14)
plt.show()
```

### 3. **Correlation Heatmap**
A **correlation heatmap** gives us a deeper understanding of how numerical features are related to each other. We can see that:

- **Survived & Pclass**: Negative correlation (-0.34), suggesting that passengers in lower classes had lower survival rates.
- **Fare & Pclass**: Strong negative correlation (-0.55), showing that higher class passengers paid significantly more for their tickets.
- **SibSp & Parch**: Moderate positive correlation (0.41), indicating that passengers with more siblings/spouses on board are likely to also have more parents/children.

```python
corr = numeric_df.corr()
sns.heatmap(corr, annot=True, cmap='coolwarm', fmt=".2f")
plt.title('Correlation Heatmap', fontsize=14)
plt.show()
```

## 🧐 Key Observations

- **Survival Rate by Class**: Lower-class passengers (Pclass 3) had significantly lower survival rates than those in higher classes.
- **Age and Survival**: Younger passengers seemed to have a better chance of survival.
- **Fare Distribution**: Most passengers paid a relatively low fare, but a few high-paying passengers might have influenced the ticket pricing strategy.
- **Family Size**: Passengers traveling with family (either as siblings/spouses or parents/children) had a higher likelihood of survival, especially in the case of **SibSp** and **Parch**.

## 🚀 Next Steps

- **Predictive Modeling**: Using machine learning algorithms to predict survival based on these features.
- **Feature Engineering**: Creating new features, such as family size or class-based survival rates, to improve model accuracy.

## 📄 Conclusion

This **Exploratory Data Analysis** (EDA) sheds light on important patterns in the Titanic dataset, including how different features correlate with survival chances. The analysis highlights key factors such as passenger class, age, and family presence that could be leveraged for predictive modeling.

## 📈 Visual Insights

- **Histograms**: Show the distribution of numerical variables.
- **Boxplots**: Reveal outliers in key features.
- **Scatterplots and Pairplots**: Provide a deeper understanding of relationships between features.
- **Correlation Heatmap**: Identifies relationships between numerical variables.
