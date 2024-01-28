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
- regularization: these are techniques to continue learning process as long as possible. Includes limiting value of parameters used by classifier
