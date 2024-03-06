---
# Documentation: https://wowchemy.com/docs/managing-content/

title: Training Implicit Networks for Image Deblurring using Jacobian-Free Backpropagation
subtitle: ''
summary: ''
authors:
- Linghai Liu
- Shuaicheng Tong
- Lisa Zhao
tags: []
categories: []
date: '2024-02-01'
lastmod: 2024-02-09
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
publishDate: '2024-02-01'
publication_types: 1
abstract: 'Recent efforts in applying implicit networks to solve inverse problems in imaging have achieved competitive or even superior results when compared to feedforward networks. These implicit networks only require constant memory during backpropagation, regardless of the number of layers. However, they are not necessarily easy to train. Gradient calculations are computationally expensive because they require backpropagating through a fixed point. In particular, this process requires solving a large linear system whose size is determined by the number of features in the fixed point iteration. This paper explores a recently proposed method, Jacobian-free Backpropagation (JFB), a backpropagation scheme that circumvents such calculation, in the context of image deblurring problems. Our results show that JFB is comparable against fine-tuned optimization schemes, state-of-the-art (SOTA) feedforward networks, and existing implicit networks at a reduced computational cost.'
pages : '10 pages'
url_preprint : 'https://arxiv.org/abs/2402.02065'
url_code : ' https://github.com/lliu58b/Jacobian-free-Backprop-Implicit-Networks'
---

Recent efforts in applying implicit networks to solve inverse problems in imaging have achieved competitive or even superior results when compared to feedforward networks. These implicit networks only require constant memory during backpropagation, regardless of the number of layers. However, they are not necessarily easy to train. Gradient calculations are computationally expensive because they require backpropagating through a fixed point. In particular, this process requires solving a large linear system whose size is determined by the number of features in the fixed point iteration. This paper explores a recently proposed method, Jacobian-free Backpropagation (JFB), a backpropagation scheme that circumvents such calculation, in the context of image deblurring problems. Our results show that JFB is comparable against fine-tuned optimization schemes, state-of-the-art (SOTA) feedforward networks, and existing implicit networks at a reduced computational cost.