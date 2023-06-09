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
install.packages('tidyverse') - For extracting data
library(tidyverse)
```

```R
install.packages('ggplot2') - For visulization
library(ggplot2)
```


```r
insta..packages('dplyr') - Manipulate data
library(dplyr)
``` 

```r 
install.packages("skimr") - For summarizing data
library(skimr)
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


# Merge sleep_day and daily_activity
combined_data <- merge(sleep_day, daily_activity, by = "Id")

# Merge combined_data with daily_calories
combined_data <- merge(combined_data, daily_calories, by = "Id")

# Merge combined_data with daily_intensities
combined_data <- merge(combined_data, daily_intensities, by = "Id")

# Merge combined_data with daily_steps
combined_data <- merge(combined_data, daily_steps, by = "Id")

```

# Share Results (visualization)
![alt text](https://github.com/databubs/BellaBeat_Case/blob/main/Plot%20daily%20sedentary%20minutes%20and%20calories%20burned.png)


![alt text](https://github.com/databubs/BellaBeat_Case/blob/main/Daily_Calories_Steps.png)

![alt text](https://github.com/databubs/BellaBeat_Case/blob/main/SedMinutes.png)

```R
ggplot(calories_by_activity_long, aes(x = Activity, y = Calories)) + 
  geom_point(aes(colour = SedentaryMinutes)) + 
  scale_colour_gradient(low = "blue", high = "red") + 
  labs(x = "Activity", y = "Calories", colour = "Sedentary Minutes")
```
![alt text](https://github.com/databubs/BellaBeat_Case/blob/main/Relationships_Activity_Calories_Burned.png)

```R
library(ggplot2)

ggplot(combined_data, aes(x = SedentaryMinutes, y = Calories.x)) + 
  geom_point(aes(color = "Sedentary")) +
  geom_point(aes(x = LightlyActiveMinutes, color = "Lightly Active")) + 
  geom_point(aes(x = FairlyActiveMinutes, color = "Fairly Active")) + 
  geom_point(aes(x = VeryActiveMinutes, color = "Very Active")) + 
  labs(x = "Activity Minutes", y = "Calories Burned", 
       title = "Relationship between Activity Intensity and Calories Burned",
       color = "Activity Intensity")
```


# Act/Suggestions

Looking at our plots we can tell that not many participants are as active as others and I have a few suggestions!

1. Develop an alarm feature that alerts user when they should start their excercise based on a specific time

2. Implement a social group where you can compete with others depending on their postal code for a giftcard certificate

3. A safetey feature where if you fall or get injured there should be a button to contact near by authorities 


                
           
