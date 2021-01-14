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
### Baseline model - average rating adjusted by user/book deviation
Baseline estimate for r_xi = u + b_x + b_i

u: global mean (overall mean book ratings)
b_x: rating deviation of user x = (avg. rating of user x) - u
b_i: rating deviation of book i = (avg. rating of book i) - u

### Collaborative filtering model - matrix factorization

By using embedding, we can uncover the latent features for both users and books and predict the rate by a given user to a given book. We used embeddings rather than the method of singular value decomposition (SVD). Since SVD is based on the rating matrix's eighenvalues and eighen vectors, which is computationally expensive. Using embeddings with sparse tensor and the optimation method of alternative least squares will improve the computation efficiency. 
<p align="center">
  <image src=visualization/CF_embedding.png />
</p>

## Future work
* Incorporate more content features
* More hyper parameter tuning
* More hidden layers in neural networks
