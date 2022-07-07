This post was written by Xiaoyun Gong, Yizhou Chen, and Xiang Ji and published with minor edits. The team was advised by Dr. James Nagy. In addition to this post, the team has also created slides for a [midterm presentation](REUmidterm_presentation.pdf
), a [poster blitz]() video, [code](), and a [paper]().

## In One Sentence:
Our group works on experimenting with iterative methods for solving inverse problems at different precision levels.

## Background: Why Low Precision?

<p align="center">
<img src="img/zelda.jpeg" alt="drawing" width="500"/> 
</p>
<p align = "center">
Figure 1: screenshot from <em>the Legend of Zelda - Breath of the Wild</em>
</p>

## Simulating Low Precision

### Matlab function chop

### Blocking
When the number is being chopped from double precision to half precision, a lot of bits are dropped (from 64 bits to 16 bits). This would certainly cause a level of inaccuracy, so in order to reduce the errors a method called blocking is used. Blocking is the same as breaking a large operation into smaller chunks, where each is computed independently and the result is summed. 

For example, there are two vectors of 6 elements:

x = [x<sub>1</sub>, x<sub>2</sub>, x<sub>3</sub>, x<sub>4</sub>, x<sub>5</sub>, x<sub>6</sub>], y = [y<sub>1</sub>, y<sub>2</sub>, y<sub>3</sub>, y<sub>4</sub>, y<sub>5</sub>, y<sub>6</sub>].

If we want to calculate the inner product between these two, instead of calculating them directly, we could break them into different groups, 2 in this case. Then, we have: 

x1 = [x<sub>1</sub>, x<sub>2</sub>, x<sub>3</sub>], y1 = [y<sub>1</sub>, y<sub>2</sub>, y<sub>3</sub>];
x2 = [x<sub>4</sub>, x<sub>5</sub>, x<sub>6</sub>], y2 = [y<sub>4</sub>, y<sub>5</sub>, y<sub>6</sub>].

We calculate the inner product between x1 y1, and x2 y2, and at last we sum them up. The result we get is more accurate. We plot the error diagram of inner product of tow random vectors. We operate for 20 times and calculate the average. The diagrams are the following, and the error are computed as the difference between the result of using chopped version of inner product function and using the function in matlab. 
<p align="center">
<img src="img/zelda.jpeg" alt="drawing" width="500"/> 
</p>


## Inverse Problems and Iterative Methods

### Conjugate Gradient Method
The conjugate gradient algorithm aims to solve the linear system Ax = b where A is SPD (symmetric and positive definite). 

In a very clever way, conjugate gradient method transforms the problem of finding solution to an optimization problem where we want to minimize 
$\phi(x)=\frac{1}{2}x^{T}Ax-x^{T}b$. This can be easily seen from $\nabla \phi (x) = 0$ -> $Ax-b=0$.


How this algorithm works is that in each iteration, x is allowed to explore one more subspace in addition to the previous subspaces it has already explored (the subspaces here are the Krylov Spaces!). During that iteration, x is updated to the point where the residual norm ||Ax-b|| is minimized. Mathematically (meaning no noise or round-off errors), CG is guaranteed to converge within a limited number of steps. Specifically if A is a nxn matrix, it will find the solution in no greater than n steps.

The CGLS algorithm is the least squares version of the CG method. To add the taste of least squares to the original problem, A -> A<sup>T</sup>A and b -> A<sup>T</sup>b.

One potential problem with this method is that it requires the calculation of inner products, which easily gets overflowed when we are at low precision. Therefore we tried another method below that avoids the use of inner products.

### Chebyshev Semi-Iterative Method
The CS method requires no inner product computation, which is great. But there is always the trade-off! CS method needs the user to have an idea of the range of eigenvalues of the matrix A. The result given by CS is a linear combination of all solutions in each iteration, and the weights are obtained from the Chebyshev polynomial, which has the favorable property of having an absolute value no greater than 1 on the interval [-1,1] and grow rapidly outside this interval. This ensures that the result obtained in each iteration of CS is smaller than a upper bound.

### regularization


## Experiment!!

### IR Tools

### Image Deblurring

### Tomography Reconstruction

