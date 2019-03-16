# Resample_Annual_Keep_Month_Day

This class performs resampling of dates grouped together by a common value in another data frame column. The resampling in each group is vectorised and based on native pandas operations. The class can handle more than one day-month combination per group. NaN values in the date column or the groupby column are filtered but preserved and can be appended to the resampled data if desired. 
    
Examples
--------
    
    resample_annual = ResampleAnnualKeepMD()
    resample_annual.fit(df, 'Date', 'Id')
    df_resampled = resample_annual.transform(dayfirst=True, dt_format='%d/%m/%Y')
    df_resampled_full = resample_annual.append_nan()
    
    df
    Out[18]: 
        Id        Date  Value Currency
    0  2.0  20-03-2008     16      GBP
    1  2.0  20-03-2011     19      GBP
    2  2.0  05-06-2012     32      GBP
    3  2.0  05-06-2015     36      GBP
    4  4.0  03-03-2016     45      EUR
    5  4.0                 61      EUR
    6  4.0                 73      EUR
    7  NaN  07-07-2020     98      EUR
    
    df_resampled
    Out[16]: 
        Id        Date  Value Currency
    0  2.0  20/03/2008   16.0      GBP
    1  2.0  20/03/2009    NaN      NaN
    2  2.0  20/03/2010    NaN      NaN
    3  2.0  20/03/2011   19.0      GBP
    4  2.0  05/06/2012   32.0      GBP
    5  2.0  05/06/2013    NaN      NaN
    6  2.0  05/06/2014    NaN      NaN
    7  2.0  05/06/2015   36.0      GBP
    8  4.0  03/03/2016   45.0      EUR
    
    df_resampled_full
    Out[18]: 
         Id        Date  Value Currency
    0   2.0  20/03/2008   16.0      GBP
    1   2.0  20/03/2009    NaN      NaN
    2   2.0  20/03/2010    NaN      NaN
    3   2.0  20/03/2011   19.0      GBP
    4   2.0  05/06/2012   32.0      GBP
    5   2.0  05/06/2013    NaN      NaN
    6   2.0  05/06/2014    NaN      NaN
    7   2.0  05/06/2015   36.0      GBP
    8   4.0  03/03/2016   45.0      EUR
    9   4.0         NaT   61.0      EUR
    10  4.0         NaT   73.0      EUR
    11  NaN  07/07/2020   98.0      EUR   
    
Notes
------
This class does not transform the original data frame that is passed to it. To tranform an existing data frame assign to it the output of the transform() or append() method.
    
