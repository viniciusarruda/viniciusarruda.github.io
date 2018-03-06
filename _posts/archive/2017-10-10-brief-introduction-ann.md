---
layout: archive-post
title: A Brief Introduction to Artificial Neural Networks
excerpt: "An introduction to Artificial Neural Networks with some numerical examples to solve logical gates and a simple way of training a ANN with genetic algorithm to play the Flappy Bird game."
categories: archive
tags: [artificial-intelligence, artificial-neural-networks, bio-inspired, python, pygame]
comments: true
share: true
---

## Biological Neuron

![Unable to display image]({{ site.url }}/images/neuron.png)
<br><sub>*Anatomy of a multipolar neuron.*</sub>
{: .center-small-image}

The biological neuron has its structure like the image above, where it gets the signals from its dendrites and somehow processes this information (we still do not know exactly how it is done), then a spike is fired through its axon, passing the signal through the terminal of the axon to the dendrites of other neurons.

## The McCulloch-Pitts Neuron Model

![Unable to display image]({{ site.url }}/images/mp_neuron.png)
<br><sub>*McCulloch-Pitts neuron model.*</sub>
{: .center-small-image}

Based on the biological neuron, Warren McCulloch and Walter Pitts [presented the idea of neural networks as computing machines](http://www.cse.chalmers.se/~coquand/AUTOMATA/mcp.pdf){:target="_blank"} in 1943, creating a fairly simple model of the biological neuron. Each $$\,i\text{-th}\,$$ dendrite has an input $$\,x_i\,$$ which is multiplied by its respectively weight $$\,w_i$$. The result of each dendrite is summed up into a single value, then a bias $$\,b_i\,$$ is added and passed it throught an activation function $$\,\varphi(\cdot)\,$$ to decide if it fires or not.

Writing in matrix form, the weights is a matrix $$\,W\,$$ that must be transposed to perform the dot product with the input column vector $$\,X\,$$ plus the bias column vector $$\,B\,$$, resulting in the following equation: $$\,\varphi(W^\intercal \cdot X + B)$$.

### A Numerical Example

#### Or

The `or` problem is a simple example, but it is intuitive for the first contact with artificial neural networks. Using the MP-neuron, it is possible to solve it by choosing the following weights:

![Unable to display image]({{ site.url }}/images/or_solve.png)
<br><sub>*Or solution.*</sub>
{: .center-large-image}

Where the bias is equal to zero and the heaviside function is used as an activation function.

![Unable to display image]({{ site.url }}/images/activationfunction.png)
<br><sub>*Heaviside function.*</sub>
{: .center-gg-image}

Which yields a line, i.e. decision boundary, which the data below and above it belongs to the classes $$\,0\,$$ and $$\,1\,$$ respectively. The figure below illustrates the situation:

![Unable to display image]({{ site.url }}/images/or.png)
<br><sub>*Graphical solution of the or problem.*</sub>
{: .center-large-image}

#### Xor

![Unable to display image]({{ site.url }}/images/xor_problem.png)
<br><sub>*Xor problem.*</sub>
{: .center-large-image}

Note that the xor can not be splitted by one straight line and, since the MP-neuron gives the possibility to draw only a straight line, i.e. a linear equation, is necessary to use more than one MP-neuron and also, change the architecture of the network.

The strategy is to map the data to other space, thus the first layer will have the role to map the data to another space. First, isolating the outside point, the following line is desired to be a decision boundary:

![Unable to display image]({{ site.url }}/images/firstfirstlayerplot.png)
<br><sub>*Isolating the (1,1) data.*</sub>
{: .center-large-image}

This is obtained by the MP-neuron below:

![Unable to display image]({{ site.url }}/images/firstfirstlayerxor.png)
<br><sub>*MP-neuron that isolates the (1,1) data.*</sub>
{: .center-large-image}

Then, to isolate the other red point, the pink line is added to be another decision boundary:

![Unable to display image]({{ site.url }}/images/xorfirstlayerplot.png)
<br><sub>*Isolating the (0,0) data.*</sub>
{: .center-large-image}

This is obtained by the following MP-neuron:

![Unable to display image]({{ site.url }}/images/secondfirstlayer.png)
<br><sub>*MP-neuron that isolates the (0,0) data.*</sub>
{: .center-large-image}

Merging the two MP-neurons, it yields a function of mapping $$\,f : (X,Y) \rightarrow (X',Y')\,$$: 

![Unable to display image]({{ site.url }}/images/firstlayer.png)
<br><sub>*Layer that maps the data to another space.*</sub>
{: .center-large-image}

Which gives the following mapping of the data: 

![Unable to display image]({{ site.url }}/images/resultfirstlayer.png)
<br><sub>*Result of mapping.*</sub>
{: .center-large-image}

Note that now, the values $$\,(0,1)\,$$ and $$\,(1,0)\,$$ from the original space are overlapped in this new space on $$\,(0,1)\,$$, and now the data can be separated by a straight line, so the work now is to find the linear equation that represents it.

![Unable to display image]({{ site.url }}/images/solution_xor.png)
<br><sub>*Graphical solution of the xor problem.*</sub>
{: .center-large-image}

Which can be the equation $$\,Y' = X' + 0.5\,$$. Putting all together: 

![Unable to display image]({{ site.url }}/images/xor_nn.png)
<br><sub>*Xor solution.*</sub>
{: .center-small-image}

In these examples, the artificial neural networks was trained by hand, what does not make it powerful since it can spent a lot of time to do it and for more complex problems it turns infeasible.

## Training an ANN with GA

For this task, was trained an artificial neural network to play the [Flappy Bird](https://en.wikipedia.org/wiki/Flappy_Bird){:target="_blank"} game (inspired by [this](http://www.askforgametask.com/tutorial/machine-learning-algorithm-flappy-bird/){:target="_blank"} post) and it was chosen the [representation of a chromosome as real values]({{ site.url }}/projects/genetic-algorithm/#Representation){:target="_blank"} to represent the weights of the network. 

![Unable to display image]({{ site.url }}/images/flappybirdarquitecture.png)
<br><sub>*Architecture of the ANN used.*</sub>
{: .center-small-image}

The architecture of the neural network used is shown above, and the bird will flap or not if the output is $$\,1\,$$ or $$\,0\,$$, respectively.

![Unable to display image]({{ site.url }}/images/xynnflappybird.png)
<br><sub>*Meaning of the ANN inputs.*</sub>
{: .center-small-image}

The $$\,X\,$$ is the horizontal distance between the bird and the center of the wall and the $$\,Y\,$$ is the vertical distance between the bird and the center of the gap in the wall. The fitness used in the genetic algorithm is the total distance traveled by the bird.

<iframe width="560" height="315" src="https://www.youtube.com/embed/C0YRzeBEjaY" frameborder="0" allowfullscreen></iframe>

The video above was captured while training the network. To increase the difficulty over time, the speed was increased every 10 seconds.

<div markdown="0" style="text-align: center"><a href="https://github.com/viniciusarruda/brief-introduction-to-artificial-neural-networks" target="_blank" class="btn">CHECKOUT THE CODE ON GITHUB</a></div>
