# Overview
This case study analyzes trends in smart device usage and explores how these trends could apply to Bellabeat customers. By analyzing data from fitness trackers, sleep trackers, and other smart devices, we aim to identify insights that can help inform Bellabeat's marketing strategy.
My name is Bobby and this is my second case study! Hoping I can implement my skills and experience working with the first case study and so fourth. You can contact me at "CHIENG@LIVE.CA" if you have any questions


# Ask
Everything going to be anaylzed using R Studio Desktop

1. What are some trends in smart device usage?

2. How could these trends apply to Bellabeat customers?

3. How could these trends help influence Bellabeat marketing strategy?

Install packages required:

```{r}
install.packages('tidyverse')
library(tidyverse)
```

```R
install.packages('ggplot2')
```






# Prepare
Download the dataset from Kaggle; [HERE](https://www.kaggle.com/datasets/arashnic/fitbit?resource=download)
(R Studio Desktop)

Open R Studio Desktop and create a new project. Set the project's working directory to the folder where you saved the dataset
C:\Users\YOUR_NAME\Desktop\BellaBeat_Case_Study

We need to add data frames to match each CSV file we are working with
Ill be using these data frames for my anaylsis. You could use different ones.
                              
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


# Process/Clean Data

```R
Check for any nulls - If it comes out as TRUE then you have nulls, false = no nulls

is.na(daily_activity)

is.na(daily_intensities)

is.na(daily_calories)

is.na(weight_log)
```

```R
Check for duplicates
duplicates <- duplicated(daily_activity)
duplicates <- duplicated(daily_intensities)
duplicates <- duplicated(daily_calories)
duplicates <- duplicated(weight_log)
duplicates <- duplicated(sleep_day)
duplicates <= TRUE

```



```R
There seems to be a problem with the date change the format because its identifying as numerical errors

daily_activity <- daily_activity %>% mutate( Weekday = weekdays(as.Date(ActivityDate, "%m/%d/%Y")))
```




                
           
