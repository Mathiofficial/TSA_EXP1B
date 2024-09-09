# Ex.No: 1 B                    CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 23/08/2024
# Name : Mathiyazhagan A
## AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data

## ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
   
## PROGRAM:
### Importing the necessary Packages:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller, kpss
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
```

### Loading the dataset:
```
data = pd.read_csv('/content/seattle_weather_1948-2017.csv', parse_dates=['DATE'], index_col='DATE')
```

### Plot the data without Conversion:
```
def test_stationarity(series):
result = adfuller(series.dropna())
print('ADF Statistic:', result[0])
print('p-value:', result[1])
print('Critical Values:', result[4])
print('')
test_stationarity(data['PRCP'])
plt.figure(figsize=(10, 6))
plt.plot(data['PRCP'], label='PRCP')
plt.title('Precipitation Over Time')
plt.xlabel('Date')
plt.ylabel('Precipitation')
plt.legend()
plt.show()

```

### REGULAR DIFFERENCING
```
data3=data
data3['diff']=data3['International airline passengers: monthly totals in thousands. Jan 49 ? Dec 60'].diff(periods=1)
data3=data3.dropna()
x=data3['Month']
y=data3['diff']
plt.xlabel('Month')
plt.ylabel('International airline passengers: monthly totals in thousands.')
plt.plot(x,y)
```

### SEASONAL ADJUSTMENT
```
data1=data
data1['SeasonalAdjustment'] = data1['International airline passengers: monthly totals in thousands. Jan 49 ? Dec 60'] - data1['International airline passengers: monthly totals in thousands. Jan 49 ? Dec 60'].shift(12)
data1['SeasonalAdjustment'].dropna()
x=data1['Month']
y=data1["SeasonalAdjustment"]
plt.xlabel('Month')
plt.ylabel('International airline passengers: monthly totals in thousands.')
plt.plot(x,y)
```

### LOG TRANSFORMATION
```
data2=data
data2['log']=np.log(data2['diff']).dropna()
data2=data2.dropna()
x=data2['Month']
y=data2['log']
plt.xlabel('Month')
plt.ylabel('International airline passengers: monthly totals in thousands.')
# plt.figure(figsize=(8, 6)) 
plt.plot(x,y)
```

## OUTPUT:
### WITHOUT CONVERSION:

![311306232-c6110233-a143-44fc-8055-73256231bdb1](https://github.com/user-attachments/assets/cb057271-a9d2-4089-ad0d-69417fd42f5c)


### REGULAR DIFFERENCING:

![311306425-f13bc5b1-f547-4a2e-b52e-53bee0ba4166](https://github.com/user-attachments/assets/57987a20-78bb-4741-9e3e-2fa8b73ca0bc)


### SEASONAL ADJUSTMENT:

![311306589-9e15eef9-4278-486b-9fa6-766b373ecc73](https://github.com/user-attachments/assets/89773311-261e-4ce4-a889-e514fac33361)


### LOG TRANSFORMATION:
![311306698-75a84c2a-e8d5-4e98-b88e-26e6da9d5d9d](https://github.com/user-attachments/assets/64c7b67e-ba0c-4d76-a237-64defc0ee98f)



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
