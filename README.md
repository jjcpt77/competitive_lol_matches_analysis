# Dragons vs. Heralds: Understanding the Impact of Early-Game Objectives on Match Victories

**Author:** Rebecca Wu

In this DSC80 course project, I utilized data on competitive League of Legends matches to attempt to answer the question of whether securing the first dragon or obtaining the first herald holds greater importance in contributing to victories. To complete this analysis, the project involved cleaning data, performing exploratory data analysis, assessing missingness, and hypothesis testing. 

## Introduction

In competitive League of Legends, strategic decisions in the early-game can set the pace for the entire match. Two critical early-game objectives that teams often fight over are dragons and heralds. As a result, one might ponder: in the early-game, which holds greater importance: securing the first dragon or obtaining the first herald? Does either claiming the first dragon or securing the first herald contribute more to victories? To understand the significance of securing the first dragon or obtaining the first herald in victorious gameplay, relevant data was extracted from a cumulative dataset of competitive League of Legends matches from 2022. 

### Understanding the dataset

The dataset contains match information from the LCS, LEC, LCK, LPL, and various other major and minor leagues. Each of the 12,450 matches documented in the dataset contributes 12 rows, with 10 rows dedicated to player information for each match, and the remaining 2 rows containing team data. Among the information given for all players and teams across all matches, this project specifically leverages the rows that encapsulate team statistics for each match. Additionally, columns indicating the match result, the acquisition of the first dragon, and the acquisition of the first herald are used in the analysis conducted in this project.  

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

This pie chart shows that teams are slightly more likely to win when obtaining the first dragon. 

<iframe src="assets/univariate_analysis_drag.html" width=800 height=600 frameBorder=0></iframe>

This pie chart shows that teams are slightly more likely to win when obtaining the first herald. 

<iframe src="assets/univariate_analysis_herald.html" width=800 height=600 frameBorder=0></iframe>

### Bivariate Analysis


## Assessment of Missingness

### NMAR Missingness

### MAR and MCAR Missingness analysis

## Hypothesis Testing


This project was created for the DSC80 course at UC San Diego.
