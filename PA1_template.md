# Reproducible Research: Peer Assessment 1
 

## Loading and preprocessing the data

```r
Mydata <- read.csv(file = "C:/Users/USRagunathA/Documents/Coursera/Data Science courses/Reproducible Research/RepData_PeerAssessment1/activity.csv ", header=TRUE, sep=",", quote="")
```

## What is mean total numbe r of steps taken per day?

```r
library(ggplot2)
```

```
## Warning: package 'ggplot2' was built under R version 3.1.3
```

```r
Total <- tapply(Mydata$X.steps., Mydata$X.date., FUN=sum, na.rm=TRUE)
Plot <- qplot(Total, binwidth=1000, xlab="Total number of steps taken each day")
print (Plot)
```

![](PA1_template_files/figure-html/mean-1.png) 

```r
Mean <- mean(Total, na.rm=TRUE)
Median <- median(Total, na.rm=TRUE)
print(Mean)
```

```
## [1] 9354.23
```

```r
print (Median)
```

```
## [1] 10395
```

## What is the average daily activity pattern?


```r
# Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

library(ggplot2)
Average <- aggregate(x=list(steps=Mydata$X.steps.), by=list(interval=Mydata$X.interval.),
                      FUN=mean, na.rm=TRUE)
Activity_plot<-ggplot(data=Average, aes(x=interval, y=steps)) + geom_line() +
    xlab("5 minute interval") +
    ylab("Average number of steps taken")
print(Activity_plot)
```

![](PA1_template_files/figure-html/activitypattern-1.png) 

```r
# 2.Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?
maxinterval<-  Average[which.max(Average$steps),]
print(maxinterval)
```

```
##     interval    steps
## 104      835 206.1698
```

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
