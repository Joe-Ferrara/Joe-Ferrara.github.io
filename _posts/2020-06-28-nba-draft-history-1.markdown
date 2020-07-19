---
layout: post
title:  "The Aggregate Statistic"
comment_issue_id: 15
sub: "draft"
---

<style>
table {width:50%;
}
</style>

The goal of this NBA Draft History project is to do a statistical analysis on the history of the NBA draft. To do this, I scraped 70 years of NBA draft history from [basketball-reference.com](https://www.basketball-reference.com/) and pipelined it to a MySQL relational database I created on my computer. The NBA drafts ranged from the 1947 draft to the 2019 draft. For each draft, the main table from the basketball-reference.com page for that draft was recorded. For example, the basketball-reference.com page for the 2003 draft can be found [here](https://www.basketball-reference.com/draft/NBA_2003.html). In addition, for any player drafted between 1967 and 2019 who played 1 or more years in the NBA, the per game statistics for each year that player played were scraped and recorded in the MySQL database. An example of the per game data for Lebron James can be found [here](https://www.basketball-reference.com/players/j/jamesle01.html).

The scraping and pipelining was done using the Python library Scrapy, and the MySQL database creation and editing was done using MySQL Connector for Python. The code for the project is available on my github, [github.com/Joe-Ferrara/nba-draft-history](https://github.com/Joe-Ferrara/nba-draft-history). The github page has detailed descriptions of the files and what they do.

For the rest of this post, I explain the aggregate statistic I created. For any player drafted in the top 60 picks between 1969 and 2013, the aggregate statistic gives a number between 0 and 10 that evaluates the entirety of the player's career in the NBA. This aggregate statistic is then used to do an analysis of the teams historically best at drafting NBA players and colleges historically best at producing NBA players. This analysis will be the subject of two subsequent posts for this project.

### The Aggregate Statistic

The goal of the aggregate statistic is to give one number for each player that represents the career value of that player. For a given player, I created this aggregate statistic from the statistics in the draft history data. These statistics fall into three categories: Longevity, Standard, and Advanced. The Longevity statistics are total years played, total games played, and total minutes played. The Standard statistics are total points, total rebounds, total assists, career field goal percentage, career three-points shooting percentage, career free throw shooting percentage, career minutes per game, career points per game, career rebounds per game, and career assists per game. The Advanced statistics are win shares (WS), win shares per 48 minutes (WS/48), box score plus minus (BPM), and value above replacement player (VORP).

To make the aggregate statistic, I focused on the Longevity and Advanced statistics. While the Standard statistics are useful, they focuses too much on offensive production, and the important aspects of the Standard statistics are accounted for in the Advanced statistics. The Advanced statistics are useful because they each measure something slightly different in an attempt to give a number that represents the value of a player over his career. The all time leaders for each Advanced statistic are found on basketball-reference.com at the following links: [win shares](https://www.basketball-reference.com/leaders/ws_career.html), [win shares per 48 minutes](https://www.basketball-reference.com/leaders/ws_per_48_career.html), [box score plus minus](https://www.basketball-reference.com/leaders/bpm_career.html), and [value above replacement player](https://www.basketball-reference.com/leaders/vorp_career.html).

The philosophy of my approach to make the aggregate statistic is wisdom of the crowd. I wanted to combine in a sensible way all of the Advanced and Longevity statistics to produce one number between 0 and 10 that evaluates a player's career. I did this in three steps. First, I created an Agg1 statistic. Second, I created an Agg2 statistic. Agg1 and Agg2 are each slightly different aggregates of the Advanced and Longevity statistics. Third, I created the final aggregate statistic, called Agg, which is the average of Agg1 and Agg2.

The players used to to create Agg are the players drafted during the years 1969 - 2013 in the top 60 picks who appeared in 100 or more NBA games. The year 1969 was chosen because it is after territorial picks were eliminated from the NBA draft and is the year Kareem Abdul-Jabbar was drafted. I stopped at the year 2013 because for more recent drafts it is difficult to evaluate a player's career since it is ongoing. By including drafts up to 2013, an Agg statistic is still established for a number of active players like Stephen Curry and Giannis Antetokounmpo, as their careers are more established than those of players drafted more recently. Only the top 60 picks were used because in the modern NBA draft there are only 60 picks. The 100 games restriction makes it so that only players that appeared in at least a full season of NBA games are considered. A large portion of NBA draft picks do not appear in many games, and the Advanced statistics can be thrown off for players who appear in very few games. The players drafted in the top 60 that appear in less than 100 games are put back into the data and assigned a low Agg score when doing the draft analysis in my following posts.

#### Aggregate Statistic 1

Using the wisdom of the crowd philosophy to get the good qualities from the statistics without relying too much on any individual statistic, Agg1 consists of an average of the Longevity and Advanced statistics. Since each of the statistics has a different range of values, taking a direct average is not ideal because the statistics with a higher range of values will have a greater impact on the final number than the statistics with a smaller range of values. Therefore, all the statistics were min/max normalized over all the players so that each falls in the range 0 to 1.

After normalizing, for the Advanced statistics an average was taken.

To incorporate the Longevity statistics I did something slightly different. The reason for including the Longevity statistics is that they are an important aspect of the value of draft pick that is not emphasized enough in the Advanced statistics. In addition to the Longevity statistics mentioned above, I also added a statistic to account for games missed because of injury. This statistic is average games per year. Average games per year is the players total games played divided by 82 times total years played. There are now four Longevity statistics: years played (Y), games played (G), minutes played (M), and average games per year (G/Y). To incorporate these Longevity statistics into the aggregate statistic without having too large of an impact, I took the average of the Longevity statistics, and then made them 10% of the aggregate statistic.

Finally, for aesthetic reasons, I made the aggregate statistic fall between 0 and 10.

Given an Advanced or Longevity statistic, WS, WS/48, BPM, VORP, Y, G, M, G/Y, the normalized statistic is denoted with a subscript n (so WS<sub>n</sub>, WS/48<sub>n</sub>, BPM<sub>n</sub>, etc). Then Agg1 is determined by the following formula:

Agg1 = (1/4)\*(Y<sub>n</sub> + G<sub>n</sub> + M<sub>n</sub> + G/Y<sub>n</sub>) + (9/4)\*(WS<sub>n</sub> + WS/48<sub>n</sub> + BPM<sub>n</sub> + VORP<sub>n</sub>).

To evaluate Agg1, I used it to produce a list of the top 20 players drafted between 1969 and 2013:

| Rank  | Player                |Agg1 |
|-------|-----------------------|------|
|    1. | LeBron James          | 9.36 |
|    2. | Michael Jordan        | 8.95 |
|    3. | Kareem Abdul-Jabbar   | 8.60 |
|    4. | John Stockton         | 8.34 |
|    5. | Karl Malone           | 8.23 |
|    6. | Tim Duncan            | 7.90 |
|    7. | Chris Paul            | 7.89 |
|    8. | David Robinson        | 7.85 |
|    9. | Kevin Garnett         | 7.72 |
|   10. | Dirk Nowitzki         | 7.61 |
|   11. | Charles Barkley       | 7.46 |
|   12. | Magic Johnson         | 7.43 |
|   13. | Shaquille O'Neal      | 7.29 |
|   14. | Larry Bird            | 7.08 |
|   15. | Kobe Bryant           | 7.05 |
|   16. | Kevin Durant          | 6.96 |
|   17. | Hakeem Olajuwon       | 6.88 |
|   18. | James Harden          | 6.87 |
|   19. | Reggie Miller         | 6.76 |
|   20. | Clyde Drexler         | 6.57 |

This list decently parallels what one would imagine are the top players of the given time period. In any list of the top players since 1969, the top three, in any order, should be LeBron James, Michael Jordan, and Kareem Abdul-Jabbar, which this list gets correct. In this list, there are no huge outliers; all the players had great NBA careers, and are or will be in the NBA Hall of Fame. The main drawback I see to this list is that it overvalues the modern player. In particular, Magic Johnson and Larry Bird should be higher, and there should be more players from the 1970s and 1980s.

One drawback I should mention of any list I create is that it will only account for career regular season statistics. The lists cannot take into account the playoffs or how many championships a player won. This causes players like Karl Malone and John Stockton who had very long careers with great statistics to always score very high on my lists, even though they never won a championship. For these reasons the lists I produce will always have some discrepancy with lists created by basketball historians and/or media outlets that value playoff and championship success.

#### Aggregate Statistic 2

For Agg2, I tried to address the Larry Bird and Magic Johnson problem of Agg1 - they should be higher on the list and the list should have more players from the 1970s and 1980s. To create Agg2, I took a similar approach to Agg1 in terms of statistics used and each statistic's contribution to the final score, but I changed how the statistics were normalized. To make a player's score more reflective of how good or bad that player was in his era, instead of normalizing each statistic across all drafts from 1969 - 2013, I normalized each statistic across the five drafts closest to the draft in question. That is, if a player was drafted in 2003, then his statistics were min/max normalized within the pool of players drafted in 2001, 2002, 2003, 2004, and 2005 for Agg2. I will denote a statistic normalized this way with a subscript n, 5. Agg2 is then determined by the formula

Agg2 = (1/4)\*(Y<sub>n,5</sub> + G<sub>n,5</sub> + M<sub>n,5</sub> + G/Y<sub>n,5</sub>) + (9/4)\*(WS<sub>n,5</sub> + WS/48<sub>n,5</sub> + BPM<sub>n,5</sub> + VORP<sub>n,5</sub>).

The list of top 20 players determine by Agg2 follows:

|Rank | Player                |Agg2  |
|-----|-----------------------|------|
|  1. | Kareem Abdul-Jabbar   | 9.97 |
|  2. | LeBron James          | 9.89 |
|  3. | Shaquille O'Neal      | 9.86 |
|  4. | Tim Duncan            | 9.78 |
|  5. | Magic Johnson         | 9.72 |
|  6. | Julius Erving         | 9.63 |
|  7. | Anthony Davis         | 9.62 |
|  8. | James Harden          | 9.58 |
|  9. | Kevin Garnett         | 9.56 |
| 10. | Michael Jordan        | 9.55 |
| 11. | Dirk Nowitzki         | 9.52 |
| 12. | Larry Bird            | 9.13 |
| 13. | Damian Lillard        | 8.95 |
| 14. | John Stockton         | 8.86 |
| 15. | David Robinson        | 8.81 |
| 16. | Karl Malone           | 8.72 |
| 17. | Kobe Bryant           | 8.69 |
| 18. | Kevin Durant          | 8.58 |
| 19. | Stephen Curry         | 8.33 |
| 20. | Chris Paul            | 8.31 |

This list again is pretty successful, but also has some drawbacks. Magic Johnson now appears in the top 5, and Larry Bird has moved up 2 spots. We also see that Julius Erving is ranked number 6, whereas he did not appear in the previous list. Unfortunately, Michael Jordan has moved down to number 10, which is far too low, and Hakeem Olajuwon has disappeared from the list. Other benefits of this list are that John Stockton and Karl Malone have moved down and Shaquille O'Neal has moved up.

#### Aggregate Statistic

To make my final statistic, I min/max normalized Agg1 and Agg2 to be more similarly distributed in the range 0 to 10 (Agg2 doesn't have as many scores close to 10 as Agg1 does), and then took the average. If the normalized Agg1 and Agg2 are denoted Agg1<sub>n</sub> and Agg2<sub>n</sub>, then the final aggregate statistic, Agg, is given by by the following formula

Agg = (Agg1<sub>n</sub> + Agg2<sub>n</sub>)/2.

The list of top 20 players according to Agg follows:

|Rank | Player               |Agg|
|-----|----------------------|--------|
|  1. | LeBron James           | 9.96 |
|  2. | Kareem Abdul-Jabbar    | 9.58 |
|  3. | Michael Jordan         | 9.56 |
|  4. | Tim Duncan             | 9.10 |
|  5. | Kevin Garnett          | 8.89 |
|  6. | John Stockton          | 8.87 |
|  7. | Magic Johnson          | 8.81 |
|  8. | Dirk Nowitzki          | 8.81 |
|  9. | Shaquille O'Neal       | 8.80 |
| 10. | Karl Malone            | 8.74 |
| 11. | David Robinson         | 8.57 |
| 12. | James Harden           | 8.43 |
| 13. | Chris Paul             | 8.34 |
| 14. | Larry Bird             | 8.31 |
| 15. | Kobe Bryant            | 8.07 |
| 16. | Kevin Durant           | 7.96 |
| 17. | Julius Erving          | 7.93 |
| 18. | Charles Barkley        | 7.86 |
| 19. | Anthony Davis          | 7.83 |
| 20. | Stephen Curry          | 7.39 |

While this list has its pros and cons as well, I think it is better than the ones produced by Agg1 and Agg2. It has the correct top 3 players, and Tim Duncan is arguably the fourth best player since 1969. Some players are perhaps too high because of their lack of playoff success that Agg cannot account for. Overall, I like this group of 20. For the utility of Agg, it is more important that the group of 20 is solid without outliers than having the exact order perfect since this statistic will be used to evaluate all players.

Here is some more information about Agg. There were 1,526 players drafted between 1969 and 2013 that played (or have played) in 100 or more games. The mean of Agg is 3.00 and the standard deviation is 1.41. The top 99 percentile of players have an Agg score of 7.95 or above and the bottom 1 percentile of players have an Agg score of 0.72 or below. A histogram of the Agg scores follows:

![image](/pictures/agg_stat.png "Histogram of the Agg Stat")

To do the draft analysis in my next two posts, players drafted between 1969 and 2013 that played less than 100 career games are put back into the dataset with an Agg score of 1.0. This puts them in the bottom 3 percentile of players, making them recorded as an unsuccessful draft pick.

#### ESPN's Top 20

Recently, ESPN created a list of the top 74 players in NBA history, which can be found [here (top 10)](https://www.espn.com/nba/story/_/id/29105801/ranking-top-74-nba-players-all-nos-10-1), [here (11-40)](https://www.espn.com/nba/story/_/id/29105681/ranking-top-74-nba-players-all-nos-40-11), and [here (41-74)](https://www.espn.com/nba/story/_/id/29105574/nbarank-players-top-74-74-41). To compare with Agg's top 20, I listed below the 20 players drafted between 1969 and 2013 according to ESPN. ESPN's actual list considers all NBA seasons, so there is some discrepancy between ESPN's list and what appears here because I have taken out players drafted before 1969 (and Moses Malone who came over from the ABA). In parenthesis on the following list is the ranking of each player given by Agg.

| Rank | Player (Rank from Agg Stat) |
|------|-----------------------------|
|   1. | Michael Jordan (3) |
|   2. | Lebron James (1) |
|   3. | Kareem Abdul-Jabbar (2) |
|   4. | Magic Johnson (7) |
|   5. | Larry Bird (14) |
|   6. | Tim Duncan (4) |
|   7. | Kobe Bryant (15) |
|   8. | Shaquille O'Neal (9) |
|   9. | Hakeem Olajuwon (26) |
|  10. | Stephen Curry (20) |
|  11. | Kevin Durant (16) |
|  12. | Julius Erving (17) |
|  13. | Karl Malone (10) |
|  14. | Dirk Nowitzki (8) |
|  15. | Kevin Garnett (5) |
|  16. | Scottie Pippen (41) |
|  17. | Charles Barkley (18) |
|  18. | David Robinson (11) |
|  19. | Kawhi Leonard (32) |
|  20. | Dwayne Wade (42) |

ESPN's top 20 and Agg's top 20 have 16 players in common. Agg1 and Agg2's top 20 each have 15 players in common with ESPN's list.
