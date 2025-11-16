# Notebook: File-1-Data-Preparation.ipynb
Total cells: 45

## Intro / Title cell (first markdown):
    ![File-1-Google-Play.png](attachment:File-1-Google-Play.png)

## Important cells (automatically detected)
### Cell [29] — type: code — score 3
**Preview (first lines):**
```py
# Data Cleaning and Transformation for the 'Size' Column
apps_data_copy['Size']=apps_data_copy['Size'].str.replace('M','000')
apps_data_copy['Size']=apps_data_copy['Size'].str.replace('k','')
apps_data_copy['Size']=apps_data_copy['Size'].replace("Varies with device",np.nan)
apps_data_copy['Size']=apps_data_copy['Size'].astype('float')
```
**Detected operations / probable purpose:**
- Changes data types of columns (e.g., to numeric or datetime).
- Uses NumPy operations (array math, numerical functions).

### Cell [4] — type: code — score 2
**Preview (first lines):**
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [42] — type: code — score 2
**Preview (first lines):**
```py
apps_data_copy['Last Updated'] = pd.to_datetime(apps_data_copy['Last Updated'])
apps_data_copy['Day'] = apps_data_copy['Last Updated'].dt.day
apps_data_copy['Month'] = apps_data_copy['Last Updated'].dt.month
apps_data_copy['Year'] = apps_data_copy['Last Updated'].dt.year
```
**Detected operations / probable purpose:**
- Parses strings into pandas datetime objects.

### Cell [2] — type: markdown — score 1
**Preview (first lines):**
```py
- Importing Various Modules
- Loading Dataset
- Data Wrangling
    - Computing the size of DataFrame
    - Summary Statistics for Numerical Columns
    - Generating Basic Information of Attributes
```

### Cell [6] — type: code — score 1
**Preview (first lines):**
```py
apps_data = pd.read_csv(r'file1_googleplaystore.csv')
```
**Detected operations / probable purpose:**
- Reads dataset(s) from CSV into a pandas DataFrame.
- Likely dataset loading / initial exploration (check variable names assigned).

### Cell [7] — type: code — score 1
**Preview (first lines):**
```py
# Print top 5 rows in the dataframe.
apps_data.head().style.set_properties(**{'background-color': '#E9F6E2','color': 'black','border-color': '#8b8c8c'})
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.

### Cell [11] — type: code — score 1
**Preview (first lines):**
```py
# Print the shape of the DataFrame
print("The shape of data frame:", apps_data.shape)
# Print the length (number of rows) of the DataFrame
print("Number of Rows in the dataframe:", len(apps_data))
# Print the number of columns in the DataFrame
print("Number of Columns in the dataframe:", len(apps_data.columns))
```

### Cell [13] — type: code — score 1
**Preview (first lines):**
```py
apps_data.describe(include='all')
```
**Detected operations / probable purpose:**
- Generates summary statistics (count, mean, std, min, max, quartiles).

### Cell [14] — type: markdown — score 1
**Preview (first lines):**
```py
### Summary of the dataset

- The described method will help to see how data has been spread for numerical values.
- We can clearly see the minimum value, mean values, different percentile values, and maximum values.
```

### Cell [23] — type: code — score 1
**Preview (first lines):**
```py
# Drop the row with index 10472 from 'apps_data_copy'.
apps_data_copy = apps_data_copy.drop(apps_data_copy.index[10472])
```
**Detected operations / probable purpose:**
- Drops specified columns or rows from a DataFrame.

### Cell [25] — type: code — score 1
**Preview (first lines):**
```py
# Converting Reviews datatype to int 
apps_data_copy["Reviews"] = apps_data_copy["Reviews"].astype(int)
```
**Detected operations / probable purpose:**
- Changes data types of columns (e.g., to numeric or datetime).

### Cell [36] — type: code — score 1
**Preview (first lines):**
```py
# List of characters to remove from specified columns
chars_to_remove = ['+', ',', '$']

# List of columns to clean
cols_to_clean = ['Installs', 'Price']
```

### Cell [37] — type: code — score 1
**Preview (first lines):**
```py
apps_data_copy.head()
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.

### Cell [39] — type: code — score 1
**Preview (first lines):**
```py
apps_data_copy['Installs'] = apps_data_copy['Installs'].astype('int')
apps_data_copy['Price'] = apps_data_copy['Price'].astype('float')
apps_data_copy.info()
```
**Detected operations / probable purpose:**
- Changes data types of columns (e.g., to numeric or datetime).

### Cell [44] — type: code — score 1
**Preview (first lines):**
```py
apps_data_copy.to_csv('file2_googleplaystore_cleaned.csv', index = False)
```
**Detected operations / probable purpose:**
- Writes DataFrame to CSV file.

## Libraries / imports detected (top-level):
- matplotlib.pyplot
- numpy
- pandas
- seaborn
- warnings

## Keywords detected across notebook:
astype, describe, drop, head, matplotlib, np, read_csv, seaborn, to_csv, to_datetime

---



# Notebook: File-2-Data-Visualization.ipynb
Total cells: 84

## Intro / Title cell (first markdown):
    ![File-2-Data-Visualization.jpg](attachment:File-2-Data-Visualization.jpg)

## Important cells (automatically detected)
### Cell [52] — type: code — score 5
**Preview (first lines):**
```py
# Set style and context
sns.set_context("talk")
sns.set_style("whitegrid")

# Create a figure with two subplots
fig, ax = plt.subplots(1, 2, figsize=(20, 7))
```
**Detected operations / probable purpose:**
- Performs aggregation operations grouped by column(s).
- Counts frequency of unique values in a Series/column.
- Creates visualizations (matplotlib/seaborn/plt).
- Counts frequency of unique values in a Series/column.

### Cell [32] — type: code — score 4
**Preview (first lines):**
```py
# Create a DataFrame of app categories and their counts
category = apps_data['Category'].value_counts().reset_index()
category.columns = ['Category', 'Count']

# Sort the DataFrame by Count in descending order
category = category.sort_values(by='Count', ascending=False)
```
**Detected operations / probable purpose:**
- Counts frequency of unique values in a Series/column.
- Creates visualizations (matplotlib/seaborn/plt).
- Counts frequency of unique values in a Series/column.

### Cell [35] — type: code — score 4
**Preview (first lines):**
```py
# Create a DataFrame for category installations
df_cat_installs = apps_data.groupby(['Category'])['Installs'].sum().sort_values(ascending=False).reset_index()
df_cat_installs['Installs (Billions)'] = df_cat_installs['Installs'] / 1e9  # Convert to billions

# Select the top 10 categories
df2 = df_cat_installs.head(10)
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.
- Performs aggregation operations grouped by column(s).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [38] — type: code — score 4
**Preview (first lines):**
```py
dfa = apps_data.groupby(['Category' ,'App'])['Installs'].sum().reset_index()
dfa = dfa.sort_values('Installs', ascending = False)
apps = ['GAME', 'COMMUNICATION', 'PRODUCTIVITY', 'SOCIAL' ]
sns.set_context("poster")
sns.set_style("darkgrid")
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.
- Performs aggregation operations grouped by column(s).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [70] — type: code — score 4
**Preview (first lines):**
```py
# Set style and context
sns.set_context("talk")
sns.set_style("whitegrid")

# Create a figure
plt.figure(figsize=(20, 10))
```
**Detected operations / probable purpose:**
- Counts frequency of unique values in a Series/column.
- Creates visualizations (matplotlib/seaborn/plt).
- Counts frequency of unique values in a Series/column.

### Cell [73] — type: code — score 4
**Preview (first lines):**
```py
# Set style and context
sns.set_context("talk")
sns.set_style("whitegrid")

# Create a figure
plt.figure(figsize=(15, 8))
```
**Detected operations / probable purpose:**
- Counts frequency of unique values in a Series/column.
- Creates visualizations (matplotlib/seaborn/plt).
- Counts frequency of unique values in a Series/column.

### Cell [4] — type: code — score 3
**Preview (first lines):**
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [29] — type: code — score 3
**Preview (first lines):**
```py
import plotly.express as px

# Calculate the category counts
category_counts = apps_data['Category'].value_counts().reset_index()
category_counts.columns = ['Category', 'Count']
```
**Detected operations / probable purpose:**
- Counts frequency of unique values in a Series/column.
- Counts frequency of unique values in a Series/column.

### Cell [41] — type: code — score 3
**Preview (first lines):**
```py
rating = apps_data.groupby(['Category','Installs', 'App'])['Rating'].sum().sort_values(ascending = False).reset_index()

toprating_apps = rating[rating.Rating == 5.0]
print("Number of 5 rated apps",toprating_apps.shape[0])
toprating_apps.head(1)
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.
- Performs aggregation operations grouped by column(s).

### Cell [49] — type: code — score 3
**Preview (first lines):**
```py
df_installs_reviews = apps_data.groupby('Category').agg({'Installs':'sum','Reviews':'sum'})
df_installs_reviews['reviews_percent'] = (df_installs_reviews['Reviews'] / df_installs_reviews['Installs']) * 100
plt.figure(figsize=(25,7))
reviews_df  = df_installs_reviews.sort_values('reviews_percent', ascending=False)['reviews_percent'].plot(kind='bar', title='Percentage of reviews in total install number')
reviews_df.set(ylabel='Percentage(%)')
```
**Detected operations / probable purpose:**
- Performs aggregation operations grouped by column(s).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [60] — type: code — score 3
**Preview (first lines):**
```py
Category_rating= apps_data.groupby('Category').agg({'Rating':'std'}).sort_values('Rating',ascending=False).plot(kind='bar',figsize=(20,7),title='Standard Deviation of the Ratings in Different Category')
Category_rating.set(ylabel='Standard Deviation')
```
**Detected operations / probable purpose:**
- Performs aggregation operations grouped by column(s).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [63] — type: code — score 3
**Preview (first lines):**
```py
# Set style and context
sns.set_context("talk")
sns.set_style("whitegrid")

# Create a figure with two subplots
fig, ax = plt.subplots(1, 2, figsize=(20, 10))
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Uses NumPy operations (array math, numerical functions).

### Cell [21] — type: code — score 2
**Preview (first lines):**
```py
for col in categorical_features:
    print(apps_data[col].value_counts(normalize=True) * 100)
    print('---------------------------')
```
**Detected operations / probable purpose:**
- Counts frequency of unique values in a Series/column.
- Counts frequency of unique values in a Series/column.

### Cell [23] — type: code — score 2
**Preview (first lines):**
```py
# Set the figure size and title
plt.figure(figsize=(15, 15))
plt.suptitle('Univariate Analysis of Numerical Features', fontsize=20, fontweight='bold', alpha=0.8, y=1.02)

# Define the number of rows and columns for subplots
rows, cols = 5, 3
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [26] — type: code — score 2
**Preview (first lines):**
```py
# Set the figure size and title
plt.figure(figsize=(15, 10))
plt.suptitle('Univariate Analysis of Categorical Features', fontsize=20, fontweight='bold', alpha=0.8, y=1.02)

# Define the categorical columns you want to analyze
categorical_columns = ['Type', 'Content Rating']
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [44] — type: code — score 2
**Preview (first lines):**
```py
# Set style and context
sns.set_context("talk")
sns.set_style("whitegrid")

# Create a figure and axis
plt.figure(figsize=(15, 8))
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [46] — type: code — score 2
**Preview (first lines):**
```py
# Set style and context
sns.set_context("talk")
sns.set_style("whitegrid")

# Create a figure and axis
plt.figure(figsize=(12, 9))
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [55] — type: code — score 2
**Preview (first lines):**
```py
# Set style and context
sns.set_context("talk")
sns.set_style("whitegrid")

# Create a figure
plt.figure(figsize=(15, 8))
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [58] — type: code — score 2
**Preview (first lines):**
```py
# Set style and context
sns.set_context("talk")
sns.set_style("whitegrid")

# Create a figure
plt.figure(figsize=(18, 8))
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [67] — type: code — score 2
**Preview (first lines):**
```py
# Set style and context
sns.set_context("talk")
sns.set_style("whitegrid")

# Create a figure
plt.figure(figsize=(14, 7))
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

## Libraries / imports detected (top-level):
- matplotlib.pyplot
- numpy
- pandas
- plotly.express
- seaborn
- warnings

## Keywords detected across notebook:
describe, groupby, head, matplotlib, np, plot, read_csv, seaborn, value_counts, value_counts_attr

---



# Notebook: File-3-Data-Preprocessing.ipynb
Total cells: 58

## Intro / Title cell (first markdown):
    ![File-3-Data-Cleaning.png](attachment:File-3-Data-Cleaning.png)

## Important cells (automatically detected)
### Cell [20] — type: code — score 3
**Preview (first lines):**
```py
# Calculate the fraction of missing data
null_counts = cleaned_apps_data.isna().sum().sort_values(ascending=False) / len(cleaned_apps_data)

# Create a figure with better aesthetics
plt.figure(figsize=(12, 6))
plt.barh(np.arange(len(null_counts)), null_counts, color='skyblue', edgecolor='royalblue')
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Uses NumPy operations (array math, numerical functions).

### Cell [31] — type: code — score 3
**Preview (first lines):**
```py
# Create a figure with subplots
fig, axs = plt.subplots(2, 2, figsize=(15, 7))

# Plot density plots using seaborn
sns.kdeplot(drop_df['Size'], color='red', ax=axs[0, 0], label='Dropped Apps', alpha=0.5)
sns.kdeplot(cleaned_apps_data_copy['Size'], color='green', ax=axs[0, 0], label='Cleaned Apps', alpha=0.5)
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [41] — type: code — score 3
**Preview (first lines):**
```py
# Create a figure with subplots
fig, axs = plt.subplots(2, 2, figsize=(15, 7))

# Plot density plots using seaborn
colors = ['blue', 'green', 'red']
labels = ['Size', 'mean_Size', 'median_Size']
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [52] — type: code — score 3
**Preview (first lines):**
```py
# Create a figure with subplots
fig, axs = plt.subplots(2, 2, figsize=(15, 7))

# Plot density plots using seaborn
colors = ['red', 'green']
labels = ['Size', 'Rating']
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [4] — type: code — score 2
**Preview (first lines):**
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
warnings.filterwarnings("ignore")
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [37] — type: code — score 2
**Preview (first lines):**
```py
cleaned_apps_data_copy_me_mo['mean_Size'] = cleaned_apps_data_copy_me_mo['Size'].fillna(cleaned_apps_data_copy_me_mo['Size'].mean())
cleaned_apps_data_copy_me_mo['median_Size'] = cleaned_apps_data_copy_me_mo['Size'].fillna(cleaned_apps_data_copy_me_mo['Size'].median())
cleaned_apps_data_copy_me_mo['mean_Rating'] = cleaned_apps_data_copy_me_mo['Rating'].fillna(cleaned_apps_data_copy_me_mo['Rating'].mean())
cleaned_apps_data_copy_me_mo['median_Rating'] = cleaned_apps_data_copy_me_mo['Rating'].fillna(cleaned_apps_data_copy_me_mo['Rating'].median())
```
**Detected operations / probable purpose:**
- Fills missing values using a specified method or value.
- This cell handles missing value treatment (imputation or row removal).

### Cell [48] — type: code — score 2
**Preview (first lines):**
```py
def Random_Sample_imputation(feature):
    random_sample=cleaned_apps_data_random[feature].dropna().sample(cleaned_apps_data_random[feature].isnull().sum())               
    random_sample.index=cleaned_apps_data_random[cleaned_apps_data_random[feature].isnull()].index
    cleaned_apps_data_random.loc[cleaned_apps_data_random[feature].isnull(),feature]=random_sample
```
**Detected operations / probable purpose:**
- Drops missing values, possibly to remove incomplete rows.
- This cell handles missing value treatment (imputation or row removal).

### Cell [2] — type: markdown — score 1
**Preview (first lines):**
```py
- Importing Various Modules
- Loading Dataset
- Data Wrangling
    - Computing the size of DataFrame
    - Summary Statistics for Numerical Columns
    - Check for Missing Data
```

### Cell [6] — type: code — score 1
**Preview (first lines):**
```py
cleaned_apps_data = pd.read_csv(r'file2_googleplaystore_cleaned.csv')
```
**Detected operations / probable purpose:**
- Reads dataset(s) from CSV into a pandas DataFrame.
- Likely dataset loading / initial exploration (check variable names assigned).

### Cell [7] — type: code — score 1
**Preview (first lines):**
```py
# Print top 5 rows in the dataframe.
cleaned_apps_data.head().style.set_properties(**{'background-color': '#E9F6E2','color': 'black','border-color': '#8b8c8c'})
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.

### Cell [11] — type: code — score 1
**Preview (first lines):**
```py
# Print the shape of the DataFrame
print("The shape of data frame:", cleaned_apps_data.shape)
# Print the length (number of rows) of the DataFrame
print("Number of Rows in the dataframe:", len(cleaned_apps_data))
# Print the number of columns in the DataFrame
print("Number of Columns in the dataframe:", len(cleaned_apps_data.columns))
```

### Cell [13] — type: code — score 1
**Preview (first lines):**
```py
# Summarize the statistics.
cleaned_apps_data.describe(include='all')
```
**Detected operations / probable purpose:**
- Generates summary statistics (count, mean, std, min, max, quartiles).

### Cell [14] — type: markdown — score 1
**Preview (first lines):**
```py
### Summary of the dataset

- The described method will help to see how data has been spread for numerical values.
- We can clearly see the minimum value, mean values, different percentile values, and maximum values.
```

### Cell [18] — type: code — score 1
**Preview (first lines):**
```py
null_df = pd.DataFrame({'Null Values' : cleaned_apps_data.isna().sum().sort_values(ascending=False), 'Percentage Null Values' : (cleaned_apps_data.isna().sum().sort_values(ascending=False)) / (cleaned_apps_data.shape[0]) * (100)})
null_df
```

### Cell [29] — type: code — score 1
**Preview (first lines):**
```py
drop_df = cleaned_apps_data_copy[cols].dropna()
drop_df
```
**Detected operations / probable purpose:**
- Drops missing values, possibly to remove incomplete rows.
- This cell handles missing value treatment (imputation or row removal).

### Cell [38] — type: code — score 1
**Preview (first lines):**
```py
print('Original Size Variance', cleaned_apps_data_copy_me_mo['Size'].var())
print('Size Variance After mean imputation', cleaned_apps_data_copy_me_mo['mean_Size'].var())
print('Size Variance After median imputation', cleaned_apps_data_copy_me_mo['median_Size'].var())
```

### Cell [39] — type: code — score 1
**Preview (first lines):**
```py
print('Original Rating Variance', cleaned_apps_data_copy_me_mo['Rating'].var())
print('Rating Variance After mean imputation', cleaned_apps_data_copy_me_mo['mean_Rating'].var())
print('Rating Variance After median imputation', cleaned_apps_data_copy_me_mo['median_Rating'].var())
```

### Cell [45] — type: code — score 1
**Preview (first lines):**
```py
cleaned_apps_data_random['Size'].dropna().sample(20)
```
**Detected operations / probable purpose:**
- Drops missing values, possibly to remove incomplete rows.
- This cell handles missing value treatment (imputation or row removal).

### Cell [47] — type: code — score 1
**Preview (first lines):**
```py
cleaned_apps_data_random['Size'].dropna().sample(1695)
```
**Detected operations / probable purpose:**
- Drops missing values, possibly to remove incomplete rows.
- This cell handles missing value treatment (imputation or row removal).

### Cell [53] — type: code — score 1
**Preview (first lines):**
```py
null_df = pd.DataFrame({'Null Values' : cleaned_apps_data_random.isna().sum().sort_values(ascending=False), 'Percentage Null Values' : (cleaned_apps_data_random.isna().sum().sort_values(ascending=False)) / (cleaned_apps_data_random.shape[0]) * (100)})
null_df
```

## Libraries / imports detected (top-level):
- matplotlib.pyplot
- numpy
- pandas
- seaborn
- warnings

## Keywords detected across notebook:
describe, dropna, fillna, head, matplotlib, np, plot, read_csv, seaborn, to_csv

---



# Notebook: File-4-Feature-Engineering.ipynb
Total cells: 40

## Intro / Title cell (first markdown):
    ![File-4-Feature-Engineering.png](attachment:File-4-Feature-Engineering.png)

## Important cells (automatically detected)
### Cell [11] — type: code — score 4
**Preview (first lines):**
```py
# Set the figure size
plt.figure(figsize=(12, 8))

# Define a custom color palette
custom_palette = sns.diverging_palette(220, 20, n=20)
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Shows a heatmap (often for correlation matrices).
- Computes pairwise correlation of columns.

### Cell [4] — type: code — score 3
**Preview (first lines):**
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import scipy.stats as stats
import warnings
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [12] — type: code — score 3
**Preview (first lines):**
```py
# Create a copy of the DataFrame
preprocessed_apps_data_copy = preprocessed_apps_data.copy()

# Filter the data to remove outliers
preprocessed_apps_data_copy = preprocessed_apps_data_copy[(preprocessed_apps_data_copy['Reviews'] > 10) & (preprocessed_apps_data_copy['Installs'] > 0)]
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Uses NumPy operations (array math, numerical functions).

### Cell [15] — type: code — score 2
**Preview (first lines):**
```py
# List of numeric features
numeric_features = [feature for feature in preprocessed_apps_data.columns if preprocessed_apps_data[feature].dtype != 'O']

# Create a figure with subplots
plt.figure(figsize=(15, 15))
plt.suptitle('Distribution of Numerical Features', fontsize=20, fontweight='bold', alpha=0.8, y=1.)
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [25] — type: code — score 2
**Preview (first lines):**
```py
# Define a function to plot QQ and PDF
def plot_qq_plot(column):
    # Create a figure with subplots
    plt.figure(figsize=(14, 6))
    
    # Create the PDF plot
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [28] — type: code — score 2
**Preview (first lines):**
```py
def plots(preprocessed_apps_data, var, transformer):
    # Set a custom color palette
    custom_palette = sns.color_palette("husl")

    # Create a figure with two subplots
    plt.figure(figsize=(13, 5))
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [38] — type: code — score 2
**Preview (first lines):**
```py
def power_plots(preprocessed_apps_data,var,t):
    plt.figure(figsize=(13,5))
    plt.subplot(121)
    sns.kdeplot(preprocessed_apps_data[var])
    plt.title('before ' + str(t))
    plt.subplot(122)
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [2] — type: markdown — score 1
**Preview (first lines):**
```py
- Importing Various Modules
- Loading Dataset
- Check Correlation using Heatmap
- Hypothesis Testing ( Check Normal Distribution )
    - Shapiro Wick Test
    - K^2 Normality Test
```

### Cell [6] — type: code — score 1
**Preview (first lines):**
```py
preprocessed_apps_data = pd.read_csv(r'file3_googleplaystore_preprocessed.csv')
```
**Detected operations / probable purpose:**
- Reads dataset(s) from CSV into a pandas DataFrame.
- Likely dataset loading / initial exploration (check variable names assigned).

### Cell [7] — type: code — score 1
**Preview (first lines):**
```py
# Print top 5 rows in the dataframe.
preprocessed_apps_data.head().style.set_properties(**{'background-color': '#E9F6E2','color': 'black','border-color': '#8b8c8c'})
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.

### Cell [9] — type: code — score 1
**Preview (first lines):**
```py
# Print the shape of the DataFrame
print("The shape of data frame:", preprocessed_apps_data.shape)
# Print the length (number of rows) of the DataFrame
print("Number of Rows in the dataframe:", len(preprocessed_apps_data))
# Print the number of columns in the DataFrame
print("Number of Columns in the dataframe:", len(preprocessed_apps_data.columns))
```

### Cell [13] — type: markdown — score 1
**Preview (first lines):**
```py
### Insights

**A High positive correlation of 0.9 exists between the number of reviews and number of downloads.** 

- This means that customers tend to download a given app more if it has been reviewed by a larger number of people.
```

### Cell [19] — type: code — score 1
**Preview (first lines):**
```py
from scipy.stats import shapiro
shapiro_wick_test = []
for column in features_to_plot:
    dataToTest = num_df[column]
    stat,p = shapiro(dataToTest)
    if p > 0.05:
```

### Cell [21] — type: markdown — score 1
**Preview (first lines):**
```py
**Test aims to establish whether or not the given sample comes from a normally distributed population. Test is based on transformations of the sample kurtosis and skewness.**
- Ho : Data is normally distributed
- H1 : Data is not normally distributed
```

### Cell [22] — type: code — score 1
**Preview (first lines):**
```py
from scipy.stats import normaltest
normaltest_test = []
for column in features_to_plot:
    dataToTest = num_df[column]
    stat,p = normaltest(dataToTest)
    if p > 0.05:
```

### Cell [24] — type: markdown — score 1
**Preview (first lines):**
```py
**A Q-Q plot is a scatterplot created by plotting two sets of quantiles against one another. If both sets of quantiles came from the same distribution, we should see the points forming a roughly straight line.**

**If the data falls in a straight line then the variable follows normal distribution otherwise not.**
```

### Cell [31] — type: code — score 1
**Preview (first lines):**
```py
log_transformer = FunctionTransformer(np.log1p)
for col in features_to_plot:
    X = np.array(preprocessed_apps_data[col])
    Y = log_transformer.transform(X)
    plots(preprocessed_apps_data,col,Y)
```
**Detected operations / probable purpose:**
- Uses NumPy operations (array math, numerical functions).

### Cell [35] — type: code — score 1
**Preview (first lines):**
```py
log_transformer = FunctionTransformer(np.sqrt)
for col in features_to_plot:
    X = np.array(preprocessed_apps_data[col])
    Y = log_transformer.transform(X)
    plots(preprocessed_apps_data,col,Y)
```
**Detected operations / probable purpose:**
- Uses NumPy operations (array math, numerical functions).

## Libraries / imports detected (top-level):
- matplotlib.pyplot
- numpy
- pandas
- scipy.stats
- seaborn
- sklearn.preprocessing
- warnings

## Keywords detected across notebook:
corr, head, matplotlib, np, plot, read_csv, seaborn, sns_heatmap

---



# Notebook: File-5-Outlier-Detection-and-Approach.ipynb
Total cells: 42

## Intro / Title cell (first markdown):
    ![File-5-Outlier-Detection-and-Approach.png](attachment:File-5-Outlier-Detection-and-Approach.png)

## Important cells (automatically detected)
### Cell [4] — type: code — score 2
**Preview (first lines):**
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [15] — type: code — score 2
**Preview (first lines):**
```py
plt.figure(figsize=(22, 18))

# Specify the number of rows and columns in the subplot grid
num_rows = 4
num_cols = 9
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [20] — type: code — score 2
**Preview (first lines):**
```py
plt.figure(figsize=(22, 18))

# Specify the number of rows and columns in the subplot grid
num_rows = 4
num_cols = 9
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [23] — type: code — score 2
**Preview (first lines):**
```py
# Set a common style for all plots
sns.set(style="whitegrid")

for col in num_df.columns:
    # Create a figure with a specific size for each boxplot
    plt.figure(figsize=(12, 4))
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [24] — type: code — score 2
**Preview (first lines):**
```py
preprocessed_apps_data_1 = preprocessed_apps_data.copy()
def remove_outliers_IQR(col):
    # Finding the IQR
    percentile25 = preprocessed_apps_data_1[col].quantile(0.25)
    percentile75 = preprocessed_apps_data_1[col].quantile(0.75)
    print("percentile25",percentile25)
```
**Detected operations / probable purpose:**
- Uses NumPy operations (array math, numerical functions).

### Cell [25] — type: code — score 2
**Preview (first lines):**
```py
def create_comparison_plot(preprocessed_apps_data, preprocessed_apps_data_1, column, name1="DataFrame 1", name2="DataFrame 2"):
    # Set a common style for all plots
    sns.set(style="whitegrid")

    # Create a figure with a specific size
    fig, axes = plt.subplots(2, 2, figsize=(16, 8))
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [2] — type: markdown — score 1
**Preview (first lines):**
```py
- Importing Various Modules
- Loading Dataset
- Data Wrangling
    - Computing the size of DataFrame
    - Z-Score
    - Interquartile Range Method (IQR)
```

### Cell [6] — type: code — score 1
**Preview (first lines):**
```py
preprocessed_apps_data = pd.read_csv(r'file3_googleplaystore_preprocessed.csv')
```
**Detected operations / probable purpose:**
- Reads dataset(s) from CSV into a pandas DataFrame.
- Likely dataset loading / initial exploration (check variable names assigned).

### Cell [7] — type: code — score 1
**Preview (first lines):**
```py
# Print top 5 rows in the dataframe.
preprocessed_apps_data.head().style.set_properties(**{'background-color': '#E9F6E2','color': 'black','border-color': '#8b8c8c'})
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.

### Cell [11] — type: code — score 1
**Preview (first lines):**
```py
# Print the shape of the DataFrame
print("The shape of data frame:", preprocessed_apps_data.shape)
# Print the length (number of rows) of the DataFrame
print("Number of Rows in the dataframe:", len(preprocessed_apps_data))
# Print the number of columns in the DataFrame
print("Number of Columns in the dataframe:", len(preprocessed_apps_data.columns))
```

### Cell [13] — type: markdown — score 1
**Preview (first lines):**
```py
- The number of standard deviations away from the mean that a particular observation is.
- A negative Z-score means an observation is below the mean.
- While a positive Z-score means means it above the mean.
- The further away from 0 the Z-Score is, the further away from the mean your observation is.
```

### Cell [14] — type: code — score 1
**Preview (first lines):**
```py
num_features=[col for col in preprocessed_apps_data.columns if preprocessed_apps_data[col].dtype!='O']
num_df = preprocessed_apps_data[num_features]
num_df.head()
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.

### Cell [17] — type: code — score 1
**Preview (first lines):**
```py
# Function to detect outliers
def outlier_thresholds(dataframe, variable):
    quartile1 = dataframe[variable].quantile(0.10)
    quartile3 = dataframe[variable].quantile(0.90)
    interquantile_range = quartile3 - quartile1
    up_limit = quartile3 + 1.5 * interquantile_range
```

### Cell [18] — type: code — score 1
**Preview (first lines):**
```py
## function to remove outliers
def replace_with_thresholds(dataframe, numeric_columns):
    for variable in numeric_columns:
        low_limit, up_limit = outlier_thresholds(dataframe, variable)
        dataframe.loc[(dataframe[variable] < low_limit), variable] = low_limit
        dataframe.loc[(dataframe[variable] > up_limit), variable] = up_limit
```

### Cell [41] — type: code — score 1
**Preview (first lines):**
```py
preprocessed_apps_data_1.to_csv('file4_googleplaystore.csv',index=False)
```
**Detected operations / probable purpose:**
- Writes DataFrame to CSV file.

## Libraries / imports detected (top-level):
- matplotlib.pyplot
- numpy
- pandas
- seaborn
- warnings

## Keywords detected across notebook:
head, matplotlib, np, plot, read_csv, seaborn, to_csv

---



# Notebook: File-6-Data-Modeling.ipynb
Total cells: 55

## Intro / Title cell (first markdown):
    ![File-6-Data-Modeling.png](attachment:File-6-Data-Modeling.png)

## Important cells (automatically detected)
### Cell [4] — type: code — score 3
**Preview (first lines):**
```py
# Data
import numpy as np
import pandas as pd
from collections import defaultdict

# Visualization
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [11] — type: code — score 2
**Preview (first lines):**
```py
apps_data['Content Rating'].value_counts()
```
**Detected operations / probable purpose:**
- Counts frequency of unique values in a Series/column.
- Counts frequency of unique values in a Series/column.

### Cell [37] — type: code — score 2
**Preview (first lines):**
```py
# Reset the index
data = df_metrics_reg.reset_index()

# Set a beautiful color palette
custom_palette = sns.color_palette("Set2")
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [54] — type: code — score 2
**Preview (first lines):**
```py
# Reset the index
data = df_metrics_clf.reset_index()

# Set a beautiful color palette
custom_palette = sns.color_palette("Set2")
```
**Detected operations / probable purpose:**
- Creates visualizations (matplotlib/seaborn/plt).

### Cell [6] — type: code — score 1
**Preview (first lines):**
```py
apps_data = pd.read_csv(r'file4_googleplaystore.csv')
```
**Detected operations / probable purpose:**
- Reads dataset(s) from CSV into a pandas DataFrame.
- Likely dataset loading / initial exploration (check variable names assigned).

### Cell [7] — type: code — score 1
**Preview (first lines):**
```py
# Print top 5 rows in the dataframe.
apps_data.head().style.set_properties(**{'background-color': '#E9F6E2','color': 'black','border-color': '#8b8c8c'})
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.

### Cell [9] — type: code — score 1
**Preview (first lines):**
```py
# Print the shape of the DataFrame
print("The shape of data frame:", apps_data.shape)
# Print the length (number of rows) of the DataFrame
print("Number of Rows in the dataframe:", len(apps_data))
# Print the number of columns in the DataFrame
print("Number of Columns in the dataframe:", len(apps_data.columns))
```

### Cell [13] — type: code — score 1
**Preview (first lines):**
```py
# Print top 5 rows in the dataframe.
apps_data.head().style.set_properties(**{'background-color': '#E9F6E2','color': 'black','border-color': '#8b8c8c'})
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.

### Cell [15] — type: code — score 1
**Preview (first lines):**
```py
X = apps_data.drop(columns=['App','Category','Rating', 'Genres', "Last Updated","Current Ver","Android Ver","Day","Month","Year"],axis=1)
```
**Detected operations / probable purpose:**
- Drops specified columns or rows from a DataFrame.

### Cell [16] — type: code — score 1
**Preview (first lines):**
```py
X.head().style.set_properties(**{'background-color': '#E9F6E2','color': 'black','border-color': '#8b8c8c'})
```
**Detected operations / probable purpose:**
- Shows the first few rows of a DataFrame for inspection.

### Cell [18] — type: code — score 1
**Preview (first lines):**
```py
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=.3, random_state=42)
```
**Detected operations / probable purpose:**
- Splits data into training and testing sets for modeling.
- This cell belongs to modeling / evaluation stage.

### Cell [21] — type: code — score 1
**Preview (first lines):**
```py
models = ['Linear', 'KNN', 'Random Forest']
datasets = ['train', 'test']
metrics = ['RMSE', 'MAE', 'R2']

multi_index = pd.MultiIndex.from_product([models, datasets, metrics],
                                         names=['model', 'dataset', 'metric'])
```

### Cell [26] — type: code — score 1
**Preview (first lines):**
```py
y_train_pred = lr.predict(X_train)
y_test_pred = lr.predict(X_test)

df_metrics_reg.loc['Linear', 'train', 'MAE'] = mean_absolute_error(y_train, y_train_pred)
df_metrics_reg.loc['Linear', 'test', 'MAE'] = mean_absolute_error(y_test, y_test_pred)
```

### Cell [30] — type: code — score 1
**Preview (first lines):**
```py
y_train_pred = knn.predict(X_train)
y_test_pred = knn.predict(X_test)

df_metrics_reg.loc['KNN', 'train', 'MAE'] = mean_absolute_error(y_train, y_train_pred)
df_metrics_reg.loc['KNN', 'test', 'MAE'] = mean_absolute_error(y_test, y_test_pred)
```

### Cell [32] — type: code — score 1
**Preview (first lines):**
```py
rf = RandomForestRegressor(max_depth=2, random_state=0)
rf.fit(X_train, y_train)
```
**Detected operations / probable purpose:**
- Trains Random Forest model for classification/regression.
- This cell belongs to modeling / evaluation stage.

### Cell [34] — type: code — score 1
**Preview (first lines):**
```py
y_train_pred = rf.predict(X_train)
y_test_pred = rf.predict(X_test)

df_metrics_reg.loc['Random Forest', 'train', 'MAE'] = mean_absolute_error(y_train, y_train_pred)
df_metrics_reg.loc['Random Forest', 'test', 'MAE'] = mean_absolute_error(y_test, y_test_pred)
```

### Cell [40] — type: code — score 1
**Preview (first lines):**
```py
y_train_int = y_train.astype(int)
y_test_int = y_test.astype(int)
```
**Detected operations / probable purpose:**
- Changes data types of columns (e.g., to numeric or datetime).

### Cell [41] — type: code — score 1
**Preview (first lines):**
```py
models = ['Logistic Regression', 'KNN', 'Random Forest']
datasets = ['train', 'test']

multi_index = pd.MultiIndex.from_product([models, datasets],
                                         names=['model', 'dataset'])
```

### Cell [44] — type: code — score 1
**Preview (first lines):**
```py
lr_clf = LogisticRegression()
lr_clf.fit(X_train, y_train_int)
```
**Detected operations / probable purpose:**
- Trains logistic regression model (classification).

### Cell [50] — type: code — score 1
**Preview (first lines):**
```py
rf_clf = RandomForestClassifier()
rf_clf.fit(X_train, y_train_int)
```
**Detected operations / probable purpose:**
- Trains Random Forest model for classification/regression.
- This cell belongs to modeling / evaluation stage.

## Libraries / imports detected (top-level):
- collections
- matplotlib.pyplot
- numpy
- pandas
- seaborn
- sklearn.ensemble
- sklearn.linear_model
- sklearn.metrics
- sklearn.model_selection
- sklearn.neighbors
- sklearn.preprocessing
- warnings

## Keywords detected across notebook:
LogisticRegression, RandomForest, astype, drop, head, matplotlib, plot, read_csv, seaborn, train_test_split, value_counts, value_counts_attr

---

