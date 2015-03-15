Reproducible Research - Peer Assessment 1
=========================================

## Load and Pre-process data


- Download as zip
- unzip to csv
- Preprosses the data


```r
zip_url <- "http://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
temp <- tempfile()
download.file(zip_url, temp, mode="wb")
unzip(temp,"activity.csv")
data <- read.table("activity.csv", sep=",", header=TRUE)
unlink(temp)

library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following object is masked from 'package:stats':
## 
##     filter
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
data_by_date <- group_by(data, date)
```

## Steps in a day

1. Calculate the total number of steps in a day
2. Plot a histogram of total number of steps in a day
3. Calculate mean and median of total number of steps in a day


```r
steps_by_date <- summarise(data_by_date, steps=sum(steps))

hist(steps_by_date$steps,
     main="Steps per day",
     xlab="Number of steps in a day")
```

![plot of chunk num_steps_per_day](figure/num_steps_per_day-1.png) 

```r
final_steps_by_date <- summarise(steps_by_date,
                                 avg_steps=mean(steps,na.rm=TRUE),
                                 med_steps=median(steps,na.rm=TRUE))

avgstp <- final_steps_by_date[1,1]
medstp <- final_steps_by_date[1,2]
```
The average number of steps in a day is 1.0766189 &times; 10<sup>4</sup>  
The median number of steps in a day is 10765

## Average daily activity pattern
1.  Time series  plot of 5-minute intervals and average number of steps taken
2.  Which 5-minute interval contains the maximum number of steps

Unfortunately, due to personal reasons, I was unable to complete this task


## Inputing missing values

### Strategy
My feeling is that people would be very consistent in their behaviour over a week.  That is, they would do the same thing at the same time.  For eaxmple, leave for work at 7:30am of a weekday, go for a walk/jog at 6am on Mon, Wed, and Fri.  Therefore, I would replace missing values with the median value for a day and 5-minute interval.  That is, the number of steps for 8:00am on a Thursday, would be replaced with the median number of steps for Monday, 8:00am across the data set.

Unfortunately, due to personal reasons, I was unable to complete this task


## Differences between weekdays
Unfortunately, due to personal reasons, I was unable to complete this task
