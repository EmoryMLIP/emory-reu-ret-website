---
# Files in this folder represent a Widget Page
type: blank
weight : 40
columns : 2
title : Projects
draft: false
---

## Joint Reconstruction of X-ray Ptychography and X-ray Fluorescence

Mentor: [Yuanzhe Xi](../authors/yxi/)

We propose to explore a cutting-edge framework for the simultaneous reconstruction of ptychographic imaging and fluorescence deconvolution. Our approach utilizes a unified model that integrates the distinct modalities of x-ray ptychography and x-ray fluorescence imaging. This joint model not only facilitates synergistic data utilization but also markedly enhances the resolution and quality of the resulting images. We aim to rigorously analyze the mathematical underpinnings of this framework and will also investigate the application of neural networks to develop a more effective link function that integrates both models. This research promises to make substantial contributions to the field of imaging science, particularly through the development of optimized computational methods that improve imaging precision and efficiency.


## Model-Aware and Data-Driven Inference 

Mentors: [Matthias Chung](https://sites.google.com/view/matthias-chung/home) and [Andrea Arnold](https://www.wpi.edu/people/faculty/anarnold)

Inversion techniques seek to uncover hidden information from observed data. Traditional methods, such as variational techniques, use iterative algorithms to refine estimates. While reliable, these methods can be computationally intensive and struggle with uncertainty.
On the other hand, modern data-driven machine learning methods directly learn patterns from data, offering faster solutions. However, these methods can lack physical interpretability and may not generalize well to new, unseen data.
This project aims to bridge the gap between these two approaches. By combining both strengths, we can develop more efficient and reliable algorithms. Students will explore, implement, and evaluate hybrid methods that balance computational efficiency with physical interpretability. We will investigate problems ranging from biological applications to medical imaging.



## Hybrid Regularization for Random Feature Models

Mentors: Chelsea Drum and [James Nagy](../authors/jnagy/)
 
Imagine you're trying to reconstruct a blurry image or fill in missing pieces of a puzzle. This is a common problem in many fields, such as medical imaging, computer vision, and data science. One way to solve these problems is by using data-driven machine-learning approaches. Traditional approaches can be slow and inefficient, especially when dealing with large datasets. A newer approach, called Random Feature Models (RFMs), can speed up these processes. However, RFMs can sometimes produce inaccurate results. To improve the accuracy of RFMs, researchers have developed a new technique called hybrid Krylov subspace methods. These methods are more efficient and can handle large datasets better than traditional methods. This project aims to further improve these hybrid Krylov subspace methods by making them even more efficient. By removing a step that requires complex calculations, these methods can be used on faster hardware and with lower precision, leading to even faster and more efficient machine-learning models.

## Optimal Control and Inverse Problems for Data-Driven Decision-Making

Mentors: [John Darges](https://jedarges.github.io) and [Matthias Chung](https://sites.google.com/view/matthias-chung/home)

Optimal control problems involve finding a control variable for a dynamical system that guides the system towards a desired outcome. Classically, the dynamical system in the problem is described by a system of differential equations governed by known parameters. In real-world applications, the system parameters may not be known. Finding the dynamical system requires solving an inverse problem, where we reconstruct parameters from observable data. A more complicated control problem is one where the dynamical system must be estimated from observations. These problems appear in wide-ranging contexts, including in epidemiology, where prediction models inform policy decisions, in healthcare, where treatment plans require understanding the patient's biological systems, and in environmental science, where knowledge of environmental dynamics informs pollution control. In coupling optimal control and inverse problems, it is understood how uncertainty in the observed data leads to uncertainty in our decision-making. This introduces computational and theoretical challenges that can be tackled through approximate inference and reduced-order modeling. This project aims to develop complementary methods for inverse problems and optimal control that yield effective and efficient decision-making from real-world data.
 