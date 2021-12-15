---
# Documentation: https://wowchemy.com/docs/managing-content/

title: A Tensor SVD-based Classification Algorithm Applied to fMRI Data
subtitle: ''
summary: ''
authors:
- Katy Keegan
- Tanvi Vishwanath
- Yihua Xu
tags: []
categories: []
date: '2021-10-31'
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
publishDate: '2021-10-31T20:45:31.467151Z'
publication_types:
- 3
abstract: 'To analyze the abundance of multidimensional data, tensor-based frameworks have been developed. Traditionally, the matrix singular value decomposition (SVD) is used to extract the most dominant features from a matrix containing the vectorized data. While the SVD is highly useful for data that can be appropriately represented as a matrix, this step of vectorization causes us to lose the high-dimensional relationships intrinsic to the data. To facilitate efficient multidimensional feature extraction, we utilize a projection-based classification algorithm using the t-SVDM, a tensor analog of the matrix SVD. Our work extends the t-SVDM framework and the classification algorithm, both initially proposed for tensors of order 3, to any number of dimensions. We then apply this algorithm to a classification task using the StarPlus fMRI dataset. Our numerical experiments demonstrate that there exists a superior tensor-based approach to fMRI classification than the best possible equivalent matrix-based approach. Our results illustrate the advantages of our chosen tensor framework, provide insight into beneficial choices of parameters, and could be further developed for classification of more complex imaging data. We provide our Python implementation at this https URL.'
pages : 23 pages
publication: '*arXiv preprint 2109.01481*'
url_pdf : 'https://arxiv.org/pdf/2109.01481'
url_code : 'https://github.com/elizabethnewman/tensor-fmri'
---

