# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date:
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load dataset
data = pd.read_csv('/content/bike_sales_india.csv')

# Select required columns
resampled_data = data[['Year','Resale Price (INR)']]

# Average resale price per year
resampled_data = resampled_data.groupby('Year')['Resale Price (INR)'].mean().reset_index()

Years = resampled_data['Year'].tolist()
Price = resampled_data['Resale Price (INR)'].tolist()

# Linear Trend
X = [i - Years[len(Years)//2] for i in Years]
x2 = [i**2 for i in X]
xy = [i*j for i,j in zip(X,Price)]

n = len(Years)

b = (n*sum(xy) - sum(Price)*sum(X)) / (n*sum(x2) - (sum(X)**2))
a = (sum(Price) - b*sum(X)) / n

linear_trend = [a + b*X[i] for i in range(n)]

# Polynomial Trend
x3 = [i**3 for i in X]
x4 = [i**4 for i in X]
x2y = [i*j for i,j in zip(x2,Price)]

coeff = [[len(X), sum(X), sum(x2)],
         [sum(X), sum(x2), sum(x3)],
         [sum(x2), sum(x3), sum(x4)]]

Y = [sum(Price), sum(xy), sum(x2y)]

A = np.array(coeff)
B = np.array(Y)

solution = np.linalg.solve(A,B)
a_poly, b_poly, c_poly = solution

poly_trend = [a_poly + b_poly*X[i] + c_poly*(X[i]**2) for i in range(n)]

# --------- A : LINEAR TREND ESTIMATION ---------
print("A - LINEAR TREND ESTIMATION")

plt.figure()

plt.plot(Years, Price, color='blue', marker='o')
plt.plot(Years, linear_trend, color='black', linestyle='--')

plt.xlabel('Year')
plt.ylabel('Resale Price (INR)')
plt.show()


# --------- B : POLYNOMIAL TREND ESTIMATION ---------
print("B - POLYNOMIAL TREND ESTIMATION")

plt.figure()

plt.plot(Years, Price, color='blue', marker='o')
plt.plot(Years, poly_trend, color='black', marker='o')

plt.xlabel('Year')
plt.ylabel('Resale Price (INR)')
plt.show()
```
### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="939" height="513" alt="Screenshot 2026-03-14 102156" src="https://github.com/user-attachments/assets/5698606b-ef33-4e15-a032-78fbec9f6e84" />

B- POLYNOMIAL TREND ESTIMATION
<img width="914" height="513" alt="Screenshot 2026-03-14 102329" src="https://github.com/user-attachments/assets/aee3046f-5b31-4462-a6f5-1f0c32aba997" />

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
