---
# Documentation: https://wowchemy.com/docs/managing-content/

title: Applications of Automatic Differentiation in Image Registration
subtitle: ''
summary: ''
authors:
- Warin Watson
- Cash Cherry
- Rachelle Lang
tags: ["Summer 2024"]
categories: []
date: '2025-07-28'
lastmod: 2025-11-18
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
projects: ["2024-registration"]
publishDate: '2025-07-28'
publication_types:
- 3
abstract: 'We demonstrate that automatic differentiation (AD), which has become commonly available in machine learning frameworks, is an efficient way to explore ideas that lead to algorithmic improvement in multi-scale affine image registration and affine super-resolution problems. In our first experiment on multi-scale registration, we implement an ODE predictor-corrector method involving a derivative with respect to the scale parameter and the Hessian of an image registration objective function, both of which would be difficult to compute without AD. Our findings indicate that exact Hessians are necessary for the method to provide any benefits over a traditional multi-scale method; a Gauss-Newton Hessian approximation fails to provide such benefits. In our second experiment, we implement a variable projected Gauss-Newton method for super-resolution and use AD to differentiate through the iteratively computed projection, a method previously unaddressed in the literature. We show that Jacobians obtained without differentiating through the projection are poor approximations to the true Jacobians of the variable projected forward map and explore the performance of other approximations in the problem of super-resolution. By addressing these problems, this work contributes to the application of AD in image registration and sets a precedent for further use of machine learning tools in this field.'
pages : 15 pages
publication: 'SIAM Undergraduate Research Online (SIURO), volume 18'
url_pdf: 'https://doi.org/10.1137/24S1710917'
url_video : 'https://youtu.be/8O9S8zm2N-E'
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/8O9S8zm2N-E" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

We demonstrate that automatic differentiation, which has become commonly available in machine learning frameworks, is an efficient way to explore ideas that lead to algorithmic improvement in multi-scale affine image registration and affine super-resolution problems. In our first experiment on multi-scale registration, we implement an ODE predictor-corrector method involving a derivative with respect to the scale parameter and the Hessian of an image registration objective function, both of which would be difficult to compute without AD. Our findings indicate that exact Hessians are necessary for the method to provide any benefits over a traditional multi-scale method; a Gauss-Newton Hessian approximation fails to provide such benefits. In our second experiment, we implement a variable projected Gauss-Newton method for super-resolution and use AD to differentiate through the iteratively computed projection, a method previously unaddressed in the literature. We show that Jacobians obtained without differentiating through the projection are poor approximations to the true Jacobians of the variable projected forward map and explore the performance of some other approximations. By addressing these problems, this work contributes to the application of AD in image registration and sets a precedent for further use of machine learning tools in this field.