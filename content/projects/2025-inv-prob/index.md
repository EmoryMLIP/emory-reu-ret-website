---
title: 'Uncertainty Quantification of Optimal Control in Ecological Systems'
date: 2025-07-25
featured: true
weight: 20
summary: 'A Bayesian framework for propagating uncertainty from data through reconstruction into optimal control of dynamical systems.'
tags: ["Summer 2025"]
# authors: [jdarges]
---

This blog post was written by Nina Chafee (Haverford College), Micah Chandler (University of North Georgia), Benjamin Lebdaoui (University of Montevallo), and Meredith Orton (LaGrange College) and published with minor edits. The team was advised by John Darges. In addition to this post, the team has also created a [poster](./Poster.pdf), given a [midterm presentation](./Midterm_Presentation.pdf), and written a [manuscript](./Inverse%20problems%20and%20uncertainty%20quantification%20for%20the%20control%20of%20dynamical%20systems.pdf).

## The Big Idea

Real-world decisions rely on models built from noisy data. Traditional approaches often ignore the uncertainty inherent in this data when making control decisions. We propose a framework that propagates uncertainty from data through parameter reconstruction into optimal control, providing decision-makers with a more complete picture of the reliability of their control strategies.

## Problem Setup

We focus on the classic Lotka-Volterra predator-prey model, which describes the dynamics of two interacting populations:

$$\frac{dx}{dt} = \alpha x - \beta xy$$
$$\frac{dy}{dt} = \delta xy - \gamma y$$

where $x$ represents the prey population, $y$ represents the predator population, and $\alpha$, $\beta$, $\gamma$, $\delta$ are model parameters governing birth rates, death rates, and interaction effects. Our goal is to stabilize ecosystem populations using optimal control while accounting for uncertainty in the model parameters.

## Methodology

### The Inverse Problem

Given noisy observations of population dynamics, we seek to estimate the unknown model parameters. This inverse problem is ill-posed because small perturbations in the data can lead to large changes in the estimated parameters. We address this challenge using a Bayesian framework.

### Bayesian Framework and MCMC

We employ Bayesian inference to quantify uncertainty in our parameter estimates. Rather than obtaining a single point estimate, we compute the posterior distribution of parameters given the observed data:

$$p(\theta | y) \propto p(y | \theta) p(\theta)$$

where $\theta$ represents the model parameters, $y$ is the observed data, $p(y | \theta)$ is the likelihood, and $p(\theta)$ is the prior distribution.

To sample from this posterior distribution, we use Markov Chain Monte Carlo (MCMC) methods, specifically the Metropolis-Hastings algorithm. This approach generates samples that allow us to characterize the full uncertainty in our parameter estimates.

### Optimal Control

With parameter estimates in hand, we apply optimal control to stabilize the ecosystem. We explored two complementary approaches:

**Pontryagin Maximum Principle (PMP):** A classical approach that derives necessary conditions for optimality, leading to a system of differential equations that can be solved to find the optimal control.

**Pseudo-Spectral Method:** A numerical approach that discretizes the control problem and solves it as a nonlinear programming problem, providing flexibility in handling various constraints.

## Results

Our framework successfully:

1. **Estimated posterior distributions** of model parameters from noisy observation data using MCMC sampling
2. **Applied optimal control** strategies to stabilize predator-prey populations
3. **Quantified uncertainty** in the control outcomes by propagating parameter uncertainty through the control optimization

By sampling control solutions across the posterior distribution of parameters, we can provide confidence intervals on the expected system behavior under optimal control, rather than a single deterministic prediction.

## Future Work

Several directions remain for extending this work:

- **Unified optimal control:** Develop methods to find a unique optimal control based on the entire posterior distribution, rather than computing separate controls for each parameter sample
- **Higher-dimensional systems:** Apply the framework to more complex ecological models with additional species and interactions
- **Alternative dynamical systems:** Extend the methodology to other domains such as epidemiological models, climate systems, or engineering applications

## Acknowledgements

This work was conducted as part of the NSF REU Computational Mathematics for Data Science program at Emory University during Summer 2025, supported by NSF Award DMS-2349534.
