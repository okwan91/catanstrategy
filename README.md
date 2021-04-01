# Two Wheat It's Own
###### The strategy of Catan

### Background
The game Settlers of Catan is a game of strategy and resource management. Often, it is compared to the likes of Monopoly but it involves more than the luck of rolling dice to win. The board is in the shape of a hexagon where you have five resources that have their tiles randomly arranged on the board:
* Lumber
* Ore
* Brick
* Sheep
* Wheat

There is also a desert piece that is placed where the Robber is initially placed. The role of the Robber is for the player, who rolls a 7 from two dice, to rob a card from another player of choices hand depending on where they place the Robber next and who has a settlement there. On the outer edges of the board you'll notice a few ports with different resources one can trade for at a 2:1 ratio. If the port has a "?" then you may trade at a 3:1 ratio for the resource of your choice. If you do not have access to a port, you can always trade resources from your hand at a ratio of 4:1.

To start the game, player order is decided in descending order by who rolls the highest number with the dice. Each player places two settlements at the intersection of resources of their choosing. On top of each resource is also a randomly placed number. When a number is rolled, players who have a settlement touching that number collects the resource that rests under it. 

The goal of the game is to be the first at obtaining 10 points. Each settlement is worth 1 point, each city is worth 2. Points can also be obtained through development cards that could contain victory points or other useful *action cards* such as Knights that allow you to move the Robber and obtain a resource from a player.

### The Inspiration
I am a fairly new Settlers of Catan player have had about a handful of wins. However, I have yet to secure a win with a more seasoned player and so I decided to use machine learning modeling techniques to explore game strategies that can help increase my chances of winning. Is there a strategy that can best help me win? Or would I need Lady Luck on my side?

### Exploratory Data Analysis
This dataset contains 50 rounds of games among 4 players. Player 2 secured the most wins at 18 games, followed by Player 3, 4, and 1. While exploring the wins, the top resource that helped secure a win was Sheep followed by Wheat and Lumber. This makes sense since the game has 4 tiles for each of those 3 resources, and 3 tiles for the remaining resources Brick and Ore. In addition, Sheep are required in order to build settlements or obtain development cards which could contain victory points.

Below shows the rankings of our players and the average amount of points they garnered across all 50 games.

![alt text](https://github.com/okwan91/catanstrategy/blob/main/Graphs/wonmostavg.png)

It appears that Player 2 faired the best while Player 1 won the least amount of times. The following graphs shows comparisons between the resources they would station their starting settlements the most, and how they differed between their overall gameplay vs winning gameplay.

#### Player 1
![alt text](https://github.com/okwan91/catanstrategy/blob/main/Graphs/player1gameplay.png)

![alt text](https://github.com/okwan91/catanstrategy/blob/main/Graphs/player1winplay.png)

Skimming through Player 1's game strategy, he appears to favor placing his starting settlements by ports. This could be because of the advantage of trading resources at a designated port requires less resources. However, a drawback is to place a settlement by a port, you could be sacrificing one or two resource tiles.

#### Player 2
![alt text](https://github.com/okwan91/catanstrategy/blob/main/Graphs/player2gplay.png)

![alt text](https://github.com/okwan91/catanstrategy/blob/main/Graphs/player2win.png)

Compared to Player 1, Player 2 would station his starting settlements on Wheat, Lumber, or Sheep, which clearly worked in his favor since he had the most wins. It can also be noted that he had a significantly higher resource production compared to Player 1.

### Building the Model
The model I chose to utilize for this was a Random Forest Regressor. After I built a model utilizing all of the given features in the dataset and observed which features had the highest correlation to a winning game. After mutliple rounds of pruning and feature reduction, I had narrowed down my features to Resource Production, Trade Gain/Loss, Robber Gain/Loss, Tribute (cards you must discard if a 7 is rolled). Some issues I ran into while pruning the model was multicollinearity between some features, such as Resource Production and starting Settlement numbers and resources. Production of resources is highly dependent on where your starting settlements are. Having a settlement on numbers such as 5, 6, 8, and 9 put a player at an advantage because those numbers have higher rates of occuring. As shown below:

![alt text](https://github.com/okwan91/catanstrategy/blob/main/Graphs/diceavg.png)

Combining those numbers with resources that have more tiles on the board (Wheat, Lumber, Sheep), it gives you an advantage of a higher chance of producing more resources each roll. 

Below displays our top 6 features for success in a game, with Production in the lead followed by Robber Gain.

![alt text](https://github.com/okwan91/catanstrategy/blob/main/Graphs/top6feat.png)

When plotting Resource Production against points gained during a game, you can see that if you have a higher resource production rate it can lead to a higher amount of points.

![alt text](https://github.com/okwan91/catanstrategy/blob/main/Graphs/resourcevspoints.png)

After refining the model, I was able to obtain an accuracy score between 75-80% and an R2 score between .44-.50 and an mean squared error score of 2.34.

I also tried a logistic regression model on this dataset, using the features that were narrowed down by the random forest mode and it faired a little better. Accuracy scores ranged between 80-86% and an R2 score of .68 and a mean squared error of 1.53. However the most importan feature according to a logistic regression model was Trade Gain, followed by Resource Production.

### So, How can I win?

My advice for you to have a high chance of winning is to have your two starting settlements favoring Wheat, Lumber, and Sheep along with numbers between 5-9 in order to have a high production rate. Ports will cost you resources so if you want to be able to utilize the benefit of lower trading costs, you should first place your settlements somewhat near a port while still having access to 3 resources. Then you can slowly build your way to a port to utilize its benefits without sacrificing resource production. As quickly as you are able to produce resources, you also want to spend those resources at a moderate rate to avoid the risk of having to discard them when a 7 is rolled or becoming a target for other players. 

Placing your settlement has a benefit I've observed, where you will suffer lower Robber Losses and a less likely target if another player rolls a 7 or utilizes a Knight to rob someone. Speaking of the Robber, robbing other players of the resources in their hands will help you obstruct their path to a win by preventing them from being able to develop their settlements or obtain a Development card that could potentially be a victory point. 

### Future Questions
1. Does player stance affect your chances of winning? This feature was not available in this dataset. I'd like to find one that does have this data recorded to see if it has a strong impact on gameplay.
2. Development card performance, are victory points really as important as they seem? Should a player aim to gain as many victory points as possible in comparison to other cards such as "The Largest Army" or "The Longest Road?"
 
