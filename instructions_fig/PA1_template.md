---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---

This is a R Markdown file created as a Course project of Reproducible Research.  
**About the data:** <br>  It is now possible to collect a large amount of data about personal movement using activity monitoring devices such as a Fitbit, Nike Fuelband, or Jawbone Up. These type of devices are part of the “quantified self” movement – a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. But these data remain under-utilized both because the raw data are hard to obtain and there is a lack of statistical methods and software for processing and interpreting the data.

This assignment makes use of data from a personal activity monitoring device. This device collects data at 5 minute intervals through out the day. The data consists of two months of data from an anonymous individual collected during the months of October and November, 2012 and include the number of steps taken in 5 minute intervals each day.

The variables included in this dataset are:

steps: Number of steps taking in a 5-minute interval (missing values are coded as NA)  
date: The date on which the measurement was taken in YYYY-MM-DD format  
interval: Identifier for the 5-minute interval in which measurement was taken  
The dataset is stored in a comma-separated-value (CSV) file and there are a total of 17,568 observations in this dataset.  
First,let us load the data and store it in an object named data.


```r
data<-read.csv("C:/Users/Pooja Naik/Documents/Coursera/activity.csv")
head(data)
```

```
##   steps       date interval
## 1    NA 01-10-2012        0
## 2    NA 01-10-2012        5
## 3    NA 01-10-2012       10
## 4    NA 01-10-2012       15
## 5    NA 01-10-2012       20
## 6    NA 01-10-2012       25
```

Let us explore the data a little more.

```r
str(data)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : Factor w/ 61 levels "01-10-2012","01-11-2012",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```
**Question 1**What is mean total number of steps taken per day?
For this part of the assignment, you can ignore the missing values in the dataset.

1.Calculate the total number of steps taken per day
To calculate the total number of steps taken per day,let us use the aggregate function.

```r
Steps_per_day<-aggregate(data$steps ,list(data$date),sum)
colnames(Steps_per_day)<-c("Date" ,"Steps")
Steps_per_day
```

```
##          Date Steps
## 1  01-10-2012    NA
## 2  01-11-2012    NA
## 3  02-10-2012   126
## 4  02-11-2012 10600
## 5  03-10-2012 11352
## 6  03-11-2012 10571
## 7  04-10-2012 12116
## 8  04-11-2012    NA
## 9  05-10-2012 13294
## 10 05-11-2012 10439
## 11 06-10-2012 15420
## 12 06-11-2012  8334
## 13 07-10-2012 11015
## 14 07-11-2012 12883
## 15 08-10-2012    NA
## 16 08-11-2012  3219
## 17 09-10-2012 12811
## 18 09-11-2012    NA
## 19 10-10-2012  9900
## 20 10-11-2012    NA
## 21 11-10-2012 10304
## 22 11-11-2012 12608
## 23 12-10-2012 17382
## 24 12-11-2012 10765
## 25 13-10-2012 12426
## 26 13-11-2012  7336
## 27 14-10-2012 15098
## 28 14-11-2012    NA
## 29 15-10-2012 10139
## 30 15-11-2012    41
## 31 16-10-2012 15084
## 32 16-11-2012  5441
## 33 17-10-2012 13452
## 34 17-11-2012 14339
## 35 18-10-2012 10056
## 36 18-11-2012 15110
## 37 19-10-2012 11829
## 38 19-11-2012  8841
## 39 20-10-2012 10395
## 40 20-11-2012  4472
## 41 21-10-2012  8821
## 42 21-11-2012 12787
## 43 22-10-2012 13460
## 44 22-11-2012 20427
## 45 23-10-2012  8918
## 46 23-11-2012 21194
## 47 24-10-2012  8355
## 48 24-11-2012 14478
## 49 25-10-2012  2492
## 50 25-11-2012 11834
## 51 26-10-2012  6778
## 52 26-11-2012 11162
## 53 27-10-2012 10119
## 54 27-11-2012 13646
## 55 28-10-2012 11458
## 56 28-11-2012 10183
## 57 29-10-2012  5018
## 58 29-11-2012  7047
## 59 30-10-2012  9819
## 60 30-11-2012    NA
## 61 31-10-2012 15414
```
The data frame Steps_per_day now the contains the sum of steps taken each day.

2.Make a histogram of the total number of steps taken each day  
<br>Creating the histogram

```r
hist(Steps_per_day$Steps,breaks=20,col="red",main="Total steps taken per day",xlab="Steps",ylab="Frequency")  
```

(PA1_template_files/figure-html/unnamed-chunk-4-1.png)
<br>3.Calculate and report the mean and median of the total number of steps taken per day

```r
mean(Steps_per_day$Steps,na.rm=TRUE)
```

```
## [1] 10766.19
```

```r
median(Steps_per_day$Steps,na.rm=TRUE)
```

```
## [1] 10765
```
<br>The mean of the total number of steps taken per day is **10766.19**
<br>The median of the total number of steps taken per day is **10765**

<br>**Question 2**What is the average daily activity pattern?
<br>1.Make a time series plot type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


```r
Steps_per_interval<-aggregate(steps~interval,data=data,mean,na.rm=TRUE)
plot(Steps_per_interval$interval,Steps_per_interval$steps,type="l" ,xlab="Interval",ylab="No.of steps",col="blue",main="Time Series plot of average steps taken per interval")
```

![](PA1_template_files/figure-html/unnamed-chunk-6-1.png)<!-- -->
<br>2.Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

```r
Steps_per_interval[grep(max(Steps_per_interval$steps), Steps_per_interval$steps),]
```

```
##     interval    steps
## 104      835 206.1698
```
The interval with maximum number of steps is interval **835**.
<br>

**Question 3**:Note that there are a number of days/intervals where there are missing values NA). The presence of missing days may introduce bias into some calculations or summaries of the data.
<br>
1.Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

```r
missing_data<-data.frame(steps=sum(is.na(data$steps)),interval<-sum(is.na(data$interval)),date<-sum(is.na(data$date)))
missing_data
```

```
##   steps interval....sum.is.na.data.interval.. date....sum.is.na.data.date..
## 1  2304                                     0                             0
```
<br>The result of above code shows that there 2304 missing values in the data.
2.Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.
<br>To fill the missing values,let us calculate the mean of the number of steps taken during that particular interval on the other days.

```r
new_data<-data
for(x in 1:17658)
{
if(is.na(new_data[x,1])==TRUE) 
{       cur_interval<-new_data[x,3]
        sub_interval<-subset(new_data,new_data$interval==cur_interval)
        new_data[x,1]<-mean(sub_interval$steps,na.rm = TRUE)
}
      

}
```
3.Create a new dataset that is equal to the original dataset but with the missing data filled in.
<br>The dataframe new_data is a new dataset with missing values filled in.

```r
head(new_data)
```

```
##       steps       date interval
## 1 1.7169811 01-10-2012        0
## 2 0.3396226 01-10-2012        5
## 3 0.1320755 01-10-2012       10
## 4 0.1509434 01-10-2012       15
## 5 0.0754717 01-10-2012       20
## 6 2.0943396 01-10-2012       25
```


4.Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

```r
imputed_steps_per_day<-aggregate(new_data$steps ,list(new_data$date),sum)
colnames(imputed_steps_per_day)<-c("Date" ,"Steps")

mean(imputed_steps_per_day$Steps,na.rm=TRUE)
```

```
## [1] 10766.19
```

```r
median(imputed_steps_per_day$Steps,na.rm=TRUE)
```

```
## [1] 10766.19
```

```r
hist(imputed_steps_per_day$Steps,breaks=20,col="green",xlab="Steps",ylab="Frequency",main="Total number of steps taken per day")
```

![](PA1_template_files/figure-html/unnamed-chunk-11-1.png)<!-- -->
<br>Mean of number of steps taken per day by imputing the missing values in the dataset= **10766.19**
<br>Median of number of steps taken per day by imputing the missing values in the dataset= **10766.19**
<br>Compare the difference in the total number of steps taken per day when the missing values in the first part of the assignment is filled with new values.

```r
par(mfrow=c(1,2))
hist(Steps_per_day$Steps,breaks=20,col="red",ylim=c(0,20),main=NULL,xlab="Steps",ylab="Frequency")
hist(imputed_steps_per_day$Steps,breaks=20,col="green",ylim=c(0,20),main=NULL,xlab="Steps",ylab="Frequency")
mtext("Histograms of Total Number of Steps Taken per day without/with imputed values",adj=0.9,font=2)
```

![](PA1_template_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

<br>It can be noticed that there is a difference in frequency.The frequency is high,when the missing values had been filled with other values.
<br>**Question 4**:Are there differences in activity patterns between weekdays and weekends?
<br>
1.Create a new factor variable in the dataset with two levels – “weekday” and “weekend” indicating whether a given date is a weekday or weekend day.

```r
new_days_data<-new_data
new_days_data$date<-as.Date(new_days_data$date)
new_days_data$day<-weekdays(new_days_data$date)
new_days_data$weekday<-as.character(rep(c(0,17568)))



for(i in 1:17658)
{
        if(new_days_data[i,4] %in% c("Saturday","Sunday"))
        {
                new_days_data[i,5]<-"weekend"
        }
        else
        {
                
                new_days_data[i,5]<-"weekday"
                
        }
        
}


new_days_data$weekday<-factor(new_days_data$weekday)
head(new_days_data)
```

```
##       steps       date interval      day weekday
## 1 1.7169811 0001-10-20        0 Saturday weekend
## 2 0.3396226 0001-10-20        5 Saturday weekend
## 3 0.1320755 0001-10-20       10 Saturday weekend
## 4 0.1509434 0001-10-20       15 Saturday weekend
## 5 0.0754717 0001-10-20       20 Saturday weekend
## 6 2.0943396 0001-10-20       25 Saturday weekend
```
<br>2.Make a panel plot containing a time series plot type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.

```r
weekday_data<-new_days_data[new_days_data$weekday=="weekday",]
weekend_data<-new_days_data[new_days_data$weekday=="weekend",]

weekday_mean<-aggregate(steps~interval,weekday_data,mean)
weekend_mean<-aggregate(steps~interval,weekend_data,mean)

par(mfrow=c(2,1),mar=c(4,4,1,2))
plot(weekday_mean$interval,weekday_mean$steps,type="l",xlab="Interval",ylab="Steps",main="Time series plot of average steps taken per day during weekdays")
plot(weekend_mean$interval,weekend_mean$steps,type="l",xlab="Interval",ylab="Steps",main="Time series plot of average steps taken per day during weekends")
```

![](PA1_template_files/figure-html/unnamed-chunk-14-1.png)<!-- -->


