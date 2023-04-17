# March Madness Simulation

## Data Sets

### [ESPN's "Who Picked Whom"](https://fantasy.espn.com/tournament-challenge-bracket/2023/en/whopickedwhom)

This data was retrieved as historically far back as possible: the 2023, 2022, 2021, 2019, and 2018 tournaments. It was readily available on ESPN’s website to be converted into a .csv file, but since the start of the 2023 tournament is no longer available online past 2022 and has been stored locally. It contains the team seed, name, and percentage of users who selected the team to advance in each round.

### [FiveThirtyEight's March Madness Predictions](https://projects.fivethirtyeight.com/2023-march-madness-predictions/)

This data was retrieved for the 2023, 2022, 2021, 2019, and 2018 tournaments. It was readily available on FiveThirtyEight’s website to be converted into a .csv file and was only retrieved from 2018-2023 since this is the range available for EPSN’s data set. It contains the team seed, name, predicted probability to advance in each round, the date the forecast was created, and other miscellaneous information. 

### [KenPom Ratings](https://kenpom.com/)

This data was retrieved for the 2023, 2022, 2021, 2019, 2018, and 2017 tournaments. A web scraper was created internally to easily access this data and was retrieved from 2017-2023 as this was as long as Ken Pomeroy’s has published the same types of ratings every year. These ratings consisted of a team's adjusted offensive efficiency, adjusted defensive efficiency, adjusted tempo, luck, adjusted offensive efficiency of opposing offenses, adjusted defensive efficiency of opposing offenses, and non-conference strength of schedule rating. 

### Historical Tournament Matchups

This data was collceted for the 2022, 2021, 2019, 2018, and 2017 tournaments. A web scraper created internally using the website [SportsReference](https://www.sports-reference.com/cbb/) was required to easily access this data and was retrieved from 2017-2022 to match the range of KenPom’s data to fit the logistic regression model. This data set consisted of a team’s seed, name, and opponent in each round.

### [Historical Seed Win Probabilities](https://mcubed.net/ncaab/seeds.shtml)

This data set consisted of the historical win probabilities of each seed versus every seed they have faced. This data was readily available on the website Mcubed.net to be converted into a .csv file and consisted of a first seed, a second seed, and the first seed’s win percentage over the second seed.

## Simulation Code

### Data Processing

The first four code blocks consist of the steps needed to load each data set, and process/clean them. This required standardizing team and region naming formats, splitting columns, subsetting data sets, and removing duplicates and NA's before approaches could be implemented and simulation could take place.

### Logistic Regression

The 5th code block consists of the steps needed to build a logistic regression model on KenPom's rating to predict win probabilities of each team in each matchup. For this, a data set was created of each matchup in historical tournaments along with the team ratings of each team. Next, training and testing splits were created, a logistic regresison model was fit, and the accuracy of the fitted model was examined using the test set.

### Bracket Building

The 6th - 12th code blocks consist of the steps needed to build brackets using each approach outlined in the study. The details of each approach are discussed in the report, but generally each method involves establishing the predetermiend 1st round matchups, using each method's decision metric to determine which team in each matchup should advance, advancing that team, and continuing this process until all picks had been made. Other metrics needed to be calculated for certain approaches such as predicted win probability of each team in each matchup for the KenPom approach, and the difference between FiveThirtyEight's predicted probabilities and ESPN's selection percentages for the difference approach. Notably, the difference strategy differed from the previous strategies as the winner of the entire tournament was selected first, filled in for all previous rounds, and then picks were made in reverse order as explained in the report.

### Monte Carlo Simulation

The 13th code block consists of the steps needed to perform Monte Carlo simulation for the tournament, and calculate simulated point totals for each strategy. For this simulation, brackets were simulated using monte carlo simulation and historical seed performance as explained in the report, then the point total each bracket approach would have gained for each simulated bracket was stored for further inference.

### Plots & Metrics

The 14th - 17th code blocks consist of steps needed to calculate metrics such as the number of points each bracket method would have actually gained in each tournament as well the the results for normality test. Additionally, plots of the distribution of simulated point totals as well as the accuracy of each approach in each round were created in this section to be used in the final report.

### Combination Strategy

The 18th code block consists of the steps needed to create the combination strategy as explained in the report. This method was created similar to the difference strategy as the winner of the entire tournament was selected first, filled in for all previous rounds, and then picks were made in reverse order as explained in the report.

### Yearly Implementation

The 19th code block on consist of the steps needed to carry out the bracket creation, monte carlo simulation, and output analysis for each year tested. This involved establishing the real bracket for historical years, specifying which teams to not include in each year (from the "play-in" games), as well as specifyign file paths, years, and the number of simulations to complete. The output for the code block of each yearly implementation was the distribution of simulated point totals, each method's accuracy in each round, the real point total each appraoch would have gained, and the picks made by the best approach (the combination approach). 
