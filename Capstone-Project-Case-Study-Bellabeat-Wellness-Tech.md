---
title: 'Capstone Project Case Study: Bellabeat Wellness Technology'
author: "Julian Clemente"
date: "7/7/2021"
output:  
  html_document:
    keep_md: true
 
---



## Introduction
This is one of several Capstone Project Case Studies for the Google Data Analytics Certificate Program which aims solve real world type of business problems using data analytics. This document follows and applies the Ask-Prepare-Process-Analyze-Share-Act framework as a methodical approach to addressing all key areas of the data analysis process.

## About the Company
Urška Sršen and Sando Mur founded Bellabeat, a high-tech company that manufactures health-focused smart products. Sršen used her background as an artist to develop beautifully designed technology that informs and inspires women around the world. Collecting data on activity, sleep, stress, and reproductive health has allowed Bellabeat to empower women with knowledge about their own health and habits. Since it was founded in 2013, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for women. 

By 2016, Bellabeat had opened offices around the world and launched multiple products. Bellabeat products became available through a growing number of online retailers in addition to their own e-commerce channel on their website. The company has invested in traditional advertising media, such as radio, out-of-home billboards, print, and television, but focuses on digital marketing extensively. Bellabeat invests year-round in Google Search, maintaining active Facebook and Instagram pages, and consistently engages consumers on Twitter. Additionally, Bellabeat runs video ads on Youtube and display ads on the Google Display Network to support campaigns around key marketing dates.

Sršen knows that an analysis of Bellabeat’s available consumer data would reveal more opportunities for growth. She has asked the marketing analytics team to focus on a Bellabeat product and analyze smart device usage data in order to gain insight into how people are already using their smart devices. Then, using this information, she would like high-level recommendations for how these trends can inform Bellabeat marketing strategy.

### Products
  + Bellabeat app: The Bellabeat app provides users with health data related to their activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions. The Bellabeat app connects to their line of smart wellness products.
  + Leaf: Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf tracker connects to the Bellabeat app to track activity, sleep, and stress.
  + Time: This wellness watch combines the timeless look of a classic timepiece with smart technology to track user activity, sleep, and stress. The Time watch connects to the Bellabeat app to provide you with insights into your daily wellness.
  + Spring: This is a water bottle that tracks daily water intake using smart technology to ensure that you are appropriately hydrated throughout the day. The Spring bottle connects to the Bellabeat app to track your hydration levels.

## Data Analysis Process
The six steps of the data analysis process as well as some guiding topics that were considered and addressed at each phase are listed below:

1. Ask 
    + Problem identification & insight driven business decisions
2. Prepare 
    + Data storage & organization
    + Bias, credibility & data integrity
    + Identification of problems/shortcomings of data
3. Process  
    + Tool selection
    + Data cleansing and documentation of processs
4. Analyze  
    + Data formatting 
    + Identification of trends or relationships
    + Relation of insights to business questions
5. Share  
    + Storytelling using new data insights
    + Communication with audience verbally and via data visualization
6. Act
    + Final conclusions and future analysis
    + Application of insights

### Case Study Roadmap - Ask

#### Key Tasks
1. Identify the business task 
  * The business task is to gain insight from how customers use their smart devices and apply it to one of Bellabeat's products and its marketing strategy in order to discover new and effective strategies and growth opportunities.
2. Consider key stakeholders 
  * The key stakeholders are the Bellabeat marketing analytics team, the cofounder and Chief Creative Officer, Urska Srsen, the co-founder/Mathematician, Sando Mur, current Bellabeat smart technology users as well as smart tech users (and potential Bellabeat users) in general.
Deliverable

#### Deliverables
1. A clear statement of the business task: 
  * The business task is to gain insight from how customers use their smart devices and apply it to one of Bellabeat's products and its marketing strategy in order to achieve new opportunities for growth.

### Case Study Roadmap - Prepare

The dataset for the "Fitbit Fitness Tracker Data" was downloaded from [Kaggle](https://www.kaggle.com/arashnic/fitbit). This raw dataset will be stored locally for cleaning and processing via RStudio.

In order to view and process these datasets, the appropriate tidyverse packages must be installed (if so, uncomment line 43) and loaded, which is done so in the following:


```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
```

```
## ✓ ggplot2 3.3.3     ✓ purrr   0.3.4
## ✓ tibble  3.1.2     ✓ dplyr   1.0.6
## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
## ✓ readr   1.4.0     ✓ forcats 0.5.1
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

The dataset includes 18 csv files which can be accessed, imported and viewed directly on RStudio with the tidyverse packages that were just installed.

The data is organized into 18 csv files that capture everything from daily activity, calories (daily, hourly and by minute), intensities (daily, hourly and by minute), number of steps (daily, hourly and by minute), heartrate, minute METs, sleep (Day and minute) and weight log info. There are several datasets that are both in long (or narrow) format as well as the wide format. However, none of these "by the minute" datasets will be imported  or used for this analysis. Therefore, for the sake of this analysis, the relevant datasets are in long format.

Per the dataset description from Kaggle, were generated via a survey conducted and distributed by Amazon Mechanical Turk March 12, 2016 and May 12, 2016. Assessing the bias/credibility of this dataset against the ROCCC criteria:
    + Reliable - Yes. Since this dataset was published on Kaggle and has been widely used by other Kaggle users for their own data analysis, it is fair to believe that the data is reliable. Kaggle given this dataset a usability score of 10.0 due to it being easy to understand, its inclusion of the appropriate metadata, being saved in a machine readible format and being frequently maintained.
    + Original - Yes. The dataset is original since it was directly gathered from Fitbit users who provided their personal tracking health data to Amazon Mechanical Turk. This is considered 2nd party data since the dataset provider/source (Amazon Mechanical Turk) collected it from their audience (Fitbit users).
    + Comprehensive - Yes. This data contains various measures of personal tracking health data which should be able to aid in identifying the trends on their smart fitness tracking devices. This includes activity, calories, intesities, sleep, number of steps and weight.
    + Current - Yes. The dataset is still fairly current to the time of this case study as the survey data was collected between March 12, 2016 and May 12, 2016.
    + Cited - Yes. These datasets cite the survey conducted by Amazon Mechanical Turk, which is a crowdsourcing website used to collect data from participants.

Upon inspection, the data appears to be useful in answering our business question. By having the different metrics and parameters that fitness tracking smart device users utilize, what current and potential Bellabeat users care about in their daily lives in regards to activity, fitness and health can be better understood. This can help to uncover new strategies/opportunities for the marketing analytics team in regards to growth opportunities for their technology.

However, the raw data must be cleaned first due to possible issues. One potential problem is that the data collected comes from only 30 Fitbit users which could arguably be considered a fairly small sample size. Another problem with the data is that we need to check for any NULL or NA values and that all the observations and columns are consistently formatted. If not properly cleaned, this possible issues or outliers in the dataset and therefore lead to erroneous insights.

 
#### Key tasks
1. Download data and store it appropriately - COMPLETE 
  * All 18 datasets/csv files have been stored locally and the filepath from RStudio has been established. For the scope of this data analysis only a selection of the 18 datasets that were deemed relevant in addressing the business task were imported into RStudio.
  

```r
# Read the select csv files into R and assigning them variable names
daily_activity <- read.csv("Datasets/Fitabase Data 4.12.16-5.12.16/dailyActivity_merged.csv")
daily_calories <- read.csv("Datasets/Fitabase Data 4.12.16-5.12.16/dailyCalories_merged.csv")
daily_intensities <- read.csv("Datasets/Fitabase Data 4.12.16-5.12.16/dailyIntensities_merged.csv")
daily_steps <- read.csv("Datasets/Fitabase Data 4.12.16-5.12.16/dailySteps_merged.csv")
hourly_calories <- read.csv("Datasets/Fitabase Data 4.12.16-5.12.16/hourlyCalories_merged.csv")
hourly_intensities <- read.csv("Datasets/Fitabase Data 4.12.16-5.12.16/hourlyIntensities_merged.csv")
hourly_steps <- read.csv("Datasets/Fitabase Data 4.12.16-5.12.16/hourlySteps_merged.csv")
daily_sleep <- read.csv("Datasets/Fitabase Data 4.12.16-5.12.16/sleepDay_merged.csv")
weight_log <- read.csv("Datasets/Fitabase Data 4.12.16-5.12.16/weightLogInfo_merged.csv")

# Omitted reading heartrate and any parameters measured by the minute.
```
  
2. Identify how it’s organized - COMPLETE
  * The imported data is organized in a narrow format. All files can be parsed by export session ID (column A) or timestamp (column B). The following lines of code below can be used to preview the first 6 rows of the imported datasets.
  

```r
# Preview datasets using head function
head(daily_activity)
```

```
##           Id ActivityDate TotalSteps TotalDistance TrackerDistance
## 1 1503960366    4/12/2016      13162          8.50            8.50
## 2 1503960366    4/13/2016      10735          6.97            6.97
## 3 1503960366    4/14/2016      10460          6.74            6.74
## 4 1503960366    4/15/2016       9762          6.28            6.28
## 5 1503960366    4/16/2016      12669          8.16            8.16
## 6 1503960366    4/17/2016       9705          6.48            6.48
##   LoggedActivitiesDistance VeryActiveDistance ModeratelyActiveDistance
## 1                        0               1.88                     0.55
## 2                        0               1.57                     0.69
## 3                        0               2.44                     0.40
## 4                        0               2.14                     1.26
## 5                        0               2.71                     0.41
## 6                        0               3.19                     0.78
##   LightActiveDistance SedentaryActiveDistance VeryActiveMinutes
## 1                6.06                       0                25
## 2                4.71                       0                21
## 3                3.91                       0                30
## 4                2.83                       0                29
## 5                5.04                       0                36
## 6                2.51                       0                38
##   FairlyActiveMinutes LightlyActiveMinutes SedentaryMinutes Calories
## 1                  13                  328              728     1985
## 2                  19                  217              776     1797
## 3                  11                  181             1218     1776
## 4                  34                  209              726     1745
## 5                  10                  221              773     1863
## 6                  20                  164              539     1728
```

```r
head(daily_calories)
```

```
##           Id ActivityDay Calories
## 1 1503960366   4/12/2016     1985
## 2 1503960366   4/13/2016     1797
## 3 1503960366   4/14/2016     1776
## 4 1503960366   4/15/2016     1745
## 5 1503960366   4/16/2016     1863
## 6 1503960366   4/17/2016     1728
```

```r
head(daily_intensities)
```

```
##           Id ActivityDay SedentaryMinutes LightlyActiveMinutes
## 1 1503960366   4/12/2016              728                  328
## 2 1503960366   4/13/2016              776                  217
## 3 1503960366   4/14/2016             1218                  181
## 4 1503960366   4/15/2016              726                  209
## 5 1503960366   4/16/2016              773                  221
## 6 1503960366   4/17/2016              539                  164
##   FairlyActiveMinutes VeryActiveMinutes SedentaryActiveDistance
## 1                  13                25                       0
## 2                  19                21                       0
## 3                  11                30                       0
## 4                  34                29                       0
## 5                  10                36                       0
## 6                  20                38                       0
##   LightActiveDistance ModeratelyActiveDistance VeryActiveDistance
## 1                6.06                     0.55               1.88
## 2                4.71                     0.69               1.57
## 3                3.91                     0.40               2.44
## 4                2.83                     1.26               2.14
## 5                5.04                     0.41               2.71
## 6                2.51                     0.78               3.19
```

```r
head(daily_steps)
```

```
##           Id ActivityDay StepTotal
## 1 1503960366   4/12/2016     13162
## 2 1503960366   4/13/2016     10735
## 3 1503960366   4/14/2016     10460
## 4 1503960366   4/15/2016      9762
## 5 1503960366   4/16/2016     12669
## 6 1503960366   4/17/2016      9705
```

```r
head(hourly_calories)
```

```
##           Id          ActivityHour Calories
## 1 1503960366 4/12/2016 12:00:00 AM       81
## 2 1503960366  4/12/2016 1:00:00 AM       61
## 3 1503960366  4/12/2016 2:00:00 AM       59
## 4 1503960366  4/12/2016 3:00:00 AM       47
## 5 1503960366  4/12/2016 4:00:00 AM       48
## 6 1503960366  4/12/2016 5:00:00 AM       48
```

```r
head(hourly_intensities)
```

```
##           Id          ActivityHour TotalIntensity AverageIntensity
## 1 1503960366 4/12/2016 12:00:00 AM             20         0.333333
## 2 1503960366  4/12/2016 1:00:00 AM              8         0.133333
## 3 1503960366  4/12/2016 2:00:00 AM              7         0.116667
## 4 1503960366  4/12/2016 3:00:00 AM              0         0.000000
## 5 1503960366  4/12/2016 4:00:00 AM              0         0.000000
## 6 1503960366  4/12/2016 5:00:00 AM              0         0.000000
```

```r
head(hourly_steps)
```

```
##           Id          ActivityHour StepTotal
## 1 1503960366 4/12/2016 12:00:00 AM       373
## 2 1503960366  4/12/2016 1:00:00 AM       160
## 3 1503960366  4/12/2016 2:00:00 AM       151
## 4 1503960366  4/12/2016 3:00:00 AM         0
## 5 1503960366  4/12/2016 4:00:00 AM         0
## 6 1503960366  4/12/2016 5:00:00 AM         0
```

```r
head(daily_sleep)
```

```
##           Id              SleepDay TotalSleepRecords TotalMinutesAsleep
## 1 1503960366 4/12/2016 12:00:00 AM                 1                327
## 2 1503960366 4/13/2016 12:00:00 AM                 2                384
## 3 1503960366 4/15/2016 12:00:00 AM                 1                412
## 4 1503960366 4/16/2016 12:00:00 AM                 2                340
## 5 1503960366 4/17/2016 12:00:00 AM                 1                700
## 6 1503960366 4/19/2016 12:00:00 AM                 1                304
##   TotalTimeInBed
## 1            346
## 2            407
## 3            442
## 4            367
## 5            712
## 6            320
```

```r
head(weight_log)
```

```
##           Id                  Date WeightKg WeightPounds Fat   BMI
## 1 1503960366  5/2/2016 11:59:59 PM     52.6     115.9631  22 22.65
## 2 1503960366  5/3/2016 11:59:59 PM     52.6     115.9631  NA 22.65
## 3 1927972279  4/13/2016 1:08:52 AM    133.5     294.3171  NA 47.54
## 4 2873212765 4/21/2016 11:59:59 PM     56.7     125.0021  NA 21.45
## 5 2873212765 5/12/2016 11:59:59 PM     57.3     126.3249  NA 21.69
## 6 4319703577 4/17/2016 11:59:59 PM     72.4     159.6147  25 27.45
##   IsManualReport        LogId
## 1           True 1.462234e+12
## 2           True 1.462320e+12
## 3          False 1.460510e+12
## 4           True 1.461283e+12
## 5           True 1.463098e+12
## 6           True 1.460938e+12
```

3. Sort and filter the data. - COMPLETE
  * The data has been pre-sorted and pre-filtered, as described above, by session ID and time stamp.
4. Determine the credibility of the data - COMPLETE
  * The credibility of the data has been established above, see #5 (line 66).

#### Deliverable
A description of all data sources used.  
  * For a high level description of each of the 9 datasets, the "glimpse" and "summary" functions in R are used. The "glimpse" function shows the number of rows, number of columns, column names, column data types and the different unique values for each column whereas the "summary" function provides a statistical summary of the data by showing the min, max, mean, median, 1st/3rd quartile data of the qualitative data.


```r
# High level summary of daily_activity
glimpse(daily_activity)
```

```
## Rows: 940
## Columns: 15
## $ Id                       <dbl> 1503960366, 1503960366, 1503960366, 150396036…
## $ ActivityDate             <chr> "4/12/2016", "4/13/2016", "4/14/2016", "4/15/…
## $ TotalSteps               <int> 13162, 10735, 10460, 9762, 12669, 9705, 13019…
## $ TotalDistance            <dbl> 8.50, 6.97, 6.74, 6.28, 8.16, 6.48, 8.59, 9.8…
## $ TrackerDistance          <dbl> 8.50, 6.97, 6.74, 6.28, 8.16, 6.48, 8.59, 9.8…
## $ LoggedActivitiesDistance <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ VeryActiveDistance       <dbl> 1.88, 1.57, 2.44, 2.14, 2.71, 3.19, 3.25, 3.5…
## $ ModeratelyActiveDistance <dbl> 0.55, 0.69, 0.40, 1.26, 0.41, 0.78, 0.64, 1.3…
## $ LightActiveDistance      <dbl> 6.06, 4.71, 3.91, 2.83, 5.04, 2.51, 4.71, 5.0…
## $ SedentaryActiveDistance  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ VeryActiveMinutes        <int> 25, 21, 30, 29, 36, 38, 42, 50, 28, 19, 66, 4…
## $ FairlyActiveMinutes      <int> 13, 19, 11, 34, 10, 20, 16, 31, 12, 8, 27, 21…
## $ LightlyActiveMinutes     <int> 328, 217, 181, 209, 221, 164, 233, 264, 205, …
## $ SedentaryMinutes         <int> 728, 776, 1218, 726, 773, 539, 1149, 775, 818…
## $ Calories                 <int> 1985, 1797, 1776, 1745, 1863, 1728, 1921, 203…
```

```r
summary(daily_activity)
```

```
##        Id            ActivityDate         TotalSteps    TotalDistance   
##  Min.   :1.504e+09   Length:940         Min.   :    0   Min.   : 0.000  
##  1st Qu.:2.320e+09   Class :character   1st Qu.: 3790   1st Qu.: 2.620  
##  Median :4.445e+09   Mode  :character   Median : 7406   Median : 5.245  
##  Mean   :4.855e+09                      Mean   : 7638   Mean   : 5.490  
##  3rd Qu.:6.962e+09                      3rd Qu.:10727   3rd Qu.: 7.713  
##  Max.   :8.878e+09                      Max.   :36019   Max.   :28.030  
##  TrackerDistance  LoggedActivitiesDistance VeryActiveDistance
##  Min.   : 0.000   Min.   :0.0000           Min.   : 0.000    
##  1st Qu.: 2.620   1st Qu.:0.0000           1st Qu.: 0.000    
##  Median : 5.245   Median :0.0000           Median : 0.210    
##  Mean   : 5.475   Mean   :0.1082           Mean   : 1.503    
##  3rd Qu.: 7.710   3rd Qu.:0.0000           3rd Qu.: 2.053    
##  Max.   :28.030   Max.   :4.9421           Max.   :21.920    
##  ModeratelyActiveDistance LightActiveDistance SedentaryActiveDistance
##  Min.   :0.0000           Min.   : 0.000      Min.   :0.000000       
##  1st Qu.:0.0000           1st Qu.: 1.945      1st Qu.:0.000000       
##  Median :0.2400           Median : 3.365      Median :0.000000       
##  Mean   :0.5675           Mean   : 3.341      Mean   :0.001606       
##  3rd Qu.:0.8000           3rd Qu.: 4.782      3rd Qu.:0.000000       
##  Max.   :6.4800           Max.   :10.710      Max.   :0.110000       
##  VeryActiveMinutes FairlyActiveMinutes LightlyActiveMinutes SedentaryMinutes
##  Min.   :  0.00    Min.   :  0.00      Min.   :  0.0        Min.   :   0.0  
##  1st Qu.:  0.00    1st Qu.:  0.00      1st Qu.:127.0        1st Qu.: 729.8  
##  Median :  4.00    Median :  6.00      Median :199.0        Median :1057.5  
##  Mean   : 21.16    Mean   : 13.56      Mean   :192.8        Mean   : 991.2  
##  3rd Qu.: 32.00    3rd Qu.: 19.00      3rd Qu.:264.0        3rd Qu.:1229.5  
##  Max.   :210.00    Max.   :143.00      Max.   :518.0        Max.   :1440.0  
##     Calories   
##  Min.   :   0  
##  1st Qu.:1828  
##  Median :2134  
##  Mean   :2304  
##  3rd Qu.:2793  
##  Max.   :4900
```

```r
# High level summary of daily_calories
glimpse(daily_calories)
```

```
## Rows: 940
## Columns: 3
## $ Id          <dbl> 1503960366, 1503960366, 1503960366, 1503960366, 1503960366…
## $ ActivityDay <chr> "4/12/2016", "4/13/2016", "4/14/2016", "4/15/2016", "4/16/…
## $ Calories    <int> 1985, 1797, 1776, 1745, 1863, 1728, 1921, 2035, 1786, 1775…
```

```r
summary(daily_calories)
```

```
##        Id            ActivityDay           Calories   
##  Min.   :1.504e+09   Length:940         Min.   :   0  
##  1st Qu.:2.320e+09   Class :character   1st Qu.:1828  
##  Median :4.445e+09   Mode  :character   Median :2134  
##  Mean   :4.855e+09                      Mean   :2304  
##  3rd Qu.:6.962e+09                      3rd Qu.:2793  
##  Max.   :8.878e+09                      Max.   :4900
```

```r
# High level summary of daily_intensities
glimpse(daily_intensities)
```

```
## Rows: 940
## Columns: 10
## $ Id                       <dbl> 1503960366, 1503960366, 1503960366, 150396036…
## $ ActivityDay              <chr> "4/12/2016", "4/13/2016", "4/14/2016", "4/15/…
## $ SedentaryMinutes         <int> 728, 776, 1218, 726, 773, 539, 1149, 775, 818…
## $ LightlyActiveMinutes     <int> 328, 217, 181, 209, 221, 164, 233, 264, 205, …
## $ FairlyActiveMinutes      <int> 13, 19, 11, 34, 10, 20, 16, 31, 12, 8, 27, 21…
## $ VeryActiveMinutes        <int> 25, 21, 30, 29, 36, 38, 42, 50, 28, 19, 66, 4…
## $ SedentaryActiveDistance  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
## $ LightActiveDistance      <dbl> 6.06, 4.71, 3.91, 2.83, 5.04, 2.51, 4.71, 5.0…
## $ ModeratelyActiveDistance <dbl> 0.55, 0.69, 0.40, 1.26, 0.41, 0.78, 0.64, 1.3…
## $ VeryActiveDistance       <dbl> 1.88, 1.57, 2.44, 2.14, 2.71, 3.19, 3.25, 3.5…
```

```r
summary(daily_intensities)
```

```
##        Id            ActivityDay        SedentaryMinutes LightlyActiveMinutes
##  Min.   :1.504e+09   Length:940         Min.   :   0.0   Min.   :  0.0       
##  1st Qu.:2.320e+09   Class :character   1st Qu.: 729.8   1st Qu.:127.0       
##  Median :4.445e+09   Mode  :character   Median :1057.5   Median :199.0       
##  Mean   :4.855e+09                      Mean   : 991.2   Mean   :192.8       
##  3rd Qu.:6.962e+09                      3rd Qu.:1229.5   3rd Qu.:264.0       
##  Max.   :8.878e+09                      Max.   :1440.0   Max.   :518.0       
##  FairlyActiveMinutes VeryActiveMinutes SedentaryActiveDistance
##  Min.   :  0.00      Min.   :  0.00    Min.   :0.000000       
##  1st Qu.:  0.00      1st Qu.:  0.00    1st Qu.:0.000000       
##  Median :  6.00      Median :  4.00    Median :0.000000       
##  Mean   : 13.56      Mean   : 21.16    Mean   :0.001606       
##  3rd Qu.: 19.00      3rd Qu.: 32.00    3rd Qu.:0.000000       
##  Max.   :143.00      Max.   :210.00    Max.   :0.110000       
##  LightActiveDistance ModeratelyActiveDistance VeryActiveDistance
##  Min.   : 0.000      Min.   :0.0000           Min.   : 0.000    
##  1st Qu.: 1.945      1st Qu.:0.0000           1st Qu.: 0.000    
##  Median : 3.365      Median :0.2400           Median : 0.210    
##  Mean   : 3.341      Mean   :0.5675           Mean   : 1.503    
##  3rd Qu.: 4.782      3rd Qu.:0.8000           3rd Qu.: 2.053    
##  Max.   :10.710      Max.   :6.4800           Max.   :21.920
```

```r
# High level summary of daily_sleep
glimpse(daily_sleep)
```

```
## Rows: 413
## Columns: 5
## $ Id                 <dbl> 1503960366, 1503960366, 1503960366, 1503960366, 150…
## $ SleepDay           <chr> "4/12/2016 12:00:00 AM", "4/13/2016 12:00:00 AM", "…
## $ TotalSleepRecords  <int> 1, 2, 1, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
## $ TotalMinutesAsleep <int> 327, 384, 412, 340, 700, 304, 360, 325, 361, 430, 2…
## $ TotalTimeInBed     <int> 346, 407, 442, 367, 712, 320, 377, 364, 384, 449, 3…
```

```r
summary(daily_sleep)
```

```
##        Id              SleepDay         TotalSleepRecords TotalMinutesAsleep
##  Min.   :1.504e+09   Length:413         Min.   :1.000     Min.   : 58.0     
##  1st Qu.:3.977e+09   Class :character   1st Qu.:1.000     1st Qu.:361.0     
##  Median :4.703e+09   Mode  :character   Median :1.000     Median :433.0     
##  Mean   :5.001e+09                      Mean   :1.119     Mean   :419.5     
##  3rd Qu.:6.962e+09                      3rd Qu.:1.000     3rd Qu.:490.0     
##  Max.   :8.792e+09                      Max.   :3.000     Max.   :796.0     
##  TotalTimeInBed 
##  Min.   : 61.0  
##  1st Qu.:403.0  
##  Median :463.0  
##  Mean   :458.6  
##  3rd Qu.:526.0  
##  Max.   :961.0
```

```r
# High level summary of daily_steps
glimpse(daily_steps)
```

```
## Rows: 940
## Columns: 3
## $ Id          <dbl> 1503960366, 1503960366, 1503960366, 1503960366, 1503960366…
## $ ActivityDay <chr> "4/12/2016", "4/13/2016", "4/14/2016", "4/15/2016", "4/16/…
## $ StepTotal   <int> 13162, 10735, 10460, 9762, 12669, 9705, 13019, 15506, 1054…
```

```r
summary(daily_steps)
```

```
##        Id            ActivityDay          StepTotal    
##  Min.   :1.504e+09   Length:940         Min.   :    0  
##  1st Qu.:2.320e+09   Class :character   1st Qu.: 3790  
##  Median :4.445e+09   Mode  :character   Median : 7406  
##  Mean   :4.855e+09                      Mean   : 7638  
##  3rd Qu.:6.962e+09                      3rd Qu.:10727  
##  Max.   :8.878e+09                      Max.   :36019
```

```r
# High level summary of hourly_calories
glimpse(hourly_calories)
```

```
## Rows: 22,099
## Columns: 3
## $ Id           <dbl> 1503960366, 1503960366, 1503960366, 1503960366, 150396036…
## $ ActivityHour <chr> "4/12/2016 12:00:00 AM", "4/12/2016 1:00:00 AM", "4/12/20…
## $ Calories     <int> 81, 61, 59, 47, 48, 48, 48, 47, 68, 141, 99, 76, 73, 66, …
```

```r
summary(hourly_calories)
```

```
##        Id            ActivityHour          Calories     
##  Min.   :1.504e+09   Length:22099       Min.   : 42.00  
##  1st Qu.:2.320e+09   Class :character   1st Qu.: 63.00  
##  Median :4.445e+09   Mode  :character   Median : 83.00  
##  Mean   :4.848e+09                      Mean   : 97.39  
##  3rd Qu.:6.962e+09                      3rd Qu.:108.00  
##  Max.   :8.878e+09                      Max.   :948.00
```

```r
# High level summary of hourly_intensities
glimpse(hourly_intensities)
```

```
## Rows: 22,099
## Columns: 4
## $ Id               <dbl> 1503960366, 1503960366, 1503960366, 1503960366, 15039…
## $ ActivityHour     <chr> "4/12/2016 12:00:00 AM", "4/12/2016 1:00:00 AM", "4/1…
## $ TotalIntensity   <int> 20, 8, 7, 0, 0, 0, 0, 0, 13, 30, 29, 12, 11, 6, 36, 5…
## $ AverageIntensity <dbl> 0.333333, 0.133333, 0.116667, 0.000000, 0.000000, 0.0…
```

```r
summary(hourly_intensities)
```

```
##        Id            ActivityHour       TotalIntensity   AverageIntensity
##  Min.   :1.504e+09   Length:22099       Min.   :  0.00   Min.   :0.0000  
##  1st Qu.:2.320e+09   Class :character   1st Qu.:  0.00   1st Qu.:0.0000  
##  Median :4.445e+09   Mode  :character   Median :  3.00   Median :0.0500  
##  Mean   :4.848e+09                      Mean   : 12.04   Mean   :0.2006  
##  3rd Qu.:6.962e+09                      3rd Qu.: 16.00   3rd Qu.:0.2667  
##  Max.   :8.878e+09                      Max.   :180.00   Max.   :3.0000
```

```r
# High level description of hourly_steps
glimpse(hourly_steps)
```

```
## Rows: 22,099
## Columns: 3
## $ Id           <dbl> 1503960366, 1503960366, 1503960366, 1503960366, 150396036…
## $ ActivityHour <chr> "4/12/2016 12:00:00 AM", "4/12/2016 1:00:00 AM", "4/12/20…
## $ StepTotal    <int> 373, 160, 151, 0, 0, 0, 0, 0, 250, 1864, 676, 360, 253, 2…
```

```r
summary(hourly_steps)
```

```
##        Id            ActivityHour         StepTotal      
##  Min.   :1.504e+09   Length:22099       Min.   :    0.0  
##  1st Qu.:2.320e+09   Class :character   1st Qu.:    0.0  
##  Median :4.445e+09   Mode  :character   Median :   40.0  
##  Mean   :4.848e+09                      Mean   :  320.2  
##  3rd Qu.:6.962e+09                      3rd Qu.:  357.0  
##  Max.   :8.878e+09                      Max.   :10554.0
```

```r
# High level summary of weight_log
glimpse(weight_log)
```

```
## Rows: 67
## Columns: 8
## $ Id             <dbl> 1503960366, 1503960366, 1927972279, 2873212765, 2873212…
## $ Date           <chr> "5/2/2016 11:59:59 PM", "5/3/2016 11:59:59 PM", "4/13/2…
## $ WeightKg       <dbl> 52.6, 52.6, 133.5, 56.7, 57.3, 72.4, 72.3, 69.7, 70.3, …
## $ WeightPounds   <dbl> 115.9631, 115.9631, 294.3171, 125.0021, 126.3249, 159.6…
## $ Fat            <int> 22, NA, NA, NA, NA, 25, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ BMI            <dbl> 22.65, 22.65, 47.54, 21.45, 21.69, 27.45, 27.38, 27.25,…
## $ IsManualReport <chr> "True", "True", "False", "True", "True", "True", "True"…
## $ LogId          <dbl> 1.462234e+12, 1.462320e+12, 1.460510e+12, 1.461283e+12,…
```

```r
summary(weight_log)
```

```
##        Id                Date              WeightKg       WeightPounds  
##  Min.   :1.504e+09   Length:67          Min.   : 52.60   Min.   :116.0  
##  1st Qu.:6.962e+09   Class :character   1st Qu.: 61.40   1st Qu.:135.4  
##  Median :6.962e+09   Mode  :character   Median : 62.50   Median :137.8  
##  Mean   :7.009e+09                      Mean   : 72.04   Mean   :158.8  
##  3rd Qu.:8.878e+09                      3rd Qu.: 85.05   3rd Qu.:187.5  
##  Max.   :8.878e+09                      Max.   :133.50   Max.   :294.3  
##                                                                         
##       Fat             BMI        IsManualReport         LogId          
##  Min.   :22.00   Min.   :21.45   Length:67          Min.   :1.460e+12  
##  1st Qu.:22.75   1st Qu.:23.96   Class :character   1st Qu.:1.461e+12  
##  Median :23.50   Median :24.39   Mode  :character   Median :1.462e+12  
##  Mean   :23.50   Mean   :25.19                      Mean   :1.462e+12  
##  3rd Qu.:24.25   3rd Qu.:25.56                      3rd Qu.:1.462e+12  
##  Max.   :25.00   Max.   :47.54                      Max.   :1.463e+12  
##  NA's   :65
```

Reviewing the ouput of our glimpse and summary functions, we notice that the "daily_activity" data frame is essentially a merged data frame that already contains the columns captured by the "daily_calories", "daily_intensities" and "daily_steps" data frames.To eliminate redundancy and duplication of data column, we drop these 3 data frames from our analysis.

### Case Study Roadmap - Process

The preferred tool used for this data analytics project will be R / RStudio as it provides all the necessary features and functions typically needed perform the analysis such as loading data, transforming data, cleaning data, data visualization as well as documentation of the work flow process (via RMarkdown files). Since the datasets would need to be uploaded on an online database (such as BigQuery) in order to use SQL and the files can be easily downloaded from Kaggle as .csv files, there may not be much benefit or advantage to using SQL to complete this analysis. Spreadsheet software programs such as Microsoft Excel or Google Sheets may not be as advantageous for this project as well, given that the # of observations (as shown by the use of the 'nrow' function) can get as large as 22,000+. This could make using the spreadsheet program fairly slow and cumbersome.
 
On R, we can ensure that the data is cleaned by installing and using the "skimr" and "janitor" packages. The step by step cleaning process involves checking for consistent and correct data types, fixing or removing any NULL or NA data, standardizing naming conventions for columns and values, removing any duplicate observations and verifying that the data types make sense.
 
 
#### Key tasks
1. Check the data for errors. - COMPLETE (see deliverable)
2. Choose your tools. - COMPLETE 
  * The primary tool selected to perform this data analysis is R / R Studio as it has all the features and packages to make performing the date cleaning, transformation, manipulation and visualization tasks easy. In addition, the process can be documented within an RMarkdown file and through the use of in-line code to describe. 
3. Transform the data so you can work with it effectively. - COMPLETE (see deliverable)
4. Document the cleaning process. - COMPLETE (see deliverable)

#### Deliverable
Documentation of any cleaning or manipulation of data

The first step in cleaning the data on R involves loading the "skimr" and "janitor" packages with the following code:


```r
## Uncomment the following lines if the "skimr" or "janitor" packages are not yet installed, otherwise, proceed to line 192)
#install.packages("skimr")
#install.packages("janitor")

library("skimr")
library("janitor")
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

First, by using the "clean_names" function as shown below, we can ensure all the column names for each of our data frames are unique, consistently lower cased and consist of only letters, numbers and/or underscores:



Next, we can proceed with doing some data cleaning on our observation data for each of our data frames. The below code checks to sum the # of values that are NULL or NA.


```r
daily_activity %>%
  is.na() %>%
  sum()
```

```
## [1] 0
```

```r
daily_sleep %>%
  is.na() %>%
  sum()
```

```
## [1] 0
```

```r
hourly_calories %>%
  is.na() %>%
  sum()
```

```
## [1] 0
```

```r
hourly_intensities %>%
  is.na() %>%
  sum()
```

```
## [1] 0
```

```r
hourly_steps %>%
  is.na() %>%
  sum()
```

```
## [1] 0
```

```r
weight_log %>%
  is.na() %>%
  sum()
```

```
## [1] 65
```

The outputs of the above lines of code indicate that the first 5 data frames contain 0 total NULL or NA values. However, for the last data frame, "weight_log", there were 65 NULL or NA values. Upon further closer examination, these values were all found under the "Fat" column. Since 65 out of the 67 observations had NA for this column, which won't be very useful or add much value to our analysis, removing the "Fat" column from our "weight_log" dataframe is appropriate. This is performed below:


```r
weight_log$Fat <- NULL

#Then we can verify that the "Fat" column is removed.
weight_log %>%
  is.na() %>%
  sum()
```

```
## [1] 0
```


Since we plan to eventually merge and plot our data, we should verify the # of unique users. This is represented by the "Id" column which is what we'll be mapping our data by since this is shared by each dataframe. 


```r
n_distinct(daily_activity$Id)
```

```
## [1] 33
```

```r
n_distinct(daily_sleep$Id)
```

```
## [1] 24
```

```r
n_distinct(hourly_calories$Id)
```

```
## [1] 33
```

```r
n_distinct(hourly_intensities$Id)
```

```
## [1] 33
```

```r
n_distinct(hourly_steps$Id)
```

```
## [1] 33
```

```r
n_distinct(weight_log$Id)
```

```
## [1] 8
```

These results indicate that there were 24 unique users who provided data for their "daily_sleep" health metrics, 8 unique users for their "weight_log" health metrics and 33 unique users for the rest. Based on this very low sample size of "weight_log" data providers, we can now make the decision to also drop that data frame as part of our analysis since it won't add much insight.

Next, we evaluate for any duplicate rows in each of our dataframes.


```r
sum(duplicated(daily_activity))
```

```
## [1] 0
```

```r
sum(duplicated(daily_sleep))
```

```
## [1] 3
```

```r
sum(duplicated(hourly_calories))
```

```
## [1] 0
```

```r
sum(duplicated(hourly_intensities))
```

```
## [1] 0
```

```r
sum(duplicated(hourly_steps))
```

```
## [1] 0
```

Based on the output of this code, "daily_sleep" features 3 duplicate observation rows. This is removed from our dataframe and saved under a new name, "daily_sleep_1" as follows:


```r
daily_sleep_1 <- daily_sleep[!duplicated(daily_sleep), ]

#Verify duplicate rows have been removed
sum(duplicated(daily_sleep_1))
```

```
## [1] 0
```

Next, comparing the columns that represent a unique timestamp, we notice a discrepancy between the name of this column for our "daily_sleep_1" data frame vs. our daily_activity data frame. On "daily_sleep_1", this column is called "SleepDay" whereas the column on the rest of the daily data frames that serves to timestamp each observation is called "ActivityDate". For the sake of consistency and in the event we want to merge these dataframes together, we will rename "SleepDay".


```r
daily_sleep_1 <- daily_sleep_1 %>%
  rename(ActivityDate = SleepDay)
```

We also notice a difference in the date format between these two data frames. For "daily_sleep_1", the date includes the time (e.g. 4/12/2016 12:00:00 AM). Using the following line of code, we omit the time by converting to the %m/%d/%y format. As a matter of fact, we also ensure that the "daily_activity" data frame follows an identical format and is of the same data type (date or date-time) as well.


```r
#Install/load lubridate package
#install.packages(lubridate)
library(lubridate)
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
daily_sleep_1$ActivityDate <- as.Date(daily_sleep_1$ActivityDate, format = "%m/%d/%Y")
daily_activity$ActivityDate <-as.Date(daily_activity$ActivityDate, format = "%m/%d/%Y")
```

Likewise, although our "ActivityHour" values on our hourly data frames are consistently formatted, their data type is incorrect. As shown by the output of the glimpse function we ran earlier, ActivityHour is shown as a <chr> (character/string data type) as opposed to a <date>. We fix this with the below line of code.


```r
hourly_calories$ActivityHour <- mdy_hms(hourly_calories$ActivityHour)
hourly_intensities$ActivityHour <-mdy_hms(hourly_intensities$ActivityHour)
hourly_steps$ActivityHour <-mdy_hms(hourly_steps$ActivityHour)
```


Following these cleaning steps, our data frames are ready for the Analyze step.

### Case Study Roadmap - Analyze

As determined by our Process step, we have a variety of data frames that measure different fitness parameters (steps, calories, distance, sleep, activity, etc) in both daily and hourly time frames. However, for organizational consistency as well as ease and simplicity, we should consolidate our data frames by whether observations are provided at a daily or hourly intervals . This is made possible because the "Id" column is a shared key that corresponds between each of our data frames.


```r
# Our "daily_activity" data frame consists of 940 observations of 33 distinct Ids. Our "daily_sleep_1" data frame consists of 410 observations of 24 distinct Ids. Since these both provide health and wellness measurements on a daily basis, we can merge these tables into a new data frame called "daily_activity_with_sleep"

daily_activity_with_sleep <- merge(daily_activity,daily_sleep_1, by=c("Id", "ActivityDate"))

# However, it is worth noting that since there are only 24 distinct Ids and 410 observations on the "daily_sleep_1" data frame, our merge creates an "inner join" between our two tables (identical values for both Id and ActivityDate have to exist in both data frames in order to be captured on the merged one).

# Our "hourly_calories", "hourly_intensities" and "hourly_steps" data frames all consist of 22099 observations of 33 distinct. We will merge these three data frames into a single data frame called "hourly_activity". This is done via "Id" and "ActivityHour":

hourly_activity <- merge(hourly_calories,hourly_intensities, by=c("Id","ActivityHour"))
hourly_activity <- merge(hourly_activity,hourly_steps, by=c("Id","ActivityHour"))
```

Now that we've performed a successful aggregation of our data into only three easy to work with data frames, we can begin performing some exploratory analysis to find trends and relationships within our data. This is done in the Deliverable section of the Analysis step below.

#### Key tasks
1. Aggregate your data so it’s useful and accessible. - COMPLETE
2. Organize and format your data. - COMPLETE
3. Perform calculations. - COMPLETE
4. Identify trends and relationships. -COMPLETE

#### Deliverable
A summary of your analysis

We can begin with a sanity check to make sure our data makes sense and that obvious and follows the patterns we would naturally expect. From our "daily_activity_with_sleep" data frame, we plot the relationship between a user's total steps and the calories they burn:


```r
# Relationship between TotalSteps and Calories.
# We hypothesize that the relationship is directly positive and that the more steps you take, the more Calories you likely burned that same day.
 ggplot(data = daily_activity_with_sleep) + geom_point(mapping = aes(x = TotalSteps, y = Calories ))  
```

![](Capstone-Project-Case-Study-Bellabeat-Wellness-Tech_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

Our plot reflects the relationship we hypothesized which is a good sign that our data make sense and that we can draw some valid conclusions/insights.

Our aggregated data frames show there to be a vast analaysis space we can explore. Several possible analysis cases and fitness parameter relations that piqued my interested while scanning through our data frames are:
   1. Correlation/Balance between Active Lifestyles and Hours of Sleep
   2. Breakdown of Activity Level by Time/Day of the Week
   3. Distribution between Calories Burned vs. Daily Activity Level
   
   
##### Case 1: Correlation/Balance between Active Lifestyles and Hours of Sleep

   
First, for Case #1, I utilize the data frame, "daily_activity_with_sleep", in order to investigate the relationship between user's active lifestyles with the amount of sleep they get. Do those who live the most active lifestyles compromise attaining the recommended number hours of sleep each night? If so, on how large or small of a scale? Conversely, could those users who tend to oversleep correlate to those who are less active? According to the [Sleep Foundation](https://www.sleepfoundation.org/how-sleep-works/how-much-sleep-do-we-really-need#:~:text=National%20Sleep%20Foundation%20guidelines1,to%208%20hours%20per%20night.), young adults and adults, which are presumably the age groups this study comprises of, are advised anywhere between 7 - 9 hours of sleep each night.

The relationship between time asleep vs. activity level can be illustrated with a pair of scatter plots. The specific columns/attributes that can be useful for analysis are "Total Steps", "Sedentary Minutes", "Calories" & "Total Minutes Asleep". 

For our first scatter plot (code shown directly below), we explore the correlation between activity level and sleep using the "TotalMinutesAsleep", "TotalSteps" and "Calories", which are represented by the x-axis, y-axis and point color, respectively. In addition to these parameters,  we also graph two vertical lines ( x = 420 & x = 540) which represent the upper and lower bounds of the recommended hours of sleep ( 7 hours & 9 hours). Lastly, we plot the best fit linear model line between our x and y parameters.



```r
Scatter_Sleep_Steps_Calories <- ggplot(data = daily_activity_with_sleep) +
  labs(title = "Sleep vs Daily Activity (Total Steps & Calories)", x = "Total Time Asleep (min)", y = "Total Steps") + 
 geom_point(mapping = aes( x = TotalMinutesAsleep, y = TotalSteps, color = Calories )) + 
  scale_color_gradientn(colors = c('red', 'orange', 'yellow', 'green', 'blue'), values = c(0, 25, 50, 75, 100/100)) + geom_smooth(formula = y ~ x, method=lm, mapping = aes(y = TotalSteps, x = TotalMinutesAsleep), color = "red") +
geom_vline(xintercept=420,linetype="dashed",size=.5, color = "black") +
geom_vline(xintercept=540,linetype="dashed",size=.5, color = "black")

plot(Scatter_Sleep_Steps_Calories) 
```

![](Capstone-Project-Case-Study-Bellabeat-Wellness-Tech_files/figure-html/unnamed-chunk-17-1.png)<!-- -->



The code below shows the 2nd scatter plot that can aid in our investigation and illustration of sleep vs. activity level. This 2nd scatter plot is set up similarly to our 1st scatter plot. However,his time we utilize the "SedentaryMinutes" parameter instead of "Calories" and represent it with a color gradient. Basically, the larger a user's Sedentary Minutes value, the less active they are during the day.


```r
Scatter_Sleep_Steps_ActMin <- ggplot(data = daily_activity_with_sleep) +
  labs(title = "Sleep vs Daily Activity (Total Steps & Sedentary Minutes)", x = "Total Time Asleep (min)", y = "Total Steps", color = "Sedantary Minutes") + 
 geom_point(mapping = aes( x = TotalMinutesAsleep, y = TotalSteps, color = SedentaryMinutes )) + 
  scale_color_gradientn(colors = c('red', 'orange', 'yellow', 'green', 'blue'), values = c(0, 25, 50, 75, 100/100))+ 
  geom_smooth(formula = y ~ x, method=lm, mapping = aes(y = TotalSteps, x = TotalMinutesAsleep), color = "red") +
geom_vline(xintercept=420,linetype="dashed",size=.5, color = "black") +
geom_vline(xintercept=540,linetype="dashed",size=.5, color = "black")

plot(Scatter_Sleep_Steps_ActMin) 
```

![](Capstone-Project-Case-Study-Bellabeat-Wellness-Tech_files/figure-html/unnamed-chunk-18-1.png)<!-- -->

Both our scatterplots we used to explore the 1st analysis case helped uncover some useful insights in regards to sleep level vs. activity. As indicated by the large number of points that fall outside of our Recommended Hours of Sleep boundary, users of all activity levels commonly fail to get between 7-9 hours of sleep. A lot of users, whether they burn 3000 calories a day or spend 1250 minutes being sedentary, are sedentary. 


```r
#Determine # of instances users who slept less than the recommended 7 hours (or 420 minutes)
daily_activity_with_sleep %>%
  count(TotalMinutesAsleep < 420)
```

```
##   TotalMinutesAsleep < 420   n
## 1                    FALSE 229
## 2                     TRUE 181
```

```r
#Determine # of instances users who slept more than the recommended 9 hours (or 540 minutes)
daily_activity_with_sleep %>%
  count(TotalMinutesAsleep > 540)
```

```
##   TotalMinutesAsleep > 540   n
## 1                    FALSE 371
## 2                     TRUE  39
```

As shown above, in 181 out of 410  (44.1%) instances, users did not get the minimum hours of recommended sleep. On the other end of the spectrum, 39 out of 410 (9.5%) instances, users slept more than the recomended hours.
 

Furthermore, our best fit line indicates a negative relationship between the # of minutes of sleep vs. the total steps daily. This tells us that those who tend to get more sleep, tend not to be as active (and get more daily steps). Interestingly, the inverse isnt necessarily true. As shown by the 2nd scatter plot and the blue (high sedentary minutes) being located on the lower left of the graph, those who tend to undersleep also tend not to be as active as well. One hypothesis is that one's job, work or other personal responsibilities may get in the way of being active and getting at least 7 hours of sleep.


##### Case 2: Breakdown of Activity Level by Time/Day of the Week


For Case #2, in which we explore what sort of tendencies users have regarding their activity level vs. the time & day of the week, we use the "hourly_activity" dataframe.  

This analysis will require some additional data preparation before we can immediately jump right in, plot the parameters of interest and uncover any new insights. First ,we can first add a new column to our data frame that indicates the day of the week (Sun, Mon, Tues, etc) for each observation conveniently based on the "ActivityHour" column. This is done as follows:


```r
hourly_activity$DayOfWeek <- weekdays(as.Date(hourly_activity$ActivityHour))
```

We can extract further information from the time of activity by categorizing the time of day into the following: 

0:00 - 3:59 - Late Night
4:00 - 7:59 - Early Morning
8:00 - 11:59 - Morning
12:00 - 15:59 - Afternoon
16:00 - 19:59 - Evening
20:00 - 23:59 - Night

The code below creates a new column called "TimeOfDay" which categorizes each observation per the above labels.



With the "DayOfWeek" and "TimeOfDay" columns added to our "hourly_activity" data frame, we can generate 2 tibbles (one for mean Calories and the other for mean Average Intensity) as broken down by the day of the week and time of the day. This is performed below


```r
# Generate Tibble of the mean Calories by Day of the week and time of day
Tibble_Day_Time_Cal <- hourly_activity %>% 
  group_by(DayOfWeek, TimeOfDay) %>%
 summarise(across(starts_with('Calories'), mean))
```

```
## `summarise()` has grouped output by 'DayOfWeek'. You can override using the `.groups` argument.
```

```r
print(Tibble_Day_Time_Cal)
```

```
## # A tibble: 42 x 3
## # Groups:   DayOfWeek [7]
##    DayOfWeek TimeOfDay     Calories
##    <chr>     <chr>            <dbl>
##  1 Friday    Afternoon        109. 
##  2 Friday    Early Morning     87.7
##  3 Friday    Evening          120. 
##  4 Friday    Late Night        69.7
##  5 Friday    Morning          106. 
##  6 Friday    Night             94.9
##  7 Monday    Afternoon        108. 
##  8 Monday    Early Morning     86.4
##  9 Monday    Evening          123. 
## 10 Monday    Late Night        68.4
## # … with 32 more rows
```

```r
# Generate Tibble of the mean Average Intensities by Day of the week and time of day
Tibble_Day_Time_Int <- hourly_activity %>% 
  group_by(DayOfWeek, TimeOfDay) %>%
 summarise(across(starts_with('AverageIntensity'), mean))
```

```
## `summarise()` has grouped output by 'DayOfWeek'. You can override using the `.groups` argument.
```

```r
print(Tibble_Day_Time_Int)
```

```
## # A tibble: 42 x 3
## # Groups:   DayOfWeek [7]
##    DayOfWeek TimeOfDay     AverageIntensity
##    <chr>     <chr>                    <dbl>
##  1 Friday    Afternoon               0.278 
##  2 Friday    Early Morning           0.129 
##  3 Friday    Evening                 0.346 
##  4 Friday    Late Night              0.0223
##  5 Friday    Morning                 0.249 
##  6 Friday    Night                   0.188 
##  7 Monday    Afternoon               0.274 
##  8 Monday    Early Morning           0.121 
##  9 Monday    Evening                 0.366 
## 10 Monday    Late Night              0.0140
## # … with 32 more rows
```

These tibbles can each be used to plot a grouped bar graph. Our first graph is the average calories burned each day of the week as broken down by the time of the day.


```r
#Re-order the day of week to follow the typical calendar order
Tibble_Day_Time_Cal$DayOfWeek <- factor(Tibble_Day_Time_Cal$DayOfWeek, levels = c("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"))

#Re-order the day of week to follow the typical chronogological order
Tibble_Day_Time_Cal$TimeOfDay <- factor(Tibble_Day_Time_Cal$TimeOfDay, levels = c("Early Morning", "Morning", "Afternoon", "Evening", "Night", "Late Night"))

Bar_DayOfTheWeek_ActivityLevel_Cal <- ggplot(data = Tibble_Day_Time_Cal) +
  geom_col(mapping =  aes(x = TimeOfDay, y = Calories, fill = TimeOfDay), width = 1, position = position_dodge(1.2)) + 
   labs( title = "Activity Level (Calories) by Day of the Week", x = "Time of Day", y="Calories", fill = "Time of Day") +
  scale_fill_brewer(palette = "Set2") +
  facet_grid(~DayOfWeek) + 
  theme(axis.text.x = element_text(angle = 90))

plot(Bar_DayOfTheWeek_ActivityLevel_Cal)
```

![](Capstone-Project-Case-Study-Bellabeat-Wellness-Tech_files/figure-html/unnamed-chunk-23-1.png)<!-- -->


Next up, we plot the average intensities of each day of the week as broken down by time of day using the code below.


```r
#Re-order the day of week to follow the typical calendar order
Tibble_Day_Time_Int$DayOfWeek <- factor(Tibble_Day_Time_Int$DayOfWeek, levels = c("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"))

#Re-order the day of week to follow the typical chronogological order
Tibble_Day_Time_Int$TimeOfDay <- factor(Tibble_Day_Time_Int$TimeOfDay, levels = c("Early Morning", "Morning", "Afternoon", "Evening", "Night", "Late Night"))

# Generate Bar graph
Bar_DayOfTheWeek_ActivityLevel_Int <- ggplot(data = Tibble_Day_Time_Int) +
  geom_col(mapping =  aes(x = TimeOfDay, y = AverageIntensity, fill = TimeOfDay), width = 1, position = position_dodge(1.2)) + 
   labs( title = "Activity Level (Average Intensity) by Day of the Week", x="Time of Day", y="Average Intensity", fill = "Time of Day") +
  scale_fill_brewer(palette = "Set2") +
  facet_grid(~DayOfWeek) + 
  theme(axis.text.x = element_text(angle = 90))

plot(Bar_DayOfTheWeek_ActivityLevel_Int)
```

![](Capstone-Project-Case-Study-Bellabeat-Wellness-Tech_files/figure-html/unnamed-chunk-24-1.png)<!-- -->


What do these grouped bar graphs tell us and is the data they provide consistent? One consistency I noticed is that regardless of whether the measure was by average calories or by average intensity, the most active time of the day where users burned the most calories was in the evenings on weekdays or in the afternoons on weekends. This makes sense as people generally have work during the day Monday through Friday and typically won't be active or exercise until after work in the evening. On the other hand, whereas most people are off on weekends, their preferred time for activity or exercise may be during the afternoon. The activity for late nights regardless of day of week also appears to be consistently low as thats the time people are generally asleep.


##### Case 3: Distribution between Calories Burned vs. Daily Activity Level

Lastly, we'll examaine the distribution between the number calories one burned in a single day vs. their activity lfor that day (fairly inactive, less active, more active, highly acive).. We can use the original "daily_activity" data frame before the merge with the sleep data frame. Since this data frame will contain all the original rows (including the ones we needed to delete to be able to perform the merge), we'll have a lot more data to work with, giving us more accurate and representative insights.

First, we can classify each session/day by their level of activity using one of the available parameters on our table. Since we've already established a strong correlation between "TotalSteps" and "Calories" we can base our classifications based on that distribution.


```r
#Print the distribution of TotalSteps
summary(daily_activity$TotalSteps)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##       0    3790    7406    7638   10727   36019
```

Based on the above distribution, we can classify each day according to the number of total steps using the following criteria:

Between 0 and 3790 Total Steps:  Fairly Inactive
Between 3791 and 7406 Total Steps: Less Active
Between 7407 and 10727 Total Steps: More Active
Between 10728 and 36019 Total Steps: Highly Active

We create a new column called "ActivityClassification" to store these new labels. 



A histogram helps to illustrate the count of each activity level classification versus how many calories were burned in that particular day. In addition, the median number of Calories burned is computed and plotted as a vertical line as reference.
   

```r
#Store the median value of Calories, which comes out to 2303.61, for plotting.
Calories.median = median(daily_activity$Calories)

#Generate plot
hist_Activity_Cal <- ggplot(daily_activity, aes(x = Calories, color = ActivityClassification)) + 
geom_histogram(fill="white", alpha=0.5, position="identity", binwidth = 50) + 
  geom_vline(data=daily_activity, aes(xintercept=Calories.median, col = "Median"),
             linetype="dashed")  +
  labs(title = "Histogram of Calories Burned by Activity Level", x = "Calories Bin", y = "Count", color = "Activity Classification")

plot(hist_Activity_Cal)
```

![](Capstone-Project-Case-Study-Bellabeat-Wellness-Tech_files/figure-html/unnamed-chunk-27-1.png)<!-- -->
Our histogram depicts a bi-modal distribution where there are two (or possibly three) "humps" in the graph. The first one or two humps, are to the left of the median line and primarily of "fairly inactive", "less active" and even a few "more active" classified days. Even days that were classified as "highly active" fell into the lower half of the median line. On the side of the spectrum, nearly all of the days where there were more calories burned than the median
number are largely classified as "highly active" or "more active" but there were a very small amount of "fairly inactive" and "less active" days.

A violin plot can also aid in our visualization of the distribution of the daily activity levels we created/classified each day by and the effective calories burned. One advantage of the violin plot over the histogram is that we can better see and more easily compare the densities of each activity level. This plot is generated with the below code.



```r
#Re-order the activity levels by increasing magnitude
daily_activity$ActivityClassification <- factor(daily_activity$ActivityClassification, levels = c("Fairly Inactive", "Less Active", "More Active", "Highly Active"))

Box_Activity_Cal <- ggplot(data = daily_activity, x =ActivityClassification, y=Distance) + 
  geom_violin(mapping = aes(x =ActivityClassification, y=Calories, fill=ActivityClassification)) +
  stat_summary(aes(x =ActivityClassification, y=Calories), fun = "mean", geom = "crossbar",color = "gold") +
  geom_hline(yintercept=Calories.median,linetype="dashed",size=1, color = "black") +
  labs(title="Daily Activity Level Vs. Calories Burned", x = "Activity Level Classification", y = "Calories Burned", fill = "Activity Level Classification")
  

plot(Box_Activity_Cal)
```

![](Capstone-Project-Case-Study-Bellabeat-Wellness-Tech_files/figure-html/unnamed-chunk-28-1.png)<!-- -->

Like with our previous histogram, we also plotted the global median number of Calories across all activity levels, which is represented by the dashed black line. Since we were able to breakdown the calories burned distribution level by activity level as well, we also plotted the individual median calories burned for each classification. This is represented by the solid gold lines.

Not only did our histogram and violin plots confirm the trends we expected but they also visualized an insight that wasn't so obvious before. From these graphs, we can see how huge of an overlap there is between the range of the minimum calories burned on a "highly active" day versus that of the maximum calories burned on a "fairly inactive" day. This value can be computed as shown:


```r
#Calculate the minimum calories burned on a highly active day
 daily_activity %>% 
    filter(ActivityClassification == "Highly Active") %>%
    pull(min(Calories)) %>%
    min()
```

```
## [1] 1551
```

```r
#Calculate the maximum calories burned on a fairly inactive day.
 daily_activity %>% 
    filter(ActivityClassification == "Fairly Inactive") %>%
    pull(max(Calories)) %>%
    max()
```

```
## [1] 3051
```


### Case Study Roadmap - Share

The preferable method of sharing these findings would be to do so using the RMarkdown file (.rmd) and publishing it either on a Data Science community such as Kaggle or via personal online portfolio. In-line R code is used throughout the case study documentation and analysis process, making sharing this .rmd file convenient to publish, easily accessible and simple to revisit and update as necessary.

#### Key tasks
1. Determine the best way to share your findings. -COMPLETE
2. Create effective data visualizations. -COMPLETE
3. Present your findings. -COMPLETE
4. Ensure your work is accessible. -COMPLETE

#### Deliverable
Supporting visualizations and key findings

### Case Study Roadmap - Act

This analysis of the fitness tracking smart device data as published and retrieved from Kaggle uncovered some important insights on the current ways as well as potential uses/benefits that Bellabeat Wellness Technology could explore.

Our very first analysis case focused on active lifestyles and whether there is any correlation with whether a sufficient or insufficient number of hours of sleep were achieved. Our first scatter plot showed the relationship between sleep and daily activity (as measured by total steps and calories). Our best fit linear line indicates a strong negative relationship between the number of minutes one spends a sleep vs. there activity level. However, the optimal amount of sleep is between 420 min (7 hours) and 560 min (9 hours). The points that had fallen within this band ranged widely between # of Calories burned as well as total steps taken. Our second scatter plot (which uses a gradient scale of Sedentary minutes instead of Calories) similarly shows his and reinforces this idea that the proper amount of sleep can be achieved regardless of how active your day is. However, in 44.1% of instances, users did not get the minimum 7 hours of sleep while in 9.5% of instances, users slept more than the maximum 9 hours. In total, 53.6% of the time, users do not get the recommended amount of sleep.

The insights from our first analysis can inspire a few new features for the Bellabeat app.

   * As our study recognizes the struggles and difficulties to get 7-9 hours of sleep, the app can send daily notifications on sleep or activity recommendations. For instance, on days where the app records a high level of activity (whether that be Calories burned or Steps taken), the app can send its user a soft reminder to try to get the recommended 7-9 hours of sleep and/or rest.
   
   * Likewise, if the app detects that users are constantly oversleeping, the app can send a soft reminder or suggestion to consider the amount of daily exercise and activity they are getting.
   
   * Lastly, in the situation where users are consistently getting less than 7 hours of sleep while showing indications of low activity, other health parameters such as stress can be looked to minimize work or personal tasks/responsibilities from acting as stressors that detract from getting sufficient amount of sleep. Perhaps, users who fall under these circumstances may benefit from meditation and mindfulness exercises. However, at this level, this is only an hypothesis and further work should be done for validation.

The second analysis case we investigated was the breakdown of activity level vs. the time of day and day of the week.To visualize this breakdown, we plotted 2 bar graphs: 1) Activity Level (as measured by Calories) vs. Day
of Week & Time of Day 2) Acitivity Level (as measured by Average Intensity) vs. Day of the Week & Time of Day. One noticeable observation is that the evening time tends to be the time of day where the most activity level is generally recorded, with the exception being on weekends where Saturday and Sunday afternoons are the most active times for users. This makes sense due to most people having work/class during the week while having Saturdays and Sundays off. Early morning, and even more so, Late night, is obviously the most consistent time of day for low activity, regardless of day of the week. As observed from our second bar graph (Average Activity Intensity), Sunday in general appears to be an overall low activity day.

Knowing what time of day and day of week users tend to be the most and least active is useful to know as it establishes a recognizable pattern. The following recommendations to Bellabeat can be made based on this information: 

* Create a feature on the Bellabeat app that enables users to "check in" at their local gyms and make that information visible to other users in real time (permission pending). Over time, this will help other users and gym goers to understand the expected crowd levels at their gym and plan their weekly visits to the gym accordingly to avoid the crowds.

* Partnering with gyms that allow the described "check in" feature above may enable them schedule fitness classes and training camps based on when they expect user's high activity level tendencies.

* At an individual level, the Bellabeat Spring (smart technology water bottle) can learn about your high level activity schedule based on time of day and day of week. Knowing this information, a feature can be added to automatically check its % filled and ping you a reminder to top it off/refill when it expects the need for hydration.

The third and final analysis delved into the distribution of calories burned with respect to the daily activity level classification as either "fairly inactive", "less active", "more active" and "highly active". The histogram generated for this analysis showed how all there were days for all activity level classifications that fell right around the median number of calories burned. But those days that were classified as highly active or more active tend to fall closer or to the left of the median line whereas less active or fairly inactive days were more likely to be at or to the left of the median line. This was an expected resulted and the following violin plot that was created further illustrated this. While it was no surprise that "highly active" days have the "highest highs" and "highest lows" of calories burned compared to the other classifications, the large amount of overlap of calories burned between these 4 classifications is an interesting observation. As computed, all 4 activity levels were represented in the 1551 to 3051 range of daily calories burned.


The results of this analysis lead to the following recommendations being made:

* The Bellabeat app and products should place a larger emphasis on providing daily encouragement and motivation to its user base. Especially for those aiming to lose weight, the # of calories one burns in a day is a key metric. Even if one didn't manage to take a whole lot of steps in a day ("fairly inactive or "less active"), this "lapse" in inactivity does not necessary put one off course and is not fatal in hitting one's daily calories burned goal.

* Bellabeat can utilize and track this data to perhaps provide its user with a midday "calories burned" forecast to inform its users what # of calories that they are on track to burn for the day. Whether the user's goal is to lose weight or gain weight, they can plan the rest of their day accordingly based on this forecast. For example, they can decide to go on an 30 minute walk around the neighborhood before dinner if they want to burn a little more calories or better plan what they consume for dinner or snack, as a means to maintain their target calorie balance.

* Since the violin plots are more "pointy" shaped at the high end of calories burned (as opposed to the lower end), our data is said to be more skewed toward higher daily number of calories burned. Bellabeat can introduce a "personal high score" system that reminds its users of their personal bests (whether that be total distance, total steps, calories burned, etc) and challenge them to beat that number and set a new daily high score.


#### Key tasks
1. Create your portfolio. -COMPLETE
2. Add your case study. -COMPLETE
3. Practice presenting your case study to a friend or family member. -COMPLETE


#### Deliverable
Your top high-level insights based on your analysis
