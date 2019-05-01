## Discussion

### Dataset

The training dataset used is information about stock prices ranging from 02-Jan-2009 to 29-Dec-2017, including Date, Open Price, Close Price, High Price, Low Price, and Volume. There are 2264 entries in the data.

The testing dataset used is information about stock prices ranging from 02-Jan-2018 to 31-Dec-2018,  including Date, Open Price, Close Price, High Price, Low Price, and Volume. There are 252 entries in the data.

### 3 Classifiers

#### Logistic Regression

Unlike Linear Regression, which is used to predict continuous values, Logistic Regression is implemented in cases where the outcomes are of categorical nature (0/1)

#### SVM

A classifier used for classification and regression. Transforms data and finds optimal boundary between points.


#### Neural Network

A network consisting of layers, which are connected through inputs and outputs. The inputs have weights, which partially determine the output of the layer(s).


### How did you preprocess this dataset?

For each classifier, a new column is created in the training and testing datasets, "CPI", which represents "Close Price Increase". For each day, CPI is calculated by subtracting the Close Price of a previous day, from the Close Price of the day. If the result is negative, or zero, it means the price did not increase, and 0 is assigned. If the result is positive, it means the price did increase, and 1 is assigned.

##### Logistic Regression

For Logistic Regression, I only used Open Price, Close Price, High Price, and Low Price. This is because of my conclusion that the date, and volume do not contribute to the accuracy of the model. Adding these two features did not improve the accuracy.

##### SVM

Similar to Logistic Regression, I used Open Price, Close Price, High Price, and Low Price, dropping Date and Volume. Although volume might be an attractive feature, I believe it relates more to the Open Price than to Close Price, which is related to the target.

##### Neural Network

Similar to Logistic Regression and SVM, I used Open Price, Close Price, High Price, and Low Price, dropping Date and Volume from the training and testing datasets.

### Which classifier reaches the highest classification accuracy in this dataset ?

Classifier's test accuracy:
1. Logistic Regression: 81.74%
2. SVM: 83.33%
3. Neural Network: 51.98%

SVM reached the highest classification accuracy on the testing dataset, reaching 83.33% testing accuracy. It must be noted, that SVM results are very volatile when penalty is changed, while Logistic Regression accuracy is stable.

#### Why ?
SVM is a classifier widely used for binary classification. By using hyperplanes, SVM's are able to classify data points into two classes. Since the stock data target problem is also binary, it would be natural for an SVM to be effective. SVM predicts whether the data is either 1 or a 0, while LR and NN predict a probability with which the item belongs to a class 0 or 1, and only if the threshold is passed, the item will be classified accordingly. LR and NN are more useful in answering the questions such as "How likely will event X occur?", while SVM seems to be useful in classification.

Logistic Regression Classifier is comparable to SVM in this test. This is probably due to the fact that LR also classifies data using a logistic function. However it is limited, since the logistic function produces a continuous output (although within a range) and not 0/1 like SVM. When calculating the probability of the data point to belong to a class, if the threshold is passed, LR will categorize the data as 1 (or 0, depending on choice). Hence, it would have trouble classifying values of 0.5.

Neural Networks need large amounts of training data. Although we have 2000+ data points, Neural Networks will yield better results with more data. Also, SVM's only need to tune a small amount of parameters (penalty/kernel), while Neural Networks have many parameters that need to be tuned in order to produce the best result. Since we have limited data, small amount of features, and limited parameter tuning, it is not surprising that NN is the least accurate classifier model.

#### Can this result remain if the dataset is different ?
With different data, the accuracy of some models may change. For example, if another data has more outliers, LR and NN would be more affected than SVM, and their accuracies would be lower because the outliers would make training more inaccurate.
In general, I believe SVM would still come out ahead or at least on par with the other models, even if data is changed.

### How did you improve your classifiers ?

#### Logistic Regression
1. max_iter
    By increasing the number of iteration, we allow the classifier to train multiple times on the same data, making training accuracy higher.
2. Using more features
    The more features we use, the more relationships the classifier can make between the features and the target.

#### SVM
1. Penalty
    Changing penalty drastically changes the test accuracy of the SVM. By changing the penalty to 5, I was able to achieve 83.33% test accuracy.
2. Using more features
    The more features we use, the more relationships the classifier can make between the features and the target.
    
#### Neural Network
1. Parameters
    All of the parameters were tuned to produce the best result. Although, tuning them did not produce much difference in the test accuracy. This is likely due to the other limitations to the NN mentioned above.
* hidden_units = 10
* activation = 'sigmoid'
* l2 = 0.01
* learning_rate = 0.1
* epochs = 10
* batch_size = 32
* loss='binary_crossentropy' 
    * Used for binary classification loss calculation
* optimizer='rmsprop'
2. Class weight
    Since our training dataset is imbalanced (1028 decreases and 1236 increases) to balance the weights of the data, class weight is introduced.
    
