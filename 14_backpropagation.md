Backpropagation is the method of applying the gradient of the model's error backward from the final layer back to the first layer. 

The error gradient is the informatin tht tells how the error changes when the weight changes.

Networks learn by minimizing mistakes; each mistake has a cost, loss, or penalty. During training, networks reduce the cost so the outputs are closer to what we want.

A brand-new classifier starts with small random weights for each neuron. When the prediction from the whole network is wrong, an error score (aka error, penalty, loss) is a calculated. The error is a floatig point number (usually always positive); the larger the error, the more wrong the network's prediction for the label of a given input. The goal is to reduce the error to as close to 0 as possible over the entire training set.

Training involves penalizing incorrect answers by assigning them a positive error score.

Can penalize several things at once by giving each one a value and adding them all up for a total error.

Learning seems to be most efficient when the weights in the network are small, like \[-1, 1\]. This can be enforced with an error term that has a large value when the weights get too far from this range.
