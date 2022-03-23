<h1 align="center">Bellabeat Project</h1>

#### Author: Nguyen Duong Khai

##### Introduction

Bellabeat is a high-tech manufacturer of healthy focused products for women. It includes bellabeat app which provide users data relate to their activity, sleep, stress and mindfulness habits and wellness tracker devices such as watch, or necklet used to connect to beallbeat app checking health information. In addition , the product provide a water bottle exams water intake every day. When connected to Beallabeat, users could know their hydration levels. The Bellabeat member is allowed to access the app  24/7 to be helped on nutrition, activity, sleep and beauty, and mindfulness based on their lifestyle and goals. Since it was established in 2013, Bellabeat has a rapid growth about a teach-driven wellness company for women. One of the reason, they has invested traditional advertising media, such as radio, out-of-home billboards, print, and television, but focuses on digital marketing extensively. Sršen , Bellabeat’s cofounder and Chief Creative Officer, knows that an analysis of Bellabeat’s available consumer data would reveal more opportunities for growth. She has asked the marketing analytics team to focus on a Bellabeat product and analyze smart device usage data to gain insight into how people are already using their smart devices

#### Objective Business
Working as a data analysist, I should identify trends in smart device usage and apply these trends to Bella Product. Then, suggest marketing strategy to help Bellabeat.
##### Importing Datasets 
Loading package

``` Python
import pandas as pd
```
Loading CSV file
 For this project, I will use Fitbit Fitness Tracker [Data](https://www.kaggle.com/arashnic/fitbit)
 
Data used: Daily Activity, Hourly Calories, Hourly Step, Sleep Day, Heart Rate, Weight Log Infor.

``` Python
dailyActivity_merged = pd.read_csv(path + 'dailyActivity_merged.csv')
hourlyCalories_merged = pd.read_csv(path + 'hourlyCalories_merged.csv')
hourlySteps_merged = pd.read_csv(path + 'hourlySteps_merged.csv')
sleepDay_merged = pd.read_csv(path + 'sleepDay_merged.csv')
weightLogInfo_merged = pd.read_csv(path + 'weightLogInfo_merged.csv')
```
I want to see some of row file of Daily Activity by using head() function
``` Python
dailyActivity_merged.head()
```
![image](https://user-images.githubusercontent.com/58326661/158985838-2aee9f07-a6fc-44f4-887a-e46f3ecf15ca.png)

Data Cleaning
To check if data with missing value by using isnum().sum() funtion.For example:
```Python
dailyActivity_merged.isnull().sum()
```
I found it, there are 65 missing value of "Fat" columns in Weight Log Infor. Howerver, I did not go further to deep Weight data, just remains unchaged it.

#### Explore and Summary Data
```Python
len(dailyActivity_merged.Id.unique()) # 33
len(hourlyCalories_merged.Id.unique()) # 33
len(hourlySteps_merged.Id.unique()) # 33
len(sleepDay_merged.Id.unique()) # 24
len(weightLogInfo_merged.Id.unique()) # 8
```
There are 33 users ID recorded in Activity, Calores and Steps file while there are 24 users Id in SleepDay and only 8 in Log Infor. Only 8 users Id is not enough to make good suggestions based on this data.




Now, look at the summary of Total Steps, Total Distacne and active minutes.
``` Python
# Activity
average_user_dailyActivity = dailyActivity_merged.groupby('Id')[['TotalSteps','TotalDistance','VeryActiveMinutes',
                                                              'FairlyActiveMinutes','LightlyActiveMinutes',
                                                              'SedentaryMinutes','Calories']].mean()
average_user_dailyActivity.describe()

# Sleep
sleepDay_average = sleepDay_merged.groupby('Id')[['TotalSleepRecords', 'TotalMinutesAsleep','TotalTimeInBed']].mean()
sleepDay_average.describe()

# Weight
weight_average = weightLogInfo_merged.groupby('Id')[['BMI','WeightKg']].mean()
weight_average.describe()
```
 
 ![image](https://user-images.githubusercontent.com/58326661/159144048-cf502323-33e2-407a-b09b-79ee307fc4a9.png)
 
 ![image](https://user-images.githubusercontent.com/58326661/159145511-14ce2240-7a08-49be-af3e-979f5ae034a7.png)
 
 ![image](https://user-images.githubusercontent.com/58326661/159144152-3c4c49e3-08b5-418a-a915-80414fc90675.png)     


Before going to summary the data, firstly, I grouped the same Id because I belived it increases accurately of dataset instead summary all of dataset.
There are some interesting points, from this summary:

 Average sedentary minutes nearly 1000 minutes, more than 16 hours. Should be reduced

 Sendentary occurs most of minutes in the active minutes.

 The CDC recommend that most adults aim for 10,000 steps per day but the average step is 7500. Need to improve !

 The average sleep per day is 380 mins corresponding 6 hours a day. 


#### Visualazation

Before visualizing the data, I want to make a column named the day_of_week in Daily Activity and hour from Hourly Step.
```Python
dailyActivity_merged['day_of_week'] = (pd.to_datetime(dailyActivity_merged.ActivityDate)
                                                                          .dt.dayofweek) 
hourlySteps_merged['hour'] = pd.to_datetime(hourlySteps_merged.ActivityHour).dt.hour
```

Look at distribution between Calories and active minutes of Daily Activity Data

![Calories and minutes](https://user-images.githubusercontent.com/58326661/159021203-ff84030d-a172-40c1-84ee-3ca1906a0394.png)


The calories is mainly focus from 1500 to 4000 corresponding fairy active minutes from 0 -> 80 mins, lightly active minutes is 0->500, sendentary minutes is 550 -> 1450 mins, and very active minutes is from 0-> 120 mins 

![Calories and TotalStep](https://user-images.githubusercontent.com/58326661/159027233-50c27c0b-d99f-4903-867b-58eb66cf2a60.png)

There are postive relationship between Calories and Total Step.With Calores from 1500 to 4000 Total Step mainly focus from 0 to 20K per day.
![Very Actiminutes per day of week](https://user-images.githubusercontent.com/58326661/159218449-825019d3-30d3-4ff5-bb57-fb84d9572fe6.png)
Active minutes reaches a peak on a Monday then starting to drop to the bottom on Thursday and it is recovered on Saturday but drop after a Sunday.

![Calories and Total Steps per day of week](https://user-images.githubusercontent.com/58326661/159219155-fe6c48dd-9a0c-4e9d-8165-ed0810e549d1.png)
The chart shows a strong relationship between Calories and Steps per day of week through both increase and decrease together. While both reaches a top on Tuesday and Saturday, Calories drop a bottom on Thursday and Total Step is on Sunday


![Total Step  over time](https://user-images.githubusercontent.com/58326661/159219240-d8dae87b-0bae-4302-a144-8f6fab5b6068.png)
The total step is rising from 5:00 and then reaches a top at 19:00 and start to drop from this hour.

Recommendation



