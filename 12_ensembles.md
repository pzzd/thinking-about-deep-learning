# Ensembles

Groups of simple learners, called ensembles, are used simultaneously to avoid mistakes. The output of an ensemble is the most popular result from its members.

## Voting
Each learner is trained on different datasets or different subsets of a single training set. This reduces the effect of bias that originates from training data. Ensemble members cast a vote in classifying. 

There are different ways to tally the votes:
- plurality voting: whichever classification gets the most votes, wins.
- weighted plurality voting
- factoring in learner confidence

### Decision tree ensembles

Ensembles are frequently used combine decision trees, which reduces their drawbacks like overfitting.

Bagging (bootstrap aggregating): from full data set, make sample sets using sample with replacement (bootstrapping). These are used to train a collection of decision trees. To evaluate a new sample, give it to all the decision trees in the ensemble: each tree gives a class as a result, treated as a vote in plurality voting. Bagging takes two parameters: how many samples to use in each bootstrap, and how many trees to build.

The law of diminishing returns in ensemble construction: adding more classifiers makes the ensemble’s predictions better, but at some point, adding more makes the system slower and the results stop improving. Use about the same number of classifiers as you have classes of data. Or use cross-validation to search for the best number of trees for a data set.

Random forest is the result of selecting features randomly at each node for a collection of decision trees. Feature bagging involves selecting a random feature on which to split a node in a decision tree. This avoids splitting nodes the same way for every tree that is trained and increases the diversity of our decisions.

Extremely randomized trees (extra trees) are produced by splitting nodes randomly based on the values it has. This reduces overfitting.

## Boosting

Boosting uses many small, fast, and inaccurate learners to make a single accurate learner.

A weak learner is any learner that is the slightest bit accurate, correct maybe just better than 50% of the time. If it’s worse than 50%, you can invert the results and now it’s better than 50%.

A weak learner is easy to make. Example: a decision tree that is one test deep (a decision stump).

Weak learners can be combined to make one strong learner. One weak learner sets a boundary between classes in a data set: this is how it votes on a class. Other weak learners set different boundaries. A boosting algorithm can weight each weak learner’s vote; not sure how weighting is determined. Then the votes are added up to determine the class of a sample.

Boosting only applies to binary classification algorithms. It’s very well suited to decision stumps.
