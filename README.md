# New-York-Taxi-Service-Optimization-Project

<h1 align="center">:taxi: Maven-Analytics-NYC-Taxi-Challenge :taxi:</h1>
<p align="center">
<img src= "https://user-images.githubusercontent.com/74512335/138792965-4a9225f1-09fc-4479-8dac-355f87af8f6f.png" />
</p>

**Link to dataset: https://www.mavenanalytics.io/blog/maven-taxi-challenge**

## Introduction
- This dataset is a part of maven taxi challenge and we are analyzing this massive dataset, containing more than 28 million taxi trips in New York City.
- Our assignment is to wrangle this massive data set, perform a thorough QA and cleaning of the data, and present a dashboard that the Lead Dispatcher can use to accurately understand historical trip information.
-----------
## Objective
- The `core objective` of this project to understand the historical trips for all Green Taxis in New York City, NYC (2017 – 2020) and to `uncover patterns and trends, with a focus on identifying opportunities to increase the efficiency of taxi services and improve customer satisfaction` in order to help firms for  better allocation of resources and meet the needs of the public.
----------------

## About the dataset
- This dataset contains 6 tables in csv format, along with a geospatial map in TopoJSON and Shapefile formats
- The `4 Taxi Trips tables `contain a total more than `28 million` Green Taxi trips in New York City from 2017 to 2020. Each record represents one trip, with fields containing details about the pick-up/drop-off times and locations, distances, fares, passengers, and more
- The `454 Calendar` table contains a `fiscal calendar (2017-2020)` used by the Taxi & Limousine Commission, with fields containing the date and fiscal year, quarter, month, and week
- The `Taxi Zones` table contains information about `265 zone locations` in New York City, including the location id, borough, and service zone
- The `Taxi Zones Map files` contain a `map of New York City with divisions for the 265 locations` that can be used to create custom map visuals in Power BI (TopoJSON) or Tableau (Shapefile)
------------
## Description of the dataset

Variable Name | Description |
--------------|------------------|
**Vendorid :**|A code indicating the [TPEP provider](https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page) that provided the record.<br>
**Pickup_datetime:**| The date and time when the meter was engaged.<br>
**Dropoff_datetime:**          |  The date and time when the meter was disengaged.<br>
**Passanger_count:**        | The number of passengers in the vehicle. This is a driver-entered value.<br>
**Trip_distance :**          | The elapsed trip distance in miles reported by the taximeter.<br>
**PULocationID :**| Taxi Zone in which the taximeter was engaged.<br>
**DOLocationID :** |Taxi Zone in which the taximeter was disengaged.<br>
**Ratecodeid :**             |The final [rate code](https://www1.nyc.gov/site/tlc/passengers/taxi-fare.page) in effect at the end of the trip.<br>
**Store_fwd_flg :**           |This flag indicates whether the trip record was held in vehicle memory before sending to the vendor, aka “store and forward”, because the vehicle did not have a connection to the server.<br>
**Pay_type :**                |Signifying how the passenger paid for the trip.<br>
**Fare_amount :**            | The time-and-distance fare calculated by the meter.<br>
**Surcharge :**              | $0.30 improvement surcharge,  $0.50 overnight surcharge 8pm to 6am, New York State Congestion Surcharge of $2.50.<br>
**MTA_tax :**                | $0.50 MTA tax that is automatically triggered based on the metered rate in use.<br>
**Tip_amount :**             | This field is automatically populated for credit card tips. Cash tips are not included.<br>
**Toll_amount :**            | Total amount of all tolls paid in trip.<br>
**Total_amount :**           | The total amount charged to passengers. Does not include cash tips.
--------------
## Tasks

## ETL and Data Modeling

#### The raw data has some issues, so we’ll need to make the following adjustments and assumptions to clean and prep the data:

- Let’s stick to trips that were NOT sent via “store and forward”
- I’m only interested in street-hailed trips paid by card or cash, with a standard rate
- We can remove any trips with dates before 2017 or after 2020, along with any trips with pickups or drop-offs into unknown zones
- Let’s assume any trips with no recorded passengers had 1 passenger
- If a pickup date/time is AFTER the drop-off date/time, let’s swap them
- We can remove trips lasting longer than a day, and any trips which show both a distance and fare amount of 0
- If you notice any records where the fare, taxes, and surcharges are ALL negative, please make them positive
- For any trips that have a fare amount but have a trip distance of 0, calculate the distance this way: (Fare amount — 2.5) / 2.5
- For any trips that have a trip distance but have a fare amount of 0, calculate the fare amount this way: 2.5 + (trip distance x 2.5)

##### The first issue, the data is quite big with more than 28 million records, so is very difficult for Power BI to process and will take a long time to process. So In this case,  I used SQL for the data cleaning and removal of columns I will not be using for the analysis. This made the dataset easier to load in Power BI for the analysis.

--------------
## Recommended Analysis
##### Once the data is cleaned up, For any given fiscal week, I'd like to be able to use historical data to answer the following questions:
- What’s the average fare trip we expect to collect?
- What’s the average distance traveled per trip?
- How do we expect trip volume to change, relative to last week?
- Which days of the week and times of the day will be busiest?
- What will likely be the most popular pick-up and drop-off locations?
-------------------
## Dashboard
![Screenshot (19)](https://user-images.githubusercontent.com/118670053/222131647-045c9a57-dda1-495d-8ad4-b7691134980f.png)

## Key Findings & Recommendations
- Overall average fare for each trip is`$12.30` 
- Overall average distance travelled for each trip is `2.87 miles`
###### Top 5 popular pickup locations are
- East Harleem North
- East Harleem South
- Central harleem
- Astoria
- Elmhurst
###### Top 5dropoff locations are
- East Harleem North
- Central Harleem North
- Central Harleem 
- Astoria
- East Harleem South
----------
- The busiest day of the week are the weekdays.
- The busiest hours in a day are are from 4pm to 7pm.
- More consideration should be take into account with the decrease in rides in 2020, dues to the Covid-19 pandemic.
- The Rush hour time, should be taken advantage off, via increase in mileage price, improvement surcharge .
- Price Adjustment should be considered for Weekends Rides.
