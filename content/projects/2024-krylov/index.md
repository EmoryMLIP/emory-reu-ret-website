---
title: 'Efficient Processing of Image Sequences with Krylov Subspace Recycling'
date: 2024-07-08
featured: true
weight : 20
summary: ''
tags: ["Summer 2024"]
authors: [lonisk]
---

This blog post was written by Clara Armstrong, Olivia Kallay, and Srijon Sarkar and published with minor edits. Our work was advised by Dr. Lucas Onisk. In addition to this post, the team has also given a midterm presentation.

## Background

We are interested in solving sequences of linear discrete ill-posed problems for the purpose of deblurring images. We let $A$ be our blurring matrix, the convolution between a _point-spread function (PSF)_ and a boundary condition. A PSF models the smearing of a pixel to its neighboring pixels for image blurring. The true image is represented by the matrix $X$ and the blurred image by the matrix $B$, both of which we vectorize to get $x$ and $b$ respectively. This forms our linear system, $Ax=b$. Subsequent images will have identical or slowly changing matrices, and the right-hand sides (e.g. subsequent blurred images) will be close. We work with the sequence of these linear problems to deblur the sequence of images.

<p align="center"><img width="234" alt="captioned_blurred" src="https://github.com/lonisk1/2024Emory_REU_KrylovRecycling/assets/171604235/7621d6e8-27da-4e4a-8f6a-4a5e5bbcb091">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img width="234" alt="captioned_psf2" src="https://github.com/lonisk1/2024Emory_REU_KrylovRecycling/assets/171604235/2848c430-bd74-4239-91f9-5472b4ea7ca5">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img width="234" alt="captioned_deblurred" src="https://github.com/lonisk1/2024Emory_REU_KrylovRecycling/assets/171604235/812e2f22-7a9a-4244-bd3d-c4f0132f6fd1"></p>

When deblurring an image, we want to solve for $x$. For exposition, we assume $A$ is invertible, giving us the linear inverse problem $A^{-1}b=x$. Since our blurred image contains error such that $Ax=b=\hat{b}+e$, solving this directly does not yield our true solution &x$. The singular values of $A$ decay towards and cluster near numerical zero, thereby making $A$ _ill-conditioned_. Thus, when we take the Singular Value Decomposition (SVD), $A=U\Sigma V^T$, and attempt to solve $A^{-1}b=x$, we end up with 

$$
\begin{aligned}
x &= V\Sigma^{-1}U^Tb \\
  &= \sum_{i=1}^{n}\frac{u_i^Tb}{\sigma_i}v_i \\
  &= \sum_{i=1}^{n}\frac{u_i^T\hat{b}}{\sigma_i}v_i+ \sum_{i=1}^{n}\frac{u_i^Te}{\sigma_i}v_i
\end{aligned}
$$

Where the first sum is our _true solution_ and the second is our _inverted noise_. For image deblurring problems, the $u_i^Te$ terms are constant in magnitude. Therefore, the solution is dominated by the inverted noise, which becomes very big as the singular values $\sigma_i$ decay to numerical zero.

By _Hadamard's criteria_, a problem is ill-posed when it meets at least one of the following conditions:

1. The problem has no exact solution.
2. The problem has multiple solutions.
3. Solutions do not depend continuously on the data.

Since our solution becomes dominated by error, it meets the third condition. As we are unable to accurately solve for $x$ using the SVD, we will employ methods that utilize regularization to help quell the error propagation in our computed solution. We will use strategies such as working in a Krylov subspace.


## Our Approach

We aim to build a small subspace that captures enough information about the system in $\mathbb{R}^n$ to compute an approximate solution to the current problem. We will focus on two different Krylov techniques: _Arnoldi_ and _Golub-Kahan bidiagonalization (GKB)_. Using Krylov methods allows us to working in a smaller subspace with a smaller operator, making our problem easier to solve than trying to solve directly. 

A Krylov subspace is the span of repeated applications of a matrix $A$ to a vector $b$, or
<p align="center">$K_p(A, b) = \text{span}\{b, Ab, A^2b, ... , A^{p-1}b\}$</p>

The Arnoldi relation is at the core of the _Generalized Minimal Residual (GMRES)_ method for solving **square nonsymmetric** linear problems. After $p$ steps of the Arnoldi iteration, which gives the Krylov subspace shown above, we develop the relation
<p align="center">$AV_p = V_{p+1}H_{p+1}$</p>

Where $A$ is the square operator from the linear system, $V_{p+1}$ has orthonormal columns that span the subspace $K_p(A, b)$, $V_p$ contains the first $p$ orthonormal columns of $V_{p+1}$, and $H_{p+1}$ is an upper Hessenberg matrix (an upper triangular matrix that contains an additional subdiagonal band) with its columns representing scalar coefficients from the orthonormalization process of Gram Schmidt, used in Arnoldi.

Similar to the relationship between the Arnoldi relation and GMRES method, GKB is associated with the LSQR method where $A$ could be **non-square**. GKB generates orthonormal vectors that span the following spaces

$$K_p(A^TA, A^Tb) \text{ and } K_p(AA^T, b)$$

After $p$ steps of GKB, we have the following relationships

$$AV_p = U_{p+1}B_{p+1} \text{ and } A^TU_{p+1} = V_{p+1}\tilde B_{p+1}$$

Where $V_{p+1}$, spanning $K_p (A^TA, A^Tb)$, and $U_{p+1}$, spanning $K_p(AA^T, b)$, contain orthonormal columns, and $B_{p+1}$ represents a lower bidiagonal matrix (a diagonal matrix with an additional subdiagonal band) that makes $\tilde B_{p+1}$ square due to the inclusion of an additional column.

## Our Observations

Since GMRES necessitates a lot of matrix-vector products, we desire to gain efficiency through recycling strategies to circumvent such repetitive computation. We observed that $r^{(2)}=Ax_{approx}^{(1)}-b^{(2)}$, the residual of the second problem using our solution to the first problem, which we call the seed problem, is higher than the breakout level but remains significantly lower than it would if we started from the zero vector (which would produce a relative residual of one). Thus, by recycling basis vectors from previous solutions to solve subsequent problems, we drastically reduce the Reconstructive Residual Norm (RRN).

$$DP \leq r^{(2)} < 1,$$

where DP represents a breakout parameter from the _Discrepancy Principle_. We note that with these types of methods, residuals decrease, but errors diverge. Thus, we adapt regularization methods such as truncated SVD (TSVD) to prevent capturing information around low singular values, as the subspace grows with each iteration, which could corrupt the solution we desire. To avoid the high propensity of error propagation, we rather undersolve by claiming breakout bounds on noise on the right-hand sides.

As the basis from the seed problem contains useful information for non-arbitrarily chosen right-hand sides (frames here), we incorporate this information by calculating

$$\text{res} = \frac{\textbf{r}^{(2)} - V_pV_p^T\textbf{r}^{(2)}}{\|\|\textbf{r}^{(2)} - V_pV_p^T\textbf{r}^{(2)}\|\|}$$

and appending it in $[V_p \quad res] = \tilde V_{\ell}$ thereby forming the _flexible Arnoldi_ method as $A[\tilde V_{\ell}] = \tilde U_{\ell+1}J_{\ell+1}$ at step $\ell$. $U$ and $J$ come from completing the back half of Arnoldi, respectively representing a new basis and a projected variant of $A$.


## Future Directions

Eventually, we will run out of memory as we continue iterating flexible Arnoldi and storing more basis vectors. To avoid this, we will utilize different compression strategies to decide which basis vectors should be retained for solving subsequent problems, and which may be discarded. The compression strategies we aim to use are 
1. Truncated Singular Value Decomposition
2. Reduced Basis Decomposition
3. Solution-Oriented Compression
4. Sparsity-Enforcing Regularization

We aim to combine compression techniques with flexible algorithms, including extending our work to non-square operators to replicate _flexible GKB_ for LSQR.

Further, as these iterative processes continue and our subspace grows, it might capture information from small singular values. So, we discern the need for penalized least squares using _Tikhonov regularization_ for our projected problems as

$${\min_\textbf{x}} ||A\textbf{x}-\textbf{b}||_2^2 + \lambda^2||\textbf{x}||_2^2.$$

So far, we have only focused on sequences of images, such as those that may arise from a video. However, these techniques can also be useful for other sequences of linear inverse problems, such as those arising from medical imaging. 

## References

1. _On the Use of Arnoldi and Golub-Kahan Bases to Solve Nonsymmetric Ill-Posed Inverse Problems_, Brown, A. M., (2015)
2. _GMRES: A Generalized Minimal Residual Algorithm for Solving Nonsymmetric Linear Systems_, Saad, Y. and Schultz, M.H., (1986)
3. _Hybrid Projection Methods with Recycling for Inverse Problems_, Jiang, J., Chung, J., and de Sturler, E., (2021)
