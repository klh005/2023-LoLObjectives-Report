---
permalink: README.html
---
# League of Legends Objective Impact Analysis
- Kliment Ho

In a game of League of Legends, players are tasked to destroy the "Nexus" in order to win a game. In order to reach the point of destroying the nexus, players must
take and destroy many other objectives such as "towers" and "inhibitors". Additionally, there are other optional objectives that will grant players immense aid
in achieving a win. The project is designed to solve the looming question: which objectives are the most impactful? By going through sections of analysis(such as
exploratory data analysis, hypothesis testing) and creating a baseline model with an accomodating fairness analysis, we can discover the identity and meaning of the 
most impactful objective upon a match's outcome.

## Project Structure
- **Data Cleaning and Preprocessing**: Includes steps to handle missing data, filtering relevant columns, and grouping data by team and match.
- **Exploratory Data Analysis (EDA)**: Univariate, Bivariate, and Aggregate analysis to uncover relationships between objectives and match outcomes.
- **Hypothesis Testing**: Statistical testing to determine the significance of various objectives in match outcomes.
- **Modeling**: Baseline and final models built to predict match outcomes based on objectives.
- **Fairness Analysis**: Evaluation of model performance across different groups to ensure fairness.

## An Objective Introduction
League of Legends (LoL) is a fast-paced, team-based strategy game where two teams of five players each aim to destroy the opposing team's Nexus, the core structure in their base. The game is won by methodically working through enemy defenses, including towers and inhibitors, while securing various objectives that grant strategic advantages.

In every match, players engage with different objectives, each offering unique benefits:

- Baron Nashor: A neutral monster, when defeated, provides a team-wide buff that strengthens players. Considered one of the most powerful buffs in the game.

- Drakes (Dragons): These elemental creatures offer stacking buffs that enhance various aspects of a team’s performance, such as attack power or healing. After four are secured, the Elder Dragon can be summoned, granting even greater power.

- Rift Herald: Limited to the "early game", Herald helps by delivering massive damage to enemy towers. It's used to capture tower or distract the enemy.

- Jungle Monsters: Including the Scuttle Crab, which grants vision and speed boosts, and other camps that offer gold, experience, and buffs.

- Towers: The defensive structures that must be destroyed to progress through the map. Taking down towers opens pathways to the Nexus and grants numerous gold to the team.

The report seeks to answer which of these objectives are most crucial to winning a game of League of Legends. Through detailed analysis and modeling, we will uncover the impact each objective has on a match's outcome, offering insights into strategic priorities for competitive play.

### Relevant Columns

The dataset provides a detailed overview of gameplay metrics and match outcomes from professional League of Legends esports matches. There are 148,992 rows in this dataset, and here’s an introduction to some of the key columns:

- **Major Outcome Columns:**
  - **league**: The specific league or tournament in which the match took place.
  - **gameid**: A unique identifier for each match.
  - **result**: Indicates the outcome of the match for the team (1 for win, 0 for loss).
  - **teamkills**: The total number of kills secured by the team.
  - **teamdeaths**: The total number of deaths experienced by the team.
  - **side**: Specifies whether the team was on the "blue" or "red" side during the match.

- **Objectives:**
  - **firstdragon**: Indicates whether the team secured the first dragon.
  - **dragons**: The total number of dragons secured by the team.
  - **opp_dragons**: The total number of dragons secured by the opposing team.
  - **elementaldrakes**: The total number of elemental drakes secured.
  - **opp_elementaldrakes**: Elemental drakes secured by the opposing team.
  - **infernals, mountains, clouds, oceans, chemtechs, hextechs**: These columns track the specific types of dragons secured by the team, each providing unique buffs.
  - **elders**: Indicates whether the team secured the Elder Dragon, a powerful late-game objective.
  - **opp_elders**: Tracks whether the opposing team secured the Elder Dragon.
  - **firstherald**: Shows whether the team secured the first Rift Herald, a key early-game objective.
  - **heralds**: The total number of Rift Heralds secured.
  - **opp_heralds**: The number of Rift Heralds secured by the opposing team.
  - **void_grubs**: Represents the number of Void Grubs secured, although this objective is generally less impactful.
  - **opp_void_grubs**: Tracks the number of Void Grubs secured by the opposing team.
  - **firstbaron**: Indicates whether the team secured the first Baron Nashor, a crucial late-game objective.
  - **barons**: The total number of Barons secured.
  - **opp_barons**: The number of Barons secured by the opposing team.
  - **firsttower**: Indicates whether the team destroyed the first tower.
  - **towers**: The total number of towers destroyed by the team.
  - **opp_towers**: The number of towers destroyed by the opposing team.
  - **firstmidtower**: Indicates whether the team destroyed the first mid-lane tower.
  - **firsttothreetowers**: Tracks whether the team destroyed the first three towers in the game.
  - **turretplates**: The number of turret plates destroyed by the team.
  - **opp_turretplates**: The number of turret plates destroyed by the opposing team.

This detailed breakdown of the dataset columns will guide our analysis as we investigate which objectives most significantly impact match outcomes in League of Legends.

## Data Cleaning
To streamline the data for analysis, we began by retaining only the relevant columns: gameid, side, result, teamkills, teamdeaths, and all the objective-related columns. This was done to focus our analysis on how objectives influence match outcomes.

Next, we performed two main grouping operations:

Grouping by league: We grouped the data by league and aggregated each objective using the maximum value. This allowed us to see the distribution of objectives across different leagues.

Grouping by gameid and side: This grouping was done to summarize each team’s performance in terms of objectives, teamkills, and teamdeaths.
These steps provided a clearer view of how objectives correlate with match outcomes and other gameplay statistics, setting the stage for further analysis.

Here is the first 50 gameid-side rows (25 different games) by the groupby below.

<iframe src="/assets/grouped_data_1.html" width="100%" height="600px" frameborder="0"></iframe>

### Univariate Analysis
- **Objective Distribution**: Histograms show the frequency of securing objectives, highlighting their importance in matches.

### Bivariate Analysis
- **Objective vs. Outcome**: Correlation matrices reveal which objectives are strongly associated with winning.
=======
https://klh005.github.io/2023-LoLObjectives-Report/
