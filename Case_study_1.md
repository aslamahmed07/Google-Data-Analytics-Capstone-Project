# GDAPC_Case Study: Cyclstic Bike-Share
*This document is created as part of Google Data Analytics Professional Certificate Programm's Capstone Project*
# Scenario
You are a junior data analyst working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director
of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore,
your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights,
your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives
must approve your recommendations, so they must be backed up with compelling data insights and professional data
visualizations.
# About the Company
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that
are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and
returned to any other station in the system anytime.

*This Project includes the following Six Steps/Phases of data analysis process -* **Ask,Prepare,Process,Analyze,Share and Act**
# PHASE 1 : ASK
#### Three questions will guide the future marketing program:
1. How do annual members and casual riders use Cyclistic bikes differently?

2. Why would casual riders buy Cyclistic annual memberships?

3. How can Cyclistic use digital media to influence casual riders to become members?
### Business Task
- Find out how do annual members and casual riders use cyclstic bikes differently.
 
- Find insgihts about bike usage which will be helpful to design marketing strategies for converting casual riders to annual members.
### Stakeholders
Primary Stakeholders : Lily Moreno,The director of marketing

Secondary Stakeholders : Cyclistics executive team
## PHASE 2 : Prepare/Data Prep
The data we will be using is Cyclist's 12 Months (January-2021 to December 2021) historical trip data made available by Motivate International Inc. 
[Click here to view Data Set](https://divvy-tripdata.s3.amazonaws.com/index.html) under this license[Click here to view license](https://ride.divvybikes.com/data-license-agreement)

The Data Includes 12 CSV Files with 13 Coloumns which have details of each ride

Downloaded the 12 CSV Files and Stored with proper naming in sepereate folder and checked each files for errors and missing data

*The Credibility of the data is determined by the ROCCC approach*

- Reliable – It is complete and accurate and it represents all bike rides taken in the city of Chicago for the selected duration of our analysis.
- Original - The data is made available by Motivate International Inc. which operates the city of Chicago’s Divvy bicycle sharing service which is powered by Lyft Bikes and scooters LLC.
- Comprehensive - the data includes all information about ride details including starting time, ending time, station name, station ID, type of membership and many more.
- Current –  Not Current, Data we are using is from year 2021 
- Cited - The data is cited and is available under Data License Agreement.[License](https://ride.divvybikes.com/dataalicense-agreement)
### Data Limitations
While Checking the data ,found some missing data in "start station name" and "end station name" and found the data incomplete had to remove those particular cells,Further obesrvations suggest the most missing data about "start station name" belongs to "electric_bikes".

This limitation could affect our analysis for findigs about electric_bikes usage which will be useful for furthers analysis and Potential marketing camapaign or data driven business decision making.
## PHASE 3 : Process
### Tools used for Process
#### Data Cleaning and combining for Analysis 
##### 1.Microsoft Excel 

Excel is used to check data for erros and incompleteness
###### Steps:
- Downloaded each excel files and stored it in proper folders
- Checked for Blank cells , foud some blank data on "Start station name" &"End station name" and removed those cells considering it as incomplete data
- Removed the Coloumns "Start Station Id" &"End Station id" which wasn't required for analysis process
- Added a  coloumn named as "ride_length" , which Calculate the length of each ride by subtracting the column “started_at” from the column “ended_at” (for example, =D2-C2) and format as HH:MM:SS using Format > Cells >
Time > 37:30:55. 
- Added a column called “day_of_week,” and calculate the day of the week that each ride started using the “WEEKDAY”
command (for example, =WEEKDAY(C2,1)) in each file. Format as General or as a number with no decimals, noting that
1 = Sunday and 7 = Saturday.
- Added a coloumn called month_of_ride and noted each month of ride for analysis.
##### 2. R stuido
Considering the size of the data , Rstuio is used for Combining the 12 Files in to a single sheet
###### Steps:


