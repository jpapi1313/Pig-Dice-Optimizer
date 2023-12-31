# Pig-Dice-Optimizer
A python code created to optimize a dice game called "Pig." This code utilizes loops, dataframes, and graphs to determine what strategy gives the player the greatest chance of winning.

**Introduction**
In our family, we enjoy playing a dice game known as Pig. The game utilizes a standard 6-sided die, with a unique twist: instead of the usual one dot, there's a pig illustration. 
Ever since I was a child, I knew that there should be a way to optimize this game. After all, the rules are elementary: A player simply rolls the dice as many times as they desire for each turn, each roll accumulates those points onto the total points per turn. The risk is that if the player rolls a pig then they get 0 points for that turn. The first player to reach 100 points wins.
To enhance the game strategy, I devised a practical approach. Instead of relying on intricate mathematical calculations, I chose a more direct method—leveraging the power of computation. By programming a computer to play tens of thousands of games and analyzing the outcomes, I aimed to uncover optimal strategies.


**Logic 1 - Stopping at x Number of Rolls**
First, I created a model out of some loops with the logic that the player would only roll x number of times then quit, regardless of what the score was. Here is my code for that simulation:

**Logic 1 Results**
The results were not surprising, once the player went up to 2 rolls per turn, the number of turns that player used to get up to 100 points became somewhat competitive. I determined that 5 rolls per turn is the optimum number of rolls, resulting in an average of around 13.5 turns.  Unsurprisingly, both 4 and 6 are also very near the 5 roll mark in terms of average turns, something that we will discuss later when we consider the real-world implementations.

![image](https://github.com/jpapi1313/Pig-Dice-Optimizer/assets/43052472/f21c848a-c363-4e59-94fb-91cc2825308a)
![image](https://github.com/jpapi1313/Pig-Dice-Optimizer/assets/43052472/607e6584-a04d-4b04-af74-a21d8b4c1626)

**Logic 2 - Stopping at x Points**
After Running this model, I thought of another strategy that could potentially be more optimized, rolling the dice until a certain number is reached for each turn. After all, if I were to roll the dice 5 times and rolled 2 every time I would only have 10 points but if I rolled 6 every time I would have 30. Rolling the dice an additional time would not garner the same risk/reward in both scenarios. By going to a certain point threshold and disregarding the number of rolls could help us find that perfect risk/reward location at which to end our turn. Here is the code I used to run that simulation:

**Logic 2 Results**
This model yielded an unexpected outcome. I initially anticipated a uniform parabolic trend, where the number of turns would gradually decrease, reach a minimum, and then ascend again. Contrary to this expectation, the graph exhibited intriguing wave-like patterns. As the points per turn increased, the number of turns decreased until reaching approximately 16 points. Subsequently, the count fluctuated slightly until showing a noticeable increase around 27 points. At 30 points, there was a significant decline in turns, approaching but not quite reaching the optimal point—determined, in this case, to be 19 points per turn, resulting in an average of around 13 turns. 
This model gave me an unexpected result. I assumed it would also be some form of a uniform parabola, where the turns would gradually decrease and then gradually increase again. I did not expect to see any wave like patterns as seen in the graph below. As the points per turn increase, the number of turns decreases until roughly 16 points. Then, the number of turns fluctuates up and down silightly until noticably increasing at roughly 27 points. At 30, the number of turns declines significantly where it gets near, but does not reach, the optimal point, which, using this method, happens to be 19. At 19 points per turn the player can average around 13 turns. This method also out performs the first method of stopping at x number of rolls by around .5 turns. This could be significant when playing 1,000 or 10,000 games but would not be noticeable in real life.
At first, when I saw this fluctuation I was concerned about the logic of my code and whether it was doing the optimization correctly. After thinking about it for a day or two I came up with a hypothesis that the fluctuations happen based on the probability of the number of rolls it takes to get to x number of points.
Statistically, rolling 15 points in 5 rolls is nearly as likely as rolling 20 in 5 rolls. To prove this, to you and myself, I plugged it into a dice calculator (omnicalculator.com). Of course the calculator doesn't account for the pig so 1's are allowed in the calculation, the concept is still valid. To roll 15 with 5 rolls has a probability of 0.0837191 and to roll 20 with the same number of rolls is 0.0837191, the exact same... The reason for this is because they both are possible with many combinations of numbers. Once we calculate the probability of rolling 25 with those 5 rolls the probability goes down to 0.0162037 and finally, rolling 30 with those 5 rolls would require us to roll a 6 every time so the probability is 0.0001286008. In short, there are certain single point increasing places along the score axis that result in a higher probability of the roll count going up than at other single point increases. For example, there is an entire 5 point stretch between 15 and 20 that all have the same probabilities with 5 rolls but as soon as we go from 25 (0.0162037) to 26 (0.00900206) we see the probability drop by .00720145. Over 0.7%. In essence, certain point increments along the score axis exhibit higher probabilities of increasing the roll count than others. This non-uniform probability distribution contributes to variations in the average turns required to complete the game, resulting in the observed waves. 
As for me and my family, I think we'll continue to trust our gut and other superstitions as to how far to push our luck, it's more fun that way. 

![image](https://github.com/jpapi1313/Pig-Dice-Optimizer/assets/43052472/c6c23d2c-8757-4e8d-ae12-2c91acc88639)
![image](https://github.com/jpapi1313/Pig-Dice-Optimizer/assets/43052472/d6e4d146-a669-41a3-b141-d1b3aa28b3f9)

**References**
Sas, Wojciech. “Dice Probability Calculator.” Omni Calculator, Omni Calculator, 6 Nov. 2023, www.omnicalculator.com/statistics/dice.
