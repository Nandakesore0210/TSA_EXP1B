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
data=pd.read_csv('/content/Crypto Data Since 2015.csv')
data['Date']=pd.to_datetime(data['Date'])
data.set_index('Date',inplace=True)

data['Bitcoin (USD)_diff']=data['Bitcoin (USD)']-data['Bitcoin (USD)'].shift(1)

result = seasonal_decompose(data['Bitcoin (USD)'], model='additive', period=12)
data['Bitcoin (USD)_sea_diff']=result.resid

data['Bitcoin (USD)_log'] = np.log(data['Bitcoin (USD)'])
data['Bitcoin (USD)_log_diff']=data['Bitcoin (USD)_log']-data['Bitcoin (USD)_log'].shift(1)
result = seasonal_decompose(data['Bitcoin (USD)_log_diff'].dropna(), model='additive', period=30)
plt.figure(figsize=(16, 16))
plt.subplot(6, 1, 1)
plt.plot(data['Bitcoin (USD)'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('No of Bitcoin (USD)')
plt.subplot(6, 1, 2)
plt.plot(data['Bitcoin (USD)_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced No of Bitcoin (USD)')
plt.subplot(6, 1, 3)
plt.plot(data['Bitcoin (USD)_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally djusted No of Bitcoin (USD)')
plt.subplot(6, 1, 4)
plt.plot(data['Bitcoin (USD)_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(No of Bitcoin (USD))')
plt.subplot(6, 1, 5)
plt.plot(data['Bitcoin (USD)_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff(Log(No of Bitcoin (USD)))')
plt.subplot(6, 1, 6)
from statsmodels.tsa.seasonal import seasonal_decompose

result = seasonal_decompose(
    data['Bitcoin (USD)_log_diff'].dropna(), 
    model='additive', 
    period=30 
)

data['Bitcoin (USD)_log_seasonal_diff'] = result.resid

plt.plot(data['Bitcoin (USD)_log_seasonal_diff'], label='Log Transformation and regular Diff')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(No of Bitcoin (USD))))')
plt.tight_layout()
plt.show()

data.plot(kind='line')
```


### OUTPUT:

#### Original Data:
<img width="1352" height="294" alt="image" src="https://github.com/user-attachments/assets/78a89be5-6833-40f1-bf0d-69a6323cce90" />

#### REGULAR DIFFERENCING:
<img width="829" height="221" alt="image" src="https://github.com/user-attachments/assets/bfad33df-9bf1-4f7d-9764-333702658fc3" />

#### SEASONAL ADJUSTMENT:
<img width="832" height="221" alt="image" src="https://github.com/user-attachments/assets/0843e188-6cdc-4ec2-b2dd-840890ae15cb" />

#### LOG TRANSFORMATION:
<img width="824" height="223" alt="image" src="https://github.com/user-attachments/assets/25627cde-da6d-4500-b968-10287fa77a82" />

#### Log Transformation and Regular Differencing and Seasonal Differencing:
<img width="847" height="614" alt="image" src="https://github.com/user-attachments/assets/58ef8940-9628-4c47-a267-2ece0bdd54c9" />

<img width="721" height="533" alt="image" src="https://github.com/user-attachments/assets/3c20a3ad-8d3a-4104-9137-fe7f4bd2635b" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
