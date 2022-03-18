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
 
Data used: Daily Activity, Hourly Calories, Hourly Intensities, Sleep Day, Heart Rate, Weight Log Infor.

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

Explore and Summary Data
```Python
len(dailyActivity_merged.Id.unique()) # 33
len(hourlyCalories_merged.Id.unique()) # 33
len(hourlySteps_merged.Id.unique()) # 33
len(sleepDay_merged.Id.unique()) # 24
len(weightLogInfo_merged.Id.unique()) # 8
```
There are 33 users ID recorded in Activity, Calores and Steps file while there are 24 users Id in SleepDay and only 8 in Log Infor. Only 8 users Id is not enough to make good suggestions based on this data.

Look at distribution between Calories and active minutes of Daily Activity Data

![Calories and minutes](https://user-images.githubusercontent.com/58326661/159021203-ff84030d-a172-40c1-84ee-3ca1906a0394.png)


The calories is mainly focus from 1500 to 4000 corresponding fairy active minutes from 0 -> 80 mins, lightly active minutes is 0->500, sendentary minutes is 550 -> 1450 mins, and very active minutes is from 0-> 120 mins 




![Calories and TotalStep](https://user-images.githubusercontent.com/58326661/159027233-50c27c0b-d99f-4903-867b-58eb66cf2a60.png)

While , Total Step mainly focus from 0 to 20K per day.


