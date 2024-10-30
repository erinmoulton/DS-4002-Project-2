# The Influence of Song Length on Position in the Billboard Top 100
Billboard Top 100 songs of the week timeseries analysis

Group Members: Erin Moulton, Hank Dickerson, Varun Pavuloori

Work completed as a part of the Data Science Project course @ UVA

Dataset sourced from: https://github.com/HipsterVizNinja/random-data

# Section 1: Software and Platform section
Software used: Google Colab

Add-on Packages needed: pandas, matplotlib.pyplot, seaborn, numpy, spotipy, sklearn <br>
API's used: Spotify Web API, Last.fm Music Discovery API

Platforms: Windows, Mac

# Section 2: Project Folder Contents
Our project folder is composed of a Data folder an Output folder a Scripts folder a License and this README.md.

The Data folder contains a file showing where to find the dataset used for this project. There is also a data appendix showing statistics for all of the variables in the dataframe that we used to complete this project.

The Output folder contains various graphs and images. There is a graph depicting the average length of songs on the top 100 across multiple years, a forecast graph that depicts the length of songs from our data and forecasts what the length of songs could be in future years. There is also a table showing outlier songs that are over six minutes long.

The Scripts folder includes a file of our source code used to obtain all of the results we observed throughout this project.

The License file is a simple copyright license.

# Section 3: Instructions to replicate results
In order to reproduce the results we have found, first click the link at the top of this document.

Then click the music folder, then inside the hot-100 folder download the hot 100 csv.

Import pandas, matplotlib.pyplot, seaborn, and numpy.

Using google colab, read/load in the hot 100 csv.

Check for null values in the dataset.

Drop uneeded columns (chart_position, song_id, consecutive_weeks, previous_week, peak_position, worst_position, chart_debut, chart_url).

Exclude all songs with a chart_date prior to the year 2005.

Define a function with artists_string as the sole input.

Within the function get rid of any featured or secondary artists as we only want to primary artist.

Have this function return the new artist string.

Apply this function to the performer variable of the dataset.

We now set up for the use of Spotify API.

Install then import spotipy.

From spotipy.oauth2 import SpotifyClientCredentials

To use this API you must have or create a spotify account. (The free version works for this)

Set a variable name client_id equal to your spotify API client id

Set a variable name client_secret equal to your spotify API client secret

Create an instance of SpotifyClientCredentials using your client id and secret.

Create a spotify object (sp) that uses your credentials for authentication.

Now we set up for use of the LastFM API.

Sign up for use of the LastFM API.

Install and import pylast.

Set variable names equal to your API key, API secret, Username, and Password.

Set a variable named network equal to pylast.LastFMNetwork with your credentials as the inputs for pylast.LastFMNetwork

Define a function get_song_length that takes in two paramaters (artist, song_title)

Use a try/except block within the function

With the try portion, use the search method in the spotify object (sp) and have it take in the artist and the song title as inputs.

Have the function return the length of the song in milliseconds.

With the except portion, have the function return a string that reads "error retrieving song length."

Create a unique dataframe by grouping the original data frame by song and performer.

Use the agregate function (.agg) to find the maximum instance, minimum chart_date (earliest), and maximum time_on_chart for each unique song

Then reset the index of the resulting dataframe to clean it up.

Initialize a new column in the unique dataframe as a placeholder for the song lengths in milliseconds.

Create a for loop that will iterate over each row in the unique dataframe.

Extract the song title and the artist name.

Call the previously made get_song_length function to get each song length in milliseconds

Update the new column we made to have each unique songs lenght.

Test for null values in the song length column.

Create a variable null_song_lengths that is equal to each song with a null value for the song length within the unique dataframe.

Define a function with one parameter of artist_string.

This function will further clean the performers of the song to not include featured or secondary artists.

If any of the following are present in the artist_string (X, x, With, Featuring, Feauring, :, feat., or Feat.) replace them and anything that follows them with a blank space.

Apply this function to the unique dataframe.

Create and run the same for loop mentioned above on this dataframe.

Define a function get_song_length_lastfm with two parameters (artist, song_title).

Use a try/except block for this function.

In the try portion, call the get_track method from the network object (an instance of the LastFM API client) 

Use the get_duration method on the dataframe to get the duration of all the songs in milliseconds.

If a duration is found return it, if not return NONE.

For the except portion, if any error occurs print ("error retrieving song lenght") and return none.

Create a for loop that iterates over each row of the null_song_lengths variable

Extract the artist and the song title from the current row

If the Value for the song length is still None in the unique dataframe, apply the get_song_length_lastfm function to the dataframe.

Append these song lengths to the unique dataframe.

Check for null values in the song_length variable.

Use null_song_lenghts.head(36) to find out which songs are still null.

Create a dictionary and manually input all 36 of these songs lengths in milliseconds.

Update the unique dataframe to include the values from the dictionary you just made.

Using the song_length column create a new column in the unique dataframe that converts the song length in miliseconds to minutes.

Save this unique dataframe as a CSV to ensure the data is secure.

From sklearn.preprocessing import LabelEncoder, StandardScaler.

From sklearn.model_selection import train_test_split.

From sklearn.metrics import mean_squared_error, r2_score.

Using pandas convert the chart_date column from the unique datafram from a string into a datetime object.

Create three new columns (chart_year, chart_month, chart_day) by extracting the year, month, and day from the chart_date object.

Use the LabelEncoder and the fit_transform methods to transform the song, performer, and instance columns from categorical to numerical format.

Drop rows with any missing values.

Create lag features by creating two new columns lag_1 and lag_7.

lag_1 will contain the values of time_on_chart shifted by 1.

lag_7 will contain the values of time_on_chart shifted by 7.

Create a column rolling_mean_7 which contains the average value of time_on_chart over the last 7 entries.

Create a column rolling_std_7 which contains the standard deviation of time_on_chart over the last 7 entries.

Remove any rows with null values for these columns.

Analysis using prophet.

Install prophet.

Convert the chart_date column in the unique dataframe to a datetime format.

Create a new dataframe prophet_df that includes only the chart_date and song_length_mins column from the unique dataframe.

Rename the column chart_date to ds and song_length_mins to y.

Ensure that ds is in datetime format.

From prophet import Prophet.

Initialize a prophet model that expects a changpoint on January first 2016, with a change_point_prior_scale of 0.0001.

Fit the model to prophet_df.

Create a dataframe to hold predictions for the next 120 months with a frequency of every month.

Predict future values using the dataframe just created with model.predict.

Use the plot method to visualize the forecast with the x-axis being date and the y-axis being song length.

Display the forecasted values (ds, yhat, yhat_lower, yhat_upper).

Initialize and fit a new prophet model on prophet_df.

Create a dataframe to hold predictions for the next 60 months with a frequency of every month.

Predict future values using the dataframe just created with model.predict.

Use the plot method to visualize the forecast with the x-axis being date and the y-axis being song length.

Display the forecasted values (ds, yhat, yhat_lower, yhat_upper).

From scipy import stats.

Create a series titled before_2016 which contains all song lengths from before January first 2016.

Create a series titled after_2016 which contains all song lengths on or after January first 2016.

Conduct an independent two sample t-test with the the two seriest just created.

print the t-statistic and the p-value.

# References

[1] Facebook. (2019). Prophet. Prophet. https://facebook.github.io/prophet/

[2] HipsterVizNinja. (2021). GitHub - HipsterVizNinja/random-data: Just a place to put all my random data sources. GitHub. https://github.com/HipsterVizNinja/random-data

[3] Wilson, S. (2017, March 31). Streaming overtakes downloads and physical sales for first time ever in bumper year for music industry. Fact Magazine. https://www.factmag.com/2017/03/31/streaming-overtakes-downloads-physical-sales-2016/

[4] “API Docs. (n.d.). Last.fm. https://www.last.fm/api

[5] Spotify. (n.d.). Web API | Spotify for Developers. Developer.spotify.com. https://developer.spotify.com/documentation/web-api

[6] A. Taylor, and R. J. McAdams, "Prophet: Forecasting at Scale," in Proceedings of the 2018 IEEE International Conference on Big Data (Big Data), 2018, pp. 2159-2166.
