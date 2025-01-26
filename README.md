# Insights-from-data-set
doing an analysis for the dataset about paris:
* For the following analysis, I have downloaded the following data from: https://data.insideairbnb.com/france/ile-de-france/paris/2024-09-06/data/calendar.csv.gz
⁠
```
import pandas as pd
data = pd.read_csv('calendar.csv')
```
 
# 1 :white_check_mark: We need to know the number of available and unavailable rooms

```
data.available.value_counts()
```
<img width="210" alt="image" src="https://github.com/user-attachments/assets/3c06fe7c-0a84-490a-bc90-0c04c1689e75" />


T stands for available, F stand for not available

# 2 Purpose: Calculates the percentage of available (t) and unavailable (f) dates.
Explaination: value_counts(normalize = True) gives proportions. Multiplying 100 converts the proportions into percentage

```
availability_percentage = data['available'].value_counts(normalize=True) * 100
availability_percentage
```
<img width="266" alt="image" src="https://github.com/user-attachments/assets/66050a9e-306d-4125-b8f5-cb8332c898b4" />

# 3 Let's Count the busiest day! :triangular_flag_on_post:

```
busiest_dates = data[data['available'] == 'f']['date'].value_counts()
print('Busiest Dates:')
print(busiest_dates.head())
```
<img width="266" alt="image" src="https://github.com/user-attachments/assets/4271d577-51d4-4d28-b5aa-6ba79dc54116" />

# 4 Plot a bar graph tp show availability percentage

```
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['green','red'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Avilable (t/f)')
plt.show()
```
<img width="562" alt="image" src="https://github.com/user-attachments/assets/f055578b-a709-4ad2-bcc0-bef9bacc7f58" />

# 5 Plot the busiest day

```
busiest_dates.head(10).plot(kind='bar', color='skyblue')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
<img width="589" alt="image" src="https://github.com/user-attachments/assets/9d356d45-cc62-4383-b5d4-8347b453495f" />

## ➕After that, we need to Download listings dataset of Hawaii from this link: https://data.insideairbnb.com/united-states/hi/hawaii/2024-09-13/data/listings.csv.gz

```
import pandas as pd
listings = pd.read_csv('listings.csv')
```

## Check the columns

```
listings.columns
```
<img width="564" alt="image" src="https://github.com/user-attachments/assets/3ba156f7-5fef-43ce-a63c-84ee126c7103" />

