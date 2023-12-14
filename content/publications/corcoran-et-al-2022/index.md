---
# Documentation: https://wowchemy.com/docs/managing-content/

title: Ensemble Kalman Filtering for Glacier Modeling
subtitle: ''
summary: ''
authors:
- Emily Corcoran
- Logan Knudsen
- Hannah Park-Kaufmann
tags: []
categories: []
date: '2022-12-01'
lastmod: 2022-12-01T16:45:31-04:00
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
publishDate: '2022-12-01T20:45:31.467151Z'
publication_types: 1
abstract: 'Working with a two-stage ice sheet model, we explore how statistical data assimilation methods can be used to improve predictions of glacier melt and relatedly, sea level rise. We find that the EnKF improves model runs initialized using incorrect initial conditions or parameters, providing us with better models of future glacier melt. We explore the necessary number of observations needed to produce an accurate model run. Further, we determine that the deviations from the truth in output that stem from having few data points in the pre-satellite era can be corrected with modern observation data. Finally, using data derived from our improved model we calculate sea level rise and model storm surges to understand the affect caused by sea level rise.'
pages : '15 pages'
url_preprint : 'https://arxiv.org/pdf/2210.02647.pdf'
url_code : ' https://github.com/hakuupi/StormSurge'
---

Working with a two-stage ice sheet model, we explore how statistical data assimilation methods can be used to improve predictions of glacier melt and relatedly, sea level rise. We find that the EnKF improves model runs initialized using incorrect initial conditions or parameters, providing us with better models of future glacier melt. We explore the necessary number of observations needed to produce an accurate model run. Further, we determine that the deviations from the truth in output that stem from having few data points in the pre-satellite era can be corrected with modern observation data. Finally, using data derived from our improved model we calculate sea level rise and model storm surges to understand the affect caused by sea level rise.