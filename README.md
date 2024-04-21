# SQLAlchemy Homework - Surf's Up!

## Step 1 - Climate Analysis and Exploration

Begin by using Python along with SQLAlchemy to perform basic climate analysis and data exploration of your climate database. Use SQLAlchemy ORM queries, Pandas, and Matplotlib for all analyses.

* Utilize the provided [starter notebook](SurfsUp/climate_starter.ipynb) and [hawaii.sqlite](SurfsUp/Resources/hawaii.sqlite) files for your climate analysis and exploration.

* Connect to your SQLite database using SQLAlchemy's `create_engine`.

* Use SQLAlchemy's `automap_base()` to reflect your tables into classes and save a reference to these classes named `Station` and `Measurement`.

* Establish a connection between Python and the database by creating an SQLAlchemy session.

* **Important:** Remember to close your session at the end of the notebook.

### Precipitation Analysis

* Begin by identifying the most recent date in the dataset.

* Retrieve the last 12 months of precipitation data by querying the preceding 12 months of data. **Note** that the date is not passed as a variable into your query.

* Select only the `date` and `prcp` values.

* Load the query results into a Pandas DataFrame and set the date column as the index.

* Sort the DataFrame values by `date`.

* Visualize the results using the DataFrame's `plot` method.

* Use Pandas to display summary statistics for the precipitation data.

### Station Analysis

* Formulate a query to compute the total number of stations available in the dataset.

* Develop a query to identify the most active stations (i.e., stations with the highest number of rows).

  * List the stations along with their observation counts in descending order.

  * Determine the station ID with the highest number of observations.

  * Using the most active station ID, calculate the minimum, maximum, and average temperature.

  * Hint: Employ functions like `func.min`, `func.max`, `func.avg`, and `func.count` within your queries.

* Create a query to retrieve the last 12 months of temperature observation data (TOBS).

  * Filter the data by the station with the highest number of observations.

  * Query the temperature observation data for the last 12 months.

  * Visualize the results as a histogram with `bins=12`.

## Step 2 - Climate App

Now that you've completed your initial analysis, design a Flask API based on the queries you developed.

* Utilize Flask to construct your routes.

### Routes

* `/`

  * Home page.

  * Display a list of available routes.

* `/api/v1.0/precipitation`

  * Convert the query results into a dictionary using `date` as the key and `prcp` as the value.

  * Return the JSON representation of the dictionary.

* `/api/v1.0/stations`

  * Return a JSON list of stations from the dataset.

* `/api/v1.0/tobs`

  * Query the dates and temperature observations of the most active station for the last year of data.

  * Return a JSON list of temperature observations (TOBS) for the previous year.

* `/api/v1.0/<start>` and `/api/v1.0/<start>/<end>`

  * Return a JSON list containing the minimum temperature (`TMIN`), average temperature (`TAVG`), and maximum temperature (`TMAX`) for a specified start date or start-end range.

  * For a start date only, calculate `TMIN`, `TAVG`, and `TMAX` for all dates greater than or equal to the start date.

  * For a start and end date, compute `TMIN`, `TAVG`, and `TMAX` for dates between the start and end date (inclusive).

## Tips

* You may need to perform joins between the `station` and `measurement` tables for certain queries.

* Use Flask's `jsonify` to convert your API data into a valid JSON response.

## Bonus: Additional Analyses

* The following analyses are optional challenges, highly recommended to attempt but not mandatory for the homework.

* Utilize the provided [temp_analysis_bonus_1_starter.ipynb](SurfsUp/temp_analysis_bonus_1_starter.ipynb) and [temp_analysis_bonus_2_starter](SurfsUp/temp_analysis_bonus_2_starter.ipynb) starter notebooks for each bonus challenge.

### Temperature Analysis I

* Investigate if there's a significant temperature difference between June and December in Hawaii.

* Use pandas for this analysis.

  * Convert the date column format from string to datetime.

  * Set the date column as the DataFrame index.

  * Drop the date column.

* Calculate the average temperatures in June and December across all stations and years in the dataset.

* Employ a t-test to determine the statistical significance of any observed temperature differences. Decide between a paired or unpaired t-test and explain your choice.

### Temperature Analysis II

* Planning a trip from August 1st to August 7th of this year? Analyze historical temperature data for insights.

* Use the `calc_temps` function to derive the minimum, average, and maximum temperatures for your chosen trip dates using corresponding dates from a prior year.

* Create a bar chart displaying the minimum, average, and maximum temperatures, with the average temperature as the bar height and the temperature range (TMAX-TMIN) as the error bar (`YERR`).

### Daily Rainfall Average

* Determine the average rainfall per weather station during matching dates from the previous year.

* Sort the results in descending order based on precipitation amount and list the station, name, latitude, longitude, and elevation.

* Compute daily normals, representing the average minimum, average, and maximum temperatures. Utilize the `daily_normals` function to calculate these normals for a specific date format (`%m-%d`) across all years.

  * Specify start and end dates for the trip.

  * Generate a list of date strings in the `%m-%d` format.

  * Compute the daily normals for each date string and append the results to a `normals` list.

* Transform the list of daily normals into a Pandas DataFrame, setting the date as the index.

* Use Pandas to plot an area plot (`stacked=False`) illustrating the daily normals.
