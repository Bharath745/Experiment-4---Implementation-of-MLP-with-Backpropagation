# Experiment-4---Implementation-of-MLP-with-Backpropagation

## AIM:
To implement a Multilayer Perceptron for Multi classification

## EQUIPMENTS REQUIRED:
Hardware – PCs
Anaconda – Python 3.7 Installation / Google Colab /Jupiter Notebook

## RELATED THEORETICAL CONCEPT:

A multilayer perceptron (MLP) is a feedforward artificial neural network that generates a set of outputs from a set of inputs. An MLP is characterized by several layers of input nodes connected as a directed graph between the input and output layers. MLP uses back propagation for training the network. MLP is a deep learning method.
A multilayer perceptron is a neural network connecting multiple layers in a directed graph, which means that the signal path through the nodes only goes one way. Each node, apart from the input nodes, has a nonlinear activation function. An MLP uses backpropagation as a supervised learning technique.
MLP is widely used for solving problems that require supervised learning as well as research into computational neuroscience and parallel distributed processing. Applications include speech recognition, image recognition and machine translation.
 
MLP has the following features:

Ø  Adjusts the synaptic weights based on Error Correction Rule

Ø  Adopts LMS

Ø  possess Backpropagation algorithm for recurrent propagation of error

Ø  Consists of two passes

  	(i)Feed Forward pass
	         (ii)Backward pass
           
Ø  Learning process –backpropagation

Ø  Computationally efficient method

![image 10](https://user-images.githubusercontent.com/112920679/198804559-5b28cbc4-d8f4-4074-804b-2ebc82d9eb4a.jpg)

3 Distinctive Characteristics of MLP:

Ø  Each neuron in network includes a non-linear activation function

![image](https://user-images.githubusercontent.com/112920679/198814300-0e5fccdf-d3ea-4fa0-b053-98ca3a7b0800.png)

Ø  Contains one or more hidden layers with hidden neurons

Ø  Network exhibits high degree of connectivity determined by the synapses of the network

3 Signals involved in MLP are:

 Functional Signal

*input signal

*propagates forward neuron by neuron thro network and emerges at an output signal

*F(x,w) at each neuron as it passes

Error Signal

   *Originates at an output neuron
   
   *Propagates backward through the network neuron
   
   *Involves error dependent function in one way or the other
   
Each hidden neuron or output neuron of MLP is designed to perform two computations:

The computation of the function signal appearing at the output of a neuron which is expressed as a continuous non-linear function of the input signal and synaptic weights associated with that neuron

The computation of an estimate of the gradient vector is needed for the backward pass through the network

TWO PASSES OF COMPUTATION:

In the forward pass:

•       Synaptic weights remain unaltered

•       Function signal are computed neuron by neuron

•       Function signal of jth neuron is
            ![image](https://user-images.githubusercontent.com/112920679/198814313-2426b3a2-5b8f-489e-af0a-674cc85bd89d.png)
            ![image](https://user-images.githubusercontent.com/112920679/198814328-1a69a3cd-7e02-4829-b773-8338ac8dcd35.png)
            ![image](https://user-images.githubusercontent.com/112920679/198814339-9c9e5c30-ac2d-4f50-910c-9732f83cabe4.png)



If jth neuron is output neuron, the m=mL  and output of j th neuron is
               ![image](https://user-images.githubusercontent.com/112920679/198814349-a6aee083-d476-41c4-b662-8968b5fc9880.png)

Forward phase begins with in the first hidden layer and end by computing ej(n) in the output layer
![image](https://user-images.githubusercontent.com/112920679/198814353-276eadb5-116e-4941-b04e-e96befae02ed.png)


In the backward pass,

•       It starts from the output layer by passing error signal towards leftward layer neurons to compute local gradient recursively in each neuron

•        it changes the synaptic weight by delta rule

![image](https://user-images.githubusercontent.com/112920679/198814362-05a251fd-fceb-43cd-867b-75e6339d870a.png)



## ALGORITHM:

1.Import the necessary libraries of python.

2. After that, create a list of attribute names in the dataset and use it in a call to the read_csv() function of the pandas library along with the name of the CSV file containing the dataset.

3. Divide the dataset into two parts. While the first part contains the first four columns that we assign in the variable x. Likewise, the second part contains only the last column that is the class label. Further, assign it to the variable y.

4. Call the train_test_split() function that further divides the dataset into training data and testing data with a testing data size of 20%.
Normalize our dataset. 

5.In order to do that we call the StandardScaler() function. Basically, the StandardScaler() function subtracts the mean from a feature and scales it to the unit variance.

6.Invoke the MLPClassifier() function with appropriate parameters indicating the hidden layer sizes, activation function, and the maximum number of iterations.

7.In order to get the predicted values we call the predict() function on the testing data set.

8. Finally, call the functions confusion_matrix(), and the classification_report() in order to evaluate the performance of our classifier.

## PROGRAM 

```
import pandas as pd
import sklearn
from sklearn import preprocessing
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.neural_network import MLPClassifier
from sklearn.metrics import classification_report, confusion_matrix

df = pd.read_csv('IRIS.csv')
df.head

names = ['sepal-length','sepal-width','petal-length','petal-width','Class']

# Take first 4 columns ans assign them to variable "X"
X = df.iloc[:,0:4]
# Take first 5th columns and assign them to variable "Y". Object dtype refers to strings
Y = df.select_dtypes(include=[object])
X.head()
Y.head()

# Y actually contains all categories or classes
Y.species.unique()

# Now transforming categorial into numerical values
le = preprocessing.LabelEncoder()
Y = Y.apply(le.fit_transform)
Y.head()

# Train and test split (80% of data into training set and 20% into test data)
X_train, X_test, Y_train, Y_test = train_test_split(X,Y,test_size = 0.20)

# Feature Scaling
scaler = StandardScaler() 
scaler.fit(X_train)
X_train = scaler.transform(X_train)
X_test = scaler.transform(X_test)
mlp = MLPClassifier(hidden_layer_sizes=(10,10,10),max_iter=1000)
mlp.fit(X_train,Y_train.values.ravel())
predictions = mlp.predict(X_test)
print(predictions)

# Evaluation of algorithm performance in classifying flowers
print(confusion_matrix(Y_test,predictions))
print(classification_report(Y_test,predictions))
```

## OUTPUT :

## First five rows:

![image](https://github.com/Bharath745/Experiment-4---Implementation-of-MLP-with-Backpropagation/assets/94508354/d9d473e3-f3f0-4695-82a2-3a615a4547de)

## First five rows of X:

![image](https://github.com/Bharath745/Experiment-4---Implementation-of-MLP-with-Backpropagation/assets/94508354/5ba86a10-c94e-48e7-a00e-b3c02631c235)

## First five rows of Y:

![image](https://github.com/Bharath745/Experiment-4---Implementation-of-MLP-with-Backpropagation/assets/94508354/f1ddc0f3-0734-4194-a8d3-9fef033b607c)


## Unique values of Y:

![image](https://github.com/Bharath745/Experiment-4---Implementation-of-MLP-with-Backpropagation/assets/94508354/e36502a1-9492-4a1d-af56-4bf1717df6eb)


## Transforming Categorical to numerical values:

![image](https://github.com/Bharath745/Experiment-4---Implementation-of-MLP-with-Backpropagation/assets/94508354/de04aaa3-3557-45d4-9134-ee61d0bc038a)


## Prediction:

![image](https://github.com/Bharath745/Experiment-4---Implementation-of-MLP-with-Backpropagation/assets/94508354/a84ffb29-d47f-4f18-a4a1-348d1c15ee36)


## Classification report:

![image](https://github.com/Bharath745/Experiment-4---Implementation-of-MLP-with-Backpropagation/assets/94508354/5459032d-eca9-4345-841b-43a26c947331)

## Confusion matrix:

![image](https://github.com/Bharath745/Experiment-4---Implementation-of-MLP-with-Backpropagation/assets/94508354/0c823be8-25e9-49d3-b841-8f387d191d03)


## RESULT:

Thus, a program to implement Multilayer Perceptron for Multi Classification is successfully created and executed.
