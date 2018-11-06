# Music Box user churn prediction and music recommender system


## 1. Project Summary

This purpose of this project is to use music box use log data (16+GB) including information on songs searched,played and downloaded, timestamp on each activity, user profile, etc to predict user churn and build a recomender system. This project builds a demo for analyzing large user record data and construct prediction and recommerder models for business. 

churn is one of the most important elements in the Key Performance Indicator (KPI) of a product or service. A full customer lifecycle analysis requires taking a look at retention rates in order to better understand the health of the business or product. In this project, churn is defined by inactivity in fixed 14 days window. It is predicted using the users' behavior pattern in a 30 day window before that 14 day window. In the churn predictioni model, features are generated from the log file, including the frequency, recency of events, total playing time, songs fully played.

Machine learning models, such as Logistic Regression, Random forest, Gradient boosting are applied to predict the user churn.Receiver Operating Characteristic (ROC) curves are used to diagnostic test evaluation. Random forest predict the end churn with accuracy around 0.92 on the training and 0.91 on the testing data set.

Feature importance is evaluated in the Logistic Regression, the top 5 most import features that increase churn risk are: 
'days_from_last_play','freq_S_last_1','freq_S_last_3','freq_P_last_1','freq_S_last_7'.

The recommender systems is based on Collaborative filtering using Alternating Least Square matrix factorization. Recommendation of songs to users and users to songs are shown in the script.

The shell scripts are used to preprocess raw user log data. The production scripts are written in Pyspark.  In this applicaiton, a user id level downsampling (randomly select 10% of users) is applied and processed on a personal computer.

## 2. Data Description

Preprocessing:
The user log data are sequentially read and total data are written into download data(down_ds.csv),play data(play_ds.csv), search data(search_ds.csv).

Data Cleaning:
Missing data, bot and outliers are removed from the processed data.
Irregular users that has a daily play time longer than 24hs are are considered bots and are consequently excluded from the data.
Song with zero length is also excluded from the recommender system.

Feature Engineering:
In the churn model,features are generated from the log file, including the frequency, recency of events, total playing time, songs fully played.
In the recommender system, play times of each song is generated to evaluate the user's rating of the song.
data set containing new features are saved as df_model_final.csv

