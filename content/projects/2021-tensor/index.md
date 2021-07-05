---
title: Tensors for fMRI
date: 2021-05-01
featured: false
tags: ["Summer 2021"]
---

<p align="center">
Understanding the human brain by extracting multidimensional information.

 
<img width="200" height="100" src="img/tensor_neuroimaging_draft1.jpg">
</p>


<!--more-->

### Overview
Advances in the neuroimaging technology of functional Magnetic Resonance Imaging (fMRI) have provided large amounts of digital data, which can be used to study the complex functionality of the human brain. A whole-brain fMRI image sample consists of a discrete-time series of 3D image scans, where each scan consists of hundreds of thousands of voxels. The size of the dataset and additional problems such as measurement noise render fMRI analysis very challenging computationally. The team will investigate the use of tensor representations to represent and analyze the fMRI data. Here, an fMRI brain image sample can be organized as a fourth-order tensor, with three space and one time dimension. This viewpoint allows for extracting information using various tensor decomposition methods.

---
### Background

A tensor is a multidimensional array of data. We denote tensors with a capital script letter $\mathcal{A} \in \mathbb{R}^{n_1\times \dots \times n_d}$.
There are many products associated with tensors including the mode-$k$ product
\begin{equation}
\mathcal{A} \times_k \mathbf{M} = \mathbf{M} \mathcal{A}_{(k)}
\end{equation}

Functional Magnetic Resonance Imaging (fMRI) gives us pictures of the brain like the following:


{{< figure src="img/brain1.jpg" caption="Regions of Interest (ROIs) for the [StarPlus fMRI data](http://www.cs.cmu.edu/afs/cs.cmu.edu/project/theo-81/www/) from Carnegie Mellon University." alt="brainROI">}}

Then we can give some more details!


