# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

setting the directory:

```r
    currentDirectory <- getwd()
    newDirectory <- paste(currentDirectory,"/PeerAssessment1",sep="")
    if(!file.exists("PeerAssessment1")){dir.create("PeerAssessment1")}
    setwd(newDirectory)
```

downloading, unzipping and reading the data:

```r
    setInternet2()
    file <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
    download.file(file,"data.zip")    
    unzip("data.zip")
    data <- read.csv("activity.csv")
```

loading required packages:

```r
    install.packages("lattice",repos="http://cran.us.r-project.org")
```

```
## Installing package into 'C:/Users/Sebastian Stenzel/Documents/R/win-library/3.0'
## (as 'lib' is unspecified)
```

```
## package 'lattice' successfully unpacked and MD5 sums checked
```

```
## Warning: cannot remove prior installation of package 'lattice'
```

```
## 
## The downloaded binary packages are in
## 	C:\Users\Sebastian Stenzel\AppData\Local\Temp\RtmpSYV47V\downloaded_packages
```

```r
    library("lattice")
```

## What is mean total number of steps taken per day?

making copy of original data (for later computation of imputing missing values):

```r
    datazero <- data
```

excluding NA-entries (otherwise days with NA entries only get the value of "0" instead of "NA" in the following computation):

```r
    data<-data[complete.cases(data),]
```

computing distribution of total number of steps per day:

```r
    StepsPerDayTotal <- tapply(data$steps,data$date,sum,na.rm=T)
```

plotting the histogram:

```r
    hist(StepsPerDayTotal,xlab="Number of Steps",
    main="Distribution Total Number of Steps per Day")
```

![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7.png) 

computing and reporting mean **number** of **steps per day**:

```r
    StepsPerDayMean <- tapply(data$steps,data$date,mean,na.rm=T)
    StepsPerDayMean 
```

```
## 2012-10-01 2012-10-02 2012-10-03 2012-10-04 2012-10-05 2012-10-06 
##         NA     0.4375    39.4167    42.0694    46.1597    53.5417 
## 2012-10-07 2012-10-08 2012-10-09 2012-10-10 2012-10-11 2012-10-12 
##    38.2465         NA    44.4826    34.3750    35.7778    60.3542 
## 2012-10-13 2012-10-14 2012-10-15 2012-10-16 2012-10-17 2012-10-18 
##    43.1458    52.4236    35.2049    52.3750    46.7083    34.9167 
## 2012-10-19 2012-10-20 2012-10-21 2012-10-22 2012-10-23 2012-10-24 
##    41.0729    36.0938    30.6285    46.7361    30.9653    29.0104 
## 2012-10-25 2012-10-26 2012-10-27 2012-10-28 2012-10-29 2012-10-30 
##     8.6528    23.5347    35.1354    39.7847    17.4236    34.0938 
## 2012-10-31 2012-11-01 2012-11-02 2012-11-03 2012-11-04 2012-11-05 
##    53.5208         NA    36.8056    36.7049         NA    36.2465 
## 2012-11-06 2012-11-07 2012-11-08 2012-11-09 2012-11-10 2012-11-11 
##    28.9375    44.7326    11.1771         NA         NA    43.7778 
## 2012-11-12 2012-11-13 2012-11-14 2012-11-15 2012-11-16 2012-11-17 
##    37.3785    25.4722         NA     0.1424    18.8924    49.7882 
## 2012-11-18 2012-11-19 2012-11-20 2012-11-21 2012-11-22 2012-11-23 
##    52.4653    30.6979    15.5278    44.3993    70.9271    73.5903 
## 2012-11-24 2012-11-25 2012-11-26 2012-11-27 2012-11-28 2012-11-29 
##    50.2708    41.0903    38.7569    47.3819    35.3576    24.4688 
## 2012-11-30 
##         NA
```


computing and reporting median **number** of **steps per day**:

```r
    StepsPerDayMedian <- tapply(data$steps,data$date,median,na.rm=T)
    StepsPerDayMedian
```

```
## 2012-10-01 2012-10-02 2012-10-03 2012-10-04 2012-10-05 2012-10-06 
##         NA          0          0          0          0          0 
## 2012-10-07 2012-10-08 2012-10-09 2012-10-10 2012-10-11 2012-10-12 
##          0         NA          0          0          0          0 
## 2012-10-13 2012-10-14 2012-10-15 2012-10-16 2012-10-17 2012-10-18 
##          0          0          0          0          0          0 
## 2012-10-19 2012-10-20 2012-10-21 2012-10-22 2012-10-23 2012-10-24 
##          0          0          0          0          0          0 
## 2012-10-25 2012-10-26 2012-10-27 2012-10-28 2012-10-29 2012-10-30 
##          0          0          0          0          0          0 
## 2012-10-31 2012-11-01 2012-11-02 2012-11-03 2012-11-04 2012-11-05 
##          0         NA          0          0         NA          0 
## 2012-11-06 2012-11-07 2012-11-08 2012-11-09 2012-11-10 2012-11-11 
##          0          0          0         NA         NA          0 
## 2012-11-12 2012-11-13 2012-11-14 2012-11-15 2012-11-16 2012-11-17 
##          0          0         NA          0          0          0 
## 2012-11-18 2012-11-19 2012-11-20 2012-11-21 2012-11-22 2012-11-23 
##          0          0          0          0          0          0 
## 2012-11-24 2012-11-25 2012-11-26 2012-11-27 2012-11-28 2012-11-29 
##          0          0          0          0          0          0 
## 2012-11-30 
##         NA
```

calculating **mean** number of **total steps over all days**:

```r
    MEAN <- mean(StepsPerDayTotal,na.rm=T)
    MEAN
```

```
## [1] 10766
```

calculating **median** number of **total steps over all days**:

```r
    MEDIAN <- median(StepsPerDayTotal,na.rm=T)
    MEDIAN
```

```
## [1] 10765
```

The **mean** and **median** number of total steps over all days are **1.0766 &times; 10<sup>4</sup>** and **10765**.



## What is the average daily activity pattern?

calculating average number of steps taken per time interval, averaged across all days:

```r
    data <- datazero 
    IntervalAverages <- tapply(data$steps,data$interval,mean,na.rm=T)
```

plotting time series data for the average number of steps taken per time interval:

```r
    plot(x=names(IntervalAverages),y=IntervalAverages,type="l", xlab="Time Inteval", 
    ylab="Number of Steps", main="Number of Steps Averaged per Time Interval")
```

![plot of chunk unnamed-chunk-13](figure/unnamed-chunk-13.png) 

computing the maximum:

```r
    Maximum <- max(IntervalAverages)
    MaxPos <- IntervalAverages == Maximum
    (IntervalAverages[MaxPos])
```

```
##   835 
## 206.2
```

```r
    MaxInterval <- names(IntervalAverages[MaxPos])
```

The Interval **835** has on average the highest number of steps: **206.1698**


## Imputing missing values

Creating data frame *dataNaRm* in which missing values are replaced with the related interval's average.

finding positions, intervals and the number of points for which no values were recorded:

```r
    MissingValues <- is.na(data$steps)
    NumberMissingValues <- sum(MissingValues)
    IntervalMissingValues <- data[MissingValues,"interval"]
    NumberMissingValues
```

```
## [1] 2304
```
For **2304** of the intervals in the dataset no values were recorded.


picking the mean interval values for those points from the *IntervalAverages* calculated above:

```r
    MeanValues <- sapply(IntervalMissingValues,function(MVInt)
      {MVIntMean <- MVInt==names(IntervalAverages);IntervalAverages[MVIntMean]})
```

creating new data frame *dataNaRm* where those missing values are replaced by the related interval means:

```r
    dataNaRm <- data
    dataNaRm[MissingValues,"steps"] <- MeanValues
```

### Ploting the histogram with the *new* data

histogram with new (NA-imputed) data compared to histogram with old (NA-removed) data for comparison

```r
    ## new hist (NA-imputed)
    hist(tapply(dataNaRm$steps,dataNaRm$date,sum,na.rm=T),xlab="Number of Steps",
    main="Distribution Total Number of Steps per Day with Missing Values replaced",
    col = "blue",breaks = 10)
    
    ## old hist (NA-removed)
    data<-datazero[complete.cases(datazero),]
    hist(tapply(data$steps,data$date,sum,na.rm=T),xlab="Number of Steps",
    main="Distribution Total Number of Steps per Day with Missing Values replaced",add =     
      T, col = "lightblue",breaks = 10)
    
    ## adding legend
    legend("right",legend = c("change by NA-imputing")
    ,fill   = c("blue")
      )
```

![plot of chunk unnamed-chunk-18](figure/unnamed-chunk-18.png) 

computing and reporting the **new** mean number of **steps per day**:

```r
    StepsPerDayMean <- tapply(dataNaRm$steps,dataNaRm$date,mean,na.rm=T)
    StepsPerDayMean 
```

```
## 2012-10-01 2012-10-02 2012-10-03 2012-10-04 2012-10-05 2012-10-06 
##    37.3826     0.4375    39.4167    42.0694    46.1597    53.5417 
## 2012-10-07 2012-10-08 2012-10-09 2012-10-10 2012-10-11 2012-10-12 
##    38.2465    37.3826    44.4826    34.3750    35.7778    60.3542 
## 2012-10-13 2012-10-14 2012-10-15 2012-10-16 2012-10-17 2012-10-18 
##    43.1458    52.4236    35.2049    52.3750    46.7083    34.9167 
## 2012-10-19 2012-10-20 2012-10-21 2012-10-22 2012-10-23 2012-10-24 
##    41.0729    36.0938    30.6285    46.7361    30.9653    29.0104 
## 2012-10-25 2012-10-26 2012-10-27 2012-10-28 2012-10-29 2012-10-30 
##     8.6528    23.5347    35.1354    39.7847    17.4236    34.0938 
## 2012-10-31 2012-11-01 2012-11-02 2012-11-03 2012-11-04 2012-11-05 
##    53.5208    37.3826    36.8056    36.7049    37.3826    36.2465 
## 2012-11-06 2012-11-07 2012-11-08 2012-11-09 2012-11-10 2012-11-11 
##    28.9375    44.7326    11.1771    37.3826    37.3826    43.7778 
## 2012-11-12 2012-11-13 2012-11-14 2012-11-15 2012-11-16 2012-11-17 
##    37.3785    25.4722    37.3826     0.1424    18.8924    49.7882 
## 2012-11-18 2012-11-19 2012-11-20 2012-11-21 2012-11-22 2012-11-23 
##    52.4653    30.6979    15.5278    44.3993    70.9271    73.5903 
## 2012-11-24 2012-11-25 2012-11-26 2012-11-27 2012-11-28 2012-11-29 
##    50.2708    41.0903    38.7569    47.3819    35.3576    24.4688 
## 2012-11-30 
##    37.3826
```

computing and reporting the **new** median number of **steps per day**:

```r
    StepsPerDayMedian <- tapply(dataNaRm$steps,dataNaRm$date,median,na.rm=T)
    StepsPerDayMedian
```

```
## 2012-10-01 2012-10-02 2012-10-03 2012-10-04 2012-10-05 2012-10-06 
##      34.11       0.00       0.00       0.00       0.00       0.00 
## 2012-10-07 2012-10-08 2012-10-09 2012-10-10 2012-10-11 2012-10-12 
##       0.00      34.11       0.00       0.00       0.00       0.00 
## 2012-10-13 2012-10-14 2012-10-15 2012-10-16 2012-10-17 2012-10-18 
##       0.00       0.00       0.00       0.00       0.00       0.00 
## 2012-10-19 2012-10-20 2012-10-21 2012-10-22 2012-10-23 2012-10-24 
##       0.00       0.00       0.00       0.00       0.00       0.00 
## 2012-10-25 2012-10-26 2012-10-27 2012-10-28 2012-10-29 2012-10-30 
##       0.00       0.00       0.00       0.00       0.00       0.00 
## 2012-10-31 2012-11-01 2012-11-02 2012-11-03 2012-11-04 2012-11-05 
##       0.00      34.11       0.00       0.00      34.11       0.00 
## 2012-11-06 2012-11-07 2012-11-08 2012-11-09 2012-11-10 2012-11-11 
##       0.00       0.00       0.00      34.11      34.11       0.00 
## 2012-11-12 2012-11-13 2012-11-14 2012-11-15 2012-11-16 2012-11-17 
##       0.00       0.00      34.11       0.00       0.00       0.00 
## 2012-11-18 2012-11-19 2012-11-20 2012-11-21 2012-11-22 2012-11-23 
##       0.00       0.00       0.00       0.00       0.00       0.00 
## 2012-11-24 2012-11-25 2012-11-26 2012-11-27 2012-11-28 2012-11-29 
##       0.00       0.00       0.00       0.00       0.00       0.00 
## 2012-11-30 
##      34.11
```

calculating the **new** mean number of **total steps over all days**:

```r
    MEAN <- mean(tapply(dataNaRm$steps,dataNaRm$date,sum,na.rm=T))
    MEAN
```

```
## [1] 10766
```

calculating the **new** median number of **total steps over all days**:

```r
    MEDIAN <- median(tapply(dataNaRm$steps,dataNaRm$date,sum,na.rm=T))
    MEDIAN
```

```
## [1] 10766
```

Replacing missing values with mean interval values centralizes the distribution. In the earlier analysis (no imputing) a day contained either NA observations only or none. Hence these days were not included ealier but now they are and they all have the value 10766.19 because it is the sum of all interval averages. This results in mean and media of **1.0766 &times; 10<sup>4</sup>** and **1.0766 &times; 10<sup>4</sup>**. 


## Are there differences in activity patterns between weekdays and weekends?


* transforming date data to date variable:

```r
    dataNaRm <- transform(dataNaRm,date=as.Date(strptime(date,"%Y-%m-%d")))
```

* adding weekday column:

```r
    dataNaRm$wkday <- weekdays(dataNaRm$date)
```

* *optional replacing german with english weekday names:*

```r
    dataNaRm$wkday[dataNaRm$wkday=="Montag"] <- "Monday"
    dataNaRm$wkday[dataNaRm$wkday=="Dienstag"] <- "Tuesday"
    dataNaRm$wkday[dataNaRm$wkday=="Mittwoch"] <- "Wednesday"
    dataNaRm$wkday[dataNaRm$wkday=="Donnerstag"] <- "Thursday"
    dataNaRm$wkday[dataNaRm$wkday=="Freitag"] <- "Friday"
    dataNaRm$wkday[dataNaRm$wkday=="Samstag"]<-"Saturday"
    dataNaRm$wkday[dataNaRm$wkday=="Sonntag"]<-"Sunday"
```

* adding weekday/weekend column:

```r
    dataNaRm$wkend <- rep("weekday",nrow(dataNaRm))
    wkend <- dataNaRm$wkday=="Saturday"|dataNaRm$wkday=="Sunday"
    dataNaRm$wkend[wkend] <- "weekend"
```

* computing-interval means for weekday and weekend data:

```r
    WeekDayComparison <- aggregate(dataNaRm$steps ~ dataNaRm$interval + dataNaRm$wkend, 
                                   list(dataNaRm$interval), FUN=mean)
    colnames(WeekDayComparison) <- c("interval", "wkend", "steps")
```

* plotting the graph:

```r
    xyplot(WeekDayComparison$steps~WeekDayComparison$interval|WeekDayComparison$wkend,
    layout=c(1,2),xlab="Interval",ylab="Number of Steps",panel=function(x,y,..){
    panel.xyplot(x,y,type="l")}) 
```

![plot of chunk unnamed-chunk-28](figure/unnamed-chunk-28.png) 

Obviously during the week there is a high activitiy around 9 am when people are presumably on their way to work. The distribution for weekend activity in contrast in rather smooth in  comparison.
