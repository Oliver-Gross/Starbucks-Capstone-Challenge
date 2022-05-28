# Starbucks-Capstone-Challenge
## Project for Udacity Data Scientist Nanodegree
![](https://upload.wikimedia.org/wikipedia/commons/3/3b/Udacity_logo.png)

### Table of Contents

1. [Installation](#installation)
2. [Project Motivation](#motivation)
3. [Description](#description)
4. [Results](#results)
5. [Authors and Acknowledgements](#licensing)

## Installations <a name="installation"></a>
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
[JSON](https://docs.python.org/3/library/json.html) exposes an API familiar to users of the standard library marshal and pickle modules.<br>
[scikit-learn](https://scikit-learn.org/stable/) is used for predictive data analysis. <br>

## Project Motivation <a name="motivation"></a>
For this project the challenge has been to analyze a dataset provided by Starbucks. It can
be analyzed any way you see fit. For example, you could build a machine learning model that predicts how much someone will spend based on demographics and offer type. Or you could build a model that predicts whether or not someone will respond to an offer.
I chose the later one and want to predict which user will respond/complete which offer.

## Description <a name="description"></a>
The used model can give you a predicition for a member/ customer whether the person will complete an offer or not.
After defining a member the model can give a list of predefined offers the member will most likely complete.

## Authors, Acknowledgements

Author: Oliver Groß <a name="licensing"></a>

Credits to the Udacity-Team for the ID-Encoder and other code from their teachings.
And Credits to Starbucks for providing the data.
