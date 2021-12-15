---
# Documentation: https://wowchemy.com/docs/managing-content/

title: Comparison of atlas-based and neural-network-based semantic segmentation for DENSE MRI images
subtitle: ''
summary: ''
authors:
- Elle Buser
- Emma Hart
- Ben Huenemann
tags: []
categories: []
date: '2021-09-29'
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
publishDate: '2021-09-29T20:45:31.467151Z'
publication_types:
- 3
abstract: 'Two segmentation methods, one atlas-based and one neural-network-based, were compared to see how well they can each automatically segment the brain stem and cerebellum in Displacement Encoding with Stimulated Echoes Magnetic Resonance Imaging (DENSE-MRI) data. The segmentation is a pre-requisite for estimating the average displacements in these regions, which have recently been proposed as biomarkers in the diagnosis of Chiari Malformation type I (CMI). In numerical experiments, the segmentations of both methods were similar to manual segmentations provided by trained experts. It was found that, overall, the neural-network-based method alone produced more accurate segmentations than the atlas-based method did alone, but that a combination of the two methods -- in which the atlas-based method is used for the segmentation of the brain stem and the neural-network is used for the segmentation of the cerebellum -- may be the most successful. '
pages : 23 pages
publication: '*arXiv preprint 2109.14116*'
url_pdf : 'https://arxiv.org/pdf/2109.14116'
url_video : 'https://www.youtube.com/watch?v=tdjXj3JdpQU&t=2s'
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/tdjXj3JdpQU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
