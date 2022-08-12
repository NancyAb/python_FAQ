# python_FAQ
Python FAQs

I always get confused on how to aggregate because sometimes I want the results summarize with only the distinct values and other times I want a value on the existing table.

df.groupby(group_col_list).rowid.transform('nunique')



df['CODE'].value_counts()

 calculated agg for each group to form a single summary value. You can do this agg in several ways by using DataFrame.aggregate(), Series.aggregate(), DataFrameGroupBy.aggregate().
 
 
 df2 = df1.groupby('target').apply(meanofTargets)


df_with_counts = df.groupby(y_col).id.transform('count')
        
 
left_df.merge(right_df, on='user_id', how='left')

df.drop(columns=['B', 'C'])

df[colname].value_counts()
