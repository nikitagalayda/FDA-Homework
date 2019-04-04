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

### Visual comparison of trees
My markup tree that I created by hand using the rules I created:

![](https://github.com/nikitagalayda/FDA-Homework/blob/master/HW2/h_tree.png)

The tree that I generated with code using scilearn DecisionTreeClassifier and graphviz:

![](https://github.com/nikitagalayda/FDA-Homework/blob/master/HW2/h_tree_scilearn.png)

### Comparing the rules
Priority represents the level of the attribute on the tree.

#### Hand-generated tree priorities
Age > Age > Sex > Weight/Activity level/Smoking/Family history

#### Code-generated tree priorities
Sex > Age/Family history > Age > Weight/Age > Smoking/Age

#### Attribute Similarity Discussion
To generate hte 'right' data, I correlated my attribute values to the chances of being affected by a heart disease:

##### Sex
I made sure that being a male represented a big factor in being affected by a heart disease. This is proven to be effective, since the code-generated tree prioritized being a male as an attribute. This attribute is similar in both of my hand-generated and code-generated trees. Although, the code-generated tree took sex as a higher priority attribute than my hand-generated tree. 

*Verdict:* Similar

##### Age
Similarly to my logic, code-generated tree also prioritized the age of a person. I specifically divided people into 4 age groups:
1. Below 40
2. Between 40 and 50
3. Between 50 and 60
4. Above 60
These age groups would have different chance of being affected by a heart disease. The older the person is, the more likely they are to be affected by a heart disease. This attribute is treated very similarly in both my rules, and the code-generated tree rules, yet my hand-generated tree prioritizes it more.
I designed my rules to specifically make sure that people of age below 40 were always healthy. The code-generated tree also did the same thing, and one of it's rules is that persons of age below 41 are always healthy.

*Verdict:* Similar

##### Weight/Smoking/Activity level
In my rules, I took weight, activity level, and smoking as a secondary statistics to deciding whether or not a person has a heart disease. IF the person has high weight and/or smokes and/or low activity level, they are more likely to have a heart disease. In the code-generated tree rules, they also plays a less important role, since they appear below the 3rd level of the tree. The two rule sets are almost identical in that regard. This shows my success in designing these rules as a secondary deciding factor, and the DecisionTreeClassifier on identifying these factors as such.

*Verdict:* Almost identical

##### Family heart disease history
Similar to real life, I wanted family heart disease history to greatly affect the chance of a person to be afflicted with a heart disease. To do so, I created a large category - "Has Family heart disease history and Male", which classified a lot of males as afflicted with a heart disease. The code-generated tree also prioritized the Family heart disease history as an important attribute, and created a rule which is more prioritizing than mine. Code-generated tree put the Family heart disease history on level 2, while in my hand-generated tree only has Family heart disease history on level 4. 

*Vecdict:* Different

#### Final Discussion
I belive that my hand-generated tree, which follows the rules I created for generating the 'right' data, is very similar to that which I created with code by using scilearn's DataTreeClassifier. I tried to put emphasis on the attibutes such as sex, age, and family heart disease history, and it was reflected in the code-generated tree, by being on top levels of the tree, and having large impact on the result. The secondary attributes - smoking/weight/activity level, were used for creating rules for more specific classification. By creating these statistics, I hoped to reduce underfitting, and I believe I largely succeeded. The code-generated tree also put the same amount of priority to these secondary statistics as I did, since they appear at 4th+ level of the tree. 

To confirm that the code-generated decision tree created similar rules to that which I created when making the 'right' data, we can look at the prediction accuracy. The data that was created was split into 2 partitions, one for training, and one for testing (500 entries in each). The code-generated decision tree achieved a 94.4% accuracy in predicting whether the person is diseased or healthy in the test dataset. This shows that the code-generated decision tree must've identified the rules and important attributes which I designed.

It seems that the rules that I was thinking about during the creation of 'right' data, were very similar to the rules which code-generated tree used. This shows that the code-generated decision tree was successful at identifying the trends in data, and creating the rules that dictate how each person should be classified. This is not only proven by the fact that my rules/hand-drawn tree is similar to the code-generated decision tree, but also by the fact that the code-generated decision tree achieved 94.4% accuracy in predicting the health status (disease/healthy) of the persons in the test dataset. 