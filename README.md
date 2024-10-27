# The Influence of Song Length on Position in the Billboard Top 100
Billboard Top 100 songs of the week timeseries analysis

Group Members: Erin Moulton, Hank Dickerson, Varun Pavuloori

Work completed as a part of the Data Science Project course @ UVA

Dataset sourced from: https://github.com/HipsterVizNinja/random-data

# Section 1: Software and Platform section
Software used: Google Colab

Add-on Packages needed: pandas, matplotlib.pyplot, seaborn, numpy, spotipy, sklearn

Platforms: Windows, Mac

# Section 2: Project Folder Contents
Our project folder is composed of a Data folder an Output folder a Scripts folder a License and this README.md.

The Data folder contains a file showing where to find the dataset used for this project. There is also a data appendix showing statistics for all of the variables in the dataframe that we used to complete this project.

# Section 3: Instructions to replicate results
In order to reproduce the results we have found, first click the link at the top of this document.

Then click the music folder, then inside the hot-100 folder download the hot 100 csv.

Import pandas, matplotlib.pyplot, seaborn, and numpy.

Using google colab, read/load in the hot 100 csv.

Check for null values in the dataset.

Drop uneeded columns (chart_position, song_id, consecutive_weeks, previous_week, peak_position, worst_position, chart_debut, chart_url).

Exclude all songs with a chart_date prior to the year 2015.

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

