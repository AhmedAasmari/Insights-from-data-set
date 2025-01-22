# Insights-from-data-set
doing an analysis for the dataset about paris:
* For the following analysis, I have downloaded the following data from: https://data.insideairbnb.com/france/ile-de-france/paris/2024-09-06/data/calendar.csv.gz
⁠
``` diff
import pandas as pd
data = pd.read_csv('calendar.csv')
```
 
# :white_check_mark: We need to know the number of available and unavailable rooms

```diff
data.available.value_counts()
```
<img width="210" alt="image" src="https://github.com/user-attachments/assets/3c06fe7c-0a84-490a-bc90-0c04c1689e75" />


T stands for available, F stand for not available

# 2 Purpose: Calculates the percentage of available (t) and unavailable (f) dates.
Explaination: value_counts(normalize = True) gives proportions. Multiplying 100 converts the proportions into percentage
``` diff
availavility_percentage = data['available'].value_counts(normalize=True) * 100
availavility_percentage
```
<img width="266" alt="image" src="https://github.com/user-attachments/assets/66050a9e-306d-4125-b8f5-cb8332c898b4" />
