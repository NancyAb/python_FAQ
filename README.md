# python_FAQ

I have a database background and code machine learning pipelines. I tend to see solutions with data first to find the optimal solution in SQL or Python. I will push the data conformance as close as possible to the source so that the data runs as clean as possible through the pipeline.

## Terminology

- **attribute** is a variable that is a class property
- **method** is a function stored in an instance or class 

## Dictionary

```python
dict = { 1:"integer", 2.03:"Decimal", "Dog":"Scooter"}

for key, value in a_dict.items():
     print(key, '->', value)
```

## Lists

## Sets

## Pandas

### lambda

- create a new column

```python
import re

df['num_words'] = df.apply(lambda x : len(re.findall(r'\w+', x['body'])),axis=1)
```

### Aggregation Summary

results summarize with only the distinct values 

### calculated agg for each group to form a single summary value. 

You can do this agg in several ways by using DataFrame.aggregate(), Series.aggregate(), DataFrameGroupBy.aggregate().

```python
df2 = df1.groupby('target').apply(meanofTargets)
grouped_multiple = df.groupby(['start_name','end_name'])
avg = grouped_multiple['duration'].mean()
```

or chain together

```python
df.groupby(['start_name','end_name']).'duration'.mean()
```

### Aggregation on existing table 

Transform creates a value for each row in the Pandas dataframe

```python
df.groupby(group_col_list).rowid.transform('nunique')
df_with_counts = df.groupby(y_col).id.transform('count')
```

### Multiple aggregations pandas groupby multiple aggregations on different columns

```python
df.groupby('class')['sepal length (cm)'].agg(
    sepal_average_length='mean',
    sepal_standard_deviation='std'
)

df.groupby('group').agg( a_sum=('a', 'sum'),
                         a_mean=('a', 'mean'),b_mean=('b', 'mean'),
                         c_sum=('c', 'sum'),
                         d_range=('d', lambda x: x.max() - x.min()))

data_df.groupby('external').agg( count= ('external','count'),
                                 min_pub = ('publication_date', 'min') ,
                                 max_pub = ('publication_date', 'max') ).reset_index()
```

### Quick Analysis Methods

```python
df[colname].value_counts()
df[colname].describe()
df[colname].plot(kind = 'hist', bins = 20) (for continuous)
df[colname].value_counts().plot(kind = 'bar') (for categorical)
```

### To join one dataframe with another use merge

- join types 'left', 'right', 'outer', 'inner'
     - 'inner' default
     - need to specify which column to join on

```python
left_df.merge(right_df, on='user_id', how='left') 
left_df.merge(right_df, left_on='user_id', right_on = 'id', how='left') 
left_df.merge(right_df, left_index=True, right_index=True, how='left')
```

### to stack one dataframe on top of another use concat

```python
frames = [df1, df2, df3]
result = pd.concat(frames)
```

### Pandas Dataframe Column Methods

```python
df.drop(columns=['B', 'C'], inplace = True)
df.rename(columns={"A": "a", "B": "c"}, inplace = True)
df.reset_index(drop=True, inplace=True)
df.set_index('column_name', inplace=True)
df.set_index(['column_name_1', column_name_2], inplace = True)
df[c] = df[c].fillna(-1)
df.index.names = ['index']  (renames index)
df.columns.names = ['column'] (for naming multilayered dataframes)
df.sort_values(by='col1', ascending=False)
```

### index on primary key advantages

https://stackoverflow.com/questions/50970859/merging-dataframes-on-an-index-is-more-efficient-in-pandas

- Indicates merging on an index speeds up the join 3.5 times
- Easy updates defaults to index

### Dates

#### Make sure not 'object' but datetime

- dataframe['Date with time'] = dataframe['Date with time'].astype('datetime64[ns]') # converts from object to datetime

- df[datetimes] = pd.to_datetime(df[datetimes])
- df['Days'] = (df['Last_Date'] - df['Earlier Date']).dt.days
- df['New Date'] =  df['Earlier Date'] + pd.**DateOffset**(days=180)
- dataframe['Date with time'] = pd.to_datetime(dataframe['Date with time']).dt.date  # datetime to date in pandas

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

### MS Excel Working with files

- MS Excel may not be able to work directly with csv files as it will often corrupt input if it contains apostrophes within columns
- Pandas can successfully read csv files without this corruption
- Pandas can write to MS Excel on if the libary is installed using df.to_excel()

```python
import openpyxl
df.to_excel(filename + '.xlsx')
df = pd.read_excel(filename + '.xlsx') # this needs to have xlwt installed
```

- To install openpxl

```
$ pip install xlwt
$ pip install openpyxl
```
   
# text

- display \n as return line in Vim

https://stackoverflow.com/questions/71323/how-to-replace-a-character-by-a-newline-in-vim

```
:set magic
:1,$s/\\n/^M/g
```

The "\n" character must have "\\\n" to escape out the special character

To get the ^M character, Under Windows, do Ctrl + Q, and Enter.

type Ctrl + V and hit Enter on other systems
