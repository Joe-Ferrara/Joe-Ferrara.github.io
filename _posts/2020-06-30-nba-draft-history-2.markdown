---
layout: post
title:  "NBA Draft History: The Best and Worst Teams at Drafting"
comment_issue_id: ??
---

<style>
table {width:40%;
}
</style>

Using the Agg statistic I introduced in my [previous post](https://joe-ferrara.github.io/2020/06/28/nba-draft-history-1.html), in this post I do an analysis of the best and worst teams at drafting players. The goal of the analysis is to determine over any given five year period, the teams that were best at evaluating NBA prospects to draft. Because higher picks in the draft are more likely to net good players, to evaluate how good a pick is, the value of the pick is compared to the average value of a pick at that pick slot. I calculated the average Agg (AA) for each pick 1 through 60 using the drafts from 1969 to 2013. Then for a given draft pick, say team t chooses player p at pick n, to evaluate how good (or bad) the pick is, the difference between player p's Agg score and the average Agg score for pick n calculated. This difference is called the Agg Over Average (AOA). If the AOA is positive, team t made an above average pick; if it is negative, then team t made a below average pick.

The following table has the AA for the first 30 picks.

| Pick | AA      | Pick | AA      |
|------|---------|------|---------|
|    1 |    4.92 |   16 |    2.60 |
|    2 |    3.79 |   17 |    2.31 |
|    3 |    4.10 |   18 |    2.59 |
|    4 |    3.77 |   19 |    2.17 |
|    5 |    3.82 |   20 |    2.27 |
|    6 |    3.02 |   21 |    2.49 |
|    7 |    3.25 |   22 |    2.12 |
|    8 |    3.09 |   23 |    2.41 |
|    9 |    3.35 |   24 |    2.48 |
|   10 |    3.11 |   25 |    2.04 |
|   11 |    2.96 |   26 |    2.06 |
|   12 |    2.73 |   27 |    1.93 |
|   13 |    2.87 |   28 |    1.86 |
|   14 |    2.52 |   29 |    2.02 |
|   15 |    2.48 |   30 |    1.85 |

Lebron James was the first pick of the 2003 draft, and he has an Agg of 9.96, so his AOA is 9.96 - 4.92 = 5.04, since the AA for the first pick is 4.92.

It is interesting to compare the above table with the distribution of Agg. The mean and standard deviation of Agg for players drafted between 1969 and 2013 that played 100 or more games is 3.00 and 1.41 respectively. Looking at the table, the first pick has a much higher AA than any other pick, being more than one standard deviation above the mean. There is a clear second group of picks in slots 2-5 where the AA ranges from 3.77 - 4.10 netting above average players.  3.77 a little over half a standard deviation above the mean. The next clear grouping is picks 6-11, which range in AA from 2.96 to 3.35, right at the mean to slightly above it. After the 11th pick all the picks have an AA below the mean, with AA going down as picks get lower.

I used AOA to evaluate all the draft picks made in the top 60 from 1969 to 2013. The top twenty picks during this time period in terms of AOA are the following:

| Player (pick, team)                 | AOA  |
|-------------------------------------|------|
| John Stockton (16, UTA)             | 6.27 |
| Karl Malone (13, UTA)               | 5.87 |
| Manu Ginóbili (57, SAS)             | 5.47 |
| Dirk Nowitzki (9, DAL)              | 5.46 |
| Michael Jordan (3, CHI)             | 5.45 |
| Larry Bird (6, BOS)                 | 5.29 |
| Kobe Bryant (13, LAL)               | 5.20 |
| Julius Erving (12, PHI)             | 5.20 |
| Kevin Garnett (5, MIN)              | 5.07 |
| LeBron James (1, CLE)               | 5.04 |
| Kareem Abdul-Jabbar (1, LAL)        | 4.66 |
| Chris Paul (4, NOK)                 | 4.58 |
| Rudy Gobert (27, UTA)               | 4.49 |
| Maurice Cheeks (36, PHI)            | 4.36 |
| Clyde Drexler (14, POR)             | 4.34 |
| James Harden (3, OKC)               | 4.33 |
| Kawhi Leonard (15, SAS)             | 4.31 |
| Reggie Miller (11, IND)             | 4.26 |
| Paul Pierce (10, BOS)               | 4.24 |
| Giannis Antetokounmpo (15, MIL)     | 4.21 |

As is evident from the list, AOA is taking into account not just how good a career the player had, but also where the player was drafted. Manu Ginóbili, who was drafted 57th and had a great career, has the third best AOA.

To determine the best and worst teams at drafting over any five year period, I used the following method: For every team and every five year period of drafts starting with the period 1969 - 1974 and ending with the period 2009 - 2013, I calculated the sum of the AOA scores of the players drafted by each team. This sum gives for each team and each five year period a Score for how well the team drafted during that five year period. Below the teams and time periods that received the largest Scores are recorded. If the same team appeared multiple times at the top of the Scores list with overlapping time periods, then that team is recorded below once with their highest score used for ranking and the other overlapping scores noted. For each team in the list, I included the draft picks, their AOAs, the team's general manager(s) during the time period, and a few notes about the success of the team following the picks.

I used the same method to determine the worst teams at drafting over any five year period. For the worst teams, I restricted the data to five year periods since 1990, when the weighted NBA lottery system began. When running the calculations on all the years since 1969, most of the worst teams were from the 70s when there were less teams in the league. With less teams in the league, each team had more picks in the top 60 picks. This led to lower scores because each team had more unsuccessful picks, which also explains the lack of any team from the 70s in the top 10 for best teams at drafting.

## 10 Best Team Periods At Drafting

### Utah Jazz 1982 - 1986, Score 15.16

| Picks (year, pick)              | AOA |
|---------------------------------|------------|
| John Stockton (1984, 16)        |       6.27 |
| Karl Malone (1985, 13)          |       5.87 |
| Dell Curry (1986, 15)           |       1.17 |
| Carey Scurry (1985, 37)         |       1.13 |
| Bob Hansen (1983, 54)           |       0.96 |
| Jerry Eaves (1982, 55)          |       0.23 |
| Thurl Bailey (1983, 7)          |      -0.04 |
| Steve Trumbo (1982, 49)         |      -0.43 |

**General Manager**: Frank Layden (1979 - 1987)

1982 - 1986 marked the era when the Utah Jazz made two of the most valuable draft picks possible, drafting John Stockton in 1984 with the 16th pick and Karl Malone in 1985 with the 13th pick. Malone and Stockton went on to have remarkably long careers with the Jazz, making it to the NBA Finals in 1997 and 1998.

Overlapping notable periods:
* 1983 - 1987, score 13.88
* 1981 - 1985, score 13.51
* 1984 - 1988, score 12.44

###  Los Angeles Lakers 1992 - 1996, Score 15.01

| Picks (year, pick)              | AOA        |
|---------------------------------|------------|
| Kobe Bryant (1996, 13)          |        5.2 |
| Eddie Jones (1994, 10)          |       2.87 |
| Nick Van Exel (1993, 37)        |       2.39 |
| Doug Christie (1992, 17)        |       2.13 |
| Derek Fisher (1996, 24)         |       1.53 |
| Anthony Peeler (1992, 15)       |       0.82 |
| Anthony Miller (1994, 39)       |       0.74 |
| George Lynch (1993, 12)         |       0.65 |
| Duane Cooper (1992, 36)         |      -0.61 |
| Frankie King (1995, 37)         |      -0.71 |

**General Manager**: Jerry West (1982 - 2000)

Jerry West helped build the Showtime Lakers of the 80s, and then in the 90s, these draft picks laid the foundation for the Kobe-Shaq three-peat. While Eddie Jones, Nick Van Exel, and Doug Christie were not with the Lakers during the Kobe-Shaq three-peat , they were great picks.

Overlapping notable periods:
* 1993 - 1997, score 12.37
* 1990 - 1994, score 11.69
* 1989 - 1993, score 11.53
  * It is worth noting that Kobe, Eddie Jones, and Derek Fisher were not picked during the 1989 - 1993 period. This period included the notable draft picks Vlade Divac (AOA 3.46) and Elden Campbell (AOA 2.19), who were on the 1991 team that lost in the NBA Finals.

### Portland Trail Blazers 1982 - 1986, Score 11.93

| Picks (year, pick)              |  AOA  |
|---------------------------------|-------|
| Clyde Drexler (1983, 14)        |  4.34 |
| Terry Porter (1985, 24)         |  3.19 |
| Jerome Kersey (1984, 46)        |  2.58 |
| Arvydas Sabonis (1986, 24)      |  2.31 |
| Dražen Petrović (1986, 60)      |  1.92 |
| Fat Lever (1982, 11)            |  1.67 |
| Steve Colter (1984, 33)         |  1.10 |
| Kevin Duckworth (1986, 33)      |  0.39 |
| Audie Norris (1982, 37)         | -0.09 |
| Juden Smith (1986, 49)          | -0.43 |
| Bernard Thompson (1984, 19)     | -0.48 |
| Fernando Martín (1985, 38)      | -0.61 |
| George Montgomery (1985, 39)    | -0.63 |
| Linton Townes (1982, 33)        | -0.67 |
| Parragiotis Fasoulas (1986, 37) | -0.71 |
| Sam Bowie (1984, 2)             | -0.90 |
| Victor Fleming (1984, 26)       | -1.06 |

**General Managers**: Stu Inman (1981 - 1986) and Bucky Buckwalter (1986 - 1992)

Tacking place before the modern lottery era, Portland had a lot of picks during this time period. These drafts laid the foundation for an extremely successful Portland run, though they never won a championship. They made it to the NBA Finals in 1990 and 1992. It is amazing to get a score this high, while including the Sam Bowie pick, which was a notoriously bad pick taking him before Michael Jordan in the 1984 draft.

### Oklahoma City Thunder late 2007 - 2011, Score 11.81

| Picks (year, pick)            | AOA   |
|---------------------------------|-------|
| James Harden (2009, 3)          |  4.33 |
| Kevin Durant (2007, 2)          |  4.18 |
| Russell Westbrook (2008, 4)     |  3.12 |
| Serge Ibaka (2008, 24)          |  2.15 |
| Reggie Jackson (2011, 24)       |  1.08 |
| Magnum Rolle (2010, 51)         | -0.24 |
| Sasha Kaun (2008, 56)           | -0.40 |
| DeVon Hardin (2008, 50)         | -0.43 |
| Kyle Weaver (2008, 38)          | -0.61 |
| Trent Plaisted (2008, 46)       | -0.64 |
| Jeff Green (2007, 5)            | -0.72 |

**General Manager**: Sam Presti (2007 - present)

Taking over as the general manager of Seatlle SuperSonics in 2007 (to become the Oklahoma City Thunder in 2008), Sam Presti began one of the most remarkable runs of drafting a general manager has accomplished. Taking Kevin Durant, Russell Westbrook, and James Harden at the top of consecutive drafts (and in addition taking Serge Ibaka in 2008 at 24) should have led to as many championships as it did MVPs. Unfortunately, though each of those three players has won an MVP award, the most the Thunder accomplished was making it to the NBA Finals in 2012. Currently, none of the top 5 players on the above list are sill with the Thunder.

Overlapping notable periods:
* 2005 - 2009, score 10.97
* 2006 - 2010, score 10.73
* 2009 - 2013, score 9.46
  * This time period does not include Kevin Durant or Russell Westbrook. Sam Presti continued drafting valuable players taking Jeremy Lamb (AOA 1.04), Andre Roberson (AOA 0.87), and Alex Abrines (AOA 0.73) that do not appear on the above list.
* 2008 - 2012, score 9.13

### San Antonio Spurs late 1997 - 2001, Score 11.65

| Picks (year, pick)            | AOA   |
|---------------------------------|-------|
| Manu Ginóbili (1999, 57)        |  5.47 |
| Tim Duncan (1997, 1)            |  4.17 |
| Tony Parker (2001, 28)          |  3.32 |
| Jason Hart (2000, 49)           |  1.24 |
| Cory Hightower (2000, 54)       | -0.23 |
| Derrick Dial (1998, 52)         | -0.26 |
| Bryan Bracey (2001, 58)         | -0.31 |
| Chris Carrawell (2000, 41)      | -0.32 |
| Robertas Javtokas (2001, 56)    | -0.40 |
| Leon Smith (1999, 29)           | -1.02 |

**General Manager**: Gregg Popovich (1994 - 2002)

A time period where the historic trio of Tim Duncan, Manu Ginóbili, and Tony Parker were drafted. The Spurs would win 5 championships during Tim Duncan's career. While Gregg Popovich was the official general manager and coach of the Spurs during this time period, he also had the help of R.C Buford who was employed by the Spurs and would become general manager in 2002, contributing to another Spurs run later on this list.

Overlapping notable periods:
* 1996, score 9.04
* 1995, score 8.27

### Seattle SuperSonics 1986 - 1990, Score 10.59

| Players (year, pick)            | AOA   |
|---------------------------------|-------|
| Gary Payton (1990, 2)           |  3.58 |
| Shawn Kemp (1989, 17)           |  2.53 |
| Nate McMillan (1986, 30)        |  2.52 |
| Dana Barros (1989, 16)          |  1.60 |
| Steve Scheffler (1990, 39)      |  1.09 |
| Derrick McKey (1987, 9)         |  0.71 |
| Olden Polynice (1987, 8)        | -0.22 |
| Abdul Shamsid-Deen (1990, 53)   | -0.31 |
| Tommy Amaker (1987, 55)         | -0.31 |
| Lemone Lampley (1986, 38)       | -0.61 |

**General Manager**: Bob Witsitt (1986 - 1994)

Drafts that would lead to the last great time period for the Seattle SuperSonics before they left Seattle to become the Oklahoma City Thunder. Gary Payton and Shawn Kemp became superstars, and Nate McMillan became known as "Mr. Sonic", the trio led the Sonics to the NBA Finals in 1996.

### San Antonio Spurs 2007 - 2011, Score 10.55

| Picks (year, pick)              |  AOA  |
|---------------------------------|-------|
| Kawhi Leonard (2011, 15)        |  4.31 |
| George Hill (2008, 26)          |  2.78 |
| Tiago Splitter (2007, 28)       |  1.86 |
| Dāvis Bertāns (2011, 42)        |  1.82 |
| DeJuan Blair (2009, 37)         |  1.33 |
| Cory Joseph (2011, 29)          |  1.08 |
| Nando De Colo (2009, 53)        |  0.97 |
| Ádám Hanga (2011, 59)           | -0.04 |
| Jack McClinton (2009, 51)       | -0.24 |
| Georgios Printezis (2007, 58)   | -0.31 |
| James Gist (2008, 57)           | -0.33 |
| Ryan Richards (2010, 49)        | -0.43 |
| Derrick Byars (2007, 42)        | -0.48 |
| Malik Hairston (2008, 48)       | -0.50 |
| James Anderson (2010, 20)       | -0.60 |
| Marcus Williams (2007, 33)      | -0.67 |

**General Manager**: R.C. Buford (2002 - present)

These drafts allowed the Spurs to continue their success as Duncan, Ginóbili, and Parker aged. George Hill was a great picked that the Spurs traded three years later for an even better pick in Kawhi Leonard. Leonard was fundamental to the 2012-13 and 2013-14 Spurs that went to the Finals, winning MVP of the 2014 Finals. Tiago Splitter and Cory Joseph also contributed to those Finals teams.

Overlapping notable periods:
* 2008, score 10.11

### Houston Rockets 2007 - 2011, Score 9.48

| Players (year, pick)            | AOA |
|---------------------------------|-------|
| Patrick Beverley (2009, 42)     |  2.06 |
| Chandler Parsons (2011, 38)     |  2.04 |
| Carl Landry (2007, 31)          |  1.58 |
| Chase Budinger (2009, 44)       |  1.33 |
| Ömer Aşık (2008, 36)            |  1.13 |
| Patrick Patterson (2010, 14)    |  1.01 |
| Marcus Morris (2011, 14)        |  0.79 |
| Aaron Brooks (2007, 26)         |  0.52 |
| Joey Dorsey (2008, 33)          |  0.25 |
| Donatas Motiejūnas (2011, 20)   | -0.19 |
| Maarty Leunen (2008, 54)        | -0.23 |
| Brad Newley (2007, 54)          | -0.23 |
| Jermaine Taylor (2009, 32)      | -0.59 |

**General Manager**: Daryl Morey (2007 - present)

Daryl Morey took over as general manager for the Rockets in 2007, and is now known as Dork Elvis for bringing a new emphasis on the role of analytics in basketball decisions. These draft picks are particularly remarkable because none of the picks are in the top 13. Known for getting the most value in any deal and valuing asset acquisition, these picks are emblematic of Morey's philosophy.

Overlapping notable periods:
* 2006 - 2010, score 8.43

### Memphis Grizzlies 2005 - 2009, Score 9.00

| Picks (year, pick)             |  AOA |
|--------------------------------|-------|
| Marc Gasol (2007, 48)          |  3.91 |
| Kyle Lowry (2006, 24)          |  3.29 |
| DeMarre Carroll (2009, 27)     |  1.46 |
| Mike Conley (2007, 4)          |  1.18 |
| Rudy Gay (2006, 8)             |  1.03 |
| Sam Young (2009, 36)           |  0.42 |
| Nick Calathes (2009, 45)       |  0.38 |
| Hakim Warrick (2005, 19)       |  0.34 |
| Darrell Arthur (2008, 27)      |  0.29 |
| Lawrence Roberts (2005, 55)    | -0.31 |
| O.J. Mayo (2008, 3)            | -1.37 |
| Hasheem Thabeet (2009, 2)      | -1.63 |

**General Managers**: Jerry West (2002 - 2007) and Chris Wallace (2007 - 2012)

Jerry West makes another appearance, though he cannot take credit for all of these picks. The top player on this list, Marc Gasol was a throw in from the Lakers in the Pau Gasol trade. This era also has Hasheem Thabeet, a notoriously bad pick, and O.J. Mayo who was not a very good pick either. The Grizzlies teams these picks led to had some success but never made it farther than the Western Conference Finals. They had a cult following though, and the period of success was known as the Grit and Grind Era.

### Chicago Bulls 2007 - 2011, Score 8.62

| Picks (year, pick)              | AOA |
|---------------------------------|-------|
| Jimmy Butler (2011, 30)         |  4.20 |
| Taj Gibson (2009, 26)           |  1.85 |
| Joakim Noah (2007, 9)           |  1.42 |
| Nikola Mirotić (2011, 23)       |  1.23 |
| James Johnson (2009, 16)        |  0.83 |
| Aaron Gray (2007, 49)           |  0.34 |
| Jameson Curry (2007, 51)        | -0.24 |
| Derrick Rose (2008, 1)          | -1.00 |

**General Managers**: John Paxson (2003 - 2009) and Gar Forman (2009 - 2020)

Considering that Derrick Rose was a much better pick than AOA is reflecting here, this was a great string of picks by the Bulls. These Bulls are a story of what could have been, having injuries to Derrick Rose preventing them from potentially making it to the Finals and/or winning a championship.

## 10 Worst Team Periods at Drafting

### Toronto Raptors 2004 -  2008, Score -8.16

| Picks (year, pick)              | AOA |
|---------------------------------|------------|
| Rafael Araújo (2004, 8)         |      -2.64 |
| Andrea Bargnani (2006, 1)       |      -2.51 |
| Joey Graham (2005, 16)          |      -0.84 |
| Albert Miralles (2004, 39)      |      -0.63 |
| Charlie Villanueva (2005, 7)    |       -0.5 |
| Edin Bavčić (2006, 56)          |       -0.4 |
| Roko Ukić (2005, 41)            |      -0.32 |
| Uroš Slokar (2005, 58)          |      -0.31 |

**General Managers**: Jack McCloskey (2004), Bob Babcock (2004 - 2006), Wayne Embry (2006), and Bryan Colangelo (2006 - 2013)

Bizarrely having four general managers during this time period (according to basketball-reference.com), this was a terrible string of picks. Andrea Bargnani is still talked about frequently today as a bad pick. Somehow Rafael Araújo gets a worse score than Bargnani. No pick during this 5 year span has positive AOA, which is hard to do. Chris Bosh, picked by the Raptors in 2003 would have had a better time in Toronto had some of these picks returned positive value.

Overlapping notable periods:
* 2002 - 2006, score -5.90

### Los Angeles Clippers 2003 - 2007, Score -7.83

| Picks (year, pick)               | AOA |
|----------------------------------|------------|
| Yaroslav Korolev (2005, 12)      |      -1.73 |
| Al Thornton (2007, 14)           |      -1.01 |
| Shaun Livingston (2004, 4)       |      -0.85 |
| Jared Jordan (2007, 45)          |       -0.8 |
| Lionel Chalmers (2004, 33)       |      -0.67 |
| Chris Kaman (2003, 6)            |      -0.54 |
| Paul Davis (2006, 34)            |      -0.51 |
| Nick Fazekas (2007, 34)          |      -0.51 |
| Sofoklis Schortsanitis (2003, 34)|      -0.51 |
| Guillermo Díaz (2006, 52)        |      -0.26 |
| Cheikh Samb (2006, 51)           |      -0.24 |
| Daniel Ewing (2005, 32)          |       -0.2 |

**General Manager**: Elgin Baylor (1986 - 2008)

The Clippers whom were almost always terrible, amazingly make it on this list three times. That means they have 3 non-overlapping five year periods of terrible draft picks. Elgin Baylor was the general manager for all three of these periods. At the end of Elgin Baylor's time as general manager, this was the worst period.

### New York Knicks 1999 - 2003, Score -7.40

| Picks (year, pick)              | AOA |
|---------------------------------|------------|
| Frederic Weis (1999, 15)        |      -1.48 |
| Mike Sweetney (2003, 9)         |      -1.11 |
| Frank Williams (2002, 25)       |      -1.04 |
| J.R. Koch (1999, 46)            |      -0.64 |
| Michael Wright (2001, 39)       |      -0.63 |
| Slavko Vraneš (2003, 39)        |      -0.63 |
| Lavor Postell (2000, 39)        |      -0.63 |
| Eric Chenowith (2001, 43)       |      -0.63 |
| Milos Vujanic (2002, 36)        |      -0.61 |

**General Managers** Dave Checketts (1999) and Scott Layden (1999 - 2003)

The Knicks made the Finals in 1999, and have been mostly bad since. Hitting on a few of these draft picks certainly would have helped continue their success as they did make the Eastern Conference Finals in 2000 and the playoffs in 2001.

Overlapping notable periods:
* 1998 - 2002, score -6.26

### Phoenix Suns 2009 - 2013, Score -6.06

| Picks (year, pick)            | AOA |
|---------------------------------|------------|
| Kendall Marshall (2012, 13)     |      -1.57 |
| Alex Len (2013, 5)              |      -0.95 |
| Earl Clark (2009, 14)           |      -0.91 |
| Gani Lawal (2010, 46)           |      -0.64 |
| Archie Goodwin (2013, 29)       |      -0.56 |
| Taylor Griffin (2009, 48)       |       -0.5 |
| Emir Preldžić (2009, 57)        |      -0.33 |
| Alex Oriakhi (2013, 57)         |      -0.33 |
| Dwayne Collins (2010, 60)       |      -0.33 |
| Markieff Morris (2011, 13)      |       0.07 |

**General Managers** Steve Kerr (2007 - 2010), Lance Blanks (2010 - 2013), Lon Babby (2013), Ryan McDonough (2013 - 2018)

No notoriously bad picks here, just a string of players that were not good in the NBA and a lot of general managers. These years overlapped with the tail end of the Steve Nash era in Phoenix, and led to a long time of mediocrity and general blandness for the Suns.

### Los Angeles Clippers 1996 - 2000, Score -5.39

| Picks (year, pick)            | AOA |
|---------------------------------|------------|
| Michael Olowokandi (1998, 1)    |      -3.48 |
| Darius Miles (2000, 3)          |      -1.54 |
| Mamadou N'Diaye (2000, 26)      |      -1.06 |
| Rico Hill (1999, 31)            |      -0.92 |
| Doron Sheffer (1996, 36)        |      -0.61 |
| James Collins (1997, 36)        |      -0.61 |
| Maurice Taylor (1997, 14)       |      -0.55 |
| Lorenzen Wright (1996, 7)       |      -0.41 |
| Keyon Dooling (2000, 10)        |      -0.37 |
| Charles Smith (1997, 26)        |        0.0 |
| Quentin Richardson (2000, 18)   |       0.89 |
| Marko Jarić (2000, 30)          |        0.9 |
| Tremaine Fowlkes (1998, 54)     |       1.02 |
| Lamar Odom (1999, 4)            |       1.34 |

**General Manager**: Elgin Baylor (1986 - 2008)

Second time that Elgin Baylor's clippers are appearing. Michael Olowokandi was a notoriously bad pick at the time that is still talked about today. Bunch of other bad picks on here, but also some decent picks as well. Lamar Odom and Quentin Richardson went on to have good NBA careers.

### Denver Nuggets 2001 - 2005, Score -5.37

| Picks (year, pick)            | AOA |
|---------------------------------|------------|
| Nikoloz Tskitishvili (2002, 5)  |      -3.37 |
| Julius Hodge (2005, 20)         |      -1.27 |
| Vincent Yarbrough (2002, 33)    |      -0.67 |
| Jamal Sampson (2002, 47)        |      -0.66 |
| Ousmane Cisse (2001, 47)        |      -0.66 |
| Sani Bečirovič (2003, 46)       |      -0.64 |
| Axel Hervelle (2005, 52)        |      -0.26 |
| Kenny Satterfield (2001, 54)    |      -0.23 |
| Linas Kleiza (2005, 27)         |       0.26 |
| Carmelo Anthony (2003, 3)       |       0.96 |
| Nenê Hilário (2002, 7)          |       1.17 |

**General Managers**: Dan Issel (1998 - 2001) and Kiki Vandeweghe (2001 - 2006)

Nikoloz Tskitishvili is the first cautionary tale of taking a European prospect based on workout tapes, and not much legitimate game footage. He was a historically bad pick. This list has Carmelo Anthony at 0.96 AOA, showing that Agg perhaps does not value him enough. Advanced statistics have never been kind to Carmelo Anthony.

### Minnesota Timberwolves 2009 - 2013, Score -5.32

| Picks (year, pick)            | AOA |
|---------------------------------|------------|
| Jonny Flynn (2009, 6)           |      -2.15 |
| Wesley Johnson (2010, 4)        |      -1.46 |
| Derrick Williams (2011, 2)      |      -1.26 |
| Lazar Hayward (2010, 30)        |      -0.85 |
| Paulo Prestes (2010, 45)        |       -0.8 |
| Henk Norel (2009, 47)           |      -0.66 |
| Malcolm Lee (2011, 43)          |      -0.63 |
| Hamady N'Diaye (2010, 56)       |       -0.4 |
| Robbie Hummel (2012, 58)        |      -0.31 |
| Shabazz Muhammad (2013, 14)     |      -0.08 |
| Ricky Rubio (2009, 5)           |      -0.06 |
| Bojan Dubljević (2013, 59)      |      -0.04 |
| Wayne Ellington (2009, 28)      |       0.73 |
| Nemanja Bjelica (2010, 35)      |       1.28 |
| Gorgui Dieng (2013, 21)         |       1.37 |

**General Managers** David Kahn (2009 - 2013) and Flip Saunders (2013 - 2015)

The infamous Kahn era in Minnesota. Three bad picks enar the top of the draft in Jonny Flynn, Wesley Johnson, and Derrick Williams. He also took Jonny Flynn and Ricky Rubio, two point gaurds, ahead of Steph Curry in 2009. Flip Saunders took over in 2013 and made some of the better picks at the bottom of this list, showing just how bad Kahn's era was.

### Chicago Bulls 2000 - 2004, Score -5.31

| Picks (year, pick)            | AOA |
|---------------------------------|------------|
| Jay Williams (2002, 2)          |      -2.79 |
| Marcus Fizer (2000, 4)          |      -2.07 |
| Dalibor Bagarić (2000, 24)      |      -1.48 |
| Eddy Curry (2001, 4)            |      -1.38 |
| Ben Gordon (2004, 3)            |      -1.04 |
| Mario Austin (2003, 36)         |      -0.61 |
| A.J. Guyton (2000, 32)          |      -0.59 |
| Khalid El-Amin (2000, 34)       |      -0.51 |
| Tommy Smith (2003, 53)          |      -0.31 |
| Trenton Hassell (2001, 30)      |       0.15 |
| Lonny Baxter (2002, 44)         |       0.22 |
| Kirk Hinrich (2003, 7)          |       0.35 |
| Roger Mason (2002, 31)          |       0.46 |
| Tyson Chandler (2001, 2)        |       0.99 |
| Luol Deng (2004, 7)             |        1.0 |
| Chris Duhon (2004, 38)          |       1.07 |
| Jamal Crawford (2000, 8)        |       1.22 |

**General Managers** Jerry Krause (1985 - 2003) and John Paxson (2003 - 2009)

A lot of bad picks near the top of the draft. Some of this is Jerry Krause's work to try and make a good Bulls team post Michael Jordan leaving (whom Krause did not want to bring back). Jay Williams could have been good before an unfortunate motorcycle accident basically ended his career.

### Los Angeles Clippers 1990 - 1994, Score -5.30

| Picks (year, pick)            | AOA |
|---------------------------------|------------|
| Bo Kimble (1990, 8)             |      -2.42 |
| LeRon Ellis (1991, 22)          |      -1.12 |
| Elmore Spencer (1992, 25)       |      -0.93 |
| Terry Dehere (1993, 13)         |      -0.78 |
| Randy Woods (1992, 16)          |      -0.75 |
| Joe Wylie (1991, 38)            |      -0.61 |
| Lamond Murray (1994, 7)         |       -0.5 |
| Matt Fish (1992, 50)            |      -0.43 |
| Leonard White (1993, 53)        |      -0.31 |
| Tony Massenburg (1990, 43)      |       0.16 |
| Loy Vaught (1990, 13)           |       0.27 |
| Elliot Perry (1991, 37)         |       1.03 |
| Eric Piatkowski (1994, 15)      |       1.09 |

**General Manager**: Elgin Baylor (1986 - 2008)

Another terrible Clippers run, this time from an earlier park of Elgin Baylor's career as their manager.

### Portland Trail Blazers 2000 - 2004, Score -5.29

| Picks (year, pick)             | AOA |
|----------------------------------|-------|
| Sergei Monia (2004, 23)          | -1.41 |
| Sebastian Telfair (2004, 13)     | -1.32 |
| Qyntel Woods (2002, 21)          | -0.95 |
| Erick Barkley (2000, 28)         | -0.86 |
| Viktor Khryapa (2004, 22)        | -0.71 |
| Ha Seung-Jin (2004, 46)          | -0.64 |
| Jason Jennings (2002, 43)        | -0.63 |
| Ruben Boumtje-Boumtje (2001, 50) | -0.43 |
| Federico Kammerichs (2002, 51)   | -0.24 |
| Nedžad Sinanović (2003, 54)      | -0.23 |
| Travis Outlaw (2003, 23)         |  0.02 |
| Zach Randolph (2001, 19)         |  2.11 |

**General Managers**: Bob Whitsitt (1994 - 2003) and John Nash (2003 - 2006)

No extraordinarily bad picks, but a lot of bad picks. The Blazers almost made it to the NBA Finals in 2000. This is another case where if they hit on a couple of these picks, it would have helped the team continue its success.
