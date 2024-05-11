Backpropagation is the method of applying the gradient of the model's error backward from the final layer back to the first layer. 

The error gradient is the informatin tht tells how the error changes when the weight changes.

Networks learn by minimizing mistakes; each mistake has a cost, loss, or penalty. During training, networks reduce the cost so the outputs are closer to what we want.

A brand-new classifier starts with small random weights for each neuron. When the prediction from the whole network is wrong, an error score (aka error, penalty, loss) is a calculated. The error is a floatig point number (usually always positive); the larger the error, the more wrong the network's prediction for the label of a given input. The goal is to reduce the error to as close to 0 as possible over the entire training set.

Training involves penalizing incorrect answers by assigning them a positive error score.

Can penalize several things at once by giving each one a value and adding them all up for a total error.

Learning seems to be most efficient when the weights in the network are small, like \[-1, 1\]. This can be enforced with an error term that has a large value when the weights get too far from this range.

Let's assume we're freezing the whole network with its values and focusing on a single weight. The error curve comes from plotting the weight on the x axis and the network's error on the y axis. The error gradient is the derivative of the curve for any given weight value. To reduce error for a positive-slope error gradient, reduce the weight; for a negative-slope error gradient, increase the weight. See figure 14-2. We can improve the network efficiently by finding every weight's error gradient and adjusting them simultaneously: the algorithm for this is called gradient descent. To avoid adverse ripple effects, only small changes to every weight are made.

Reducing overall error by adjusting network's weights happens in two steps: 
- backpropagation: for each neuron, a number related to the network's error is calculated and stored. Using this, every weight coming into every neuron is updated.
- optimization: coming in the next chapter.

Activation functions are nonlinear and are essential to making neural networks work but we will ignore them in this discussion. Just know that activiation functions are accounted forin any backprop implementation.

When any neuron output in the network changes, the final output error changes by a proportional amount. (This is true if you leave out activiation functions.) The change in the network's final output can be predicted from either a change to any neuron's output or any weight in the network.
- Let's consider an neuron whose output has changed, for whatever reason; this change has an effect on the network's error, but what effect exactly? Delta is a number associated with a neuron as a result of evaluating the current network with the current sample. If a neuron's output changes by a particular amount (called m), we can multiply that change by the neuron's delta to see how the entire network's output will change. Because the neuron's output will change by m, we know the change in the final error is m times the neuron's delta.
- Where does m come from? We can produce an m by changing a neuron's input, that is, the previous neuron's output.
- We can use the delta associated with each neuron to tell whether each of its incoming weights should be adjusted in the positive or negative direction.
- Put another way: delta scales the change in the output of a neuron to give the change in the error.
- Adding the original error and the change in the error gives the new error. If either m or delta is negative (not both!) the error decreases.

Now a simplified discussion of backpropagation.
- Backprop is all about finding the delta value for each neuron.
- First find the error gradients at the end of the network: the output layer.
- The propagate those gradients backward to the start.
- The error of a network is calculated by comparing the final output or prediction of a network with the label for the sample. For example you could make lists of predictions and lists of labels and compare them with one-hot encoding. Cross entropy is used for this. Almost all deep learning libraries have a built-in cross entropy function to find the error in a classifier. This function also provides a gradient to show how the error will change if we increase any of its inputs.
- How much should we nudge an input? Look at the error gradient (the slope of the error curve, that is, its derivative) to find decide. The cross entropy function does NOT give the error curve, only the derivative. See Figure 14-9 for an example.
- The gradient accurately predicts the new error after each change to the prediction value as long as the change is small. A small change on a graph shows the gradient and curve are still close together. The bigger the change in the prediction value, the less accurate the prediction in the error:the gradient line and the error curve pull away from each other.
- The change in error is equal to the slope of the gradient times the change in the output. I think that means that the slope of the gradient at the original output is delta! See Figure 14-9 and 14-10.
- As soon as the value of the prediction changes, for any reason, the error curve changes and neuron's delta has to be computed all over again.
- This is how we do a round of finding the deltas for all the neurons. They will be used later to change weights.

It may not be possible to get the error of a network to 0.
- It may not be possible to get every prediction with an error of 0 if adjusting weights in a previous neuron reduces error in one output neuroon but increases error in another output neuron.
- We may not have the error to be 0 anyway. This might indicate overfitting: training error decreases but ability to handle new data gets worse. We want to minimize error without overfitting.

We can improve all the weights in the network at the same time as long as we take very small steps. After adjusting weights, evaluate errors again to find new curves, new derivatives, and new deltas on a new sample. Then repeat.


