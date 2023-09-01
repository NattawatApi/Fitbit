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
   Referring to the source of data, there are numerous dataset which is able to use in the project. However, according to the project's objective, I decided to use 2 datasets which are dailyActivity_merged.csv containing a record of customer id, date, time, exercising time, exercising distance and burnt calories, and sleepDay_merged.csv which includes a data of customer id, date, total minutes of sleep.
   
  Tools Preparing:
   Due to a massive amount of data, I chose to use spreadsheet to clean and format the datasets, and use SQL in order to organize and manipulate the massive data. In term of visualizing data, I used R for creating and visualizing a data in a graph ways.
   
Process:
  Firstly, I downloaded a 2 datasets into csv file, I then uploaded it on Googlesheet to clean it. Afterward, I realized that a date column of both dailyActivity and sleepDay files were in a different format in its column, some were formatted in date, some were plain text. As well as, a date format due to a different time zone that I used DD/MM/YYYY, but it should actually be MM/DD/YYYY. Therefore, just changing its format wasn't enough to fix it.
  
  ![Different format of Date](https://user-images.githubusercontent.com/113785212/190891383-62b867e1-e03c-4c4b-8177-fab73ca6b463.png)
  
  In order to clean and format the data, I inserted a new column on the right side of date column to re-format it by using a formula "=ARRAYFORMULA(DATE(RIGHT($B$2:$B,4),LEFT($B$2:$B,2),MID($B$2:$B,4,2)))", and pasted the adjusted date into column B.
  
  ![Adjusted Date Column](https://user-images.githubusercontent.com/113785212/190892904-20adc3ec-23fe-4c0e-bc65-d0798aeda1d3.png)

  Furthermore, I would like to analyze what day is the most active day of customer. Thus, I add a column indicating the day which is named "Day" by writing a formula "=ARRAYFORMULA(TEXT($C$2:$C,"DDDD"))".

  ![Add New Column Indicating the Day](https://user-images.githubusercontent.com/113785212/190904892-48419f57-b8ac-4183-adc4-8e11f5b0e95b.png)
  
  But only cleaning the data in dailyActivity_merged.csv file wasn't enough. Consequently, I had to clean the data in sleepDay_merged.csv as well, which the entire steps of cleaning was as same as the step of dailyActivity_merged.csv as I mentioned earlier.
  
Analyze:
  After cleaning all data, I decided to use SQL to manipulate and organize data. So, I uploaded the prepared files on BigQuery, and manipulated it. Referring to the objectives, I would like to analyze both activity and sleep data having the day as a primary key. Thereby, I had to organize and merge the data from both tables into a new one. As a result, I eventually created the new table by coding SQL, the code is stored in "SQL_Fitbit" file in the repository:
  
  ![Summarized Table](https://user-images.githubusercontent.com/113785212/190912448-a5f481e6-6653-438c-9b05-a280ce425788.png)

  The code gave me the table of summarized data having the day as a primary key, a total customers exercising each day, a total step that customers took each day, a total distance each day, and a total minute customers slept each day.
  
  Additionally, I also analyze the correlation betwwen customer's sleep behavior and exercising behavior by coding on R with the following code:
  
  "fb <- read_csv("fitbit.csv")
  
  cor(fb$total_sleep_min,fb$total_distance)"
  
  The result came out that the correlation of total distance and total sleep is 0.67. It seems that both of them are slightly related to each others.
  
Share:
  To understanably visualize a summarized data, I decided to display it in 4 bar charts showing a different data contained in each column. Consequently, I used R to visualize and summarized it by writing the following code:
  
"fb <- read_csv("fitbit.csv")

id <- select(fb, day, total_customer)

step <- select(fb, day, total_step)

distance <- select(fb, day, total_distance)

sleep <- select(fb, day, total_sleep_min)

id_plot <- ggplot(data=id, aes(factor(fb$day, level = unique(fb$day)), total_customer, fill = day)) +
  geom_bar(stat = "Identity") + labs(title = "Total Customer Each Day", x = "Day", y = "Customers") +
  theme(text = element_text(size = 8))
  
step_plot <- ggplot(data=step, aes(factor(fb$day, level = unique(fb$day)), total_step, fill = day)) +
  geom_bar(stat = "Identity") + labs(title = "Total Step Each Day", x = "Day", y = "Steps") +
  theme(text = element_text(size = 8))
  
dist_plot <- ggplot(data=distance, aes(factor(fb$day, level = unique(fb$day)), total_distance, fill = day)) +
  geom_bar(stat = "Identity") + labs(title = "Total Distance Each Day", x = "Day", y = "Distance") +
  theme(text = element_text(size = 8))
  
sleep_plot <- ggplot(data=sleep, aes(factor(fb$day, level = unique(fb$day)), total_sleep_min, fill = day)) +
  geom_bar(stat = "Identity") + labs(title = "Total Sleep Each Day", x = "Day", y = "Sleep Minutes") +
  theme(text = element_text(size = 8))

grid.arrange(id_plot, step_plot, dist_plot, sleep_plot, ncol = 2)"

  ![Fitbit Bar Charts](https://user-images.githubusercontent.com/113785212/191079070-1fd0d4a7-7e08-4bb5-a397-fea3d4cde9c8.png)
  [Fitbit_plots.pdf](https://github.com/NattawatApi/Fitbit/files/9601108/Fitbit_plots.pdf)

  The result was saved as pdf file, and showed the summary of analysis in an effective and comprehensive way.
  
Act:
  In conclusion, it shows that every customers using smmart devices constantly exercise everyday during a record. Moreover, it displays that Tuesday is the most active day which customers take a longest distance and most step to exercise. On the other hand, Sunday is the least active day of the week. In addition, I also found that on the day customers take a longer distance of exercising, they will often take a lomger sleep time on the same day.
  As a result, most of customers use smart devices to analyze and monitor thier health by statistically recording their daily activity, for instance exercising and sleeping. Nevertheless, the result represents that some customer occasionally sleep less or more than enough which it's able to directly affect their health. Consequently, I relize that it would be better if there is a service or device being able to automatically suggest a proper length of sleep to the customers, along with automatic notification an appropriate bed time and wake-up time.
