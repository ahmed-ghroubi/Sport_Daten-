# Olympic Basketball & NBA Players Analysis

## Overview
This project analyzes the relationship between the number of NBA players in national basketball teams and their performance in the Olympic Games (measured by medals: Gold, Silver, Bronze, or no medal).

The goal is to explore whether having more NBA players increases the likelihood of winning medals and how this relationship evolves over time.

---

## Dataset
The dataset (`final_data`) contains historical Olympic basketball data, including:

- `Year` – Olympic year  
- `Team` – National team  
- `Medal` – Medal won (Gold, Silver, Bronze, or NaN)  
- `NBA` – Number of NBA players in the team  

---

## Methodology

### Data Preparation
- Filtered Olympic years (from 1948 onward, every 4 years)  
- Created team abbreviations for better visualization  
- Separated teams by medal type  
- Aggregated number of NBA players per team and year  

---

## Analysis & Visualizations

### Plot 1 – NBA Players in Medal-Winning Teams Over Time
- Stacked bar chart  
- Shows the number of NBA players in teams winning Gold, Silver, and Bronze medals  
- Includes annotations (e.g., USA absence in 1980)  

Insert Plot 1 here

---

### Plot 2 – Distribution of NBA Players by Medal Type
- Boxplot comparing:
  - Gold medal teams  
  - Silver medal teams  
  - Bronze medal teams  
  - Non-medal teams  
- Helps identify differences in team composition  

Insert Plot 2 here

---

### Plot 3 – Poisson Regression Analysis
- Applied Poisson regression to model:
  - Number of NBA players over time  
  - Separate models for each medal category  
- Visualized:
  - Predicted trends  
  - Differences between first and last Olympic years  

Insert Plot 3 here

---

## Key Findings
- Teams winning Gold medals tend to have more NBA players on average  
- The presence of NBA players has increased over time, especially in top-performing teams  
- The gap between medal-winning teams and non-medal teams is visible but not absolute  
- Regression results suggest a positive trend over time, particularly for high-performing teams  

---

## Technologies Used
- Python  
- Pandas  
- Plotly  
- Statsmodels  

---

## How to Run the Project

```bash
pip install pandas plotly statsmodels
