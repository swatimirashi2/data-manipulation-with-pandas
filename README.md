📘 Data Manipulation With Pandas 

Perfect for daily revision, exams, coding rounds, projects, and real data analysis.


---

1️⃣ Importing & Loading Data

import pandas as pd

df = pd.read_csv('file.csv')
df = pd.read_excel('file.xlsx')
df = pd.read_json('file.json')
df = pd.read_sql(query, connection)
df = pd.read_parquet('file.parquet')


---

2️⃣ Basic Dataset Inspection

df.shape
df.columns
df.index
df.info()
df.describe()
df.describe(include='all')
df.head()
df.tail()
df.sample(5)


---

3️⃣ Data Types & Conversions

df.dtypes
df['col'].dtype

df['col'] = df['col'].astype('int/float/str/bool/category')
df['col'] = pd.to_datetime(df['col'])
df['col'] = pd.to_numeric(df['col'], errors='coerce')
df['col'] = df['col'].astype('category')


---

4️⃣ Selecting Data (Rows & Columns)

Columns

df['col']
df[['c1','c2']]
df.filter(like='sales')
df.filter(regex='^A')   # columns starting with A

Rows

df.iloc[3]
df.iloc[2:8]
df.loc[100]
df.loc[df['age'] > 25]
df.loc[(df['age'] > 25) & (df['city']=='Pune')]

Unique & Counts

df['col'].unique()
df['col'].nunique()
df['col'].value_counts()
df['col'].value_counts(normalize=True)


---

5️⃣ Filtering Techniques

Comparison

df[df['col'] > 10]
df[(df['age'] > 25) & (df['salary'] < 40000)]

String filters

df['name'].str.startswith('A')
df['name'].str.endswith('h')
df['name'].str.contains('ra')
df['name'].str.upper()
df['name'].str.lower()

Regex

df['col'].str.extract('(\d+)')
df['email'].str.contains('@gmail', regex=True)


---

6️⃣ Missing Data Handling

Check

df.isna().sum()
df.notna().sum()
df.isna().mean()

Drop

df.dropna()
df.dropna(subset=['col'])
df.dropna(how='all')

Fill

df['col'].fillna(0)
df['col'].fillna(df['col'].mean())
df['col'].fillna(df['col'].median())
df['col'].fillna(df['col'].mode()[0])

Forward / Backward fill

df.fillna(method='ffill')
df.fillna(method='bfill')

Group-wise fill

df['val'] = df.groupby('city')['val'].transform(lambda x: x.fillna(x.mean()))


---

7️⃣ Duplicate Handling

df.duplicated()
df.duplicated().sum()
df[df.duplicated()]
df.drop_duplicates()
df.drop_duplicates(subset=['c1','c2'], keep='last')


---

8️⃣ Creating, Updating, Replacing Columns

Create

df['new'] = df['a'] + df['b']
df['price_total'] = df['qty'] * df['price']

Update with condition

df.loc[df['age'] > 50, 'group'] = 'Senior'
df.loc[df['score'] < 40, 'grade'] = 'Fail'

Replace

df['col'].replace({'M': 'Male', 'F': 'Female'})
df['col'].replace([1,2,3], ['Low','Med','High'])

Map

df['gender_text'] = df['gender'].map({1: 'Male', 2: 'Female'})


---

9️⃣ Removing / Renaming Columns

df.drop('col', axis=1)
df.drop(['c1','c2'], axis=1)
df.rename(columns={'old':'new'})
df.columns = df.columns.str.lower()
df.columns = df.columns.str.replace(' ','_')


---

🔟 Sorting & Ranking

df.sort_values('salary')
df.sort_values('salary', ascending=False)
df.sort_values(['city','salary'], ascending=[True, False])

df.nlargest(5, 'score')
df.nsmallest(5, 'score')

df['rank'] = df['score'].rank(ascending=False)
df.loc[df['score'].idxmax()]
df.loc[df['score'].idxmin()]


---

1️⃣1️⃣ GroupBy & Aggregations

Single column

df.groupby('region')['sales'].sum()

Multiple aggregations

df.groupby('city').agg({
    'sales':'sum',
    'profit':'mean',
    'qty':'count'
})

Group max record

df.loc[df.groupby('city')['sales'].idxmax()]

Cumulative operations

df['cum_sum'] = df['sales'].cumsum()
df['cum_mean'] = df['sales'].expanding().mean()


---

1️⃣2️⃣ Pivot Tables

pd.pivot_table(
    df,
    values='sales',
    index='region',
    columns='product',
    aggfunc='sum',
    fill_value=0,
    margins=True
)


---

1️⃣3️⃣ Merging / Joining DataFrames

df1.merge(df2, on='id', how='inner')
df1.merge(df2, how='left', on='id')
df1.merge(df2, how='right', on='id')
df1.merge(df2, how='outer', on='id')

Concat

pd.concat([df1, df2], axis=0)
pd.concat([df1, df2], axis=1)


---

1️⃣4️⃣ Apply, Lambda, Functions

df['new'] = df['col'].apply(lambda x: x*10)

df['full'] = df.apply(
    lambda r: r['first'] + " " + r['last'], axis=1
)

df.applymap(lambda x: x*2)     # element-wise on DataFrame


---

1️⃣5️⃣ Date & Time Handling

df['date'] = pd.to_datetime(df['date'])

df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df['day'] = df['date'].dt.day
df['day_name'] = df['date'].dt.day_name()

df['is_month_end'] = df['date'].dt.is_month_end
df['is_month_start'] = df['date'].dt.is_month_start


---

1️⃣6️⃣ Window Functions

df['rolling_mean'] = df['sales'].rolling(3).mean()
df['rolling_sum'] = df['sales'].rolling(5).sum()
df['expanding_sum'] = df['sales'].expanding().sum()


---

1️⃣7️⃣ Binning / Categorization

df['age_group'] = pd.cut(
    df['age'],
    bins=[0,18,30,50,100],
    labels=['Teen','Young','Adult','Senior']
)


---

1️⃣8️⃣ Outlier Detection (IQR)

Q1 = df['salary'].quantile(0.25)
Q3 = df['salary'].quantile(0.75)
IQR = Q3 - Q1

outliers = df[(df['salary'] < Q1 - 1.5*IQR) | 
              (df['salary'] > Q3 + 1.5*IQR)]


---

1️⃣9️⃣ Correlation

df.corr(numeric_only=True)


---

2️⃣0️⃣ Query API

df.query("age > 25 & city == 'Pune'")
df.query("gender == 'Female'")


---

2️⃣1️⃣ Exporting Data

df.to_csv('file.csv', index=False)
df.to_excel('file.xlsx', index=False)
df.to_json('file.json')


---

2️⃣2️⃣ Performance Optimization

df.memory_usage()
df.sample(frac=0.1)
df.astype('category')
df['col'].astype('float32')


---

2️⃣3️⃣ MultiIndex (Advanced)

df.set_index(['region','product'], inplace=True)
df.sort_index()
df.reset_index()


---

2️⃣4️⃣ String Cleaning (Real datasets)

df['name'] = df['name'].str.strip()
df['name'] = df['name'].str.replace('[^A-Za-z ]','', regex=True)
df['col'] = df['col'].str.lower()
df['email_domain'] = df['email'].str.split('@').str[1]


---

2️⃣5️⃣ JSON Handling

df = pd.json_normalize(json_data)


