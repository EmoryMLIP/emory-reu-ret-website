---
title: 'Mixed-Precision Algorithms for Image Processing'
date: 2022-06-27T11:36:49-04:00
lastmod: 2022-06-27T11:36:49-04:00
featured: true
weight : 100
summary: 'Since numbers in the computer are represented with a fixed number of bits, loss of accuracy during calculation is unavoidable. At high precision where more bits are allocated to each number, round-off errors are typically small. On the other hand, doing calculation at a lower precision has the advantage of being much faster. This research focuses on experimenting doing arithmetic at different precision levels. We would first simulate low-precision arithmetic with the Matlab function chop on basic operations such as inner product of vectors, norms, matrix- matrix multiplication, etc. Then, we would modify iterative methods in the IR tools package to make the arithmetic happen at lower precision and mixed precision, run experiments on the image processing tasks and compare their performance at different precision level.'
tags: ["Summer 2022"]
---
This post was written by [Xiaoyun Gong](https://github.com/kristinagxy), [Yizhou Chen](https://github.com/RileyCYZ), and Xiang Ji and published with minor edits. The team was advised by Dr. [James Nagy](https://github.com/jnagy1). In addition to this post, the team has also created slides for a [midterm presentation](REUmidterm_presentation.pdf
), a [poster blitz]() video, [code](), and a [paper]().

## In One Sentence:
Our group works on experimenting with iterative methods for solving inverse problems at different precision levels. 

<p align="center">
<img src="img/zelda.jpeg" alt="drawing" width="500"/> 
</p>
<p align = "center">
Figure 1: screenshot from <em>the Legend of Zelda - Breath of the Wild</em>
</p>

## Background: Why Low Precision?
What is the most important aspect for an excellent gaming experience? A lot of people would answer real-time! Everyone want their games to be fast, and it is always a bummer that the screen freezes during a critical combat. This is why we are investigating low precision arithmetic: to decrease the computation time and speed things up.

Nowadays, most computer systems operate on double precision (64-bit) arithmetic. However, if we decrease the number of bits for each number to 16 bits or even lower, the processing time can be much significantly reduced, although the benefit comes at the cost of a loss of accuracy.



<p align="center">
<img src="img/IEEE.png" alt="drawing" width="500"/> 
</p>

## Simulating Low Precision

### Matlab function chop
To simulate low precision arithmetic on our 64-bit computers, we have imported a MATLAB package called [chop](https://www.mathworks.com/matlabcentral/fileexchange/70651-chop?s_tid=mwa_osa_a). The toolbox allows us to explore single precision, half precision, and other customized formats. Each input needs to be transformed, but the real work comes from chopping each operation. The code below is a toy example of how to calculate $x + y \times z$ in half precision with chop.

<p align="center">
<img src="img/chop_overview.png" alt="drawing" width="300"/> 
</p>

### Blocking
When the number is being chopped from double precision to half precision, a lot of bits are dropped (from 64 bits to 16 bits). This would certainly cause a level of inaccuracy, so in order to reduce the errors a method called blocking is used. Blocking is the same as breaking a large operation into smaller chunks, where each is computed independently and the result is summed. 

We do the inner product for each precision and block size for 20 times and calculate the average. The diagrams are the following, and the error are computed as the difference between the result of using chopped version of inner product function and using the function in matlab. 
<p align="center">
<img src="img/blocksize.png" alt="draw" width="700"/> 
</p>
In the graph on the left hand side, the errors of half precision is the lagrgest, which makes sense because it has the least bits. If we take a closer look at only half precision, we get the right-hand-side graph. The errors decrease sharply when blocking method is introduced. However, the larger block size doesn't necessarily mean lower errors, as the graph suggested: the errors increase as the block size keeps growing. That's because when the block size is large, it's the same as doing no blocking at all. For example, for the size-500 vector, as long as the block size reaches 500, it means just putting the whole vector into the first block, the same as when block size is 0. Therefore, the line becomes flat staring from block size is 500. It is reasonable to say that which block size is better depends on the problem size, so we use 258 as our default block size in our codes, because the matrix dimension is rather large in our problem.

## Inverse Problems and Iterative Methods
Inverse problems are problems where our goal is to find the internal or hidden information (input) from outside measurements (result). The internal data can be approximated by iterative methods, a repeating implementation of the same system of equations, with variables getting updated each round, hoping the value generated can be closer to the ture value we want each term. 

### Conjugate Gradient Method
The [conjugate gradient algorithm](https://www.cs.cmu.edu/~quake-papers/painless-conjugate-gradient.pdf) aims to solve the linear system Ax = b where A is SPD (symmetric and positive definite),transforming the problem of finding solution to an optimization problem where we want to minimize $\phi(x)=\frac{1}{2}x^{T}Ax-x^{T}b$. This can be easily seen from $\nabla \phi (x) = 0$ -> $Ax-b=0$.

In each step length the method provides us with a search direction and a step-length so that the error of this iteration is A-orthogonal to the search direction of the last oteration. Eventually it will converge to the min point. The CGLS algorithm is the least squares version of the CG method,applied to the normal equation A<sup>T</sup>Ax = A<sup>T</sup>b.

### Chebyshev Semi-Iterative Method

The Chebyshev Semi-Iterative (CS) Method requires no inner product computation, which is great because it will cause overflow easily in CG. But there is always the trade-off! The CS method needs the user to have an idea of the range of eigenvalues of the matrix A. The result given by CS is a linear combination of all solutions in each iteration, and the weights are obtained from the Chebyshev polynomial, which has the favorable property to ensure that the result obtained in each iteration of CS is smaller than an upper bound.

## Experiment!!

### IR Tools
We modified CGLS method in [IRtool](https://github.com/jnagy1/IRtools.git) package in Matlab so that it can operate in lower precisions, and we used two test problems in the same package to investigate how the method performs at lower precision, mainly half precision. 
### Image Deblurring Using CGLS
First, we used our modified version of CGLS without regularization to run the image deblurring problem, and we used the function called PRshowx to plot the graph generated from x value in the last iteration. At the beginning we didn’t add any noise to the b in the problem of Ax = b, and the graphs are put below. 
<p align="center">
<img src="img/blur no noise.png" alt="draw" width="600"/> 
</p>

We used cgls_chop for the single and half precision, and the graph in single precision is similar to the graph in double precision. However, for the half precision, the background is not the same as that in double-precision or half-precision graph. The background looks redder and there are red and black squiggly lines.

We also plotted the error norms of the x value we get in compared to the true value of x in different precision. 
<p align="center">
<img src="img/enrm blur no noise.png" alt="draw" width="600"/> 
</p>

From the graph, all three lines overlap from the beginning until around 20 iterations, where the half precision line differs, starting to go up. It’s due to the round up errors of the half precision, which adds up and takes over. Also, the line of half precision stops at around 30 iterations, because at 28th iteration, we get infinities, so the next few iterations generate nothing but NaNs.

After investigating the idealized situations where there is no noise in the output image, we then apply our code to graphs that are mixed with random noise to see how it is likely to perform in real life.

For half precision, with 0.1% noise, the picture looks almost the same as the one that contains no noise. However, if the noise level is increased to 1%, the background turns into random red ripples while the middle object is still identifiable. Noise has taken over the black background but not the satellite yet. Eventually, the whole image is flushed with the noisy ripples with 10% noise; the picture no longer contains any meaningful information.

<p align="center">
<img src="img/2.png" alt="draw" width="700"/> 
</p>

Now we turn our attention to the error norm, the difference between the original image and the one our algorithm generates. When 0.1% noise is added, as the number of iterations goes up, the error norm reduces significantly across all three formats. Intriguingly, for images with 1% or 10% noise, the best reconstruction is not the last iteration but somewhere along the middle (it’s around the 50th iteration for 1% and 10th for 10%). The reason behind the phenomenon is that while we are transforming the output image, b, along each iteration, the blended noise also gets inverted. Eventually, the random data accumulates and dominates the solution at some point. Please also notice that we are showing the images constructed from the last iteration rather than the best one, since we do not have information on the true image in real life situations, and thus the error norm and the best iteration are unknown.

<p align="center">
<img src="img/3.png" alt="draw" width="700"/> 
</p>

### Tomography Reconstruction Using CGLS
Below is the result when we run CGLS on the test problem at different precision levels. We can see for double and single precision, the reconstruction is doing well, yet for the fp16 problem we started to get this completely blue picture from the first iteration caused by overflow of Inf/-Inf.

<p align="center">
<img src="img/tomo_plot.png" alt="draw" width="800"/> 
</p>

Our solution to this is that we rescaled Both A and b by dividing both of them by 100. And we get the result below:

<p align="center">
<img src="img/tomo_rescale.png" alt="draw" width="300"/> 
</p>
which is still blurry but at least the shape is visible :)

And then we add noise to the right hand side b, and plotted the error norms below:

<p align="center">
<img src="img/error_tomo.png" alt="draw" width="800"/> 
</p>

As in the image deblurring problem, the error norm first decreases then increases. In the cases with noise, this is mainly because noise started to take over in later part of the iteration. We still see the same behavior in the test problem even without noise at fp16. This is because the truncation errors got accumulated as the iteration goes on.

### Image Deblurring Using CS
In order to prevent overflow from occuring, we changed to CS algorithm (so no inner products used) and used chop to enable it run in lower precision. We applied Tikhonov regularization to CS after we find out that the algorithm performs poorly due to the close-to-zero singular value of A when it's ill-conditioned. Now we are solving:
$$\min_{x} \{||Ax-b||_2^2+\lambda^2||x||_2^2\}$$ where $\lambda$ is generated by the function [IRhybrid_lsqr](https://www.emis.de/journals/ETNA/vol.28.2007-2008/pp149-167.dir/pp149-167.pdf).

From the graph below, it is clear that even with 10% noise, the half graph looks very similar to that in double precision, better than what we have using CGLS. 
<p align="center">
<img src="img/cs_reg_0.1_blur.png" alt="draw" width="500"/> 
</p>
For image deblurring problem, We further comfirmed by plotting the error norm. 
<p align="center">
<img src="img/cs_reg_0.1_blur_Enrm.png" alt="draw" width="300"/> 
</p>
We can see that the error norms of three precisions overlap, proving the result in half precision is similar to that in double precision. 

### Tomography Reconstruction Using CS
We also ran the code to solve tomography reconstruction too, and the result is showed below. 
<p align="center">
<img src="img/cs_reg_0.1_tomo.png" alt="draw" width="500"/> 
</p>
Although there is no inner product in CS, we still have overflow in half precision, which is because the A is too large. Therefore, we rescale A and b by diving both of by 100, so that the algorithm successfully ran to the end without generating NaNs. The image in half precision is as good as double precision, possessing clear boundaries and backgrounds. The error norm also shows great overlappings among the three precisions.

### Image Deblurring Using CGLS with regularizationand 
To fully compare CGLS and CS, we added Tikhonov regularization to CGLS and ran the two test problems. The diagrams are listed below.
We also ran the code to solve tomography reconstruction too, and the result is showed below. 
<p align="center">
<img src="img/cg_reg_blur_64_0.1_m.png" alt="draw" width="500"/> 
</p>
<p align="center">
<img src="img/cg_reg_m_0.1_blur_Enrm.png" alt="draw" width="300"/> 
</p>
The diagram for half precision looks much better than that produced by CGLS without regularization. However, in the background there is still a different between half and double precision. From the error norm, we can see that at the end of the iteration for half precision, the error norm still starts to go up. To see the error norms more clearly, we zoomed in the picture of error norm for CS and CGLS with regularization, and this is what we got:
<p align="center">
<img src="img/Zoom in of Enrm for cs and cg.png" alt="draw" width="500"/> 
</p>
We can see that the error norm for half precision converges for CS but increases rapidly for CGLS, suggesting that for half precision, CS is a better choice. However, for double precision, the CGLS with regularization is clearly more stable. Therefore, CGLS with regularizatin is more suitable for double precision. For tomography reconstruction, the result is similar to this, so it not shown here. There is detailed information in our [paper](https://github.com/kristinagxy/emory-reu-ret-website/tree/main/content/projects/2022-mixed-precision), and we welcome you to check it out.

