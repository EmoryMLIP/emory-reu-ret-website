---
title: 'Mixed-Precision Algorithms for Image Processing'
date: 2022-06-27T11:36:49-04:00
lastmod: 2022-06-27T11:36:49-04:00
featured: true
weight : 100
summary: 'Since numbers in the computer are represented with a fixed number of bits, loss of accuracy during calculation is unavoidable. At high precision where more bits are allocated to each number, round-off errors are typically small. On the other hand, doing calculation at a lower precision has the advantage of being much faster. This research focuses on experimenting doing arithmetic at different precision levels. We would first simulate low-precision arithmetic with the Matlab function chop on basic operations such as inner product of vectors, norms, matrix- matrix multiplication, etc. Then, we would modify iterative methods in the IR tools package to make the arithmetic happen at lower precision and mixed precision, run experiments on the image processing tasks and compare their performance at different precision level.'
tags: ["Summer 2022"]
---
