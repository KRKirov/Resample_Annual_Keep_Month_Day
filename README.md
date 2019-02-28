# Resample_Annual_Keep_Month_Day
Annual frequency resampling of a date column in a data frame while preserving the day and month offsets in date columns with mixed dates.

This class performs resampling of dates grouped together by a common value in another data frame column. The resampling in each group is vectorised and based on native pandas operations. The class can handle more than one day-month combination per group. NaN values in the date column or the groupby column are filtered but preserved and can be appended to the resampled data if desired. 
    
Examples
--------
    
    resample_annual = ResampleAnnualKeepMD()
    resample_annual.fit(df, 'Date', 'Id')
    df_resampled = resample_annual.transform()
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
    Out[19]: 
        Id       Date  Value Currency
    0  2.0 2008-03-20   16.0      GBP
    1  2.0 2009-03-20    NaN      NaN
    2  2.0 2010-03-20    NaN      NaN
    3  2.0 2011-03-20   19.0      GBP
    4  2.0 2012-06-05   32.0      GBP
    5  2.0 2013-06-05    NaN      NaN
    6  2.0 2014-06-05    NaN      NaN
    7  2.0 2015-06-05   36.0      GBP
    8  4.0 2016-03-03   45.0      EUR
    
    df_resampled_full
    Out[20]: 
        Id       Date  Value Currency
    0   2.0 2008-03-20   16.0      GBP
    1   2.0 2009-03-20    NaN      NaN
    2   2.0 2010-03-20    NaN      NaN
    3   2.0 2011-03-20   19.0      GBP
    4   2.0 2012-06-05   32.0      GBP
    5   2.0 2013-06-05    NaN      NaN
    6   2.0 2014-06-05    NaN      NaN
    7   2.0 2015-06-05   36.0      GBP
    8   4.0 2016-03-03   45.0      EUR
    9   4.0        NaT   61.0      EUR
    10  4.0        NaT   73.0      EUR
    11  NaN 2020-07-07   98.0      EUR    
    
Notes
------
This class does not transform the original data frame that is passed to it. To tranform an existing data frame assign to it the output of the transform() or append() method.
    
