---
title: 'Reproducible Research: Peer Assessment 1'
output:
  html_document:
    keep_md: yes
    self_contained: no
---


## Loading and preprocessing the data


First we have to unzip the data, we will use the function unz and then we read the CSV file:





```r
zipfile="activity.zip" 
file="activity.csv"
activity <- read.csv(unz(zipfile, file), sep=",", header=TRUE, stringsAsFactors=FALSE)
```




cheking the names of the columns, it is found that the data has the following: steps, date, interval. With the names we will evaluate the class of the columns in order to know if is necesarry some transformation on the variables:

```r
class(activity$steps)
```

```
## [1] "integer"
```

```r
class(activity$date)
```

```
## [1] "character"
```

```r
class(activity$interval)
```

```
## [1] "integer"
```

As you see the column *date*  is factor, in fact this is a date, so, we could transform to a date, but for now we will let it as factor.

## What is mean total number of steps taken per day?

In this point is useful use the function *aggregate* , we will take account the *N.A* to know in which date there is no data, also the column of the stpes is renamed to **TotalStepsDay**


```r
total<-aggregate(steps ~ date, data = activity, sum,na.action=na.pass)
colnames(total)[2] <- "Total"
```

Below you will find the histogram for the total steps.

```r
hist(total$Total, col="red", main="Total steps per day", xlab="Steps")
```

![plot of chunk histogram total](figure/histogram total-1.png) 

now we will calcilate the mean and the median of the total


```r
meanT<-mean(total$Total, na.rm=TRUE)
medianT<-median(total$Total, na.rm = TRUE)
```

With the above calculations we see that the mean is 1.0766189 &times; 10<sup>4</sup> and the median is 10765



## What is the average daily activity pattern?

We will make the timeseries with the intervals 5-minutes and I got a complete crazy plot....


```r
plot(activity$interval, activity$steps, col="blue", main="Pattern", ylab="Steps", type = "l", xlab="5 min interval")
```

![plot of chunk timeseries](figure/timeseries-1.png) 


## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
