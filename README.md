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
_Dataset description_: The penguins dataset from seaborn package will be used for this project. 

| species   | island | bill_length_mm | flipper_length_mm  | body_mass_g  | sex |
|-----------|--------|----------------|--------------------|--------------|-----|
|Adelie     |Torgersen|39.1           |18.7                |181           |MALE |
|Adelie     |Torgersen|39.5           |17.4                |186           |FEMALE|
|Adelie     |Torgersen|               |                    |              |      |
|Adelie     |Torgersen|36.7           |19.3                |193           |FEMALE|
|Adelie     |Torgersen|39.3           |20.6                |190           |MALE |
|Adelie     |Torgersen|38.9           |17.8                |181           |FEMALE|


# Start Project

### Step 1. Add .ipynb juypter file
1. Create the Notebook: In the VS Code Explorer, create a new file named jingyuan_eda.ipynb. 
2. Verify the new notebook is open for editing. If needed, view the project files in VS Code Explorer and double-click the notebook file to open it for editing.
3. Add a Markdown cell at the top of your notebook with the introduction (include the title, author, date and the purpose of the project).

### Step 2. Import all dependencies 

```python
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
```

### Step 3. Load the dataset 

Load the data into a pandas DataFrame.

```python
# load the penguins dataset from sns
penguins = sns.load_dataset('penguins')

# see the first five rows
print("dataset size (rows,cols)",penguins.shape)
penguins.head()

#returns the summary of the number of rows/columns, names, and its type
penguins.info()
```

### Step 4. Data cleaning

Display the first 10 rows of the DataFrame, check the shape, and display the data types of each column using df.head(10), df.shape, and df.dtypes.

Jupyter Notebook / Python cell example:

```python

penguins.dropna(inplace=True)
```
### Step 5: Get summary statistics 
```python
penguins.describe(percentiles=[0.25,0.5,0.75,0.95])
penguins.corr()
```

### Step 6: Seaborn Visualization
```python
# to get the proportion of male vs female penguin for each species
sns.catplot(data=penguins,hue="sex",y="species",kind="count",palette='Set2')

# to check if the proportion be the same across all three islands
sns.catplot(data=penguins,hue='sex',y="species",col="island",kind='count',palette='Set2')

# to get the distribution of the penguin’s feature and finding out the correlation between two numerical variables
sns.pairplot(penguins,hue='species',palette='Set2')

# to perform a univariate distribution analysis on the body mass and flipper length. Also see the corresponding density plots on the marginal axes.
sns.jointplot("body_mass_g","flipper_length_mm",data=penguins[Gentoo],kind='reg')
```
Afterwards, use a Markdown cell to document your observations.
