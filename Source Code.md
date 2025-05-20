import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load road accident dataset
df = pd.read_csv('road_accidents.csv')

# Preview data
print(df.head())

# Basic stats
print(df.describe())

# Number of accidents per state or region
accidents_by_state = df['State'].value_counts()
accidents_by_state.plot(kind='bar', figsize=(10,5), title='Accidents by State')
plt.ylabel('Number of Accidents')
plt.show()

# Accidents by time of day
df['Hour'] = pd.to_datetime(df['Time'], errors='coerce').dt.hour
sns.histplot(df['Hour'].dropna(), bins=24, kde=False)
plt.title('Accidents by Hour')
plt.xlabel('Hour of Day')
plt.ylabel('Accident Count')
plt.show()
