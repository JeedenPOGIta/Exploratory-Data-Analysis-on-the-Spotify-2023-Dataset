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
<br>


### [BASIC DESCRIPTIVE STATISTICS]

### [TOP PERFORMERS]

### [TEMPORAL TRENDS]

### [GENRE AND MUSIC CHARACTERISTICS]

### [PLATFORM POPULARITY]

### [ADVANCED ANALYSIS]

### [TAKEAWAYS]

### [VERSION(s)]

## [END OF REPOSITORY]



</div>
