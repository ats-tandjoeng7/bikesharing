# Bike Sharing
This project focused on the application of Python Pandas and Tableau, and how we leveraged their useful functions and GUIs for performing in-depth data analytics and visualizations.

## Table of Contents
- [Overview of Project](#overview-of-project)
  - [Resources](#resources)
  - [Challenge Overview](#challenge-overview)
  - [GitHub Repo Branches](#github-repo-branches)
- [Experimental and Analysis Results](#experimental-and-analysis-results)
  - [Deliverable 1](#deliverable-1)
  - [Deliverable 2-1](#deliverable-2-1)
  - [Deliverable 2-2](#deliverable-2-2)
  - [Deliverable 2-3](#deliverable-2-3)
  - [Deliverable 3](#deliverable-3)
- [Summary](#summary)
- [References](#references)

## Overview of Project
This project and Module 15 assignment focused on cultivating knowledge and skills of data analytics and visualizations that helped to further understand the concepts of crafting convincing analysis report and bike sharing business proposal. During the completion of this project we mainly leveraged the powerful features offered by Python Pandas and [Tableau Public](https://www.tableau.com/products/public), a free platform that lets us explore, create, and publicly share data visualizations online.

### Resources
- Source code: NYC_Citibike_Challenge.ipynb
- Source data: [201908-citibike-tripdata](https://s3.amazonaws.com/tripdata/201908-citibike-tripdata.csv.zip)
- Image file: png files
- Software: [Tableau Public](https://www.tableau.com/products/public), [Pandas User Guide](https://pandas.pydata.org/pandas-docs/stable/user_guide/index.html#user-guide).

### Challenge Overview
Below is the outline of our deliverables and a written report for presenting our results and analysis summary. Upon completion of this project, we created visualizations that showed the length of time that bikes were checked out for all riders and genders, the number of bike trips for all riders and genders for each hour of each day of the week, and the number of bike trips for each type of user and gender for each day of the week. We then compiled a final presentation that summarizes our analysis results and data visualizations for our stakeholders and potential investors.

- ☑️ Deliverable 1: Change Trip Duration to a Datetime Format.
- ☑️ Deliverable 2: Create Visualizations for the Trip Analysis.
- ☑️ Deliverable 3: Create a Story and Report for the Final Presentation.
- ☑️ Summary: A summary on the bike sharing visualizations and business proposal (this ["README.md"](./README.md)).

### GitHub Repo Branches
All required deliverables are committed in this GitHub repo as outlined below.  

main branch  
|&rarr; [./README.md](./README.md)  
|&rarr; [./NYC_Citibike_Challenge.ipynb](./NYC_Citibike_Challenge.ipynb)  
|&rarr; ./Data/  
  &emsp; |&rarr; [./Data/citibike_df_table_image.png](./Data/citibike_df_table_image.png)  
  &emsp; |&rarr; [./Data/CheckoutTimesForUsers.png](./Data/CheckoutTimesForUsers.png)  
  &emsp; |&rarr; [./Data/CheckoutTimesByGender.png](./Data/CheckoutTimesByGender.png)  
  &emsp; |&rarr; [./Data/TripsByWeekdayPerHour.png](./Data/TripsByWeekdayPerHour.png)  
  &emsp; |&rarr; [./Data/TripsByGender_WeekdayPerHour.png](./Data/TripsByGender_WeekdayPerHour.png)  
  &emsp; |&rarr; [./Data/UserTripsByGenderByWeekday.png](./Data/UserTripsByGenderByWeekday.png)  
  &emsp; |&rarr; [./Data/GenerationAndGenderBreakdownPerUsertype.png](./Data/GenerationAndGenderBreakdownPerUsertype.png)  
  &emsp; |&rarr; [./Data/BikeUtilizationByGenerationByGender.png](./Data/BikeUtilizationByGenerationByGender.png)  
  &emsp; |&rarr; [./Data/BikeidToRepair.png](./Data/BikeidToRepair.png)  

## Experimental and Analysis Results
We first reformatted the original csv data by using Python Pandas and then used Tableau to perform in-depth analysis and visualizations. Although I retained all the initial field data when saving the modified DataFrame to a csv file, there were several unique approaches that I used when accomplishing the required visualizations as discussed and highlighted below. Some of the improvement ideas for future analysis were also analyzed and embodied in the Tableau visualization dashboard (<a href="https://public.tableau.com/app/profile/s.tandjoeng/viz/bikesharing_visualizations_16701338840620/NYCCitiBikeStory?publish=yes" target="_blank" title="Link to NYC Citi Bike Story">Bike Sharing Visualizations</a>).

### Deliverable 1
We used Python Pandas's `to_datetime()` function to convert the datatype of trip duration data in the original table from **int64** to **datetime64[ns]**, which is a datetime format with nanosecond **[ns]** precision. I double checked the resulting time format by using `datetime.strftime('%H:%M:%S')`. The source code can be referred in [NYC_Citibike_Challenge.ipynb](./NYC_Citibike_Challenge.ipynb) and the first five rows of our modified dataframe table are shown in Fig. 1. Please be kindly informed that the modified csv file, *201908-citibike-tripdata_new.csv.zip*, was too massive to be uploaded to a GitHub repo.

```
import pandas as pd
import datetime as dt
# 3. Convert the 'tripduration' column to datetime datatype.
citibike_df["tripduration"] = pd.to_datetime(citibike_df["tripduration"], unit='s')
# double check datetime conversion
print(pd.to_datetime(citibike_df["tripduration"], unit='s', utc=True).dt.strftime('%H:%M:%S'))
```

![Fig. 1](./Data/citibike_df_table_image.png 'Fig. 1 Modified 201908-citibike-tripdata table')\
**Fig. 1 Modified 201908-citibike-tripdata table**

### Deliverable 2-1
Instead of `IF-ELSEIF-END` statement, I used `IIF(condition, then, else)` function as demonstrated below, which is more suitable for generating simple binning labels such as gender classification, to create a calculated field from the **Gender** field and named the new field as **Gender Category**. The **Gender Category** field used in this work was identical to **Number to String** field in the Module 15 instructions. The visualizations of the number of bikes checked out by duration for all users and for each gender category by the hour are shown in Fig. 2 and Fig. 3. The filters on custom value lists, titles, and axis labels had been adjusted accordingly.

```
// IIF() function is suitable for simple labels
IIF([Gender] = 1, 'MALE', IIF([Gender] = 2, 'FEMALE', 'UNKNOWN'))
```

![Fig. 2](./Data/CheckoutTimesForUsers.png 'Fig. 2 Checkout Times for Users')\
**Fig. 2 Checkout Times for Users**

![Fig. 3](./Data/CheckoutTimesByGender.png 'Fig. 3 Checkout Times by Gender')\
**Fig. 3 Checkout Times by Gender**

Most trip duration fell within an hour long and the maximum trip duration was pretty brief, 5 minutes for male users and 6 minutes for female users on average. The line graphs in Fig. 2 and Fig. 3 could suggest that
- users relied on bike sharing service for going places that were in proximity,
- users might have used the bike sharing service several times, but every trip only lasted a few minutes and rarely exceeded 60 minutes.

### Deliverable 2-2
We reproduced the heatmap visualizations representing the number of bike trips for each hour of each day of the week without and with gender classification as shown by Fig. 4 and Fig. 5. The filters on custom value lists, titles, and axis labels had been customized according to the challenge requirements, including the use of abbreviations of days of the week and 12-hour format.

![Fig. 4](./Data/TripsByWeekdayPerHour.png 'Fig. 4 Trips by Weekday for Each Hour')\
**Fig. 4 Trips by Weekday for Each Hour**

![Fig. 5](./Data/TripsByGender_WeekdayPerHour.png 'Fig. 5 Trips by Gender (Weekday for Each Hour)')\
**Fig. 5 Trips by Gender (Weekday for Each Hour)**

Peak hours in the month of August 2019 were either between 7-9 AM in the morning or between 5-8 PM in the afternoon on weekdays, except for Wednesday's afternoon that looked less busy than the rest of weekdays. Timeframe between 5-7 PM on Thursdays was the busiest of all other timeframes. Peak hours on Friday's afternoon shifted earlier that the other weekdays, probably because most users finished early on Fridays. The heatmap visualizations also suggested that on weekends, 7-9 AM timeframe was less busy because most users started to use the bike sharing service after 9 AM, and most government offices and businesses were probably closed on weekends. As for gender dependency, the majority of users was male. There was no clear tendency observed in the *UNKNOWN* gender category.

### Deliverable 2-3
The heatmap visualizations representing the number of bike trips for each type of user and gender for each day of the week are shown in Fig. 6. The filters on custom value lists, titles, and axis labels had been modified according to the challenge requirements. Fig. 6 reconfirmed our observations based on Fig. 4 and Fig. 5. It also reiterated that the majority of bike sharing users were annual subscribers instead of random customers.

![Fig. 6](./Data/UserTripsByGenderByWeekday.png 'Fig. 6 User Trips by Gender by Weekday')\
**Fig. 6 User Trips by Gender by Weekday**

## Summary
All deliverables have been crafted and analyzed according to the assignment requirements, including code refactoring, quality assurance for ensuring accurate results, more descriptive field labels, better usability, and optimized dashboard performance. I hope users and stakeholders will be able to benefit from our visualizations online <a href="https://public.tableau.com/app/profile/s.tandjoeng/viz/bikesharing_visualizations_16701338840620/NYCCitiBikeStory?publish=yes" target="_blank" title="Link to NYC Citi Bike Story">Bike Sharing Visualizations</a> and easily explore our analysis summary and story before drawing the final conclusions.

To better understand the demographic of users and which gender or generation groups the bike sharing businesses should target to boost the bike utilization, I further created custom groups based on Birth Year of our users and conducted visualizations with fixed ranges of *Number of Trips* to better crunch the dataset as demonstrated in Fig. 7. The chart and filter we embedded in Fig. 7 was part of my suggestions for future analysis. It significantly helped us understand the demographic of bike sharing users and users' gender gaps at once.
- More than 80% of users were annual subscribers.
- Users were approximately 65% male, 25% female, and 10% other genders. Male users were the top users of bike sharing service, including the length of bike utilization, across all generations except for Gen X.
- Gen Y (Millennials) were the most frequent users overall regardless of gender, though *UNKNOWN* gender users were top in the random customer usertype.
- *UNKNOWN* gender category was mainly from those users belonged to Gen X because they might have opted for not reporting, though we do not know why Gen X was not providing their gender information in most cases.

![Fig. 7](./Data/GenerationAndGenderBreakdownPerUsertype.png 'Fig. 7 Generation and Gender Breakdown per Usertype')\
**Fig. 7 Generation and Gender Breakdown per Usertype**

![Fig. 8](./Data/BikeUtilizationByGenerationByGender.png 'Fig. 8 Bike Utilization by Generation by Gender')\
**Fig. 8 Bike Utilization by Generation by Gender**

![Fig. 9](./Data/BikeidToRepair.png 'Fig. 9 Bikeid due for Repairs')\
**Fig. 9 Bikeid due for Repairs**

Fig. 8 together with Fig. 7 illustrated great tools that should allow us to draw more solid decisions in terms of demographic trends. Fig. 9 helped us pinpoint which Bikeids should be repaired immediately or was beyond repair because its utilization length has exceeded certain safety criteria. Users could just hover over the chart to quickly spot a specific Bikeid or a group of Bikeids that were due for repairs.

Based on our data analytics and visualizations, to boost revenues we will need to study why non-male users were less likely to use bike sharing service and how to expand accessibility of our bike sharing service to female and other gender groups, for example by providing easily adjustable size/power, assorted color selection, trackable safety apps, or even specialized bike sharing service for female and other gender groups. Providing a few bike options, including a cheaper rental option, might also be the key to be inclusive and better attract Gen Z to become frequent users. As for software app improvement, integrating better Search Engine Optimization (SEO) into the bike sharing service apps, such that different gender and community groups could easily find and access bikes that they will likely use more regularly.

## References
[Pandas User Guide](https://pandas.pydata.org/pandas-docs/stable/user_guide/index.html#user-guide)\
[[ISO 8601 Standard - date and time format](https://en.wikipedia.org/wiki/ISO_8601)\
[Tableau Public](https://www.tableau.com/products/public)\
[IF vs IIF and performance difference?](https://stackoverflow.com/questions/41576894/if-vs-iif-and-performance-difference)\
[6 tips to make your dashboards more performant](https://www.tableau.com/blog/5-tips-make-your-dashboards-more-performant-48574)\
[Generational Breakdown: Info About All Of The Generations](https://genhq.com/the-generations-hub/generational-faqs/)
