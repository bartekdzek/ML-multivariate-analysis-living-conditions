# Analysis of Living Conditions: Unsupervised Machine Learning Approach

A project applying Unsupervised Machine Learning algorithms and Multivariate Comparative Analysis (MCA) to classify and rank counties in Southeastern Poland based on socio-economic data from 2023. This project was completed as part of the course *Statistical Data Analysis*.

## Project Overview

This project focuses on the application of Data Science techniques to regional statistics. The primary objective was to uncover hidden patterns in demographic and economic data using clustering algorithms and linear ordering methods.

By treating the administrative units as data points in a multidimensional space, the study identifies clusters of counties with similar characteristics and constructs a synthetic ranking of living standards.

**Key Domains:**
* Unsupervised Machine Learning (Clustering)
* Multivariate Statistics
* Socio-Economic Geography

**Authors:**
* Sebastian Szklarski
* Bartosz Tasak

## Project Objectives

1.  **Algorithm Implementation:** Application of Machine Learning algorithms (K-Means, Hierarchical Clustering) to segment the dataset.
2.  **Data Engineering:** Building a robust dataset from the Local Data Bank (BDL) and performing feature selection.
3.  **Linear Ordering:** Creating a synthetic index to rank counties from "best" to "worst" living conditions.
4.  **Evaluation:** Validating cluster quality using metrics like Silhouette Score and the Elbow Method.
5.  **Insight Generation:** Interpreting the results to identify regions of prosperity and stagnation.

## Data Source

The dataset was constructed using the **Local Data Bank (Bank Danych Lokalnych - BDL)** data from Statistics Poland (GUS).
* **Timeframe:** 2023
* **Scope:** Małopolskie, Podkarpackie, and Świętokrzyskie voivodeships.

## Diagnostic Variables & Feature Selection

The initial dataset consisted of 19 potential features. A feature selection process was applied.
### Full List of Analyzed Features:

| Symbol | Variable Name | Type | Unit |
| :---: | :--- | :---: | :---: |
| **X1** | Registered unemployment rate | Destimulant | % |
| **X2** | Newly registered entities (REGON) | Stimulant | per 10k pop. |
| **X3** | Share of long-term unemployed (>12 months) | Destimulant | % |
| **X4** | Average monthly gross salary | Stimulant | PLN |
| **X5** | Net migration rate (total) | Stimulant | per 1000 pop. |
| **X6** | Old-age dependency ratio | Destimulant | % |
| **X7** | Population using sewage system | Stimulant | % |
| **X8** | Useful floor area per person | Stimulant | m² |
| **X9** | Population per pharmacy | Destimulant | persons |
| **X10** | Doctors per 10k inhabitants | Stimulant | persons |
| **X11** | Crimes ascertained by Police | Destimulant | per 1000 pop. |
| **X12** | Passenger cars per 1000 inhabitants | Stimulant | pcs. |
| **X13** | Hard-surface road density | Stimulant | km/100km² |
| **X14** | Road accidents per 100k inhabitants | Destimulant | pcs. |
| **X15** | Gas pollution emission | Destimulant | t/km² |
| **X16** | Parks and green areas share | Stimulant | % |
| **X17** | Legally protected areas share | Stimulant | % |
| **X18** | Gross enrollment rate | Stimulant | % |
| **X19** | Pupils per school section | Destimulant | persons |

*Note: Destimulants (where lower values are better) were transformed into Stimulants during the preprocessing stage to ensure mathematical consistency.*

## Methodology: Machine Learning & Statistics

The project was implemented in Python using the following pipeline:

### 1. Preprocessing & Normalization
* **Standarization:** Scaling features to ensure that variables with large magnitudes (like salaries) do not dominate the distance metrics.
* **Correlation Analysis:** Removing redundant features to improve model performance.

### 2. Linear Ordering (Ranking Models)
Two statistical models were built to score the counties:
* **Pattern Method (Hellwig):** Measures the Euclidean distance of each data point from a theoretical "ideal" point (pattern).
* **Non-Pattern Method:** Aggregates normalized values to produce a composite score.

### 3. Unsupervised Learning (Clustering)
To segment the counties into distinct groups, two clustering techniques were deployed:

* **Hierarchical Clustering (Ward's Method):**
    * Used to visualize the data structure via a **Dendrogram**.
    * Helps in understanding the nested relationships between counties.

* **K-Means Clustering:**
    * An iterative algorithm used to partition the dataset into *k* non-overlapping subgroups.
    * **Hyperparameter Tuning:** The optimal number of clusters (*k=4*) was determined using the **Elbow Method** and **Silhouette Analysis**.

## Results and Findings

The Machine Learning models identified 4 distinct classes of counties:

1.  **Class 1 (High Development):** Major urban centers (e.g., Kraków) and industrial hubs. Characterized by high salaries, positive migration, and strong infrastructure.
2.  **Class 2, 3, 4 (Transitional & Peripheral):** A gradient of development showing a clear spatial pattern. The eastern parts of the analyzed region (Peripheral clusters) exhibit structural challenges, such as lower healthcare accessibility (X9) and negative migration trends.

**Spatial Autocorrelation:** The results confirm strong spatial dependencies—economic well-being is geographically clustered, supporting the theory of regional convergence/divergence.

## Project structure

```text
project/
│
├── A02_Granice_powiatow.shp      # Main shapefile containing county boundaries (Geometry)
├── A02_Granice_powiatow.shx      # Shape index file (required for GIS operations)
├── A02_Granice_powiatow.dbf      # Attribute table for the shapefile (Database)
├── A02_Granice_powiatow.prj      # Projection file (Coordinate Reference System info)
│
├── sprawozdanie.html             # Static project report (exported for easy viewing)
├── sprawozdanie.ipynb            # Main Jupyter Notebook with source code & analysis
│
└── README.md                     # Project documentation

```
## Tech Stack

* **Python 3.13**
* **Jupyter notebook**
* **Machine Learning:** `scikit-learn` (KMeans, Preprocessing, Metrics)
* **Scientific Computing:** `pandas`, `numpy`, `scipy`
* **Visualization:** `matplotlib`, `seaborn`

## All libraries 
```
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
import matplotlib.colors as mcolors
from sklearn.preprocessing import StandardScaler
from IPython.display import display, HTML
import geopandas as gpd
import matplotlib.patches as mpatches
from scipy.stats import kendalltau, spearmanr
from sklearn.cluster import KMeans
from scipy.cluster.hierarchy import linkage, dendrogram, fcluster
from sklearn.metrics import calinski_harabasz_score
```
