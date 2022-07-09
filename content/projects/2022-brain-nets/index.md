---
title: 'Shallow vs. Deep Brain Network Models for Mental Disorder Analysis'
date: 2022-06-27T11:36:49-04:00
lastmod: 2022-06-27T11:36:49-04:00
featured: true
weight : 100
summary: 'Orchestrating behavior and cognition, human brains lie at the core of complex neurobiological systems. Understanding of the structures, functions and mechanisms inside the brains has been an intriguing pursuit throughout human history. Recent studies in neuroscience and brain imaging have reached the consensus that the interactions among brain regions are driving factors for neural development and disorders, but there has not been an understanding in what mathematical models should be used to analyze such interactions, a.k.a the brain networks. In this project, we will explore and analyze different approaches for the modeling of brain networks, especially ranging from traditional shallow graph models to modern deep graph neural networks, towards the analysis of mental disorders, such as PTSD, depression and substance misuse. We will adapt different graph mining techniques for brain networks, statistically and visually analyze the results, and quantitatively evaluate them in the standard graph classification setting.'
tags: ["Summer 2022"]
---
## Overview: Comparing Shallow vs. Deep Brain Network Models

We are comparing and benchmarking the performance of graph kernels and graph neural networks applied to disease classification based on neuroimaging data.
For useful background and definitions refer to the [definitions](#definitions) section.


## Datasets

We are working with 2 datasets: one classifying human immunodeficiency virus (HIV) and one classifying bipolar disorder (BP). Each dataset consists of functional magnetic resonance imaging (fMRI) scans, diffusion tensor imaging (DTI) scans, and classification labels in the form of integers, where 1 indicates a healthy patient and -1 indicates an unhealthy patient. Both datasets have been processed for us, as detailed in [section 3](https://arxiv.org/abs/2204.07054) of the paper authored by Cui et al. 

## Problem Formulation
The DTI and FMRI brain scans of each patient $i$ are represented as weighted adjacency matrices $\mathbf{W}_i \in \mathbb{R}^{M \times M}$. FMRI scans are considered to be more robust than DTI scans, so our experiments prioritize working with them. Nodes in the brain network represent regions of interest (ROI), and edge links between nodes indicate the strength of the connection between the two regions.

### Classification Task

The standard graph classification task considers the problem of classifying graphs into two or more categories. The goal is to learn a model that maps graphs in the set of graphs $G$ to a set of labels $Y$. In this project, we aim to accurately classify patients into either diseased or healthy based on graphs constructed from their brain scan data.

### Implementation

For implementation of support vector machines (SVM) with graph kernels, we utilized threshold rounding to remove edge weights and sparsify the adjacency matrices. While this results in information loss, it preserves the overall structure of the adjacency matrices and makes them usable for this particular classification method. Further manipulation creates a list of graph objects that are compatible with the Python package [GraKel](https://ysig.github.io/GraKeL/0.1a8/). 

For implementation of graph convolutional networks (GCN's), we followed [BrainGB](https://github.com/HennyJie/BrainGB)'s code to create a data type that can be used with the Python package [PyG](https://pytorch-geometric.readthedocs.io/en/latest/).

## Methods

### 1. Graph Kernels

<img src="img/SVC.png" alt="SVC" width="1000"/>
<figcaption align = "center"><b>Fig.1 - Support Vector Machines with Kernels</b></figcaption>
<br/>

For SVM, we computed three kernels: Weisfeiler-Lehman (WL), Weisfeiler-Lehman Optimal Assignment (WLOA), and propagation (Prop). The choice of these kernels is motivated by exploiting structural information (i.e., subgraphs) in the brain networks.

### 2. Graph Convolutional Networks (GCN's)

<img src="img/BrainGB_final.png" alt="BrainGB" width="1000"/>
<figcaption align = "center"><b>Fig.2 - BrainGB Framework</b></figcaption>
<br/>

### 3. Merging Graph Kernels and GNN's

<img src="img/GKNN.png" alt="Graph Kernel GNN" width="1000"/>
<figcaption align = "center"><b>Fig.3 - Example Architecture of Graph Kernel GNN</b></figcaption>
<br/>

To leverage the higher order structural information given by graph kernels and local information given by GCN's, we implemented GNN's that incorporated various graph kernels (WL, WLOA, etc.) and benchmarked their performance on our dataset.

## Benchmarks

### BrainGB Classification Accuracy (Test Set)

| Dataset   | Accuracy            | F1                  | AUC                 |
|-----------|---------------------|---------------------|---------------------|
| HIV-GCN (concat)      | $0.64_{\pm 0.15}$ | $0.59_{\pm 0.20}$ | $0.77_{\pm 0.20}$ |
| BP-GCN (concat)       | $0.53_{\pm 0.13}$ | $0.51_{\pm 0.14}$  | $0.54_{\pm 0.16}$ |
| HIV-GAT (concat)      | $0.73_{\pm 0.16}$ | $0.71_{\pm 0.17}$ | $0.81_{\pm 0.19}$ |
| BP-GAT (concat)       | $0.53_{\pm 0.13}$  | $0.50_{\pm 0.13}$  | $0.57_{\pm 0.19}$  |
| HIV-GCN (edge concat) | $0.71_{\pm 0.11}$ | $0.69_{\pm 0.12}$ | $0.77_{\pm 0.17}$ |
| BP-GCN (edge concat)  | $0.63_{\pm 0.12}$ | $0.61_{\pm 0.13}$  | $0.61_{\pm 0.17}$ |
| HIV-GAT (edge concat) | $0.69_{\pm 0.18}$ | $0.67_{\pm 0.19}$ | $0.73_{\pm 0.24}$ |
| BP-GAT (edge concat)  | $0.52_{\pm 0.17}$  | $0.51_{\pm 0.16}$  | $0.59_{\pm 0.19}$  |

Both HIV and BP datasets were tested using GCN and GAT as labeled in the table. "Concat" and "edge concat" denote the message passing mechanism that was used in the experiment.

<br/>


### SVC Classification Accuracy (Test Set)

| Dataset         | Threshold = 0.5     | Optimal Threshold*  | 
|-----------------|---------------------|---------------------|
| HIV-WL (0.2*)   | $0.59_{\pm 0.18}$   | $0.65_{\pm 0.17}$   |
| BP-WL (0.4*)    | $0.53_{\pm 0.14}$   | $0.63_{\pm 0.19}$   |
| HIV-WLOA (0.2*) | $0.59_{\pm 0.18}$   | $0.64_{\pm 0.15}$   |
| BP-WLOA (0.4*)  | $0.54_{\pm 0.15}$   | $0.63_{\pm 0.18}$   |
| HIV-Prop (0.2*) | $0.59_{\pm 0.18}$   | $0.65_{\pm 0.17}$   |
| BP-Prop (0.4*)  | $0.54_{\pm 0.13}$   | $0.60_{\pm 0.17}$   |
<br/>

### Kernel Parameter Tests

<p float="center">
  <img src="img/WL-kernel-performance.png" width="330" /> 
  <img src="img/WLOA-kernel-performance.png" width="330" />
  <img src="img/propagation-kernel-performance.png" width="330" />
</p>

## Limitations and Discussion

Limitations: data set size, lack of specific understanding of intermediate steps in machine learning processes such as neural networks, extremely limited patient data (size and characteristics) prevents certain controls being implemented and also prevents examining cross-correlations between potential confounding variables, so we have no way of knowing that our model is actually measuring what it is supposed to be measuring other than classification accuracy percentage, which is only locally relevant and may not be generalizable.

Discussion: future research and improvements to study design

## Definitions

For technical details of implementing support vector classifiers (SVC) using the Python package [sklearn](https://scikit-learn.org/stable/), see this [link](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html).

For the mathematical theory underlying SVC, see this [blog post](https://towardsdatascience.com/support-vector-machine-introduction-to-machine-learning-algorithms-934a444fca47).

For an introduction to graph neural networks (GNN's), see this [blog post](https://distill.pub/2021/gnn-intro/).

## References

[BrainGB: A Benchmark for Brain Network Analysis with Graph Neural Networks](https://arxiv.org/abs/2204.07054)

[BrainNNExplainer: An Interpretable Graph Neural Network Framework for Brain Network based Disease Analysis](https://arxiv.org/abs/2107.05097)

[Deep Graph Kernels](https://dl.acm.org/doi/abs/10.1145/2783258.2783417)

[Graph Kernel Neural Networks](https://arxiv.org/abs/2112.07436)

[KerGNNs: Interpretable Graph Neural Networks with Graph Kernels](https://www.aaai.org/AAAI22Papers/AAAI-6564.FengA.pdf)