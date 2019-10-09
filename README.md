# Pymaceuticals Inc
This project is part of the Data Analytics and Visualization Certification at Washington University in St. Louis.  Other projects can be found at the [main GitHub repo](https://github.com/jfandata).

#### -- Project Status: [Completed]

## Project Intro/Objective
The purpose of this project is to analyize and compare a cancer drug study done on 250 mice over the course of 45 days. Visualizations show the changes over time for each treatment. 

### Methods Used
* visual data analysis
* statistical analysis
* linear analysis

### Technologies
* Python
* Jupyter Notebook
* Matplotlib
* NumPy
* Pandas 

## Project Description
This project analyzed the treatment data to compare the level of treatment response among three drug treatments and a placebo. Graphs were created to visualize the data results. Visual analysis allows easy reading of trending data such as the effect of drug treatments on metastatic spread, survival rate of mice during treatment and tumor changes at the end of treatment. 

### Observations:

1. The placebo and drugs Infabinol and Ketapril resulted in increasing tumor growth over time. Only drug Capomulin shows effectively decreasing the volume (size) of the tumor.

![alt text](https://github.com/jfandata/MATPLOTLIB_Pymaceuticals/blob/master/Results/tumor_response.jpg "Tumor Response to Treatment")

2. After 45 days, the metastatic spread taking Ketapril did not prove to be any more effective than the Placebo. 

![alt text](https://github.com/jfandata/MATPLOTLIB_Pymaceuticals/blob/master/Results/metastatic.jpg "Metastatic Spread During Treatment")

3. The survival rate of drug Capomulin was much higher than the other two drugs and the placebo. After 45 days, the other two drugs Infubinol and Ketapril had similiar survival rates as the placebo.

![alt text](https://github.com/jfandata/MATPLOTLIB_Pymaceuticals/blob/master/Results/mouse_count.jpg "Survival During Treatment")

4. Drugs Infubinol and Ketapril and the placebo shows the volume of tumor increased at least 46%. Capomulin shows a decrease of tumor volume by 19% over a 45 day treatment.

![alt text](https://github.com/jfandata/MATPLOTLIB_Pymaceuticals/blob/master/Results/tumor_change.jpg "Tumor Change Over 45 Day Treatment")

## Needs of this Project

- data exploration/descriptive statistics
- data processing/cleaning
- statistical modeling

## Contents of Project Repository

1. Raw Data is being kept [here](https://github.com/jfandata/MATPLOTLIB_Pymaceuticals/tree/master/data) within this repo.

2. Data processing/transformation scripts and results are kept [here](https://github.com/jfandata/MATPLOTLIB_Pymaceuticals/blob/master/pymaceuticals_starter.ipynb)

## Key Takeaways

1. Dependencies and setup.
```python
%matplotlib inline
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import os
import csv
```

2. Minor data munging to re-format the data frames.
```python
means=mean_df.unstack(0)
means_df=means["Tumor Volume (mm3)"] #goes down a level
```

3. Generate the plot (with Error Bars) and save the figure.
```python
error = stderr["Tumor Volume (mm3)"]["Capomulin"]
c=plt.errorbar(x_axis, means_df["Capomulin"], yerr=error, fmt="o", ls="dotted", color="blue")

error = stderr["Tumor Volume (mm3)"]["Infubinol"]
i=plt.errorbar(x_axis, means_df["Infubinol"], yerr=error, fmt="^", ls="dotted", color="red")

error = stderr["Tumor Volume (mm3)"]["Ketapril"]
k=plt.errorbar(x_axis, means_df["Ketapril"], yerr=error, fmt="s", ls="dotted", color="black")

error = stderr["Tumor Volume (mm3)"]["Placebo"]
p=plt.errorbar(x_axis, means_df["Placebo"], yerr=error, fmt="d", ls="dotted", color="green")

plt.title("Tumor Response to Treatment")
plt.xlabel("Time (Days)")
plt.ylabel("Tumor Volume (mm3)")
plt.grid(linestyle="-")
plt.legend((c,i,k,p),("Capomulin", "Infubinol", "Ketapril", "Placebo"))
plt.show()

# Save the Figure
plt.savefig("tumor_response.jpg")
```