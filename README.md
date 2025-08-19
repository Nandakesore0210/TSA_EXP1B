# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 18/8/25

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

file_path = "/content/AirPassengers.csv"
data = pd.read_csv(file_path)

if 'Month' not in data.columns:
    data.rename(columns={data.columns[0]: 'Month'}, inplace=True)

if '#Passengers' not in data.columns:
    data.rename(columns={data.columns[1]: '#Passengers'}, inplace=True)

data['Month'] = pd.to_datetime(data['Month'], errors='coerce')
data = data.dropna(subset=['Month'])
data.set_index('Month', inplace=True)

data['#Passengers'] = pd.to_numeric(data['#Passengers'], errors='coerce')
data = data.dropna()

data['passengers_diff'] = data['#Passengers'] - data['#Passengers'].shift(1)

result = seasonal_decompose(data['#Passengers'], model='additive', period=12)
data['passengers_sea_diff'] = result.resid

data['passengers_log'] = np.log(data['#Passengers'])

data['passengers_log_diff'] = data['passengers_log'] - data['passengers_log'].shift(1)

result = seasonal_decompose(data['passengers_log_diff'].dropna(), model='additive', period=12)
data['passengers_log_seasonal_diff'] = result.resid

plt.figure(figsize=(16, 18))

plt.subplot(6, 1, 1)
plt.plot(data['#Passengers'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('No of Passengers')

plt.subplot(6, 1, 2)
plt.plot(data['passengers_diff'], label='Regular Differencing')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced No of Passengers')

plt.subplot(6, 1, 3)
plt.plot(data['passengers_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally Adjusted Passengers')

plt.subplot(6, 1, 4)
plt.plot(data['passengers_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(No of Passengers)')

plt.subplot(6, 1, 5)
plt.plot(data['passengers_log_diff'], label='Log + Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff(Log(No of Passengers))')

plt.subplot(6, 1, 6)
plt.plot(data['passengers_log_seasonal_diff'], label='Log + Regular + Seasonal Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Differencing + Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(No of Passengers)))')

plt.tight_layout()
plt.show()

data.plot(kind='line', figsize=(14, 7), title="All Transformations")
plt.show()

print("\nFinal Data (first 10 rows):")
print(data.head(10))

```


### OUTPUT:

#### Original Data:
<img width="1732" height="303" alt="image" src="https://github.com/user-attachments/assets/3853d759-d575-42ff-9f1a-50e961b43a59" />

#### REGULAR DIFFERENCING:
<img width="1737" height="328" alt="image" src="https://github.com/user-attachments/assets/b70520da-1240-4013-8ab9-27fea6208a6a" />

#### SEASONAL ADJUSTMENT:
<img width="1740" height="325" alt="image" src="https://github.com/user-attachments/assets/e3782e4a-bb19-4865-bf01-2d9f6885936c" />

#### LOG TRANSFORMATION:
<img width="1747" height="317" alt="image" src="https://github.com/user-attachments/assets/97c1560e-e146-4ae7-a398-f81587210033" />

#### Log Transformation and Regular Differencing:
<img width="1748" height="308" alt="image" src="https://github.com/user-attachments/assets/528bbcc0-270e-4ea9-9c00-c883caa99810" />

#### Log Transformation and Regular Differencing and Seasonal Differencing:
<img width="1749" height="331" alt="image" src="https://github.com/user-attachments/assets/32464f32-e3c7-4e30-9fed-f2c6869dbf92" />

<img width="1287" height="710" alt="image" src="https://github.com/user-attachments/assets/cab0c35c-f43f-42e1-a30d-9d3a64b93716" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
