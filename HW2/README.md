## Problem Design

### My Problem
Predicting if a person has a heart disease.
Two classes:
* Disease - person has a heart disease
* Healthy - person does not have a heart disease

### My Attributes:
1. Age
2. Sex
3. Weight
4. Activity level (exercise)
5. Smoking
6. Family heart disease history

### My Rules:
Disease:

1. If age > 60 AND Male
2. If 50 < age < 60
	*If Family heart disease history
	* If Smoking
	* If Weight > 100
	* If Activity level = 0
3. If 40 < age < 50
	* If Activity level = 0 AND Weight > 100
	* If Smoking AND Activity level = 0
	* If Smoking AND Weight > 100
4. If Family heart disease history AND Male

Healthy:

1. All other possibilities




## Comparison of two trees

My markup tree that I created by hand using the rules I created:
![](https://github.com/nikitagalayda/FDA-Homework/blob/master/HW2/h_tree.png)

The tree that I generated with code using scilearn DecisionTreeClassifier and graphviz:

![](https://github.com/nikitagalayda/FDA-Homework/blob/master/HW2/h_tree_scilearn.png)