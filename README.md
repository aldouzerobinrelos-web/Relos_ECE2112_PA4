# Relos_ECE2112_PA4

The content of this repository contains Programming Assignment 4 for the course "Advance Computer Programming" S.Y. 2026 - 2027. This project covers 3 python problems connected to Module 4 - Data Wrangling and Data Visualization

# A. VISAYAS COMMUNICATION DATAFRAME

The goal of this problem is to create a DataFrame named `VisComm` containing students whose Hometown is Visayas and whose Track is Communication. Retain only these columns, in the stated order: 

`Name`, `Gender`, `Math`, `Electronics`, `Average`. 

Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to the source dataset before the columns are selected.

---

```python
import pandas as pd      

board2 = pd.read_excel('board2.xlsx')    

board2["Average"] = ((board2["Math"]+board2["Electronics"])/2)
```

`import pandas as pd` imports Pandas and gives it the shorter name `pd`. `board2 = pd.read_excel('board2.xlsx')` reads the Excel file and stores the data in `board2`. `board2["Average"] = ((board2["Math"]+board2["Electronics"])/2)` calculates the average of Math and Electronics and stores it in the `Average` column.

```python
VisComm = pd.DataFrame(board2.loc[
    (board2['Hometown'] == "Visayas") &
    (board2['Track'] == "Communication"),
    ["Name", "Gender", "Math", "Electronics","Average"]
])
```

`VisComm = pd.DataFrame(board2.loc[...])` creates a new DataFrame named `VisComm`. `(board2['Hometown'] == "Visayas")` selects students from Visayas, while `&` means both conditions must be true. `(board2['Track'] == "Communication")` selects students in the Communication track. The list `["Name", "Gender", "Math", "Electronics","Average"]` keeps only the required columns in the stated order.

```python
display(VisComm)
display(VisComm.shape[0])
```

`display(VisComm)` displays the resulting DataFrame. `display(VisComm.shape[0])` displays the number of rows in `VisComm`, which is `5`.

# B. VISAYAS FEMALE DATAFRAME

Create a second DataFrame named `VisFemale` containing students whose Hometown is Visayas and whose Gender is Female. Retain only: 

`Name`, `Track`, `GEAS`, `Electronics`, `Average`. 

Display `VisFemale`. Then display only the rows of `VisFemale` whose `Average` is at least 60. Do not overwrite `VisFemale` when performing this second filter.

---

```python
board2["Average-2"] = ((board2["GEAS"]+board2["Electronics"])/2)
```
`board2["Average-2"] = ((board2["GEAS"]+board2["Electronics"])/2)` calculates the average of GEAS and Electronics and stores it in `Average-2`.

```python

VisFemale = pd.DataFrame(board2.loc[
    (board2['Hometown'] == "Visayas") &
    (board2['Gender'] == "Female"),
    ["Name", "Track", "GEAS", "Electronics","Average"]
])
```

`VisFemale = pd.DataFrame(board2.loc[...])` creates a new DataFrame named `VisFemale`. `(board2['Hometown'] == "Visayas")` selects students from Visayas, while `&` means both conditions must be true. `(board2['Gender'] == "Female")` selects female students. The list `["Name", "Track", "GEAS", "Electronics","Average"]` keeps only the required columns.

```python
display(VisFemale)

display(VisFemale.loc[(VisFemale['Average'] >= 60)])
```

`display(VisFemale)` displays the complete `VisFemale` DataFrame, while `VisFemale.loc[(VisFemale['Average'] >= 60)]` filters the DataFrame to find students whose `Average` is at least 60.


# C. CATEGORY-AVERAGE VISUALIZATION

Examine how the recorded `Average` differs across the three categorical features `Track`, `Gender`, and `Hometown`.

a. For each feature, compute the mean of `Average` for every category using Pandas.

b. Display the three summary tables.

c. Create one figure containing three bar charts: mean `Average` by `Track`, by `Gender`, and by `Hometown`.

d. Below the figure, write three concise statements identifying the category with the highest sample mean for each feature.

---

```python
import matplotlib.pyplot as plt

board2['Average'] = (board2['Math'] + board2['Electronics'] + board2['GEAS'] + board2['Communication']) / 4
```

`import matplotlib.pyplot as plt` imports Matplotlib's `pyplot` and gives it the shorter name `plt`. `board2['Average'] = ...` adds the Math, Electronics, GEAS, and Communication scores together and divides the total by 4 to calculate the average for each student.

```python
track_mean = board2.groupby('Track')['Average'].mean().reset_index()
gender_mean = board2.groupby('Gender')['Average'].mean().reset_index()
hometown_mean = board2.groupby('Hometown')['Average'].mean().reset_index()
```

`track_mean = board2.groupby('Track')['Average'].mean().reset_index()` groups the students by Track and calculates the mean `Average` for each track. 

`gender_mean = board2.groupby('Gender')['Average'].mean().reset_index()` groups the students by Gender and calculates the mean `Average` for each gender. 

`hometown_mean = board2.groupby('Hometown')['Average'].mean().reset_index()` groups the students by Hometown and calculates the mean `Average` for each hometown. 

`reset_index()` changes the grouped results back into normal DataFrames.

```python
display(track_mean)
display(gender_mean)
display(hometown_mean)
```

`display(track_mean)` displays the summary table for Track. `display(gender_mean)` displays the summary table for Gender. `display(hometown_mean)` displays the summary table for Hometown.

```python
plt.figure(figsize=(20, 4))

plt.bar(track_mean['Track'], track_mean['Average'])
plt.bar(gender_mean['Gender'], gender_mean['Average'])
plt.bar(hometown_mean['Hometown'], hometown_mean['Average'])

plt.show()
```

`plt.figure(figsize=(20, 4))` creates a figure that is 20 inches wide and 4 inches tall. `plt.bar(track_mean['Track'], track_mean['Average'])` creates a bar chart using the Track categories and their mean Average. `plt.bar(gender_mean['Gender'], gender_mean['Average'])` creates a bar chart using the Gender categories and their mean Average. `plt.bar(hometown_mean['Hometown'], hometown_mean['Average'])` creates a bar chart using the Hometown categories and their mean Average. `plt.show()` displays the figure.

---

Thank you for reading!

For the main program for Programming Assignment 4 click this link

https://github.com/aldouzerobinrelos-web/Relos_ECE2112_PA4/blob/main/Relos_ECE2112_PA4.ipynb

then download, then open on Google Colab or Jupyter Notebook, and run every cell.

**Readme File History:**

September 14 2026 - started initial readme file

September 15 2026 - started and finished the 1st and 2nd problems

September 16 2026 - started and finished 3rd problem, added link to programming assignment 4

September 17 2026 - changed csv file back to excel file and deleted board2.csv from repository
