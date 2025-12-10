📘 Data Manipulation With Pandas

A quick-reference guide to revise all important Pandas concepts for Data Analyst roles.


---

📑 INDEX

1. Basics

What is Series?

What is DataFrame?

Create DataFrame

Read CSV, Excel, JSON

head(), tail()

shape, info(), describe()

columns, index



---

2. Selecting / Retrieving Data

A. Basic Selection

df['col']

df[['col1', 'col2']]

df[row_filter]


B. loc (labels)

df.loc[row_labels, column_labels]


C. iloc (indexes)

df.iloc[row_index, col_index]


D. Useful Selectors

df.query()

df.isin()

df.between()

df.filter()



---

3. Filtering Conditions

==, >, <, >=, <=

&, |, ~

df['col'].str.contains()

df[df['col'].notnull()]



---

4. Missing Value Handling

isnull(), notnull()

dropna()

fillna()

replace()

duplicated(), drop_duplicates()



---

5. Data Cleaning

strip(), lower(), upper()

replace unwanted characters

convert datatypes

astype()

to_datetime()

extract year, month, day



---

6. Sorting

sort_values()

nlargest(), nsmallest()



---

7. Grouping & Aggregation

groupby()

agg()

sum, mean, count, max, min

multiple aggregations

pivot_table()



---

8. Joining & Combining

A. Merging:

merge()

inner / left / right / outer join


B. Concatenating:

concat(axis=0 or 1)


C. Append:

df.append() (old, avoid)



---

9. Column Operations

Creating new columns

apply()

lambda

map(), replace

cut(), qcut()

arithmetic operations



---

10. Index Operations

reset_index()

set_index()

sort_index()



---

11. Working with Dates

to_datetime()

dt.year, dt.month, dt.day

filtering dates

date range



---

12. Descriptive Statistics

mean, median, mode

std, var

corr(), cov()



---

13. Exporting Data

to_csv()

to_excel()

to_json()



