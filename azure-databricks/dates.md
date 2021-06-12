# PySpark Date Functions

At first let's create a dataframe with sample date values
    
    df = spark.createDataFrame([('2019-02-20','2019-10-18',)],['start_dt','end_dt'])
    df

> DataFrame[start_dt: string, end_dt: string]

    df_dates = df.select(df.start_dt.cast('date'),df.end_dt.cast('date'))
    df_dates

> DataFrame[start_dt: date, end_dt: date]

## Change Date Format

    df_dates.select("start_dt","end_dt",date_format("start_dt",'dd/MM/yyyy').alias("dt_format")).show()

|  start_dt | end_dt | dt_format |
| :- | :- | :- |
|2019-02-20|2019-10-18|20/02/2019|


## Fetch Current Date

    df_dates.select("start_dt","end_dt",current_date().alias("cur_dt")).show()

|  start_dt | end_dt | cur_dt |
| :- | :- | :- |
|2019-02-20|2019-10-18|2019-03-17|


## Add Days to date

    df_dates.select("start_dt","end_dt",date_add("start_dt",2).alias("add_2_dt")).show()
    
|  start_dt | end_dt | add_2_dt |
| :- | :- | :- |
|2019-02-20|2019-10-18|2019-02-22|
    

## Add Months to date

    df_dates.select("start_dt","end_dt",add_months("start_dt",2).alias("add_2_mth")).show()
    
|  start_dt | end_dt | add_2_mth |
| :- | :- | :- |
|2019-02-20|2019-10-18|2019-04-20|
    

## Subtract 2 dates

    df_dates.select("start_dt","end_dt",datediff("end_dt","start_dt").alias("sub_2_dt")).show()

| start_dt | end_dt| sub_2_dt |
| :- | :- | :- |
|2019-02-20|2019-10-18|240|
    

## Extract Year from Date

    df_dates.select("start_dt","end_dt",year("start_dt").alias("ext_year")).show()
    
| start_dt | end_dt | ext_year |
| :- | :- | :- |
|2019-02-20|2019-10-18|2019|
    

## Extract Month from Date

    df_dates.select("start_dt","end_dt",month("start_dt").alias("ext_month")).show()
    
| start_dt | end_dt | ext_month |
| :- | :- | :- |
|2019-02-20|2019-10-18| 2|
    

## Extract Day from Date

    df_dates.select("start_dt","end_dt",dayofmonth("start_dt").alias("ext_day")).show()

| start_dt | end_dt | ext_day |
| :- | :- | :- |
|2019-02-20|2019-10-18|20|
    

## Subtract days from date

    df_dates.select("start_dt","end_dt",date_sub("start_dt",2).alias("sub_2_dt")).show()
    
| start_dt | end_dt | sub_2_dt |
| :- | :- | :- |
|2019-02-20|2019-10-18|2019-02-18|
    

or

    df_dates.select("start_dt","end_dt",date_add("start_dt",-2).alias("sub_2_dt")).show()
    
|  start_dt | end_dt | sub_2_dt |
| :- | :- | :- |
|2019-02-20|2019-10-18|2019-02-18|
    

## Fetch Day of the year

"Julian Date"

    df_dates.select("start_dt","end_dt",dayofyear("start_dt").alias("day_of_year")).show()
    
| start_dt| end_dt | day_of_year |
| :- | :- | :- |
|2019-02-20|2019-10-18|51|
    

## Last Day of Month

    df_dates.select("start_dt","end_dt",last_day("start_dt").alias("last_day")).show()
    
| start_dt | end_dt | last_day |
| :- | :- | :- |
|2019-02-20|2019-10-18|2019-02-28|
    

## Determine how many months between 2 Dates

    df_dates.select("start_dt","end_dt",months_between("end_dt","start_dt").alias("mth_btw")).show()
    
| start_dt | end_dt | mth_btw |
| :- | :- | :- |
|2019-02-20|2019-10-18|7.93548387|
    

## Identify date of next Weekday

    df_dates.select("start_dt","end_dt",next_day("start_dt","Mon").alias("nxt_Mon")).show()
    
| start_dt | end_dt | nxt_Mon|
| :- | :- | :- |
|2019-02-20|2019-10-18|2019-02-25|
    

And so on with Tue, Wed, Thu, Fri, Sat, Sun.

## Fetch quarter of the year

    df_dates.select("start_dt","end_dt",quarter("start_dt").alias("Quarter_of_Year")).show()

| start_dt | end_dt | Quarter_of_Year |
| :- | :- | :- |
|2019-02-20|2019-10-18|1|
    

## Truncate Date to Year/Month

    df_dates.select("start_dt","end_dt",trunc("start_dt","year").alias("trunc_Year")).show()
    
| start_dt | end_dt | trunc_Year |
| :- | :- | :- |
|2019-02-20|2019-10-18|2019-01-01|
    
    df_dates.select("start_dt","end_dt",trunc("start_dt","month").alias("trunc_Month")).show()
    
| start_dt | end_dt| trunc_Month |
| :- | :- | :- |
|2019-02-20|2019-10-18|2019-02-01|
    

## Fetch week of the Year

    df_dates.select("start_dt","end_dt",weekofyear("start_dt").alias("week_of_year")).show()

| start_dt| end_dt| week_of_year |
| :- | :- | :- |
|2019-02-20|2019-10-18|8|


