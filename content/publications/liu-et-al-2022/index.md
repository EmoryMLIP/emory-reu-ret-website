---
# Documentation: https://wowchemy.com/docs/managing-content/

title: Solving Inverse Problems Using Implicit Networks and Jacobian-free Backpropagation
subtitle: ''
summary: ''
authors:
- Linghai Liu
- Shuaicheng Tong
- Lisa Zhao
- Samy Wu Fung
tags: []
categories: []
date: '2022-07-26'
lastmod: 2022-07-26T16:45:31-04:00
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
publishDate: '2022-07-26'
publication_types: 1
abstract: 'Recent efforts in applying implicit networks to solve inverse problems in imaging have achieved competitive or even better results when compared with feedforward networks. Moreover, they require less memory and can theoretically be of infinite depth. However, implicit networks are not necessarily easy to train with their fixed point due to the presence and computation of a large linear system. This paper introduces Jacobian-free Backpropagation (JFB), a fast and easy-to-implement scheme for backpropagation that circumvents such calculation and is applicable to image deblurring tasks. Our results show that JFB is effective and gives competitive results against fine-tuned optimization schemes, state-of-the-art (SOTA) feedforward methods, and existing implicit networks.'
pages : '15 pages'
url_preprint : 'https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiEsrzd-uX-AhWrk2oFHbvlAEkQFnoECAwQAQ&url=http%3A%2F%2Fwww.math.emory.edu%2Fsite%2Fcmds-reuret%2Fprojects%2F2022-implicit%2FManuscript_JFB.pdf&usg=AOvVaw3e9QN82Bo8qHdkE4Wq0qPO'
url_code : ' https://github.com/lliu58b/Jacobian-free-Backprop-Implicit-Networks'
---

Recent efforts in applying implicit networks to solve inverse problems in imaging have achieved competitive or even better results when compared with feedforward networks. Moreover, they require less memory and can theoretically be of infinite depth. However, implicit networks are not necessarily easy to train with their fixed point due to the presence and computation of a large linear system. This paper introduces Jacobian-free Backpropagation (JFB), a fast and easy-to-implement scheme for backpropagation that circumvents such calculation and is applicable to image deblurring tasks. Our results show that JFB is effective and gives competitive results against fine-tuned optimization schemes, state-of-the-art (SOTA) feedforward methods, and existing implicit networks.