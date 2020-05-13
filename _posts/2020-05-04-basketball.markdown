---
layout: post
title:  Predicting NBA Games
comment_issue_id: 10
---



In this post I compare how different machine learning algorithms do at predicting the outcomes of NBA games. The post is inspired by the paper, *Exploiting sports-betting market using machine learning*, by Hubáček, Šourek, and Železný ([[HSZ]](#HSZ)), where they use logistic regression and neural network models to predict the outcomes of basketball games, and then devise a betting strategy based on their models. In my following post I plan to explore possible betting strategies using the models from this post.

The models used in this post are logistic regression, a support vector machine, nearest neighbors, and a multilayer perceptron neural network. The dataset used is game statistics from the 12 NBA seasons 2007-08 through 2019-20. Each model is used on player only statistics, team only statistics, and the combination of player and team statistics. The predictions from each type of statistics is then compared. As a baseline model, naive predictions are made using the winning percentages and average points scored of the home and away teams. A dataset of Las Vegas betting odds from the same time period of NBA games is also analyzed. The predictions made by all of the models are compared to the predictions made by the Las Vegas odds.

The data and code for the project are found on my github page [here](https://github.com/Joe-Ferrara/predicting-nba-games).

## The Data

# NBA Games Data

The NBA game statistics data was found on kaggle.com, [here](https://www.kaggle.com/nathanlauga/nba-games). Thanks to Nathan Lauga for posting it. The data contains team and player statistics from every NBA preseason, regular season, and postseason game from the 2004-05 season through February of the 2019-20 season.

The file, *games.csv*, has one row for each game, with columns giving game identifiers, home team statistics, and away team statistics. For example, here are the game identifiers and home team statistics from the first five rows:

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

The ``HOME_TEAM_WINS`` column, which says whether or not the home team won the game, is the column of interest to be predicted.

The file, *games_details.csv*, has the player statistics. It has one row for each (game, player) pair, and has columns giving (game, player) identifiers, and player statistics for that game. An example of some of the (game, player) identifiers and player statistics follows:

|   GAME_ID |    TEAM    |   PLAYER_ID | MIN   |   FGM |   FGA |   PTS |   REB |   AST |
|----------:|-----------:|------------:|:------|------:|------:|------:|------:|------:|
|  21900895 | MIL        |      202083 | 27:08 |     3 |    11 |     8 |     8 |     2 |
|  21900895 | MIL        |      203507 | 34:55 |    17 |    28 |    41 |    20 |     6 |
|  21900895 | MIL        |      201572 | 26:25 |     4 |    11 |    16 |     7 |     0 |
|  21900895 | MIL        |     1628978 | 27:35 |     1 |     5 |     2 |     7 |     5 |
|  21900895 | MIL        |      202339 | 22:17 |     2 |     8 |     4 |     1 |     2 |

To predict outcomes of games, this data was aggregated to contain teams and players cumulative statistics from all previous games each season. The new cumulative data has one row for each game with the average and total stats for each team and player going into the game. The script *regular_season_stats_running_and_totals.py* creates the cumulative statistics from *games.csv* and *games_details.csv*. The files, *teams_running.csv* and *players_running.csv* contain the cumulative statistics as well as the statistics in *games.csv* and *games_details.csv*. A slice of *teams_running.csv* with some of the home team statistics follows:


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

The files *teams_totals.csv* and *players_totals.csv* contain the end of the year statistics for each team and player. Some random rows from these datasets were cross-checked with the statistics at [basketball-reference.com](https://www.basketball-reference.com/) to ensure that no mistakes were made when in calculating the cumulative statistics. To my knowledge the cumulative statistics of a team or player from a specific date during a season are not publicly available, so the cumulative statistics could not be checked directly.

In order to easily use all of these statistics to predict games, *teams_running.csv* and *players_running.csv* were merged into one dataset that contains for each game the cumulative team and player statistics. The player columns were numbered from player 1 to player 16, and ordered by minutes played in the game the row represents. The script that merges *teams_running.csv* and *players_running.csv* is *merge_player_team.py*, which outputs the merged dataset as *full_stats_running.csv*.

# Betting Odds Data

The betting odds data was found at the website sportsbookreviewsonline.com, [here](https://www.sportsbookreviewsonline.com/scoresoddsarchives/nba/nbaoddsarchives.htm). It contains the betting odds for all regular and postseason games from the 2007-08 season through March of the 2019-20 season. For each game, the odds data contains the closing over/under, spread, and money lines odds. The data is organized as one csv file for each season. The 2007-08 season csv is titled *nba_odds_2007-08.csv* with the other seasons titled similarly. The first four games in the 2007-08 season are recorded as follows:

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

The odds data was organized into a new csv with one row for each game, and with the date and team names labeled as in *full_stats_running.csv*. In the new csv, the odds are translated into predictions for the score of the game and the probability of each team winning. The script that creates the new csv is *clean_odds_data.py*. It outputs one file for each season. The file for the 2007-08 season is titled *odds_2007.csv*, with the others titled similarly. The new files look as follows (these are the rows that correspond to the same four games as above):

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

# How good is Vegas at predicting NBA games?

The script *odds_analysis.py* does some analysis on how well Vegas predicts the outcomes of the games during this time period. In the data there are 15,211 games. Of these games, Vegas correctly predicted the winner 68.25% of the time.

The average score (home or away) error is 8.41 points, with 66.62% of the score predictions being within 10 points. 308 times either the home or away team's score is predicted exactly correct. Twice both the home and away teams score in the same game is predicted correctly. The average spread error is 6.98 points, with 35.26% of the spread predictions within 3 points. The average over/under prediction error is 13.83 points, with 45.65% of the over/under predictions within 10 points.

## Models and Predictions

# Pre-processing

In this section, I record the pre-processing that was done to all the data before making predictions along with some explanation for the conventions.

The first 10 games of each season for each team were taken out of the data for small sample size reasons. One could not hope to make good predictions based on the statistics during before these games.

To make the betting odds data and NBA games data match, the years before 2007 were taken out of the NBA games data, and any preseason and postseason games were removed from the NBA games data and betting odds data.

For each game and each team, only the top 9 players in order of minutes played were kept. This way only the more relevant players statistics are considered. One may disagree with the convention to apriori keep players based on their minutes played in the game one wants to predict. The reason for this convention is to attempt to recreate the information one has at the beginning of the game about the players that will play in the game. Using cumulative stats to decide which players to keep for each game do not capture when a player misses a game due to injury or suspension, while someone betting on the game (as well as Las Vegas when making the closing odds) has this information. A serious basketball fan could predict at the beginning of a game with good accuracy which 8 players on a team would play the highest minutes.

The script *pre_processing.py* does all to the *full_stats_running.csv* dataset, and then creates input and output dataframes to input into the machine learning models. It creates one input dataframe for player statistics, one for team statistics, and one for player and team statistics. The output dataframe is the column of *full_stats_running.csv* that says whether or not the home team won the game. This script also does the training, validation, and test splitting of the data, which is discussed in the following section.

The support vector machine and multi-layer perceptron models have the extra pre-processing step of the scaling the features to make them uniform. The data was scaled using ``StandardScaler`` from ``sklearn.preprocessing`` to make the columns have mean 0 and variance 1.

# Training and Validation

The naive models were run on all the games since there is no training and validation for these models.

For the machine learning models, the 2018-19 and 2019-20 seasons were held out as a test set, and the 2007-08 through 2017-18 seasons were split 80%, 20% for training and validation respectively. In the training, validation, and test data there are 9,113 games, 2,279 games, and 1,790 games respectively.

For each of the machine learning models, the model hyperparameters were tuned using the training and and validation data to avoid overfitting and underfitting. Each model has it's own script that does this, with obvious naming conventions. The script *test.py* runs all the models with the determined hyperparameters on the training, validation, and test data. For each of these models we record the percent correct on the training, validation, and test data.

# Naive Models

There are three naive prediction models:
* Points per game: predict the winner of the game by the team with the higher average points per game.
* Point differential: predict the winner of the game by the team with the higher average point differential. Average point differential is average points per game minus averaged points per game allowed.
* Winning percentage: predict the winner of the game by the team with the higher winning percentage.

The script that carries out the naive models is *naive_predictions.py*.

The results of baseline models and the Vegas odds predictions are recorded in the following table:

| Prediction Method | Percent Correct |
|-------------------|--------------------|
| Vegas Odds        | 68.25%             |
| Winning Percentage| 65.54%             |
| Point Differential| 65.49%             |
| Points Per Game   | 58.94%             |

Each of the naive models was also run using home and away splits for each team instead of the total average. This means for the home team, only their previous home game averages were used, and for the away team, only their previous away game averages. These are the results with the home and away splits:

| Using home and away splits | Percent Correct |
|------------------------|-----------------|
| Winning Percentage     | 66.12%          |
| Point Differential     | 57.58%          |
| Points per Game        | 55.35%          |

# Logistic Regression

``LogisticRegression`` from ``sklean.linear_model`` was used with the default parameters.

|Stats Group \  Percent Correct|Training Data|Validation Data|Test Data|
|-----------|----------|----------|----------|
|Player     | 70.57% | 67.40% | 73.63% |
|Team       | 67.68% | 67.79% | 67.09% |
|Player and Team | 70.67% | 68.19% | 73.91% |

# Nearest Neighbor

``KNeighborsClassifier`` from ``sklearn.neighbors`` was used with the number of neighbors parameter, ``n_neighbors=100``.

|Stats Group \  Percent Correct|Training Data|Validation Data|Test Data|
|-----------|----------|----------|----------|
|Player     | 67.92% | 66.78% | 66.42% |
|Team       | 68.32% | 67.49% | 67.04% |
|Player and Team | 68.44% | 67.53% | 67.09% |

# Support Vector Machine

``LinearSVC`` from ``sklearn.svm`` with regularization parameter ``C=1`` was used. Note: Various nonlinear support vector machines were used on the training and validation data, all performing similarly or worse than the linear support vector machine.

|Stats Group \  Percent Correct|Training Data|Validation Data|Test Data|
|-----------|----------|----------|----------|
|Player     | 70.59% | 67.44% | 73.46% |
|Team       | 67.85% | 67.88% | 66.98% |
|Player and Team | 70.67% | 68.32% | 73.41% |

# Multi-layer Perceptron (MLP)

Details of the model parameters: The model has 5 dense layers with the first through fifth layer having 100, 100, 50, 25, and 10 neurons respectively. For these 5 dense layers the activation function *tanh* is used. The output layer has 1 neuron with activation function *sigmoid* since binary classification is being done. For regularization, a dropout rate of 0.2 is used for each dense layer and an l2 regularization rate of 0.004 is used for every layer.

The model was made and ran using ``keras`` with the ``tensorflow`` backend.

|Stats Group \  Percent Correct|Training Data|Validation Data|Test Data|
|-----------|----------|----------|----------|
|Player     | 70.12% | 67.49% | 65.25% |
|Team       | 66.68% | 66.74% | 65.70% |
|Player and Team | 69.78% | 67.13% | 67.04% |

## Conclusions

All the models except the player MLP and team MLP models beat the best naive model. The player and the player and team logistic regression and support vector machine models beat the betting odds predictions on the test data, but the logistic regression and support vector machine numbers are a bit odd since the percentages on the test data are higher than the percentages on training and validation data. This is perhaps due to randomness, and the fact that the test data is relatively small. Another possible explanation is that the models are better at predicting some seasons over other seasons. A more season by season analysis is something to explore in the future, and could help explain this phenomenon.

In general, the models all performed better when using the player and the player and team statistics over using just the team statistics. This is not surprising because the player statistics are more detailed and numerous.

It is interesting that all of the models performed similarly on the training and validation data; none of them beating the betting odds predictions. The fact that all the models perform similarly suggests they are all finding similar patterns in the data, with logistic regression and the support vector machine perhaps doing a slightly better job.

The numbers on the predictions here are consistent with the survey of related work on the subject in section 2 of [[HSZ]](#HSZ) as well as being consistent with the predictions made in [[HSZ]](#HSZ).

## Future Work

There are many directions for future work with the project. One direction  is to do a finer analysis of the logistic regression and multi-layer perceptron models' predictions by considering the probabilities they output versus just rounding the probabilites to predict whether or not the home team will win. A way to do this would be to compare the probabilities the models output with the probabilities from the betting odds in order to devise a betting strategy. This is done in [[HSZ]](#HSZ), and I plan to explore betting possibilities in my next post.

# Reference

<a name="HSZ">[HSZ]</a> O. Hubáček, G Šourek, F. Železný, *Exploiting sports-betting market using machine learning*, International Journal of Forecasting, **35** (2019), 783-796.