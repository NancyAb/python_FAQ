# python_FAQ

I have a database background and code machine learning pipelines. I tend to see solutions with data first to find the optimal solution in SQL or Python. I will push the data conformance as close as possible to the source so that the data runs as clean as possible through the pipeline.

## Terminology

- **attribute** is a variable that is a class property
- **method** is a function stored in an instance or class 

## Aggregation

results summarize with only the distinct values 

### calculated agg for each group to form a single summary value. 

You can do this agg in several ways by using DataFrame.aggregate(), Series.aggregate(), DataFrameGroupBy.aggregate().
 
df2 = df1.groupby('target').apply(meanofTargets)

df_with_counts = df.groupby(y_col).id.transform('count')

and other times I want a value on the existing table.

df.groupby(group_col_list).rowid.transform('nunique')

### Quick Analysis Methods

- df[colname].value_counts()
- df[colname].describe()

## Joins

### To join one dataframe with another use merge
 
left_df.merge(right_df, on='user_id', how='left')

## Pandas Dataframe Column Methods

- df.**drop**(columns=['B', 'C'], inplace = True)
- df.**rename**(columns={"A": "a", "B": "c"}, inplace = True)
- df.**reset_index**(drop=True, inplace=True)
- df.**set_index**('column_name', inplace=True)
- df.**set_index**(['column_name_1', column_name_2], inplace = True)
- df[c] = df[c].**fillna**(-1)

## index on primary key advantages

https://stackoverflow.com/questions/50970859/merging-dataframes-on-an-index-is-more-efficient-in-pandas

- Indicates merging on an index speeds up the join 3.5 times
- Easy updates defaults to index

## Dates

- df[datetimes] = pd.to_datetime(df[datetimes])
- df['Days'] = (df['Last_Date'] - df['Earlier Date']).dt.days
- df['New Date'] =  df['Earlier Date'] + pd.**DateOffset**(days=180)

# MS Excel 

- excel_start_date = date(1899, 12, 30)

- remove time from all datetime columns and fix excel formatting bug that prevents date alignment
    
- df[datetimes] = pd.to_datetime(df[datetimes]).dt.date
- df[datetimes] = df[datetimes] - excel_start_date
- df[datetimes] = df[datetimes].dt.days
   
