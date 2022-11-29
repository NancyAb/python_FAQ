# python_FAQ

I have a database background and code machine learning pipelines. I tend to see solutions with data first to find the optimal solution in SQL or Python. I will push the data conformance as close as possible to the source so that the data runs as clean as possible through the pipeline.

## Terminology

- **attribute** is a variable that is a class property
- **method** is a function stored in an instance or class 

## Dictionary

for key, value in a_dict.items():
     print(key, '->', value)
     
## Lists

## Sets

## Pandas

### lambda

- create a new column

import re
df['num_words'] = df.apply(lambda x : len(re.findall(r'\w+', x['body'])),axis=1)

### Aggregation Summary

results summarize with only the distinct values 

### calculated agg for each group to form a single summary value. 

You can do this agg in several ways by using DataFrame.aggregate(), Series.aggregate(), DataFrameGroupBy.aggregate().
 
df2 = df1.groupby('target').apply(meanofTargets)
grouped_multiple = df.groupby(['start_name','end_name'])
avg = grouped_multiple['duration'].mean()

or chain together

df.groupby(['start_name','end_name']).'duration'.mean()

### Aggregation on existing table 

Transform creates a value for each row in the Pandas dataframe

df.groupby(group_col_list).rowid.transform('nunique')
df_with_counts = df.groupby(y_col).id.transform('count')

### Quick Analysis Methods

- df[colname].value_counts()
- df[colname].describe()
- df[colname].plot(kind = 'hist', bins = 20) (for continuous)
- df[colname].plot(kind = 'bar') (for categorical)

### To join one dataframe with another use merge

- join types 'left', 'right', 'outer', 'inner'
- 'inner' default
- need to specify which column to join on
- 
 
left_df.merge(right_df, on='user_id', how='left') 

### Pandas Dataframe Column Methods

- df.**drop**(columns=['B', 'C'], inplace = True)
- df.**rename**(columns={"A": "a", "B": "c"}, inplace = True)
- df.**reset_index**(drop=True, inplace=True)
- df.**set_index**('column_name', inplace=True)
- df.**set_index**(['column_name_1', column_name_2], inplace = True)
- df[c] = df[c].**fillna**(-1)
- df.index.names = ['index']  (renames index)
- df.columns.names = ['column'] (for naming multilayered dataframes)

### index on primary key advantages

https://stackoverflow.com/questions/50970859/merging-dataframes-on-an-index-is-more-efficient-in-pandas

- Indicates merging on an index speeds up the join 3.5 times
- Easy updates defaults to index

### Dates

- df[datetimes] = pd.to_datetime(df[datetimes])
- df['Days'] = (df['Last_Date'] - df['Earlier Date']).dt.days
- df['New Date'] =  df['Earlier Date'] + pd.**DateOffset**(days=180)

### Distinct Values

.unique() returns a list
.nunique() returns number of unique values

### Working with Nulls

- total NaN values in column 'B'

print(data['B'].isnull().sum())

.count() returns count of non-null values

- total null values in the dataframe

df.isnull().sum().sum()

## Jupyter Notebook

See all the columns and not be limited by width for seeing a pandas dataframe

pd.set_option('display.max_colwidth', None)
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows',20)

## MS Excel 

- excel_start_date = date(1899, 12, 30)

- remove time from all datetime columns and fix excel formatting bug that prevents date alignment
    
- df[datetimes] = pd.to_datetime(df[datetimes]).dt.date
- df[datetimes] = df[datetimes] - excel_start_date
- df[datetimes] = df[datetimes].dt.days
   
# text

- display \n as return line in Vim

https://stackoverflow.com/questions/71323/how-to-replace-a-character-by-a-newline-in-vim

:set magic

:1,$s/\\\n/^M/g

To get the ^M character, Under Windows, do Ctrl + Q, and Enter.

type Ctrl + V and hit Enter on other systems
