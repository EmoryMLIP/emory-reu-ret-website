---
# Documentation: https://wowchemy.com/docs/managing-content/

title: Alternating Minimization for Computed Tomography with Unknown Geometry Parameters
subtitle: ''
summary: ''
authors:
- Mai Phuong Pham Huynh
- Manuel Santana
- Ana Castillo
tags: []
categories: []
date: '2021-08-18'
lastmod: 2021-12-14T16:45:31-04:00
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
publishDate: '2021-08-18T20:45:31.467151Z'
publication_types:
- 3
abstract: 'Due to the COVID-19 pandemic, there is an increasing demand for portable CT machines worldwide in order to diagnose patients in a variety of settings [16]. This has lead to a need for CT image reconstruction algorithms that can produce high-quality images in the case when multiple types of geometry parameters have been perturbed. In this paper, we present an alternating descent algorithm to address this issue, where one step minimizes a regularized linear least squares problem, and the other minimizes a bounded non-linear least-square problem. Additionally, we survey existing methods to accelerate the convergence algorithm and discuss implementation details through the use of MATLAB packages such as IRtools and imfil. Finally, numerical experiments are conducted to show the effectiveness of our algorithm. '
pages : 21 pages
publication: 'SIAM Undergraduate Research Online (SIURO), volume 15'
url_pdf : 'https://dx.doi.org/10.1137/21S1441638'
url_video : 'https://www.youtube.com/watch?v=qdcGe9MKCoI'
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/qdcGe9MKCoI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Due to the COVID-19 pandemic, there is an increasing demand for portable CT machines worldwide in order to diagnose patients in a variety of settings [16]. This has lead to a need for CT image reconstruction algorithms that can produce high-quality images in the case when multiple types of geometry parameters have been perturbed. In this paper, we present an alternating descent algorithm to address this issue, where one step minimizes a regularized linear least squares problem, and the other minimizes a bounded non-linear least-square problem. Additionally, we survey existing methods to accelerate the convergence algorithm and discuss implementation details through the use of MATLAB packages such as IRtools and imfil. Finally, numerical experiments are conducted to show the effectiveness of our algorithm.