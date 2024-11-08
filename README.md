# 🎵Exploratory Data Analysis on Spotify 2023 Dataset🎵

## Introduction
This github repository

## Table of Contents
1. [Introduction](#-Introduction)
2. [Dataset Overview](#-DatasetOverview) 
   - s
4. [Basic Descriptive Statistics](#-BasicDescriptiveStatistics)
   - s
6. Top Performers
   - s
8. Temporal Trends
   - Yearly Released Tracks
   - Track Distribution Count
   - Annual Musical Attributes
   - Monthly Released Tracks
10. Genre and Music Characteristics
    - s
12. Platform Popularity
    - s
14. Advanced Analysis
    - s
16. Conclusion





## Dataset Overview
> This section dives into the analytic display of data 
#### 💻 *Code:*
```Ruby
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

spotify = pd.read_csv('spotify-2023.csv', encoding = 'latin-1')
spotify
```
![image](https://github.com/user-attachments/assets/d86cf563-8184-4d1a-a1c7-910f8b9bb49f) 


#### 💻 *Code:*
```Ruby
# How many rows and columns does the dataset contain?
print("The Spotify Dataset contains", spotify.shape[0], "rows")
print("The Spotify Dataset contains", spotify.shape[1], "columns")
```
![image](https://github.com/user-attachments/assets/5bce33ee-a304-432a-9c3f-60c51144a6a8)
![image](https://github.com/user-attachments/assets/16e85fad-09e8-4d21-8978-917d66911738)


#### 💻 *Code:*
```Ruby
spotify.info()
```
![image](https://github.com/user-attachments/assets/923f3df7-40cc-4821-8290-c99e28991ea1)

#### 💻 *Code:*
```Ruby
# To check if there are any missing values
print(spotify.isnull().sum())
```
![image](https://github.com/user-attachments/assets/b2ac0617-be5c-434a-b3ca-37a51fdce0ab)


## Basic Descriptive Statistics


#### 💻 *Code:*
```Ruby
spotify.describe()
```
![image](https://github.com/user-attachments/assets/6ffd061b-a044-4f5a-b160-d6851fa8c557)


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
![image](https://github.com/user-attachments/assets/c4d93468-ab51-4d2d-be44-a4256e471151)


## Spotify Top Performers

#### 💻 *Code:*
```Ruby
# Convert 'streams' to numeric after removing commas
spotify['streams'] = pd.to_numeric(spotify['streams'].astype(str).str.replace(',', ''), errors='coerce')

# Sort the top 5 streams then print
top_5_sorted_df = spotify.sort_values(by='streams', ascending=False).head(5).reset_index(drop=True)
top_5_sorted_df
```
![image](https://github.com/user-attachments/assets/51795d9d-69df-4b62-b0f9-e5b9e7eff25e)


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
![image](https://github.com/user-attachments/assets/492bd922-16a4-499c-8a6b-e91cdc985240)






## Temporal Trends

#### 💻 *Code:*
```Ruby
# Group by year and count the number of tracks
tracks_per_year = spotify['released_year'].value_counts().sort_index()

# Create a plot
plt.figure(figsize=(12, 6))
tracks_per_year.plot(kind='bar', color='green')
plt.title('Number of Tracks Released Per Year')
plt.xlabel('Year')
plt.ylabel('Number of Tracks')
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()
```
![image](https://github.com/user-attachments/assets/fbc560c3-5bf3-4c2c-b504-90459e96552b)


#### 💻 *Code:*
```Ruby
# Group by year and count the number of tracks
artist_count = spotify['artist_count'].value_counts().sort_index()

# Create a plot
plt.figure(figsize=(12, 6))
artist_count.plot(kind='bar', color='green')
plt.title('Distribution of Tracks by Artist Count')
plt.xlabel('Number of Artists')
plt.ylabel('Number of Tracks')
plt.grid(axis = 'y', linestyle='-', alpha = 0.5)
plt.show()
```
![image](https://github.com/user-attachments/assets/ac7c56a9-ea03-484b-b4a4-4a0599bdf00e)

#### 💻 *Code:*
```Ruby
attributes_by_year = spotify.groupby('released_year')[['danceability_%', 'energy_%', 'acousticness_%', 'valence_%']].mean()

# Plotting trends for each attribute using scatter plot
plt.figure(figsize=(12, 6))
for attribute in attributes_by_year.columns:
    plt.plot(attributes_by_year.index, attributes_by_year[attribute], label = attribute)

plt.xlabel('Year')
plt.ylabel('Average Value')
plt.title('Annual Average Musical Attributes')
plt.legend()
plt.grid(True)
plt.show()
```
![image](https://github.com/user-attachments/assets/e00fd7af-2791-47fd-b7a1-510e93b01e96)


## Genre and Music Characteristics
#### 💻 *Code:*

## Platform Popularity
#### 💻 *Code:*

## Advanced Analysis
#### 💻 *Code:*
