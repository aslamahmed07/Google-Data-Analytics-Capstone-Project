# Google Data Analytics_Case Study: Cyclstic Bike-Share
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
## PHASE 1 : Ask
#### Three questions will guide the future marketing program:
1. How do annual members and casual riders use Cyclistic bikes differently?

2. Why would casual riders buy Cyclistic annual memberships?

3. How can Cyclistic use digital media to influence casual riders to become members?
### Business Task
- Find out how do annual members and casual riders use cyclstic bikes differently.
 
- Find insgihts about bike usage which will be helpful to design marketing strategies for converting casual riders to annual members.
### Stakeholders
Primary Stakeholders : Lily Moreno,The director of marketing

Secondary Stakeholders : Cyclistic executive team
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
- Uploaded the 12 Excel files to RStudio to Combine them in to Single Sheet
- Used "readxl" function to upload the data into R and named the dataset as "cb1,cb2,cb3,cb3,cb4,cb5,cb6,cb7,cb8,cb9,cb10,cb11,cb12"   
``` sql
library(readxl)
cb1 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/1-202101-divvy-tripdata.xlsx") 
cb2 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/2-202102-divvy-tripdata.xlsx") 
cb3 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/3-202103-divvy-tripdata.xlsx") 
cb4 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/4-202104-divvy-tripdata.xlsx")
cb5 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/5-202105-divvy-tripdata.xlsx")
cb6 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/6-202106-divvy-tripdata.xlsx")
cb7 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/7-202107-divvy-tripdata.xlsx")
cb8 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/8-202108-divvy-tripdata.xlsx")
cb9 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/9-202109-divvy-tripdata.xlsx")
cb10 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/10-202110-divvy-tripdata.xlsx")
cb11 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/11-202111-divvy-tripdata.xlsx")
cb12 <- read_excel("E:/GDAC_Capestone_Project/Case_study-Cyclistic Bike Share/Data Set/12-202112-divvy-tripdata.xlsx")
```
- Combine the 12 Excelsheet into single excel file 
- Used "bind_rows" function to Combine the data by rows and named it as "Summmary_data_2021"
``` sql
install.packages("dplyr")
library(dplyr)
summmary_data_2021<-bind_rows(cb1,cb2,cb3,cb4,cb5,cb6,cb7,cb8,cb9,cb10,cb11,cb12)
View(summmary_data_2021)
```
- Exported the file into system by using "write.csv" function and saved it under file name "consodata2021"
``` sql
write.csv(summmary_data_2021,"Consodata2021.csv")
```

The Final Data Contatins 4,588,302 Rows and 14 Coloumns , which is used for analyzing the data

## PHASE 4 : Data Analyze

*Data Visulizations and  Key Insights i found are Explained in this Phase* [Click here to view the Dashboard](https://public.tableau.com/app/profile/aslam.ahmed/viz/GDAC_Capstone_Project_CyclisticBike-Share/Project#1)

### Membership Type Vs Number of Rides

![](https://github.com/aslamahmed07/Google-Data-Analytics---Capstone-Project/blob/main/Membershiptype.png)

####  Data Findings :
- Member Riders takes more number of trips than Casual Riders
  
   *Member Riders : 2,539,923   55% of Total Rides*
   
   *Casual Riders : 2,048,379  45% of Total Rides*
   
- Member Riders use Cyclistic bike Share on daily basis  as main mode of point to point transportation

### Average Ride Length by Membershiptype

![](https://github.com/aslamahmed07/Google-Data-Analytics---Capstone-Project/blob/main/2-Avg_Ride_Length.png)

#### Data Findings : 

  *Average Ride length* 

  *Member  Rider : 14 Mints*

  *Casual Rider : 30 Mints* 

- Casual Riders takes less number of rides for longer durations

- Casual Riders mostly use bikes for recreational Purposes

- Annual Members takes more number of rides for short durations

### Number of Rides by Bike Type

![](https://github.com/aslamahmed07/Google-Data-Analytics---Capstone-Project/blob/main/3-BikeType_Rideable%20type.png)

#### Data Findings : 

- Popular bike type among both Member Rider and Casual rider is classic bike 
  
  *Total No of Rides : 3,241,988*

- Found 71 % of Riders use Classic Bikes Comparing with total of rides in the year 2021

- Docked bike are only used by Casual rider

  *Total No of Rides : 3,12,048*
  
### Number of Rides Vs Month of Ride
  
  ![](https://github.com/aslamahmed07/Google-Data-Analytics---Capstone-Project/blob/main/4-Month%20of%20Ride.png)
  
  #### Data Findings :
  
##### Casual Rider                                                                   

- Popular Months  : June,July & August                                          
   
- Season : Summer Season                                                       
  
- Number of Rides in Each Month                                                 
   
   June : 3,04,192                                                               
   
   July : 3,69,415
   
   August : 3,41,476

- Highest Number of  rides on month July in Year 2021

##### Member Rider

- Popular Months  : June,July& August 

- Season : Summer Season 

- Number of Rides in each Month

   June : 3,04,586

   July : 3,22,906

   August : 3,32,933

- Highest Number of  rides on month August in  Year 2021


### Number of Rides Vs Day of Week
  
  ![](https://github.com/aslamahmed07/Google-Data-Analytics---Capstone-Project/blob/main/5-Day%20of%20Week.png)
  
#### Data Findings :
  
#### Casual Rider 
- Popular days  : Saturday & Sunday
- Weekend days
- Number of Rides in Each Days
   Saturday : 4,68,331
   Sunday : 4,03,789 

- Casual Riders uses Cyclistic bikes mostly on weekend days.

- Significant increase in number of rides from friday to saturday.

#### Member Rider
 
- Popular days  : Tuesday & Wednesday
- Weekdays
- Number of Rides in Each Days
   Tuesday : 3,88,132
   Wednesday : 3,97,720
   
- Member Riders uses Cyclistic bikes mostly on weekdays.

- Couldnt find any remarkable increase in the number of rides through out the week. 

### Number of Rides Vs Time of day

![](https://github.com/aslamahmed07/Google-Data-Analytics---Capstone-Project/blob/main/6-Ridetime%20of%20Day.png)

#### Data Findings :

#### Casual Rider 
- Peak time  : 4PM & 5PM
- Number of Rides 
   4PM : 1,67,976
   5PM : 1,95,963 

- Peak time for Casual riders to use bikes are 4PM & 5PM of the Day

#### Member Rider 
- Peak time  : 4PM & 5PM
- Number of Rides 
   4PM : 2,16,690
   5PM : 2,73,672 

- Peak time for Member riders to use bikes are 4PM & 5PM of the Day

### Peak Ride time on Summer Season

![](https://github.com/aslamahmed07/Google-Data-Analytics---Capstone-Project/blob/main/7-Ride%20Time%20of%20day%20on%20Peak%20Months.png)

#### Data Findings :

- As we found earlier popular or peak month for both Casual and member riders was June July & August which is the Summer Seaon

- When we analysed the Number of rides of the summer season we found that Evening time was the peak time for Most usage of Bikes

### Popular Start Stations

![](https://github.com/aslamahmed07/Google-Data-Analytics---Capstone-Project/blob/main/8-Popular%20Start%20Station.png)

### Popular End Stations

![](https://github.com/aslamahmed07/Google-Data-Analytics---Capstone-Project/blob/main/8-Popular%20Start%20Station.png)

#### Data Findings :

##### Top 5 Popular Start & End Staions
       Streeter Dr & Grand Ave.
       Michigan Ave & Oak St.
       Well St & Concord Ln.
       Millenium Park.
       Clark St & Elm St.
       
## PHASE 5 : Share

- Tableau Desktop 2022.1 Software is used for Data Visulization and Presenting Key Insights  
 [Click here to view the Dashboard](https://public.tableau.com/app/profile/aslam.ahmed/viz/GDAC_Capstone_Project_CyclisticBike-Share/Project#1)

## PHASE  : Act

### Conclusions

- Casual Riders takes less number of trips for Longer duration

- Casual riders are most active on weekend days and on summer season

- Peak ride time is the evening time of the day ie 4Pm - 5PM

- Top 3 Popular Start and End Statins : Streeter Dr & Grand Ave.,Michigan Ave & Oak St.Well St & Concord Ln.

### My Recommendations based on the Key Findings :

- Increase the charge for single day or Single ride passes on weekend days to promote Membership.

- Increase the Charge for Single ride Passes on Evening time especially 4PM to 5 PM to Promote Membership

- Implement Special Summer Season riding Packages including Special offers and discount.

- Conduct Weekend Contest and Summer events to Promote Membership.

- Effective and efficient Promotions for targeting casual riders during busiest time and Stations.

     - Days : Weekend Days (Saturday & Sunday)
     
     - Month : Summer Season (June, July & August)
     
     - Top Three Stations : Streeter Dr & Grand Ave.,Michigan Ave & Oak St.Well St & Concord Ln.

- Our Promotions or advetisement must aware people about Benefits of Cycling on daily life

    #### Main Benefits of Cycling 
   
    - Imporve Mental & Physical Health .
    
    - Cuts down on greenhouse gas emissions and global climate change.

    - Reduces noise pollution and congestion.

    - Saves More Money When Comparing  to Current Fuel Price.
 
 #### Thank you for Viewing My Work, Have a nice day and Happy Analyzing !  :)

### References
 
[Clck here to View Data Set](https://divvy-tripdata.s3.amazonaws.com/index.html)


[Clck here to View Data License](https://ride.divvybikes.com/data-license-agreement)


[Click her to View My Linkedin Profile](https://www.linkedin.com/in/aslam-ahmed-39237a145/)






































