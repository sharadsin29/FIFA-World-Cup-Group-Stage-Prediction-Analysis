# FIFA World Cup Group Stage Prediction Analysis

## TLDR
Football is a complex sport to predict due to its fluid nature. Traditional methods like using past performances have been shown to be unreliable. This project aims to use xG, a more robust and indicative metric, to predict which teams will advance past the group stages in the FIFA World Cup.

## Objective
Predict the outcomes of the 48 Group Stage Matches for the FIFA World Cup in Qatar using xG (Expected Goals) as the primary metric. 

## Introduction

#### The Challenge of Predicting Football

Football (Soccer) is one of the hardest sports to predict due to the free-flowing nature of the game, unlike other sports which are more of a stop-start nature. This fluidity makes football quite unique and also quite difficult to predict. Nonetheless, I shall attempt to run simulations and try to come up with predictions.

#### Limitations of Using Past Results

The most common approach to prediction is to use past results as an indicator of future performances. However, this method, while having some merit, doesn’t always hold true. For instance, no one would’ve predicted coming into the 2010 World Cup that Italy, the World Cup winners of 2006, would fail to get past the group stages. Similar fates have befallen other World Cup winners like Spain and Germany. Hence, we cannot solely rely on past results as an indicator for future outcomes.

#### The Need for a Reliable Metric

We need a metric that can fully encompass the events in a match and also be indicative of the eventual outcome of the game. As we know, scorelines can often be deceptive. We’ve all witnessed the classic “smash and grab” phenomenon where one team keeps on piling up the pressure on the opponent’s goal only to be undone by a counterattack. The scoreline in those games isn’t indicative of the team’s performance.

#### The Role of Expected Goals (xG)

Fortunately, there exists such a metric that allows us to capture most of the nuances in a game and be used as a fair indicator of the teams’ performance. It’s called xG (Expected Goals). This metric is calculated for each attempt on goal and takes into account various factors like distance from goal, the angle from which the shot is taken, and other similar factors. The purpose of xG is not to predict right before a shot gets taken whether it’ll be a goal or not. Rather, it is supposed to be used to assess the quality of a chance and thereby the quality of the team’s performance.


## Dataset
The dataset includes xG values for international teams, sourced from Footystats. The xG metric takes into account factors like distance from the goal, the angle of the shot, etc.

- **Source**: [Footystats](https://www.footystats.org/)
- **Features**: Team Name, xG For, xG Against

![Dataset Sample](dataset_sample.png)

## Methodology

1. **Data Scraping**: Scraped xG statistics for the last 10 games for each team from Footystats using R.
2. **Data Preprocessing**: Handled missing values and normalized team names for the USA and South Korea.
3. **Home Advantage Adjustments**(Optional): The Home and Away are being used as mere labels and there is no such advantage associated with the home team (this can be adjusted for club matches where there is an actual advantage) although we could probably give a Boost to the actual Home nation Qatar. But as we've seen in the past world cups where weaker teams were host nations, for instance, South Africa in 2010, there isn't much advantage to the host nation unless they are ranked in the top 20 teams in the world.
4. **Matchup Adjustments**: In order to adjust the xG values according to the Matchup, we are going to multiply the xG values of the team with their opponent's xGA values and divide it by the average xG value for all the 32 teams combined. This method is flexible enough to account for the relative strengths of the teams. For instance, if we have a strong team playing against a weaker team their xG value will go up as their own xG values will be quite high and their opponent's xGA value will also be quite high resulting in a higher adjusted value which depicts their strength comparative to the opponent they are facing.

   ```python
   xG_avg = df['xGFor'].mean()
   wc_df['xG_adjusted_Home']= (wc_df['xG_Home'] * wc_df['xGA_Away']) / xG_avg
   wc_df['xG_adjusted_Away']= (wc_df['xG_Away'] * wc_df['xGA_Home']) / xG_avg
   ```
   
6. **Simulation and Prediction**: 
   - **Monte Carlo Simulation**: Used a Monte Carlo simulation with Poisson distribution to simulate 10,000 match outcomes for each group stage match.
   - **Probabilistic Metrics**: Calculated the following metrics based on the simulated outcomes:
      - Home and Away team winning probabilities
      - Clean sheet percentages for Home and Away teams
      - Creating an Additional metric to determine the games that are most likely to have more than two goals scored and thereby being an entertaining watch
      

## Results

Here are the teams predicted to advance through the group stages:

- Group A: <span style="color: green;">Netherlands</span>, <span style="color: green;">Senegal</span>
- Group B: <span style="color: green;">England</span>, <span style="color: green;">USA</span>
- Group C: <span style="color: red;">Mexico</span>, <span style="color: green;">Argentina</span>
- Group D: <span style="color: green;">France</span>, <span style="color: red;">Tunisia</span>
- Group E: <span style="color: red;">Germany</span>, <span style="color: green;">Spain</span>
- Group F: <span style="color: green;">Morocco</span>, <span style="color: green;">Croatia</span>
- Group G: <span style="color: green;">Brazil</span>, <span style="color: green;">Switzerland</span>
- Group H: <span style="color: green;">Portugal</span>, <span style="color: green;">South Korea</span>

Of the three predictions that the model incorrectly made, all three teams finished third in their respective groups, indicating that the predictions were not significantly off. Notably, both Germany and Mexico concluded with the same number of points as the second-placed teams in their groups, missing out on progression solely due to goal difference. Additionally, each of these three teams amassed a total of 4 points.

Total Score: 13/16
  
### Comparison with Expert Predictions

<p align="center">
  <img src="https://github.com/sharadsin29/FIFA-World-Cup-Group-Stage-Prediction-Analysis/blob/main/img/CraigPred.png" width="250px" height="200px"/>
  <br>
  <em>Craig's Prediction: 11/16</em>
</p>
<p align="center">
  <img src="https://github.com/sharadsin29/FIFA-World-Cup-Group-Stage-Prediction-Analysis/blob/main/img/DanPred.png" width="250px" height="200px"/>
  <br>
  <em>Dan's Prediction: 10/16</em>
</p>
<p align="center">
  <img src="https://github.com/sharadsin29/FIFA-World-Cup-Group-Stage-Prediction-Analysis/blob/main/img/DonPred.png" width="250px" height="200px"/>
  <br>
  <em>Don's Prediction: 12/16</em>
</p>
<p align="center">
  <img src="https://github.com/sharadsin29/FIFA-World-Cup-Group-Stage-Prediction-Analysis/blob/main/img/FrankPred.png" width="250px" height="200px"/>
  <br>
  <em>Frank's Prediction: 9/16</em>
</p>
<p align="center">
  <img src="https://github.com/sharadsin29/FIFA-World-Cup-Group-Stage-Prediction-Analysis/blob/main/img/ShakaPred.png" width="250px" height="200px"/>
  <br>
  <em>Shaka's Prediction: 10/16</em>
</p>
<p align="center">
  <img src="https://github.com/sharadsin29/FIFA-World-Cup-Group-Stage-Prediction-Analysis/blob/main/img/GabPred.png" width="250px" height="200px"/>
  <br>
  <em>Gab's Prediction: 10/16</em>
</p>


## Conclusions
As I reflect on the incredible spectacle that unfolded in Qatar, watched by approximately 5 billion people, I'm transported back to August 2022. It was three months before the start of the tournament, and I was deeply immersed in a project, part of an assignment that now holds a newfound significance. This piece of my past had slipped from my memory, but recently, my friend Samuel brought it back to my attention. His reminder has not only rekindled my interest but also connected me once again with the work I had almost forgotten amidst the grandeur of the global event.

The results are impressive: my model correctly predicted 13 out of 16 outcomes, including the tournament's biggest shock – Morocco outqualifying Belgium, the world's number one ranked team at the time. Although my model foresaw this stunning upset, I was too skeptical to trust its predictions and prematurely abandoned the project without forecasting the rest of the tournament. Nevertheless, my model outperformed many expert football pundits, lending credibility to the approach.

I hope you've enjoyed this intersection of two of my passions: Football and Data Science. Thank you for reading this far.

## Contact
For any further queries or job opportunities, feel free to reach out to me:
- LinkedIn: [LinkedIn Profile](https://www.linkedin.com/in/sharad-kumar-singh/)
- Email: sharadksingh97@gmail.com
