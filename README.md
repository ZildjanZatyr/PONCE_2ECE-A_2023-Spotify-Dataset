# 🎵Exploratory Data Analysis on Spotify 2023 Dataset🎵
![image](https://github.com/user-attachments/assets/0bd0cf79-8893-420e-a050-64192a3ad80f)


## 🖥️ Introduction
This repository serves as a comprehensive overview of the most streamed Spotify Songs of 2023, highlighting the tracks that defined the musical memoir of the past year. This serves as an extensive guide containing yearly to monthly trends, including top artists, frequently played songs, and musical attributes that shaped 2023 and defined our Generation Z. 
> [!NOTE]
> #### All information gathered in this repository is sourced from the dataset available at Kaggle.
> https://www.kaggle.com/datasets/nelgiriyewithana/top-spotify-songs-2023


## 1. Dataset Overview 📑
### A. 2023 Spotify Dataframe
#### 💻 *Code:*
```Ruby
# Import Python libraries to be used
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Print dataframe
spotify = pd.read_csv('spotify-2023.csv', encoding = 'latin-1')
spotify
```
> [!IMPORTANT]
> #### This repository wouldn't be possible without 2023 Spotify Data Frame.
> spotify-2023.csv
###### *Output:*
![image](https://github.com/user-attachments/assets/d86cf563-8184-4d1a-a1c7-910f8b9bb49f) 

### B. Dataset Rows and Columns
#### 💻 *Code:*
```Ruby
# How many rows and columns does the dataset contain?
rows = spotify.shape[0]
columns = spotify.shape[1]

# To create a dataframe to store inputs
shape_info = pd.DataFrame({
    'Data': ['Rows', 'Columns'],
    'Count': [rows, columns]
})

# Prints the dataframe
shape_info
```
###### *Output:*
![image](https://github.com/user-attachments/assets/e04beb6b-c625-43ec-8b0c-1950272af785)

### C. Dataset General Info
#### 💻 *Code:*
```Ruby
# Examine info per column containing non-null count and data type
spotify.info()
```
###### *Output:*
```Ruby
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 953 entries, 0 to 952
Data columns (total 24 columns):
 #   Column                Non-Null Count  Dtype 
---  ------                --------------  ----- 
 0   track_name            953 non-null    object
 1   artist(s)_name        953 non-null    object
 2   artist_count          953 non-null    int64 
 3   released_year         953 non-null    int64 
 4   released_month        953 non-null    int64 
 5   released_day          953 non-null    int64 
 6   in_spotify_playlists  953 non-null    int64 
 7   in_spotify_charts     953 non-null    int64 
 8   streams               953 non-null    object
 9   in_apple_playlists    953 non-null    int64 
 10  in_apple_charts       953 non-null    int64 
 11  in_deezer_playlists   953 non-null    object
 12  in_deezer_charts      953 non-null    int64 
 13  in_shazam_charts      903 non-null    object
 14  bpm                   953 non-null    int64 
 15  key                   858 non-null    object
 16  mode                  953 non-null    object
 17  danceability_%        953 non-null    int64 
 18  valence_%             953 non-null    int64 
 19  energy_%              953 non-null    int64 
 20  acousticness_%        953 non-null    int64 
 21  instrumentalness_%    953 non-null    int64 
 22  liveness_%            953 non-null    int64 
 23  speechiness_%         953 non-null    int64 
dtypes: int64(17), object(7)
memory usage: 178.8+ KB
```

### D. Dataset Missing Values
#### 💻 *Code:*
```Ruby
# To check if there are any missing values
spotify.isnull().sum()
```
###### *Output:*
```Ruby
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


## 2. Basic Descriptive Statistics 📑
### A. Statistical Description
#### 💻 *Code:*
```Ruby
# Obtain a statistical summary for the numerical columns in the spotify dataframe
spotify.describe()
```
###### *Output:*
![image](https://github.com/user-attachments/assets/6ffd061b-a044-4f5a-b160-d6851fa8c557)


### B. Measure of Central Tendency 
#### 💻 *Code:*
```Ruby
df = pd.DataFrame(spotify)

# Convert the object datatype to numeric values
df['streams'] = pd.to_numeric(df['streams'], errors = 'coerce')

# Calculate the mean, median, and standard deviation
mean = round(df['streams'].mean(), 2)
median = df['streams'].median()
std = round(df['streams'].std(), 2)

# Print the values
print(f"The Mean is: {mean}")
print(f"The Median is: {median}")
print(f"The Standard Deviation is: {std}")
```
###### *Output:*
```Ruby
The Mean is: 514137424.94
The Median is: 290530915.0
The Standard Deviation is: 566856949.04
```


## 3. Spotify Top Performers 📑
### A. 2023's Spotify Top Performing Artists
#### 💻 *Code:*
```Ruby
# Convert 'streams' to numeric after removing commas
spotify['streams'] = pd.to_numeric(spotify['streams'].astype(str).str.replace(',', ''), errors = 'coerce')

# Sort the top 5 streams then print
sorted_df = spotify.sort_values(by = 'streams', ascending = False).head(5).reset_index(drop = True)
sorted_df
```
###### *Output:*
![image](https://github.com/user-attachments/assets/51795d9d-69df-4b62-b0f9-e5b9e7eff25e)

### B. Top Performing Artist by Track Count
#### 💻 *Code:*
```Ruby
top_artists = spotify.assign(artist = spotify['artist(s)_name'].str.split(', ')).explode('artist')

# Group by artist and count occurrences
top_5_artists = top_artists['artist'].value_counts().head(5)

# Convert to DataFrame then print
top_artists_df = top_5_artists.reset_index()
top_artists_df.columns = ['Artist', 'Track Count']
top_artists_df
```
###### *Output:*
![image](https://github.com/user-attachments/assets/492bd922-16a4-499c-8a6b-e91cdc985240)






## 4. Temporal Trends 📑
### A. Tracks Released Per Year
#### 💻 *Code:*
```Ruby
# Groups yearly then counts the number of tracks 
tracks_per_year = spotify['released_year'].value_counts().sort_index()

# Generates the plot
plt.figure(figsize = (12, 6))
tracks_per_year.plot(kind = 'bar', color = 'green', edgecolor = 'black')
plt.title('Number of Tracks Released Per Year', fontsize = 16, fontweight = 'bold')
plt.xlabel('Year', fontsize = 11)
plt.ylabel('Number of Tracks', fontsize = 11)
plt.grid(axis = 'y', linestyle='--', alpha = 0.7)
plt.show()
```
###### *Output:*
![image](https://github.com/user-attachments/assets/f0019893-d7ab-4f9f-bdaf-5faabdc0d5b5)
#### *🔎 Key Findings:*
This analytical graph demonstrates the number of tracks released per year since a decade; starting from 1930 all the way to 2023. There is a significant spike in the tracks released in the year 2022, followed by 2023, and then 2021. The spike in 2022 has reached an all time high shadowing its competitor by almost double or even both 2023 and 2021 combined altogether. 

### B. Tracks Released by Artist Count
#### 💻 *Code:*
```Ruby
# Groups by year then counts the number of tracks
artist_count = spotify['artist_count'].value_counts().sort_index()

# Generates the plot
plt.figure(figsize = (12, 6))
artist_count.plot(kind = 'bar', color='green', edgecolor = 'black')
plt.title('Number of Tracks by Artist Count', fontsize = 16, fontweight = 'bold')
plt.xlabel('Number of Artists', fontsize = 11)
plt.ylabel('Number of Tracks', fontsize = 11)
plt.show()
```
###### *Output:*
![image](https://github.com/user-attachments/assets/f251a0a3-7277-45c3-943d-a62287a2fbec)


### C. Yearly Average Musical Attributes
#### 💻 *Code:*
```Ruby
attributes_by_year = spotify.groupby('released_year')[['bpm', 'danceability_%', 'energy_%', 'acousticness_%', 'valence_%', 'instrumentalness_%', 'liveness_%', 'speechiness_%']].mean()

# Plotting trends
plt.figure(figsize = (12, 7))
for attribute in attributes_by_year.columns:
    plt.plot(attributes_by_year.index, attributes_by_year[attribute], label = attribute)

# Generates the plot
plt.xlabel('Year', fontsize = 11)
plt.ylabel('Average Value', fontsize = 11)
plt.title('Annual Average Musical Attributes', fontsize = 16, fontweight = 'bold')
plt.legend(title = 'Attributes')
plt.grid(True)
plt.show()
```
###### *Output:*
![image](https://github.com/user-attachments/assets/8390e0f6-da28-465f-b655-bc29eee1694f)


### D. Tracks Released Per Month
#### 💻 *Code:*
```Ruby
tracks_per_month = spotify['released_month'].value_counts().sort_index()

# Generates the plot
plt.figure(figsize = (12, 6))
tracks_per_month.plot(kind = 'bar', color='green', edgecolor = 'black')
plt.title('Number of Tracks Released Per Month', fontsize = 16, fontweight = 'bold')
plt.xlabel('Month', fontsize = 11)
plt.ylabel('Number of Tracks', fontsize = 11)
plt.grid(axis = 'y', linestyle = '--', alpha = 0.5)
plt.xticks(ticks = range(12), labels = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'])
plt.show()
```
###### *Output:*
![image](https://github.com/user-attachments/assets/a765aad1-8efc-4ad7-a709-79b2b44fa1e4)


### E. Monthly Average Musical Attributes
#### 💻 *Code:*
```Ruby
monthly_attributes = spotify.groupby('released_month')[['bpm', 'danceability_%', 'energy_%', 'acousticness_%', 'valence_%', 'instrumentalness_%', 'liveness_%', 'speechiness_%']].mean()

# Plotting trends for each attribute using scatter plot
plt.figure(figsize = (12, 7))
for attribute in monthly_attributes.columns:
    plt.plot(monthly_attributes.index, monthly_attributes[attribute], label = attribute)

plt.xlabel('Month', fontsize = 11)
plt.ylabel('Average Values', fontsize = 11)
plt.title('Monthly Average Musical Attributes', fontsize = '16', fontweight = 'bold')
plt.legend(title = 'Attributes', loc = 'upper left')
plt.grid(True)
plt.xticks(ticks = range(1, 13), labels = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'])
plt.show()
```
###### *Output:*
![image](https://github.com/user-attachments/assets/81fb1b71-e712-4e78-ac0a-11a5a3eb8629)



## 5. Genre and Music Characteristics 📑
### A. Streams vs. Musical Attributes
#### 💻 *Code:*
```Ruby
# Convert specified columns to numeric, coercing errors to NaN
columns_to_convert = ['streams', 'bpm', 'danceability_%', 'energy_%', 'valence_%', 'acousticness_%', 'instrumentalness_%', 'liveness_%', 'speechiness_%']
spotify[columns_to_convert] = spotify[columns_to_convert].apply(pd.to_numeric, errors = 'coerce')

# Create and display the heatmap
plt.figure(figsize=(12, 6))
sns.heatmap(spotify[columns_to_convert].corr(), annot = True, cmap = 'Blues', fmt = '.2f', 
            xticklabels = columns_to_convert, yticklabels = columns_to_convert)
plt.title('Correlation between Streams and Musical Attributes', fontsize = 16, fontweight = 'bold')
plt.xticks(rotation = 45, ha = 'right', color = 'black')
plt.yticks(rotation = 0, color = 'black')
plt.show()
```
###### *Output:*
![image](https://github.com/user-attachments/assets/6fbc456c-3ece-46e2-9bc6-eebe34d97ca3)


### B. Danceability_% vs. Energy_% 📑
#### 💻 *Code:*
```Ruby
# Calculate the correlation coefficient
correlation = spotify['danceability_%'].corr(spotify['energy_%'])

# Create a scatter plot
plt.figure(figsize=(10, 6))
sns.scatterplot(data=spotify, x='danceability_%', y = 'energy_%', alpha = 0.6)
plt.title('Scatter Plot of Danceability vs Energy', fontsize = 12, fontweight = 'bold')
plt.xlabel('Danceability (%)', fontsize = 11)
plt.ylabel('Energy (%)', fontsize = 11)
plt.grid(True)
plt.show()

print(f'Correlation between danceability_% and energy_%: {correlation:.2f}')
```
###### *Output:*
![image](https://github.com/user-attachments/assets/b30d0bda-1a2e-4419-af32-a16cf0ac58cf)
```Ruby
Correlation between danceability_% and energy_%: 0.20
```

### C. Valence_% vs. Acousticness_% 📑
#### 💻 *Code:*
```Ruby
# Calculate the correlation coefficient
correlation = spotify['valence_%'].corr(spotify['acousticness_%'])

# Create a scatter plot
plt.figure(figsize = (10, 6))
sns.scatterplot(data = spotify, x = 'valence_%', y = 'acousticness_%', alpha = 0.6)
plt.title('Scatter Plot of Valence vs Acousticness', fontsize = 12, fontweight = 'bold')
plt.xlabel('Valence (%)', fontsize = 11)
plt.ylabel('Acousticness (%)', fontsize = 11)
plt.grid(True)
plt.show()

print(f'Correlation between valence_% and acousticness_%: {correlation:.2f}')
```
###### *Output:*
![image](https://github.com/user-attachments/assets/cd2bf586-7ca7-419c-826a-dfa533d703b4)

```Ruby
Correlation between valence_% and acousticness_%: -0.08
```


## 6. Platform Popularity 📑
#### 💻 *Code:*
```Ruby
# Convert specified columns to numeric
columns_to_convert = ['in_spotify_playlists', 'in_spotify_charts', 'in_apple_playlists', 'in_apple_charts', 'in_deezer_playlists', 'in_deezer_charts']
spotify[columns_to_convert] = spotify[columns_to_convert].apply(pd.to_numeric, errors = 'coerce')

# Reshape and sort the dataframe
platform_data = spotify.melt(value_vars = columns_to_convert, var_name = 'Platform', value_name = 'Count')
platform_data = platform_data.groupby('Platform')['Count'].sum().reset_index()
platform_data = platform_data.sort_values(by = 'Count', ascending = False)

# Plotting
plt.figure(figsize = (12, 6))
sns.barplot(data = platform_data, y = 'Platform', x = 'Count', color = 'green' , edgecolor = 'black')
plt.title('Number of Tracks by Platform', fontsize = 16, fontweight = 'bold')
plt.ylabel('Platform', fontsize = 11)
plt.xlabel('Number of Tracks', fontsize = 11)
plt.show()
```
###### *Output:*
![image](https://github.com/user-attachments/assets/31c99e96-2cf6-4e17-afed-c8772251e19c)


## 7. Advanced Analysis 📑
### A. Major vs. Minor Keys Streamability
#### 💻 *Code:*
```Ruby
key_plot = spotify.groupby(['key', 'mode']).size().reset_index(name = 'Count')

# Generates the plot
plt.figure(figsize = (12, 6))
sns.barplot(data = key_plot, y = 'Count', x = 'key', hue = 'mode', palette = 'bwr', edgecolor = 'black' , dodge = True) 
plt.title('Average Streamability of Keys', fontsize = 16, fontweight = 'bold')
plt.ylabel('Track Count', fontsize = 11)
plt.xlabel('Key', fontsize = 11)
plt.legend(title = 'mode')
plt.show()
```
###### *Output:*
![image](https://github.com/user-attachments/assets/1aac6f02-3392-4229-afa4-a6da4b91c920)
#### *🔎 Key Findings:*
This analysis aimed to explore the distribution of musical keys and their corresponding modes within a dataset of tracks from the Spotify platform. The bar plot reveals how many tracks are associated with each musical key, highlighting the most common keys used in the dataset.

### B. Most Frequently Appearing Artists
#### 💻 *Code:*
```Ruby
playlist_chart_columns = [
    'in_spotify_playlists', 
    'in_spotify_charts', 
    'in_apple_playlists', 
    'in_apple_charts', 
    'in_deezer_playlists', 
    'in_deezer_charts'
]

# Calculate total appearances of each artist across specified columns
artist_appearance_counts = spotify.groupby("artist(s)_name")[playlist_chart_columns].sum().sum(axis=1)
top_10_artists = artist_appearance_counts.nlargest(10).reset_index()
top_10_artists.columns = ['Artist', 'Total_Appearances']

# Sort the DataFrame from highest to lowest
top_10_artists = top_10_artists.sort_values(by = 'Total_Appearances', ascending = True)

# Generates the plot
plt.figure(figsize = (14, 7))
# Using plt.barh for a different approach
plt.barh(top_10_artists['Artist'], top_10_artists['Total_Appearances'], edgecolor = 'black', color=sns.color_palette("gist_earth", len(top_10_artists)))
plt.title('Top 10 Artists by Appearances in Playlists and Charts', fontsize = 16, fontweight = 'bold')
plt.xlabel('Total Appearances', fontsize = 11)
plt.ylabel('Artist', fontsize = 11)
plt.grid(axis = 'x', linestyle = '--', alpha = 0.7)

# Adds extra labels to individual bars
for index, value in enumerate(top_10_artists['Total_Appearances']):
    plt.text(value, index, str(value), va = 'center')

plt.show()
```
###### *Output:*
![image](https://github.com/user-attachments/assets/91cdf229-826a-41f0-8da6-0693ad6c8667)
#### *🔎 Key Findings:*
Findings were visualized with a horizontal bar chart effectively displaying the total appearances of each artist. 

## 🔐 Conclusion
This repository encapsulates a vibrant year in music history, showcasing tracks that resonated with listeners and broke record around the globe. We explored the appearances of various artists across multiple streaming platforms, specifically focusing on their presence in playlists and charts. The highlight of this data reveals the top 10 artists with the highest total appearances, showcasing their popularity and reach across these platforms. Such insights are valuable for music  industry stakeholders, including record labels, marketers, and artists themselves, as they navigate the competitive landscape of music streaming and audience engagement.
> [!NOTE]
> #### With 2023 wrapped, Kaggle has made available the Most Streamed Spotify Songs of 2024. See attached link below: 
> https://www.kaggle.com/datasets/nelgiriyewithana/most-streamed-spotify-songs-2024

## 👨‍💻 Author
#### *Zildjan Zatyr C. Ponce || 2ECE - A* 
#### *University of Santo Tomas*
#### *Submitted: November 9, 2024*

