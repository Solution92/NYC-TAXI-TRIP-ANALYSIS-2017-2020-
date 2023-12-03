# NYC TAXI TRIP ANALYSIS (2017–2020)

## Table of Content

- [Business Objective](#business-objective)
- [Data Source](#data-source)
- [Tools Used](#tools-used)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Data Transformation and Cleaning](#data-transformation-and-cleaning)
- [Report and Visualization](#report-and-visualization)
- [Insights and Visualization](#insights-and-visualization)
- [The Dashboard](#the-dashboard)
- [Summary and Recommendation](#summary-and-recommendation)


### Business Objective: 

Below are the main purposes of this Analysis:

What’s the average number of trips we can expect this week, What’s the average fare per trip we expect to collect, What’s the average distance traveled per trip, How do we expect trip volume to change, relative to last week, Which days of the week and times of the day will be busiest, and What will likely be the most popular pick-up and drop-off locations?

### Data Source:

The dataset was provided by the Company in CSV file format.

### Tools Used

Power BI — Data Cleaning, Transformation, Analysis, and Creating Reports.

### Data Cleaning and Preparation

This dataset contains six tables in CSV format, along with a geospatial map in Topojson and Shapefile formats. The four Taxi Trips tables contain a total of 28 million Green Taxi trips in New York City from 2017 to 2020. Each record represents one trip, with fields containing details about the pick-up/drop-off times and locations, distances, fares, passengers, and more.

There is also another table -The 454 Calendar table which contains a fiscal calendar (2017–2020) used by the Taxi & Limousine Commission, with fields containing the date and fiscal year, quarter, month, and week. The Taxi Zones table contains information about 265 zone locations in New York City, including the location id, borough, and service zone.

The Taxi Zones Map files contain a map of New York City with divisions for the 265 locations that can be used to create custom map visuals in Power BI.

### Data Transformation and Cleaning

Merging and Appending, the first thing was to load the four Taxi Trips tables into the power query editor and append all as they all have an equal number of columns to increase rows. Secondly, I Merged the Taxi Zones Map files with the Appended tables using location as the primary key.

#### Conditional Columns

- Trip Type: I further used the conditional column to transform the trip_type column as 1= Street-hail; 2= Dispatch, and named it Trip Type1.

- Payment Type: I also used a conditional column to transform the payment type column as 1= Credit card; 2= Cash; 3= No charge; 4= Dispute; 5= Unknown; 6= Voided trip, as given in the instructions, and renamed it as Payment Type 1.

- Clean: Tolls Amount and improvement_surcharge Column has a series of ‘null’ values which were replaced with ‘0’. I also replaced -0.3 with 0.3 according to the instructions.

#### Total Amount, Trip Amount, and Fare Amount Column

Expanded these columns to see the number of negative values then transformed them to positive values — according to instruction in the pdf.

#### Transforming Negative to Positive Values

First, highlight the column you want to transform, go to the ‘Transform’ pane, then click on the drop-down arrow on “Scientific”, then click on “Absolute Value”.

#### Transform RatecodeID Column

Use a Conditional Column to transform the RatecodeID as 1= Standard rate; 2= JFK; 3= Newark; 4= Nassau or Westchester; 5= Negotiated fare; 6= Group ride, according to the data dictionary.

#### Transform VendorID Column

Used Conditional Column to transform the VendorID as 1 = Creative Mobile Technologies, LLC; 2= Verifone Inc. according to the data dictionary

#### Store_and_fwd_flag Column

Used Conditional Column to transform the Store_and_fwd_flag Column as Y= store and forward trip; N= not a store and forward trip, according to the data dictionary.

#### Trip_distance Column

For any trips that have a fare amount but have a trip distance of 0, calculate the distance this way: (Fare amount — 2.5) / 2.5

From the table Fare Amount = 5

#### Fare_amount Column

For any trips that have a trip distance but have a fare amount of 0, calculate the fare amount this way: 2.5 + (trip distance x 2.5)

From the table trip distance =0.67

So, fare amount = 2.5 + (0.67 x 2.5) = 4.175 ==4.2. In the fare amount column, replace ‘0’ with ‘4.2’ as the fare amount.


### Report and Visualization

- KPI
  - Total Fare Amount = SUM(Taxi_trip[fare_amount]) = 374.5M
  - Total Trips = SUM(Taxi_trip[passenger_count]) = 36.85M
  - AVG Fare Amount = CALCULATE(AVERAGE(Taxi_trip[fare_amount])) = $13.22
  - AVG Distance = CALCULATE(AVERAGE(Taxi_trip[trip_distance])) = 3.87KM
  - Total Passengers = SUM(Taxi_trip[passenger_count]) = 37M

### Insights/Visualization

- AVG Number of Trips by Week
- AVG Fare Amount by Week
- AVG Distance by Week
- Total Trips by Service Zones
- Pickup by Location
- Total Trip by Week

### The Dashboard

![Screenshot_121](https://github.com/Solution92/NYC-TAXI-TRIP-ANALYSIS-2017-2020-/assets/144762124/962e9356-7a85-45fc-b203-599d64648fbb)

### Summary and Recommendation

The question has been clearly answered by the dashboard. The average number of trips per week is 16 while the average weekly fare amounts to $13. The average distance by week is between 3.50km to 4.39km ranging from Friday to Tuesday in the chat.

Furthermore, the Total trips by service Zone is Boro Zone, 31.27M representing 84.8% with EWR, 5.58M which is 15.14% of the service Zones.

Meanwhile, the busiest day of the week is seen to be on Saturday and the most popular pick-up location is Jamaica Bay.

Gracias, Gracias.























