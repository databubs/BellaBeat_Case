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
(Tidying codes)

```R
install.packages('ggplot2')
library(ggplot2)
```
(Visulization charts ranging to bar, and pies.)

```r
insta..packages('dplyr')
library(dplyr)
```
(Filters, organizes, mutates desired columns)
```r
install.packages("skimr")
library(skimr)
```
(Reads data for cleaning quicker)


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

```R
 See what collums they provide

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

Data Summary
```R
skim_without_charts(daily_activity)
skim_without_charts(daily_calories)
skim_without_charts(daily_intensities)
skim_without_charts(daily_steps)
skim_without_charts(sleep_day)
skim_without_charts(weight_log)
```


# CHECK POINT

This is a check point to remind yourself what you have done so far :)

Loaded CSV files and imported using R Studio  ✔️

Check for nulls and duplicates ✔️

Summarize and familarize yourself within each column ✔️

Double checked colnames and made sure they are mergable ✔️


# Merge
```r
merged_data <- merge(combined_data, daily_calories, by="Id")
merged_data <- merge(merged_data, daily_intensities, by="Id")
merged_data <- merge(merged_data, daily_steps, by="Id") - ********
merged_data <- merge(merged_data, weight_log, by="Id")
```

# Share Results (visualization)
![alt text](https://github.com/databubs/BellaBeat_Case/blob/main/Plot%20daily%20sedentary%20minutes%20and%20calories%20burned.png)
![alt text](https://github.com/databubs/BellaBeat_Case/blob/main/Daily_Calories_Steps.png)
![alt text](https://github.com/databubs/BellaBeat_Case/blob/main/TOTALSTEPS.png)
![alt text](https://github.com/databubs/BellaBeat_Case/blob/main/Weight_LOG.png)

# My Conclusion

In conclusion you can see that the data set





![alt text](https://scontent.fyvr4-1.fna.fbcdn.net/v/t39.30808-6/278375259_3173522536223995_4691224045261329961_n.jpg?_nc_cat=105&ccb=1-7&_nc_sid=09cbfe&_nc_ohc=6vzpvMf6xHgAX8vRKT0&_nc_ht=scontent.fyvr4-1.fna&oh=00_AfAQYGXTLR97gS-fhBx9uvhlabErznUf6e1wSb-geUCNjQ&oe=64389416)

                
           
