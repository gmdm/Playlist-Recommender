<p align="center">
  <image src=https://ksassets.timeincuk.net/wp/uploads/sites/55/2013/07/VinylRecordShop02PA010911-1.jpg>
</p>

# Music Playlist Recommender

Music Playlist Recommendation System

## Overview

With the growing popularity and functionality of recommendation systems, we are living in a world where everything feels personalized to us. Whether it be specific ads popping up in your Instagram feed minutes after you talk about a certain product with a friend or Amazon suggesting items you might want to purchase, technology has given us the ability give recommendations.

As someone who enjoys music and the joy of discovering a new song, I wanted to explore how these recommenders work and build a system that will give me similar songs to the one's I've listened to.

## Objective
The objective of this project is to build an effective song recommender system by looking at certain features of the songs and by looking at similarities between users. 

## Data
Track Features Data and User Playlist Data from Spotify 

I worked with 2 datasets: 

* one with 170K songs and 17 different features that describe this song (e.g. energy, loudness, valance, danceability, etc.)
* another one with 15K users and their playlists which comprise a total number of 2M unique songs

## Data Exploration and Analysis


1. I plotted the distribution of the song features to get a sense of which ones might be useful in making good recommendations. Features that are distributed more evenly would likely generate a better recommender as opposed to distributions that are heavily skewed to one side.

* Distribution of Valence -- As you'll see in the histrogram below, valance is normally distributed. Good feature to use!
<p align="center">
  <image src=img/EDA_Valence_Dist.png>
</p>



* Distribution of Acousticness -- Acousticness has a bi-modal distribution which is low in the center and has 2 peaks, both at each side (i.e. "inverted bell curve" or "well curve"). Also a good feature to use!  
<p align="center">
  <image src=img/EDA_Acousticness_Dist.png>
</p>
 
 
 
* Distribution of Instrumentalness -- Instrumentalness has a distribution that is heavily positively skewed. Most of the values of instrumentalness fall within ~0.1. Probably not a good feature to use.
<p align="center">
  <image src=img/EDA_Instrumentalness_Dist.png>
</p>
  

2. I also looked at the number of unique users and unique tracks in the user playlist dataset. There were 15K unique users and 2M unique tracks. This amounted to 12M rows which was way too much so I decided to only include the users that have 3K or more tracks in their playlists and only using tracks that appear on someone's playlist 1K times or more. All in all, I trimmed the data down to 319K rows with 693 unique users and 460 unique tracks.


## Models
### Content Based Recommender


1. Used the following features to recommend songs:

* Valence
* Acousticness
* Danceability
* Energy
* Loudness
* Tempo

2. Used cosine similarity as similarity measure.

3. Sample of recommended songs:

<p align="center">
  <image src=img/Blinding_Lights_Recos.png>
</p>
  

<p align="center">
  <image src=img/Bad_Romance_Recos.png>
</p>
  
4. The songs definetly had similary feature scores. However, the list of songs recommended does not immediately stand out as being similar to the input song. I had to listen to them to realize they actually are similar.
  
  
### Collaborative Filtering Recommender

1. Used Surprise python library (http://surpriselib.com/) to cross validate different collaborative filtering methods.

2. Using the cleaned up dataset with trimmed down users and tracks and pseudo-ratings calculated based on # of times a particular song appeared on a particular user's playlists, I fit the data into different algorithms. I used Root Mean Squared Error (RMSE) to evaluate.

<p align="center">
  <image src=img/Blinding_Lights_Recos.png>
</p>




## Future work
* Incorporate more content features
* More hyper parameter tuning
* More hidden layers in neural networks
