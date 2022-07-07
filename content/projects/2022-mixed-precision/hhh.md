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

We calculate the inner product between x1 y1, and x2 y2, and at last we sum them up. The result we get is more accurate, and we plot the error diagram of inner product of tow random vectors. We do the inner product for each precision and block size for 20 times and calculate the average. The diagrams are the following, and the error are computed as the difference between the result of using chopped version of inner product function and using the function in matlab. 
<p align="center">
<img src="img/blocksize.png" alt="draw" width="600"/> 
</p>
In the graph on the left hand side, the errors of half precision is the lagrgest, which makes sense because it has the least bits. If we take a closer look at only half precision, we get the right-hand-side graph. The errors decrease sharply when blocking method is introduced. However, the larger block size doesn't necessarily mean lower errors, as the graph suggested: the errors increase as the block size keeps growing. That's because when the block size is large, it's the same as doing no blocking at all. For example, for the size-500 vector, as long as the block size reaches 500, it means just putting the whole vector into the first block, the same as when block size is 0. Therefore, the line becomes flat staring from block size is 500. It is reasonable to say that which block size is better depends on the problem size, so we use 258 as our default block size in our codes, because the matrix dimension is rather large in our problem.

## Inverse Problems and Iterative Methods
Inverse problems are problems where our goal is to find the internal or hidden information (input) from outside measurements (result). The internal data can be approximated by iterative methods, a repeating implementation of the same system of equations, with variables getting updated each round, hoping the value generated can be closer to the ture value we want each term. 



### Conjugate Gradient Method
The conjugate gradient algorithm aims to solve the linear system Ax = b where A is SPD (symmetric and positive definite). 

In a very clever way, conjugate gradient method transforms the problem of finding solution to an optimization problem where we want to minimize 
$\phi(x)=\frac{1}{2}x^{T}Ax-x^{T}b$. This can be easily seen from $\nabla \phi (x) = 0$ -> $Ax-b=0$.

How this algorithm works is that in each iteration, x is allowed to explore one more subspace in addition to the previous subspaces it has already explored (the subspaces here are the Krylov Spaces!). During that iteration, x is updated to the point where the residual norm ||Ax-b|| is minimized. Mathematically (meaning no noise or round-off errors), CG is guaranteed to converge within a limited number of steps. Specifically if A is a nxn matrix, it will find the solution in no greater than n steps.

The CGLS algorithm is the least squares version of the CG method. To add the taste of least squares to the original problem, A -> A<sup>T</sup>A and b -> A<sup>T</sup>b.

One potential problem with this method is that it requires the calculation of inner products, which easily gets overflowed when we are at low precision. Therefore we tried another method below that avoids the use of inner products.

### Chebyshev Semi-Iterative Method

The CS method requires no inner product computation, which is great. But there is always the trade-off! CS method needs the user to have an idea of the range of eigenvalues of the matrix A. The result given by CS is a linear combination of all solutions in each iteration, and the weights are obtained from the Chebyshev polynomial, which has the favorable property of having an absolute value no greater than 1 on the interval [-1,1] and grow rapidly outside this interval. This ensures that the result obtained in each iteration of CS is smaller than a upper bound.

## Experiment!!

### IR Tools

### Image Deblurring
First, we use our modified version of cgls without regularization to run the image deblurring problem, and we use the function called PRshowx to plot the graph generated from x value in the last iteration. At the beginning we didn’t add any noise to the b in the problem of Ax = b, and the graphs are put below. 
<p align="center">
<src="img/blur no noise.png" alt="draw" width="600"/> 
</p>

For the double precision, we used the original cgls method because it’s faster and we could have a reference. We used cgls_chop for the single and half precision, and the graph in single precision is similar to the graph in double precision. However, for the half precision, the background is not the same as that in double-precision or half-precision graph. The background looks redder and there are red and black squiggly lines.

### Tomography Reconstruction
<p align="center">
<img src="img/Screen Shot 2022-07-07 at 10.42.11 AM.png" alt="draw" width="800"/> 
</p>
