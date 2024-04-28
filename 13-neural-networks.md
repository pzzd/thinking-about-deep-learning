# Neural Networks

## Artificial Neurons

An artificial neuron used in machine learning is inspired by real neurons and only has a resemblence to the real thing. Artificial neurons borrow the ideas of networking of neurons and hitting a threshold of signals.

Modern artificial neurons have these parts
- one or more inputs: An input is a floating-point number coming from an earlier output. An input is multiplied by its own floating-point weight. Each input has its own weight
- bias: every neuron has its own bias, a number value. It does not come from the output of a previous neuron. It is treated like an input of 1.0 with its own weight.
- a summation step where are all the weighted inputs and the bias are added together
- action function: a mathematical function that takes the addition step as input and outputs a new floating-point value.

## Networks

In deep learning, neurons are arranged in layers: neurons of one layer get inputs from the previous layer and send their outputs to a next layer. Data is processed hierarchically.

The most common network structure is feed-forward network: data from in only one direction, earlier neurons delivering values to later neurons. "The art of desinging a deep learning system lies in choosing the right sequence of layers, and the right parameters, to creat the basic architecture."

## Neural network graphs

A neural network is usually represented as a directed acycyclic graph (DAG). Neurons are nodes that are connected to other nodes by edges. Start of by putting data into input nodes, data flows through edges and subsequent nodes, until it reaches output nodes. No data returns to a previous node; data flows forward only and there are no loops. (A recurrent neural network is cyclic, will cover that later.)

DAGs are popular in machine learning because they are easier to understand, analyze, and design than networks with loops. Loops introduce feedback and can be hard to control.

Later we will see how training temporarily flips the direction of the network using a feed-backward, backward-flow, or reverse-feed algorithm.

## Initializing weights

How weights are initialized can have a big effect on how quickly the network learns. There are several algorithms provided by libraries that initialize weights based on uniform distribution or normal distribution. A default technique offered by a library usually works fine.

## Deep networks

Deep learning refers to the fact that the network used for it is hierarchical and made of many layers. It implies a visual depiction that is vertical with inputs on the bottom, but that's just one convention. 

A hidden layer has neurons and processes data. The total number of these layers is the depth of the network. Some layers are support layers: they do not have neurons and do no processing; they are not counted to determine the network depth.

The layers are:
- input layer: the bottom of the network. There is no processing in this layer, just memory for initial input values. Considered a support layer.
- hidden layers: each layer with neurons that does some processing
- output layer

A fully connected layer (aka FC, linear, or dense layer) is a set of neurons that each receive an input from every neuron on the previous layer. A network made up of only dense layers is called a fully connected network (aka multilayer perceptron). There are other types of layers too; more to come.

## Tensors

A neuron outputs a single value, but a layer has outputs from all of its neurons. We can describe the full output of values from a layer as a tensor. A tensor is a collection of numbers arranged in a box shape with any number of dimensions; tensor is a generic term for an arrangement of numbers like array/list/vector, grid/matrix, volume/block or shape with more dimensions. It's used in terms like input tensor (all the input values) or output tensor (all the output values). 

## Network collapse

Network collapse describes the fact that networked neurons with no activation function are equivalent to a big single neuron. This is because the calculating the weighted some of the inputs all along is arithmetic with addtion and multiplication, so it can be all be reduced to the arithmetic in a single neuron. The functions used are only linear functions and can be combined. But a single neuron has little computation power and are not useful for deep learning.

Later we will see that when a neuron's derivative is 0, it stops learning and makes it more likely that preceding neurons in the network stop learning too. A neuron whose output never changes no longer participates in learning: it has died.

Computing derivatives for outputs of neurons is important in teaching neural networks. For derivatives, you need smooth, continuous functions.

## Activation function 

An activation funciton (aka transfer function or non-linearity) is a non-linear function that takes a floating-point as input and outputs a floating point. Because it is a non-linear function, an activation function can be used to prevent network collapse. 

The same activiation function is usually assigned to all the neurons in a layer. But you can also set a different activiation funtion for each neuron.

### Straight-line functions

Ok, so this is a linear function and doesn't prevent network collapse. This is used either on the output at the very end or after summation in order to process values for the activation function step.

### Step functions

The output for a range of x value equals a y value until a threshold value of x. At this value, the y value changes to another step. There several types of step functions.

### Piecewise linear functions

Different segments are linear, resulting in a total curve that is not a linear function. Popular piecewise liner function are rectified linear unit (ReLU) and leaky ReLU.

ReLU use to be the most popular, but leaky ReLU is becoming moreso because it often learns faster. This because ReLU outputs 0 for every negatiave input, no matter how negative it is, and the derivative is also 0. 

The point at where segments meat has no derivative. This has an impact on teaching neural networks.

### Smooth functions

 Examples:
- softplus: smooths out ReLU
- exponential ReLU
- swish: another smoothed-out ReLU
- sigmoid: sqashes x from negative infinity to infinity into a small range of output values to \[0,1\]
- tanh (hyberbolic tangent): similar to sigmoid, squashes to \[-1,1\]
- sine wave: squashes to \[-1,1\], but doesn't saturate for inputs that are far from 0

### Comparing activation functions

Leaky ReLU provides a different output for every input. It's derivative is not 0. It does not die.

The sine wave function has a non-zero derivative except at the top and bottom of each wave.

Sigmoid and tanh are smooth and outputs are bounded. Experience has shown that networks learn most efficiently when all the values flowing through it are in a limited range.

Generally speaking, eLU or leaky ReLU are applied to most neurons on hiddne layers, particulary fully connected layers.

For a regression network, often no activation function is used on the final layer (or a linear function is used) because the specific output value is important.

In a classifier with two classes, there is a single output value: use sigmoid to decide between one class or the other.

For a classifier with more than two classes, a different activiation function is used.

## Softmax

Softmax is an operation performed on all of the output values from a classifier network with two or more output neurons. It processes them together to produce a new output value for each neuron: it turns raw score outputs into class probabilities between 0 and 1. The probabilities sum up to 1.

Softmax takes the place of an activation function that would normally be applied to output neurons.

If one class has a larger score than some other class, the network things that class is more likely. But the score values don't tell you how much more likely: use softmax to calculate that.

Softmax exaggerates the influence of the output with the largest value. It crushes the other values such that the largest value dominates the others more obviously.


