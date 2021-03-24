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
This dataset contains 50 rounds of games among 4 players. Player 2 secured the most wins at 18 games, followed by Player 3, 4, and 1. While exploring the wins, the top resource that helped secure a win was Sheep followed by Wheat and Lumber. This makes sense since the game has 4 tiles for each of those 3 resources, and 3 tiles for the remaining resources Brick and Ore. 

[insert table here]

In addition, Sheep are required in order to build settlements or obtain a development card. 

### Building the Model
The model I chose to utilize for this was a Random Forest Regressor. After I built a model utilizing all of the given features in the dataset, I extracted the top features that 

