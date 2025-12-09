# 📌 Data Manipulation with Pandas

This document is a complete, easy-to-use reference for all essential **Pandas functions**, covering data inspection, cleaning, transformation, grouping, merging, and advanced operations.  
Useful for **coding interviews, take-home assignments, and real-world data analysis tasks**.

---

## 1️⃣ Inspecting the Dataset

```python
df.shape                 # (rows, columns)
df.columns               # list column names
df.info()                # data types, non-null counts, memory usage
df.describe()            # summary stats for numeric columns
df.describe(include='all')   # summary for all columns
df.head(n)               # first n rows
df.tail(n)               # last n rows
df.sample(5)             # random sample rows
df.isna()                # missing values as True/False
df.isna().sum()          # missing count per column

---

Data Type Handling:

# To Check all column dtypes
df.dtypes

# To Check dtype of a single column
df['col'].dtype

# Type Conversions 
# df['col'] = df['col'].astype(datatype)   # int, float, str, bool, 'category'

# Convert to datetime
df['col'] = pd.to_datetime(df['col'])

---

# Handling Duplicates:

df.duplicated()  # Find duplicate rows
df.duplicated().sum()  # Count duplicate rows
df[df.duplicated()]  # Display only duplicate rows
df[df.duplicated(subset=['col1', 'col2'], keep=False)]
df = df.drop_duplicates() # Drop duplicates (keep first)
df = df.drop_duplicates(keep='last') # Drop duplicates (keep last)
df = df.drop_duplicates(subset=['col1', 'col2']) # Drop duplicates based on specific columns
df['is_dup'] = df.duplicated() # Mark duplicates

---

2️⃣ Selecting Data

df['col']                        # select single column (Series)
df[['col1','col2']]              # select multiple columns (DataFrame)

df.iloc[2]                       # row by position
df.iloc[2:5]                     # row slice by position
df.loc[101]                      # row by label/index
df.loc[df['col'] > value]        # boolean filtering

df.loc[condition, ['col1','col2']]     # rows + selected columns
df.loc[start:end, :]                   # row range + all columns
df.loc[start:end, 'c1':'c3']           # row & column range

df['col'].unique()               # distinct values


---

3️⃣ Filtering Rows

df[df['col'] > value]                     # single condition
df[(cond1) & (cond2)]                     # AND
df[(cond1) | (cond2)]                     # OR

df['col'].str.startswith('S')
df['col'].str.endswith('a')
df['col'].str.contains('ah')


---

4️⃣ Handling Missing Data

df.isna().sum()              # column-wise missing count
df.isna().sum(axis=1)        # row-wise missing count

df.dropna(subset=['col'], inplace=True)   # drop rows with NaN in column

df['col'].fillna(value, inplace=True)     # fill with constant
df['col'].fillna(df['col'].mean(), inplace=True)
df['col'].fillna(df['col'].median(), inplace=True)
df['col'].fillna(df['col'].mode()[0], inplace=True)

df['col'].fillna(df.groupby('group')['col'].transform('mean'), inplace=True)

df['col'].fillna(method='ffill', inplace=True)  # forward fill
df['col'].fillna(method='bfill', inplace=True)  # backward fill

df['col'] = df['col'].interpolate()             # interpolation


---

5️⃣ Adding / Calculating Columns

df['new'] = value                            # constant
df['new'] = df['c1'] + df['c2'] * 2          # arithmetic formula
df.loc[condition, 'col'] = value             # conditional update
df.loc[(cond1) & (cond2), 'col'] = value


---

6️⃣ Dropping / Renaming Columns

df.drop('col', axis=1, inplace=True)
df.drop(['c1','c2'], axis=1, inplace=True)
df.rename(columns={'old':'new'}, inplace=True)


---

7️⃣ Sorting / Ranking

df.sort_values(by='col')                     # ascending
df.sort_values(by='col', ascending=False)    # descending

df.sort_values(by=['c1','c2'], ascending=[True, False])

df.nlargest(5, 'col')
df.nsmallest(5, 'col')

df.loc[df['col'].idxmax()]                  # row with highest value
df.loc[df['col'].idxmin()]                  # row with lowest value


---

8️⃣ Aggregation & Grouping

df['col'].sum()
df['col'].mean()
df['col'].count()
df['col'].max()
df['col'].min()

df.groupby('group')['col'].mean()

df.groupby(['c1','c2']).agg({'c3':'mean', 'c4':'sum'})

df.loc[df.groupby('group')['value'].idxmax()]   # max per group

pd.pivot_table(df, values='col', index='group', aggfunc='sum')

df.size        # includes NaN
df.count()     # excludes NaN
df.nunique()   # unique count


---

9️⃣ Conditional Updates

df.loc[df['col']==value, 'col2'] = new_value
df.loc[(cond1) & (cond2), 'col'] = new_value


---

🔟 Merging & Combining DataFrames

df1.merge(df2, on='col', how='inner')    # inner, left, right, outer
pd.concat([df1, df2], axis=0)            # vertical stack
pd.concat([df1, df2], axis=1)            # horizontal stack


---

1️⃣1️⃣ Apply Custom Functions

df['new'] = df['col'].apply(lambda x: x*10)   # element-wise

df['combine'] = df.apply(
    lambda row: f"{row['c1']}-{row['c2']}",
    axis=1
)


---

1️⃣2️⃣ Pivot Table (Advanced)

pd.pivot_table(
    data=df,
    values='sales',
    index='region',
    columns='product',
    aggfunc='sum',
    fill_value=0,
    margins=True
)


---

🔹 Extra Interview-Focused Techniques

# Top N items per group
df.groupby('group').apply(lambda x: x.nlargest(3, 'score'))

# Ranking within groups
df['rank'] = df.groupby('team')['points'].rank(ascending=False)

# Cumulative operations
df['cum_sum'] = df['col'].cumsum()
df['cum_mean'] = df['col'].expanding().mean()

# Date handling
df['date'] = pd.to_datetime(df['date'])
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month

# Query-style filtering (very readable)
df.query('age > 25 & salary < 60000')


---

✔️ Suitable For

Coding interview preparation

Face-to-face interview explanations

Machine test / take-home assignments

Data cleaning, preprocessing & analysis



