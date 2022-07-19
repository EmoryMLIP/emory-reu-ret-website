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

This post was written by Emma Hayes, Mathias Heider, and Carrie Vanty and published with minor edits. The team was advised by Dr. Deepanshu Verma.
https://mathheider.github.io/

In addition to this post, the team has also created slides for a [midterm presentation], a poster blitz video, and a poster.



## Project Overview: 
Imagine a spring mass system (Figure 1). We want to be able to find the location of the mass at any given time point. In order to find the coordinates, we must understand the dynamics of the system. In a spring mass system, energy is conserved, so we chose to use a Hamiltonian Ordinary Differential Equation, which has the quality of energy conservation. To solve our problem, we use machine learning that uses Hamiltonians in the forward propagation to predict our coordinates.

<p align="center">
<img src=images/Simple_harmonic_oscillator.gif>
<figcaption align = "center"><b>Figure 1 - Spring Mass by Oleg Alexandrov [1]</b></figcaption>

Our project aims to compute both a value for the Hamiltonian and coordinates for any given time using Hamiltonian Inspired Neural Networks. We will then compare our results to Sparse Identification of Nonlinear Dynamics ([4], [5]) to assess efficiency and accuracy. In order to build our neural network, we must first understand the background of machine learning. Then, we will discuss the mathematics behind our network, including differential equations and discretization choice. Results will then be presented and analyzed.



## Background: 
In this project we heavily rely on machine learning, specifically deep learning. Machine Learning is the use of statistical learning and optimization methods that let computers analyze datasets and identify patterns. Deep learning is a type of machine learning and artificial intelligence (AI) that imitates the way humans gain certain types of knowledge. Neural Networks are an example of deep learning and are inspired by how the human brain works as they mimic the way neurons signal. 

<p align="center">
<img src=images/resnet.png width="370" height="300"  class="aligncenter"/>
<figcaption align = "center"><b>Figure 2 - Neural Net by Carrie Vanty </b></figcaption>

Neural Nets create an adaptive system that computers use to learn from their mistakes and improve continuously.In a neural network you have an input layer, output layer, and a varying number of hidden layers. Through these layers a function applies weights to solve a problem.  An issue that arises in traditional Neural Networks is the vanishing or exploding gradient problem, the training and test errors increasing the deeper you go in your network. Residual Neural Networks (RNNs) use skip connections to create residual blocks which can help with this issue. This changes how the network is mapped and allowing the model to skip a layer if it hurts the performance.

<p align="center">
<img src=images/Residual-Block.png class="align center">
<figcaption align = "center"><b>Figure 3 - Residual Block [2] </b></figcaption>

A lot of times in computer science, neural networks are thought of as a black box, where the actual inner-workings are not the main focus. However, since we are mathematicians, we want to understand how the network functions in order to best optimize it. For this reason, we first wanted to look at why and how ODEs were first used in neural networks. Ordinary differential equations were first used in Residual Neural Networks due to the similarity between the forward propagation equation and discretization of an ordinary differential equation. The only difference is multiplication of the step size, which we denote as $\mathbf{h}$. 
$$Y_{j+1} = Y_j + \mathbf{h}\sigma(Y_j  K_j + b_j)$$
In the context of our residual neural network, the ODE as forward propagation means that for each layer of the network, we will move one time step forward in the discretization of our network ODE. The weights and biases, $K$ and $b$, may be changed in between the layers depending on the given values in the network ODE. The final outputs are additional coordinates that match new time data that would fit the overarching dynamics of the original system. An ODE for forward propagation has many benefits for continuous transformations and was used to develop the concept of Hamiltonian Inspired Neural Networks.

When estimating coordinates of a Hamiltonian system or the value of the Hamiltonian itself, a Hamiltonian ODE should be used for forward propagation. Hamiltonians have energy conservation intrinsically built in them, which means there is less potential for error buildup when training in these examples. In many studies ([6], [3]), they have found that by using the Hamiltonian, error has decreased. We plan to investigate this further and find which discretization methods and algorithms will perform the best.





##Learning Hamiltonians from Data

To learn about Hamiltonian dynamics from data, we use neural networks. Specifically a modified version of the Residual Neural Network (RNN), which we call a Hamiltonian Inspired Neural Network (HINN) drawn from CITE. To create this HINN, we primarily used 2 packages - PyTorch and hessQuik. The difference between our HINN, and the traditional RNN and Lars’ HINN, is in our forward propagation method and how we input values into our MSE loss function. The forward propagation uses the autograd feature to calculate both $\frac{\partial \mathcal{H}_{\theta}}{\partial  \mathbf{p}}$ and $\frac{\partial \mathcal{H}_{\theta}}{\partial \mathbf{q}}$, where $\theta$ are the network parameters we wish to optimize and $\mathcal{H}_{\theta}$ is our network output. We then use these values in discretizing $\mathbf{p_{\theta}}$ and $\mathbf{q_{\theta}}$.
\begin{equation}
    \mathbf{p}_{\theta+1} = \mathbf{p}_{\theta} + h\frac{\partial \mathcal{H}_{\theta}}{\partial \mathbf{q}} \label{eq:6}
\end{equation}
\begin{equation*}
    \mathbf{q}_{\theta+1} = \mathbf{q}_\theta - h\frac{\partial \mathcal{H}_{\theta}}{\partial \mathbf{p}}
\end{equation*}
The new values are then plugged into our MSE loss function. Using these techniques we created two HINNs for two different examples, those being the Simple Spring Mass System and the Two Body Problem. https://github.com/mathheider/Learn-ODEs-HINNs


##Results
  <p align="center">
  <img src=findingNemo (3).png class="align center">
  <figcaption align = "center"><b>Figure 2 - Spring Mass System [2] </b></figcaption>

  <p align="center">
  <img src=2 body final (1).png class="align center">
  <figcaption align = "center"><b>Figure 3 - Two Body Problem [2] </b></figcaption>



## Comparison

## Information about Us
Mathias Heider is a rising senior at the University of Delaware, majoring in Computer Science and Mathematics and Economics. His interest are in machine learning and data science specifically when it relates to dataset with bioinformatics applications. Outside of class, Mathias likes to ski, hangout with friends, and play video games

Carrie Vanty is a rising senior at Middlebury College, majoring in mathematics. She loves working with ordinary differential equations in applied math. Outside of school, Carrie likes to ski, hike, and craft.

Emma Hayes is a rising junior at Carnegie Mellon University, majoring in Computational and Applied Mathematics. She enjoys learning about new topics in mathematics and incorporating computer science into her work. Outside of class, Emma likes hiking, baking, and making art.

## References
[1] https://en.wikipedia.org/wiki/Effective_mass_(spring%E2%80%93mass_system)#/media/File:Simple_harmonic_oscillator.gif

[2] [Kaiming He, X. Zhang, Shaoqing Ren, and Jian Sun. Deep residual learning for image recognition. 2016 IEEE Conference on Computer Vision and Pattern Recognition (CVPR), pages 770–778, 2016.](https://arxiv.org/abs/1512.03385)

[3] [Eldad Haber and Lars Ruthotto. Stable architectures for deep neural networks. Inverse Problems, 34(1):014004, 22, 2018.](https://arxiv.org/abs/1705.03341)

[4] [Brian de Silva, Kathleen Champion, Markus Quade, Jean-Christophe Loiseau, J. Kutz, and Steven Brunton. Pysindy: A python package for the sparse identification of nonlinear dynamical systems from data. Journal of Open Source Software, 5(49):2104, 2020.](https://doi.org/10.21105/joss.02104)

[5] [Alan A. Kaptanoglu, Brian M. de Silva, Urban Fasel, Kadierdan Kaheman, Andy J. Goldschmidt, Jared Callaham, Charles B. Delahunt, Zachary G. Nicolaou, Kathleen Champion, Jean-Christophe Loiseau, J. Nathan Kutz, and Steven L. Brunton. Pysindy: A comprehensive python package for robust sparse system identification. Journal of Open Source Software, 7(69):3994, 2022.](https://doi.org/10.21105/joss.03994)

[6] [Sam Greydanus, Misko Dzamba, and Jason Yosinski. Hamiltonian neural networks. ArXiv, abs/1906.01563, 2019.](https://arxiv.org/abs/1906.01563)
