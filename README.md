# Basketball Moneyball

When most people hear the term "Moneyball", their minds go to the popular movie starring Brad Pitt and Jonah Hill. The basic premise of this, frankly, great movie was that the 2002 Oakland Athletics were faced with the unenviable task of assembling a championship-caliber roster within a budget that was approximately a third of the size of the other competitive teams. The 2001 Oakland Athletics had finished the season with 102 wins and had suffered a crushing loss to the New York Yankees, a team in-route to its fourth consecutive world series appearance and fifth in 6 years. To make matters worse, the Oakland Athletics were quickly outbid in their attempts to resign three key players: first baseman and 2000 American League MVP Jason Giambi signed with the aforementioned New York Yankees, outfielder Johnny Damon signed with Boston Red Sox, and relief pitcher Jason Isringhausen signed with the St. Louis Cardinals.


The loss of these key players should have devastated the franchise and eliminated them from contention but remarkably the exact opposite happened. While they again lost in 5 games in the ALDS, they somehow managed to not only remain competitive but even win more games than they had the previous season. They won the exact same number of games as the 2002 New York Yankees after losing their best offensive player to them and with a fraction of the payroll. How did they accomplish this seemingly impossible goal? As everyone should do when operating within a tight budget, they micromanaged their expenses. Rather than evaluating players with traditional statistics like batting average, they developed advanced statistics that correlated more strongly with winning games. They used these advanced statistics to find undervalued players that they could afford and were able to assemble a championship contending team.
My goal in this work is to apply a similar logic, albeit a different methodology, to the evaluation of basketball players. Traditional statistics like points per game do not necessarily correlate with winning. This works seeks to calculate a more advanced stat that can be used to find undervalued NBA players that could help a team contending for a championship. 


To do this, I calculated the regularized adjusted plus-minus score for every NBA player between 2011 and 2016 with aggregated data for the most common 5-player lineups during each season. Anyone who has ever been involved in the game of basketball has heard the phrase, "defense and rebounding wins championships". While both important, coaches are mainly trying to express the importance of these overlooked aspects of the game. However, the truest statement about what it takes to win is, "outscoring your opponent wins championships". While certainly a pedantic correction, this is exactly what RAPM tries to measure. How much does a team outscore their opponent on average with player X on the court?

We can calculate RAPM by first assembling a collection of individual plus/minus statistics for players. Plus/minus is the net score for a player while he is on the court. The problem with this statistic in isolation is that average players could have inflated plus/minus scores simply by being present on a very strong team. So how do we isolate his contribution to determine if he is the main cause for the plus/minus, or more of an bystander? I scraped the NBA.com website for plus/minus during individual "stints". Unfortunately, NBA.com only records aggregated data for the most common 5-player lineups. Ideally, we would have had more data snippits to work with but we had to work within the confines of our data constraints. Code was written to pull, clean, and extract the data into a large input matrix where each column represents a unique player and each row is a binary, sparse vector indicating which players were on the court. The y-vector is just the average net score of those players, on a per-minute basis. This was then multiplied by 36 to convert the value into a per-36 minute basis. 

Since we are also interested in finding players who are undervalued, we pulled salary information from ESPN.com. Note that a player could begin or end his NBA career within that time-frame as well, resulting in some missing salary information data. We resolved this by imputing the missing values with their average salaries. With the matrix constructed, I trained the RAPM model using CV-grid search. 
The RAPM player rankings were consistent with expectation. Perennial all-star players and the unanimously proclaimed “best-players” of the generation were towards the top of the rankings. However, we are not concerned with those players. We do not need a sophisticated model to tell us that LeBron James is a difference maker on a championship team, we are looking for the undervalued players. 

Using matplotlib, I plotted RAPM against salary and highlighted players who fell in the top 40% and top 25% of RAPM score and salary, respectively. In the upper-right quadrant, we begin to see the obvious choices (e.g., LeBron James, Kevin Durant, Chris Paul, etc.). Interestingly, Kobe Bryant had the league’s highest salary but fell towards the middle of this region. This is likely due to his post-Achilles tendon tear years, where he struggled to regain his form at. In the upper-left quadrant, these players are the ones I argue must be undervalued. Notice the presence of Stephen Curry, he notably __ ankles and was underpaid, as the Golden State Warriors were unsure whether or not he would ever be able to overcome these debilitating injuries. By the end of the 2016 season however, he had led the team to the 2015 NBA Championship, won 2 MVP’s (one of which made him the first unanimous MVP selection), and broke the 1996 Bulls record for most wins in a single season (73-9). Similarly, Kawhi Leonard blossomed into a perrential all-star during the 2016 season, hence his relatively low salary. 

Now let’s consider the non-obvious candidates in particular Kyle Korver and Jae Crowder. During this span, Kyle Korver is considered one of the greatest 3 point shooters of all time. His presence on the court is immensely valuable as he can consistently punish a defense for leaving him open. While Jae Crowder isn’t quite the shooter that Kyle Korver is, he was an excellent defender and could make open 3’s at an above average rate if left open. However, these are antecodal and rely on my knowledge of the game to validate their effectiveness. I performed a student’s t-test on the effective field goal percentage of players on players in the top 30% and bottom 30% of RAPM scores and were in the bottom 40% of salary. The basic premise here is that better role players should be able to score the ball more efficiently. This is not completely true since one can shoot the ball efficiently but lack the shot volume to impact the game significantly -  but we would expect this to be true for the most part. The p-value of the t-test was 0.00003 suggesting that there is a statistical difference and that the RAPM score is likely reasonably accurate. 




