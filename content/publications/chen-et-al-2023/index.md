---
# Documentation: https://wowchemy.com/docs/managing-content/

title: Iterative Methods at Lower Precision
subtitle: ''
summary: ''
authors:
- Yizhou Chen 
- Xiaoyun Gong 
- Xiang Ji
tags: []
categories: []
date: '2031-08-01'
lastmod: 2023-09-22
featured: true
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ''
  focal_point: ''
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
publishDate: '2023-08-01'
publication_types:
- 3
abstract: 'Since numbers in the computer are represented with a fixed number of bits, loss of accuracy during calculation is unavoidable. At high precision where more bits (e.g. 64) are allocated to each number, round-off errors are typically small. On the other hand, calculating at lower precision, such as half (16 bits), has the advantage of being much faster. This research focuses on experimenting with arithmetic at different precision levels for large-scale inverse problems, which are represented by linear systems with ill-conditioned matrices. We modified the Conjugate Gradient Method for Least Squares (CGLS) and the Chebyshev Semi-Iterative Method (CS) with Tikhonov regularization to do arithmetic at lower precision using the MATLAB chop function, and we ran experiments on applications from image processing and compared their performance at different precision levels. We concluded that CGLS is a more stable algorithm, but overflows easily due to the computation of inner products, while CS is less likely to overflow but it has more erratic convergence behavior. When the noise level is high, CS outperforms CGLS by being able to run more iterations before overflow occurs; when the noise level is close to zero, CS appears to be more susceptible to accumulation of round-off errors.'
pages : 22 pages
publication: 'SIAM Undergraduate Research Online (SIURO), volume 16'
url_pdf : 'https://dx.doi.org/10.1137/22S152637X'
url_video : 'https://www.dropbox.com/s/139l0u7zi6eloao/mixed-precision.mp4?dl=0'
---


Since numbers in the computer are represented with a fixed number of bits, loss of accuracy during calculation is unavoidable. At high precision where more bits (e.g. 64) are allocated to each number, round-off errors are typically small. On the other hand, calculating at lower precision, such as half (16 bits), has the advantage of being much faster. This research focuses on experimenting with arithmetic at different precision levels for large-scale inverse problems, which are represented by linear systems with ill-conditioned matrices. We modified the Conjugate Gradient Method for Least Squares (CGLS) and the Chebyshev Semi-Iterative Method (CS) with Tikhonov regularization to do arithmetic at lower precision using the MATLAB chop function, and we ran experiments on applications from image processing and compared their performance at different precision levels. We concluded that CGLS is a more stable algorithm, but overflows easily due to the computation of inner products, while CS is less likely to overflow but it has more erratic convergence behavior. When the noise level is high, CS outperforms CGLS by being able to run more iterations before overflow occurs; when the noise level is close to zero, CS appears to be more susceptible to accumulation of round-off errors.