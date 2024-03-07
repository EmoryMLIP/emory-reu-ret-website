---
# Files in this folder represent a Widget Page
type: blank
weight : 40
columns : 2
title : Projects
draft: false
---

## Enhancing Variational Autoencoders with Flexible Conditional Normalizing Flows

Mentor: [Deepanshu Verma](https://dpnshvrm.github.io/)

In [deep generative modeling](https://www.math.emory.edu/~lruthot/workshops/dgm/), one trains a neural network with many hidden layers to map a tractable low-dimensional latent distribution to an intractable target distribution represented by samples. Variational autoencoders (VAE) are one of the main frameworks for training image generators. Compared to other  GANs and diffusion models, VAEs are generally easier to train to a reasonable accuracy, but the generated images are often not as photorealistic.  We seek to explore and overcome this limitation by leveraging recent advances for estimating conditional distributions. This project investigates if a more accurate posterior approximation via normalizing flows improves the quality of the generated images. 


## Optimizing Image Acquisition with Generative Models 

Mentor: [Nicole Yang](https://nicoletyang.github.io/)

Reconstructing images from noisy and indirect measurements is an ill-posed inverse problem critical for many medical and geophysical imaging applications. Improving the measurement process by finding the best measurements to take is often desirable and possible. In many applications, slight improvements in the information content in the measurements or small reductions in the measurement costs can lead to significant outcomes. Optimizing the image acquisition usually leads to difficult or intractable problems. As a possibly simpler approach, this project investigates the potential of generative models to learn the best measurement process from examples.


## Efficient Processing of Image Sequences with Krylov Subspace Recycling

Mentor: [Lucas Onisk](https://sites.google.com/view/lucas-onisk/home)
 
Learning underlying images from noisy and blurry observations leads to large-scale linear least squares problems that are challenging to solve because of their size and ill-posedness. The associated least squares problem cannot be solved directly, even for a moderately sized image. As such, iterative methods are the preferred solvers as they can also address the ill-posedness of the problem. However, applying iterative methods frame-by-frame to image sequences is inefficient, especially when both the spatial and the temporal resolution is high, as is desired, for example, in dynamic magnetic resonance imaging (MRI) or computer tomography (CT). This project aims to develop accelerated iterative reconstruction methods for linear discrete ill-posed problems stemming from sequences of images through a combination of Krylov subspace methods and recycling strategies.

## Bridging Neural ODEs and Image Registration

Mentor: [Lars Ruthotto](https://www.math.emory.edu/~lruthot/)

Given two or more images, [image registration](https://epubs.siam.org/doi/pdf/10.1137/1.9780898718843.fm) aims to find transformations that align corresponding features in those images. This is an ill-posed problem since it is usually impossible to find a unique mapping.  Image registration is commonly phrased as a nonlinear optimization problem that seeks to minimize the distance between a reference image and the transformed template image subject to some regularization that encodes prior knowledge about the transformation. We will develop new numerical algorithms for efficiently solving large-scale instances of the nonlinear optimization problem by leveraging advances from 
 stochastic optimization and [neural ODEs](https://arxiv.org/abs/1806.07366). 
 
 ## Estimating the Latent Dimension of Data

Mentor: Mikhail Lepilov

It has been observed in a multitude of settings that distributions of “real-world” data observed in a high-dimensional space, such as the set of handwritten digits or the set of images of a rubber ducky, may often be approximated extremely well by another, latent distribution in a lower-dimensional space. Various generative models attempt to fit a latent distribution to a given set of data, which is assumed to be a set of i.i.d. samples from the high-dimensional distribution. Variational autoencoders (VAEs) comprise one popular approach of obtaining such a model by restricting the choice of latent distribution and using an empirical version of KL divergence as the measure of goodness of fit. A key step in this approach involves using a neural network to take values from the latent distribution to the parameters of the large distribution.  Despite the popularity of VAEs, however, relatively little theory is available to help choose the dimension of the latent distribution. The modeling process may thus be inefficient due to a poor initial choice of latent dimension, which would then require a whole new set of computations. In this project, we will address this inefficiency by finding a priori estimates for the dimension of the latent space from the starting data.