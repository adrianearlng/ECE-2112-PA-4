# ECE-2112-PA-4
**Made by: Adrian Earl A. Ng | 2ECE-C** \
\
This repository contains Programming Assignment 4 for the course "ADVANCED COMPUTER PROGRAMMING AND ALGORITHMS" with code ECE2112 during S.Y.2026-2027.
Programming Assignment 4 has 3 python problems related to Module 4: Data Wrangling and Visualization.


Initializations of libraries to be used
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```
# A. VISAYAS COMMUNICATION DATAFRAME
Create a DataFrame named `VisComm` containing students whose Hometown is Visayas and whose Track is Communication. Retain only these columns, in the stated order: `Name`, `Gender`, `Math`, `Electronics`, `Average` 

Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to the source dataset before the columns are selected
```python
board2 = pd.read_excel('board2.xlsx')
board2['Average'] = board2[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis = 1)
VisComm = board2.loc[(board2['Hometown']=='Visayas') & (board2['Track']=='Communication'), ['Name', 'Gender', 'Math', 'Electronics', 'Average']]
print ("Number of rows in DataFrame VisComm: ", VisComm.shape[0])
VisComm
```

# B. VISAYAS FEMALE DATAFRAME
Create a second DataFrame named `VisFemale` containing students whose `Hometown` is *Visayas* and whose `Gender` is *Female*. Retain only: `Name`, `Track`, `GEAS`, `Electronics`, `Average`

Display `VisFemale`. Then display only the rows of `VisFemale` whose `Average` is at least **60**. Do not overwrite `VisFemale` when performing this second filter.
```python
VisFemale = board2.loc[(board2['Hometown']=='Visayas') & (board2['Gender']=='Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
VisFemale

VisFemale.loc[(VisFemale['Average']>=60)]
```

# C. CATEGORY-AVERAGE VISUALIZATION
Examine how the recorded `Average` differs across the three categorical features `Track`, `Gender`, and `Hometown`.  
a. For each feature, compute the mean of `Average` for every category using **Pandas**.  
b. Display the three summary tables.  
c. Create one figure containing three bar charts: **mean Average by Track**, **by Gender**, and **by Hometown**.  
d. Below the figure, write three concise statements identifying the category with the highest sample mean for each feature.

**Interpretation rule:** Describe the observed dataset only. A difference in group means does not, by itself, establish that a feature causes a higher board-exam score.
```python
AveTr = board2.groupby('Track')['Average'].mean()
AveGe = board2.groupby('Gender')['Average'].mean()
AveHt = board2.groupby('Hometown')['Average'].mean()

ds = plt.figure(figsize=[20,6])
bar1, bar2, bar3 = ds.add_subplot(1, 3, 1), ds.add_subplot(1, 3, 2), ds.add_subplot(1, 3, 3)

bar1.bar(AveTr.index, AveTr.values, color='darkgreen')
bar1.set(title='Average Mean by Track', xlabel='Track', ylabel='Average')

bar2.bar(AveGe.index, AveGe.values, color='navy')
bar2.set(title='Average Mean by Gender', xlabel='Gender', ylabel='Average')

bar3.bar(AveHt.index, AveHt.values)
bar3.set(title='Average Mean by Hometown', xlabel='Hometown', ylabel='Average')

ds.text(0.1, -0.1, 'Sorting by track, Communication has the highest average mean.\nBy gender, males have a higher average mean.\nBy hometown, Luzon has a higher average mean.', style='oblique')
```

**README File Version History:**  
September 17, 2026 - Initial README output
