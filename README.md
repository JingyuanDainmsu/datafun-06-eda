# datafun-06-eda
_Overview_:
Project 6 focuses on creating your own custom exploratory data analysis (EDA) project using GitHub, Git, Jupyter, pandas, Seaborn and other popular data analytics tools. 

_Objective_:
Perform and publish a custom EDA project to demnostrate skills with Jupyter, pandas, Seaborn and popular tools for data analytics. The notebook should tell a data story and visually present findings in a clear and engaging manner. 

_Setting up environment_: 
### Create Virtual Environment

```shell

py -m venv .venv
.venv\Scripts\Activate
```

### Add dependencies

```shell

py -m pip install jupyterlab numpy pandas pyarrow matplotlib seaborn scipy
```

### Freeze dependencies

```shell

py -m pip freeze > requirements.txt
```

```
_Dataset description_:

species,island,bill_length_mm,bill_depth_mm,flipper_length_mm,body_mass_g,sex
Adelie,Torgersen,39.1,18.7,181,3750,MALE
Adelie,Torgersen,39.5,17.4,186,3800,FEMALE
Adelie,Torgersen,40.3,18,195,3250,FEMALE
Adelie,Torgersen,,,,,
Adelie,Torgersen,36.7,19.3,193,3450,FEMALE
Adelie,Torgersen,39.3,20.6,190,3650,MALE
Adelie,Torgersen,38.9,17.8,181,3625,FEMALE
Adelie,Torgersen,39.2,19.6,195,4675,MALE
Adelie,Torgersen,34.1,18.1,193,3475,
Adelie,Torgersen,42,20.2,190,4250,
Adelie,Torgersen,37.8,17.1,186,3300,
Adelie,Torgersen,37.8,17.3,180,3700,
Adelie,Torgersen,41.1,17.6,182,3200,FEMALE
Adelie,Torgersen,38.6,21.2,191,3800,MALE
Adelie,Torgersen,34.6,21.1,198,4400,MALE
Adelie,Torgersen,36.6,17.8,185,3700,FEMALE
Adelie,Torgersen,38.7,19,195,3450,FEMALE
Adelie,Torgersen,42.5,20.7,197,4500,MALE
Adelie,Torgersen,34.4,18.4,184,3325,FEMALE
Adelie,Torgersen,46,21.5,194,4200,MALE
Adelie,Biscoe,37.8,18.3,174,3400,FEMALE
Adelie,Biscoe,37.7,18.7,180,3600,MALE
Adelie,Biscoe,35.9,19.2,189,3800,FEMALE
Adelie,Biscoe,38.2,18.1,185,3950,MALE
Adelie,Biscoe,38.8,17.2,180,3800,MALE
Adelie,Biscoe,35.3,18.9,187,3800,FEMALE
Adelie,Biscoe,40.6,18.6,183,3550,MALE
Adelie,Biscoe,40.5,17.9,187,3200,FEMALE
Adelie,Biscoe,37.9,18.6,172,3150,FEMALE
Adelie,Biscoe,40.5,18.9,180,3950,MALE
Adelie,Dream,39.5,16.7,178,3250,FEMALE
Adelie,Dream,37.2,18.1,178,3900,MALE

# Start Project

### Step 1. Add juypter file
1. Create the Notebook: In the VS Code Explorer, create a new file i.e., yourname_eda.ipynb. Ensure it has a .ipynb extension.
2. Verify your new notebook is open for editing. If needed, view the project files in VS Code Explorer and double-click the notebook file to open it for editing.
3. Add a Markdown cell at the top of your notebook with the introduction (include the title, author, date and the purpose of the project).

```shell
ni blehman_eda.ipynb
```

### Step 2. Import Dependencies (At the Top, After the Introduction)

```python
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
```

### Step 3. Data Acquisition

Load the data into a pandas DataFrame.
Use the pd read functions such as pd.read_csv() or pd.read_excel() as appropriate.
To read from the Seaborn dataset, we'll use sns.load_dataset() function and pass in the 'titanic' to populate our DataFrame.

Jupyter Notebook / Python cell example:

```python
# Load the dataset into a pandas DataFrame 
df = sns.load_dataset('titanic')

# Inspect first rows of the DataFrame
print(df.head())
```

### Step 4. Initial Data Inspection

Display the first 10 rows of the DataFrame, check the shape, and display the data types of each column using df.head(10), df.shape, and df.dtypes.

Jupyter Notebook / Python cell example:

```python

print(df.head(10))
print(df.shape)
print(df.dtypes)
```
### Step 5. Initial Descriptive Statistics

Use the DataFrame describe() method to display summary statistics for each column.

Jupyter Notebook / Python cell example:

```python
print(df.describe())
```

### Step 6. Initial Data Distribution for Numerical Columns

Choose a numerical column and use df['column_name'].hist() to plot a histogram for that specific column.
To show all the histograms for all numerical columns, use df.hist().

Jupyter Notebook / Python cell example:

```python
# Inspect histogram by numerical column
df['survived'].hist()
plt.xlabel('Survival (0 = No, 1 = Yes)')
plt.ylabel('Frequency')
plt.title('Distribution of Survival')

# Inspect histograms for all numerical columns
df.hist()

# Function to help with not overlapping of subplots
plt.tight_layout()

# Show all plots
plt.show()
```
Afterwards, use a Markdown cell to document your observations.

### Step 7. 

Choose a categorical column and use df['column_name'].value_counts() to display the count of each category.
Use a loop to show the value counts for **all** categorical columns.

Jupyter Notebook / Python cell example:

```python
# Initial Data Distribution for Categorical Columns

# Inspect value counts by categorical column
df['who'].value_counts()

# Inspect value counts for all categorical columns
for col in df.select_dtypes(include=['object', 'category']).columns:
    # Display count plot
    sns.countplot(x=col, data=df)
    plt.title(f'Distribution of {col}')
    plt.show()

# Show all plots
plt.show()
```

## Data transformation

### Renaming column

```python
def rename_column(df, old_column, new_column):
    df = df.rename(columns={old_column: new_column})
    return df

# Rename the 'sibsp' column to 'siblings_spouses_aboard'
df = rename_column(df, 'sibsp', 'siblings_spouses_aboard')

print(df.dtypes)
```
### Inserting a column

```python 
# Insert a new column

# Insert a new column 'new_column' with dummy values
df['first_time_passenger'] = 'yes'

# Print the DataFrame to verify the new column
print(df.head())
```

## Initial Visualizations

```python
# Barplot of Survival by Passenger Class
sns.barplot(x="pclass", y="survived", data=df);
```

```python
# Barplot of Survival by Passenger Class
sns.barplot(x="sex", y="survived", data=df);
```

```python
# Define age categories 
bins = [0, 18, 30, 50, 100]
labels = ['0-18', '19-30', '31-50', '51+']

# Create a pie chart
plt.pie(age_counts, labels=age_counts.index, autopct='%1.1f%%', startangle=90, colors=plt.cm.Paired.colors)
plt.title('Age Distribution in Titanic Dataset')
plt.show()
```
```python
# Set up the Seaborn style
sns.set(style="whitegrid")

# Create a scatter plot with hue encoding for passenger class and survival status
plt.figure(figsize=(12, 8))
scatter_plot = sns.scatterplot(x='age', y='survived', hue='pclass', data=df_age_notnull, palette='viridis', alpha=1)

# Customize the plot
plt.title('Age vs. Survival by Passenger Class')
plt.xlabel('Age')
plt.ylabel('Survived (0 = No, 1 = Yes)')
plt.legend(title='Passenger Class')

# Show the plot
plt.show()
```
