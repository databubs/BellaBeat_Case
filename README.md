# Overview
This case study analyzes trends in smart device usage and explores how these trends could apply to Bellabeat customers. By analyzing data from fitness trackers, sleep trackers, and other smart devices, we aim to identify insights that can help inform Bellabeat's marketing strategy.
My name is Bobby and this is my second case study! Hoping I can implement my skills and experience working with the first case study and so fourth. You can contact me at "CHIENG@LIVE.CA" if you have any questions

# Scenario 
You are a junior data analyst working on the marketing analyst team at Bellabeat, a high-tech manufacturer of health-focused
products for women. Bellabeat is a successful small company, but they have the potential to become a larger player in the
global smart device market. Urška Sršen, cofounder and Chief Creative Officer of Bellabeat, believes that analyzing smart
device fitness data could help unlock new growth opportunities for the company. You have been asked to focus on one of
Bellabeat’s products and analyze smart device data to gain insight into how consumers are using their smart devices. The
insights you discover will then help guide marketing strategy for the company. You will present your analysis to the Bellabeat
executive team along with your high-level recommendations for Bellabeat’s marketing strategy.


# Ask
Everything going to be anaylzed using R Studio Desktop

1. What are some trends in smart device usage?

2. How could these trends apply to Bellabeat customers?

3. How could these trends help influence Bellabeat marketing strategy?

## Install packages required:

```{r}
install.packages('tidyverse')
library(tidyverse)
```

```R
install.packages('ggplot2')
library(ggplot2)
```

```r
insta..packages('dplyr')
library(dplyr)
```





# Prepare
Download the dataset from Kaggle; [HERE](https://www.kaggle.com/datasets/arashnic/fitbit?resource=download)
(R Studio Desktop)

Open R Studio Desktop and create a new project. Set the project's working directory to the folder where you saved the dataset
C:\Users\YOUR_NAME\Desktop\BellaBeat_Case_Study

We need to add data frames to match each CSV file we are working with
Ill be using these data frames for my anaylsis. You can use different ones.

Creating Data Frames
```R
daily_intensities <- read.csv("dailyIntensities_merged.csv")
daily_activity <- read.csv("dailyActivity_merged.csv")
daily_calories <- read.csv("dailyCalories_merged.csv")
sleep_day <- read.csv("sleepDay_merged.csv")
weight_log <- read.csv("weightloginfo_merged.csv")
```     


## See what collums they provide

```R
colnames(daily_intensities)
colnames(daily_activity)
colnames(daily_calories)
colnames(sleep_day)
colname(weight_log)
```
Notice how all the dataframes have one similar collumn? BINGO! "ID" we can later on merge them together!

# Process/Cleaning Data

Check for any nulls - If it comes out as TRUE then you have nulls, false = no nulls
```R

is.na(daily_activity)

is.na(daily_intensities)

is.na(daily_calories)

is.na(weight_log)
```
Check for duplicates
```R
duplicates <- duplicated(daily_activity)
duplicates <- duplicated(daily_intensities)
duplicates <- duplicated(daily_calories)
duplicates <- duplicated(weight_log)
duplicates <- duplicated(sleep_day)
print(duplicates)

```
Seems to have a slight problem refering to the date format in daily_activity - numberical error when trying to merge!
```R
daily_activity <- daily_activity %>% mutate( Weekday = weekdays(as.Date(ActivityDate, "%m/%d/%Y")))
```


# CHECK POINT

This is a check point to remind yourself what you have done so far :)

Check each collums of the data frame to make sure they can merge using "ID" 

Loaded CSV files and imported using R Studio  ✔️

Check for nulls and duplicates ✔️



# Understanding the data
```r
daily_activity %>%  
  select(TotalSteps,
         TotalDistance,
         SedentaryMinutes) %>%
  summary()

 
 TotalSteps    TotalDistance    SedentaryMinutes
 Min.   :    0   Min.   : 0.000   Min.   :   0.0  
 1st Qu.: 3790   1st Qu.: 2.620   1st Qu.: 729.8  
 Median : 7406   Median : 5.245   Median :1057.5  
 Mean   : 7638   Mean   : 5.490   Mean   : 991.2  
 3rd Qu.:10727   3rd Qu.: 7.713   3rd Qu.:1229.5  
 Max.   :36019   Max.   :28.030   Max.   :1440.0  
```
 
```r
 TotalSleepRecords TotalMinutesAsleep TotalTimeInBed 
 Min.   :1.000     Min.   : 58.0      Min.   : 61.0  
 1st Qu.:1.000     1st Qu.:361.0      1st Qu.:403.0  
 Median :1.000     Median :433.0      Median :463.0  
 Mean   :1.119     Mean   :419.5      Mean   :458.6  
 3rd Qu.:1.000     3rd Qu.:490.0      3rd Qu.:526.0  
 Max.   :3.000     Max.   :796.0      Max.   :961.0


summary(daily_steps$StepTotal)
 Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
      0    3790    7406    7638   10727   36019 
     
```

```r
 summary(daily_intensities)
       Id            ActivityDay        SedentaryMinutes
 Min.   :1.504e+09   Length:940         Min.   :   0.0  
 1st Qu.:2.320e+09   Class :character   1st Qu.: 729.8  
 Median :4.445e+09   Mode  :character   Median :1057.5  
 Mean   :4.855e+09                      Mean   : 991.2  
 3rd Qu.:6.962e+09                      3rd Qu.:1229.5  
 Max.   :8.878e+09                      Max.   :1440.0  
 LightlyActiveMinutes FairlyActiveMinutes VeryActiveMinutes
 Min.   :  0.0        Min.   :  0.00      Min.   :  0.00   
 1st Qu.:127.0        1st Qu.:  0.00      1st Qu.:  0.00   
 Median :199.0        Median :  6.00      Median :  4.00   
 Mean   :192.8        Mean   : 13.56      Mean   : 21.16   
 3rd Qu.:264.0        3rd Qu.: 19.00      3rd Qu.: 32.00   
 Max.   :518.0        Max.   :143.00      Max.   :210.00   
 SedentaryActiveDistance LightActiveDistance ModeratelyActiveDistance
 Min.   :0.000000        Min.   : 0.000      Min.   :0.0000          
 1st Qu.:0.000000        1st Qu.: 1.945      1st Qu.:0.0000          
 Median :0.000000        Median : 3.365      Median :0.2400          
 Mean   :0.001606        Mean   : 3.341      Mean   :0.5675          
 3rd Qu.:0.000000        3rd Qu.: 4.782      3rd Qu.:0.8000          
 Max.   :0.110000        Max.   :10.710      Max.   :6.4800          
 VeryActiveDistance
 Min.   : 0.000    
 1st Qu.: 0.000    
 Median : 0.210    
 Mean   : 1.503    
 3rd Qu.: 2.053    
 Max.   :21.920
```


![alt text](https://scontent.fyvr4-1.fna.fbcdn.net/v/t39.30808-6/278375259_3173522536223995_4691224045261329961_n.jpg?_nc_cat=105&ccb=1-7&_nc_sid=09cbfe&_nc_ohc=6vzpvMf6xHgAX8vRKT0&_nc_ht=scontent.fyvr4-1.fna&oh=00_AfAQYGXTLR97gS-fhBx9uvhlabErznUf6e1wSb-geUCNjQ&oe=64389416)

                
           
