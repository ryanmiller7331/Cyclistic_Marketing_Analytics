<h1> Marketing Analytics on a Bicycle Sharing Service (via GDACC Capstone) </h1>

<h4> This business case study explores how a fictional Chicago-based bicycle-sharing service leverages historical trip data to analyze and differentiate behaviors among rider membership types, with the primary objective of boosting annual memberships. The study entails the application of advanced Excel techniques for data consolidation, cleaning, and manipulation, complemented by descriptive analysis and visualization in RStudio. </h4>

<h2> Introduction: </h2>


<h3> Scenario: </h3>

Cyclistic is an established bicycle sharing service in the Chicago area with hundreds of daily riders. With looming competition, one of the key advantages is the offering of assistive transportation options for disabled riders, accounting for 8% of sales. It also offers flexible pricing options: single-ride passes, full-day passes, and annual memberships. It's been recently determined that annual memberships are significantly more profitable that casuals (single-ride/full-day passes)

Cyclistic believes maximizing annual memberships is key to future growth, and is developing a strategy in the hopes of redirecting resources to focus less on attracting all-new users, but converting casual riders into annual membership holders.

Utilizing historical trip data, how do annual members and casual riders use Cyclistic bikes differently?

--------------

<h3> Initial Data Sources: </h3>

(Note: Cyclistic is a fictional company. The data has been made available by Motivate International Inc. under this license [https://www.divvybikes.com/data-license-agreement].)

(Disclaimer: .csv data was consolidated to 10,000 rows per sheet in the interest of preserving compute in order to avoid crashes/extended import times with tools used)

(Limitation: in the interest of data-privacy, we're prohibited from using riders’ personally identifiable information, meaning inability to connect pass purchases to credit card numbers, determining if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.)

Dataset location: https://divvy-tripdata.s3.amazonaws.com/index.html
Dataset description: Files utilizing last years' (2022) metrics loaded & prepared for analysis

<h3> Metrics: </h3>

- ride_id
- rideable_type
- started_at
- ended_at
- start_station_name
- start_station_id
- end_station_name
- end_station_id
- start_lat
- start_lng
- end_lat
- end_lng
- member_casual


<h2> Process & Analyze: Step by Step </h2>

<h3> Excel </h3> 


1. Download .csv from location (all 2022 files, separated by month, 12 files.)

2. Import .csv's into Excel. 

3. Considering all column metrics are the same across each month, I began to combine each sheet into one for cleaning & manipulation purposes in Excel. (120,000 rows)

4. Once my sheets were combined, I began my cleaning process:
	- I checked for duplicates in the "ride_id" column, as these ought to have unique values. 
	- Next, I applied filters to "rideable_type", "member_casual" as these should have expected unique values in the single digits
	- While checking for missing data, I noticed that quite a few rows had missing start stations, end stations, or a combination of the two. This might be useful in identifying riding habits of casual vs. annual membership riders (i.e., do annual members typically start & end at stations?).  

5. Next, I began manipulating this data to in order to analyze new metrics: 
	- I added "ride_length" by subtracting "started_at" from "ended_at"
	- Added "day_of_week" column
	- Added "month" column
	- Added "time_of_use" column
	- Finally, calculated "distance_in_mi" using the Halversine formula:
		- created "helper columns" to find the radians of each coordinate (=I2 * PI() / 180 , =K2 * PI() / 180 , =J2 * PI() / 180 , =L2 * PI() / 180)
		- Next, used the Halversine formula to calculate distance in miles [=3958.8 * ACOS(COS(R2) * COS(S2) * COS(T2 - U2) + SIN(R2) * SIN(S2))]
		- Then formatted the distance to 2 decimal places. 
		- Finally, I copied the final values only, and deleted the helper columns 
		--Disclaimer, I had around 8,000 produce zero, but after checking multiple values I decided to keep my formula but notate.

6. After cleaning & manipulation, data was exported to .csv:

	"2022.Bikeshare.Data_totals.csv"


<h3> Posit (RStudio)</h3>

After reviewing and brainstorming the original dataset, then manipulating to have actionable columns within Excel I began developing questions that I could answer with this dataset; How are Casual vs. Membership riders different?:



1. Number of rides for users overall; casual vs. member? 
	- By day of the week?
	- By month?

2. Busiest time/total rides per hour of use by user type?

3. What are the preferred bike types of each rider type?

4. What are the top 3 start stations by user?
	- Top 3 end stations? 

5. Average ride length of each rider type?

6. Average distance by user type?

7. Average speed by user?


<h3> From here on out, check out the additional contents of this repository for the following: </h3>

- R scripts for cleaning, manipulating & analysis.

- R scripts for visualizations used in the final presentation.

- Final presentation, with summarized findings & action items. 



Thanks for reading!
 
Ryan
