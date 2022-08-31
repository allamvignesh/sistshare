import csv
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split

data = [["Region", "Age", "Income", "Online Shoppping"],
		["India", 49, 86400, "No"],
		["Brazil", 32, 57600, "Yes"],
		["USA", 35, 64800, "No"],
		["Brazil", 43, 73200, "No"],
		["USA", 45, 0, "Yes"],
		["India", 40, 69600, "Yes"],
		["Brazil", 0, 62400, "No"],
		["India", 53, 94800, "Yes"],
		["USA", 55, 99600, "No"],
		["India", 42, 80000, "Yes"]]

f = open("sample.csv", "w")
writer = csv.writer(f)
writer.writerows(data)
f.close()

data = pd.read_csv("sample.csv")
array = np.array(data)

def fillEmpty(arr, col):
	for i,j in enumerate(array):
		if j[col] == 0:
			array[i][col] = "NAN"

def NANToMean(arr, col):
	tot, count = 0, 0
	for i in array[:, col]:
		if i != "NAN":
			tot += i
	mean = tot//(len(array[:,col])-list(array[:,col]).count("NAN"))

	for i, j in enumerate(array):
		if j[col] == "NAN":
			array[i][col] = mean

print(array)
fillEmpty(array, 1)
NANToMean(array, 1)

fillEmpty(array, 2)
NANToMean(array, 2)

x = array[:,:-1]
y = array[:,-1]

x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.05, random_state=0)
