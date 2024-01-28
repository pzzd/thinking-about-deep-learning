# Overfitting and Underfitting

**Overfitting** is when a system learns well from training data but does poorly processing new data. This is usually the harder problem in deep learning. During training, training accuracy is high and training error is low. When evaluating new data, generalization accuracy is low and generalization error is high. Controlled by stopping learning process when rules get too specific and using regularization methods.

**Underfitting** is when a system does not learn well from the training data. Rules are too vague or generic. Fixed with more training data.

Errors you can measure are:
- training error: happen during training
- validation error: estimate of errors system will make when deployed
- generalization error: errors the system will make when deployed

In a learning process where you validate after each epoch, typically both training and validation errors drop.  But at some point the validation error no longer improves (flattens or gets worse) while the training error continues to improve: this is overfitting. Overfitting happens when the system learns from information specific to the data rather than general rules, which is why the training error keeps improving. 

To control overfitting:
- early stopping: stopping some time before training error is 0. Library functions come with a way to help detect when validation error starts to rise from a set of noisy validation data.
- regularization: these are techniques to continue learning process as long as possible. One way is limiting value of parameters used by classifier, so that focus is not concentrated too much on a single parameter. But there are lot of other ways, too.

**Bias** is the tendency of a system to consistently learn the wrong things. A large amount of bias means that a system is prejudiced toward a particular kind of result. Data is not much of an influence. High bias avoids overfitting but doesn't match data very well.

**Variance** is the tendency of a system to learn irrelevant details. A large amount of variance means that the answers returned by the system are too specific to the data. Data has a higher influence. High variance risks over fitting because it matches the data very well.

Typically, you have to make a decision in the bias-variance trade-off.

Bias and variance are used to describe families or collections of results, not a single result. For example, in a situation where you are trying to describe noisy data (figure 9-8) with a single curve, you can analyze it several times to produce a number of curves to find the right curve. You must weigh a preference for bias or variance in the resulting curves. You select random points from the data and fit a curve in several iterations. 

Favoring bias: You choose to get a simple, smooth curve to fit the data: this is a predetermined preference for a simple shape. In each iteration, the curve is so simple that it doesn't actually pass through the random sample of points. Over the whole collection of iterations the curves look very similar to each other. This shows high bias (favoring a certain shape) and low variance (the curves are very alike).

Favoring variance: You choose to fit a complex curve to the sample points in each iteration. In each iteration, the curve does a better job of passing through some data points or getting close to them. Over the whole collection of iterations, the curves differ quite a bit. This shows low bias (not so much predetermined preference on the curve shape) and high variance (the curves are not alike and strongly influenced by the data).
