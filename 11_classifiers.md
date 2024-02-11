# Classifiers

There are two approaches to classifiers:

- parametric: the classifier algorithm starts with a preconceived description of the data, then searches for parameters of that description to make it fit. E.g., if we have normally distributed data, we would look for mean and standard deviation. 
- nonparametric: data is analyzed first and then a way to represent it comes next. E.g., try to find a boundary that splits data into classes.

## k-Nearest Neighbors

kNN is a nonparametric algorithm. The letter k refers to a number: a hyper parameter that is set before the algorithm runs. kNN works with labeled data; it’s used in supervised learning.

When kNN is used, it accepts a sample and a value for k. The k value is the number of the neighbors nearest to the sample. Whichever class is most populous with k nearest neighbors of a sample is the sample’s class. There are various ways to break ties and handle exceptional cases.

kNN is fast to train: it saves a copy of every sample into a db. But it requires a lot of memory. This can slow the algorithm down.

kNN is a ‘lazy’ or ‘on-demand’ algorithm: it does not process samples during the learning phase, it only saves them.

Classification can be slow because of having to calculate the distance to neighbors. This might make kNN a bad option when you need a real-time system.

A lot of training data is required for kNN to classify effectively. But if the data also has a lot of dimensions, then kNN suffers the “curse of dimensionality”.  Also, a higher number of dimensions requires a lot of training data, otherwise the data is too spread out for classifying.

Finding the right value for k takes repeated experimentation and cross-validation.

kNN doesn’t explicitly represent boundaries between classes; it can handle any distribution of classes.

## Decision Tree

AKA categorical variable decision tree. They work with discrete categorical variables.

A tree is built from the samples in the training set. During training, when a sample makes it to a leaf, it’s compared to the class of other samples in the leaf. If it’s a match, the sample is added to the leaf. If not, a decision node is added here and the samples are divided between to new leaves. The test is saved with the node.

Decision tree is a ‘greedy’ algorithm: it’s focused on maximizing its immediate, short-term gains. The tree is built one sample at a time. It’s only aware of the data it has processed and the data it is currently processing. 

Evaluating new samples starts at the root and you work your way down to a leaf after going to node tests. Samples are classified by the leaves they end up in.

Sometimes leaves have a mix of classes. In that case, you might say your sample has a certain probability of being of a particular class.

Decision tree results are explainable. That doesn’t mean they are correct or fair.

Decision trees are prone to overfitting. They are sensitive to each input sample: every sample can influence the shape of the tree. You can see this clearly when you create different trees from different 70% cut of the training data.  Overfitting can be controlled by depth limiting: The first few steps of training give a general tree shape and the overfitting tends to happen deep at the end of branches. Overfitting can also be controlled by setting a minimum number of samples required before splitting. Another approach is pruning leaves at the end of building the tree; you have to accept a certain amount of error. All these methods to control overfitting have an impact on the results.

### Splitting nodes


Does a node need to be split? It depends on how much samples in a node should be considered in the same class. ‘Purity’ is a number that describes the uniformity of a node’s contents. Check the purity against a threshold to determine whether the node should be split.

How should a node be split? Use one or more features to make up splitting tests. Each node can have its own test. There are two ways to test the results of splitting:
- information gain compares the  measurements of the entropy of the node and the entropy of children resulting from the split.  A uniform node has low entropy. If you split the node and thereby reduce entropy, you have gained information.
- Gini impurity is a technique that uses math to reduce the chance of an incorrect classification.

Libraries offer ways to try a potential split. You likely have to try different options and pick what works best for your data.

## Support Vector Machines

SVM is a parametric algorithm that finds the boundary that is farthest from all the points in clusters of data. 

Support vectors are the nearest samples between different classes of samples.  SVM identifies these nearest samples, and then finds the boundary (a line in 2D data or a plane in 3D data) near the middle that’s farthest from every sample in each set. The distance from the boundary to the lines/boundaries that pass through the support vectors is called a margin.

The boundaries between samples are the only data saved to memory.

SVM takes parameter C, to control how strict the algorithm is about letting points into the region between the margins. A higher value of C means the algorithm demands a more empty zone in the margins around the boundary. C is found using trial and error and cross-validation.

SVM is for linear shapes like lines or plans. But you can use a trick to apply SVM to classes arranged like a 2D bulls eye. You can temporarily add a third dimension to each sample: that dimension is the distance of each sample from the center. This effectively separates two classes into a point of a cone and the base of the cone, and now SVM can place a boundary.

You can try other transformations to find other ways to separate classes in noisy data. SVM uses the kernel trick to find distances between transformed points without transforming them so you can find the best transformation quickly.

## Naive Bayes

This is a parametric classifier that used when you need quick results and you are ok with less accuracy.

It’s quick because you start with assumptions about the data, using that as prior. This approach is ‘naive’ because the prior is decided without knowing the contents of the data: you assume you know the structure of the data.

The less well the data matches the assumption, the worse the results are. But if the assumption is correct or nearly so, you can classify quickly.  This turns out to be the case fairly often. For example, it is common to assume samples follow a Gaussian distribution. Naive Bayes often does a good job on all kinds of data, probably because a lot of real-world data comes from Gaussian processes.

## Comparing Classifiers

### kNN

Pros: Flexible, can handle complicated data structure from class samples in training data.

Cons: Slow. Requires a lot of memory and disk space.

### Decision trees

Pros: Fast to train, fast when making predictions. Can handle weird boundaries between classes. Easy to interpret.

Cons: Prone to overfitting. 

### SVM

Pros: Fast predictions. Does not require a lot of memory.

Cons: Training time grows with size of training set.

### Naive Bayes

Pros: Trains quickly. Predicts quickly. Not too hard to explain results. No parameters to tune. Often produces good results if classes are well separated. Works well with Gaussian data. Works well with data with many features. Good to try early to get to know the data set.

