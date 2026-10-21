# A Business Approach to Fantasy Football: Player Valuation and Risk Analysis

## Project Overview

This project uses Python to analyze NFL fantasy football performance through a business and investment perspective. By comparing preseason average draft position (ADP) with actual player production, the goal is to identify which players have provided the greatest value relative to their draft cost.

## Tools and Technologies

- Python
- Pandas
- Matplotlib
- nflreadpy
- Google Colab

## Methodology

I developed a weighted investment scoring model based on three factors:

- **50% Production:** Fantasy points scored relative to replacement-level players.
- **30% Draft Overperformance:** How much a player exceeded expectations based on preseason draft position.
- **20% Bargain Value:** Production relative to the player's original draft cost.

The analysis also measures weekly scoring volatility and downside risk, defined as the percentage of recorded games with fewer than 10 PPR points.

## Key Features

- NFL player performance data analysis
- Preseason ADP comparisons
- Positional replacement-value calculations
- Player investment rankings
- Risk versus return visualizations

## Limitations

The analysis uses partial-season data and evaluates historical performance rather than predicting future results. The model's weights are subjective, and downside-risk calculations exclude missed games.

## Future Improvements

Update the model throughout the NFL season as new player statistics become available.
