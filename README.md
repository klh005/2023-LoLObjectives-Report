
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

The dataset provides a detailed overview of gameplay metrics and match outcomes from professional League of Legends esports matches.

- **Major Outcome Columns:**
  - **league**: The specific league or tournament in which the match took place.
  - **gameid**: A unique identifier for each match.
  - **result**: Indicates the outcome of the match for the team (1 for win, 0 for loss).
  - **teamkills**: The total number of kills secured by the team.
  - **teamdeaths**: The total number of deaths experienced by the team.
  - **totalgold**: The total number of gold accumulated by the team.
  - **side**: Specifies whether the team was on the "blue" or "red" side during the match.
  - **champion**: The name of the champion a player selected. Is NaN if the row is considered "team data".

&nbsp; 

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

<iframe src="assets/grouped_data_1.html" width="100%" height="600px" frameborder="0"></iframe>

### Univariate Analysis: Distribution of Towers Destroyed

We conducted a detailed univariate analysis on the distribution of towers destroyed within our dataset. The histogram, after filtering out duplicate objective statistics, reveals a notable bimodal distribution. This pattern shows significant peaks where the number of towers destroyed is concentrated around 2 and 9.

The first peak at 2 towers suggests that many teams, likely the losing ones, managed to destroy only a couple of towers before succumbing to defeat. This could indicate that early tower destruction is not always enough to secure a win, possibly due to stronger defensive plays or a lack of follow-through on early-game advantages.

On the other hand, the second peak at 9 towers highlights the winning teams, who typically dominate the map, securing most or all of the enemy's towers. This suggests that teams capable of destroying a higher number of towers are generally those that secure the victory, emphasizing the critical importance of maintaining pressure and pushing objectives throughout the game.

This analysis underlines the strategic importance of tower objectives in League of Legends. The distinct distribution suggests that while early tower destruction provides some advantages, consistent objective control, leading to the destruction of a majority of towers, is often what separates the winning teams from the losing ones.

<iframe src="assets/dist_towers.html" width="100%" height="600px" frameborder="0"></iframe>

It also suggests that games typically remain dominate on one side in terms of objectives. This effect is called "snowballing" where a team is able to carry a small lead into a larger lead throughout the entire game. Surprisingly, although reaching the end of the game takes a minimum of five turrets to be destroyed, many winners appear to have destroyed more. Below is a distribution of towers destroyed by the winning teams.

<iframe src="assets/win_dist_towers.html" width="100%" height="600px" frameborder="0"></iframe>

Obtaining more towers lead to the acquisition of more gold, resulting in a further lead that will secure a win.

Another column that is integral to visualize is the distribution of major objectives taken other than towers. Major objectives include: baron, dragons, herald and void grubs. The distribution shows that while some teams managed to secure only a few major objectives, others were able to take control of many, which likely contributed to their success in the match. The variability in the number of major objectives taken highlights the importance of these objectives in determining the outcome of the game.

<iframe src="assets/major_objectives_distribution.html" width="100%" height="600px" frameborder="0"></iframe>

Similarly to towers destroyed, the graph also demonstrates a "snowballing" effect with objectives.

<iframe src="assets/win_major_objectives_distribution.html" width="100%" height="600px" frameborder="0"></iframe>

### Bivariate Analysis: Impact of Objective Control on Match Outcome

We performed a bivariate analysis on the relationship between securing major objectives and the match results to understand how objective control influences the likelihood of winning.

#### Barons and Match Outcome
The plot below illustrates the proportion of wins and losses based on the number of Barons secured by a team. Teams that secure more Barons tend to have a higher win rate, suggesting that controlling Baron Nashor provides a significant strategic advantage in securing victory.

<iframe src="assets/Barons_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### Dragons and Match Outcome
The following plot shows the win/loss proportions based on the number of Dragons secured. Similar to Barons, securing more Dragons is associated with a higher probability of winning, emphasizing the importance of Dragon control throughout the match.

<iframe src="assets/Dragons_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### First Dragon and Match Outcome
The proportion of wins and losses based on whether the first Dragon was secured indicates that teams who take the first Dragon have a higher win rate, further supporting the strategic value of early objective control.

<iframe src="assets/Firstdragon_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### Towers and Match Outcome
This plot shows the win/loss proportions based on the number of Towers destroyed. As expected, teams that destroy more Towers have a higher likelihood of winning, reinforcing the importance of this objective in determining match outcomes.

<iframe src="assets/Towers_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### Void Grubs and Match Outcome
Although Void Grubs are less impactful than other objectives, the plot still indicates a positive correlation between securing them and winning the match, though the effect is less pronounced.

<iframe src="assets/Void_grubs_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### Elders and Match Outcome
The Elder Dragon, a powerful late-game objective, shows a strong correlation with match outcomes. Teams that secure the Elder Dragon have a significantly higher chance of winning, highlighting its critical role in the late game.

<iframe src="assets/Elders_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### Inhibitors and Match Outcome
Finally, the plot for Inhibitors shows that teams which destroy more Inhibitors are overwhelmingly likely to win the game, confirming the crucial importance of this objective in closing out matches.

<iframe src="assets/Inhibitors_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

This analysis demonstrates the significant impact of controlling key objectives on match outcomes in League of Legends. Each of these objectives contributes strategically to a team's success, with higher control correlating with better chances of winning.

### Aggregated Data by Towers Destroyed

The table below shows aggregated statistics based on the number of towers destroyed:

<iframe src="assets/by_towers_df.html" width="100%" height="400px" frameborder="0"></iframe>

### Aggregated Data by Major Objectives Taken

The table below shows aggregated statistics based on the number of major objectives taken:

<iframe src="assets/by_major_objectives_df.html" width="100%" height="400px" frameborder="0"></iframe>

&nbsp; 

## Assessment of Missingness

### Not Missing At Random (NMAR) Analysis

The NaN values in the 'first' objective columns, such as `firsttower`, `firstdragon`, and `firstbaron`, are likely Not Missing At Random (NMAR). These NaNs indicate that a team did not meet the specific conditions required to secure these objectives. For example, a NaN in `firsttower` means the team did not take the first tower. This missingness is not random and it directly results from the team's in-game decisions and strategy. Without additional data explaining these strategic choices, the missingness remains NMAR. There is the possibility of other objectives to depend on each other; however, in this dataset, NaN only appears in columns where it is NMAR after data cleaning.

### Missingness Dependency

In this section, we explore whether the missingness of certain columns in our dataset depends on other variables. Specifically, we performed permutation tests to assess the dependency of the missingness of the `firstdragon` and `void_grubs` columns on other factors like `league` and `result`.

#### Permutation Test 1: Missingness of `firstdragon` vs. `league`

**Null Hypothesis**: The distribution of `league` is the same whether `firstdragon` is missing or not.

**Alternative Hypothesis**: The distribution of `league` is different when `firstdragon` is missing.

**Results**:
- **Observed TVD**: 48.81
- **P-value**: 0.0000

Since the p-value is significantly less than our significance level of 0.5, we reject the null hypothesis. This indicates that the missingness of `firstdragon` is dependent on the `league` column.

<iframe src="assets/firstdragon_league_tvd.html" width="100%" height="600px" frameborder="0"></iframe>

#### Permutation Test 2: Missingness of `firstdragon` vs. `result`

**Null Hypothesis**: The number of wins (`result`) is the same whether `firstdragon` is missing or not.

**Alternative Hypothesis**: The number of wins (`result`) differs when `firstdragon` is missing.

**Results**:
- **Observed Difference**: -7567.0
- **P-value**: 0.5180

With a p-value greater than our significance level of 0.5, we fail to reject the null hypothesis. This suggests that the missingness of `firstdragon` does not significantly depend on the `result`.

<iframe src="assets/firstdragon_result_diff.html" width="100%" height="600px" frameborder="0"></iframe>

#### Permutation Test 3: Missingness of "void_grubs" vs. Result (Wins) Using TVD

**Null Hypothesis**: The distribution of results (wins/losses) is the same regardless of whether "void_grubs" is missing or not.

**Alternative Hypothesis**: The distribution of results is different depending on whether "void_grubs" is missing.

Since the data for "void_grubs" showed that it was mostly missing with a few rows being zero, we tested the dependency using TVD. The observed TVD was **1.9941**, with a **p-value of 0.6190**. This suggests that the missingness of "void_grubs" does not depend on the result of the match. Since the p-value greater than our significance level of 0.5, we fail to reject the null hypothesis.

<iframe src="assets/void_grubs_result_tvd.html" width="100%" height="600px" frameborder="0"></iframe>

## Hypothesis Testing

To investigate the impact of the number of major objectives (Baron, Dragon, Rift Herald, Void Grubs) on the likelihood of winning a match, we conducted a hypothesis test.

- **Null Hypothesis (H₀)**: The number of major objectives secured does not significantly affect the probability of winning.
- **Alternative Hypothesis (H₁)**: The number of major objectives secured significantly increases the probability of winning.
- **Test Statistic**: Absolute difference in win proportions.
- **Significance Level**: 5%

### Results
- **Observed Difference**: 0.0455
- **P-value**: 0.4350

Based on the p-value obtained from the permutation test, which is 0.4350, we fail to reject the null hypothesis. This suggests that the number of major objectives secured does not significantly impact the probability of winning. Although the observed difference in win proportions was positive, indicating a slight increase in win rate with more objectives secured, the result is not statistically significant.

### Visualization

Below is a histogram showing the distribution of the test statistics during the permutation test, with the observed difference highlighted by a neon green vertical line:

<iframe src="/assets/major_objectives_win_diff.html" width="100%" height="600px" frameborder="0"></iframe>

### Interpretation of Results

The results from our hypothesis test indicate that non-tower major objectives (such as Baron, Dragons, Rift Herald, and Void Grubs) have a minor impact on the outcome of a match, but this impact is not substantial. The observed difference in win rates is small, and the p-value suggests that this difference is not statistically significant. This means that while securing these objectives may provide some advantage, no single major objective significantly influences the overall outcome of a match on its own.

## Framing a Prediction Problem

The goal of this prediction problem is to estimate the total gold of the losing team based on the objectives secured by the winning team. By predicting the opponent’s total gold, we aim to quantify the "gold gap" or disparity between the two teams, providing insights into how objectives contribute to the winning team's lead and dominance. Understanding this gap can help evaluate the impact of in-game objectives on maintaining or widening a team's advantage. By predicting the opponent's total gold, we aim to measure how objectives directly contribute to the overall advantage of the winning team. This approach focuses on the importance of objectives in influencing game outcomes, helping teams understand which objectives contribute most to maintaining a lead.

The dataset will be split into training and testing sets using an 80/20 split to avoid overfitting the data. The target variable is the opponent's **totalgold**, aiming to predict the losing team's total gold using the winning team’s objective statistics. We will evaluate the model using Mean Squared Error (MSE) and R-squared. MSE will provide insight into the average prediction error, while R-squared will indicate how much of the variance in the opponent's total gold is explained by the features. A higher R-squared value would indicate a better fit.

Below is the merged DataFrame used to train for the prediction problem. We merged both sides of a match into one row to compare the differences of gold for each team based on the winning team's objectives:

<iframe src="/assets/merged_df.html" width="100%" height="600px" frameborder="0"></iframe>

### Overfitting and Underfitting Considerations
By focusing on key objective metrics (`elementaldrakes`, `elders`, `barons`, `heralds`, `firsttower`, and `towers`), we reduce the likelihood of overfitting while retaining essential predictors. These features were chosen because they reflect significant moments in the game that contribute directly to a team’s overall gold advantage. Limiting the feature set ensures the model generalizes well to new data without losing predictive power.

## Prediction Model

### Features in the Model
For this prediction model, we used a Random Forest Regressor to predict the total gold earned by the opposing team based on the winning team's objective statistics and match duration.

The features used for this model are:
- **Gamelength** (Quantitative): The duration of the game, which influences the number of objectives taken and the total gold accrued by both teams.
- **Firstdragon_winner** (Nominal): A binary column indicating whether the winning team secured the first dragon.
- **Dragons_winner** (Quantitative): The total number of dragons taken by the winning team.
- **Barons_winner** (Quantitative): The total number of barons taken by the winning team.
- **Towers_winner** (Quantitative): The total number of towers destroyed by the winning team.

### Encodings
The variables are either quantitative or binary. The `firstdragon_winner` column is nominal and already encoded as binary (0 or 1). No additional encodings were needed, but a StandardScaler was used to standardize the numerical features.

### Model Performance
The model was evaluated using the following metrics:
- **Mean Squared Error (MSE)**: 9,905,658.8615
- **R-squared (R²)**: 0.9234

This means the model explains about 92.34% of the variance in the opponent's total gold based on the given features, which is a strong result. However, the high Mean Squared Error indicates that while the model captures overall trends well, there may be significant variance in the predictions for some instances.

### Model Evaluation
The model seems to perform well, as indicated by the high R² score, but further tuning may be necessary to reduce the MSE. It's also important to note that this model is trained based on objective statistics, which inherently limits its ability to predict large variations in gold from other factors such as player skill or in-game strategy.

<iframe src="/assets/merged_df.html" width="100%" height="600px" frameborder="0"></iframe>

=======
https://klh005.github.io/2023-LoLObjectives-Report/
