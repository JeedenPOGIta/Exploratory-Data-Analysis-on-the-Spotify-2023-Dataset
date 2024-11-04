# Exploratory-Data-Analysis-on-the-Spotify-2023-Dataset

<div align="justify">

Welcome! This repository focuses on the use of Pandas, Matplot, and Seaborn for data wrangling and data visualization using Python.

### [OBJECTIVES]

The task aims to analyze, visualize, and interpret the given data to extract meaningful insights. The task also serves as 
a refresher of how python aids in data wrangling and visualization. <br>

___________________________

### [DATA EXPLORATION AND CLEANING]

This section of the repository focuses on the exploration and cleaning of the dataset before performing functions that
python has to offer. <br>

Before starting the exploration of the dataset, I first imported all the libraries that I think I should and would be using:
Pandas, Matplot, and Seaborn. <br><br>
```
#to import pandas
import pandas as pd
```
```
#to import seaborn
import seaborn as sns
```
```
#to import matplot
import matplotlib.pyplot as plt
```
<br>

Then I loaded the dataset into the python code so I can access and refine the data however I see fit. If somehow you are intrested 
in accessing the full raw dataset that was used in this mini project, you can find it in this link:

https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023 <br>

Just press download and you should be ready to use the dataset however you like! Kaggle is a website that contains many more
raw datasets that can be explored and used for practice in data wrangling and visualization such as this. Credits to them for
providing us with a platform to find these different datasets. <br><br>

Going back to our data exploration, I loaded the dataset into the code so that I can explore it within the code using different
python functions. 

```
df = pd.read_csv('spotify-2023.csv') 
```
<br>

However, I first ran into an error while trying to import the dataset into the code. I kept encountering the 
"UTF-8 encoding error" which meant that the file is not in UTF-8 format. I surfed around the internet to find
a solution and found one provided by Saturn Cloud. It told me to check the encoding format my file is in by
using a text editor like notepad++ and check the "Encoding" menu. After, I was able to successfully load the 
file into the code by using the following syntax:

```
df = pd.read_csv('spotify-2023.csv', encoding='ISO-8859-1') #encoding fixes the thingy format
```
<br>

The first thing that crossed my mind after looking at how large the dataset is, is to check for missing values 
in the data that might hinder some of the functions of python to work properly. I managed to check for these 
missing values using the .isnull() function. 
<br>

```
#check for missing values. True = Missing
missing = df.isnull()
```
<br>

I manage to see the first few rows of the data and seemed like there was nothing wrong with them. However, with
just this function alone, I still need to check for "True" or missing values in the hundreds of indexes in the dataset
so, I opted for a summation of missing values in each column using the .sum() function with the previous .isnull()
function. <br>

```
#check for total number of missing values
missing_sum = df.isnull().sum()
```
<br>
OUTPUT:

```
track_name               0
artist(s)_name           0
artist_count             0
released_year            0
released_month           0
released_day             0
in_spotify_playlists     0
in_spotify_charts        0
streams                  0
in_apple_playlists       0
in_apple_charts          0
in_deezer_playlists      0
in_deezer_charts         0
in_shazam_charts        50
bpm                      0
key                     95
mode                     0
danceability_%           0
valence_%                0
energy_%                 0
acousticness_%           0
instrumentalness_%       0
liveness_%               0
speechiness_%            0
dtype: int64
```
<br>

Tada! By using the .sum() function I was able to locate the total number of missing values in each column.
The results then told me that there are 50 missing values in shazam_charts and 95 in the key columns respectively.

<br>

Now that I know there are missing values in the dataset, It's time for me to remove them. I achieved this using the 
.dropna() function for both the rows and columns of the dataframe. 

```
#Remove missing values
df.dropna() #for rows
df.dropna(axis=1) #for columns
```
<br>
___________________________________________________________________

### [OVERVIEW OF THE DATASET]

This section of the repository provides a basic information regarding the dataset. <br>

To start, I checked the scale of the dataset by checking the number of rows and columns I am dealing with.
This was done using the .shape function of pandas:

```
#No. of rows and columns
df.shape
```
<br>

OUTPUT:
```
(953, 24)
```
The output then suggests that there are a total of 953 rows and 24 columns in the entire dataset. <br>

After this, I checked the data types of each column so that I would know which columns can be explored right away 
using the pandas functions and which columns needed conversion before usage. I used the .dtypes function to do so
and the output is as follows:

```
track_name               object
artist(s)_name           object
artist_count              int64
released_year             int64
released_month            int64
released_day              int64
in_spotify_playlists      int64
in_spotify_charts         int64
streams                  object
in_apple_playlists        int64
in_apple_charts           int64
in_deezer_playlists      object
in_deezer_charts          int64
in_shazam_charts         object
bpm                       int64
key                      object
mode                     object
danceability_%            int64
valence_%                 int64
energy_%                  int64
acousticness_%            int64
instrumentalness_%        int64
liveness_%                int64
speechiness_%             int64
dtype: object
```
___________________________________________________________________

### [BASIC DESCRIPTIVE STATISTICS]
This section of the repository focuses on finding the mean, median, and standard deviation of the "streams" column 
and the distribution of artists and the years of releases. This section also aims to find out if there are any
noticeable outliers in the data. <br><br>

I first looked for the mean, median, and standard deviation of the "streams" column, which was done using the following syntax:

```
#mean of streams column
stream_mean = df['streams'].mean()

#median of streams column
stream_median = df['streams'].median()

#standard deviation of streams column
stream_sd = df['streams'].std()
```
<br>

Seeing that the output has a lot of decimals in it, I decided to limit the number of decimals to only two (2) decimals for each 
value to make it more pleasing to the eyes. I revised the code and used the following syntax to do so:

```
#mean of streams column
stream_mean = df['streams'].mean().round(2)

#median of streams column
stream_median = df['streams'].median()
stream_median_rounded = round(stream_median, 2) #round to 2 decimals only 

#standard deviation of streams column
stream_sd = df['streams'].std()
stream_sd_rounded = round(stream_sd, 2) #round to 2 decimals only 
```
<br>

OUTPUT:

```
The mean number of streams:
 514137424.94 

The median in streams:
 290530915.0

The standard deviation of streams:
 566856949.04 
```
<br>

Up next, I was tasked to find out whether the distribution of the artist_counts and the song's year of release had any noticeable trends
or outliers. For this section, I decided to use boxplots so that I could notice any outliers easily. <br><br>

OUTPUT:
[INSERT IMAGE HERE]

<br>

As the graph suggests, there is a noticeable trend wherein the artist counts nearing the year 2000s had more artists deciding to collaborate with another
in comparison to the years before it, with a few exceptions/outliers. <br><br>

### [TOP PERFORMERS]

This section of the repository focuses on exploring the top five (5) most streamed tracks and the top 5 artists who appear the most in the dataset. <br>

To find out, I used the .nlargest() function with the "streams" column. 

```
#top 5 songs! Based on the number of streams 
top_songs = df.nlargest(5, 'streams')
```
<br>

This outputs a table with the details of the top 5 performers and their songs however, there are some data that could be removed to get a clearer view of what is being asked, the top 5 artists.

UNCLEANED OUTPUT:
|    | track_name                                    | artist(s)_name        |   artist_count |   released_year |   released_month |   released_day |   in_spotify_playlists |   in_spotify_charts |     streams |   in_apple_playlists |   in_apple_charts |   in_deezer_playlists |   in_deezer_charts |   in_shazam_charts |   bpm | key   | mode   |   danceability_% |   valence_% |   energy_% |   acousticness_% |   instrumentalness_% |   liveness_% |   speechiness_% |
|---:|:----------------------------------------------|:----------------------|---------------:|----------------:|-----------------:|---------------:|-----------------------:|--------------------:|------------:|---------------------:|------------------:|----------------------:|-------------------:|-------------------:|------:|:------|:-------|-----------------:|------------:|-----------:|-----------------:|---------------------:|-------------:|----------------:|
|  0 | Blinding Lights                               | The Weeknd            |              1 |            2019 |               11 |             29 |                  43899 |                  69 | 3.7039e+09  |                  672 |               199 |                   nan |                 20 |                nan |   171 | C#    | Major  |               50 |          38 |         80 |                0 |                    0 |            9 |               7 |
|  1 | Shape of You                                  | Ed Sheeran            |              1 |            2017 |                1 |              6 |                  32181 |                  10 | 3.56254e+09 |                   33 |                 0 |                   nan |                  7 |                  0 |    96 | C#    | Minor  |               83 |          93 |         65 |               58 |                    0 |            9 |               8 |
|  2 | Someone You Loved                             | Lewis Capaldi         |              1 |            2018 |               11 |              8 |                  17836 |                  53 | 2.88724e+09 |                  440 |               125 |                   nan |                  0 |                nan |   110 | C#    | Major  |               50 |          45 |         41 |               75 |                    0 |           11 |               3 |
|  3 | Dance Monkey                                  | Tones and I           |              1 |            2019 |                5 |             10 |                  24529 |                   0 | 2.86479e+09 |                  533 |               167 |                   nan |                  6 |                nan |    98 | F#    | Minor  |               82 |          54 |         59 |               69 |                    0 |           18 |              10 |
|  4 | Sunflower - Spider-Man: Into the Spider-Verse | Post Malone, Swae Lee |              2 |            2018 |               10 |              9 |                  24094 |                  78 | 2.8081e+09  |                  372 |               117 |                   843 |                  4 |                 69 |    90 | D     | Major  |               76 |          91 |         50 |               54 |                    0 |            7 |               5 |


<br>
I decided to remove a few columns to get a clearer view using the following syntax:

```
#clean the table appearance - display only what is relevant
top_songs_clean = top_songs[['track_name','artist(s)_name', 'released_year', 'streams']].reset_index(drop = True) 
top_songs_clean.index = range(1, 6) #reassigns indexes from 1 to 5
```

CLEANED OUTPUT:
|    | track_name                                    | artist(s)_name        |   released_year |     streams |
|---:|:----------------------------------------------|:----------------------|----------------:|------------:|
|  1 | Blinding Lights                               | The Weeknd            |            2019 | 3.7039e+09  |
|  2 | Shape of You                                  | Ed Sheeran            |            2017 | 3.56254e+09 |
|  3 | Someone You Loved                             | Lewis Capaldi         |            2018 | 2.88724e+09 |
|  4 | Dance Monkey                                  | Tones and I           |            2019 | 2.86479e+09 |
|  5 | Sunflower - Spider-Man: Into the Spider-Verse | Post Malone, Swae Lee |            2018 | 2.8081e+09  |

<br>
To find out the artists who appear the most frequently in the dataset, I used the .value_counts() function together with the .head()
function to display the 5 artists who have the most tracks in the dataset.

```
most_released = df['artist(s)_name'].value_counts().head()
```

OUTPUT:
```
The artists who appear most on spotify in 2023 are: 

 artist(s)_name
Taylor Swift    34
The Weeknd      22
Bad Bunny       19
SZA             19
Harry Styles    17
Name: count, dtype: int64
```
The output suggests that Taylor Swift has released a song most frequently in the years leading up to 2023 with 34 appearances. <br>
___________________________________________________________________
### [TEMPORAL TRENDS]

This section focuses on the analysis of the trends in the number of tracks released over time and exploring noticeable patterns. <br>

To achieve this, I first counted the number of tracks released per year using the .value_counts() function together with the sort_index to 
quickly sort them.

```
#count the number of released tracks
track_numbers = df['released_year'].value_counts().sort_index()
```

Right after, I used a line graph, which I think is the best form of graph to represent a trend over time. The following syntax was used to
form one (1) of the two (2) graphs:

```
#number of no. of tracks vs. year
plt.plot(track_numbers.index,track_numbers.values, marker = 'o', color = 'tab:green')
plt.title('Number of Tracks Released Across the Years') # title

plt.xlabel('Year of Release') #x values
plt.ylabel('Number of Tracks') #y values

plt.xticks(track_numbers.index) #xticks
plt.legend(['Number of Tracks']) #legend
```
OUTPUT:
[INSERT IMAGE] <br>

Analyze the trends in the number of tracks released over time. Plot the number of tracks released per year.

The graph suggests that there was a big spike in the number of songs released in the year 2020. Going back to this year, the trend makes 
sense because this was the start of the COVID-19 pandemic years, and everyone is stuck in their homes in fear of the virus. Hence, a lot of artists 
had more time to release their creativity through songs as a way of relieving their boredom and communicating with the rest of the world other than
social media. <br>

The next graph shows the number of releases per month. Just like the first graph, I started by counting the number of songs released in the "released_month" column using the .value_counts() function. <br>

```
#count the number of released tracks by month
track_numbers_monthly = df['released_month'].value_counts().sort_index()
```
<br>

And I also used the line graph to display the data so that it is much easier to notice a trend if there is one. The following syntax was used:

```
#number of no. of tracks vs. year
plt.plot(track_numbers_monthly.index,track_numbers_monthly.values, marker = 'o', color = 'tab:green')
plt.title('Number of Tracks Released Across the Months') # title

plt.xlabel('Month of Release') #x values
plt.ylabel('Number of Tracks') #y values

plt.xticks(track_numbers_monthly.index)

plt.legend(['Number of Tracks']) #legend
```
<br>
OUTPUT:<br>
[INSERT IMAGE]

<br><br>
The number of tracks released per month did not necessarily follow a noticeable pattern. As seen in the graph, the trend has an unstable pattern in which there is no guarantee that there will be a continuous growth or continuous decline in the number of songs released per month. The graph also implies that January has the most song releases so far.

___________________________________________________________________

### [GENRE AND MUSIC CHARACTERISTICS]

This section of the repository focuses on the correlation between streams and musical attributes. <br><br>

First, I was tasked to examine the correlation between streams and musical attributes like bpm, danceability_%, and energy_%. When it comes to correlations, the scatterplot always comes to mind. Hence, I opted for a scatterplot to display what was being asked. The syntax of the graph is as follows: <br>

```
#plot a figure 20x12 inches
plt.figure(figsize=(20,12))

#title
plt.title('Correlation Between Streams and Musical Attributes') 

#streams vs musical attributes
plt.scatter(df['bpm'],df['streams'], color = 'purple')
plt.scatter(df['danceability_%'],df['streams'], color = 'red')
plt.scatter(df['energy_%'],df['streams'], color = 'green')

plt.ylabel('No. of Streams') #x values
plt.xlabel('Musical Attributes') #y values

#legends 
plt.legend(['bpm','danceability_%','energy_%'])
```
<br>

OUTPUT:
[INSERT IMAGE] <br>

The graph suggests that the danceabilty_% and energy_% influence streams the most. As seen in the graph, danceability_% and energy_% range from 50 to close to 100 and are the most dense parts. This means that this range of musical attributes had more impact on the number of streams in comparison to the bpm_%. <br>

The next task is to find out if there is a correlation between danceability_% and energy_%. To do this, I used another scatterplot to determine the correlation between the two. I used the following syntax: 

```
#plot a figure 20x10 inches
plt.figure(figsize=(20,10))

#title
plt.title('Danceability vs. Energy') 

#danceability vs. energy
plt.scatter(df['danceability_%'],df['energy_%'], color = 'purple')

plt.xlabel('Danceability%') #x values
plt.ylabel('Energy%') #y values
```
<br>

OUTPUT: <br>
[INSERT IMAGE] <br>

The plots are scattered equally across the graph. Hence, the graph suggests that there is no correlation between danceability and energy.<br><br>

I was also tasked to find out the correlation between valence_% and acousticness_%. Just like the last graph, I also used a scatterplot to display their correlation. The syntax is pretty much the same:

```
#plot a figure 20x10 inches
plt.figure(figsize=(20,10))

#title
plt.title('Valence vs. Acousticness') # title

#valence vs. acousticness
plt.scatter(df['valence_%'],df['acousticness_%'], color = 'lightgreen')

plt.xlabel('Valence%') #x values
plt.ylabel('Acousticness%') #y values
```
<br>

OUTPUT: <br>
[INSERT IMAGE]<br>

Just like the previous graph, the graph for valence_% and acousticness_% also shows no correlation. This was observed since the plots show randomness. <br>
___________________________________________________________________

### [PLATFORM POPULARITY]

This section of the repository focuses on how the numbers of tracks in spotify_playlists, deezer_playlists, and apple_playlists compare. To find out, I first got the total number of tracks on each platform. I used the .sum() function on each of the columns like this: <br>

```
#get the number of tracks in each platform
in_spotify_playlists_sum = df['in_spotify_playlists'].sum()
in_deezer_playlists_sum = df['in_deezer_playlists'].sum()
in_apple_playlists_sum = df['in_apple_playlists'].sum()
```
<br>

OUTPUT: <br>
```
The number of tracks in each platform are:
Spotify: 4955719
Deezer: 95913.0
Apple: 64625 
```
The results revealed that the leading platform is Spotify, with 4,955,719 tracks in playlists; followed by Deezer with 95,913 tracks, and Apple with 64,625 tracks. I wanted to show how these three compare in a much cleaner way. Hence, I created a bar graph comparing the number of tracks in a much more concise way. I achieved this by creating a data frame for the existing data and then creating a graph for it. The syntax I used is as follows: 

```
#create a dictionary to turn into a dataframe
tracks = {'Spotify': in_spotify_playlists_sum, 'Deezer': in_deezer_playlists_sum, 'Apple': in_apple_playlists_sum}
#create a dataframe from a dictionary
tracks_df = pd.DataFrame.from_dict(tracks, orient = 'index', columns = ['Total Number of Tracks'])

#plot
plt.figure(figsize = (20,10)) #size ni fig
tracks_df.plot(kind = 'bar', color = 'purple') #bar graph
plt.title('Number of Tracks by Platform')

plt.xlabel('Platform') #label of x
plt.ylabel('Number of Tracks') #label of y
```
<br>

OUTPUT: <br>
[INSERT IMAGE HERE] <br>

In this way, we can clearly see what platform is the most favored. <br><br>

Onto the next task, for this one, I intend to find out which platform seems to favor the most popular tracks. I opted to use a scatter plot for this one
and compare each of the platforms and their corresponding number of streams to see which platform favors the most popular tracks. So, I created a plot with three subplots displaying each of the platforms and their correlation with their number of streams. I did this using the following syntax:

```
#plot with 3 subplots
fig, ax = plt.subplots(1,3, figsize=(20, 10))

#first plot details
ax[0].scatter(df['in_spotify_playlists'],df['streams'], color = 'lightgreen')
ax[0].set_title('Streams vs. Total in_spotify_playlist')
ax[0].set_xlabel('in_spotify_playlist')
ax[0].set_ylabel('Streams')

#second plot details
ax[1].scatter(df['in_deezer_playlists'],df['streams'], color = 'purple')
ax[1].set_title('Streams vs.Total in_deezer_playlist')
ax[1].set_xlabel('in_deezer_playlist')
ax[1].set_ylabel('Streams')

#third plot details
ax[2].scatter(df['in_apple_playlists'],df['streams'], color = 'lightblue')
ax[2].set_title('Streams vs. Total in_apple_playlist')
ax[2].set_xlabel('in_apple_playlist')
ax[2].set_ylabel('Streams')

#title
plt.suptitle('Streams Vs. In_Playlist')
```
<br>

OUTPUT: <br>
[INSERT IMAGE HERE] <br>

The graphs suggest that Spotify favors the most popular tracks as it has a positive correlation with the number of streams. Hence, this suggests that most of the streams are on Spotify and is the most favored out of all the platforms. <br>

___________________________________________________________________
### [ADVANCED ANALYSIS]

This section of the repository focuses on identifying patterns among tracks with the same key or mode. To find out, I used two types of graphs: a line and a bar graph. I used these graphs to easily identify a pattern if there is one. <br><br>

First, I used a line graph to see the trend in the different keys and their corresponding number of streams. I achieved this using the following syntax:

```
#first plot details
ax[0].plot(key_avg_streams['key'],key_avg_streams['streams'], color = 'pink') #bar plot
ax[0].set_title('Keys Vs. Streams')
ax[0].set_xlabel('Keys')
ax[0].set_ylabel('Streams')
```
<br>

OUTPUT: <br>
[INSERT IMAGE HERE] <br>

The graph suggests that there is an increase in the number of streams from the A key up until the C# key. The keys after C# experienced a slow decline in their number of streams. However, it is also worth noting that the notes with sharps (#) are higher than their original counterparts. For instance, tracks on the A# key have a significantly higher number of streams than tracks on the A key only. <br><br>

For the modes, I opted to use a bar graph instead of a line graph since it only has two modes to compare with one another. To clearly see their differences, I thought that the bar graph would best represent this. I used the following syntax to create my bar graph:

```
#second plot details
ax[1].bar(mode_avg_streams['mode'],mode_avg_streams['streams'], color = 'lightblue') #bar plot parin
ax[1].set_title('Mode Vs. Streams')
ax[1].set_xlabel('Mode')
ax[1].set_ylabel('Streams')
```
<br>

OUTPUT:<br>
[INSERT IMAGE HERE]<br>

And there we go; the output suggests that the tracks in the major mode have a higher number of streams than those in the minor mode. <br><br>

For this last part, I was tasked to perform an analysis comparing the most frequently appearing artists on playlists and charts. For this, I first created a new data frame, which only included the necessary details for my analysis. These data include the sum of their appearances in both playlists and charts on each of the platforms. I used the following syntax to do so:

```
# create a dataframe with artist names, in playlists, and in charts
ayokona = df[['artist(s)_name', 
            'in_spotify_playlists', 'in_deezer_playlists', 'in_apple_playlists',
            'in_spotify_charts','in_deezer_charts','in_apple_charts']].copy()

#add new column - total appearances in playlists
ayokona['Total Playlist Apperances'] = ayokona[['in_spotify_playlists', 'in_deezer_playlists', 'in_apple_playlists']].sum(axis = 1)

#add new column - total appearances in charts
ayokona['Total Chart Apperances'] = ayokona[['in_spotify_charts', 'in_deezer_charts', 'in_apple_charts']].sum(axis = 1)

#add new column - total appearances in playlists and charts
ayokona ['Total Appearances'] = ayokona[['Total Playlist Apperances','Total Chart Apperances']].sum(axis = 1)

#group by artists then get total appearances
grouping = ayokona.groupby('artist(s)_name')['Total Appearances'].sum().reset_index()
#sort values by descending order
groupingfinal = grouping.sort_values(by = 'Total Appearances', ascending = False)

#stores the top 10 values
final10 = groupingfinal.head(10)
#indexes are from 1 to 10 
final10.index = range(1,11)
```
<br>

OUTPUT:<br>
|    | artist(s)_name      |   Total Appearances |
|---:|:--------------------|--------------------:|
|  1 | The Weeknd          |              149419 |
|  2 | Taylor Swift        |              138944 |
|  3 | Ed Sheeran          |              132533 |
|  4 | Harry Styles        |              115056 |
|  5 | Eminem              |               88251 |
|  6 | Arctic Monkeys      |               85963 |
|  7 | Coldplay            |               77009 |
|  8 | Avicii              |               68973 |
|  9 | Adele               |               66980 |
| 10 | Dr. Dre, Snoop Dogg |               66131 |

<br>
I created a bar graph so that the differences in the data of each artist are easily seen to further simplify the data presented. The following syntax is what I used to plot the graph: <br>

```
#figsize
plt.figure(figsize=(20,10))

#bar plot 
plt.bar(final10['artist(s)_name'],final10['Total Appearances'], color = 'purple')

#title
plt.title('Total Number of Apperances of Artists in Playlists and Charts')

plt.xlabel('Artists') #label of x
plt.ylabel('Number of appearances') #label of y
```
<br>

OUTPUT: <br>
[INSERT IMAGE HERE] <br>

And there we go! The bar graph suggests that The Weeknd had the most appearances in playlists and charts on Spotify 2023; closely followed by Taylor Swift and Ed Sheeran. <br>
___________________________________________________________________
### [TAKEAWAYS]


___________________________________________________________________
### [VERSION(s)]


___________________________________________________________________
### [END OF REPOSITORY]
And that is a wrap! This is the end of my repository on an exploratory data analysis on the Spotify 2023 dataset. Please let me know if you have any feedback, tips, tricks, or suggestions for improving my coding efficiency! Thank you once again!

### [ACKNOWLEDGEMENT]
I would like to acknowledge Ms. Ma. Madecheen Pangaliman and Mr. Nikko John Lobos for providing knowledge about Python pandas, data wrangling, and data visualization and for providing the guide in conducting an exploratory data analysis presented in the repository. Thank you to both of you!

</div>
