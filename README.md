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

# 4 Plot a bar graph to show availability percentage

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

# ✅ Room type and price is given seperately

Let's compbine them
```
import matplotlib.pyplot as plt
price_by_room = listings.groupby('room_type')['price'].mean()
print(price_by_room)

# Plot price by room type
price_by_room.plot(kind='bar', color='cyan')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')

plt.show()
```
<img width="554" alt="image" src="https://github.com/user-attachments/assets/a419bccb-bf78-4d42-b72b-b785f0acfa77" />

# ✅ Which are the top 10 neighborhoods with the most listings?

```
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='lightcoral')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```
<img width="554" alt="image" src="https://github.com/user-attachments/assets/816917e4-e3f0-4adc-801e-e879c987e2b1" />

# ✅ Geographical Distribution of Listings (Price Colored)
```
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
<img width="555" alt="image" src="https://github.com/user-attachments/assets/dd4d1823-7063-4202-baa2-3f22c42ca476" />

# Let us see the listings on a real map
- Hotter Areas (Red/Yellow): High Density: The areas that appear in red or yellow (the   "hot" colors) indicate higher density or concentration of listings. This means there   are more listings in these areas. Popular Locations: These regions might be more     
  popular or in high demand. It could be near tourist attractions, popular 
  neighborhoods, or central areas in Hawaii where people tend to stay more often. 
  Colder Areas (Green/Blue):

- Low Density: Areas with blue or green (the "cold" colors) indicate a lower   
  concentration of listings. These regions have fewer listings available. Less Popular 
  Locations: These areas might be less popular or further from key attractions. If 
  you're looking at pricing or other factors, lower density could imply less 
  competition in these regions, which might indicate more affordable areas or less 
  tourist traffic. Density Patterns:

- Clustered Areas: If you notice clusters of heatmap intensity, they represent 
  hotspots. These might correspond to high-traffic areas like resorts, beaches, or 
  urban centers. Spread-Out Listings: If the heatmap shows a more uniform  
  distribution, it could suggest that listings are more evenly spread across the 
  region, which may reflect a more balanced demand for rentals across different areas 
  of Albany.

```
import folium
from folium.plugins import HeatMap
import pandas as pd


albany_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Albany
m = folium.Map(location=[42.65265406144247, -73.75935740854021], zoom_start=10)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in albany_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('Albany_heatmap.html')

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m
```
<img width="533" alt="image" src="https://github.com/user-attachments/assets/f4a2bc8d-790d-4eea-860d-73f1f47eb6a1" />

# 🚨 How do I find location for my city?
- Type your city name on google maps
- Click on What`s here
<img width="1464" alt="image" src="https://github.com/user-attachments/assets/61609d2e-6aa8-4eb3-a5ef-ea931ebfcf69" />
