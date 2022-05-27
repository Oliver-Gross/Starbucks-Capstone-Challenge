# Starbucks-Capstone-Challenge
## Project for Udacity Data Scientist Nanodegree
![](https://upload.wikimedia.org/wikipedia/commons/3/3b/Udacity_logo.png)

## Installations
```
import pandas as pd
import numpy as np
import math
import json
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
%matplotlib inline

from sklearn.tree import DecisionTreeClassifier
from sklearn.neighbors import KNeighborsClassifier
from sklearn.ensemble import RandomForestClassifier, AdaBoostClassifier
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import accuracy_score
from sklearn.metrics import precision_score
from sklearn.metrics import recall_score
from sklearn.metrics import f1_score
from sklearn.metrics import confusion_matrix
```
[Panda](https://en.wikipedia.org/wiki/Pandas_(software)) is a Python package providing fast, flexible, and expressive data structures designed to make working with “relational” or “labeled” data both easy and intuitive. <br>
[Matplotlib](https://en.wikipedia.org/wiki/Matplotlib) is a plotting library used to visualize our results. <br>
[JSON](https://docs.python.org/3/library/json.html) exposes an API familiar to users of the standard library marshal and pickle modules.
[SKlearn](https://scikit-learn.org/stable/) is used for predictive data analysis. <br>
## Motivation
As a first project for my Data Science Nanodegree at [Udacity](https://www.udacity.com/school-of-data-science) I am asked to choose a data set and analyze, model and visualize it. For my project I chose a [Heart Failure Prediction Dataset](https://www.kaggle.com/fedesoriano/heart-failure-prediction). <br>
It contains mostly medical data which can be used for a early detection of a heart disease.

## Description
The used model can give you a predicition for a member/ customer whether the person will complete an offer or not.
After defining a member the model can give a list of predefined offers the member will most likely complete.

## Authors, Acknowledgements

Author: Oliver Groß

Credits to the Udacity-Team for the ID-Encoder and other code from their teachings.
