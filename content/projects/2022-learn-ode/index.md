---
title: 'Learning Ordinary Differential Equations from Data'
date: 2022-06-27T11:36:49-04:00
lastmod: 2022-06-27T11:36:49-04:00
featured: true
weight : 100
summary: 'Assume you are given observations of a dynamical system at a few time points and want to learn its underlying ODE. Problems like this are abundant in scientific applications and there are several machine learning approaches to this problem. One approach with soaring popularity is called Neural ODEs, that is, ODEs whose dynamics are trainable neural networks, which makes them very flexible. Another approach that does not rely on neural networks and thus can yield a more interpretable result is called sparse identification of nonlinear dynamics (SINDy). The goal of this project is to compare the advantages and disadvantages of both of these (and perhaps other) approaches experimentally and mathematically. One particular aspect we will investigate is how ODE properties like stability and stiffness impact the effectiveness of the learning process.'
tags: ["Summer 2022"]
---
<!--more-->
<!-- --- -->
<!-- # Emory REU Learn ODE:   -->

<!--Starting new section-->
<!-- --- -->

This post was written by Mathias Heider, Emma Hayes, and Carrie Vanty and published with minor edits. The team was advised by Dr. Deepanshu Verma.

In addition to this post, the team has also created slides for a [midterm presentation]



## Project Overview: 
Imagine a spring mass system (Figure 1). We want to be able to find the location of the mass at any given time point. In order to find the coordinates, we must understand the dynamics of the system. In a spring mass system, energy is conserved, so we chose to use a Hamiltonian Ordinary Differential Equation, which has the quality of energy conservation. To solve our problem, we use machine learning that uses Hamiltonians in the forward propagation to predict our coordinates.
<!--Image-->
![mainImage](images/Simple_harmonic_oscillator.gif "Figure 1")

Our project aims to compute both a value for the Hamiltonian and coordinates for any given time using Hamiltonian Inspired neural networks. We will then compare our results to Sparse Identification of Nonlinear Dynamics to assess efficiency and accuracy. In order to build our neural network, we will begin by talking about the background of machine learning. Then, we will discuss the mathematics behind our network, including differential equations and discretization choice. Results will then be presented and analyzed.



## Background: 
In this project we heavily rely on machine learning, specifically deep learning. Machine Learning is the use of statistical learning and optimization methods that let computers analyze datasets and identify patterns. Deep learning is a type of machine learning and artificial intelligence (AI) that imitates the way humans gain certain types of knowledge. Neural Networks are an example of deep learning and are inspired by how the human brain works as they mimic the way neurons signal. 
<!--Image-->
![mainImage](images/resnet.png "Neural Net")

Neural Nets create an adaptive system that computers use to learn from their mistakes and improve continuously.In a neural network you have an input layer, output layer, and a varying number of hidden layers. Through these layers a function applies weights to solve a problem.  An issue that arises in traditional Neural Networks is the vanishing or exploding gradient problem, the training and test errors increasing the deeper you go in your network. Residual Neural Networks (RNNs) solve this issue using skip connections to create residual blocks . This changes how the network is mapped and allowing the model to skip a layer if it hurts the performance.
<!--Image-->
![mainImage](images/Residual-Block.png "Residual Block")

A lot of times in computer science, neural networks are thought of as a black box, where the actual inner-workings are not the main focus. However, since we are mathematicians, we want to understand how the network functions in order to best optimize it. For this reason, we first wanted to look at why and how ODEs were first used in neural networks. Ordinary differential equations were first used in Residual Neural Networks due to the similarity between the forward propagation equation and discretization of an ordinary differential equation. The only difference is multiplication of the step size, which we denote as $\mathbf{h}$. 
$$Y_{j+1} = Y_j + \mathbf{h}\sigma(Y_j  K_j + b_j)$$
In the context of our residual neural network, the ODE as forward propagation means that for each layer of the network, we will move one time step forward in the discretization of our network ODE. The weights and biases, $K$ and $b$, may be changed in between the layers depending on the given values in the network ODE. The final outputs are additional coordinates that match new time data that would fit the overarching dynamics of the original system. An ODE for forward propagation has many benefits for continuous transformations and was used to develop the concept of Hamiltonian Inspired Neural Networks.

When estimating coordinates of a Hamiltonian system or the value of the Hamiltonian itself, a Hamiltonian ODE should be used for forward propagation. Hamiltonians have energy conservation intrinsically built in them, which means there is less potential for error buildup when training in these examples. In many studies (cite), they have found that by using the Hamiltonian, error has decreased. We plan to investigate this further and find which discretization methods and algorithms will perform the best.





## Materials and Methods

We constructed two Residual Neural Networks and three Hamiltonian Neural Networks using three different discretization methods as forward propagation methods and utilizing the PyTorch package. Our initial ResNet was built using forward Euler as the forward propagation method, with our activation function $\sigma$ being the antiderivative of $tanh$. This method uses the current steps position to find the future step's. We used $$Y_{j+1} = Y_j + \mathbf{h}\sigma(Y_j  K_j + b_j)$$ in our ResNet for this method.

We then implemented the fourth order Runge-Kutta method (RK4) in a ResNet. This method
finds four different slopes based on the current and next positions and times, then calculates
the weighted average of those slopes and uses Euler's method to find the future position. It
is three orders of magnitude more accurate than Euler's method. We used the following as our 
implementation of the RK4 method in our ResNet
$$Y_{j+1} = Y_j + \frac{h}{6}(k_1 + 2k_2 + 2k_3 + k_4)$$
$$ k_1 = h * \sigma(y), k_2 = h * \sigma(y + h*\frac{k_1}{2})$$
$$ k_2 = h * \sigma(y + h * \frac{k_2}{2}), k_3 = h * \sigma(y + h * k_3)$$


After implementing those methods in our ResNets, we decided to move to our first Hamiltonian Inspired Neural Network, beginning with RK4 as our forward propagation method. Once we had our HINN working, we decided to implement the Verlet method. We believed the Verlet method would work the best for our second order Hamiltonians because the Verlet method is symplectic and also second order.
We used the following as our implementation of the Verlet method in our HINNs:
$$z_{j + \frac{1}{2}} = z_{j - \frac{1}{2}} - h\sigma(K_j^T y_j + b_j)$$ 
$$y_{j+1} = y_j + h\sigma(K_j z_{j + \frac{1}{2}} + b_j)$$

In our ResNets and HINNs with their respective discretization methods, we had our network learn the y and z values for our Hamiltonian ODEs from time data. To train our Neural Networks to output y and z data for our times, we input $t$, $y$, and $z$ and used one of our discretization methods for our forward propagation. When testing, we need only to input $t$ and initial values for $y$ and $z$ to be able to learn the ODE and give a prediction on some future time steps.


Since all of us love math, we wanted to do more than just calculate the coordinates at any given time step, but also calculate the value of the Hamiltonian. To do this, we created a new Hamiltonian Inspired Neural Network with the hess Quik package. The network inputs time and two coordinates, $y$ and $z$, and outputs the value of the Hamiltonian. This was built by using our Hamiltonian inspired forward propagation that was already implemented, with both RK4 and Verlet methods. The back propagation used the autograd feature to calculate both $\frac{\partial H}{\partial z}$ and $\frac{\partial H}{\partial y}$. The property of a Hamiltonian in \eqref{eq:13} was then written as a system of first order ODEs with the value calculated for the partials on the right side. Verlet method was implemented to predict the $y$ and $z$ values at different time steps to then be compared to the given $y$ and $z$ values with the loss equation, where $\theta$ is the value approximated by our network and $t$ is the true value \eqref{eq:14}. This system will now be able input a time and two initial coordinates, $y_0$ and $z_0$, and approximate the Hamiltonian value at the given time point.


Talk about SINDy and using the PySINDy package.

PySINDy package
->Description of what you input, what it does, how it is more interpretable 
->Discuss what types of equations we used most? (whenever we get there)


## Comparison
Compare different methods to ode stuff

## Information about Us
Mathias Heider is a rising senior at the University of Delaware, majoring in 

Carrie Vanty is a rising senior at Middlebury College, majoring in mathematics. She loves working with ordinary differential equations in applied math. Outside of school, Carrie likes to ski, hike, and craft.

Emma Hayes is a rising junior at Carnegie Mellon University, majoring in Computational and Applied Mathematics. She enjoys learning about new topics in mathematics and incorporating computer science into her work. Outside of class, Emma likes hiking, baking, and making art.

## References
