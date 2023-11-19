# Dragons vs. Heralds: Understanding the Impact of Early-Game Objectives on Match Victories

**Author:** Rebecca Wu

In this DSC80 course project, I utilized data on competitive League of Legends matches to attempt to answer the question of whether securing the first dragon or obtaining the first herald holds greater importance in contributing to victories. To complete this analysis, the project involved cleaning data, performing exploratory data analysis, assessing missingness, and hypothesis testing. 

## Introduction

In competitive League of Legends, strategic decisions in the early-game can set the pace for the entire match. Two critical early-game objectives that teams often fight over are dragons and heralds. As a result, one might ponder: in the early-game, which holds greater importance: securing the first dragon or obtaining the first herald? Does either claiming the first dragon or securing the first herald contribute more to victories? To understand the significance of securing the first dragon or obtaining the first herald in victorious gameplay, relevant data was extracted from a cumulative dataset of competitive League of Legends matches from 2022. 

### Understanding the dataset

The dataset used to investigate the topic can be found [here](https://oracleselixir.com/tools/downloads). The dataset contains match information from the LCS, LEC, LCK, LPL, and various other major and minor leagues. Each of the 12,450 matches documented in the dataset contributes 12 rows, with 10 rows dedicated to player information for each match, and the remaining 2 rows containing team data. Among the information given for all players and teams across all matches, this project specifically leverages the rows that encapsulate team statistics for each match. Additionally, columns indicating the match result, the acquisition of the first dragon, and the acquisition of the first herald are used in the analysis conducted in this project.  

### Description of relevant columns

- `gameid`: A unique identifier assigned to each game in the dataset
- `league`: Indicates the league or tournament to which each match belongs
- `gamelength`: Duration of the match, in seconds
- `result`: Outcome of the match for a team
- `firstdragon`: Indicates whether a team secured the first dragon in the match, `True` if the team secured first dragon, `False` otherwise
- `firstherald`: Indicates whether a team secured the first herald in the match, `True` if the team secured first dragon, `False` otherwise

## Cleaning and Exploratory Data Analysis

The original dataset was filtered to include only rows where the `position` column is labeled as `team`.  This step ensures that only the team-level statistics are retained and individual player daya is excluded. A subset of relevant columns were selected for analysis, including `gameid`, `league`, `gamelength`, `result`, `firstdragon`, and `firsthearld`. Noting that NaN values in `firstdragon` and `firstheard` columns should not be filled with 0 or False, since the missing values do not imply that the objective was not taken, these two columns were converted to boolean values based on the condition that the values are not NaN. The `result` column was transforms to represent wins as "Victory" and losses as "Defeat for better interpretability. 
**The first 5 rows of the DataFrame are shown below:**

| gameid                | league   |   gamelength | result   |   firstdragon |   firstherald |
|:----------------------|:---------|-------------:|:---------|--------------:|--------------:|
| ESPORTSTMNT01_2690210 | LCKC     |         1713 | Defeat   |             0 |             1 |
| ESPORTSTMNT01_2690210 | LCKC     |         1713 | Victory  |             1 |             0 |
| ESPORTSTMNT01_2690219 | LCKC     |         2114 | Defeat   |             0 |             1 |
| ESPORTSTMNT01_2690219 | LCKC     |         2114 | Victory  |             1 |             0 |
| 8401-8401_game_1      | LPL      |         1365 | Victory  |           nan |           nan |

### Univariate Analysis

This pie chart shows the distribution of team victories and losses following the acquisition of the first dragon. Looking at the distribution, it appears that teams have a slightly higher likelihood of winning when securing the first dragon.
<iframe src="assets/univariate_analysis_drag.html" width=650 height=450 frameBorder=0></iframe>

This pie chart shows the distribution of team victories and losses following the acquisition of the first herald. Similarly, it appears that teams have a slightly higher likelihood of winning when securing the first herald.
<iframe src="assets/univariate_analysis_herald.html" width=650 height=450 frameBorder=0></iframe>

### Bivariate Analysis

This multiple boxplot graph visualizes the game duration distributions for two distinct outcomes: victories and defeats. The plot is divided by the type of first objective achieved in League of Legends matches, offering a comparative analysis of how securing different early-game objectives influences the overall length of matches. Teams that secure both early-game objectives tend to achieve victories with the shortest game times. In instances where only the first herald or only the first dragon was obtained, teams securing the first herald experienced slightly shorter game durations for victories.
<iframe src="assets/bivariate_analysis.html" width=800 height=450 frameBorder=0></iframe>

### Interesting Aggregates

This table presents the win rates of teams based on the acquisition of specific early-game objectives, dragon and herald, across all Tier 1 Leagues (excluding LPL). By providing league-specific trends, this table provides insights into the impact of these objectives on team success in different competitive environments, as well as shows region-specific approaches to playing around these objectives. Notably, there is a large variation in win rates observed in the LCS, indicating a potential inconsistency in the effectiveness of teams in the LCS when it comes to utilizing the first herald as opposed to the first dragon.

| league   |   Winrate with Dragon |   Winrate with Herald |
|:---------|----------------------:|----------------------:|
| CBLOL    |              0.555556 |              0.555556 |
| LCK      |              0.5803   |              0.543897 |
| LCS      |              0.620915 |              0.558824 |
| LEC      |              0.572016 |              0.576132 |
| LJL      |              0.551402 |              0.502347 |
| LLA      |              0.604278 |              0.6      |
| PCS      |              0.645756 |              0.605166 |
| VCS      |              0.585139 |              0.603715 |

## Assessment of Missingness

### NMAR Analysis

I do not believe that there are any NMAR missingness patterns for the values in the dataset.  Since the completeness of each row in the dataset is explicitly labeled as either `complete` or `partial`, rows with missing values can easily be isolated. For rows labeled `complete`, missing values in the corresponding columns are MD and MAR dependent on `position`. Since some columns are dedicated to team statistics and others to player statistics, their missingness is inherently tied to the 'position' column and is missing by choice of the author of the dataset. In instances where the rows are partially complete, the missing team statistics specifically pertain to the Chinese leagues, indicating that missingness, in this case, is MAR dependent on `league`.

### Missingness Dependency

**`firstherald` is MAR dependent on `patch`.**
Knowing that the missingness of team statistics is dependent on `league`, it is reasonable to speculate that it is also missing dependent on `patch`. The patch that teams across leagues play on differs and is independent from one another. With a significance level of 0.05 and using TVD as the test statistic, the resulting p-value = 0. This p-value indicates that the missingness of `firstherald` is MAR dependent on `patch`. 

<iframe src="assets/empirical_TVD_MAR.html" width=1050 height=450 frameBorder=0></iframe>

**`firstherald` is MCAR dependent on `inhibitors`.**
To determine whether `firstherald ` is MAR or MCAR dependent on the number of `inhibitors` taken by a team, a significance level of 0.05 was set and the TVD was used as the test statistic. With a calculated p-value = 0.2754, it can be concluded that the missingness of `firstherald` is MCAR dependent on `inhibitors`. 

<iframe src="assets/empirical_TVD_MCAR.html" width=1050 height=450 frameBorder=0></iframe>

## Hypothesis Testing

### Permutation Testing

To revisit, the goal of this analysis is to analyze the importance of early-game objectives relative to each other. More specifically, it is meant to answer the question: In the early-game, which holds greater importance: securing the first dragon or obtaining the first herald? Put differently, does claiming the first dragon or does securing the first herald contribute more to victories? (By default, Chinese leagues, such as the LPL and Demacia Cup, will be excluded from the analysis.) A permutation test is most appropriate to answer this question, since the distributions of two samples are being compared against each other. Since two categorical variables (win/loss & dragon/herald) are being compared, the TVD can be used as the test statistic. 

### Hypotheses

- **Null hypothesis:** The distribution of win rate in games where the team obtained the first herald is the same as the distribution of win rate in games where the team obtained the first dragon. 
- **Alternate hypothesis:** The distribution of win rate in games where the team obtained the first herald is different from the distribution of win rate in games where the team obtained the first dragon.

### Results

The plot below shows the distribution of TVDs for 5,000 simulations. 

<iframe src="assets/permutation_test.html" width=1050 height=450 frameBorder=0></iframe>

- **Significance level:** α = 0.05
- **Observed p-value:** p = 0.2524

### Conclusion

At the conventional significance level of 0.05, the permutation test resulted in a p-value of 0.2524, and we failed to reject the null hypothesis. While obtaining the first objective generally correlates to a positive win rate, there is no evidence to prove that one provides substantial advantages over the other.

