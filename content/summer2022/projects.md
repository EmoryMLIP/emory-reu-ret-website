---
# Files in this folder represent a Widget Page
type: blank
weight : 21
columns : 2
title : Projects
---

## Uncertainty Quantification for Ozone Forecasting  

Mentor: [Bree Ettinger](../author/bree-ettinger/)

Ground level ozone is a harmful air pollutant. Predicting low-level ozone can inform air quality forecasts and help people determine which outside activities are safe. Functional linear regression models have recently shown their ability to predict low levels of ozone. In this project, we will study functional models based on bivariate splines over triangulation to approximate the spatially distributed ozone measurements on a surface.  We will focus not just on computing a forecast but also on quantifying the uncertainty associated with our predictions. 

## Data assimilation for Hurricane Storm Surge Modeling 

Mentor: [Talea Mayo](../author/talea-mayo/)

Numerical models of coastal hydrodynamics play a vital role in understanding hurricane storm surges, particularly as the climate changes. However, uncertainties in model parameters and their representations, e.g., bottom stress and surface wind stress, limit the confidence of model results.  Data is becoming increasingly available but also contains uncertainties. In this project we will explore methods of data assimilation, which utilize information about the uncertainties in both modeled and observed data to improve estimates of the coastal system state.

## [Fast Training of Implicit Networks with Applications in Inverse Problems](../projects/2022-implicit)

Mentor: [Samy Wu Fung](../author/samy-wu-fung/)

Implicit networks are a special type of architecture whose outputs are defined by a fixed point (or optimality) condition. To evaluate these networks, one performs an iterative process, where each iteration is considered a layer of the network. The depth of these networks often vary depending on the complexity of the input data; for instance, in natural language processing, it might take 3 iterations (or layers) to output the sentiment of a simple sentence, but it might take 100 layers for the network to output the sentiment of a complicated sentence. Unfortunately, training implicit networks efficiently typically comes at additional computational cost. This project explores fast and efficient algorithms for training implicit networks, with emphasis on their applications to inverse problems. 

## Shallow vs. Deep Brain Network Models for Mental Disorder Analysis

Mentor: [Carl Yang](../author/carl-yang/)

Orchestrating behavior and cognition, human brains lie at the core of complex neurobiological systems. Understanding of the structures, functions and mechanisms inside the brains has been an intriguing pursuit throughout human history. Recent studies in neuroscience and brain imaging have reached the consensus that the interactions among brain regions are driving factors for neural development and disorders, but there has not been an understanding in what mathematical models should be used to analyze such interactions, a.k.a the brain networks. In this project, we will explore and analyze different approaches for the modeling of brain networks, especially ranging from traditional shallow graph models to modern deep graph neural networks, towards the analysis of mental disorders, such as PTSD, depression and substance misuse. We will adapt different graph mining techniques for brain networks, statistically and visually analyze the results, and quantitatively evaluate them in the standard graph classification setting. 

## Learning Ordinary Differential Equations from Data

Mentor: [Deepanshu Verma](../author/deepanshu-verma/)

Assume you are given observations of a dynamical system at a few time points and want to learn its underlying ODE.
Problems like this are abundant in scientific applications and there are several machine learning approaches to this problem.
One approach with soaring popularity is called [Neural ODEs](https://arxiv.org/abs/1806.07366), that is, ODEs whose dynamics are trainable neural networks, which makes them very flexible.
Another approach that does not rely on neural networks and thus can yield a more interpretable result is called [sparse identification of nonlinear dynamics (SINDy)](https://www.pnas.org/content/113/15/3932). 
The goal of this project is to compare the advantages and disadvantages of both of these (and perhaps other) approaches experimentally and mathematically.
One particular aspect we will investigate is how ODE properties like stability and stiffness impact the effectiveness of the learning process. 


## Model-based approaches to neuronal network firing and its subsequent validation with a previously recorded in-vivo dataset

Mentor: [Mike Caiola](../author/mike-caiola)

The human brain sends signals using around 100 billion neurons connected in a complex and dynamic fashion. The sheer number of neurons makes the task of modeling, particularly at the network level, difficult. Instead of modeling each individual neuron, one can instead approximate the system using a series of coupled ordinary or delay differential equations. Using bifurcation theory, this approximate system can then be manipulated to mimic neuronal level changes that lead to neuronal dysfunction, disease states, and, ultimately, possible trajectories in parameter space that lead back to a healthy neuronal state. These types of models help add to the understanding of neuronal dysfunction but are pretty useless without data to validate the model. Fortunately, a rich dataset of in-vivo primate neuronal data recorded throughout various movement-related brain areas is available to help validate and corroborate findings for this project.

## Data vs. Models: Optimal Control of Ordinary Differential Equations

Mentor: [Lars Ruthotto](../author/lars-ruthotto/)

Given a computational model of some real world process in form of an ODE equation with some parameters you can control, how do you   choose the control parameters to achieve a certain goal.
For example, let's say you want to determine when to break or accelerate your car on a highway such that you minimize your travel time and also keep a safe distance.
There are ample examples of problems like this and they  be formulated and solved using the framework of optimal control.
Model-based approaches (e.g., approaches that use the ODE) have been used very successfully in a wide range of science and engineering applications. 
However, in recent years success stories like that of AlphaGo and more recently AlphaFold have demonstrated the ability of  reinforcement learning to find (almost) optimal controls using data instead of models. 
This REU project investigates the trade-off between model-based and data-driven approaches for several examples from the optimal control literature. 
To this end, we will study theoretical properties of both approaches and also perform numerical comparisons.
