# A Business Approach to Fantasy Football: Player Valuation and Risk Analysis

I made this Python project because I wanted to combine my interest in fantasy football with business and finance. Instead of just looking at which players score the most points, I wanted to see which players were actually the best draft picks based on where they were selected.

I thought it would be interesting to look at fantasy football like investing, where getting a good return for what you paid is important.

## Project Overview

This project uses 2026 NFL fantasy football data to compare where players were drafted with how they've performed so far this season.

Some questions I wanted to answer were:
- Who were the best picks in fantasy drafts?
- Which players have been the biggest disappointments?
- How much does draft position actually matter?
- Which players have been the most consistent?

**Data used:**
- 279 drafted quarterbacks, running backs, wide receivers, and tight ends
- 256 players with recorded stats
- 2026 NFL season through around Week 7
- PPR fantasy scoring

## Tools I Used

- Python
- Pandas and NumPy
- Matplotlib
- nflreadpy
- Google Colab
- FantasyPros ADP Rankings

## How I Made the Model

### 1. Getting the Data

First, I used nflreadpy to get weekly NFL player stats. I also downloaded preseason draft rankings from FantasyPros.

I cleaned up the data and matched the players from both datasets so I could compare their draft positions to their actual performances.

### 2. Comparing Players by Position

I didn't think it would make sense to compare every player the same way because some positions naturally score more points than others.

To fix this, I used replacement-level players in a 12-team fantasy league:

- QB12
- RB24
- WR24
- TE12

Basically, this gave me a way to compare each player to someone who could realistically replace them on a fantasy team.

### 3. Making an Investment Score

I created an investment score to rank players based on how well they've played and where they were drafted.

I used three different factors:

| Factor | Weight | What It Means |
|---|---|---|
| Production | 50% | How many points a player scores above replacement level |
| Draft Overperformance | 30% | How much better a player has been than expected |
| Bargain Value | 20% | How much value a player provides compared to their draft position |

I gave production the most weight because I still wanted good players to rank highly. But I also wanted to give credit to players who were drafted later and ended up being really good.

Players have to perform above replacement level to receive an investment score.

### 4. Finding the Worst Picks

I also wanted to figure out which players have been the worst draft picks.

For this, I made a separate score that looks at players drafted in the top 100 who are performing below replacement level. It also looks at players drafted in the first three rounds who have fallen at least 12 spots in their positional rankings.

This helped me find players who haven't performed as well as people expected.

### 5. Looking at Risk

I wanted to include risk because that's also important when looking at investments.

I measured it in two ways:

- **Weekly volatility:** How much a player's points change from week to week.
- **Downside risk:** How often a player scores fewer than 10 PPR points.

This helped me see which players were consistent and which ones had more ups and downs.

## What I Found

*Data through October 25, 2026.*

### Best Draft Picks

| Rank | Player | Position | Draft ADP | PPG | Investment Score |
|---|---|---|---|---|---|
| 1 | Kenneth Walker III | RB | 20.0 | 19.7 | 67.9 |
| 2 | D'Andre Swift | RB | 44.5 | 17.5 | 65.3 |
| 3 | Jaxon Smith-Njigba | WR | 8.0 | 23.6 | 63.6 |
| 4 | Jahmyr Gibbs | RB | 1.5 | 22.0 | 57.3 |
| 5 | Matthew Golden | WR | 162.0 | 14.4 | 55.8 |
| 6 | Christian Watson | WR | 66.5 | 17.0 | 54.1 |

Some results that stood out to me:

- D'Andre Swift was drafted around RB21 but is now performing as RB4.
- Matthew Golden went from WR54 in preseason rankings to WR8.
- Christian Watson was drafted around WR27 but is performing as WR3.

I thought it was interesting that Kenneth Walker and D'Andre Swift ranked higher than Jahmyr Gibbs, who was the first overall pick.

Even though Gibbs has played really well, Walker and Swift have been better values because they were drafted much later.

### Biggest Disappointments

| Player | Position | Draft ADP | Draft Position Rank | Current Position Rank | PPG |
|---|---|---|---|---|---|
| De'Von Achane | RB | 9.0 | 6 | 39 | 8.2 |
| Saquon Barkley | RB | 14.5 | 10 | 50 | 5.8 |
| A.J. Brown | WR | 26.0 | 8 | 67 | 6.4 |
| Omarion Hampton | RB | 12.5 | 7 | 29 | 9.6 |
| Brian Thomas Jr. | WR | 88.0 | 37 | 81 | 4.3 |

These players haven't performed nearly as well as their draft positions suggested they would.

One thing to keep in mind is injuries. For example, Achane has only played three games, so his ranking might not tell the whole story.

### Does Draft Position Matter?

I also looked at how many points players scored on average based on which round they were drafted in.

- First-round picks averaged about 19.5 points per game.
- Third-round picks averaged about 15.5 points per game.
- Players drafted in the ninth round or later averaged around 8–10 points per game.

This wasn't too surprising because better players are usually drafted earlier. But I still thought it was interesting to see the difference.

### Risk vs. Return

Kenneth Walker and Jaxon Smith-Njigba both had high investment scores and were also really consistent.

Neither had scored fewer than 10 PPR points in a game so far.

On the other hand, Christian Watson and Jaylen Warren had good investment scores but scored fewer than 10 points in about a third of their games.

This showed me that just looking at a player's average points doesn't always tell you how reliable they are.

## Limitations

There are a few things my model doesn't do perfectly.

- **Only part of the season:** I only used about seven weeks of data, so the rankings could change a lot.
- **Injuries:** Players who miss games are hurt in the rankings because their missed weeks count against their production.
- **Weights:** I picked the 50/30/20 weights myself based on what I thought mattered most.
- **Not a prediction model:** This model looks at how players have already performed. It doesn't predict future games.
- **Missing players:** There were 23 drafted players without recorded stats that weren't included.

## What I Want to Improve

There are a few things I would like to work on as I get better at Python.

- Update the rankings throughout the rest of the season.
- Try different weights to see how much the rankings change.
- Use data from past seasons to see if the model works well.
- Find a better way to account for players who miss games because of injuries.

## How to Run the Project

1. Open the notebook in Google Colab or Jupyter.
2. Download the FantasyPros 2026 Overall ADP Rankings CSV.
3. Put the file in the same folder as the notebook and name it `FantasyPros_2026_Overall_ADP_Rankings.csv`.
4. Run the cells. The first cell installs nflreadpy.

## What I Learned

This was my first time making a project like this, and I learned a lot about using Python to work with real data.

I got more practice with Pandas, cleaning datasets, making graphs, and creating my own scoring system.

I also learned that making a model isn't always straightforward. I had to change how I ranked players a few times because some of the results didn't make much sense at first.

Overall, I enjoyed working on something that combined fantasy football with my interest in business and finance. I want to keep improving the project as I learn more Python.
