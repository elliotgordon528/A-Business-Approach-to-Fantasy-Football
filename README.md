# A Business Approach to Fantasy Football: Player Valuation and Risk Analysis

A Python project that evaluates NFL fantasy football players the way an investor evaluates assets. It compares each player's preseason draft cost (ADP) with their actual production, then ranks players by return relative to cost and measures how risky each one has been week to week.

## Project Overview

Most fantasy rankings ask who scores the most points. This project asks a different question: **who delivered the best return on their draft price?** It applies business concepts (valuation, return on investment, replacement level, and downside risk) to 2026 NFL data.

- **Scope:** 279 drafted QB/RB/WR/TE players, 256 of whom have recorded NFL stats
- **Season coverage:** 2026 regular season through roughly Week 7 (analysis run as of Oct 25, 2026)
- **Scoring:** PPR (points per reception)

## Tools and Technologies

- Python
- Pandas and NumPy
- Matplotlib
- nflreadpy (NFL player stats)
- Google Colab
- FantasyPros 2026 Overall ADP Rankings (preseason draft data)

## Methodology

1. **Collect and clean data.** Load 2026 weekly player stats with `nflreadpy`, keep regular season QB/RB/WR/TE players, and match them to FantasyPros ADP data using standardized player names.
2. **Set replacement level.** For each position, replacement level is the production of the last "startable" player in a 12-team league (QB12, RB24, WR24, TE12).
3. **Score each player.** Players above replacement level receive an investment score:

| Component | Weight | What it measures |
|---|---|---|
| Production | 50% | Fantasy points per week above replacement level |
| Draft Overperformance | 30% | How many positional ranks a player beat his draft position by |
| Bargain Value | 20% | Production above replacement relative to draft cost |

4. **Identify busts.** A separate disappointment score flags top-100 draft picks who performed below replacement level, or first-to-third-round picks who fell 12 or more positional ranks.
5. **Measure risk.** Risk is measured two ways: weekly scoring volatility (standard deviation of weekly points) and downside risk (the share of games under 10 PPR points).

## Key Findings

*As of Oct 25, 2026.*

### Best draft investments

| Rank | Player | Pos | Draft ADP | PPG | Investment Score |
|---|---|---|---|---|---|
| 1 | Kenneth Walker III | RB | 20.0 | 19.7 | 67.9 |
| 2 | D'Andre Swift | RB | 44.5 | 17.5 | 65.3 |
| 3 | Jaxon Smith-Njigba | WR | 8.0 | 23.6 | 63.6 |
| 4 | Jahmyr Gibbs | RB | 1.5 | 22.0 | 57.3 |
| 5 | Matthew Golden | WR | 162.0 | 14.4 | 55.8 |
| 6 | Christian Watson | WR | 66.5 | 17.0 | 54.1 |

- **D'Andre Swift** was drafted as roughly RB21 and is performing as RB4.
- **Matthew Golden** jumped from WR54 in the preseason rankings to WR8.
- **Christian Watson** was drafted as roughly WR27 and is performing as WR3.
- The best investments are not simply the highest scorers. Walker and Swift rank above Gibbs, the top overall pick, because they produced similar value at a much lower draft cost.

### Biggest disappointments

| Player | Pos | Draft ADP | Draft Pos. Rank | Current Pos. Rank | PPG |
|---|---|---|---|---|---|
| De'Von Achane | RB | 9.0 | 6 | 39 | 8.2 |
| Saquon Barkley | RB | 14.5 | 10 | 50 | 5.8 |
| A.J. Brown | WR | 26.0 | 8 | 67 | 6.4 |
| Omarion Hampton | RB | 12.5 | 7 | 29 | 9.6 |
| Brian Thomas Jr. | WR | 88.0 | 37 | 81 | 4.3 |

Achane has played only 3 games, so his ranking reflects a small sample.

### Draft round production

Average PPG falls steadily with draft round: first-round picks average about 19.5 PPG, third-round picks about 15.5, and picks from the ninth round on average roughly 8 to 10.

### Risk versus return

Kenneth Walker III and Jaxon Smith-Njigba have the top investment scores with no games under 10 PPR points so far. Christian Watson and Jaylen Warren score well but carry more downside risk, with about a third of their games under 10 points.

## Limitations

- **Partial season.** The analysis covers roughly the first seven weeks, so rankings will shift as more games are played. Small samples (such as players with 3 games) can distort results.
- **Missed games.** Points per week divides by total weeks in the dataset, not games played, so players who missed games are penalized in the production and replacement-level calculations. Downside-risk calculations exclude missed games.
- **Subjective weights.** The 50/30/20 weighting is a judgment call, not a statistically fitted result.
- **Historical, not predictive.** The model measures past value. It does not forecast future performance.
- **Unmatched players.** 23 drafted players had no recorded stats and are excluded.

## Future Improvements

- Update the model weekly through the rest of the season
- Run a sensitivity analysis to test how rankings change under different weights
- Backtest the scoring model on previous seasons
- Normalize production by games played to handle injuries more fairly

## How to Run

1. Open the notebook in Google Colab or Jupyter.
2. Download the FantasyPros 2026 Overall ADP Rankings CSV and place it in the same folder as the notebook, named `FantasyPros_2026_Overall_ADP_Rankings.csv`.
3. Run all cells. The first cell installs `nflreadpy`.
