# Fitbit
Description:
  This is my personal project aiming to represent my basic knowledge and skill to analyze data by using spreadsheet, SQL and R.

Objective: 
  To figure out a customer's behavior using smart device, and analyze what new product ought to be launched to the market.

Source/Dataset:
  Fitbit Fitness Tracker Data by Kaggle (https://www.kaggle.com/datasets/arashnic/fitbit)
  
Steps:
  This report was separated into 6 steps, including with Ask, Prepare, Process, Analyze, Share and Act, in order to describe a methodology and tools used through the project to acheive the effective outcomes.
  
Ask:
  - What is current customer's behavior using smart device?
  - According to the data, what smart device tend to be appropirate to the customers in the future?

Prepare:
  Data Preparing:
   Referring to the source of data, there are numerous dataset which is able to use in the project. However, according to the project's objective, I decided to use 2 datasets which are dailyActivity_merged.csv containing a record of customer id, date, time, exercising time, exercising distance and burnt calories, and sleepDaymerged.csv which includes a data of customer id, date, total minutes of sleep.
   
  Tools Preparing:
   Due to a massive amount of data, I chose to use spreadsheet to clean and format the datasets, and use SQL in order to organize and manipulate the massive data. In term of visualizing data, I used R for creating and visualizing a data in a graph ways.
   
Process:
  Firstly, I downloaded a 2 datasets into csv file, I then uploaded it on Googlesheet to clean it. Afterward, I realized that a date column of both dailyActivity and sleepDay files were in a different format in its column, some were formatted in date, some were plain text. As well as, a date format due to a different time zone that I used DD/MM/YYYY, but it should actually be MM/DD/YYYY. Therefore, just changing its format wasn't enough to fix it.
  ![Different format of Date](https://user-images.githubusercontent.com/113785212/190891383-62b867e1-e03c-4c4b-8177-fab73ca6b463.png)
  In order to clean and format the data, I inserted a new column on the right side of date column to re-format it by using a formulas
