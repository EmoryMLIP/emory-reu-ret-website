---
title: 'Accurately Classifying Out-Of-Distribution Data in Facial Recognition'
date: 2023-12-01
featured: true
weight : 20
summary: 'Standard classification theory assumes that the input distributions of the test and the training sets are identical. In reality, classifiers are often applied to unseen data (out-of-distribution data) that is different from the training data distribution (in-distribution data). Therefore, building a trust-worthy machine learning system is important, for example, in criminal justice applications, where facial recognition for decision-making is highly consequential.  Our project focuses on developing a neural network that differentiates data from different distributions. We are interested in the following question: Can we improve the performance of the neural network on out-of-distribution data by using multiple in-distribution datasets during training? We approach this problem using the Outlier Exposure Model and investigate how the performance of the model changes when other datasets of facial images are used.'
tags: ["Summer 2023"]
authors: [nyang]
---
<!-- https://docs.google.com/document/d/1u7_vNpwToqwOdBlpbuRNXYDAMrgsaymMO8iSxA8UqNw/edit -->


This blog post was written by Gianluca Barone, Aashirit Cunchala, and Rudy Nunez and published with minor edits. The team was advised by  [Nicole Yang](https://nicoletyang.github.io/). In addition to this post, the team gave a midterm presentation, made a poster blitz video, wrote a paper, and won the best poster award for their [poster](content/2023-OOD-Poster.pdf).

## Introduction

As facial recognition technology is deployed at large scales, it is crucial to ensure its fairness. A fair model has approximately equal performance in all different classes. However, models are often unfair due to bias, which can occur for several reasons, such as having an unbalanced training set. One common assumption in machine learning is that the training and test images are from the same distribution, but in real-world applications, that is often not the case; for example, if a model is trained on an imbalanced training set, it may not do well on a balanced set. Due to this, the minority class can be overpowered by the majority class. 

The core goal of this project is to increase a model’s fairness when encountering images outside of the training distribution. Such 
out-of-distribution (OOD) images belong to a distribution different from the one the model was trained on. We used two different face datasets to have different distributions: our training dataset was UTKFace, an imbalanced dataset of 20,000 images, and our testing dataset was FairFace, a balanced dataset of 100,000 images. 

## Outlier Exposure  
One approach to making a model more familiar with out-of-distribution data is through [outlier exposure](https://arxiv.org/abs/1812.04606). In outlier exposure, a model is exposed to both in-distribution and out-of-distribution data during training stages. When it encounters the OOD data during testing, it is more likely to classify it accurately. To do this, we attempted to collect the furthest OOD images from each dataset. One approach to finding these images was using Kullback–Leibler (KL) divergence based on pixels. KL divergence measures the distance between two different distributions. Using this, we found the images with the largest KL distance, which means they are the furthest from the distribution.

In outlier exposure, the loss function is modified to include an additional term. In this term, there is a parameter lambda that scales the significance of the other term, which we were able to train to find an optimal lambda. We used the KL divergence to relate the loss function to the distance between distributions.

Using the KL score, we have noticed that UTKFace and Fairface have quite similar distributions due to the low KL score. Due to this, outlier exposure may not be as effective since it does better when the distributions are more dissimilar. To rectify this, we increased the training set by combining UTKFace with 20% of outliers from FairFace. We found these outliers by collecting the 20% of images that are the furthest from the mean distribution of  FairFace chosen through KL divergence. 


## Main Results
We observe that the accuracy and other metrics of the model can be improved by applying Outlier Exposure, incorporating a trainable weight parameter to increase the model's emphasis on outlier images, and by re-weighting the importance of different class labels. 
Some items of future work include using feature norms of the images and other outputs of the CNN to sort the
images and improve classification. Further, one may adapt the activation features code into the outlier exposure code to see if it is
more accurate than using the KL divergence based on pixels.

## Reflection

This project taught us much about neural networks and how to improve facial recognition models. We also learned more about writing manuscripts and doing research.  We plan on continuing our work on this project and exploring the possibility of using image features and additional weight parameters to classify out-of-distribution data.


## Interested in Learning More?
Please see our award-winning [poster](content/2023-OOD-Poster.pdf).
