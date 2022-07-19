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

This post was written by Emma Hayes, [Mathias Heider](https://mathheider.github.io/), and Carrie Vanty and published with minor edits. The team was advised by Dr. Deepanshu Verma.


In addition to this post, the team has also created slides for a [midterm presentation](pdfs/presentation.pdf), a [poster blitz video](), and a [poster](pdfs/poster.pdf).



## Project Overview: 
Imagine a spring mass system (Figure 1). What if you wanted to find the location of the mass at any given time point? In order to find this information, you must first understand the dynamics of the system. A spring mass system is an example of simple harmonic motion where total energy is conserved. This means that you can model the dynamics using a Hamiltonian Ordinary Differential Equation, which has the quality of energy conservation. To solve our problem, we use neural networks utilizing Hamiltonians in the forward propagation to predict our coordinates.

<p align="center">
<img src=images/Simple_harmonic_oscillator.gif>
<figcaption align = "center"><b>Figure 1 - Spring Mass by Oleg Alexandrov [1]</b></figcaption>

Our project aims to compute the value of the Hamiltonian for any given time and set of initial conditions using Hamiltonian Inspired neural networks. We will first introduce the mathematical background of our project and the novel technique we implemented for our forward propagation. Results will then be presented and analyzed. Lastly, we will compare our work to Greydanus et al and discuss future work.



## Background: 
Often, neural networks are thought of as a black box, where the actual inner-workings are not the main focus. However, since we are mathematicians, we want to understand how the network functions in order to best optimize it. For this reason, we began by looking at why and how ODEs were first used in neural networks. Ordinary differential equations were first used in Residual Neural Networks due to the similarity between the forward propagation equation and discretization of an ordinary differential equation. The only difference is multiplication of the step size, which we denote as $\mathbf{h}$. 
$$Y_{j+1} = Y_j + \mathbf{h}\sigma(Y_j  K_j + b_j)$$
In the context of our residual neural network, the ODE as forward propagation means that for each layer of the network, we will move one time step forward in the discretization of our network ODE. The weights and biases, $K$ and $b$, may change in between the layers depending on the given values in the network ODE. The output of our network is the Hamiltonian value at the given time, and from that we are able to approximate position and velocity values for the mass. 
When estimating coordinates of a Hamiltonian system, or the value of the Hamiltonian itself, the Hamiltonian relationships are important for forward propagation. Hamiltonians intrinsically conserve energy, meaning the network is better able to learn conservation laws and predict examples with energy conservation. Without considering these relationships, it would be much more difficult for the network to learn conservation, which can cause a buildup of error. In many studies ([3](https://arxiv.org/abs/1705.03341), [6](https://arxiv.org/abs/1906.01563)), they have found that by using the Hamiltonian equations in Hamiltonian data sets, error has decreased. We plan to investigate this further and find which discretization methods and algorithms will perform the best.





## Learning Hamiltonians from Data

To learn about Hamiltonian dynamics from data, we use neural networks. Specifically a modified version of the Residual Neural Network (RNN), which we call a Hamiltonian Inspired Neural Network (HINN) drawn from [3](https://arxiv.org/abs/1705.03341). To create this HINN, we primarily used 2 packages - PyTorch and hessQuik. The difference between our HINN, and the traditional RNN and Lars’ HINN, is in our forward propagation method and how we input values into our MSE loss function. The forward propagation uses the autograd feature to calculate both $\frac{\partial H_{\theta}}{\partial \mathbf{p}}$ and $\frac{\partial H_{\theta}}{\partial \mathbf{q}}$, where $\theta$ are the network parameters we wish to optimize and $H_{\theta}$ is our network output. We then use these values in discretizing $\mathbf{p_{\theta}}$ and $\mathbf{q_{\theta}}$.
$$\mathbf{p_{\theta+1}} = \mathbf{p_{\theta}} + h\frac{\partial H_{\theta}}{\partial \mathbf{q}} $$
$$\mathbf{q_{\theta+1}} = \mathbf{q_{\theta}} - h\frac{\partial H_{\theta}}{\partial \mathbf{p}}$$

  The new values are then plugged into our MSE loss function. Using these techniques we [created two HINNs](https://github.com/mathheider/Learn-ODEs-HINNs) for two different examples, those being the Simple Spring Mass System and the Two Body Problem. 


Results:
<p align="center">
<img src=images/findingNemo.png width = "800">
<figcaption align = "center"><b>Figure 2 - Spring Mass System [2] 1. Training Loss Graph 2. Learned Position Values over True Position Values 3. Relationship of Learned p and q over ground truth </b></figcaption>


<p align="center">
<img src=images/2Body.png width = "800">
<figcaption align = "center"><b>Figure 3 - Two Body Problem [3] 1. Training Loss Graph 2. Learned Trajectories Graph over True Trajectories 3. Learned Energy over True Energy 4. Learned Position over True Position.  </b></figcaption>






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
