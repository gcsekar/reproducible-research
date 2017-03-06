# Reproducible Research Assignment - Week 2
Chandrasekar Ganesan  
February 26, 2017  



## Getting and processing the data

>Let's first get the data


```r
library(dplyr)
library(graphics)

activitydata <- read.csv("activity.csv", header = TRUE, na.strings = "NA")

#Format the date column as date
activitydata$date <- as.POSIXct(activitydata$date)

isdatana <- is.na(activitydata$steps)

#Ignore the NA values
data <- activitydata[!isdatana,]
```

## Histogram of the total number of steps taken each day


```r
steps_per_day_group <- group_by(data, date)
steps_per_day <- summarize(steps_per_day_group,sumsteps=sum(steps))
hist(steps_per_day$sumsteps, xlab="Sum of steps per day", ylab = "Frequency", main="Histogram of number of steps per day")
```

![](Figs/unnamed-chunk-2-1.png)<!-- -->

## Mean and Median steps taken each day

```r
summary(steps_per_day)
```

```
##       date                        sumsteps    
##  Min.   :2012-10-02 00:00:00   Min.   :   41  
##  1st Qu.:2012-10-16 00:00:00   1st Qu.: 8841  
##  Median :2012-10-29 00:00:00   Median :10765  
##  Mean   :2012-10-30 17:37:21   Mean   :10766  
##  3rd Qu.:2012-11-16 00:00:00   3rd Qu.:13294  
##  Max.   :2012-11-29 00:00:00   Max.   :21194
```

**Mean steps are 10766, Median steps are 10765**

## Average daily activity pattern


```r
steps_group <- aggregate(steps ~ interval, data, mean)

plot(steps_group$interval, steps_group$steps, type="l", xlab="Interval", ylab="Average steps", main="Average daily activity pattern")
```

![](Figs/unnamed-chunk-4-1.png)<!-- -->


## The 5-minute interval that, on average, contains the maximum number of steps


```r
steps_group <- aggregate(steps ~ interval, data, mean)

plot(steps_group$interval, steps_group$steps, type="l", xlab="Interval", ylab="Average steps", main="Average daily activity pattern")

abline(h = max(steps_group$steps), lty=2, col='red')

text(y=max(steps_group$steps)-5,x=400,labels = paste("Max Steps =",max(steps_group$steps),sep=" "))
```

![](Figs/unnamed-chunk-5-1.png)<!-- -->

## Imputing missing data


