<h1 align="center">Bellabeat Project</h1>

#### Author: Nguyen Duong Khai

##### [Dashboard](https://public.tableau.com/views/Bella_16475280530160/Bella_Dashboard?:language=en-GB&:display_count=n&:origin=viz_share_link)

##### [Jupiter](Fitbit_Data_Analysis.ipynb)

# 
The project follow the steps of the data analysis process : 

### [Ask](#1-Ask)
### [Prepare](#2-Prepare)
### [Process](#3-Process)
### [Analyzie](#4-Analyze)
### [Share](#5-Share)
### [Act](#6-Act)

## Introduction

Bellabeat is a high-tech manufacturer of healthy focused products for women. It includes bellabeat app which provide users data relate to their activity, sleep, stress and mindfulness habits and wellness tracker devices such as watch, or necklet used to connect to beallbeat app checking health information. In addition , the product provide a water bottle exams water intake every day. When connected to Beallabeat, users could know their hydration levels. The Bellabeat member is allowed to access the app  24/7 to be helped on nutrition, activity, sleep and beauty, and mindfulness based on their lifestyle and goals. Since it was established in 2013, Bellabeat has a rapid growth about a teach-driven wellness company for women. One of the reason, they has invested traditional advertising media, such as radio, out-of-home billboards, print, and television, but focuses on digital marketing extensively. Sršen , Bellabeat’s cofounder and Chief Creative Officer, knows that an analysis of Bellabeat’s available consumer data would reveal more opportunities for growth. She has asked the marketing analytics team to focus on a Bellabeat product and analyze smart device usage data to gain insight into how people are already using their smart devices

## 1/ Ask
**Business task**: Working as a data analysist, I should identify trends in smart device usage and apply these trends to Bella Product. Then, suggest marketing strategy to help Bellabeat.

##### Importing Datasets 

## 2/ Prepare data
For this project, I use Fitbit Fitness Tracker [Data](https://www.kaggle.com/arashnic/fitbit)

This dataset generated by respondents to a distributed survey via Amazon Mechanical Turk between 03.12.2016-05.12.2016. Thirty eligible Fitbit users consented to the submission of personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring. Individual reports can be parsed by export session ID (column A) or timestamp (column B). Variation between output represents use of different types of Fitbit trackers and individual tracking behaviors / preferences. 

Limitations of this data such as the size of data sample and outdor-indoor activities would narrow the scope of analysis.

Data used: Daily Activity, Hourly Calories, Hourly Step, Hour Intensity, Sleep Day, and Weight Log Infor.


Loading package

``` Python
import pandas as pd
```
Loading CSV file
 

``` Python
dailyActivity_merged = pd.read_csv(path + 'dailyActivity_merged.csv')
hourlyCalories_merged = pd.read_csv(path + 'hourlyCalories_merged.csv')
hourlySteps_merged = pd.read_csv(path + 'hourlySteps_merged.csv')
hourlyIntensities_merged = pd.read_csv(path + 'hourlyIntensities_merged.csv')
sleepDay_merged = pd.read_csv(path + 'sleepDay_merged.csv')
weightLogInfo_merged = pd.read_csv(path + 'weightLogInfo_merged.csv')
```
## 3/ Process

Data Cleaning
To check if data used with missing value by using isnum().sum() funtion.For example:
```Python
dailyActivity_merged.isnull().sum()
```
I found it, there are 65 missing value of "Fat" columns in Weight Log Infor data. Howerver, I did not go further deeply Weight data, just remains unchaged it.

Next, checking how many people recorded their result in each of data.

```Python
len(dailyActivity_merged.Id.unique()) # 33
len(hourlyCalories_merged.Id.unique()) # 33
len(hourlySteps_merged.Id.unique()) # 33
len(sleepDay_merged.Id.unique()) # 24
len(weightLogInfo_merged.Id.unique()) # 8
```
There are 33 users ID recorded in Activity, Calores and Steps file while there are 24 users Id in SleepDay and only 8 in Log Infor. Only 8 users Id is not enough to make good suggestions based on this data.

Create a new column like day_of_week and hour from dataset by extracting columns which is a type of datetime.

```Python
# Monday = 0, Sunday = 6
dailyActivity_merged['day_of_week'] = (pd.to_datetime(dailyActivity_merged.ActivityDate).dt.dayofweek)
hourlyIntensities_merged['hour'] = pd.to_datetime(hourlyIntensities_merged['ActivityHour']).dt.hour
```


## 4/ Analyze


Now, look at the summary of Total Steps, Total Distacne and active minutes.

![image](https://user-images.githubusercontent.com/58326661/159964142-c578b4b5-a8d4-4352-89cd-1fe44df0e346.png)
 
 ![image](https://user-images.githubusercontent.com/58326661/159964184-130be858-c4d2-4bc0-b328-629b9d814b83.png)

![image](https://user-images.githubusercontent.com/58326661/159964361-ca20f717-a314-481d-8ad0-2ef37fef5750.png)


Before going to summary the data, firstly, I grouped the same Id because I belived it increases accurately of dataset instead summary all of dataset.
There are some interesting points, from this summary:

- Average sedentary minutes nearly 1000 minutes, more than 16 hours. Should be reduced

- Sendentary occurs most of minutes in the active minutes.

- The CDC recommend that most adults aim for 10,000 steps per day but the average step is 7500. Need to improve !

- The average sleep per day is 380 mins corresponding 6 hours a day. 

![image](https://user-images.githubusercontent.com/58326661/160088421-63fe9550-6614-49d6-97e5-25630cf858d9.png)

42 mins is the diffenrece between the time in bed and the time feel asleep



### Visualization



![Calories and active mins](https://user-images.githubusercontent.com/58326661/159988545-79b333d9-6c99-46de-8323-57ca234ea040.png)

The calories is mainly focus from 1500 to 4000 corresponding fairy active minutes from 0 -> 80 mins, lightly active minutes is 0->500, sendentary minutes is 550 -> 1450 mins, and very active minutes is from 0-> 120 mins 

![Very active minutes per day of week](https://user-images.githubusercontent.com/58326661/159988804-4fcb8d89-78ee-468e-8e67-a7a9ef76c172.png)

Active minutes reaches a peak on a Monday then starting to drop to the bottom on Thursday and it is recovered on Saturday but drop after a Sunday.

![Calories and Total Steps per day of week](https://user-images.githubusercontent.com/58326661/159989208-ed612306-5033-4cf1-a29b-ba98e54d88f3.png)

The chart shows a strong relationship between Calories and Steps per day of week through both increase and decrease together. While both reaches a top on Tuesday and Saturday, Calories drop a bottom on Thursday and Total Step is on Sunday

![Intensity vs Hour](https://user-images.githubusercontent.com/58326661/159988744-3c952d1f-8f66-428a-b76b-041d74a43f5b.png)


The Intensity is rising from 5:00 and then reaches a top at 19:00 and start to drop from this hour.It reaches a peach between 6 and 7 pm. Based on this time, we encourage users consuming more energy by going to gym or play sports or exercises.

![Sleep vs Sendentary Mintues](https://user-images.githubusercontent.com/58326661/159988920-25bd8a19-d83e-4789-936f-4d865600e11a.png)

There are a negative relationship between Sleep and Sendentary Minutes. To improve better sleep, Bella users must reduce sedentary minutes.

## 5 / Sharing 

![Bella_Dashboard](https://user-images.githubusercontent.com/58326661/160078841-e9f90326-1b0c-4094-9282-e71c2498a514.png)

## 6/ Act

After analyzing dataset, I found some insight data which could help the company have a some markerting strategy

### Target Audience

More than 16 hours for sedentary minutes desmonstrates the women spends a lot of time in front of computer to work and only spends 20 mins for active minutes . It means  they seems not to excercise. Hence, the company need to have a nice strategy encourage users to stay healthy. 

Recommendation for the Bellbeat Apps:
- Send the totification to their phone a list of task  per day such as have an average step 8000 everyday
- To improve a better sleep, the app need to warm users reduce a sendentary minutes or a time lying the bed for social media.  
- Encourage a gym or play sport on 18:00 - 19:00 to improve their healthy instead of other time, because in this time, they consume a lot of intenssity.
