---
title: 'Fast & Fair: Efficient Training of Fair Neural Networks'
date: 2023-12-01
featured: true
weight : 20
summary: 'This project explores adversarial training techniques to develop fairer Deep Neural Networks (DNNs) to mitigate the inherent bias they are known to exhibit. DNNs are susceptible to inheriting bias with respect to sensitive attributes such as race and gender, which can lead to life-altering outcomes (e.g., demographic bias in facial recognition software used to arrest a suspect). We propose a robust optimization problem to improve fairness in DNNs, and leveraging second-order information, we can efficiently find a solution.'
tags: ["Summer 2023"]
authors: [enewman]
---
<!-- https://docs.google.com/document/d/1aIJEDrfuTmHEsgWYf9xfC-uX9ub8IPgOiKTmKlBMgck/edit#heading=h.dou3952sp91t -->

This blog post was written by Allen Minch, Hung Anh Vu, and Annie Warren and published after some minor edits. The team was advised by  [Dr. Elizabeth Newman](../author/elizabeth-newman/). More information about this project can be found in our paper, [poster blitz video](https://youtu.be/7J0WmeorOF8), and [poster](content/2023-Fast-And-Fair-Poster.pdf).

## (Un)Fairness in Machine Learning

Our project focuses on a key problem in machine learning: unfairness. How do we define unfairness, and where does it come from? 

Classifiers in machine learning, such as deep neural networks, can be very good at classifying complex data, such as images. However, machine learning classifiers trained through supervised learning are designed to minimize the average classification error in the data they are trained on. This means they are inherently designed to be very “faithful” to the data they are trained on and to reflect patterns and correlations in that data. This can be a problem when such correlations involve a sensitive attribute  - for instance, a correlation of a person’s race with an attribute we believe should not be related to race. 

Suppose the real-world data set that a machine learning classifier is trained on is biased with respect to some sensitive attribute, like race. In that case, the classifier will, in trying to maximize its accuracy on the data it is being trained on, be “faithful” to the bias that it is given and be trained to make predictions that reflect this bias. While it could be fairly stated that these biased predictions are not the fault of the machine learning algorithm itself but the data on which it is trained, that doesn’t change the fact that, as a society, we would generally view it as unfair to base real-world decisions on using a machine learning classifier that makes biased predictions. This is especially true when the stakes are high, where a biased classifier prediction could mean someone getting unfairly arrested, unfairly not being hired for a job, or unfairly being denied a loan. It is thus in our interests as a society to be careful about using machine learning classifiers that might be biased in their predictions and try to tweak how they are trained to reduce this unfairness.


## Improving Fairness Through Adversarial Training

We develop efficient adversarial training techniques to reduce the unfairness of classifiers in machine learning in the context of a sensitive attribute like race. In our project, we are dealing with supervised machine learning, where a classifier is trained on a dataset with many samples of input features and a corresponding true label. Because the context is supervised, we have true labels as information to help us evaluate the classifier's performance. To assess our success in improving the fairness of a classifier, we need to have fairness metrics by which to evaluate a classifier. 

Why would we think that adversarial training would help improve fairness? There are a couple of lenses for understanding why we might expect this to improve fairness. One lens has to do with the idea of overfitting. Intuitively, a primary reason we expect a classifier to be unfair is that it is overfitting to the bias in the particular data it is trained on. Adversarial training, by nature, tries to combat overfitting to the training data with its efforts to make a classifier more robust by giving perturbations to the training data points. Thus, we might expect combating overfitting with adversarial training also to combat unfairness, making the classifier less sensitive to bias in the given data. A second lens is that intuitively, a situation we would tend to view as most flagrantly unfair is when two individuals are quite similar yet happen to be part of different sensitive groups and turn out to be classified differently by a classifier. Perhaps some unfairness we observe in a classifier manifests in this kind of scenario. If we can make our classifier more robust - so that two nearby points are more likely to be classified the same way - perhaps this kind of unfairness could be reduced, which could minimize the unfairness of our classifier overall. Since adversarial training improves robustness, this would be another lens to understand why we might expect adversarial training to improve fairness.

We develop a second-order optimization method for solving the adversarial training problem. When solving an optimization problem, first-order methods are used when we only need to compute the gradient. This means we rely solely on first-order information to optimize our function. In the unconstrained case, we can take a step as large as necessary in the direction of the gradient for maximal increase/decrease. However, for our approach, we must satisfy a constraint requiring us to project our solution onto the constraint set. Computing the gradient and projecting the solution can become very computationally expensive. Therefore, with some mathematical speculation, we could utilize second-order information (computing the Hessian) to solve the optimization problem more efficiently. 

## Evaluating Fairness

We used multiple metrics for evaluating fairness with respect to sensitive attributes. To describe these intuitively, imagine that we had a dataset of individuals whose race is either white or non-white and with true labels as to whether or not they have committed a crime in the past. Suppose we used this data to train a classifier designed to predict whether or not an individual will commit a crime in the future and then used a test dataset to see how the classifier performs.

- **Independence** This means that the prediction of our classifier is uncorrelated with the sensitive attribute; a positive prediction is equally likely for all groups. In our example, independence being satisfied in a test dataset would mean that if 15% of white individuals in the dataset are predicted to commit a crime in the future, then 15% of non-white individuals are also. (Note: Y represents the true label, Y_hat the predicted label, and S the sensitive attribute in the graphic below. The graphic shows two probabilities that would have to be equal for independence to be satisfied).
- **Separation**   This means that the prediction of our classifier is conditionally independent of the sensitive attribute, given an individual’s true label.
- **Sufficiency**:  This means that our classifier’s predictive usefulness is equal across sensitive groups. If sufficiency is satisfied, then for each $(x, y)$, the probability that an individual’s true label is $x$ given the value of their predicted label is $y$ is the same across sensitive groups. 

We implemented these fairness metrics in Python with PyTorch tensors. We worked with binary classification and sensitive attributes in our project, which meant that being given PyTorch tensors containing each individual’s sensitive attribute, true label, and predicted label respectively, we could obtain the proportions needed for evaluating our fairness metrics leveraging some boolean indexing tricks.

## Coding Strategies and Main Findings

Our adversarial training problem consists of two optimization problems: an inner one and an outer one. The outer optimization problem is the typical machine learning problem of finding optimal classifier parameters. The inner optimization problem consists of, for each point in the training data set, finding a perturbation to that point within some radius that maximizes the value of the loss function. In practice, to computationally solve a two-layered optimization problem like this, the approach we take is to solve the inner optimization problem at each point, update parameters in the outer optimization problem based on these solutions, solve the inner optimization problem again, and continue going back and forth between the two problems. 

As it turns out, robust training, because it requires solving the inner optimization problem at every training data point in every epoch of the outer optimization problem, can be pretty slow computationally compared to simply doing non-robust training. Thus, as the FastNFair team, we focused on solving the inner optimization problem as quickly and efficiently as possible. 

Our numerical results on three datasets show that our method is more efficient than first-order methods.
We also observe that adversarial training can improve fairness but potentially at the cost of accuracy.
If robust training with a certain radius improves fairness, it appears to
improve fairness by larger margins than random perturbation; solving
the optimization problem well is worthwhile.

## Interested in Learning More?
Please see our [poster](content/2023-Fast-And-Fair-Poster.pdf).
