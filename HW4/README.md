## Discussion

### Dataset
The dataset chosen was the "Dota2 Games Results". I am quite familiar with the game Dota 2 and play it regularly, which sparked my interest in this dataset. The dataset contains the following information in the columns:
1. Team won the game (1 or -1)
2. Cluster ID (related to location)
3. Game mode (eg All Pick)
4. Game type (eg. Ranked)
5 - end: Each element is an indicator for a hero. Value of 1 indicates that a player from team '1' played as that hero and '-1' for the other team. Hero can be selected by only one player each game. This means that each row has five '1' and five '-1' values.

### Data analysis
I remapped some of the column values to more convenient ones, such as 0 and 1. I also changed some column names to better represent the values contained in them.

One of the imortant statistics in Dota 2 is the hero pick rate, which represents the probability of a hero being picked by either team (how often the hero is picked). I calculate this value in order to discover which heroes are popular in this dataset. 

Another important statistic is which side (Dire or Radiant, in this case 0 or 1) has a higher win rate overall. This is calculated by simply dividing the number of victories of each side by total number of games. This can provide insight into inequality of the Dota 2 map, and whether any particular side has an advantage. For example, if one side has a much higher win rate, then any team has a higher chance to win using that win rate.

### Problem
The problem defined for this dataset is predicting the results of a given Dota 2 game (1 for win and 0 for loss). 

This is important information for anyone who wants to predict the result of a given game of Dota given the information, and most importantly the "draft". Every game of Dota 2 is played by 2 sides, with 5 players each. Each side chooses 5 heroes, and the resulting 10 heroes are called the Draft. Since the draft is just the beginning of the game, and a lot can affect the outcome of the game (such as players' skill, types of heroes picked, language restrictions, etc.), it is very difficult to predict the outcome of the game based on the draft. 

### Initial Approach
I used Logistic Regression to tackle the problem. I used LR because it is a good model for binary classification, especially where data is also binary. Logistic Regression has minimal hyperparameter tuning and good prediction results.

### Results and improvement

#### Initial Results
My initial prediction results results were as follows:
* Train accuracy: 0.6007987048030221
* Test accuracy: 0.5956868078492326

#### Reasons
These results are actually not too terrible, considering how volatile the results of Dota games are. 
I believe the main reason as to why the prediction accuracy is relatively low is because there are far too many factors which can affect the game to account for. Some of these factors are:
1. MMR (Match Making Rating)
2. Kills/Deaths/Assists
3. Roles picked (Carry/Mid/Support)
4. Hero gold
5. Roshan kills (Boosts the team)

For example, there is no data about player MMR (Match Making Rating) which represents a players skill level. A team of high MMR players would almost always win against a team of low MMR players, no matter what heroes are picked. Cases such as these might be outliers, and outliers greatly affect the Logistic Regression model. The chance of winning a Dota game is extremely erratic, and changes with these factors. 

There is an AI developed by the creators of Dota 2 (Valve Corporation) which predicts the probability of each team winning the game. I used such AI, and it is noticable how volatile the win probability is. For example, if one team is losing, but suddenly win a team-fight, earning a lot of gold, their win probability might jump by 10%. Therefore, Dota game win probability is best predicted in real time, rather than in draft phase.

Given that, having almost 60% accuracy in predicting the outcome of a Dota game based on draft is quite impressive.

#### My Approaches
In order to increase the accuracy of the prediction model, I tried to tune the hyperparameters to their optimal values. I used "sklearn.model_selection.GridSearchCV" which finds the best parameters for the given option of parameters of the given model. At the least, GridSearchCV takes in an estimator, parameters grid, and cv (Cross validation folds). For my implementation, The estimator is the Logistic Regression model, parameters are:
parameters = {'class_weight': ['None', 'balanced'],
'solver':['lbfgs', 'sag', 'saga'],
}
and cv is the default value of 5. I did not tune other parameters since they have either no effect, or no effect on the binary data that is in the dataset. 
The optimal parameters that GridSearchCV found are:
	class_weight': 'None'
	solver: 'lbfgs'
I also found the optimal value of the LR parameter C to be 0.7, using GridSearchCV. 

#### Improvement
After finding the optimal parameters, the prediction results were:
* Train accuracy: 0.6010577441985969
* Test accuracy: 0.5982125510005829

Evidently, the improvement to the accuracy of the prediciton is minimal, although present. This is to be expected, since as I mentioned earlier, predicting Dota 2 games is extremely difficult due to the flexibility, and volatility of the game.

### Conclusion
Overall the final accuracy of the Logistic Regression prediction model was just shy of 60%. This result might seem underwhelming to a person unfamiliar with Dota 2, and quite impressive to anyone who does have experience with the game. Tuning the hyperparameters of the Logistic Regression model minimally improved accuracy. 