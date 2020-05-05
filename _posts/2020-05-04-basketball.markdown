---
layout: post
title:  Predicting NBA Games
comment_issue_id: 10
---

The goal of this project is to use machine learning algorithms to predict the outcomes of NBA games. The models used are logistic regression and a multilayer perceptron neural network. The dataset is game statistics from the 12 NBA seasons ranging from 2007 through 2019. As a baseline model, naive predictions are made based on the winning percentages and average points scored of the teams going into the games. The predictions made by all of the models are compared to the predictions made by Las Vegas when setting odds for people to bet on games during the time period.

The data and code for the project are found [here](https://github.com/Joe-Ferrara/predicting-nba-games).

## The Data

# NBA Games Data

The NBA game results data was found on kaggle.com, [here](https://www.kaggle.com/nathanlauga/nba-games). Thanks to Nathan Lauga for posting it. The NBA games data contains team and player results and statistics from every NBA preseason, regular season, and postseason game during the time period from the beginning of the 2004-05 season to February 2020.

The file, *games.csv*, has one row for each game, with columns giving the game identifiers, home team statistics and away team statistics. For example, here are the game identifiers and home team statistics for the first five rows:

|   GAME_ID | DATE            |   SEASON |   HOME_TEAM_ID |   PTS_home |   FG_PCT_home |
|----------:|:----------------|---------:|---------------:|-----------:|--------------:|
|  21900895 | 2020-03-01      |     2019 |     1610612766 |         85 |         0.354 |
|  21900896 | 2020-03-01      |     2019 |     1610612750 |         91 |         0.364 |
|  21900897 | 2020-03-01      |     2019 |     1610612746 |        136 |         0.592 |
|  21900898 | 2020-03-01      |     2019 |     1610612743 |        133 |         0.566 |
|  21900899 | 2020-03-01      |     2019 |     1610612758 |        106 |         0.407 |

|   FT_PCT_home |   FG3_PCT_home |   AST_home |   REB_home |   HOME_TEAM_WINS |
|--------------:|---------------:|-----------:|-----------:|-----------------:|
|         0.9   |          0.229 |         22 |         47 |                0 |
|         0.4   |          0.31  |         19 |         57 |                0 |
|         0.805 |          0.542 |         25 |         37 |                1 |
|         0.7   |          0.5   |         38 |         41 |                1 |
|         0.885 |          0.257 |         18 |         51 |                1 |

An important feature to note is the ``HOME_TEAM_WINS`` column, which says whether or not the home team won the game. This is the column that will be predicted.

The file, *games_details.csv*, has the player statistics. It has one row for each (game, player) pair, and has columns giving (game, player) identifiers, and player statistics for that game. An example of some of the (game, player) identifiers and player statistics follows:

|   GAME_ID |    TEAM    |   PLAYER_ID | MIN   |   FGM |   FGA |   PTS |   REB |   AST |
|----------:|-----------:|------------:|:------|------:|------:|------:|------:|------:|
|  21900895 | MIL        |      202083 | 27:08 |     3 |    11 |     8 |     8 |     2 |
|  21900895 | MIL        |      203507 | 34:55 |    17 |    28 |    41 |    20 |     6 |
|  21900895 | MIL        |      201572 | 26:25 |     4 |    11 |    16 |     7 |     0 |
|  21900895 | MIL        |     1628978 | 27:35 |     1 |     5 |     2 |     7 |     5 |
|  21900895 | MIL        |      202339 | 22:17 |     2 |     8 |     4 |     1 |     2 |

To predict outcomes of games, the data was aggregated to contain teams and players running stats from all previous games each season. The new aggregated data has in each row the average and total stats for each team or player going into the game in question. The script *regular_season_stats_averages_and_totals.py* contains the code used to create these running statistics. The files, *teams_running.csv* and *players_running.csv* contain the aggregated running statistics in addition to the statistics in *games.csv* and *games_details.csv*. A slice of *teams_running.csv* with some of the home team statistics follows:


|   GAME_ID | HOME   |   HOME_WINS |   HOME_LOSSES |   HOME_WIN_PCT |
|----------:|:-------|------------:|--------------:|---------------:|
|  21900895 | CHA    |          21 |            38 |       0.355932 |
|  21900896 | MIN    |          17 |            41 |       0.293103 |
|  21900897 | LAC    |          40 |            19 |       0.677966 |
|  21900898 | DEN    |          40 |            19 |       0.677966 |
|  21900899 | SAC    |          25 |            34 |       0.423729 |

|   HOME_PTS_AVE |   HOME_AST_AVE |   HOME_REB_AVE |
|---------------:|---------------:|---------------:|
|        102.237 |        23.6949 |        43.0339 |
|        113.224 |        23.7414 |        44.931  |
|        115.881 |        24.0678 |        48.1186 |
|        110.525 |        26.3729 |        44.4915 |
|        108.339 |        23.3729 |        42.2542 |

Here is a slice of *players_running.csv* with some of the player statistics going into the game:

|   GAME_ID |     TEAM    |   PLAYER_ID |   MIN_AVE |  PTS_AVE |   REB_AVE |   AST_AVE |
|----------:|------------:|------------:|----------:|---------:|----------:|----------:|
|  21900895 | MIL         | 202083      |   24.5375 |  7.58929 |   2.44643 |   1.5     |
|  21900895 | MIL         | 203507      |   30.817  | 29.717   |  13.6792  |   5.81132 |
|  21900895 | MIL         | 201572      |   26.5512 | 10.6964  |   4.41071 |   1.625   |
|  21900895 | MIL         | 1628978     |   22.7954 |  9.05556 |   4.81481 |   2.16667 |
|  21900895 | MIL         | 202339      |   27.248  | 15.6667  |   4.82353 |   5.47059 |

There are two other files, *teams_totals.csv* and *players_totals.csv*, that contain the end of the year statistics for each team and player. Some random rows from these csv's were cross-checked with the statistics at [basketball-reference.com](https://www.basketball-reference.com/) to ensure that no mistakes were made when in calculating the running statistics. To my knowledge the running statistics of a team or player from a specific date in a season are not publicly available, so I could not check the running statistics directly.

In order to easily use all of these statistics to predict games, the two running  datasets were merged into one dataset that contains for each game the running team statistics and player statistics for every player that appeared in the game. The player columns were numbered from player 1 to player 16, and ordered by points per game average so that later on it would be easy to discard the inconsequential players. The script that merges the two running statistics datasets is *merging_and_cleaning_stats.py*, which outputs the merged dataset as the file *full_stats.csv*.

# Betting Data: How good is Vegas at predicting NBA games?

The betting odds data used was found at the website sportsbookreviewsonline.com, [here](https://www.sportsbookreviewsonline.com/scoresoddsarchives/nba/nbaoddsarchives.htm). It contains the betting odds from all regular and postseason games from the 2007-08 season through the current 2020 season. For each game, the odds data contains the closing over/under, closing spread, and closing money line for each team. This data is organized as one csv file for each season. The 2007-08 season csv is titled *nba_odds_2007-08.csv* with the other seasons titled similarly. The first four games in the 2007-08 season are recorded in the csv as follows:

|   Date | VH   | Team         |   Final |   Close |    ML |
|-------:|:-----|:-------------|--------:|--------:|------:|
|   1030 | V    | Portland     |      97 |   189.5 |   900 |
|   1030 | H    | SanAntonio   |     106 |    13   | -1400 |
|   1030 | V    | Utah         |     117 |   212   |   100 |
|   1030 | H    | GoldenState  |      96 |     1   |  -120 |
|   1030 | V    | Houston      |      95 |     5   |  -230 |
|   1030 | H    | LALakers     |      93 |   199   |   190 |
|   1031 | V    | Philadelphia |      97 |   191   |   255 |
|   1031 | H    | Toronto      |     106 |     6.5 |  -305 |

Every two rows corresponds to one game with the away team as the first row and the home team as the second. The ``Close`` column has the over/under as the larger number, and the spread for the game in the row of the favored team. The ``ML`` column has the money line for each of the teams.

This data was organized into a csv with one row for each game, as well as the date and team names labeled the same as the csv's from the NBA games data section. The betting odds are also translated into predictions for the score of the game and the probability of the home team winning. The script that creates the new odds csv is *clean_odds_data.py*. It outputs a file for each season. The file for the 2007-08 season is titled *odds_2007.csv*, and the other seasons are titled similarly. The organized data for the first four games is as follows:

| DATE       | HOME   | AWAY   |   HOME_PTS |   AWAY_PTS |   HOME_WINS |
|:-----------|:-------|:-------|-----------:|-----------:|------------:|
| 2007-10-30 | SAS    | POR    |        106 |         97 |           1 |
| 2007-10-30 | GSW    | UTA    |         96 |        117 |           0 |
| 2007-10-30 | LAL    | HOU    |         93 |         95 |           0 |
| 2007-10-31 | TOR    | PHI    |        106 |         97 |           1 |

|   PRED_HOME_PTS |   PRED_AWAY_PTS |   PRED_HOME_WINS |   HOME_WIN_PROB |
|----------------:|----------------:|-----------------:|----------------:|
|          101.25 |           88.25 |                1 |        0.933333 |
|          106.5  |          105.5  |                1 |        0.545455 |
|           97    |          102    |                0 |        0.344828 |
|           98.75 |           92.25 |                1 |        0.753086 |

The script *odds_analysis.py* does some analysis on how well Vegas predicts the outcomes of the games during this time period. In the data there are 15211 games. Of these games, Vegas correctly predicted the winner 68.25% of the time.

There are some other interesting statistics from the Vegas odds data, though these statistics will not be used anywhere else in the project. The average score (home or away) error is 8.41 points, with 66.62% of the score predictions being within 10 points. 308 times either the home or away team's score is predicted exactly correct. 2 times both the home and away teams score in the same game is predicted correctly. The average spread error is 6.98 points, with 35.26% of the spread predictions within 3 points. The average over/under prediction error is 13.83 points, with 45.65% of the over/under predictions within 10 points.

## Models and Predictions

# Model Preprocessing

The first 10 games of the season were taken out of the data for small sample size reasons. In these cases, there are not enough games earlier in the season for the data to have any hope of being predictive. The years before 2007 were taken out of the NBA games data to make the years of the NBA games data match the years of odds data. Also, any preseason and postseason games were removed from the datasets.

For each game only the top 8 players in order of average points on each team were kept, so only the more relevant players are considered.

For the logistic regression and multi-layer perceptron models, the 2018-19 and 2019-20 games data was held out as a test set. The 2007-08 through 2017-18 seasons data was split 80%, 20% for training and validation. On the other hand, the naive models were run on all the games data since there is no training and validation in these models.

For the multi-layer perceptron model, the data was scaled using ``StandardScaler`` from ``sklearn.preprocessing`` to make the columns have mean 0 and values in the range -1 to 1.

# Naive Models

There are three naive prediction models:
* Points per game: predict the winner of the game by the team with the higher average points per game.
* Point differential: predict the winner of the game by the team with the higher average point differential. Average point differential is average points per game minus averaged points per game allowed.
* Winning percentage: predict the winner of the game by the team with the higher winning percentage.

The script that carries out the naive models is *naive_predictions.py*.

The results of these baseline models and the Vegas odds predictions are recorded in the following table:

| Prediction Method | Percent Correct |
|-------------------|--------------------|
| Vegas Odds        | 68.25%             |
| Winning Percentage| 65.54%             |
| Point Differential| 65.49%             |
| Points Per Game   | 58.94%             |

Each of the naive models was also done using home and away splits for each team instead of the total average. This means for the home team, only their previous home game averages were used, and for the away team, only their previous away game averages. The results with the home and away splits are in the following table:

| Using home and away splits | Percent Correct |
|------------------------|-----------------|
| Winning Percentage     | 66.12%          |
| Point Differential     | 57.58%          |
| Points per Game        | 55.35%          |

Point differential and points per game using the home and away splits did worse, while when using winning percentage the home and away splits did slightly better.

In general, I was surprised how close the naive method of prediction by winning percentage is to the Vegas odds predictions.

# Logistic Regression

A logistic regression model was run on 3 different groups of statistics:
* Player statistics: All the player average statistics in *full_stats.csv*.
* Team statistics: All the team statistics in *full_stats.csv*.
* Player and team statistics: Combination of the player and team statistics.

The script for the logistic regression model is *logistic_regression.py*. The model used is ``LogisticRegression`` from ``sklean.linear_model`` with the default parameters.

The results from the logistic regression model are recorded in the following table:

|Statistics<br>Group|Training Data<br>Percent Correct|Validation Data<br>Percent Correct|
|-----------|----------|----------|
|Player     | 70.43%   | 68.93%   |
|Team  | 67.64%   | 67.79%   |
|Player and <br> Team | 70.51% | 69.42% |

The player, as well as player and team statistics, narrowly beat Vegas on the validation data. The training and validation numbers are good and close, evidence of little overfitting or underfitting.

# Multi-layer Perceptron

The multi-layer perceptron model was run on the same three groups of statistics as the logistic regression model. The model used is ``MLPClassifier`` from ``sklearn.neural_network``. The parameters of the model were tuned to obtain optimal results. The activation parameter functions *relu*, *tanh*, and *logistic* were all tried with *tanh* giving the best results. Various numbers of layers, hidden layer sizes, and values for the *alpha* parameter were systematically searched.

It was difficult to find parameters that beat the Vegas odds on the training and validation sets. The following four model parameters were settled on as the best:
* MLP 1: ``alpha = 1000, hidden_layer_sizes = (100, 75, 50), activation = 'tanh'``
* MLP 2: ``alpha = 1000, hidden_layer_sizes = (100, 100, 100), activation = 'tanh'``
* MLP 3: ``alpha = 900, hidden_layer_sizes = (100, 75, 50), activation = 'tanh'``
* MLP 4: ``alpha = 900, hidden_layer_sizes = (100, 100, 100), activation = 'tanh'``

The performance of these models on the training and validation data is recorded in the following table:

| Model | Statistics Used| Training Data<br>Percent Correct|Validation Data<br>Percent Correct|
|-------|--------------|------------|--------------------------|
| MLP 1 | Player | 59.17% | 59.46% |
|       | Team | 59.17% | 59.46% |
|       | Player and Team | 68.29% | 68.58% |
| MLP 2 | Player | 67.20% | 66.70% |
|       | Team | 59.17% | 59.46% |
|       | Player and Team | 68.24% | 68.63% |
| MLP 3 | Player | 68.30% | 66.34% |
|       | Team | 59.17% | 59.46% |
|       | Player and Team | 68.68% | 68.76% |
| MLP 4 | Player | 68.28% | 66.43% |
|       | Team | 59.17% | 59.46% |
|       | Player and Team | 68.85% | 65.98% |

These numbers show that for the multi-layer perceptron model, using just the team statistics does worse than using players or players and teams. MLP 1, 2, and 3 beat the Vegas odds on the validation data when the player and team statistics are used.

One weird phenomenon from the numbers is that some of the MLP models are performing better on the validation set than the training set. While this is possible, I am not sure why it is happening. It could be a combination of the facts that the parameters are tuned to minimize overfitting and that the validation set is too small.

# Results on Test Data

On the test data, all 4 MLP models were run. MLP 3 performed best on training and validation, as well as on the test data for all three statistical categories, so only MLP 3 is recorded in the following table comparison between the MLP model and logistic regression:

| Model | Player Stats | Team Stats | Player and Team<br>Stats |
|----------|----------|----------|----------|
| Logistic Regression | 65.87% | 65.64% | 66.31% |
| MLP  | 65.75% | 57.54% | 66.03% |

Both models had significant drops from the validation data to the test data. This could be because teams may develop a certain statistical profile throughout a season causing in season prediction to be easier than cross-season prediction. The models may have generalized better to the validation data than the test data because the training data and validation data both contain the same seasons.

MLP and logistic regression beat the best naive model when using player statistics and player and team statistics.

# Future Work

This projects lends itself to many future possibilities. One is to create more advanced statistics than just the ones considered. For instance, using the game dates, one could put the number of days off before the game into the datasets. More advanced team statistics can also be obtained by aggregating the player statistics for each team. A second direction to pursue is to add a convolution layer to the neural network. This could potentially use the player stats in a more efficient and interesting manner. A third direction is to consider more of the Vegas odds data and the probabilities predicted by the models to derive a betting strategy that could win a potential bettor money.
