# Bellabeat Case Study - Data Analysis and Insights for Product and Marketing Strategies
By: Hiep Nguyen
## Case Study Roadmap - Ask
### Guiding questions
● What is the problem you are trying to solve?
* Analyze smart device usage data to gain insight into how consumers use non-Bellabeat smart devices, so that it can be applied or implemented into their own smart devices

● How can your insights drive business decisions?
* The insights gained from analyzing non-Bellabeat smart device usage data can drive business decisions in several ways:
1. Product Optimization: By understanding how consumers are using competing devices, we can identify features, functionalities, and design elements that resonate with users. Implementing these insights into Bellabeat's product roadmap will allow us to optimize our offerings and better meet customer needs and preferences
2. Competitive Advantage: Applying the trends and best practices observed in the broader smart device market will help Bellabeat stay competitive and innovative. Leveraging these insights to enhance our products will enable us to differentiate our brand and appeal to a wider customer base.
3. Data-Driven Decision Making: A data-driven approach to product development, based on real user behavior and preferences, will lead to more informed and strategic business decisions. This will increase the likelihood of successful product launches and improved sales performance.
4. Targeted Marketing: The usage insights can also inform our marketing strategies by identifying the most effective messaging, channels, and value propositions to reach and engage our target customers. Tailoring our marketing efforts based on these insights will drive higher conversion rates and sales.
	 By implementing the trends and best practice observed in the non-Bellabeat smart device market, we can optimize our products, stay competitive, make data-driven decisions, and ultimately improve sales and market share for Bellabeat.

### Key tasks
1. Identify the business task
	- The key business task is to analyze smart device usage data to gain insights that can be applied to improve Bellabeat's own smart devices and marketing strategies.
	- The cofounder and Chief Creative Officer of Bellabeat, has asked the marketing analytics team to:
		- Analyze smart devices usage data to identify trends in how consumers use non-Bellabeat smart devices
		- Select one Bellabeat product and apply the insights gained from the analysis to make high-level recommendations for Bellabeat's marketing strategy
	- The goal is to uncover opportunities for growth by leveraging data-driven insights about consumer behavior and preferences in the broader smart device market.

2. Consider key stakeholders
	- Urška Sršen, co-founder and Chief Creative Officer of Bellabeat
		- Sršen is the primary stakeholder who has requested the analysis and will be the recipient of the final report and recommendations.
	- Sando Mur, mathematician, co-founder, and a key member of the Bellabeat executive
		- Mur will likely be involved in reviewing the findings and determining how to apply them to the company's marketing strategy as a key member of the executive team.

3. Bellabeat Product:
	The primary objective of this case study is to analyze fitness data collected from Bellabeat's smart devices, with the aim of identifying potential new growth opportunities for the company. Our analysis will concentrate on the Bellabeat app, which consolidates various health metrics for users, including activity levels, sleep patterns, stress management, menstrual cycle tracking, and mindfulness practices. By leveraging this comprehensive data, the Bellabeat app empowers users to gain deeper insights into their current habits and make more informed decisions to improve their overall well-being. Importantly, the app seamlessly integrates with Bellabeat's suite of smart wellness products, enabling a holistic experience.

### Deliverable
A clear statement of the business task:

Urška Sršen, co-founder and Chief Creative Officer of Bellabeat, has asked the marketing analytics team to analyze smart device usage data to identify trends in how consumers use non-Bellabeat products. The goal is to gain insights that can be applied to improve Bellabeat's own smart devices and marketing strategies. The team will select one Bellabeat product and make high-level recommendations for how the identified trends can inform the company's marketing approach. This analysis aims to uncover opportunities for growth by leveraging data-driven insights about consumer behavior and preferences in the broader smart device market.

## Case Study Roadmap - Prepare
### Guiding questions
● Where is your data stored?
	The dataset is stored in Kaggle and was made available through Mobius
● How is the data organized? Is it in long or wide format?
- We have access to 18 CSV files containing Fitbit data. Each CSV represents different quantitative metrics tracked by Fitbit devices.
- Every user has a unique identifier (ID) that allows their data to be linked across the different CSV files. 
- The data is structed in long format, meaning each row corresponds to a single time point per user. As a result, each user will have multiple rows of data, with one row per day and time point.
● Are there issues with bias or credibility in this data? Does your data ROCCC?
- There is some limitations in the dataset due to 
	- the small sample size (only 33 users)
	- lack of demographic data
- The analysis may suffer from sampling bias, as we cannot be certain if this limited sample is truly representative of the broader population. Another potential issue is that the dataset is not up-to-date, as it was collected over a relatively short 2-month period.
- Given these constraints around sample size, demographics, and data currency, our case study will take a more operational approach. Rather than making broad generalizations, we will focus on practical applications and insights that can be directly applied to Bellabeat's business. Our recommendations will be grounded in the available data, while acknowledging the limitations in terms of sample size and recency.
- By taking an operational approach, we can still extract meaningful insights from the data to inform Bellabeat's marketing strategy, while being transparent about the constraints of the dataset. The goal is to provide actionable recommendations based on the data at hand, while recognizing that further research with a larger, more representative sample would be needed to draw definitive conclusions.
● How are you addressing licensing, privacy, security, and accessibility?
	The dataset we are working with is open-source, meaning the owner has dedicated it to the public domain by waiving all copyrights and related rights to the fullest extent permitted by law. This allows anyone to freely copy, modify, distribute , and build upon the data, even for commercial purposes, without needing to obtain permission. The open-source licensing encourages collaboration and innovation by making the dataset universally accessible. As long as we adhere to the principles of attribution and non-endorsement, we can confidently utilize this open-source data for our analysis and share our findings.
● How did you verify the data’s integrity?
- Using:
``` MYSQL
SELECT Id, Time, COUNT(*) AS count
FROM TABLE_NAME
GROUP BY Id, Time
HAVING count > 1;
```
- can check for duplicates in any of the tables
- Using:
``` MYSQL
SELECT COUNT(DISTINCT Id) AS num_of_ids, COUNT(DISTINCT Time) as num_of_days 
FROM TABLE_NAME;
```
- can check for number of users and number of days in any of the tables

● How does it help you answer your question?
	It helps answer my question because it allows us to have a clean data to work with and analyze. Checking for the number of users in any given table will also help us determine if we should ignore certain csv files that had an even smaller sample size than the original 33 users.
● Are there any problems with the data?
	The sample size is too small and there were duplicates.

### Key tasks
1. Download data and store it appropriately.
	 I created a schema and created tables and loaded all the csv files into their respective tables.

2. Identify how it’s organized.

#Table

| Data Table Name                | File Type           | MYSQL Table Name          | Description                                                                                                                                                                                                                |
| ------------------------------ | ------------------- | ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dailyActivity_merged           | Microsoft Excel CSV | daily_activity            | Contains daily activity metrics including steps, distance, intensity levels, and calories burned for 33 users tracked over a 31-day period                                                                                 |
| dailyCalories_merged           | Microsoft Excel CSV | daily_calories            | Contains daily calorie intake records for 33 users over a 31-day period                                                                                                                                                    |
| dailyIntensities_merged        | Microsoft Excel CSV | daily_intensities         | Contains daily intensity metrics including, measured in minutes and distance, with intensity levels categorized into sedentary, lightly active, fairly active, and very active groups for 33 users over a 31-day period.   |
| dailySteps_merged              | Microsoft Excel CSV | daily_steps               | Contains daily steps count records for 33 users over a 31-day period                                                                                                                                                       |
| heartrate_seconds_merged       | Microsoft Excel CSV | heartrate_seconds         | Contains timestamped heart rate logs recorded for 7 specific users over a 31-day period                                                                                                                                    |
| hourlyCalories_merged          | Microsoft Excel CSV | hourly_calories           | Contains hourly calorie burn records for 33 users over a 31-day period                                                                                                                                                     |
| hourlyIntensities_merged       | Microsoft Excel CSV | hourly_intensities        | Contains hourly records of total and average intensity levels for 33 users over a 31-day period                                                                                                                            |
| hourlySteps_merged             | Microsoft Excel CSV | hourly_steps              | Contains hourly step count records for 33 users over a 31-day period                                                                                                                                                       |
| minuteCaloriesNarrow_merged    | Microsoft Excel CSV | minute_calories_narrow    | Contains minute-by-minute calorie burn records with each minute represented as a separate row for 33 users over a 31-day period                                                                                            |
| minuteCaloriesWide_merged      | Microsoft Excel CSV | minute_calories_wide      | Structured in a wide format, with each minute represented as a separate column, containing the calorie burn records for 33 users over a 31-day period                                                                      |
| minuteIntensitiesNarrow_merged | Microsoft Excel CSV | minute_intensities_narrow | Contains minute-by-minute intensity level records with each minute represented as a separate row for 33 users over a 31-day period                                                                                         |
| minuteIntensitiesWide_merged   | Microsoft Excel CSV | minute_intensities_wide   | Structured in a wide format, with each minute represented as a separate column, containing the intensity level records for 33 users over a 31-day period                                                                   |
| minuteMETsNarrow_merged        | Microsoft Excel CSV | minute_mets_narrow        | Contains minute-by-minute records of the metabolic equivalent (MET) values, which represents the ratio of energy expended during physical activity compared to the resting metabolic rate of 33 users over a 31-day period |
| minuteSleep_merged             | Microsoft Excel CSV | minute_sleep              | Contains minute-by-minute sleep logs for 24 users over a 32-day period, with the specific "value" column unspecified                                                                                                       |
| minuteStepsNarrow_merged       | Microsoft Excel CSV | minute_step_narrow        | Contains minute-by-minute records of the number of steps taken with each minute represented as a separate row for 33 users over a 31-day period                                                                            |
| minuteStepsWide_merged         | Microsoft Excel CSV | minute_steps_wide         | Structured in a wide format, with each minute represented as a separate column, containing the number of steps taken for 33 users over a 31-day period                                                                     |
| sleepDay_merged                | Microsoft Excel CSV | sleep_day                 | Contains daily sleep logs, tracking the total count of sleep sessions, total sleep minutes, and total time spent in bed for each day for 24 users over a 31-day period                                                     |
| weightLogInfo_merged           | Microsoft Excel CSV | weight_log_info           | Contains daily weight records in kilograms and pounds for 8 users over a 31-day period, including calculated BMI values, with 5 users reporting their weight manually and 3 users not reporting.                           |


3. Sort and filter the data.
	To thoroughly analyze the dataset despite its small sample size, I leveraged my Python and MySQL's capabilities by sorting, filtering, creating a schema, and creating tables for each data table in that schema. This allowed me to validate the attributes, observations, and relationships within and across the tables. Specifically, I counted the number of users represented in each table to confirm the overall sample size, and verified that the data covered a 31-day period, providing a sufficient timeframe for analysis. By taking these steps to explore and validate the data through the SQL tables, I could gain a comprehensive understanding of the dataset's structure, content, and integrity before proceeding with further analysis.

4. Determine the credibility of the data.
- There is some limitations in the dataset due to 
	- the small sample size (only 33 users)
	- lack of demographic data
- The analysis may suffer from sampling bias, as we cannot be certain if this limited sample is truly representative of the broader population. Another potential issue is that the dataset is not up-to-date, as it was collected over a relatively short 2-month period.
- Given these constraints around sample size, demographics, and data currency, our case study will take a more operational approach. Rather than making broad generalizations, we will focus on practical applications and insights that can be directly applied to Bellabeat's business. Our recommendations will be grounded in the available data, while acknowledging the limitations in terms of sample size and recency.
- By taking an operational approach, we can still extract meaningful insights from the data to inform Bellabeat's marketing strategy, while being transparent about the constraints of the dataset. The goal is to provide actionable recommendations based on the data at hand, while recognizing that further research with a larger, more representative sample would be needed to draw definitive conclusions.

### Deliverable
A description of all data sources used
(The Table in 2)

## Case Study Roadmap - Process
### Guiding questions
● What tools are you choosing and why?
	Leveraging the accessibility of Python and SQL, the substantial amount of data, and the capability to generate data visualizations, I will conduct my analysis and present the findings to stakeholders through visually compelling representations.

● Have you ensured your data’s integrity?
- Consolidated the 2 months of data into a single data frame for comprehensive analysis
- Checked for missing or incorrect data type from the csv files by creating queries for every table
- Removed any duplicates entries from the csv file by using python
- Documented the data cleaning and transformation process using Jupyter Notebook and Obsidian (mark -up language)

● What steps have you taken to ensure that your data is clean?
	I have made queries for every table to ensure that there are no duplicates, missing values, or incorrect data types

● How can you verify that your data is clean and ready to analyze?
	I checked the rows that the tables had before hand before removing the duplicates. I also checked the amount of rows of duplicates there were, that way when the removal process is finished, I can confirm that I remove all the duplicates necessary.

● Have you documented your cleaning process so you can review and share those results?
	Yes, everything has been documented.

### Key tasks
1. Check the data for errors.
	- minuteSleep_merged and sleepDay_merged had duplicate entries in their csv files.
	- weight_log_info dataset has a bunch of blank values in the "Fat" column

2. Choose your tools.
	- Python and SQL (MySQL)

3. Transform the data so you can work with it effectively.
	- minuteSleep_merged and sleepDay_merged had duplicate entries in their csv files. I could not import them using MySQL because of that. 
		- Therefore, I used python to identify and remove these duplicates so that they could be loaded into tables.
	- weight_log_info dataset has a bunch of blank values in the "Fat" column. 
		- I had to change them to NULL values so that they could be loaded into tables.
	- Time:
		- Every date column got changed from "m/d/yyyy" to "yyyy-mm-dd" as they became a DATE type in MySQL
		- Date columns with the included the time section, "hh:mm:ss" got transformed into a 24 hour time in SQL so that it could work nicely as it is auto done with the type DATETYPE.
			- (ex: "5/2/2016 11:59:59 PM" turned into "2016-05-02 23:59:59")
		- I did this for the sake of consistency in all the date tables.

4. Document the cleaning process.
	Originally, I started off by checking every data in excel to see if I could use pivot tables at first. This was working well for dailyActivity_merged, dailyCalories_merged, dailyIntensities_merged, dailySteps_merged. Then I got to heartrate_seconds_merged. When trying to import the csv file into excel, I got an error telling me the data set is too large for the Excel grid: 

[![[Pasted image 20240512045843.png]]](https://github.com/HiepNguyenDA/Bellabeat-Case-Study/blob/main/error.png?raw=true)
This is when I decided I was going to use Python and SQL to my data processing.

#### Creating Schema and Tables in MySQL
I started off by creating the schema: "fitbit" for my database.
```MySQL
CREATE SCHEMA fitbit;
```

I had then created a table creation query with the name for each of the csv files:
Table Creation Code:
``` MySQL: table_creation.sql
USE fitbit;

-- Daily Activity
CREATE TABLE IF NOT EXISTS daily_activity (
  Id BIGINT,
  ActivityDate DATE,
  TotalSteps BIGINT,
  TotalDistance DOUBLE,
  TrackerDistance DOUBLE,
  LoggedActivitiesDistance DOUBLE,
  VeryActiveDistance DOUBLE,
  ModeratelyActiveDistance DOUBLE,
  LightActiveDistance DOUBLE,
  SedentaryActiveDistance FLOAT,
  VeryActiveMinutes INT,
  FairlyActiveMinutes INT,
  LightlyActiveMinutes INT,
  SedentaryMinutes INT,
  Calories INT,
  PRIMARY KEY (Id, ActivityDate)
);

-- Daily Calories
CREATE TABLE IF NOT EXISTS daily_calories (
  Id BIGINT,
  ActivityDay DATE,
  Calories INT,
  PRIMARY KEY (Id, ActivityDay)
);

-- Daily Intensities
CREATE TABLE IF NOT EXISTS daily_intensities (
    Id BIGINT,
    ActivityDay DATE,
    SedentaryMinutes INT,
    LightlyActiveMinutes INT,
    FairlyActiveMinutes INT,
    VeryActiveMinutes INT,
    SedentaryActiveDistance FLOAT,
    LightActiveDistance DOUBLE,
    ModeratelyActiveDistance DOUBLE,
    VeryActiveDistance DOUBLE,
    PRIMARY KEY (Id , ActivityDay)
);

-- Daily Steps
CREATE TABLE IF NOT EXISTS daily_steps (
  Id BIGINT,
  ActivityDay DATE,
  StepTotal BIGINT,
  PRIMARY KEY (Id , ActivityDay)
);

-- Heartrate Seconds
-- Create the target table if it doesn't exist
CREATE TABLE IF NOT EXISTS heartrate_seconds (
  Id BIGINT,
  Time DATETIME,
  Value INT,
  PRIMARY KEY (Id, Time)
);

-- Hourly Calories
CREATE TABLE IF NOT EXISTS hourly_calories (
  Id BIGINT,
  ActivityHour DATETIME,
  Calories INT,
  PRIMARY KEY (Id, ActivityHour)
);

-- Hourly Intensities
CREATE TABLE IF NOT EXISTS hourly_intensities (
  Id BIGINT,
  ActivityHour DATETIME,
  TotalIntensity INT,
  AverageIntensity DOUBLE,
  PRIMARY KEY (Id, ActivityHour)
);

-- Hourly Steps
CREATE TABLE IF NOT EXISTS hourly_steps (
  Id BIGINT,
  ActivityHour DATETIME,
  StepTotal BIGINT,
  PRIMARY KEY (Id, ActivityHour)
);

-- Minutes Calories Narrow
CREATE TABLE IF NOT EXISTS minute_calories_narrow (
  Id BIGINT,
  ActivityMinute DATETIME,
  Calories DOUBLE,
  PRIMARY KEY (Id, ActivityMinute)
);

-- Minutes Calories Wide
CREATE TABLE IF NOT EXISTS minute_calories_wide (
    Id BIGINT,
    ActivityHour DATETIME,
    Calories00 DOUBLE,
    Calories01 DOUBLE,
    Calories02 DOUBLE,
    Calories03 DOUBLE,
    Calories04 DOUBLE,
    Calories05 DOUBLE,
    Calories06 DOUBLE,
    Calories07 DOUBLE,
    Calories08 DOUBLE,
    Calories09 DOUBLE,
    Calories10 DOUBLE,
    Calories11 DOUBLE,
    Calories12 DOUBLE,
    Calories13 DOUBLE,
    Calories14 DOUBLE,
    Calories15 DOUBLE,
    Calories16 DOUBLE,
    Calories17 DOUBLE,
    Calories18 DOUBLE,
    Calories19 DOUBLE,
    Calories20 DOUBLE,
    Calories21 DOUBLE,
    Calories22 DOUBLE,
    Calories23 DOUBLE,
    Calories24 DOUBLE,
    Calories25 DOUBLE,
    Calories26 DOUBLE,
    Calories27 DOUBLE,
    Calories28 DOUBLE,
    Calories29 DOUBLE,
    Calories30 DOUBLE,
    Calories31 DOUBLE,
    Calories32 DOUBLE,
    Calories33 DOUBLE,
    Calories34 DOUBLE,
    Calories35 DOUBLE,
    Calories36 DOUBLE,
    Calories37 DOUBLE,
    Calories38 DOUBLE,
    Calories39 DOUBLE,
    Calories40 DOUBLE,
    Calories41 DOUBLE,
    Calories42 DOUBLE,
    Calories43 DOUBLE,
    Calories44 DOUBLE,
    Calories45 DOUBLE,
    Calories46 DOUBLE,
    Calories47 DOUBLE,
    Calories48 DOUBLE,
    Calories49 DOUBLE,
    Calories50 DOUBLE,
    Calories51 DOUBLE,
    Calories52 DOUBLE,
    Calories53 DOUBLE,
    Calories54 DOUBLE,
    Calories55 DOUBLE,
    Calories56 DOUBLE,
    Calories57 DOUBLE,
    Calories58 DOUBLE,
    Calories59 DOUBLE,
    PRIMARY KEY (Id, ActivityHour)
);

-- Minutes Intensities Narrow
CREATE TABLE IF NOT EXISTS minute_intensities_narrow (
  Id BIGINT,
  ActivityMinute DATETIME,
  Intensity DOUBLE,
  PRIMARY KEY (Id, ActivityMinute)
);

-- Minutes Intensities Wide
CREATE TABLE IF NOT EXISTS minute_intensities_wide (
    Id BIGINT,
    ActivityHour DATETIME,
    Intensity00 INT,
    Intensity01 INT,
    Intensity02 INT,
    Intensity03 INT,
    Intensity04 INT,
    Intensity05 INT,
    Intensity06 INT,
    Intensity07 INT,
    Intensity08 INT,
    Intensity09 INT,
    Intensity10 INT,
    Intensity11 INT,
    Intensity12 INT,
    Intensity13 INT,
    Intensity14 INT,
    Intensity15 INT,
    Intensity16 INT,
    Intensity17 INT,
    Intensity18 INT,
    Intensity19 INT,
    Intensity20 INT,
    Intensity21 INT,
    Intensity22 INT,
    Intensity23 INT,
    Intensity24 INT,
    Intensity25 INT,
    Intensity26 INT,
    Intensity27 INT,
    Intensity28 INT,
    Intensity29 INT,
    Intensity30 INT,
    Intensity31 INT,
    Intensity32 INT,
    Intensity33 INT,
    Intensity34 INT,
    Intensity35 INT,
    Intensity36 INT,
    Intensity37 INT,
    Intensity38 INT,
    Intensity39 INT,
    Intensity40 INT,
    Intensity41 INT,
    Intensity42 INT,
    Intensity43 INT,
    Intensity44 INT,
    Intensity45 INT,
    Intensity46 INT,
    Intensity47 INT,
    Intensity48 INT,
    Intensity49 INT,
    Intensity50 INT,
    Intensity51 INT,
    Intensity52 INT,
    Intensity53 INT,
    Intensity54 INT,
    Intensity55 INT,
    Intensity56 INT,
    Intensity57 INT,
    Intensity58 INT,
    Intensity59 INT,
    PRIMARY KEY (Id, ActivityHour)
);

-- Minutes METs Narrow
CREATE TABLE IF NOT EXISTS minute_mets_narrow (
  Id BIGINT,
  ActivityMinute DATETIME,
  METs INT,
  PRIMARY KEY (Id, ActivityMinute)
);

-- Minute Sleep 
CREATE TABLE IF NOT EXISTS minute_sleep (
  Id BIGINT,
  date DATETIME,
  value INT,
  logId BIGINT,
  PRIMARY KEY (Id, date)
);

-- Minutes Steps Narrow
CREATE TABLE IF NOT EXISTS minute_step_narrow (
  Id BIGINT,
  ActivityMinute DATETIME,
  Steps INT,
  PRIMARY KEY (Id, ActivityMinute)
);

-- Minutes Steps Wide
CREATE TABLE IF NOT EXISTS minute_steps_wide (
    Id BIGINT,
    ActivityHour DATETIME,
    Steps00 INT,
    Steps01 INT,
    Steps02 INT,
    Steps03 INT,
    Steps04 INT,
    Steps05 INT,
    Steps06 INT,
    Steps07 INT,
    Steps08 INT,
    Steps09 INT,
    Steps10 INT,
    Steps11 INT,
    Steps12 INT,
    Steps13 INT,
    Steps14 INT,
    Steps15 INT,
    Steps16 INT,
    Steps17 INT,
    Steps18 INT,
    Steps19 INT,
    Steps20 INT,
    Steps21 INT,
    Steps22 INT,
    Steps23 INT,
    Steps24 INT,
    Steps25 INT,
    Steps26 INT,
    Steps27 INT,
    Steps28 INT,
    Steps29 INT,
    Steps30 INT,
    Steps31 INT,
    Steps32 INT,
    Steps33 INT,
    Steps34 INT,
    Steps35 INT,
    Steps36 INT,
    Steps37 INT,
    Steps38 INT,
    Steps39 INT,
    Steps40 INT,
    Steps41 INT,
    Steps42 INT,
    Steps43 INT,
    Steps44 INT,
    Steps45 INT,
    Steps46 INT,
    Steps47 INT,
    Steps48 INT,
    Steps49 INT,
    Steps50 INT,
    Steps51 INT,
    Steps52 INT,
    Steps53 INT,
    Steps54 INT,
    Steps55 INT,
    Steps56 INT,
    Steps57 INT,
    Steps58 INT,
    Steps59 INT,
    PRIMARY KEY (Id, ActivityHour)
);

-- Sleep Day 
CREATE TABLE IF NOT EXISTS sleep_day (
  Id BIGINT,
  SleepDay DATETIME,
  TotalSleepRecords INT,
  TotalMinutesAsleep INT,
  TotalTimeInBed INT,
  PRIMARY KEY (Id, SleepDay)
);

-- Weight Log Info
CREATE TABLE IF NOT EXISTS weight_log_info (
    Id BIGINT,
    Date DATETIME,
    WeightKg DOUBLE,
    WeightPounds DOUBLE,
    Fat INT NULL,
    BMI DOUBLE,
    IsManualReport TINYINT,
    LogId BIGINT
);
```

#### Loading CSV files into Tables and Removing Duplicates
After all the table creation, I began to load the data in from each csv files into the tables.

Table Load Code:
``` MySQL: table_load.sql

-- Daily Activity
LOAD DATA INFILE 'dailyActivity_merged.csv'
INTO TABLE daily_activity
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityDate,TotalSteps,TotalDistance,TrackerDistance,LoggedActivitiesDistance,VeryActiveDistance,ModeratelyActiveDistance,LightActiveDistance,SedentaryActiveDistance,VeryActiveMinutes,FairlyActiveMinutes,LightlyActiveMinutes,SedentaryMinutes,Calories)
SET ActivityDate = STR_TO_DATE(@var_ActivityDate, '%m/%d/%Y');

-- Daily Calories
LOAD DATA INFILE 'dailyCalories_merged.csv'
INTO TABLE daily_calories
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityDay,Calories)
SET ActivityDay = STR_TO_DATE(@var_ActivityDay, '%m/%d/%Y');

-- Daily Intensities
LOAD DATA INFILE 'dailyIntensities_merged.csv'
INTO TABLE daily_intensities
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityDay,SedentaryMinutes,LightlyActiveMinutes,FairlyActiveMinutes,VeryActiveMinutes,SedentaryActiveDistance,LightActiveDistance,ModeratelyActiveDistance,VeryActiveDistance)
SET ActivityDay = STR_TO_DATE(@var_ActivityDay, '%m/%d/%Y');

-- Daily Steps
LOAD DATA INFILE 'dailySteps_merged.csv'
INTO TABLE daily_steps
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityDay,StepTotal)
SET ActivityDay = STR_TO_DATE(@var_ActivityDay, '%m/%d/%Y');

-- Heartrate Seconds
LOAD DATA INFILE 'heartrate_seconds_merged.csv'
INTO TABLE heartrate_seconds
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_Time,Value)
SET Time = STR_TO_DATE(@var_Time, '%m/%d/%Y %h:%i:%s %p');

-- Hourly Calories
LOAD DATA INFILE 'hourlyCalories_merged.csv'
INTO TABLE hourly_calories
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityHour,Calories)
SET ActivityHour = STR_TO_DATE(@var_ActivityHour, '%m/%d/%Y %h:%i:%s %p');

-- Hourly Intensities
LOAD DATA INFILE 'hourlyIntensities_merged.csv'
INTO TABLE hourly_intensities
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityHour,TotalIntensity,AverageIntensity)
SET ActivityHour = STR_TO_DATE(@var_ActivityHour, '%m/%d/%Y %h:%i:%s %p');

-- Hourly Steps
LOAD DATA INFILE 'hourlySteps_merged.csv'
INTO TABLE hourly_steps
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityHour,StepTotal)
SET ActivityHour = STR_TO_DATE(@var_ActivityHour, '%m/%d/%Y %h:%i:%s %p');

-- Minutes Calories Narrow
LOAD DATA INFILE 'minuteCaloriesNarrow_merged.csv'
INTO TABLE minute_calories_narrow
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityMinute,Calories)
SET ActivityMinute = STR_TO_DATE(@var_ActivityMinute, '%m/%d/%Y %h:%i:%s %p');

-- Minutes Calories Narrow
LOAD DATA INFILE 'minuteCaloriesWide_merged.csv'
INTO TABLE minute_calories_wide
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityHour,Calories00,Calories01,Calories02,Calories03,Calories04,Calories05,Calories06,Calories07,Calories08,Calories09,Calories10,Calories11,Calories12,Calories13,Calories14,Calories15,Calories16,Calories17,Calories18,Calories19,Calories20,Calories21,Calories22,Calories23,Calories24,Calories25,Calories26,Calories27,Calories28,Calories29,Calories30,Calories31,Calories32,Calories33,Calories34,Calories35,Calories36,Calories37,Calories38,Calories39,Calories40,Calories41,Calories42,Calories43,Calories44,Calories45,Calories46,Calories47,Calories48,Calories49,Calories50,Calories51,Calories52,Calories53,Calories54,Calories55,Calories56,Calories57,Calories58,Calories59)
SET ActivityHour = STR_TO_DATE(@var_ActivityHour, '%m/%d/%Y %h:%i:%s %p');

-- Minutes Intensities Narrow
LOAD DATA INFILE 'minuteIntensitiesNarrow_merged.csv'
INTO TABLE minute_intensities_narrow
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityMinute,Intensity)
SET ActivityMinute = STR_TO_DATE(@var_ActivityMinute, '%m/%d/%Y %h:%i:%s %p');

-- Minutes Intensities Wide
LOAD DATA INFILE 'minuteIntensitiesWide_merged.csv'
INTO TABLE minute_intensities_wide
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityHour,Intensity00,Intensity01,Intensity02,Intensity03,Intensity04,Intensity05,Intensity06,Intensity07,Intensity08,Intensity09,Intensity10,Intensity11,Intensity12,Intensity13,Intensity14,Intensity15,Intensity16,Intensity17,Intensity18,Intensity19,Intensity20,Intensity21,Intensity22,Intensity23,Intensity24,Intensity25,Intensity26,Intensity27,Intensity28,Intensity29,Intensity30,Intensity31,Intensity32,Intensity33,Intensity34,Intensity35,Intensity36,Intensity37,Intensity38,Intensity39,Intensity40,Intensity41,Intensity42,Intensity43,Intensity44,Intensity45,Intensity46,Intensity47,Intensity48,Intensity49,Intensity50,Intensity51,Intensity52,Intensity53,Intensity54,Intensity55,Intensity56,Intensity57,Intensity58,Intensity59)
SET ActivityHour = STR_TO_DATE(@var_ActivityHour, '%m/%d/%Y %h:%i:%s %p');

-- Minutes METs Narrow
LOAD DATA INFILE 'minuteMETsNarrow_merged.csv'
INTO TABLE minute_mets_narrow
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityMinute,METs)
SET ActivityMinute = STR_TO_DATE(@var_ActivityMinute, '%m/%d/%Y %h:%i:%s %p');

-- Minute Sleep
LOAD DATA INFILE 'minuteSleep_merged.csv'
INTO TABLE minute_sleep
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_date, value, logId)
SET date = STR_TO_DATE(@var_date, '%m/%d/%Y %h:%i:%s %p');

-- Minute Steps Narrow
LOAD DATA INFILE 'minuteStepsNarrow_merged.csv'
INTO TABLE minute_step_narrow
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityMinute,Steps)
SET ActivityMinute = STR_TO_DATE(@var_ActivityMinute, '%m/%d/%Y %h:%i:%s %p');

-- Minute Steps Wide
LOAD DATA INFILE 'minuteStepsWide_merged.csv'
INTO TABLE minute_steps_wide
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_ActivityHour,Steps00,Steps01,Steps02,Steps03,Steps04,Steps05,Steps06,Steps07,Steps08,Steps09,Steps10,Steps11,Steps12,Steps13,Steps14,Steps15,Steps16,Steps17,Steps18,Steps19,Steps20,Steps21,Steps22,Steps23,Steps24,Steps25,Steps26,Steps27,Steps28,Steps29,Steps30,Steps31,Steps32,Steps33,Steps34,Steps35,Steps36,Steps37,Steps38,Steps39,Steps40,Steps41,Steps42,Steps43,Steps44,Steps45,Steps46,Steps47,Steps48,Steps49,Steps50,Steps51,Steps52,Steps53,Steps54,Steps55,Steps56,Steps57,Steps58,Steps59)
SET ActivityHour = STR_TO_DATE(@var_ActivityHour, '%m/%d/%Y %h:%i:%s %p');

-- Sleep Day
LOAD DATA INFILE 'sleepDay_merged.csv'
INTO TABLE sleep_day
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(Id,@var_SleepDay,TotalSleepRecords,TotalMinutesAsleep,TotalTimeInBed)
SET SleepDay = STR_TO_DATE(@var_SleepDay, '%m/%d/%Y %h:%i:%s %p');

-- Weight Log Info
LOAD DATA INFILE 'weightLogInfo_merged.csv'
INTO TABLE weight_log_info
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(id, @var_Date, WeightKg, WeightPounds, @var_Fat, BMI, @var_IsManualReport, LogId)
SET Date = STR_TO_DATE(@var_Date, '%m/%d/%Y %r'),
    Fat = NULLIF(@var_Fat, ''),
    IsManualReport = CASE WHEN @var_IsManualReport = 'True' THEN 1 ELSE 0 END;

```

Issues that arisen:
As I was loading the data though, I was getting errors in the minute_sleep and sleep_day tables. I was getting the error:
```MySQL
Error Code: 1062. Duplicate entry '4702921684-2016-05-06 21:10:00' for key 'minute_sleep.PRIMARY'

-- and

Error Code: 1062. Duplicate entry '4388161847-2016-05-05 00:00:00' for key 'sleep_day.PRIMARY'
```

This means that there were duplicates in the csv files when attempting to load in them into the tables.

I cleaned the csv file using Python.
Python Cleaning Code:
```Python 3.0
# REMOVING Duplicates from minuteSleep_merged.csv
import pandas as pd

df = pd.read_csv(r'C:\ProgramData\MySQL\MySQL Server 8.0\Data\fitbit\minuteSleep_merged.csv')

print(df)


duplicates = df[df.duplicated()]
print("Duplicated Rows:")
print(duplicates)
print("Number of Duplicates: ", len(duplicates))


                Id                  date  value        logId
0       1503960366  4/12/2016 2:47:30 AM      3  11380564589
1       1503960366  4/12/2016 2:48:30 AM      2  11380564589
2       1503960366  4/12/2016 2:49:30 AM      1  11380564589
3       1503960366  4/12/2016 2:50:30 AM      1  11380564589
4       1503960366  4/12/2016 2:51:30 AM      1  11380564589
...            ...                   ...    ...          ...
188516  8792009665   5/4/2016 9:59:00 AM      1  11552534115
188517  8792009665  5/4/2016 10:00:00 AM      1  11552534115
188518  8792009665  5/4/2016 10:01:00 AM      1  11552534115
188519  8792009665  5/4/2016 10:02:00 AM      1  11552534115
188520  8792009665  5/4/2016 10:03:00 AM      1  11552534115

[188521 rows x 4 columns]
Duplicated Rows:

                Id                 date  value        logId
99770   4702921684  5/6/2016 9:10:00 PM      3  11573168523
99771   4702921684  5/6/2016 9:11:00 PM      3  11573168523
99772   4702921684  5/6/2016 9:12:00 PM      2  11573168523
99773   4702921684  5/6/2016 9:13:00 PM      1  11573168523
99774   4702921684  5/6/2016 9:14:00 PM      1  11573168523
...            ...                  ...    ...          ...
100308  4702921684  5/7/2016 6:08:00 AM      2  11573168523
100309  4702921684  5/7/2016 6:09:00 AM      1  11573168523
100310  4702921684  5/7/2016 6:10:00 AM      2  11573168523
100311  4702921684  5/7/2016 6:11:00 AM      1  11573168523
100312  4702921684  5/7/2016 6:12:00 AM      1  11573168523

[543 rows x 4 columns]
Number of Duplicates:  543

# Confirming 188521 rows, 543 duplicates, so 188521-543 = 187978 which is how many rows we end up with after removing dupes
df = df.drop_duplicates()
print(df)
                Id                  date  value        logId
0       1503960366  4/12/2016 2:47:30 AM      3  11380564589
1       1503960366  4/12/2016 2:48:30 AM      2  11380564589
2       1503960366  4/12/2016 2:49:30 AM      1  11380564589
3       1503960366  4/12/2016 2:50:30 AM      1  11380564589
4       1503960366  4/12/2016 2:51:30 AM      1  11380564589
...            ...                   ...    ...          ...
188516  8792009665   5/4/2016 9:59:00 AM      1  11552534115
188517  8792009665  5/4/2016 10:00:00 AM      1  11552534115
188518  8792009665  5/4/2016 10:01:00 AM      1  11552534115
188519  8792009665  5/4/2016 10:02:00 AM      1  11552534115
188520  8792009665  5/4/2016 10:03:00 AM      1  11552534115

[187978 rows x 4 columns]

# Saving result to csv file named: "minuteSleep_merged_cleaned.csv"

folder_path = r'C:\ProgramData\MySQL\MySQL Server 8.0\Data\fitbit'
file_name = 'minuteSleep_merged_cleaned.csv'
file_path = folder_path + '\\' + file_name

df.to_csv(file_path, index=False)

# REMOVING Duplicates from sleepDay_merged.csv
df = pd.read_csv(r'C:\ProgramData\MySQL\MySQL Server 8.0\Data\fitbit\sleepDay_merged.csv')

print(df)


duplicates = df[df.duplicated()]
print("Duplicated Rows:")
print(duplicates)
print("Number of Duplicates: ", len(duplicates))

0    1503960366  4/12/2016 12:00:00 AM                  1                 327   
1    1503960366  4/13/2016 12:00:00 AM                  2                 384   
2    1503960366  4/15/2016 12:00:00 AM                  1                 412   
3    1503960366  4/16/2016 12:00:00 AM                  2                 340   
4    1503960366  4/17/2016 12:00:00 AM                  1                 700   
..          ...                    ...                ...                 ...   
408  8792009665  4/30/2016 12:00:00 AM                  1                 343   
409  8792009665   5/1/2016 12:00:00 AM                  1                 503   
410  8792009665   5/2/2016 12:00:00 AM                  1                 415   
411  8792009665   5/3/2016 12:00:00 AM                  1                 516   
412  8792009665   5/4/2016 12:00:00 AM                  1                 439   

     TotalTimeInBed  
0               346  
1               407  
2               442  
3               367  
4               712  
..              ...  
408             360  
409             527  
410             423  
411             545  
412             463  

[413 rows x 5 columns]
Duplicated Rows:
             Id               SleepDay  TotalSleepRecords  TotalMinutesAsleep  \
161  4388161847   5/5/2016 12:00:00 AM                  1                 471   
223  4702921684   5/7/2016 12:00:00 AM                  1                 520   
380  8378563200  4/25/2016 12:00:00 AM                  1                 388   

     TotalTimeInBed  
161             495  
223             543  
380             402  
Number of Duplicates:  3

# Confirming 413 rows, 3 duplicates, so 413-3 = 410 which is how many rows we end up with after removing dupes
df = df.drop_duplicates()
print(df)

             Id               SleepDay  TotalSleepRecords  TotalMinutesAsleep  \
0    1503960366  4/12/2016 12:00:00 AM                  1                 327   
1    1503960366  4/13/2016 12:00:00 AM                  2                 384   
2    1503960366  4/15/2016 12:00:00 AM                  1                 412   
3    1503960366  4/16/2016 12:00:00 AM                  2                 340   
4    1503960366  4/17/2016 12:00:00 AM                  1                 700   
..          ...                    ...                ...                 ...   
408  8792009665  4/30/2016 12:00:00 AM                  1                 343   
409  8792009665   5/1/2016 12:00:00 AM                  1                 503   
410  8792009665   5/2/2016 12:00:00 AM                  1                 415   
411  8792009665   5/3/2016 12:00:00 AM                  1                 516   
412  8792009665   5/4/2016 12:00:00 AM                  1                 439   

     TotalTimeInBed  
0               346  
1               407  
2               442  
3               367  
4               712  
..              ...  
408             360  
409             527  
410             423  
411             545  
412             463  

[410 rows x 5 columns]

# Saving result to csv named: "sleepDay_merged_cleaned.csv"

folder_path = r'C:\ProgramData\MySQL\MySQL Server 8.0\Data\fitbit'
file_name = 'sleepDay_merged_cleaned.csv'
file_path = folder_path + '\\' + file_name

df.to_csv(file_path, index=False)
```

Now that the data has been cleaned, I change the respective loading data code in MySQL:
```MySQL table_load.sql
-- Minute Sleep (removed dupes in python, so that I could use the PK)
LOAD DATA INFILE 'minuteSleep_merged_cleaned.csv'

-- and

-- Sleep Day (removed dupes in python, so that I could use the PK)
LOAD DATA INFILE 'sleepDay_merged_cleaned.csv'
```

This fixed the duplicates in our csv files because we are using the "id" and "date" columns as primary keys for every table.

#### Exploring and Summarizing Data

I created individual queries for every single table that checks the amount of unique ids and distinct amount of days.
As an example, for the daily_activity table, I had a query called daily_activity_query which contained:
```MySQL daily_activity_query
SELECT * FROM fitbit.daily_activity; -- Check Table Contents
SELECT COUNT(*) FROM fitbit.daily_activity; -- Count Rows of Table
SELECT COUNT(DISTINCT Id) AS num_of_ids, COUNT(DISTINCT ActivityDate) as num_of_days
FROM fitbit.daily_activity; -- Returns number of ids and number of days

SELECT Id, ActivityDate, COUNT(*) AS count -- Checks for duplicates (safety measure)
FROM fitbit.daily_activity
GROUP BY Id, ActivityDate
HAVING count > 1;
```

What I really valued to check was the amount of users in each table and how long the time period was.

I've listed them in the description of each table in the Preparation stage. Here is what I found out:

| MYSQL Table Name          | Description                                                                                                                                                                                                              |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| daily_activity            | Contains daily activity metrics including steps, distance, intensity levels, and calories burned for 33 users tracked over a 31-day period                                                                               |
| daily_calories            | Contains daily calorie intake records for 33 users over a 31-day period                                                                                                                                                  |
| daily_intensities         | Contains daily intensity metrics including, measured in minutes and distance, with intensity levels categorized into sedentary, lightly active, fairly active, and very active groups for 33 users over a 31-day period. |
| daily_steps               | Contains daily steps count records for 33 users over a 31-day period                                                                                                                                                     |
| heartrate_seconds         | Contains timestamped heart rate logs recorded for 7 specific users over a 31-day period                                                                                                                                  |
| hourly_calories           | Contains hourly calorie burn records for 33 users over a 31-day period                                                                                                                                                   |
| hourly_intensities        | Contains hourly records of total and average intensity levels for 33 users over a 31-day period                                                                                                                          |
| hourly_steps              | Contains hourly step count records for 33 users over a 31-day period                                                                                                                                                     |
| minute_calories_narrow    | Contains minute-by-minute calorie burn records with each minute represented as a separate row for 33 users over a 31-day period                                                                                          |
| minute_calories_wide      | Structured in a wide format, with each minute represented as a separate column, containing the calorie burn records for 33 users over a 31-day period                                                                    |
| minute_intensities_narrow | Contains minute-by-minute intensity level records with each minute represented as a separate row for 33 users over a 31-day period                                                                                       |
| minute_intensities_wide   | Structured in a wide format, with each minute represented as a separate column, containing the intensity level records for 33 users over a 31-day period                                                                 |
| minute_mets_narrow        | Contains minute-by-minute records of the metabolic equivalent (MET) values, which represents the ratio of energy expended during physical activity compared to the resting metabolic rate                                |
| minute_sleep              | Contains minute-by-minute sleep logs for 24 users over a 32-day period, with the specific "value" column unspecified                                                                                                     |
| minute_step_narrow        | Contains minute-by-minute records of the number of steps taken with each minute represented as a separate row for 33 users over a 31-day period                                                                          |
| minute_steps_wide         | Structured in a wide format, with each minute represented as a separate column, containing the number of steps taken for 33 users over a 31-day period                                                                   |
| sleep_day                 | Contains daily sleep logs, tracking the total count of sleep sessions, total sleep minutes, and total time spent in bed for each day for 24 users over a 31-day period                                                   |
| weight_log_info           | Contains daily weight records in kilograms and pounds for 8 users over a 31-day period, including calculated BMI values, with 5 users reporting their weight manually and 3 users not reporting.                         |

I will only use the ones with sufficient participants in the analysis because the smaller ones (8 users in weight_log_info, and 7 users heartrate_seconds) do not contain a big enough sample size to draw any meaningful conclusions. Therefore, I will use:
- daily_activity (33 users)
- hourly_calories (33 users)
- hourly_intensities (33 users)
- sleep_day (24 users)
	- Although 30 is the minimal sample size, we will still analyze sleep_day for practicing purpose

We will start by looking at the 

```MySQL
SELECT * FROM fitbit.daily_activity
limit 10;
```

| Id         | ActivityDate | TotalSteps | TotalDistance    | TrackerDistance  | LoggedActivitiesDistance | VeryActiveDistance | ModeratelyActiveDistance | LightActiveDistance | SedentaryActiveDistance | VeryActiveMinutes | FairlyActiveMinutes | LightlyActiveMinutes | SedentaryMinutes | Calories |
|------------|--------------|------------|------------------|------------------|--------------------------|--------------------|--------------------------|---------------------|-------------------------|-------------------|---------------------|----------------------|------------------|----------|
| 1503960366 | 2016-04-12   | 13162      | 8.5              | 8.5              | 0                        | 1.87999999523163   | 0.550000011920929        | 6.05999994277954    | 0                       | 25                | 13                  | 328                  | 728              | 1985     |
| 1503960366 | 2016-04-13   | 10735      | 6.96999979019165 | 6.96999979019165 | 0                        | 1.57000005245209   | 0.689999997615814        | 4.71000003814697    | 0                       | 21                | 19                  | 217                  | 776              | 1797     |
| 1503960366 | 2016-04-14   | 10460      | 6.73999977111816 | 6.73999977111816 | 0                        | 2.44000005722046   | 0.400000005960464        | 3.91000008583069    | 0                       | 30                | 11                  | 181                  | 1218             | 1776     |
| 1503960366 | 2016-04-15   | 9762       | 6.28000020980835 | 6.28000020980835 | 0                        | 2.14000010490417   | 1.25999999046326         | 2.82999992370605    | 0                       | 29                | 34                  | 209                  | 726              | 1745     |
| 1503960366 | 2016-04-16   | 12669      | 8.15999984741211 | 8.15999984741211 | 0                        | 2.71000003814697   | 0.409999996423721        | 5.03999996185303    | 0                       | 36                | 10                  | 221                  | 773              | 1863     |
| 1503960366 | 2016-04-17   | 9705       | 6.48000001907349 | 6.48000001907349 | 0                        | 3.19000005722046   | 0.779999971389771        | 2.50999999046326    | 0                       | 38                | 20                  | 164                  | 539              | 1728     |
| 1503960366 | 2016-04-18   | 13019      | 8.59000015258789 | 8.59000015258789 | 0                        | 3.25               | 0.639999985694885        | 4.71000003814697    | 0                       | 42                | 16                  | 233                  | 1149             | 1921     |
| 1503960366 | 2016-04-19   | 15506      | 9.88000011444092 | 9.88000011444092 | 0                        | 3.52999997138977   | 1.32000005245209         | 5.03000020980835    | 0                       | 50                | 31                  | 264                  | 775              | 2035     |
| 1503960366 | 2016-04-20   | 10544      | 6.67999982833862 | 6.67999982833862 | 0                        | 1.96000003814697   | 0.479999989271164        | 4.23999977111816    | 0                       | 28                | 12                  | 205                  | 818              | 1786     |
| 1503960366 | 2016-04-21   | 9819       | 6.34000015258789 | 6.34000015258789 | 0                        | 1.3400000333786    | 0.349999994039536        | 4.65000009536743    | 0                       | 19                | 8                   | 211                  | 838              | 1775     |

```MySQL
SELECT * FROM fitbit.sleep_day
limit 10;
```

| Id         | SleepDay              | TotalSleepRecords | TotalMinutesAsleep | TotalTimeInBed |
|------------|-----------------------|-------------------|--------------------|----------------|
| 1503960366 | "2016-04-12 00:00:00" | 1                 | 327                | 346            |
| 1503960366 | "2016-04-13 00:00:00" | 2                 | 384                | 407            |
| 1503960366 | "2016-04-15 00:00:00" | 1                 | 412                | 442            |
| 1503960366 | "2016-04-16 00:00:00" | 2                 | 340                | 367            |
| 1503960366 | "2016-04-17 00:00:00" | 1                 | 700                | 712            |
| 1503960366 | "2016-04-19 00:00:00" | 1                 | 304                | 320            |
| 1503960366 | "2016-04-20 00:00:00" | 1                 | 360                | 377            |
| 1503960366 | "2016-04-21 00:00:00" | 1                 | 325                | 364            |
| 1503960366 | "2016-04-23 00:00:00" | 1                 | 361                | 384            |
| 1503960366 | "2016-04-24 00:00:00" | 1                 | 430                | 449            |

I will focus on cleaning the time format for both daily_activity and daily_sleep since I want to eventually inner join both data tables together.

I use the code:
```MySQL
ALTER TABLE fitbit.sleep_day
MODIFY COLUMN SleepDay DATE;
```
to remove the 00:00:00 from dates in the SleepDay column.

Now to check if it worked:
```MySQL
SELECT * FROM fitbit.sleep_day
limit 10;
```

| Id         | SleepDay   | TotalSleepRecords | TotalMinutesAsleep | TotalTimeInBed |
|------------|------------|-------------------|--------------------|----------------|
| 1503960366 | 2016-04-12 | 1                 | 327                | 346            |
| 1503960366 | 2016-04-13 | 2                 | 384                | 407            |
| 1503960366 | 2016-04-15 | 1                 | 412                | 442            |
| 1503960366 | 2016-04-16 | 2                 | 340                | 367            |
| 1503960366 | 2016-04-17 | 1                 | 700                | 712            |
| 1503960366 | 2016-04-19 | 1                 | 304                | 320            |
| 1503960366 | 2016-04-20 | 1                 | 360                | 377            |
| 1503960366 | 2016-04-21 | 1                 | 325                | 364            |
| 1503960366 | 2016-04-23 | 1                 | 361                | 384            |
| 1503960366 | 2016-04-24 | 1                 | 430                | 449            |

To combine both daily_activity and sleep_day, I use the code:
```MySQL
SELECT * FROM fitbit.daily_activity da INNER JOIN fitbit.sleep_day sd on (da.ActivityDate = sd.SleepDay and da.id = sd.id)
limit 10;
```

| Id         | ActivityDate | TotalSteps | TotalDistance    | TrackerDistance  | LoggedActivitiesDistance | VeryActiveDistance | ModeratelyActiveDistance | LightActiveDistance | SedentaryActiveDistance | VeryActiveMinutes | FairlyActiveMinutes | LightlyActiveMinutes | SedentaryMinutes | Calories | Id         | SleepDay   | TotalSleepRecords | TotalMinutesAsleep | TotalTimeInBed |
|------------|--------------|------------|------------------|------------------|--------------------------|--------------------|--------------------------|---------------------|-------------------------|-------------------|---------------------|----------------------|------------------|----------|------------|------------|-------------------|--------------------|----------------|
| 1503960366 | 2016-04-12   | 13162      | 8.5              | 8.5              | 0                        | 1.87999999523163   | 0.550000011920929        | 6.05999994277954    | 0                       | 25                | 13                  | 328                  | 728              | 1985     | 1503960366 | 2016-04-12 | 1                 | 327                | 346            |
| 1503960366 | 2016-04-13   | 10735      | 6.96999979019165 | 6.96999979019165 | 0                        | 1.57000005245209   | 0.689999997615814        | 4.71000003814697    | 0                       | 21                | 19                  | 217                  | 776              | 1797     | 1503960366 | 2016-04-13 | 2                 | 384                | 407            |
| 1503960366 | 2016-04-15   | 9762       | 6.28000020980835 | 6.28000020980835 | 0                        | 2.14000010490417   | 1.25999999046326         | 2.82999992370605    | 0                       | 29                | 34                  | 209                  | 726              | 1745     | 1503960366 | 2016-04-15 | 1                 | 412                | 442            |
| 1503960366 | 2016-04-16   | 12669      | 8.15999984741211 | 8.15999984741211 | 0                        | 2.71000003814697   | 0.409999996423721        | 5.03999996185303    | 0                       | 36                | 10                  | 221                  | 773              | 1863     | 1503960366 | 2016-04-16 | 2                 | 340                | 367            |
| 1503960366 | 2016-04-17   | 9705       | 6.48000001907349 | 6.48000001907349 | 0                        | 3.19000005722046   | 0.779999971389771        | 2.50999999046326    | 0                       | 38                | 20                  | 164                  | 539              | 1728     | 1503960366 | 2016-04-17 | 1                 | 700                | 712            |
| 1503960366 | 2016-04-19   | 15506      | 9.88000011444092 | 9.88000011444092 | 0                        | 3.52999997138977   | 1.32000005245209         | 5.03000020980835    | 0                       | 50                | 31                  | 264                  | 775              | 2035     | 1503960366 | 2016-04-19 | 1                 | 304                | 320            |
| 1503960366 | 2016-04-20   | 10544      | 6.67999982833862 | 6.67999982833862 | 0                        | 1.96000003814697   | 0.479999989271164        | 4.23999977111816    | 0                       | 28                | 12                  | 205                  | 818              | 1786     | 1503960366 | 2016-04-20 | 1                 | 360                | 377            |
| 1503960366 | 2016-04-21   | 9819       | 6.34000015258789 | 6.34000015258789 | 0                        | 1.3400000333786    | 0.349999994039536        | 4.65000009536743    | 0                       | 19                | 8                   | 211                  | 838              | 1775     | 1503960366 | 2016-04-21 | 1                 | 325                | 364            |
| 1503960366 | 2016-04-23   | 14371      | 9.03999996185303 | 9.03999996185303 | 0                        | 2.80999994277954   | 0.870000004768372        | 5.3600001335144     | 0                       | 41                | 21                  | 262                  | 732              | 1949     | 1503960366 | 2016-04-23 | 1                 | 361                | 384            |
| 1503960366 | 2016-04-24   | 10039      | 6.40999984741211 | 6.40999984741211 | 0                        | 2.92000007629395   | 0.209999993443489        | 3.27999997138977    | 0                       | 39                | 5                   | 238                  | 709              | 1788     | 1503960366 | 2016-04-24 | 1                 | 430                | 449            |


Now that we every table is loaded and cleaned and we got to know more about our data structures, it is time to analyze.


### Deliverable
Documentation of any cleaning or manipulation of data
	See above for all the documentation of cleaning and manipulations of the data

## Case Study Roadmap - Analyze
### Guiding questions
● How should you organize your data to perform analysis on it?
- See which columns are organized across all tables to see which is the most common
- See if the date columns are the same type across all tables
● Has your data been properly formatted?
	Yes, I reformatted the date columns for the tables I was looking at
● What surprises did you discover in the data?
	The significant portion (51.5%) of users classified as "Physically Inactive" and the lack of a clear linear relationship between sleep duration and activity levels were surprising discoveries.
● What trends or relationships did you find in the data?
	 Key trends and relationships found include the strong positive correlation between total sleep time and time in bed, the mostly linear relationship between steps and calorie expenditure (with some outlier influence), and the concentration of users within specific ranges of sleep duration and activity levels.
● How will these insights help answer your business questions?
	These insights provide a better understanding of Bellabeat's user base, their diverse activity levels, sleep patterns, and the relationships between tracked metrics, which can inform product development, marketing strategies, and user engagement initiatives to better cater to different user segments and promote healthy behaviors.

### Key tasks
1. Aggregate your data so it’s useful and accessible.
	Done when joining the daily_activity and sleep_day tables

2.  Organize and format your data.
	Every table has an id table
	```MySQL
-- We found that Id was a common column, let's make sure that it is in every table we have
SELECT
 table_name,
 SUM(CASE
     WHEN column_name = "Id" THEN 1
   ELSE
   0
 END
   ) AS has_id_column
FROM
INFORMATION_SCHEMA.COLUMNS
WHERE
	table_schema = 'fitbit'
GROUP BY
 1
ORDER BY
 1 ASC;
	```

| TABLE_NAME                | has_id_column |
|---------------------------|---------------|
| daily_activity            | 1             |
| daily_calories            | 1             |
| daily_intensities         | 1             |
| daily_steps               | 1             |
| heartrate_seconds         | 1             |
| hourly_calories           | 1             |
| hourly_intensities        | 1             |
| hourly_steps              | 1             |
| minute_calories_narrow    | 1             |
| minute_calories_wide      | 1             |
| minute_intensities_narrow | 1             |
| minute_intensities_wide   | 1             |
| minute_mets_narrow        | 1             |
| minute_sleep              | 1             |
| minute_step_narrow        | 1             |
| minute_steps_wide         | 1             |
| sleep_day                 | 1             |
| weight_log_info           | 1             |

This is important as it shows that id is definitely a primary key.

```MySQL
-- This query checks to make sure that each table has a column of a date or time related type
-- If your column types were detected properly prior to upload this table should be empty
SELECT
 table_name,
 SUM(CASE
     WHEN data_type IN ("TIMESTAMP", "DATETIME", "TIME", "DATE") THEN 1
   ELSE
   0
 END
   ) AS has_time_info
FROM
INFORMATION_SCHEMA.COLUMNS
WHERE 
table_schema = 'fitbit' and
 data_type IN ("TIMESTAMP",
   "DATETIME",
   "DATE")
GROUP BY
 1
HAVING
 has_time_info = 0;
```

This query returned nothing, which is a good sign. That means every table also has a data type with a date, which can also be used as our other primary key, which turns this into a composite key.

3. Perform calculations and Identify trends and relationships.
#### Interesting facts:

```MySQL
SELECT AVG(steptotal) FROM fitbit.daily_steps;
```
7637.9106
steps, which lies in the somewhat active range according to:
https://karencollinsnutrition.com/10000-step-goal-5-key-questions/
```MySQL
SELECT AVG(sedentaryminutes) FROM fitbit.daily_intensities;
```
991.2106
minutes, which is the same as 16.5 hours. This was a shock and is definitely a good catch.
#### Calculations
- I will perform certain calculations, such as joining specific tables together, then exporting the results in a csv, so I can then use Python to visualize what is happening and look for trends and relationships.
```MySQL
-- daily_activity join sleep_day
SELECT * FROM fitbit.daily_activity da INNER JOIN fitbit.sleep_day sd on (da.ActivityDate = sd.SleepDay and da.id = sd.id);
-- saved results into daily_activity_join_sleep_day.csv

```

```MySQL

-- daily_steps join daily_calories
SELECT * FROM fitbit.daily_steps ds INNER JOIN fitbit.daily_calories dc on (ds.ActivityDay = dc.ActivityDay and ds.id = dc.id);
-- saved results into daily_steps_join_daily_calories.csv

```

#### Visualization:
```Python 3.0
# Read data from CSV file
df = pd.read_csv(r'C:\ProgramData\MySQL\MySQL Server 8.0\Data\fitbit\sleepDay_merged_cleaned.csv')

# Create a scatter plot
plt.scatter(df['TotalMinutesAsleep'], df['TotalTimeInBed'], s=10, alpha=0.5)


# Add a linear regression line
coefficients = np.polyfit(df['TotalMinutesAsleep'], df['TotalTimeInBed'], 1)
poly = np.poly1d(coefficients)
new_x = np.linspace(df['TotalMinutesAsleep'].min(), df['TotalMinutesAsleep'].max())
new_y = poly(new_x)
plt.plot(new_x, new_y, 'r-', label='Linear Regression')

# Add labels and title
plt.xlabel('Total Minutes Asleep')
plt.ylabel('Total Time in Bed (minutes)')
plt.legend()
plt.title('Total Minutes Asleep vs Total Time in Bed (Minutes)')

# Show the plot
plt.show()
```
![[Untitled 7.png]]
The scatter plot of total minutes asleep versus total time in bed exhibits a very strong positive correlation, with the data points closely following the line y=x. This indicates a near-linear relationship between the two variables. The majority of the data points are concentrated between 300 and 550 minutes (5 to 9 hours) for both total minutes asleep and total time in bed.

```Python 3.0
# Read data from CSV file
df = pd.read_csv(r'C:\ProgramData\MySQL\MySQL Server 8.0\Data\fitbit\calculations\daily_steps_join_daily_calories.csv')

# Extract data from the dataframe
x = np.array(df['StepTotal'])
y = np.array(df['Calories'])

# Create a scatter plot
plt.scatter(x, y, s=10, alpha=0.6)

# Fit a polynomial curve
degree = 3  # Adjust the degree as needed
coeffs = np.polyfit(x, y, degree)
poly = np.poly1d(coeffs)

# Create a range of x-values for the curve
x_curve = np.linspace(min(x), max(x), 100)
y_curve = poly(x_curve)

# Plot the curve
line, = plt.plot(x_curve, y_curve, 'r-', label='Polynomial Fit')

# Add labels and title
plt.xlabel('Total Steps')
plt.ylabel('Calories Burned')
plt.title('Total Steps vs Calories Burned')

# Add legend
plt.legend(handles=[line])  # Pass the line object, not the NumPy array

# Show the plot
plt.show()
```
![[Untitled 12.png]]
The scatter plot exhibits a distinct polynomial curve pattern with 3 degrees of freedom between total steps and calories burned, with most data points falling in the 1,000 to 15,000 step range and 1,000 to 3,000 calories burned range. While the overall trend appears mostly linear, aligning with the expectation of more steps leading to more calories burned, the presence of some outliers likely contributes to the higher degree 3rd order polynomial curve fitting.

```Python 3.0
# Read data from CSV file
df = pd.read_csv(r'C:\ProgramData\MySQL\MySQL Server 8.0\Data\fitbit\calculations\daily_activity_join_sleep_day.csv')

# Extract the relevant columns
x = df['TotalTimeInBed']
y = df['TotalSteps']

# Create the scatter plot
plt.scatter(x, y, s=10, alpha=0.6)

# Add labels and title
plt.xlabel('Total Minutes Asleep')
plt.ylabel('Total Steps')
plt.title('Total Steps vs Total Minutes Asleep')

# Show the plot
plt.show()
```
![[Untitled 9.png]]
The scatter plot does not show a clear linear relationship between sleep duration and activity levels measured by total steps. However, there is a concentration of data points within the range of approximately 400 to 600 minutes of total sleep and 1,000 to 15,000 total steps, suggesting that a significant portion of users experienced sleep durations and activity levels falling within those particular value ranges.

Now, I want to calculate the daily average steps of each user and categorize them into 4 sections classified by:
https://karencollinsnutrition.com/10000-step-goal-5-key-questions/
This study shows 5 different sections of classifications depending on how many steps the user takes per day and 2 sections. One of the sections being physically active and the other being physically inactive.

1. People who likely meet current recommended levels of physical activity are further classified as
	* **Highly Active:** more than 12,500 steps per day
	- **Active:** 10,000-12,499 steps per day
	- **Somewhat Active:** 7,550-9,999 steps per day
2. People considered physically inactive are classified as:
	- **Low Active:** 5,000-7,499 steps per day
	- **Sedentary:** less than 5,000 steps per day

Using the query:
```MySQL
SELECT 
    Id,
    AVG(StepTotal) AS 'Average Steps',
    CASE
        WHEN AVG(StepTotal) >= 12500 THEN 'Highly Active'
        WHEN AVG(StepTotal) BETWEEN 10000 AND 12499 THEN 'Active'
        WHEN AVG(StepTotal) BETWEEN 7500 AND 9999 THEN 'Somewhat Active'
        WHEN AVG(StepTotal) BETWEEN 5000 AND 7499 THEN 'Low Active'
        ELSE 'Sedentary'
    END AS 'Activity Level'
FROM fitbit.daily_steps
GROUP BY Id;
-- saved results into average_steps_for_users.csv
```

| Id         | "Average Steps" | "Activity Level"  |
| ---------- | --------------- | ----------------- |
| 1503960366 | 12116.7419      | Active            |
| 1624580081 | 5743.9032       | "Low Active"      |
| 1644430081 | 7282.9667       | "Low Active"      |
| 1844505072 | 2580.0645       | Sedentary         |
| 1927972279 | 916.1290        | Sedentary         |
| 2022484408 | 11370.6452      | Active            |
| 2026352035 | 5566.8710       | "Low Active"      |
| 2320127002 | 4716.8710       | Sedentary         |
| 2347167796 | 9519.6667       | "Somewhat Active" |
| 2873212765 | 7555.7742       | "Somewhat Active" |
| 3372868164 | 6861.6500       | "Low Active"      |
| 3977333714 | 10984.5667      | Active            |
| 4020332650 | 2267.2258       | Sedentary         |
| 4057192912 | 3838.0000       | Sedentary         |
| 4319703577 | 7268.8387       | "Low Active"      |
| 4388161847 | 10813.9355      | Active            |
| 4445114986 | 4796.5484       | Sedentary         |
| 4558609924 | 7685.1290       | "Somewhat Active" |
| 4702921684 | 8572.0645       | "Somewhat Active" |
| 5553957443 | 8612.5806       | "Somewhat Active" |
| 5577150313 | 8304.4333       | "Somewhat Active" |
| 6117666160 | 7046.7143       | "Low Active"      |
| 6290855005 | 5649.5517       | "Low Active"      |
| 6775888955 | 2519.6923       | Sedentary         |
| 6962181067 | 9794.8065       | "Somewhat Active" |
| 7007744171 | 11323.4231      | Active            |
| 7086361926 | 9371.7742       | "Somewhat Active" |
| 8053475328 | 14763.2903      | "Highly Active"   |
| 8253242879 | 6482.1579       | "Low Active"      |
| 8378563200 | 8717.7097       | "Somewhat Active" |
| 8583815059 | 7198.5161       | "Low Active"      |
| 8792009665 | 1853.7241       | Sedentary         |
| 8877689391 | 16040.0323      | "Highly Active"   |

Now we can put this data in Python to do some more visualization.

```Python 3.0
# Read data from CSV file
df = pd.read_csv(r'C:\ProgramData\MySQL\MySQL Server 8.0\Data\fitbit\calculations\average_steps_for_users_with_classification.csv')

# Define the desired order of categories
categories = ['Sedentary', 'Low Active', 'Somewhat Active', 'Active', 'Highly Active']

# Convert the 'Activity Level' column to categorical data type with the desired order
df['Activity Level'] = pd.Categorical(df['Activity Level'], categories=categories, ordered=True)

# Count the occurrences of each activity level
activity_counts = df['Activity Level'].value_counts()

# Sort the activity counts based on the desired order
activity_counts = activity_counts.reindex(categories)

# Create a pie chart
fig, ax = plt.subplots(figsize=(8, 6))
ax.pie(activity_counts, labels=activity_counts.index, autopct='%1.1f%%', startangle=90, counterclock=False)
ax.axis('equal')  # Equal aspect ratio ensures the pie chart is drawn as a circle
ax.set_title('Activity Levels of Users')

# Show the plot
plt.show()
```
![[Untitled 10.png]]
```Python 3.0
# Define the categories to group
inactive_categories = ['Sedentary', 'Low Active']
active_categories = ['Somewhat Active', 'Active', 'Highly Active']

# Create a new column 'Activity Group' based on the grouping
df['Activity Group'] = np.where(df['Activity Level'].isin(inactive_categories), 'Physically Inactive', 'Physically Active')

# Count the occurrences of each activity group
activity_group_counts = df['Activity Group'].value_counts()

# Create a pie chart
fig, ax = plt.subplots(figsize=(8, 6))
ax.pie(activity_group_counts, labels=activity_group_counts.index, autopct='%1.1f%%')
ax.axis('equal')  # Equal aspect ratio ensures the pie chart is drawn as a circle
ax.set_title('Physical Activity Levels of IDs')

# Show the plot
plt.show()
```
![[Untitled 11.png]]
The data shows the distribution of 33 users across different activity level categories based on their total step counts:

- 24.2% in the sedentary category (less than 2,500 steps)
- 27.3% in the low active category (between 5,000 and 7,499 steps)
- 27.3% in the somewhat active category (between 7,500 and 9,999 steps)
- 15.2% in the active category (between 10,000 and 12,499 steps)
- 6.1% in the highly active category (more than 12,500 steps)

Additionally, the data is categorized into two broader groups:

- 51.5% of users classified as "Physically Inactive" (combining sedentary and low active categories)
- 48.5% of users classified as "Physically Active" (combining somewhat active, active, and highly active categories)

### Deliverable
A summary of your analysis.

The data reveals insights into the relationships between various metrics tracked by Bellabeat's fitness products, as well as the activity levels of their user base. Sleep Analysis:

- There is a very strong positive correlation between total minutes asleep and total time in bed, indicating a near-linear relationship. Most users fall within the range of 5 to 9 hours for both sleep duration and time in bed.

Activity and Calorie Expenditure:

- The scatter plot of total steps versus calories burned exhibits a polynomial curve pattern with 3 degrees of freedom, suggesting a non-linear but generally positive correlation.
- While the overall trend appears mostly linear (more steps leading to more calories burned), the presence of outliers likely contributes to the higher-order polynomial curve fitting.

Sleep Duration and Activity Levels:

- There is no clear linear relationship between sleep duration and activity levels measured by total steps.
- However, a significant portion of users experienced sleep durations between 400 to 600 minutes (6.7 to 10 hours) and activity levels within the range of 1,000 to 15,000 total steps.

User Activity Level Distribution:

- 24.2% of users are classified as sedentary (less than 2,500 steps).
- 27.3% are low active (5,000 to 7,499 steps), and another 27.3% are somewhat active (7,500 to 9,999 steps).
- 15.2% are active (10,000 to 12,499 steps), and 6.1% are highly active (more than 12,500 steps).
- Overall, 51.5% of users are classified as "Physically Inactive" (sedentary and low active combined), while 48.5% are "Physically Active" (somewhat active, active, and highly active combined).

Interesting Facts:

- The average total steps per user is 7,638.
- The average sedentary time per user is around 16.5 hours.

This analysis provides insights into the diverse activity levels, sleep patterns, and relationships between various metrics tracked by Bellabeat's products, which can inform product development, marketing strategies, and user engagement initiatives.
## Case Study Roadmap - Share
### Guiding questions
● Were you able to answer the business questions?
	Yes, the analysis provides insights that can help answer key business questions around understanding user activity levels, sleep patterns, and relationships between tracked metrics to inform product development and marketing strategies.
● What story does your data tell?
	 The data tells a story of a diverse user base with varying activity levels and sleep durations, while revealing relationships like the linear connection between steps and calorie expenditure, and the concentration of users within specific activity/sleep ranges.
● How do your findings relate to your original question?
	 The findings directly relate to the original questions by uncovering patterns, distributions, and correlations within the user data that can guide decisions around Bellabeat's product offerings and user engagement initiatives.
● Who is your audience? What is the best way to communicate with them?
	 The audience is Bellabeat's leadership team and stakeholders. The best way to communicate the findings is through a clear, visually-supported presentation or report that highlights the key insights and their potential business implications for the company
● Can data visualization help you share your findings?
	 Yes, data visualization is crucial for effectively sharing the findings, as the visualizations (scatter plots, pie charts) clearly illustrate the relationships, distributions, and patterns identified in the analysis.
● Is your presentation accessible to your audience?
	 To ensure accessibility, the presentation should follow best practices such as providing alternative text descriptions for visualizations, ensuring color choices are suitable for individuals with color vision deficiencies, and considering the needs of individuals with disabilities if presenting in person.

## Case Study Roadmap - Act
### Guiding questions
● What is your final conclusion based on your analysis?
	 The analysis reveals diverse activity levels, sleep patterns, and relationships between tracked metrics, providing insights into Bellabeat's user base and their behaviors.
● How could your team and business apply your insights?
	 These insights can inform product development, marketing strategies, and user engagement initiatives to better cater to different user segments and promote healthy behaviors.
● What next steps would you or your stakeholders take based on your findings?
	 Potential next steps include further analyzing specific user segments, exploring additional data sources, and developing targeted product features or campaigns based on the identified patterns and relationships.
● Is there additional data you could use to expand on your findings?
	 Additional data sources like user demographics, location data, or qualitative feedback could provide more context and expand on the current findings.
### Deliverable
Your top high-level insights based on your analysis

1. Significant portion (51.5%) of users classified as "Physically Inactive," presenting an opportunity to promote and encourage more active lifestyles.
	- This highlights a major segment of Bellabeat's user base that could benefit from targeted interventions and features aimed at increasing physical activity levels.
	- Potential strategies could include personalized goal-setting, activity challenges, rewards/gamification, or integration with fitness programs tailored for inactive individuals.
	- Promoting the health benefits of an active lifestyle and providing educational resources could also help motivate and support this segment in making positive changes.
2. Strong positive correlation between sleep duration and time in bed, suggesting potential for sleep optimization features or recommendations.
	- The near-linear relationship indicates that users who spend more time in bed tend to get more sleep, presenting an opportunity for sleep tracking and optimization.
	- Bellabeat could develop features that provide personalized sleep duration recommendations based on an individual's time in bed and other factors.
	- Sleep hygiene tips, bedtime reminders, and integration with smart home devices (e.g., adjusting temperature, lighting) could help users optimize their sleep environment and routines.
3. Mostly linear relationship between steps and calorie expenditure, enabling accurate calorie estimation based on step data, a valuable feature for fitness tracking.
	- The ability to reliably estimate calorie burn from step counts alone could differentiate Bellabeat's offerings in the wearable fitness market.
	- Developing accurate calorie estimation models based on step data could provide users with a simple and effective way to monitor their calorie expenditure without needing additional sensors or complex algorithms.
	- This could be a key selling point for Bellabeat's products, as accurate calorie tracking is a highly sought-after feature in the fitness tracking space.
4. Concentration of users within specific ranges of sleep duration and activity levels, indicating potential target segments for tailored product offerings or marketing campaigns.
	- The identified ranges (e.g., 400-600 minutes of sleep, 1,000-15,000 steps) represent significant segments of Bellabeat's user base.
	- Bellabeat could develop targeted product features, content, or marketing campaigns specifically tailored to the needs and preferences of these segments.
	- For example, users within the identified sleep range could benefit from sleep tracking and optimization features, while those in the activity level range could be targeted with step challenges or activity-based rewards.
