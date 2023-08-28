# moodify-for-spotify

**MAIN DATASET:**
https://github.com/vaslnk/Spotify-Song-Recommendation-ML/tree/master/data?fbclid=IwAR30mCJqGeehmMyhwkK26WvK5grtOB_ciP-Rjlpwa-2avySKdSNtu4c1-qs

**DATA:**

- playlist2tracks_full.txt - contains all of the playlists inner dataset 

- tracks2features_full.csv/tracks2features_full.db - contains a table that has the track title, artist name, and audio features


**CODE:**

- audio_errors.py - visualization for the errors of the audio feature pairs to better determine which pair produced the lowest error

- audio_playlist_generation.py - generated 500 unique playlists with audio feature clustering

- data_collector.py - script to collect the data and dump it in a .db file and a .txt file

- final_audio_pairs.py - clustering audio feature pairs with visualization, six total combinations of the four features

- final_kmeans.py - clustering four audio features including plot after PCA dimensionality reduction and elbow-point plot

- sparse_playlists.py - this program, alongside utils_playlists.py, creates a similarity matrix using song vectors and context windows


**PLAYLISTS:**

- 500 playlists for each method


**Moodify for Spotify**

**Introduction & Goals**

Have you ever wondered how Spotify makes their recommended playlists? Don't you love the process of creating your own? This project aims to use Spotify past user-generated playlist data and Spotify song audio features to group songs into similar topics and be able to generate our own data-driven playlists.


**Project Overview**

This project is based on a **Spotify dataset of 4000 user-generated playlists** (containing **over 2 million songs** in total). The data is stored as a JSON object: each playlist is a dictionary of its features, with one being a list of tracks within the said playlist. I used this JSON, alongside the Spotify API, to construct two corpuses of data:
‍
1.  A **mapping from playlist titles to track titles** within that playlist in order to implement a **playlist generation model based on the deep learning word vector algorithm**.
‍
2.  A **mapping from song titles to a predefined set of audio features** that I estimated to be most important **(tempo • valence • danceability • energy)** is used to implement a **playlist-generating model using K-Means clustering**. Audio features were found by making 75,833 API calls to the Spotify server through the unique track IDs of each track.


**Method 1: Song Recs by Playlist Similarity**

The first method of determining the similarity between songs was by using **song vectorizations and context windows**. I determined the closeness of songs by **how often they appear in the same playlist together**. In other words, this method represents similarity as determined through the user-generated playlists - **representative of user opinions**. Each song is assigned a vector which determines how often every other song appears in the same playlist as that song. I found the distance between songs using a cosine distance metric between the two vectors. This helps to determine the most similar songs and be able to find the top most similar songs to a particular song. Next, I applied the **TSNE dimensionality reduction algorithm** to map the distance vectors into two dimensions most representative of the variation. Then I ran K-Means clustering on it. The result from **6-cluster K-Means** is our song set divided into 6 topics of songs that are most similar to each other. Finally, I ran **K-Means** using **500 clusters to produce 500 playlists of the most similar songs**. Playlists are self-labeled.


**Method 2: Song Clustering By Audio Features (K-Means)**

For the second playlist-generating program, I decided to **cluster tracks based on their audio feature similarities**. That is, tracks were similar if the difference between their audio features was small. After consulting several musician friends, I chose to focus on 4 audio features - tempo, valence, danceability, and energy. They suggested that this set is the most representative of a song out of the 13 pre-defined audio features in the Spotify API. Since audio features have different scales, I normalized each feature by its maximum existing value. Then, I decided to implement K-Means clustering in 2 different ways:

1) I **clustered songs based on all 5 features and used the PCA dimensionality-reduction algorithm** to reduce our plots to 3 dimensions. I ran the program for a range of N-clusters and used the accumulated errors to plot an elbow graph and **concluded that the optimum number of clusters is 7**.

2) I used all **6 possible pairs of features from the 4 features** I selected and clustered each of them to get this 6-cluster graph on the left (e.g. **Energy & Danceability, Valence & Tempo, etc**).
‍
I **compared the clustering errors of each pair**, as seen in the graph below. The pair of audio features resulting in the lowest clustering error is **Tempo & Danceability**.
‍

**Conclusions**

Firstly, through the use of two methods, 1) similarity by user-generated playlists, and 2) similarity by audio features, I was able to **create 500 playlists each of similar songs**. Secondly, I determined through K-Means clustering on various audio features of songs, that through looking at the clustering errors, the pair of audio features that results in the lowest error is **Tempo & Danceability**.
‍
