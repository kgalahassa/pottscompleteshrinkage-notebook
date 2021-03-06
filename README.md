# pottscompleteshrinkage-notebook
A notebook to describe the Potts Complete Shrinkage Package


```python
### first install the package using pip: '''pip install pottscompleteshrinkage'''
```


```python


import pandas as pd
import random
import numpy as np
from numpy import linalg as LA
from sklearn import datasets

# import some data to play with
iris = datasets.load_iris()
Train_PottsData_demo = iris.data[:, :3]

```


```python
#Import the Potts Complete Shrinkage module
import pottsshrinkage.completeshrinkage as PCS
```


```python
#Choose the number of colors
q = 20
```


```python
#Compute Initial Potts Clusters as a first Random Partition (with Potts Model)
InitialPottsClusters = PCS.InitialPottsConfiguration(Train_PottsData_demo, q, Kernel="Mercer")
```


```python

#Choose your temperature (T) level
T = 1000

#Set the bandwidth of the model
sigma = 1

#Set the Number of Random_Partitions you want to simulate
Number_of_Random_Partitions = 3

#Set your initial (random) Potts partition as computed above
Initial_Partition = InitialPottsClusters

#Set the Minimum Size desired for each partition generated
MinClusterSize = 5

#Run your Potts Complete Shrinkage Model to simulate the Randomly Shrunk Potts Partitions. Partitions_Sets is a dictionary that can be saved 
#with pickle package.
Partitions_Sets,Spin_Configuration_Sets = PCS.Potts_Random_Partition (Train_PottsData_demo, T, sigma, Number_of_Random_Partitions, MinClusterSize, Initial_Partition,  Kernel="Mercer")
```

    We are at step: 1
    Clusters Size of Current Partition [11, 10, 13, 7, 6, 7, 8, 11, 10, 6, 8, 6, 8, 6, 10, 7, 10, 6]
    Partition is: [[34, 9, 12, 1, 29, 3, 42, 13, 38, 8, 41], [39, 7, 23, 37, 4, 35, 47, 2, 6, 22], [40, 17, 0, 28, 27, 36, 31, 20, 46, 21, 19, 32, 16], [48, 10, 5, 18, 33, 14, 15], [49, 30, 25, 43, 11, 24], [89, 53, 80, 59, 64, 26, 104], [95, 61, 82, 71, 88, 79, 44, 116], [97, 75, 58, 54, 74, 65, 127, 91, 56, 51, 85], [106, 98, 93, 57, 60, 99, 67, 81, 45, 144], [113, 94, 69, 90, 92, 62], [135, 130, 107, 122, 105, 118, 131, 117], [138, 70, 96, 66, 55, 84], [140, 112, 132, 108, 137, 128, 103, 134], [141, 77, 76, 86, 52, 50], [142, 101, 83, 114, 123, 119, 146, 72, 87, 68], [143, 124, 120, 129, 102, 125, 109], [147, 115, 110, 139, 145, 133, 111, 148, 136, 100], [149, 121, 126, 73, 63, 78]]
    We are at step: 2
    Clusters Size of Current Partition [7, 10, 9, 6, 7, 8, 10, 7, 11, 7, 9, 8, 8, 7, 11, 10, 8, 7]
    Partition is: [[39, 7, 23, 36, 28, 27, 20], [40, 17, 0, 35, 37, 4, 42, 6, 2, 22], [45, 12, 1, 29, 3, 38, 8, 13, 41], [46, 21, 19, 32, 16, 44], [48, 10, 5, 18, 33, 14, 15], [49, 30, 9, 25, 43, 26, 11, 24], [89, 53, 69, 80, 59, 81, 60, 79, 34, 76], [95, 61, 94, 88, 93, 47, 58], [99, 67, 82, 71, 92, 62, 98, 57, 64, 31, 86], [121, 96, 66, 55, 90, 84, 106], [126, 73, 63, 78, 97, 75, 54, 74, 65], [135, 130, 107, 122, 105, 118, 131, 117], [137, 116, 128, 103, 133, 111, 134, 149], [138, 70, 127, 91, 56, 51, 85], [142, 101, 83, 114, 113, 123, 119, 146, 72, 87, 68], [144, 124, 120, 139, 129, 102, 140, 112, 132, 108], [147, 115, 110, 145, 77, 141, 52, 50], [148, 136, 104, 100, 143, 125, 109]]
    We are at step: 3
    Clusters Size of Current Partition [10, 11, 8, 6, 12, 6, 8, 10, 7, 9, 6, 8, 7, 7, 11, 9, 6, 9]
    Partition is: [[43, 26, 11, 24, 40, 17, 0, 37, 4, 44], [45, 12, 1, 30, 29, 3, 42, 13, 38, 8, 41], [46, 21, 19, 32, 36, 31, 20, 18], [48, 10, 16, 33, 14, 15], [49, 28, 35, 39, 23, 34, 9, 25, 47, 2, 6, 22], [86, 65, 75, 58, 54, 74], [93, 57, 60, 80, 59, 79, 7, 52], [94, 89, 53, 69, 92, 62, 98, 81, 27, 50], [95, 61, 88, 82, 64, 5, 148], [99, 67, 96, 66, 55, 90, 84, 121, 106], [126, 73, 63, 78, 97, 71], [135, 130, 107, 122, 105, 118, 131, 117], [138, 70, 127, 91, 56, 51, 85], [140, 112, 132, 108, 139, 129, 102], [142, 101, 83, 114, 113, 123, 119, 146, 72, 87, 68], [144, 124, 120, 136, 104, 100, 143, 125, 109], [145, 115, 110, 141, 77, 76], [147, 111, 137, 128, 103, 116, 149, 133, 134]]
    We are at step: 4
    Clusters Size of Current Partition [10, 8, 11, 6, 6, 6, 11, 6, 6, 10, 7, 12, 8, 11, 9, 8, 15]
    Partition is: [[39, 7, 23, 34, 9, 25, 43, 26, 11, 24], [40, 17, 0, 35, 36, 31, 28, 27], [45, 12, 1, 30, 29, 3, 42, 13, 38, 8, 41], [46, 21, 19, 32, 16, 44], [47, 2, 6, 22, 37, 4], [48, 10, 5, 33, 14, 15], [89, 53, 69, 80, 59, 81, 60, 57, 93, 49, 133], [95, 61, 88, 71, 20, 125], [97, 75, 58, 54, 74, 65], [99, 67, 82, 79, 64, 92, 62, 98, 18, 96], [121, 94, 90, 84, 66, 55, 106], [123, 72, 83, 146, 119, 87, 68, 149, 114, 142, 101, 113], [135, 107, 118, 131, 122, 105, 117, 130], [138, 70, 126, 73, 63, 78, 127, 91, 56, 51, 85], [141, 77, 76, 86, 52, 50, 145, 115, 110], [144, 124, 120, 139, 129, 102, 143, 109], [147, 111, 137, 116, 128, 103, 134, 140, 112, 132, 108, 148, 136, 104, 100]]
    


```python

```
