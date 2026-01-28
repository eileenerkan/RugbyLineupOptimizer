# Sports Lineup Optimizer

This project uses **Ridge Regression** and **Linear Programming** to determine the most effective 4-player lineup for a focal team against a specific opponent. It calculates individual player contributions from stint-level data and optimizes the lineup based on a team rating cap.

## Features
* **Ridge Regression Modeling**: Estimates individual player "goal rates" while accounting for teammate quality.
* **Linear Programming Optimization**: Uses the `PuLP` library to maximize team value under a strict rating constraint (e.g., total rating ≤ 8.0).
* **Scenario Simulation**: Easily test "What-if" scenarios, such as player injuries (unavailability) or fatigue (performance penalties).
* **Automated Reporting**: Generates a clean summary table of the best lineups across different game conditions.

## Requirements
Ensure you have the following Python libraries installed:
```bash
pip install pandas numpy scikit-learn pulp
```
## Data Input
The script requires two CSV files:
1. player_data.csv: Must contain player names and their corresponding rating.
2. stint_data.csv: Must contain game stints including h_team, a_team, minutes, h_goals, a_goals, and player columns (home1-4, away1-4).

## Configuration
You can customize the analysis directly in the script's configuration section (cell 2):
- FOCAL_TEAM: The team you are optimizing for (e.g., "Canada").
- OPPONENT: The team you are facing (e.g., "Sweden").
- RATING_CAP: The maximum allowable sum of player ratings in a lineup.
- ALPHA: The regularization strength for the Ridge model.

## Example Output
| Scenario | Lineup | Total Value | Total Rating |
| :--- | :--- | :--- | :--- |
| **Baseline** | Canada_p1, Canada_p3, Canada_p5, Canada_p7 | 0.8421 | 7.80 |
| **Missing Star** | Canada_p1, Canada_p3, Canada_p5, Canada_p9 | 0.7105 | 7.50 |
| **Fatigue** | Canada_p1, Canada_p5, Canada_p7, Canada_p10 | 0.6543 | 7.90 |
