# Neural Networks

## Artificial Neurons

An artificial neuron used in machine learning is inspired by real neurons and only has a resemblence to the real thing. Artificial neurons borrow the ideas of networking of neurons and hitting a threshold of signals.

Modern artificial neurons have these parts
- one or more inputs: An input is a floating-point number coming from an earlier output. An input is multiplied by its own floating-point weight. Each input has its own weight
- bias: every neuron has its own bias, a number value. It does not come from the output of a previous neuron. It is treated like an input of 1.0 with its own weight.
- a step where are all the weighted inputs and the bias are added together
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

