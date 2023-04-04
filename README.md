# Introduction
My name is Bobby and this is my second case study! Hoping I can implement my skills and experience working with the first case study and so fourth. You can contact me at "CHIENG@LIVE.CA" if you have any questions


# Ask
Everything going to be anaylzed using R Studio Desktop

1. What are some trends in smart device usage?

2. How could these trends apply to Bellabeat customers?

3. How could these trends help influence Bellabeat marketing strategy?


# Prepare

Download the dataset from Kaggle;
We will be working with daily_activities, daily_calories, sleep_day, daily_steps, daily_intensities and weightloginfo

Add data frames to match the file name

daily_intensities <-read.csv("dailyIntensities_merged.csv")

daily_activity <- read.csv("dailyActivity_merged.csv")

daily_calories <- read.csv("dailyCalories_merged.csv")

sleep_day <- read.csv("sleepDay_merged.csv")

weight_log <-read.csv("weightloginfo_merged.csv")

Now we have them in our data frame we should check the alignment/format of these collums so we could merge it!
colnames(daily_intensities, daily_activity, and so fourth)
As we can see they all have a similar collumn "ID" so we can merge it at ease later on.


# Proccess/Cleaning Using R Studio Desktop
