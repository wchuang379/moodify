# moodify-for-spotify
MAIN DATASET:
https://github.com/vaslnk/Spotify-Song-Recommendation-ML/tree/master/data?fbclid=IwAR30mCJqGeehmMyhwkK26WvK5grtOB_ciP-Rjlpwa-2avySKdSNtu4c1-qs

DATA:

playlist2tracks_full.txt - contains all of the playlists inner dataset 

tracks2features_full.csv - contains a table that has the track title, artist name, and audio features

tracks2features_full.db - 

CODE:

audio_errors.py - visualization for the errors of the audio feature pairs to better determine which pair produced the lowest error

audio_playlist_generation.py - generated 500 unique playlists with audio feature clustering

data_collector.py - script to collect the data and dump it in a .db file and a .txt file

final_audio_pairs.py - clustering audio feature pairs with visualization, six total combinations of the four features

final_kmeans.py - clustering four audio features including plot after PCA dimensionality reduction and elbow-point plot

sparse_playlists.py - this program, alongside utils_playlists.py, creates a similarity matrix using song vectors and context windows
