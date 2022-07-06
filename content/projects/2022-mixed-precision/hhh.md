This post was written by Xiaoyun Gong, Yizhou Chen, and Xiang Ji and published with minor edits. The team was advised by Dr. James Nagy. In addition to this post, the team has also created slides for a [midterm presentation](), a [poster blitz]() video, [code](), and a [paper]().

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

## Inverse Problems and Iterative Methods

### CGLS
The conjugate gradient algorithm aims to solve the linear system Ax = b where A is SPD (symmetric and positive definite). 

How this algorithm works is that in each iteration, x is allowed to explore one more subspace in addition to the previous subspaces it has already explored (the subspaces here are the Krylov Spaces!). During that iteration, x is updated to the point where the residual norm ||Ax-b|| is minimized. Mathematically (meaning no noise or round-off errors), CG is guaranteed to converge within a limited number of steps. Specifically if A is a nxn matrix, it will find the solution in no greater than n steps.


### CS

## Experiment!!

### Image Deblurring

### Tomography Reconstruction
