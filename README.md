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

### Univariate Analysis

### Bivariate Analysis

## Assessment of Missingness

### NMAR Missingness

### MAR and MCAR Missingness analysis

## Hypothesis Testing


This project was created for the DSC80 course at UC San Diego.
