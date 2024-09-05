
# The Study of Objective-based Gameplay: 
# An Analysis On League of Legends' Objectives
- Report by Kliment Ho

In a game of League of Legends, players are tasked to destroy the "Nexus" in order to win a game. In order to reach the point of destroying the nexus, players must
take and destroy many other objectives such as "towers" and "inhibitors". Additionally, there are other optional objectives that will grant players immense aid
in achieving a win. This project seeks to answer: in what ways are objectives impactful a match of League of Legends?

Through exploratory data analysis, hypothesis testing, and modeling, we investigate the influence of objectives on match outcomes and provide insights into which objectives are most critical to winning. By doing so, we can uncover how in-game decisions related to objectives affect a team's chances of securing victory.

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

There are also plenty of smaller objectives such as "scuttle crab" which grants extra vision(integral for a team's planning and information) for the team. However, for the sake of the report, we choose to focus on the above-mentioned objectives along with other stats such as "teamkills", "teamdeaths", "teamgold", "minionkills", and if a team claims a specific objective first. The report seeks to answer which of these objectives are most crucial to winning a game of League of Legends. Through detailed analysis and modeling, we will uncover the impact each objective has on a match's outcome, offering insights into strategic priorities for competitive play.

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

We performed two main grouping operations:

We grouped the data by league and aggregated each objective using the maximum value, allowing us to see the distribution of objectives across different leagues.

We also had grouping done to summarize each team’s performance in terms of objectives, teamkills, and teamdeaths, providing a clearer view of how objectives correlate with match outcomes and other gameplay statistics.

Below is the first 50 gameid-side rows (25 different games):

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

We performed a bivariate analysis on the relationship between securing major objectives and each team across all matches to understand how objective control influences the likelihood of winning. The graph shows two colors, representing the winning and losing teams. This will compare the proportions of the number of wins to losses over the objective score.

#### Barons
The plot below illustrates the proportion of wins and losses based on the number of Barons secured by a team. Teams that secure more Barons tend to have a higher win rate, suggesting that controlling Baron Nashor provides a significant strategic advantage in securing victory.

<iframe src="assets/Barons_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### Dragons
The following plot shows the win/loss proportions based on the number of Dragons secured. Similar to Barons, securing more Dragons is associated with a higher probability of winning, emphasizing the importance of Dragon control throughout the match.

<iframe src="assets/Dragons_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### First Dragon
The proportion of wins and losses based on whether the first Dragon was secured indicates that teams who take the first Dragon have a higher win rate, further supporting the strategic value of early objective control.

<iframe src="assets/Firstdragon_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### Towers
This plot shows the win/loss proportions based on the number of Towers destroyed. As expected, teams that destroy more Towers have a higher likelihood of winning, reinforcing the importance of this objective in determining match outcomes.

<iframe src="assets/Towers_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### Void Grubs
Although Void Grubs are less impactful than other objectives, the plot still indicates a positive correlation between securing them and winning the match, though the effect is less pronounced. However, as we would later see, void grubs would be rendered irrelevant for this report.

<iframe src="assets/Void_grubs_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### Elders
The Elder Dragon, a powerful late-game objective, shows a strong correlation with match outcomes. Teams that secure the Elder Dragon have a significantly higher chance of winning, highlighting its critical role in the late game.

<iframe src="assets/Elders_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

#### Inhibitors
The plot for Inhibitors shows that teams which destroy more Inhibitors are overwhelmingly likely to win the game, confirming the crucial importance of this objective in closing out matches. At the end of the game, inhibitors can respawn which allows the possibility of an unlimited range of inhibitors destroyed as long as the game does not end.

<iframe src="assets/Inhibitors_prop_bar.html" width="100%" height="600px" frameborder="0"></iframe>

The above columns are compared against the total number of matches, showing the number of teams having 4 dragons claimed or taking no barons at all.

### Aggregated Data by Towers Destroyed

The table below shows aggregated statistics based on the number of towers destroyed:

<iframe src="assets/by_towers_df.html" width="100%" height="400px" frameborder="0"></iframe>

### Aggregated Data by Major Objectives Taken

The table below shows aggregated statistics based on the number of major objectives taken:

<iframe src="assets/by_major_objectives_df.html" width="100%" height="400px" frameborder="0"></iframe>

&nbsp; 

## Assessment of Missingness

### Not Missing At Random (NMAR) Analysis

The NaN values in the 'first' objective columns, such as `firsttower`, `firstdragon`, and `firstbaron`, are likely Not Missing At Random (NMAR). These NaNs indicate that a team did not meet the specific conditions required to secure these objectives. For example, a NaN in `firsttower` means the team did not take the first tower. This missingness is not random and it directly results from the team's in-game decisions and strategy. Without additional data explaining these strategic choices, the missingness remains NMAR. There is the possibility of other objectives to depend on each other; however, in this dataset, NaN only appears in columns where it is NMAR after data cleaning. Without data cleaning, however, the values would then be considered Missing At Random as there are objective stats that could be tied to invalid games or matches with weird data organization.

### Missingness Dependency

In this section, we explore whether the missingness of certain columns in our dataset depends on other variables. Specifically, we performed permutation tests to assess the dependency of the missingness of the `firstdragon` and `void_grubs` columns on other factors like `league` and `result`. For this experiment, we will set the significance level to 0.5 due to the nature of the objective `firstdragon` being a nominal categorical variable with two outcomes: is the team to take the first dragon or is not the team to take the first dragon.

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

Since the data for "void_grubs" showed that it was mostly missing with a few rows being zero, we tested the dependency using TVD. The observed TVD was **1.9941**, with a **p-value of 0.6190**. This suggests that the missingness of "void_grubs" does not depend on the result of the match. Since the p-value greater than our significance level of 0.5, we fail to reject the null hypothesis. Looking closer at the dataset, we can see that the objective was not implemented for any 2023 matches and we can safely discard the column. Void grubs are objectives that was added in version 14.1; however, all patches in 2023 start with the version '13' which further shows that void grubs are an unnecessary column to include.

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

Based on the p-value obtained from the permutation test, which is 0.4350, we fail to reject the null hypothesis. This suggests that the number of major objectives secured does not significantly impact the probability of winning. Although the observed difference in win proportions was positive, indicating a slight increase in win rate with more objectives secured, the result is not statistically significant. Below is a histogram showing the distribution of the test statistics during the permutation test, with the observed difference highlighted by a neon green vertical line:

<iframe src="assets/major_objectives_win_diff.html" width="100%" height="600px" frameborder="0"></iframe>

The results from our hypothesis test indicate that non-tower major objectives (such as Baron, Dragons, Rift Herald, and Void Grubs) have a minor impact on the outcome of a match, but this impact is not substantial. The observed difference in win rates is small, and the p-value suggests that this difference is not statistically significant. This means that while securing these objectives may provide some advantage, no single major objective significantly influences the overall outcome of a match on its own.

## Framing a Prediction Problem

The goal of this prediction problem is to estimate the total gold of the losing team based on the objectives secured by the winning team. By predicting the opponent’s total gold, we aim to quantify the "gold gap" or disparity between the two teams, providing insights into how objectives contribute to the winning team's lead and dominance. Understanding this gap can help evaluate the impact of in-game objectives on maintaining or widening a team's advantage. By predicting the opponent's total gold, we aim to measure how objectives directly contribute to the overall advantage of the winning team. This approach focuses on the importance of objectives in influencing game outcomes, helping teams understand which objectives contribute most to maintaining a lead.

In more concise words, can we predict the losing team's total gold based on knowing what objectives the winning team captured?

The already filtered dataset will be using an 80/20 split to avoid overfitting the data. The target variable is the opponent's **totalgold**, aiming to predict the losing team's total gold using the winning team’s objective statistics. We will evaluate the model using Mean Squared Error and R-squared. MSE will provide insight into the average prediction error, while R-squared will indicate how much of the variance in the opponent's total gold is explained by the features. A higher R-squared value would indicate a better fit.

Below is the merged DataFrame used to train for the prediction problem. We merged both sides of a match into one row to compare the differences of gold for each team based on the winning team's objectives:

<iframe src="assets/merged_df.html" width="100%" height="600px" frameborder="0"></iframe>

By focusing on key objective metrics (`elementaldrakes`, `elders`, `barons`, `heralds`, `firsttower`, and `towers`), we reduce the likelihood of overfitting while retaining essential predictors. These features were chosen because they reflect significant moments in the game that contribute directly to a team’s overall gold advantage. Limiting the feature set ensures the model generalizes well to new data without losing predictive power.

## Baseline Model
We used a Random Forest Regressor to predict the total gold earned by the opposing team based on the winning team's objective statistics and match duration.

The features used for this model are:
- **gamelength** (Continuous, Quantitative): The duration of the game, which influences the number of objectives taken and the total gold accrued by both teams.
- **firstdragon** (Nominal): A binary column indicating whether the winning team secured the first dragon.
- **dragons** (Discrete, Quantitative): The total number of dragons taken by the winning team.

The variables are either quantitative or binary. The `firstdragon_winner` column is nominal and already encoded as binary (0 or 1). No additional encodings were needed, but a StandardScaler was used to standardize the numerical features.

As a result...
- **Mean Squared Error (MSE)**: 11103121.0851
- **R-squared (R²)**: 0.9142

About 91.42% of the variance in the opponent's total gold based on the given features could be explained by the model. Skeptically this is already a strong result and defeats the previous narrative of predicting the enemy's `totalgold` as being extremely varying. With that being said, the high Mean Squared Error indicates that while the model captures overall trends well which would indicate a significant variance in the predictions for some to many cases. Turning the MSE to RMSE shows that the total gold could vary in error by roughly 3000 gold. The median of the `totalgold` for winners in our dataset is 60577 gold. Reasonably, the RMSE calculation is accurate within an appropriate range; further improvement to decreasing the RMSE may later incentivize hyperpara

### Model Evaluation
The model seems to perform well, as indicated by the high R² score, but further tuning may be necessary to reduce the MSE. It's also important to note that this model is trained based on objective statistics, which inherently limits its ability to predict large variations in gold from other factors such as player skill or in-game strategy.

<iframe src="assets/merged_df.html" width="100%" height="600px" frameborder="0"></iframe>

## Final Model

In our final model, we added three additional features: `teamkills`, `teamdeaths`, and `minionkills`. These features were incorporated because they are directly linked to a team's ability to generate gold and maintain control throughout the game. In League of Legends, minion kills represent a reliable and constant source of income that can scale a team’s strength. Similarly, team kills offer immediate gold rewards and momentum, while team deaths signify moments when the team is vulnerable and can lose control over objectives.

- **teamkills**: Captures how successful the team is in executing fights, overall gaining gold.
- **teamdeaths**: Helps indicate moments of weakness and identify the gaps between the winner and losing team.
- **barons**: The total number of barons taken by the team; baron gives gold.
- **towers**: The total number of towers destroyed by the team; tower gives gold and shows how far ahead the winning team is.
- **minionkills**: A vital source of gold. More minion kills typically equates to more gold and a focus on gaining gold.

Because of their strong correlation with in-game performance, planning, and the effect of a team's ability to achieve objectives, the above features are added to aid in a tighter MSE calculation.

Our final model utilized a **Random Forest Regressor** to predict the opponent’s total gold (`totalgold_loser`) based on the winning team's statistics. The model relied on features like `gamelength`, `totalgold_winner`, `firstdragon`, `dragons`, `barons`, `towers`, as well as the newly added `teamkills`, `teamdeaths`, and `minionkills`.

### Quantitative Features
- `teamkills`: Discrete, captures the total number of kills the winning team secured.
- `teamdeaths`: Discrete, captures the number of times the winning team’s members died.
- `minionkills`: Discrete, measures the number of minions the winning team killed.
- `gamelength`: Continuous, provides the length of the match, influencing gold accumulation.
- `totalgold`: Discrete, measures the total gold earned by the winning team.
- `firstdragon`, `dragons`, `barons`, `towers`: Discrete, captures the number of key objectives taken.

All used quantitative features were scaled using `StandardScaler` to normalize the data.

We attempted to perform hyperparameter tuning but realized that the offset of runtime was not needed when considering its marginal results. In which case, the best hyperparameters settings are:
- `regressor__max_depth`: 20
- `regressor__min_samples_leaf`: 1
- `regressor__min_samples_split`: 10
- `regressor__n_estimators`: 300

### Model Performance
After training the model, we observed the following results:
- **Mean Squared Error (MSE)**: 4591782.9952
- **R-squared (R²)**: 0.9659

The more-than-average high R² value explain approximately 96.59% of the variance in the opponent's total gold (indicated by `totalgold_loser`) based on the winning team's objectives (such as dragons, barons, towers, etc.) and major statistics. This indicates a strong predictive capability, allowing us to understand how the objectives and performance metrics of the winning team correlate with the resources accumulated by their opponents.

Compared to our baseline model, which used fewer features, the final model's performance saw significant improvements. By adding features like `teamkills`, `teamdeaths`, and `minionkills`, we captured a more holistic view of the game dynamics, improving the model's predictive power. These features allowed the model to account for more nuances in how games progress and how gold is distributed between teams.

Although we did not tune hyperparameters in this iteration, the inclusion of more relevant features greatly enhanced the model's performance, showcasing that understanding in-game objectives in conjunction with kills and farming efficiency provides a more accurate prediction of the opponent’s total gold.

### Residuals and Actual vs Predicted Plot

Below is the **Actual vs Predicted** plot for our final model:

<iframe src="assets/scatter_actual_vs_predicted.html" width="100%" height="600px" frameborder="0"></iframe>

The **Actual vs Predicted Plot** helps in visualizing the accuracy of our model:
- **x-axis**: The actual total gold for the losing team (`totalgold_loser`).
- **y-axis**: The predicted total gold based on the winning team’s statistics.
The closer the points are to the red dashed line (representing perfect prediction), the better the model’s predictions. 

From the plot, it can be seen that most points lie near the red line, which shows that our model is performing well in predicting total gold for the losing team. 

Next, the **Residuals Plot** shows the difference between the actual and predicted values:

<iframe src="assets/residual_plot.html" width="100%" height="600px" frameborder="0"></iframe>

Residuals represent the difference between actual and predicted values (Residual = Actual - Predicted). A residual plot helps visualize how well the model's predictions match the actual values:
- **x-axis**: Residuals (difference between actual and predicted).
- **y-axis**: Frequency of residuals.

In the residual plot, most residuals are concentrated around zero, indicating that the majority of predictions are accurate. The presence of a few outlier residuals (further from zero) suggests some deviations, but these are within acceptable bounds for complex game data like this. 

#### Importance of Residuals and Actual vs Predicted Plot
The **residual plot** shows that our model's predictions are unbiased, as residuals are centered around zero without forming any noticeable patterns. The **actual vs predicted plot** confirms that the model has a strong predictive performance, as most predictions align closely with the actual values. While no model is perfect, the consistent alignment of points and the limited spread of residuals indicate that this model is plausible and reliable for predicting the losing team's total gold based on the winning team's objectives and in-game performance.

## Fairness Analysis

To determine whether our model is fair, we evaluate the model based on the **team kills to game length ratio** secured by the winning team. For short, we will call this new column `teamkills_ratio`.

Our question: "Does our model perform worse for games where the winning team has a lower teamkills_ratio (less aggressive games) compared to games with a higher teamkills_ratio (more aggressive games)?"

The reason to choose this question is because total gold of a team can vastly variate by how passive or aggressive a team plays. Passive games would mean that teams are "farming" for gold, having higher `minionkills` which equates to higher gold count. More aggressive games will have teams with higher `teamkills` per `gamelength` which mean that the gap of gold between the winning and losing team would be more divided. As seen many times above, matches tend to be "snowbally" or one-sided, a case where one team tends to have dominance throughout the match based on early performance. We fear that the model could potentially treat these two situations unfairly, favoring less agressive games as `totalgold` is more easily calculated based on `minionkills`; on the other hand, more aggressive games may have more variability which would interfere with the model's effectiveness. As such, we split the data into two groups as shown below:

- **Group X**: Teams with a **teamkills_ratio ≤ 0.01** (less aggressive games).
- **Group Y**: Teams with a **teamkills_ratio > 0.01** (more aggressive games).

The **teamkills_ratio** is defined as the number of team kills divided by the game length, which provides a normalized measure of the team's aggression throughout the match.

### Evaluation Metric

We selected **Mean Squared Error (MSE)** as our evaluation metric. We are predicting the total gold of the losing team and MSE helps us assess the accuracy of the predictions by showing the average squared difference between the predicted and actual values. Our models used Random Forest Regression which results in a metric of MSE. A lower MSE indicates better performance of the model.

Deciding our hypothesis requires us to consider the fairness between aggressive and passive games, as seen below:

- **Null Hypothesis (H₀)**: The model is fair. The MSE for teams with a **teamkills_ratio ≤ 0.0100** is roughly the same as the MSE for teams with a **teamkills_ratio > 0.01**, and any observed differences are due to random chance.
- **Alternative Hypothesis (H₁)**: The model is unfair. The MSE for teams with a **teamkills_ratio ≤ 0.0100** is different from the MSE for teams with a **teamkills_ratio > 0.01**.

We used the **difference in MSE** between Group X and Group Y as the test statistic, and we set our significance level at **0.05**.

### Results

- **Median teamkills_ratio**: 0.0100
- **Observed MSE difference**: -342769.32801399636
- **P-value**: 0.776

As displayed above, we decided to split the groups by the median teamkills_ratio of 0.01.

Since the p-value is greater than the significance level of 0.05, we fail to reject the null hypothesis.  There is no significant difference in the model's performance between the two groups; however, the p-value of 0.392 indicates that there is some effect of unfairness in the model. The negative observed MSE difference indicates that the model actually performs slightly better for the more aggressive games (higher teamkills_ratio), but the difference is not statistically significant.

The model appears to be fair with respect to the teamkills_ratio, and there is no evidence to suggest that it performs worse for games with a lower teamkills_ratio compared to games with a higher teamkills_ratio.


=======
https://klh005.github.io/2023-LoLObjectives-Report/
