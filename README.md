# FIFA World Cup 2026 Predictor & Tournament Simulator
**Probabilistic Sports Analytics & Monte Carlo Simulation Engine**

## Overview
An end-to-end sports analytics pipeline built to model match outcome distributions and simulate the expanded 48-team tournament structure for the 2026 FIFA World Cup across the United States, Mexico, and Canada.

## Pipeline Architecture

### 1. Dynamic Feature Engineering & Elo Engine
- Tracks historical international match results from 2000 to present day.
- Implements a custom Elo rating system with dynamic tournament-tier K-factors (Friendly: 14, Major Tournament: 34), goal margin multipliers ($\ln(\Delta\text{G} + 1) + 1$), and home/neutral venue adjustments.
- Computes 20-match rolling form features (goals scored, goals conceded, points earned) for both home and away sides.

### 2. Probabilistic Goal Modeling (Poisson GLM)
- Trains a regularized **Poisson Regressor** ($\alpha=0.002$) within an scikit-learn standard scaling pipeline.
- Generates team-specific expected goal intensities ($\lambda_1, \lambda_2$) adjusted for FIFA rank differentials, team playstyle overrides (attack vs. defense tempos), and venue geographic factors.
- Computes full bivariate score distributions ($9 \times 9$ matrix, 81 discrete outcomes) using independent Poisson probability mass functions to derive exact win, draw, and loss probabilities.

### 3. Tournament Simulation Engine
- **Group Stage:** Simulates all 72 group-stage fixtures across 12 groups (A–L), applying standard tiebreakers (Points, Goal Difference, Goals For, Head-to-Head).
- **Bracket Resolution:** Formulates third-place qualification (top 8 of 12) and assigns them to the Round of 32 knockout grid using recursive backtracking.
- **Knockout Simulation:** Evaluates 90-minute regulation, 30-minute extra time goal intensities, and penalty shootout win probabilities scaled by Elo disparity.
- **Interactive Visualizations:** Renders win probability bar charts, bivariate score heatmaps, team strength maps, and knockout bracket trees via Plotly.

## Tech Stack
- **Languages:** Python 3.10+
- **Machine Learning & Modeling:** scikit-learn (`PoissonRegressor`, `StandardScaler`), SciPy (`poisson`), NumPy, Pandas
- **Visualization:** Plotly Express & Graph Objects
- **Environment:** Jupyter / Google Colab
