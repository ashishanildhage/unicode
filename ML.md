# Machine Learning Complete Tutorial

## Table of Contents

1. [Introduction to Machine Learning](#1-introduction-to-machine-learning)
2. [Data Preparation and Feature Engineering](#2-data-preparation-and-feature-engineering)
3. [Supervised Learning Algorithms](#3-supervised-learning-algorithms)
4. [Unsupervised Learning Algorithms](#4-unsupervised-learning-algorithms)
5. [Deep Learning Fundamentals](#5-deep-learning-fundamentals)
6. [Model Evaluation and Validation](#6-model-evaluation-and-validation)
7. [Hyperparameter Tuning and Optimization](#7-hyperparameter-tuning-and-optimization)
8. [Model Deployment and Production](#8-model-deployment-and-production)
9. [Advanced Topics and Best Practices](#9-advanced-topics-and-best-practices)
10. [Resources and Further Learning](#10-resources-and-further-learning)

---

## 1. Introduction to Machine Learning

### 1.1 What is Machine Learning?

**Machine Learning (ML)** is a subset of artificial intelligence (AI) that enables computers to learn and make decisions from data without being explicitly programmed for every specific task. Instead of following pre-written instructions, ML algorithms build mathematical models based on training data to make predictions or decisions.

**Key Concepts:**
- **Learning**: The process of automatically learning patterns from data
- **Prediction**: Using learned patterns to make future predictions
- **Generalization**: The ability to perform well on unseen data
- **Adaptation**: Improving performance as more data becomes available

**Why Machine Learning Matters:**
- **Automation**: Automates complex decision-making processes
- **Scalability**: Handles large-scale data processing efficiently
- **Discovery**: Finds hidden patterns humans might miss
- **Personalization**: Enables customized experiences and recommendations

### 1.2 Types of Machine Learning

#### Supervised Learning
**Supervised Learning** involves training a model on labeled data, where each training example has both input features and the correct output (label). The goal is to learn a mapping function that can predict outputs for new, unseen inputs.

**Characteristics:**
- **Labeled Data**: Training data includes both features and target labels
- **Prediction Focus**: Makes predictions on new data
- **Evaluation**: Performance measured against known correct answers
- **Examples**: Email spam detection, price prediction, medical diagnosis

**Common Applications:**
- **Classification**: Categorizing items into discrete classes (spam/not spam)
- **Regression**: Predicting continuous numerical values (house prices, temperature)

#### Unsupervised Learning
**Unsupervised Learning** works with unlabeled data, finding hidden patterns or structures without predefined labels. The algorithm explores the data to discover inherent groupings or relationships.

**Characteristics:**
- **Unlabeled Data**: No target labels provided
- **Pattern Discovery**: Finds hidden structures in data
- **Exploratory**: Used for understanding data distribution
- **Examples**: Customer segmentation, anomaly detection, topic modeling

**Common Applications:**
- **Clustering**: Grouping similar items together
- **Dimensionality Reduction**: Simplifying data while preserving important information
- **Association Mining**: Finding relationships between variables

#### Reinforcement Learning
**Reinforcement Learning** involves an agent learning through interaction with an environment. The agent receives rewards or penalties for actions and learns to maximize cumulative rewards over time.

**Characteristics:**
- **Interactive Learning**: Learns through trial and error
- **Reward-Based**: Actions are reinforced through feedback
- **Sequential Decision Making**: Considers future consequences
- **Examples**: Game playing, robotic control, recommendation systems

**Key Components:**
- **Agent**: The learner or decision-maker
- **Environment**: The system the agent interacts with
- **Actions**: Choices available to the agent
- **Rewards**: Feedback signals for good/bad actions

### 1.3 Machine Learning Workflow

#### The Standard ML Pipeline

**1. Problem Definition**
- Clearly define the business problem
- Determine if ML is the right solution
- Identify success metrics and constraints

**2. Data Collection**
- Gather relevant data from various sources
- Ensure data quality and representativeness
- Consider data privacy and ethical implications

**3. Data Preparation**
- Clean and preprocess raw data
- Handle missing values and outliers
- Transform data into suitable format

**4. Feature Engineering**
- Create meaningful features from raw data
- Select important features
- Reduce dimensionality if needed

**5. Model Selection**
- Choose appropriate algorithms
- Consider problem type (classification/regression/clustering)
- Evaluate computational requirements

**6. Model Training**
- Split data into training and validation sets
- Train model on training data
- Tune hyperparameters using validation data

**7. Model Evaluation**
- Assess model performance on test data
- Compare different models
- Validate against business requirements

**8. Model Deployment**
- Integrate model into production systems
- Monitor performance in real-world usage
- Plan for model updates and maintenance

### 1.4 Setting Up Your ML Environment

#### Python Environment Setup

**Why Python for Machine Learning:**
- **Rich Ecosystem**: Extensive libraries for data science and ML
- **Community Support**: Large community and comprehensive documentation
- **Interoperability**: Works well with other languages and systems
- **Productivity**: High-level abstractions reduce development time

**Essential Libraries:**
```python
# Core scientific computing libraries
import numpy as np  # Numerical computing and array operations
import pandas as pd  # Data manipulation and analysis
import matplotlib.pyplot as plt  # Data visualization
import seaborn as sns  # Statistical data visualization

# Machine Learning libraries
from sklearn.model_selection import train_test_split  # Data splitting utilities
from sklearn.preprocessing import StandardScaler  # Feature scaling
from sklearn.linear_model import LinearRegression  # Linear models
from sklearn.ensemble import RandomForestClassifier  # Ensemble methods
from sklearn.metrics import accuracy_score, classification_report  # Model evaluation

# Deep Learning libraries
import tensorflow as tf  # Google's deep learning framework
import torch  # Facebook's deep learning framework
import keras  # High-level neural network API

# Additional utilities
import scipy.stats as stats  # Statistical functions
import scikit-learn as sklearn  # Comprehensive ML toolkit
```

**Conda Environment Setup:**
```bash
# Create a new conda environment for ML
conda create -n ml-env python=3.9

# Activate the environment
conda activate ml-env

# Install core data science packages
conda install -c conda-forge numpy pandas matplotlib seaborn scikit-learn

# Install deep learning frameworks
conda install -c conda-forge tensorflow pytorch

# Install Jupyter for interactive development
conda install -c conda-forge jupyter notebook

# Optional: Install GPU support
conda install -c conda-forge cudatoolkit cudnn
```

#### Development Environment Best Practices

**Jupyter Notebook Setup:**
```python
# Configure Jupyter for better ML development
import warnings
warnings.filterwarnings('ignore')  # Suppress warnings for cleaner output

# Set random seeds for reproducibility
import numpy as np
import random
import torch

np.random.seed(42)
random.seed(42)
torch.manual_seed(42)

# Configure matplotlib for inline plotting
%matplotlib inline
import matplotlib.pyplot as plt
plt.style.use('seaborn-v0_8')  # Use a clean plotting style

# Enable autoreload for development
%load_ext autoreload
%autoreload 2
```

**Project Structure:**
```
ml-project/
├── data/
│   ├── raw/           # Raw, immutable data
│   ├── processed/     # Cleaned, processed data
│   └── external/      # External data sources
├── notebooks/         # Jupyter notebooks for exploration
├── src/
│   ├── __init__.py
│   ├── data.py        # Data loading and preprocessing
│   ├── features.py    # Feature engineering
│   ├── models.py      # Model definitions
│   └── utils.py       # Utility functions
├── models/            # Saved model artifacts
├── tests/             # Unit and integration tests
├── requirements.txt   # Python dependencies
└── README.md          # Project documentation
```

---

## 2. Data Preparation and Feature Engineering

### 2.1 Understanding Your Data

#### Data Types in Machine Learning

**Structured Data:**
- **Tabular Data**: Rows and columns with consistent structure
- **Time Series**: Data points ordered by time
- **Examples**: Customer databases, financial records, sensor readings

**Unstructured Data:**
- **Text**: Natural language documents, social media posts
- **Images**: Photographs, medical scans, satellite imagery
- **Audio**: Speech recordings, music, environmental sounds
- **Video**: Moving image sequences with temporal information

**Semi-structured Data:**
- **JSON/XML**: Hierarchical data with some structure
- **Logs**: System logs with timestamped events
- **Examples**: Web clickstreams, IoT sensor data

#### Data Quality Assessment

**Completeness:**
- **Missing Values**: Identify and quantify missing data
- **Coverage**: Assess how well data represents the target population
- **Temporal Gaps**: Check for time periods with no data

**Accuracy:**
- **Measurement Errors**: Validate data collection accuracy
- **Outliers**: Identify anomalous values
- **Consistency**: Check for logical inconsistencies

**Timeliness:**
- **Freshness**: How current is the data?
- **Latency**: Time between data generation and availability
- **Relevance**: Does the data still represent current conditions?

### 2.2 Data Preprocessing

#### Handling Missing Values

**Understanding Missing Data Patterns:**
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Load sample dataset
df = pd.read_csv('data/raw/dataset.csv')

# Analyze missing data patterns
def analyze_missing_data(df):
    """
    Comprehensive analysis of missing data in a DataFrame.

    Parameters:
    df (pd.DataFrame): Input dataframe to analyze

    Returns:
    dict: Summary of missing data analysis
    """
    # Calculate missing value statistics
    missing_stats = df.isnull().sum()
    missing_percent = (missing_stats / len(df)) * 100

    # Create missing data summary
    missing_summary = pd.DataFrame({
        'Missing Count': missing_stats,
        'Missing Percentage': missing_percent
    }).sort_values('Missing Percentage', ascending=False)

    # Visualize missing data
    plt.figure(figsize=(12, 6))
    sns.heatmap(df.isnull(), cbar=False, cmap='viridis')
    plt.title('Missing Data Heatmap')
    plt.show()

    # Identify patterns
    print("Columns with missing data:")
    print(missing_summary[missing_summary['Missing Count'] > 0])

    return missing_summary

# Analyze missing data
missing_analysis = analyze_missing_data(df)
```

**Missing Value Imputation Strategies:**

**1. Mean/Median/Mode Imputation:**
```python
from sklearn.impute import SimpleImputer

def impute_missing_values(df):
    """
    Impute missing values using appropriate strategies for different data types.

    Parameters:
    df (pd.DataFrame): Input dataframe with missing values

    Returns:
    pd.DataFrame: DataFrame with imputed values
    """
    df_imputed = df.copy()

    # Numerical columns - use median (robust to outliers)
    numerical_cols = df.select_dtypes(include=[np.number]).columns
    if len(numerical_cols) > 0:
        num_imputer = SimpleImputer(strategy='median')
        df_imputed[numerical_cols] = num_imputer.fit_transform(df[numerical_cols])

    # Categorical columns - use most frequent value
    categorical_cols = df.select_dtypes(include=['object', 'category']).columns
    if len(categorical_cols) > 0:
        cat_imputer = SimpleImputer(strategy='most_frequent')
        df_imputed[categorical_cols] = cat_imputer.fit_transform(df[categorical_cols])

    return df_imputed

# Apply imputation
df_clean = impute_missing_values(df)
```

**2. Advanced Imputation Techniques:**
```python
from sklearn.experimental import enable_iterative_imputer
from sklearn.impute import IterativeImputer, KNNImputer
from sklearn.ensemble import RandomForestRegressor

def advanced_imputation(df):
    """
    Apply advanced imputation techniques for better accuracy.

    Parameters:
    df (pd.DataFrame): Input dataframe with missing values

    Returns:
    pd.DataFrame: DataFrame with advanced imputation
    """
    df_advanced = df.copy()

    # KNN imputation for numerical data
    numerical_cols = df.select_dtypes(include=[np.number]).columns
    if len(numerical_cols) > 0:
        knn_imputer = KNNImputer(n_neighbors=5)
        df_advanced[numerical_cols] = knn_imputer.fit_transform(df[numerical_cols])

    # Iterative imputation using random forest
    # This models each feature with missing values as a function of other features
    iterative_imputer = IterativeImputer(
        estimator=RandomForestRegressor(n_estimators=10, random_state=42),
        random_state=42
    )
    df_advanced[numerical_cols] = iterative_imputer.fit_transform(df[numerical_cols])

    return df_advanced

# Apply advanced imputation
df_advanced_clean = advanced_imputation(df)
```

#### Outlier Detection and Treatment

**Statistical Methods for Outlier Detection:**
```python
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt

def detect_outliers_iqr(df, column, multiplier=1.5):
    """
    Detect outliers using Interquartile Range (IQR) method.

    The IQR method identifies outliers as data points that fall below Q1 - 1.5*IQR
    or above Q3 + 1.5*IQR, where IQR is the interquartile range.

    Parameters:
    df (pd.DataFrame): Input dataframe
    column (str): Column name to check for outliers
    multiplier (float): IQR multiplier (default 1.5)

    Returns:
    tuple: (outlier_indices, outlier_values)
    """
    Q1 = df[column].quantile(0.25)  # First quartile (25th percentile)
    Q3 = df[column].quantile(0.75)  # Third quartile (75th percentile)
    IQR = Q3 - Q1  # Interquartile range

    # Define outlier bounds
    lower_bound = Q1 - multiplier * IQR
    upper_bound = Q3 + multiplier * IQR

    # Find outliers
    outliers = df[(df[column] < lower_bound) | (df[column] > upper_bound)]
    outlier_indices = outliers.index.tolist()

    print(f"Column: {column}")
    print(f"IQR: {IQR:.2f}")
    print(f"Lower bound: {lower_bound:.2f}, Upper bound: {upper_bound:.2f}")
    print(f"Number of outliers: {len(outliers)}")

    return outlier_indices, outliers[column].values

def detect_outliers_zscore(df, column, threshold=3):
    """
    Detect outliers using Z-score method.

    The Z-score method identifies outliers as data points that are more than
    a certain number of standard deviations away from the mean.

    Parameters:
    df (pd.DataFrame): Input dataframe
    column (str): Column name to check for outliers
    threshold (float): Z-score threshold (default 3)

    Returns:
    tuple: (outlier_indices, outlier_values)
    """
    # Calculate Z-scores
    z_scores = np.abs(stats.zscore(df[column]))

    # Find outliers
    outliers = df[z_scores > threshold]
    outlier_indices = outliers.index.tolist()

    print(f"Column: {column}")
    print(f"Z-score threshold: {threshold}")
    print(f"Number of outliers: {len(outliers)}")

    return outlier_indices, outliers[column].values

# Example usage
numerical_columns = df.select_dtypes(include=[np.number]).columns

for col in numerical_columns:
    print(f"\n=== Analyzing {col} ===")

    # IQR method
    iqr_outliers_idx, iqr_outliers_val = detect_outliers_iqr(df, col)

    # Z-score method
    z_outliers_idx, z_outliers_val = detect_outliers_zscore(df, col)

    # Visualize distribution
    plt.figure(figsize=(12, 4))

    plt.subplot(1, 3, 1)
    plt.hist(df[col], bins=50, alpha=0.7)
    plt.title(f'{col} Distribution')
    plt.xlabel(col)
    plt.ylabel('Frequency')

    plt.subplot(1, 3, 2)
    plt.boxplot(df[col])
    plt.title(f'{col} Box Plot')

    plt.subplot(1, 3, 3)
    stats.probplot(df[col], dist="norm", plot=plt)
    plt.title(f'{col} Q-Q Plot')

    plt.tight_layout()
    plt.show()
```

**Outlier Treatment Strategies:**
```python
def handle_outliers(df, column, method='cap', **kwargs):
    """
    Handle outliers using various strategies.

    Parameters:
    df (pd.DataFrame): Input dataframe
    column (str): Column name to handle outliers for
    method (str): Method to use ('remove', 'cap', 'transform')
    **kwargs: Additional parameters for specific methods

    Returns:
    pd.DataFrame: DataFrame with outliers handled
    """
    df_handled = df.copy()

    if method == 'remove':
        # Remove outliers using IQR method
        Q1 = df[column].quantile(0.25)
        Q3 = df[column].quantile(0.75)
        IQR = Q3 - Q1
        lower_bound = Q1 - 1.5 * IQR
        upper_bound = Q3 + 1.5 * IQR

        df_handled = df_handled[
            (df_handled[column] >= lower_bound) &
            (df_handled[column] <= upper_bound)
        ]
        print(f"Removed {len(df) - len(df_handled)} outliers from {column}")

    elif method == 'cap':
        # Cap outliers at percentile values
        lower_percentile = kwargs.get('lower_percentile', 5)
        upper_percentile = kwargs.get('upper_percentile', 95)

        lower_cap = np.percentile(df[column], lower_percentile)
        upper_cap = np.percentile(df[column], upper_percentile)

        df_handled[column] = np.clip(df[column], lower_cap, upper_cap)
        print(f"Capped outliers in {column} at {lower_percentile}th and {upper_percentile}th percentiles")

    elif method == 'transform':
        # Apply log transformation for right-skewed data
        if (df[column] > 0).all():  # Ensure all values are positive
            df_handled[column] = np.log1p(df[column])  # log(1+x) to handle zeros
            print(f"Applied log transformation to {column}")
        else:
            print(f"Cannot apply log transformation to {column} - contains non-positive values")

    return df_handled

# Example usage
# Remove extreme outliers
df_no_outliers = handle_outliers(df, 'price', method='remove')

# Cap outliers at reasonable percentiles
df_capped = handle_outliers(df, 'income', method='cap', lower_percentile=1, upper_percentile=99)

# Transform skewed data
df_transformed = handle_outliers(df, 'transaction_amount', method='transform')
```

### 2.3 Feature Engineering

#### Feature Scaling and Normalization

**Why Feature Scaling Matters:**
- **Algorithm Performance**: Many ML algorithms perform better with scaled features
- **Convergence Speed**: Gradient-based algorithms converge faster with scaled features
- **Interpretability**: Makes feature importance more comparable
- **Distance-Based Algorithms**: KNN, SVM, PCA require scaled features

**Standardization (Z-score normalization):**
```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler, RobustScaler

def apply_standardization(df, columns):
    """
    Apply standardization (Z-score normalization) to specified columns.

    Standardization transforms features to have mean=0 and standard deviation=1.
    This is useful when features have different units or scales.

    Formula: z = (x - μ) / σ
    where μ is mean and σ is standard deviation

    Parameters:
    df (pd.DataFrame): Input dataframe
    columns (list): List of column names to standardize

    Returns:
    pd.DataFrame: DataFrame with standardized columns
    """
    df_scaled = df.copy()

    scaler = StandardScaler()

    # Fit and transform the specified columns
    df_scaled[columns] = scaler.fit_transform(df[columns])

    print("Standardization applied to columns:", columns)
    print(f"Original mean: {df[columns].mean().round(3).tolist()}")
    print(f"Original std: {df[columns].std().round(3).tolist()}")
    print(f"Scaled mean: {df_scaled[columns].mean().round(3).tolist()}")
    print(f"Scaled std: {df_scaled[columns].std().round(3).tolist()}")

    return df_scaled, scaler

# Example usage
numerical_features = ['age', 'income', 'credit_score']
df_standardized, std_scaler = apply_standardization(df, numerical_features)
```

**Min-Max Normalization:**
```python
def apply_minmax_scaling(df, columns, feature_range=(0, 1)):
    """
    Apply Min-Max normalization to specified columns.

    Min-Max scaling transforms features to a fixed range (default 0-1).
    This is useful when you need features in a specific bounded range.

    Formula: x_scaled = (x - x_min) / (x_max - x_min) * (max_range - min_range) + min_range

    Parameters:
    df (pd.DataFrame): Input dataframe
    columns (list): List of column names to scale
    feature_range (tuple): Desired range for scaled features

    Returns:
    pd.DataFrame: DataFrame with scaled columns
    """
    df_scaled = df.copy()

    scaler = MinMaxScaler(feature_range=feature_range)

    # Fit and transform the specified columns
    df_scaled[columns] = scaler.fit_transform(df[columns])

    print(f"Min-Max scaling applied to columns: {columns}")
    print(f"Feature range: {feature_range}")
    print(f"Original range: {df[columns].min().round(3).tolist()} - {df[columns].max().round(3).tolist()}")
    print(f"Scaled range: {df_scaled[columns].min().round(3).tolist()} - {df_scaled[columns].max().round(3).tolist()}")

    return df_scaled, scaler

# Example usage
df_minmax, minmax_scaler = apply_minmax_scaling(df, numerical_features)
```

**Robust Scaling (for data with outliers):**
```python
def apply_robust_scaling(df, columns):
    """
    Apply robust scaling to specified columns.

    Robust scaling uses median and IQR instead of mean and standard deviation,
    making it more robust to outliers.

    Formula: x_scaled = (x - median) / IQR

    Parameters:
    df (pd.DataFrame): Input dataframe
    columns (list): List of column names to scale

    Returns:
    pd.DataFrame: DataFrame with robustly scaled columns
    """
    df_scaled = df.copy()

    scaler = RobustScaler()

    # Fit and transform the specified columns
    df_scaled[columns] = scaler.fit_transform(df[columns])

    print("Robust scaling applied to columns:", columns)
    print(f"Median: {df[columns].median().round(3).tolist()}")
    print(f"IQR: {(df[columns].quantile(0.75) - df[columns].quantile(0.25)).round(3).tolist()}")

    return df_scaled, scaler

# Example usage
df_robust, robust_scaler = apply_robust_scaling(df, numerical_features)
```

#### Categorical Variable Encoding

**One-Hot Encoding:**
```python
from sklearn.preprocessing import OneHotEncoder
import pandas as pd

def apply_onehot_encoding(df, categorical_columns):
    """
    Apply one-hot encoding to categorical columns.

    One-hot encoding creates binary columns for each category,
    where 1 indicates presence of the category and 0 indicates absence.

    This is suitable for nominal categorical variables (no inherent order).

    Parameters:
    df (pd.DataFrame): Input dataframe
    categorical_columns (list): List of categorical column names

    Returns:
    pd.DataFrame: DataFrame with one-hot encoded columns
    """
    df_encoded = df.copy()

    # Initialize encoder
    encoder = OneHotEncoder(sparse=False, drop='first')  # drop='first' to avoid multicollinearity

    # Apply encoding to each categorical column
    for col in categorical_columns:
        # Fit and transform
        encoded_data = encoder.fit_transform(df[[col]])

        # Create column names for encoded features
        feature_names = [f"{col}_{category}" for category in encoder.categories_[0][1:]]

        # Create DataFrame with encoded features
        encoded_df = pd.DataFrame(encoded_data[:, 1:], columns=feature_names, index=df.index)

        # Concatenate with original dataframe
        df_encoded = pd.concat([df_encoded, encoded_df], axis=1)

        # Drop original categorical column
        df_encoded = df_encoded.drop(col, axis=1)

        print(f"One-hot encoded {col}: {len(feature_names)} new features created")

    return df_encoded, encoder

# Example usage
categorical_features = ['gender', 'education_level', 'employment_status']
df_onehot, onehot_encoder = apply_onehot_encoding(df, categorical_features)
```

**Label Encoding:**
```python
from sklearn.preprocessing import LabelEncoder

def apply_label_encoding(df, categorical_columns):
    """
    Apply label encoding to categorical columns.

    Label encoding assigns integer values to categories.
    This is suitable for ordinal categorical variables (with inherent order).

    Note: This can introduce ordinal relationships where none exist,
    so use carefully with nominal variables.

    Parameters:
    df (pd.DataFrame): Input dataframe
    categorical_columns (list): List of categorical column names

    Returns:
    pd.DataFrame: DataFrame with label encoded columns
    """
    df_encoded = df.copy()
    encoders = {}

    for col in categorical_columns:
        encoder = LabelEncoder()

        # Handle missing values by filling with a placeholder
        df_encoded[col] = df_encoded[col].fillna('Unknown')

        # Fit and transform
        df_encoded[col] = encoder.fit_transform(df_encoded[col])

        # Store encoder for potential inverse transformation
        encoders[col] = encoder

        print(f"Label encoded {col}:")
        for i, category in enumerate(encoder.classes_):
            print(f"  {i}: {category}")

    return df_encoded, encoders

# Example usage (for ordinal variables)
ordinal_features = ['education_level', 'income_bracket']  # These have inherent order
df_label, label_encoders = apply_label_encoding(df, ordinal_features)
```

**Target Encoding (for high-cardinality categorical variables):**
```python
def apply_target_encoding(df, categorical_columns, target_column, smoothing=1.0):
    """
    Apply target encoding to categorical columns.

    Target encoding replaces categorical values with the mean of the target variable
    for that category. This is useful for high-cardinality categorical variables.

    Includes smoothing to prevent overfitting.

    Parameters:
    df (pd.DataFrame): Input dataframe
    categorical_columns (list): List of categorical column names
    target_column (str): Name of target column
    smoothing (float): Smoothing parameter to prevent overfitting

    Returns:
    pd.DataFrame: DataFrame with target encoded columns
    """
    df_encoded = df.copy()

    for col in categorical_columns:
        # Calculate global mean
        global_mean = df[target_column].mean()

        # Calculate category means
        category_means = df.groupby(col)[target_column].mean()

        # Calculate category counts for smoothing
        category_counts = df.groupby(col)[target_column].count()

        # Apply smoothing: weighted average of category mean and global mean
        smoothed_means = (category_counts * category_means + smoothing * global_mean) / (category_counts + smoothing)

        # Map smoothed means to categories
        df_encoded[f"{col}_encoded"] = df[col].map(smoothed_means)

        # Fill any missing categories with global mean
        df_encoded[f"{col}_encoded"] = df_encoded[f"{col}_encoded"].fillna(global_mean)

        print(f"Target encoded {col}: {len(category_means)} unique categories")

    return df_encoded

# Example usage (for classification target)
df_target_encoded = apply_target_encoding(df, ['zip_code', 'occupation'], 'is_churn')
```

#### Feature Selection Techniques

**Filter Methods:**
```python
from sklearn.feature_selection import SelectKBest, f_classif, f_regression, mutual_info_classif
from sklearn.feature_selection import chi2, SelectPercentile
import pandas as pd

def apply_filter_methods(X, y, problem_type='classification', k=10):
    """
    Apply filter methods for feature selection.

    Filter methods select features based on statistical properties,
    independent of any machine learning algorithm.

    Parameters:
    X (pd.DataFrame): Feature matrix
    y (pd.Series): Target variable
    problem_type (str): 'classification' or 'regression'
    k (int): Number of top features to select

    Returns:
    list: Names of selected features
    """
    if problem_type == 'classification':
        # For classification: ANOVA F-test, Mutual Information, Chi-squared
        selectors = {
            'f_classif': SelectKBest(score_func=f_classif, k=k),
            'mutual_info': SelectKBest(score_func=mutual_info_classif, k=k),
            'chi2': SelectKBest(score_func=chi2, k=k)
        }
    else:
        # For regression: F-test, Mutual Information
        selectors = {
            'f_regression': SelectKBest(score_func=f_regression, k=k),
            'mutual_info': SelectKBest(score_func=mutual_info_regression, k=k)
        }

    selected_features = {}

    for method_name, selector in selectors.items():
        try:
            X_selected = selector.fit_transform(X, y)
            selected_indices = selector.get_support(indices=True)
            selected_feature_names = X.columns[selected_indices].tolist()

            selected_features[method_name] = selected_feature_names

            # Display results
            print(f"\n{method_name.upper()} - Top {k} features:")
            feature_scores = pd.DataFrame({
                'feature': X.columns,
                'score': selector.scores_
            }).sort_values('score', ascending=False).head(k)

            for _, row in feature_scores.iterrows():
                print(".4f")

        except Exception as e:
            print(f"Error with {method_name}: {e}")

    return selected_features

# Example usage
# Assuming X is your feature matrix and y is your target
# X = df.drop('target_column', axis=1)
# y = df['target_column']

# selected_features = apply_filter_methods(X, y, problem_type='classification', k=10)
```

**Wrapper Methods:**
```python
from sklearn.feature_selection import RFE, RFECV
from sklearn.linear_model import LogisticRegression, LinearRegression
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor
import matplotlib.pyplot as plt

def apply_wrapper_methods(X, y, problem_type='classification', cv=5):
    """
    Apply wrapper methods for feature selection.

    Wrapper methods use a machine learning algorithm to evaluate
    feature subsets and select the best performing combination.

    Parameters:
    X (pd.DataFrame): Feature matrix
    y (pd.Series): Target variable
    problem_type (str): 'classification' or 'regression'
    cv (int): Number of cross-validation folds

    Returns:
    dict: Selected features from different wrapper methods
    """
    if problem_type == 'classification':
        estimator = LogisticRegression(random_state=42, max_iter=1000)
        rf_estimator = RandomForestClassifier(n_estimators=100, random_state=42)
    else:
        estimator = LinearRegression()
        rf_estimator = RandomForestRegressor(n_estimators=100, random_state=42)

    selected_features = {}

    # Recursive Feature Elimination (RFE)
    print("Applying Recursive Feature Elimination (RFE)...")
    rfe = RFE(estimator=rf_estimator, n_features_to_select=10)
    rfe.fit(X, y)

    rfe_features = X.columns[rfe.support_].tolist()
    selected_features['RFE'] = rfe_features

    print(f"RFE selected {len(rfe_features)} features:")
    for i, feature in enumerate(rfe_features, 1):
        print(f"{i}. {feature}")

    # Recursive Feature Elimination with Cross-Validation (RFECV)
    print("\nApplying RFECV...")
    rfecv = RFECV(estimator=estimator, step=1, cv=cv, scoring='accuracy' if problem_type == 'classification' else 'neg_mean_squared_error')
    rfecv.fit(X, y)

    rfecv_features = X.columns[rfecv.support_].tolist()
    selected_features['RFECV'] = rfecv_features

    print(f"RFECV selected {len(rfecv_features)} features with optimal CV score: {rfecv.cv_results_['mean_test_score'][-1]:.4f}")

    # Plot RFECV results
    plt.figure(figsize=(10, 6))
    plt.plot(range(1, len(rfecv.cv_results_['mean_test_score']) + 1),
             rfecv.cv_results_['mean_test_score'])
    plt.xlabel('Number of Features')
    plt.ylabel('Cross-Validation Score')
    plt.title('RFECV: Number of Features vs CV Score')
    plt.grid(True)
    plt.show()

    return selected_features

# Example usage
# wrapper_features = apply_wrapper_methods(X, y, problem_type='classification')
```

**Embedded Methods:**
```python
from sklearn.linear_model import Lasso, Ridge
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor
from sklearn.feature_selection import SelectFromModel
import numpy as np

def apply_embedded_methods(X, y, problem_type='classification'):
    """
    Apply embedded methods for feature selection.

    Embedded methods perform feature selection during model training,
    incorporating feature selection as part of the learning process.

    Parameters:
    X (pd.DataFrame): Feature matrix
    y (pd.Series): Target variable
    problem_type (str): 'classification' or 'regression'

    Returns:
    dict: Selected features from different embedded methods
    """
    selected_features = {}

    if problem_type == 'classification':
        rf_model = RandomForestClassifier(n_estimators=100, random_state=42)
        lasso_model = LogisticRegression(penalty='l1', solver='liblinear', random_state=42)
    else:
        rf_model = RandomForestRegressor(n_estimators=100, random_state=42)
        lasso_model = Ridge(alpha=1.0, random_state=42)

    # Random Forest Feature Importance
    print("Random Forest Feature Importance:")
    rf_model.fit(X, y)

    # Get feature importances
    feature_importances = pd.DataFrame({
        'feature': X.columns,
        'importance': rf_model.feature_importances_
    }).sort_values('importance', ascending=False)

    # Select top features based on importance
    rf_selector = SelectFromModel(rf_model, prefit=True)
    rf_selected_mask = rf_selector.get_support()
    rf_features = X.columns[rf_selected_mask].tolist()

    selected_features['RandomForest'] = rf_features

    print(f"Random Forest selected {len(rf_features)} features:")
    for feature in rf_features:
        importance = feature_importances[feature_importances['feature'] == feature]['importance'].values[0]
        print(".4f")

    # L1 Regularization (Lasso)
    print("\nL1 Regularization (Lasso) Feature Selection:")
    lasso_model.fit(X, y)

    # For linear models, coefficients close to zero indicate less important features
    if hasattr(lasso_model, 'coef_'):
        if problem_type == 'classification' and len(np.unique(y)) > 2:
            # Multi-class case - use max absolute coefficient across classes
            coef_importance = np.max(np.abs(lasso_model.coef_), axis=0)
        else:
            coef_importance = np.abs(lasso_model.coef_.flatten())

        lasso_feature_importances = pd.DataFrame({
            'feature': X.columns,
            'coef_abs': coef_importance
        }).sort_values('coef_abs', ascending=False)

        # Select features with non-zero coefficients
        lasso_selector = SelectFromModel(lasso_model, prefit=True)
        lasso_selected_mask = lasso_selector.get_support()
        lasso_features = X.columns[lasso_selected_mask].tolist()

        selected_features['Lasso'] = lasso_features

        print(f"Lasso selected {len(lasso_features)} features:")
        for feature in lasso_features:
            coef = lasso_feature_importances[lasso_feature_importances['feature'] == feature]['coef_abs'].values[0]
            print(".4f")

    return selected_features, feature_importances

# Example usage
# embedded_features, importances = apply_embedded_methods(X, y, problem_type='classification')
```

---

## 3. Supervised Learning Algorithms

### 3.1 Linear Regression

#### Understanding Linear Regression

**Linear Regression** is a supervised learning algorithm that models the relationship between a dependent variable (target) and one or more independent variables (features) using a linear equation.

**Mathematical Foundation:**
```
y = β₀ + β₁x₁ + β₂x₂ + ... + βₙxₙ + ε
```
Where:
- `y` is the predicted value (dependent variable)
- `β₀` is the intercept (bias term)
- `β₁, β₂, ..., βₙ` are the coefficients (weights)
- `x₁, x₂, ..., xₙ` are the feature values
- `ε` is the error term

**Key Assumptions:**
1. **Linearity**: Relationship between features and target is linear
2. **Independence**: Observations are independent of each other
3. **Homoscedasticity**: Constant variance of errors
4. **No multicollinearity**: Features are not highly correlated
5. **Normality**: Error terms are normally distributed

#### Simple Linear Regression Implementation

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score
import seaborn as sns

class SimpleLinearRegressor:
    """
    Custom implementation of simple linear regression to understand the algorithm.

    This class demonstrates the mathematical foundations of linear regression
    before using scikit-learn's optimized implementation.
    """

    def __init__(self):
        """Initialize the linear regression model."""
        self.coefficient = None  # Slope (β₁)
        self.intercept = None    # Intercept (β₀)

    def fit(self, X, y):
        """
        Fit the linear regression model using the normal equation.

        The normal equation provides a closed-form solution:
        β = (X^T * X)^(-1) * X^T * y

        Parameters:
        X (array-like): Feature matrix (single feature for simple regression)
        y (array-like): Target values
        """
        X = np.array(X).flatten()
        y = np.array(y)

        # Calculate means
        x_mean = np.mean(X)
        y_mean = np.mean(y)

        # Calculate coefficient (slope)
        numerator = np.sum((X - x_mean) * (y - y_mean))
        denominator = np.sum((X - x_mean) ** 2)
        self.coefficient = numerator / denominator

        # Calculate intercept
        self.intercept = y_mean - self.coefficient * x_mean

        return self

    def predict(self, X):
        """
        Make predictions using the fitted model.

        Parameters:
        X (array-like): Feature values for prediction

        Returns:
        array: Predicted values
        """
        if self.coefficient is None or self.intercept is None:
            raise ValueError("Model must be fitted before making predictions")

        X = np.array(X).flatten()
        return self.intercept + self.coefficient * X

    def get_coefficients(self):
        """Return the model coefficients."""
        return {
            'intercept': self.intercept,
            'coefficient': self.coefficient,
            'equation': f'y = {self.intercept:.2f} + {self.coefficient:.2f}x'
        }

def demonstrate_simple_linear_regression():
    """
    Complete demonstration of simple linear regression with visualization.
    """
    # Generate sample data
    np.random.seed(42)
    X = np.random.randn(100, 1) * 10
    y = 2.5 * X.flatten() + 1.5 + np.random.randn(100) * 2  # y = 2.5x + 1.5 + noise

    # Fit custom model
    custom_model = SimpleLinearRegressor()
    custom_model.fit(X, y)

    # Fit scikit-learn model for comparison
    sklearn_model = LinearRegression()
    sklearn_model.fit(X, y)

    # Make predictions
    X_test = np.linspace(X.min(), X.max(), 100).reshape(-1, 1)
    y_custom = custom_model.predict(X_test)
    y_sklearn = sklearn_model.predict(X_test)

    # Calculate metrics
    y_pred = custom_model.predict(X)
    mse = mean_squared_error(y, y_pred)
    r2 = r2_score(y, y_pred)

    # Print results
    print("=== Simple Linear Regression Results ===")
    print(f"Custom Model - Intercept: {custom_model.intercept:.4f}, Coefficient: {custom_model.coefficient:.4f}")
    print(f"Scikit-learn - Intercept: {sklearn_model.intercept_:.4f}, Coefficient: {sklearn_model.coef_[0]:.4f}")
    print(f"Mean Squared Error: {mse:.4f}")
    print(f"R² Score: {r2:.4f}")
    print(f"Equation: {custom_model.get_coefficients()['equation']}")

    # Visualization
    plt.figure(figsize=(12, 5))

    # Scatter plot with regression line
    plt.subplot(1, 2, 1)
    plt.scatter(X, y, alpha=0.6, label='Data points')
    plt.plot(X_test, y_custom, 'r-', linewidth=2, label='Custom model')
    plt.plot(X_test, y_sklearn, 'g--', linewidth=2, label='Scikit-learn model')
    plt.xlabel('X (Feature)')
    plt.ylabel('y (Target)')
    plt.title('Simple Linear Regression Fit')
    plt.legend()
    plt.grid(True, alpha=0.3)

    # Residuals plot
    plt.subplot(1, 2, 2)
    residuals = y - y_pred
    plt.scatter(y_pred, residuals, alpha=0.6)
    plt.axhline(y=0, color='r', linestyle='--', linewidth=2)
    plt.xlabel('Predicted Values')
    plt.ylabel('Residuals')
    plt.title('Residuals Plot')
    plt.grid(True, alpha=0.3)

    plt.tight_layout()
    plt.show()

    return custom_model, sklearn_model

# Run the demonstration
if __name__ == "__main__":
    custom_model, sklearn_model = demonstrate_simple_linear_regression()
```

#### Multiple Linear Regression

**Multiple Linear Regression** extends simple linear regression to handle multiple features, modeling the relationship between a dependent variable and multiple independent variables.

```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score, mean_absolute_error
from sklearn.preprocessing import StandardScaler
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

class MultipleLinearRegressionDemo:
    """
    Comprehensive demonstration of multiple linear regression.
    """

    def __init__(self):
        self.model = None
        self.scaler = None
        self.feature_names = None

    def prepare_data(self, df, target_column, test_size=0.2, random_state=42):
        """
        Prepare data for multiple linear regression.

        Parameters:
        df (pd.DataFrame): Input dataframe
        target_column (str): Name of target column
        test_size (float): Proportion of data for testing
        random_state (int): Random state for reproducibility

        Returns:
        tuple: (X_train, X_test, y_train, y_test)
        """
        # Separate features and target
        X = df.drop(target_column, axis=1)
        y = df[target_column]

        self.feature_names = X.columns.tolist()

        # Split data
        X_train, X_test, y_train, y_test = train_test_split(
            X, y, test_size=test_size, random_state=random_state
        )

        print(f"Dataset shape: {df.shape}")
        print(f"Training set: {X_train.shape[0]} samples")
        print(f"Test set: {X_test.shape[0]} samples")
        print(f"Number of features: {X.shape[1]}")

        return X_train, X_test, y_train, y_test

    def fit_model(self, X_train, y_train, scale_features=True):
        """
        Fit the multiple linear regression model.

        Parameters:
        X_train (pd.DataFrame): Training features
        y_train (pd.Series): Training target
        scale_features (bool): Whether to scale features

        Returns:
        LinearRegression: Fitted model
        """
        # Scale features if requested
        if scale_features:
            self.scaler = StandardScaler()
            X_train_scaled = self.scaler.fit_transform(X_train)
            X_train_scaled = pd.DataFrame(X_train_scaled, columns=X_train.columns, index=X_train.index)
        else:
            X_train_scaled = X_train

        # Fit model
        self.model = LinearRegression()
        self.model.fit(X_train_scaled, y_train)

        print("=== Model Coefficients ===")
        for feature, coef in zip(self.feature_names, self.model.coef_):
            print(".4f")
        print(".4f")

        return self.model

    def evaluate_model(self, X_test, y_test):
        """
        Evaluate the model performance.

        Parameters:
        X_test (pd.DataFrame): Test features
        y_test (pd.Series): Test target

        Returns:
        dict: Evaluation metrics
        """
        # Scale test data if scaler was used
        if self.scaler:
            X_test_scaled = self.scaler.transform(X_test)
            X_test_scaled = pd.DataFrame(X_test_scaled, columns=X_test.columns, index=X_test.index)
        else:
            X_test_scaled = X_test

        # Make predictions
        y_pred = self.model.predict(X_test_scaled)

        # Calculate metrics
        mse = mean_squared_error(y_test, y_pred)
        rmse = np.sqrt(mse)
        mae = mean_absolute_error(y_test, y_pred)
        r2 = r2_score(y_test, y_pred)

        metrics = {
            'MSE': mse,
            'RMSE': rmse,
            'MAE': mae,
            'R²': r2
        }

        print("=== Model Evaluation ===")
        print(f"Mean Squared Error (MSE): {mse:.4f}")
        print(f"Root Mean Squared Error (RMSE): {rmse:.4f}")
        print(f"Mean Absolute Error (MAE): {mae:.4f}")
        print(f"R² Score: {r2:.4f}")

        # Interpretation of R²
        if r2 > 0.8:
            print("Excellent fit (R² > 0.8)")
        elif r2 > 0.6:
            print("Good fit (0.6 < R² ≤ 0.8)")
        elif r2 > 0.3:
            print("Fair fit (0.3 < R² ≤ 0.6)")
        else:
            print("Poor fit (R² ≤ 0.3)")

        return metrics, y_pred

    def analyze_residuals(self, y_test, y_pred):
        """
        Analyze model residuals for assumptions checking.

        Parameters:
        y_test (pd.Series): Actual target values
        y_pred (array): Predicted values
        """
        residuals = y_test - y_pred

        # Create residual plots
        fig, axes = plt.subplots(2, 2, figsize=(12, 10))

        # Residuals vs Fitted
        axes[0, 0].scatter(y_pred, residuals, alpha=0.6)
        axes[0, 0].axhline(y=0, color='r', linestyle='--')
        axes[0, 0].set_xlabel('Fitted Values')
        axes[0, 0].set_ylabel('Residuals')
        axes[0, 0].set_title('Residuals vs Fitted')
        axes[0, 0].grid(True, alpha=0.3)

        # Q-Q Plot for normality
        stats.probplot(residuals, dist="norm", plot=axes[0, 1])
        axes[0, 1].set_title('Q-Q Plot (Residual Normality)')

        # Residuals distribution
        axes[1, 0].hist(residuals, bins=30, alpha=0.7, edgecolor='black')
        axes[1, 0].set_xlabel('Residuals')
        axes[1, 0].set_ylabel('Frequency')
        axes[1, 0].set_title('Residuals Distribution')
        axes[1, 0].axvline(x=0, color='r', linestyle='--')

        # Scale-Location plot (for homoscedasticity)
        standardized_residuals = residuals / np.std(residuals)
        axes[1, 1].scatter(y_pred, np.sqrt(np.abs(standardized_residuals)), alpha=0.6)
        axes[1, 1].set_xlabel('Fitted Values')
        axes[1, 1].set_ylabel('√|Standardized Residuals|')
        axes[1, 1].set_title('Scale-Location Plot')
        axes[1, 1].grid(True, alpha=0.3)

        plt.tight_layout()
        plt.show()

        # Statistical tests
        print("=== Residual Analysis ===")

        # Normality test
        _, p_value = stats.shapiro(residuals)
        print(f"Shapiro-Wilk normality test p-value: {p_value:.4f}")
        if p_value > 0.05:
            print("Residuals appear normally distributed")
        else:
            print("Residuals do not appear normally distributed")

        # Homoscedasticity test (Breusch-Pagan)
        try:
            from statsmodels.stats.diagnostic import het_breuschpagan
            from statsmodels.regression.linear_model import OLS
            import statsmodels.api as sm

            # Add constant for statsmodels
            X_with_const = sm.add_constant(y_pred)
            model = OLS(residuals**2, X_with_const).fit()
            bp_test = het_breuschpagan(model.resid, X_with_const)

            print(f"Breusch-Pagan test p-value: {bp_test[1]:.4f}")
            if bp_test[1] > 0.05:
                print("Homoscedasticity assumption holds")
            else:
                print("Heteroscedasticity detected")
        except ImportError:
            print("Install statsmodels for homoscedasticity testing")

    def plot_feature_importance(self):
        """Plot feature importance based on coefficients."""
        if not self.model or not self.feature_names:
            print("Model must be fitted first")
            return

        # Create feature importance dataframe
        importance_df = pd.DataFrame({
            'feature': self.feature_names,
            'coefficient': np.abs(self.model.coef_)
        }).sort_values('coefficient', ascending=True)

        # Plot
        plt.figure(figsize=(10, 6))
        bars = plt.barh(importance_df['feature'], importance_df['coefficient'])
        plt.xlabel('Absolute Coefficient Value')
        plt.ylabel('Features')
        plt.title('Feature Importance (Absolute Coefficients)')
        plt.grid(True, alpha=0.3)

        # Add value labels
        for bar, value in zip(bars, importance_df['coefficient']):
            plt.text(bar.get_width() + 0.001, bar.get_y() + bar.get_height()/2,
                    '.3f', ha='left', va='center')

        plt.tight_layout()
        plt.show()

def run_multiple_linear_regression_demo():
    """
    Complete demonstration of multiple linear regression.
    """
    # Create sample dataset (you would replace this with your actual data)
    np.random.seed(42)
    n_samples = 1000

    # Generate features
    X = pd.DataFrame({
        'feature1': np.random.randn(n_samples),
        'feature2': np.random.randn(n_samples) * 2,
        'feature3': np.random.randint(1, 5, n_samples),
        'feature4': np.random.exponential(1, n_samples)
    })

    # Generate target with known relationships
    y = (2.5 * X['feature1'] +
         -1.8 * X['feature2'] +
         0.5 * X['feature3'] +
         1.2 * X['feature4'] +
         np.random.randn(n_samples) * 0.5)  # Add noise

    # Create dataframe
    df = X.copy()
    df['target'] = y

    # Initialize demo
    demo = MultipleLinearRegressionDemo()

    # Prepare data
    X_train, X_test, y_train, y_test = demo.prepare_data(df, 'target')

    # Fit model
    model = demo.fit_model(X_train, y_train, scale_features=True)

    # Evaluate model
    metrics, y_pred = demo.evaluate_model(X_test, y_test)

    # Analyze residuals
    demo.analyze_residuals(y_test, y_pred)

    # Plot feature importance
    demo.plot_feature_importance()

    return demo

# Run the demonstration
if __name__ == "__main__":
    demo = run_multiple_linear_regression_demo()
```

### 3.2 Logistic Regression

#### Understanding Logistic Regression

**Logistic Regression** is a supervised learning algorithm used for binary and multi-class classification problems. Despite its name, it's a classification algorithm that uses a logistic (sigmoid) function to model the probability of a binary outcome.

**Mathematical Foundation:**
```
P(y=1|X) = 1 / (1 + e^(-(β₀ + β₁x₁ + β₂x₂ + ... + βₙxₙ)))
```
Where:
- `P(y=1|X)` is the probability of the positive class
- `β₀, β₁, ..., βₙ` are the model coefficients
- `x₁, x₂, ..., xₙ` are the feature values

**Key Concepts:**
- **Logit Function**: log(P/(1-P)) = β₀ + β₁x₁ + ...
- **Sigmoid Function**: Converts logit to probability (0-1 range)
- **Decision Boundary**: Threshold (usually 0.5) for classification
- **Odds Ratio**: e^βᵢ represents the change in odds for a one-unit increase in xᵢ

#### Binary Classification Implementation

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import (accuracy_score, precision_score, recall_score,
                           f1_score, roc_auc_score, confusion_matrix,
                           classification_report, roc_curve, auc)
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
import seaborn as sns
import warnings
warnings.filterwarnings('ignore')

class LogisticRegressionDemo:
    """
    Comprehensive demonstration of logistic regression for binary classification.
    """

    def __init__(self, random_state=42):
        self.model = None
        self.scaler = None
        self.random_state = random_state
        self.feature_names = None

    def prepare_data(self, df, target_column, test_size=0.2):
        """
        Prepare data for logistic regression.

        Parameters:
        df (pd.DataFrame): Input dataframe
        target_column (str): Name of target column (binary: 0/1)
        test_size (float): Proportion of data for testing

        Returns:
        tuple: (X_train, X_test, y_train, y_test)
        """
        # Separate features and target
        X = df.drop(target_column, axis=1)
        y = df[target_column]

        self.feature_names = X.columns.tolist()

        # Verify binary classification
        unique_classes = y.unique()
        if len(unique_classes) != 2:
            raise ValueError(f"Target must be binary, found {len(unique_classes)} classes: {unique_classes}")

        print(f"Classes: {unique_classes}")
        print(f"Class distribution: {y.value_counts().to_dict()}")

        # Check class balance
        class_balance = y.value_counts(normalize=True)
        print(f"Class balance: {class_balance.round(3).to_dict()}")

        if min(class_balance) < 0.1:
            print("⚠️  Warning: Severe class imbalance detected!")

        # Split data
        X_train, X_test, y_train, y_test = train_test_split(
            X, y, test_size=test_size, random_state=self.random_state, stratify=y
        )

        print(f"\nDataset: {df.shape[0]} samples, {X.shape[1]} features")
        print(f"Training set: {X_train.shape[0]} samples")
        print(f"Test set: {X_test.shape[0]} samples")

        return X_train, X_test, y_train, y_test

    def fit_model(self, X_train, y_train, scale_features=True, class_weight=None):
        """
        Fit the logistic regression model.

        Parameters:
        X_train (pd.DataFrame): Training features
        y_train (pd.Series): Training target
        scale_features (bool): Whether to scale features
        class_weight (str or dict): Class weights for imbalanced data

        Returns:
        LogisticRegression: Fitted model
        """
        # Scale features if requested
        if scale_features:
            self.scaler = StandardScaler()
            X_train_scaled = self.scaler.fit_transform(X_train)
            X_train_scaled = pd.DataFrame(X_train_scaled, columns=X_train.columns, index=X_train.index)
        else:
            X_train_scaled = X_train

        # Initialize model with appropriate parameters
        self.model = LogisticRegression(
            random_state=self.random_state,
            max_iter=1000,
            class_weight=class_weight  # Handle class imbalance
        )

        # Fit model
        self.model.fit(X_train_scaled, y_train)

        # Display coefficients
        print("=== Model Coefficients ===")
        print(f"Intercept: {self.model.intercept_[0]:.4f}")

        coef_df = pd.DataFrame({
            'feature': self.feature_names,
            'coefficient': self.model.coef_[0],
            'odds_ratio': np.exp(self.model.coef_[0])
        }).sort_values('coefficient', ascending=False)

        print("\nTop positive coefficients (increase probability of positive class):")
        for _, row in coef_df.head(5).iterrows():
            print(".4f")

        print("\nTop negative coefficients (decrease probability of positive class):")
        for _, row in coef_df.tail(5).iterrows():
            print(".4f")

        return self.model

    def evaluate_model(self, X_test, y_test, threshold=0.5):
        """
        Evaluate the model performance.

        Parameters:
        X_test (pd.DataFrame): Test features
        y_test (pd.Series): Test target
        threshold (float): Classification threshold

        Returns:
        dict: Evaluation metrics
        """
        # Scale test data if scaler was used
        if self.scaler:
            X_test_scaled = self.scaler.transform(X_test)
            X_test_scaled = pd.DataFrame(X_test_scaled, columns=X_test.columns, index=X_test.index)
        else:
            X_test_scaled = X_test

        # Get prediction probabilities
        y_prob = self.model.predict_proba(X_test_scaled)[:, 1]

        # Make predictions with custom threshold
        y_pred = (y_prob >= threshold).astype(int)

        # Calculate metrics
        accuracy = accuracy_score(y_test, y_pred)
        precision = precision_score(y_test, y_pred)
        recall = recall_score(y_test, y_pred)
        f1 = f1_score(y_test, y_pred)
        auc = roc_auc_score(y_test, y_prob)

        metrics = {
            'accuracy': accuracy,
            'precision': precision,
            'recall': recall,
            'f1_score': f1,
            'auc': auc,
            'threshold': threshold
        }

        print(f"\n=== Model Evaluation (Threshold: {threshold}) ===")
        print(f"Accuracy:  {accuracy:.4f}")
        print(f"Precision: {precision:.4f}")
        print(f"Recall:    {recall:.4f}")
        print(f"F1-Score:  {f1:.4f}")
        print(f"AUC:       {auc:.4f}")

        # Classification report
        print("
Detailed Classification Report:")
        print(classification_report(y_test, y_pred, target_names=['Negative', 'Positive']))

        return metrics, y_pred, y_prob

    def plot_evaluation_curves(self, y_test, y_prob):
        """
        Plot evaluation curves (ROC, Precision-Recall).

        Parameters:
        y_test (pd.Series): True labels
        y_prob (array): Prediction probabilities
        """
        fig, axes = plt.subplots(1, 3, figsize=(18, 6))

        # Confusion Matrix
        y_pred = (y_prob >= 0.5).astype(int)
        cm = confusion_matrix(y_test, y_pred)

        sns.heatmap(cm, annot=True, fmt='d', cmap='Blues',
                   xticklabels=['Predicted Negative', 'Predicted Positive'],
                   yticklabels=['Actual Negative', 'Actual Positive'],
                   ax=axes[0])
        axes[0].set_title('Confusion Matrix')
        axes[0].set_ylabel('True Label')
        axes[0].set_xlabel('Predicted Label')

        # ROC Curve
        fpr, tpr, _ = roc_curve(y_test, y_prob)
        roc_auc = auc(fpr, tpr)

        axes[1].plot(fpr, tpr, color='darkorange', lw=2,
                    label=f'ROC curve (AUC = {roc_auc:.2f})')
        axes[1].plot([0, 1], [0, 1], color='navy', lw=2, linestyle='--')
        axes[1].set_xlim([0.0, 1.0])
        axes[1].set_ylim([0.0, 1.05])
        axes[1].set_xlabel('False Positive Rate')
        axes[1].set_ylabel('True Positive Rate')
        axes[1].set_title('Receiver Operating Characteristic (ROC)')
        axes[1].legend(loc="lower right")
        axes[1].grid(True, alpha=0.3)

        # Precision-Recall Curve
        from sklearn.metrics import precision_recall_curve, average_precision_score

        precision, recall, _ = precision_recall_curve(y_test, y_prob)
        avg_precision = average_precision_score(y_test, y_prob)

        axes[2].plot(recall, precision, color='blue', lw=2,
                    label=f'Precision-Recall curve (AP = {avg_precision:.2f})')
        axes[2].set_xlim([0.0, 1.0])
        axes[2].set_ylim([0.0, 1.05])
        axes[2].set_xlabel('Recall')
        axes[2].set_ylabel('Precision')
        axes[2].set_title('Precision-Recall Curve')
        axes[2].legend(loc="lower left")
        axes[2].grid(True, alpha=0.3)

        plt.tight_layout()
        plt.show()

    def find_optimal_threshold(self, X_val, y_val, metric='f1'):
        """
        Find optimal classification threshold for a given metric.

        Parameters:
        X_val (pd.DataFrame): Validation features
        y_val (pd.Series): Validation target
        metric (str): Metric to optimize ('f1', 'precision', 'recall')

        Returns:
        float: Optimal threshold
        """
        # Scale validation data
        if self.scaler:
            X_val_scaled = self.scaler.transform(X_val)
            X_val_scaled = pd.DataFrame(X_val_scaled, columns=X_val.columns, index=X_val.index)
        else:
            X_val_scaled = X_val

        # Get prediction probabilities
        y_prob = self.model.predict_proba(X_val_scaled)[:, 1]

        # Try different thresholds
        thresholds = np.arange(0.1, 0.9, 0.05)
        best_score = 0
        best_threshold = 0.5

        for threshold in thresholds:
            y_pred = (y_prob >= threshold).astype(int)

            if metric == 'f1':
                score = f1_score(y_val, y_pred)
            elif metric == 'precision':
                score = precision_score(y_val, y_pred)
            elif metric == 'recall':
                score = recall_score(y_val, y_pred)
            else:
                raise ValueError(f"Unknown metric: {metric}")

            if score > best_score:
                best_score = score
                best_threshold = threshold

        print(f"\nOptimal threshold for {metric}: {best_threshold:.2f} (score: {best_score:.4f})")
        return best_threshold

    def plot_feature_importance(self):
        """Plot feature importance based on coefficients."""
        if not self.model or not self.feature_names:
            print("Model must be fitted first")
            return

        # Create feature importance dataframe
        importance_df = pd.DataFrame({
            'feature': self.feature_names,
            'coefficient': self.model.coef_[0],
            'abs_coefficient': np.abs(self.model.coef_[0]),
            'odds_ratio': np.exp(self.model.coef_[0])
        }).sort_values('abs_coefficient', ascending=False)

        # Plot coefficients
        fig, axes = plt.subplots(1, 2, figsize=(15, 6))

        # Absolute coefficient values
        bars1 = axes[0].barh(importance_df['feature'][:10], importance_df['abs_coefficient'][:10])
        axes[0].set_xlabel('Absolute Coefficient Value')
        axes[0].set_title('Top 10 Feature Importance (Absolute Coefficients)')
        axes[0].grid(True, alpha=0.3)

        # Odds ratios
        bars2 = axes[1].barh(importance_df['feature'][:10], importance_df['odds_ratio'][:10])
        axes[1].set_xlabel('Odds Ratio')
        axes[1].set_title('Top 10 Features (Odds Ratios)')
        axes[1].axvline(x=1, color='r', linestyle='--', alpha=0.7, label='No effect')
        axes[1].legend()
        axes[1].grid(True, alpha=0.3)

        # Add value labels
        for ax, bars, values in [(axes[0], bars1, importance_df['abs_coefficient'][:10]),
                                (axes[1], bars2, importance_df['odds_ratio'][:10])]:
            for bar, value in zip(bars, values):
                ax.text(bar.get_width() + 0.01, bar.get_y() + bar.get_height()/2,
                       '.2f', ha='left', va='center', fontsize=8)

        plt.tight_layout()
        plt.show()

def run_logistic_regression_demo():
    """
    Complete demonstration of logistic regression for binary classification.
    """
    # Create sample dataset (replace with your actual data)
    np.random.seed(42)
    n_samples = 1000

    # Generate features
    X = pd.DataFrame({
        'age': np.random.normal(35, 10, n_samples).clip(18, 80),
        'income': np.random.exponential(50000, n_samples),
        'credit_score': np.random.normal(650, 50, n_samples).clip(300, 850),
        'debt_ratio': np.random.beta(2, 5, n_samples),
        'employment_years': np.random.exponential(5, n_samples).clip(0, 40)
    })

    # Generate target with realistic relationships
    logit = (-3.5 +
             0.02 * X['age'] +
             0.00003 * X['income'] +
             0.01 * X['credit_score'] +
             -2.0 * X['debt_ratio'] +
             0.1 * X['employment_years'])

    prob = 1 / (1 + np.exp(-logit))
    y = np.random.binomial(1, prob, n_samples)

    # Create dataframe
    df = X.copy()
    df['approved'] = y

    print("Sample dataset created with credit approval scenario")
    print(f"Approval rate: {y.mean():.1%}")

    # Initialize demo
    demo = LogisticRegressionDemo()

    # Prepare data
    X_train, X_test, y_train, y_test = demo.prepare_data(df, 'approved')

    # Fit model
    model = demo.fit_model(X_train, y_train, scale_features=True)

    # Evaluate model
    metrics, y_pred, y_prob = demo.evaluate_model(X_test, y_test)

    # Plot evaluation curves
    demo.plot_evaluation_curves(y_test, y_prob)

    # Find optimal threshold
    optimal_threshold = demo.find_optimal_threshold(X_test, y_test, metric='f1')

    # Evaluate with optimal threshold
    print(f"\n=== Evaluation with Optimal Threshold ({optimal_threshold:.2f}) ===")
    opt_metrics, _, _ = demo.evaluate_model(X_test, y_test, threshold=optimal_threshold)

    # Plot feature importance
    demo.plot_feature_importance()

    return demo

# Run the demonstration
if __name__ == "__main__":
    demo = run_logistic_regression_demo()
```

### 3.3 Decision Trees and Random Forests

#### Understanding Decision Trees

**Decision Trees** are supervised learning algorithms that create a tree-like model of decisions and their possible consequences. They work by recursively partitioning the data based on feature values to create homogeneous subsets.

**Key Concepts:**
- **Root Node**: Starting point of the tree
- **Internal Nodes**: Decision points based on feature values
- **Leaf Nodes**: Final outcomes or predictions
- **Splitting**: Process of dividing data based on feature thresholds
- **Pruning**: Removing branches to prevent overfitting

**Advantages:**
- **Interpretability**: Easy to understand and visualize
- **No Feature Scaling**: Not affected by feature scales
- **Handles Mixed Data**: Works with numerical and categorical features
- **Non-parametric**: No assumptions about data distribution

**Disadvantages:**
- **Overfitting**: Can create complex trees that don't generalize
- **Instability**: Small data changes can result in very different trees
- **Bias towards dominant classes**: Can be biased in imbalanced datasets

#### Decision Tree Implementation

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.tree import DecisionTreeClassifier, DecisionTreeRegressor, plot_tree
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.metrics import (accuracy_score, classification_report,
                           mean_squared_error, r2_score)
from sklearn.preprocessing import LabelEncoder
import seaborn as sns
from sklearn import tree
import graphviz

class DecisionTreeDemo:
    """
    Comprehensive demonstration of decision tree algorithms.
    """

    def __init__(self, problem_type='classification', random_state=42):
        self.problem_type = problem_type
        self.random_state = random_state
        self.model = None
        self.feature_names = None
        self.target_names = None

    def prepare_data(self, df, target_column, test_size=0.2):
        """
        Prepare data for decision tree modeling.

        Parameters:
        df (pd.DataFrame): Input dataframe
        target_column (str): Name of target column
        test_size (float): Proportion of data for testing

        Returns:
        tuple: (X_train, X_test, y_train, y_test)
        """
        # Separate features and target
        X = df.drop(target_column, axis=1)
        y = df[target_column]

        self.feature_names = X.columns.tolist()

        # Handle categorical target for visualization
        if self.problem_type == 'classification':
            le = LabelEncoder()
            y_encoded = le.fit_transform(y)
            self.target_names = le.classes_.tolist()

            # Check class distribution
            print(f"Classes: {self.target_names}")
            print(f"Class distribution: {pd.Series(y).value_counts().to_dict()}")
        else:
            y_encoded = y
            self.target_names = None

        # Split data
        X_train, X_test, y_train, y_test = train_test_split(
            X, y_encoded, test_size=test_size, random_state=self.random_state,
            stratify=y_encoded if self.problem_type == 'classification' else None
        )

        print(f"\nDataset: {df.shape[0]} samples, {X.shape[1]} features")
        print(f"Training set: {X_train.shape[0]} samples")
        print(f"Test set: {X_test.shape[0]} samples")

        return X_train, X_test, y_train, y_test

    def fit_model(self, X_train, y_train, max_depth=None, min_samples_split=2,
                  min_samples_leaf=1, criterion='gini'):
        """
        Fit the decision tree model.

        Parameters:
        X_train (pd.DataFrame): Training features
        y_train (pd.Series): Training target
        max_depth (int): Maximum depth of the tree
        min_samples_split (int): Minimum samples to split a node
        min_samples_leaf (int): Minimum samples in leaf nodes
        criterion (str): Splitting criterion ('gini' or 'entropy' for classification)

        Returns:
        Decision tree model
        """
        if self.problem_type == 'classification':
            self.model = DecisionTreeClassifier(
                max_depth=max_depth,
                min_samples_split=min_samples_split,
                min_samples_leaf=min_samples_leaf,
                criterion=criterion,
                random_state=self.random_state
            )
        else:
            self.model = DecisionTreeRegressor(
                max_depth=max_depth,
                min_samples_split=min_samples_split,
                min_samples_leaf=min_samples_leaf,
                random_state=self.random_state
            )

        # Fit model
        self.model.fit(X_train, y_train)

        # Display model information
        print("=== Decision Tree Model ===")
        print(f"Tree depth: {self.model.get_depth()}")
        print(f"Number of leaves: {self.model.get_n_leaves()}")
        print(f"Number of nodes: {self.model.tree_.node_count}")

        if self.problem_type == 'classification':
            print(f"Feature importances (top 5):")
            feature_importance = pd.DataFrame({
                'feature': self.feature_names,
                'importance': self.model.feature_importances_
            }).sort_values('importance', ascending=False)

            for _, row in feature_importance.head(5).iterrows():
                print(".4f")

        return self.model

    def evaluate_model(self, X_test, y_test):
        """
        Evaluate the decision tree model.

        Parameters:
        X_test (pd.DataFrame): Test features
        y_test (pd.Series): Test target

        Returns:
        dict: Evaluation metrics
        """
        # Make predictions
        y_pred = self.model.predict(X_test)

        if self.problem_type == 'classification':
            # Classification metrics
            accuracy = accuracy_score(y_test, y_pred)

            metrics = {
                'accuracy': accuracy,
                'predictions': y_pred
            }

            print("=== Classification Results ===")
            print(f"Accuracy: {accuracy:.4f}")
            print("
Detailed Classification Report:")
            print(classification_report(y_test, y_pred,
                                      target_names=self.target_names if self.target_names else None))

        else:
            # Regression metrics
            mse = mean_squared_error(y_test, y_pred)
            rmse = np.sqrt(mse)
            r2 = r2_score(y_test, y_pred)

            metrics = {
                'mse': mse,
                'rmse': rmse,
                'r2': r2,
                'predictions': y_pred
            }

            print("=== Regression Results ===")
            print(f"MSE:  {mse:.4f}")
            print(f"RMSE: {rmse:.4f}")
            print(f"R²:   {r2:.4f}")

        return metrics

    def visualize_tree(self, max_depth=3, figsize=(20, 10)):
        """
        Visualize the decision tree.

        Parameters:
        max_depth (int): Maximum depth to display
        figsize (tuple): Figure size for the plot
        """
        if not self.model:
            print("Model must be fitted first")
            return

        plt.figure(figsize=figsize)

        if self.problem_type == 'classification':
            plot_tree(self.model,
                     feature_names=self.feature_names,
                     class_names=self.target_names,
                     filled=True,
                     rounded=True,
                     max_depth=max_depth,
                     fontsize=10)
        else:
            plot_tree(self.model,
                     feature_names=self.feature_names,
                     filled=True,
                     rounded=True,
                     max_depth=max_depth,
                     fontsize=10)

        plt.title(f"Decision Tree Visualization (max_depth={max_depth})")
        plt.show()

    def plot_feature_importance(self, top_n=10):
        """Plot feature importance."""
        if not self.model or self.problem_type != 'classification':
            print("Feature importance only available for classification models")
            return

        # Get feature importances
        importance_df = pd.DataFrame({
            'feature': self.feature_names,
            'importance': self.model.feature_importances_
        }).sort_values('importance', ascending=False).head(top_n)

        # Plot
        plt.figure(figsize=(10, 6))
        bars = plt.barh(importance_df['feature'], importance_df['importance'])
        plt.xlabel('Feature Importance')
        plt.ylabel('Features')
        plt.title(f'Top {top_n} Feature Importance')
        plt.grid(True, alpha=0.3)

        # Add value labels
        for bar, value in zip(bars, importance_df['importance']):
            plt.text(bar.get_width() + 0.001, bar.get_y() + bar.get_height()/2,
                    '.3f', ha='left', va='center')

        plt.tight_layout()
        plt.show()

    def analyze_tree_complexity(self, X_train, y_train):
        """
        Analyze how tree complexity affects performance.

        Parameters:
        X_train (pd.DataFrame): Training features
        y_train (pd.Series): Training target
        """
        max_depths = range(1, 21)
        train_scores = []
        val_scores = []

        # Use cross-validation to evaluate different depths
        for depth in max_depths:
            if self.problem_type == 'classification':
                model = DecisionTreeClassifier(max_depth=depth, random_state=self.random_state)
                scores = cross_val_score(model, X_train, y_train, cv=5,
                                       scoring='accuracy')
            else:
                model = DecisionTreeRegressor(max_depth=depth, random_state=self.random_state)
                scores = cross_val_score(model, X_train, y_train, cv=5,
                                       scoring='neg_mean_squared_error')
                scores = -scores  # Convert to positive MSE

            train_scores.append(scores.mean())

        # Plot complexity analysis
        plt.figure(figsize=(10, 6))
        plt.plot(max_depths, train_scores, 'b-', label='CV Score', marker='o')
        plt.xlabel('Tree Depth')
        plt.ylabel('Score')
        plt.title('Decision Tree Complexity Analysis')
        plt.grid(True, alpha=0.3)
        plt.legend()

        # Find optimal depth
        optimal_depth = max_depths[np.argmax(train_scores)]
        plt.axvline(x=optimal_depth, color='r', linestyle='--',
                   label=f'Optimal depth: {optimal_depth}')
        plt.legend()

        plt.show()

        print(f"Optimal tree depth: {optimal_depth}")

def run_decision_tree_demo():
    """
    Complete demonstration of decision tree algorithms.
    """
    # Create sample classification dataset
    np.random.seed(42)
    n_samples = 1000

    # Generate features
    X = pd.DataFrame({
        'age': np.random.normal(35, 10, n_samples).clip(18, 80),
        'income': np.random.exponential(50000, n_samples),
        'credit_score': np.random.normal(650, 50, n_samples).clip(300, 850),
        'debt_ratio': np.random.beta(2, 5, n_samples),
        'employment_years': np.random.exponential(5, n_samples).clip(0, 40)
    })

    # Generate target (loan approval)
    features = X.values
    # Simple decision rules for demonstration
    approval_score = (
        (X['credit_score'] > 650).astype(int) * 2 +
        (X['income'] > 40000).astype(int) * 1.5 +
        (X['debt_ratio'] < 0.3).astype(int) * 2 +
        (X['employment_years'] > 2).astype(int) * 1 +
        np.random.normal(0, 0.5, n_samples)  # Add noise
    )

    y = (approval_score > 4).astype(int)

    # Create dataframe
    df = X.copy()
    df['approved'] = y

    print("Sample loan approval dataset created")
    print(f"Approval rate: {y.mean():.1%}")

    # Initialize demo
    demo = DecisionTreeDemo(problem_type='classification')

    # Prepare data
    X_train, X_test, y_train, y_test = demo.prepare_data(df, 'approved')

    # Analyze tree complexity
    demo.analyze_tree_complexity(X_train, y_train)

    # Fit model with reasonable depth
    model = demo.fit_model(X_train, y_train, max_depth=5, criterion='gini')

    # Evaluate model
    metrics = demo.evaluate_model(X_test, y_test)

    # Visualize tree
    demo.visualize_tree(max_depth=3)

    # Plot feature importance
    demo.plot_feature_importance()

    return demo

# Run the demonstration
if __name__ == "__main__":
    demo = run_decision_tree_demo()
```

#### Random Forest Implementation

**Random Forest** is an ensemble learning method that constructs multiple decision trees and merges their results. It reduces overfitting and improves generalization through bagging and feature randomness.

```python
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor
from sklearn.model_selection import RandomizedSearchCV, GridSearchCV
from sklearn.metrics import roc_curve, auc, precision_recall_curve
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np

class RandomForestDemo:
    """
    Comprehensive demonstration of Random Forest algorithms.
    """

    def __init__(self, problem_type='classification', random_state=42):
        self.problem_type = problem_type
        self.random_state = random_state
        self.model = None
        self.best_model = None
        self.feature_names = None

    def prepare_data(self, df, target_column, test_size=0.2):
        """Prepare data for Random Forest modeling."""
        X = df.drop(target_column, axis=1)
        y = df[target_column]

        self.feature_names = X.columns.tolist()

        X_train, X_test, y_train, y_test = train_test_split(
            X, y, test_size=test_size, random_state=self.random_state, stratify=y
        )

        print(f"Dataset: {df.shape[0]} samples, {X.shape[1]} features")
        return X_train, X_test, y_train, y_test

    def fit_baseline_model(self, X_train, y_train, n_estimators=100, max_depth=None):
        """
        Fit a baseline Random Forest model.

        Parameters:
        n_estimators (int): Number of trees in the forest
        max_depth (int): Maximum depth of each tree
        """
        if self.problem_type == 'classification':
            self.model = RandomForestClassifier(
                n_estimators=n_estimators,
                max_depth=max_depth,
                random_state=self.random_state,
                n_jobs=-1  # Use all available cores
            )
        else:
            self.model = RandomForestRegressor(
                n_estimators=n_estimators,
                max_depth=max_depth,
                random_state=self.random_state,
                n_jobs=-1
            )

        self.model.fit(X_train, y_train)

        print("=== Baseline Random Forest Model ===")
        print(f"Number of trees: {self.model.n_estimators}")
        print(f"Max depth: {self.model.max_depth}")
        print(f"Number of features: {self.model.n_features_in_}")

        return self.model

    def hyperparameter_tuning(self, X_train, y_train, method='random', n_iter=20):
        """
        Perform hyperparameter tuning for Random Forest.

        Parameters:
        method (str): 'random' for RandomizedSearchCV, 'grid' for GridSearchCV
        n_iter (int): Number of iterations for random search
        """
        # Define parameter distributions
        param_dist = {
            'n_estimators': [50, 100, 200, 300],
            'max_depth': [None, 10, 20, 30, 40],
            'min_samples_split': [2, 5, 10],
            'min_samples_leaf': [1, 2, 4],
            'max_features': ['auto', 'sqrt', 'log2'],
            'bootstrap': [True, False]
        }

        if self.problem_type == 'classification':
            scoring = 'accuracy'
            base_model = RandomForestClassifier(random_state=self.random_state, n_jobs=-1)
        else:
            scoring = 'neg_mean_squared_error'
            base_model = RandomForestRegressor(random_state=self.random_state, n_jobs=-1)

        print(f"Starting {method} search for hyperparameter tuning...")

        if method == 'random':
            search = RandomizedSearchCV(
                base_model, param_dist, n_iter=n_iter, cv=5,
                scoring=scoring, n_jobs=-1, random_state=self.random_state,
                verbose=1
            )
        else:
            # Use a subset of parameters for grid search
            param_grid = {
                'n_estimators': [100, 200],
                'max_depth': [None, 20, 30],
                'min_samples_split': [2, 5],
                'min_samples_leaf': [1, 2]
            }
            search = GridSearchCV(
                base_model, param_grid, cv=5, scoring=scoring, n_jobs=-1, verbose=1
            )

        search.fit(X_train, y_train)

        self.best_model = search.best_estimator_

        print("=== Hyperparameter Tuning Results ===")
        print(f"Best parameters: {search.best_params_}")
        print(f"Best cross-validation score: {search.best_score_:.4f}")

        return self.best_model, search

    def evaluate_model(self, X_test, y_test, model_name="Random Forest"):
        """Evaluate the Random Forest model."""
        model = self.best_model if self.best_model else self.model

        y_pred = model.predict(X_test)

        if self.problem_type == 'classification':
            # Get prediction probabilities for ROC curve
            y_prob = model.predict_proba(X_test)[:, 1]

            accuracy = accuracy_score(y_test, y_pred)
            precision = precision_score(y_test, y_pred)
            recall = recall_score(y_test, y_pred)
            f1 = f1_score(y_test, y_pred)
            auc_score = roc_auc_score(y_test, y_prob)

            print(f"=== {model_name} Classification Results ===")
            print(f"Accuracy:  {accuracy:.4f}")
            print(f"Precision: {precision:.4f}")
            print(f"Recall:    {recall:.4f}")
            print(f"F1-Score:  {f1:.4f}")
            print(f"AUC:       {auc_score:.4f}")

            return {
                'accuracy': accuracy,
                'precision': precision,
                'recall': recall,
                'f1': f1,
                'auc': auc_score
            }
        else:
            mse = mean_squared_error(y_test, y_pred)
            rmse = np.sqrt(mse)
            r2 = r2_score(y_test, y_pred)

            print(f"=== {model_name} Regression Results ===")
            print(f"MSE:  {mse:.4f}")
            print(f"RMSE: {rmse:.4f}")
            print(f"R²:   {r2:.4f}")

            return {'mse': mse, 'rmse': rmse, 'r2': r2}

    def plot_feature_importance(self, top_n=10):
        """Plot feature importance for Random Forest."""
        model = self.best_model if self.best_model else self.model

        importance_df = pd.DataFrame({
            'feature': self.feature_names,
            'importance': model.feature_importances_
        }).sort_values('importance', ascending=False).head(top_n)

        plt.figure(figsize=(10, 6))
        bars = plt.barh(importance_df['feature'], importance_df['importance'])
        plt.xlabel('Feature Importance')
        plt.ylabel('Features')
        plt.title(f'Random Forest Top {top_n} Feature Importance')
        plt.grid(True, alpha=0.3)

        for bar, value in zip(bars, importance_df['importance']):
            plt.text(bar.get_width() + 0.001, bar.get_y() + bar.get_height()/2,
                    '.3f', ha='left', va='center')

        plt.tight_layout()
        plt.show()

    def analyze_bias_variance(self, X_train, y_train, X_test, y_test):
        """
        Analyze bias-variance tradeoff by comparing training and test performance
        across different numbers of trees.
        """
        n_estimators_range = [10, 25, 50, 100, 150, 200]
        train_scores = []
        test_scores = []

        for n_est in n_estimators_range:
            if self.problem_type == 'classification':
                model = RandomForestClassifier(
                    n_estimators=n_est, random_state=self.random_state, n_jobs=-1
                )
                model.fit(X_train, y_train)
                train_score = accuracy_score(y_train, model.predict(X_train))
                test_score = accuracy_score(y_test, model.predict(X_test))
            else:
                model = RandomForestRegressor(
                    n_estimators=n_est, random_state=self.random_state, n_jobs=-1
                )
                model.fit(X_train, y_train)
                train_score = r2_score(y_train, model.predict(X_train))
                test_score = r2_score(y_test, model.predict(X_test))

            train_scores.append(train_score)
            test_scores.append(test_score)

        # Plot bias-variance analysis
        plt.figure(figsize=(10, 6))
        plt.plot(n_estimators_range, train_scores, 'b-', label='Training Score', marker='o')
        plt.plot(n_estimators_range, test_scores, 'r-', label='Test Score', marker='s')
        plt.xlabel('Number of Trees')
        plt.ylabel('Score')
        plt.title('Bias-Variance Analysis: Training vs Test Performance')
        plt.legend()
        plt.grid(True, alpha=0.3)
        plt.show()

        # Find optimal number of trees
        score_diffs = np.array(train_scores) - np.array(test_scores)
        optimal_idx = np.argmin(score_diffs)  # Minimize overfitting gap
        optimal_trees = n_estimators_range[optimal_idx]

        print(f"Suggested optimal number of trees: {optimal_trees}")
        print(".4f")
        print(".4f")

def run_random_forest_demo():
    """Complete demonstration of Random Forest algorithms."""
    # Create sample dataset
    np.random.seed(42)
    n_samples = 1000

    X = pd.DataFrame({
        'age': np.random.normal(35, 10, n_samples).clip(18, 80),
        'income': np.random.exponential(50000, n_samples),
        'credit_score': np.random.normal(650, 50, n_samples).clip(300, 850),
        'debt_ratio': np.random.beta(2, 5, n_samples),
        'employment_years': np.random.exponential(5, n_samples).clip(0, 40)
    })

    # Generate target
    logit = (-3.5 + 0.02 * X['age'] + 0.00003 * X['income'] +
             0.01 * X['credit_score'] - 2.0 * X['debt_ratio'] +
             0.1 * X['employment_years'])
    prob = 1 / (1 + np.exp(-logit))
    y = np.random.binomial(1, prob, n_samples)

    df = X.copy()
    df['approved'] = y

    print("Random Forest demo with loan approval dataset")

    # Initialize demo
    demo = RandomForestDemo(problem_type='classification')

    # Prepare data
    X_train, X_test, y_train, y_test = demo.prepare_data(df, 'approved')

    # Fit baseline model
    baseline_model = demo.fit_baseline_model(X_train, y_train, n_estimators=50)

    # Evaluate baseline
    baseline_metrics = demo.evaluate_model(X_test, y_test, "Baseline Random Forest")

    # Analyze bias-variance tradeoff
    demo.analyze_bias_variance(X_train, y_train, X_test, y_test)

    # Hyperparameter tuning
    best_model, search_results = demo.hyperparameter_tuning(X_train, y_train, method='random', n_iter=10)

    # Evaluate tuned model
    tuned_metrics = demo.evaluate_model(X_test, y_test, "Tuned Random Forest")

    # Plot feature importance
    demo.plot_feature_importance()

    # Compare results
    print("\n=== Model Comparison ===")
    print("Baseline vs Tuned Performance:")
    for metric in ['accuracy', 'precision', 'recall', 'f1', 'auc']:
        baseline_val = baseline_metrics.get(metric, 0)
        tuned_val = tuned_metrics.get(metric, 0)
        improvement = tuned_val - baseline_val
        print(".4f")

    return demo

if __name__ == "__main__":
    demo = run_random_forest_demo()
```

This comprehensive ML tutorial provides detailed explanations and practical implementations of fundamental machine learning concepts, algorithms, and best practices. The code examples are thoroughly documented with comments explaining what each section does and why certain approaches are used.