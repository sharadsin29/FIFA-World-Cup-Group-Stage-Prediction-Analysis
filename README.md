# FIFA World Cup Group Stage Prediction Analysis

## Objective
Predict the outcomes of the 48 Group Stage Matches for the FIFA World Cup in Qatar using xG (Expected Goals) as the primary metric. 

## Introduction
Football is a complex sport to predict due to its fluid nature. Traditional methods like using past performances have been shown to be unreliable. This project aims to use xG, a more robust and indicative metric, to predict which teams will advance past the group stages in the FIFA World Cup.

## Dataset
The dataset includes xG values for international teams, sourced from Footystats. The xG metric takes into account factors like distance from the goal, the angle of the shot, etc.

- **Source**: [Footystats](https://www.footystats.org/)
- **Features**: Team Name, xG For, xG Against

![Dataset Sample](dataset_sample.png)

## Methodology

1. **Data Scraping**: Scraped xG statistics for the last 10 games for each team from Footystats.
2. **Data Preprocessing**: Handled missing values and normalized team names for the USA and South Korea.

3. **Simulation and Prediction**: 
   - **Monte Carlo Simulation**: Used a Monte Carlo simulation with Poisson distribution to simulate 10,000 match outcomes for each group stage match.
   - **Probabilistic Metrics**: Calculated the following metrics based on the simulated outcomes:
      - Home and Away team winning probabilities
      - Clean sheet percentages for Home and Away teams
      
   ```python
   matchups = win_cs(df=wc_df[0:48], home_goals_col='xG_adjusted_Home', away_goals_col='xG_adjusted_Away')
   ```

```python
# Example code for data preprocessing
# ...
```

## Results

Here are the teams predicted to advance through the group stages:

- Group A: Team1, Team2
- Group B: Team1, Team2
- ...
  
### Comparison with Expert Predictions

![Comparison Chart](comparison_chart.png)

## Conclusions
The project showcases the utility of xG as a more reliable predictor for football match outcomes, especially for events as unpredictable as the FIFA World Cup.

## Contact
For any further queries or job opportunities, feel free to reach out to me:
- LinkedIn: [Your LinkedIn Profile](https://www.linkedin.com/in/sharad-kumar-singh/)
- Email: sharadksingh97@gmail.com
