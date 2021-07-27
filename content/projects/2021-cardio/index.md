---
title: From Images to Patient-Specific Models in Cardiology
date: 2021-05-01
featured: true
summary: 'Short summary of project to be shown on the front page.'
tags: ["Summer 2021"]
---



<!--more-->
---
# Mathematically Modeling from the Heart <!--Header-->

## Introduction:
The role of mathematical modeling in clinics is particularly evident in cardiology, as computational mechanics for many historical reasons is a mature field of applied mathematics; on the other hand, many important cardiovascular pathologies have a significant mechanical component, in terms of fluid, structure and their interactions. The clinical impact of mathematical models strongly relies on reconstructing patient geometries to customize and personalize numerical simulations. Advances in medical image processing made over the last two decades have enabled virtual patient-specific models. A key step of the processing pipeline in Cardiology is the extraction of complex vascular geometries like an aortic dissection from medical images (typically, Computed Tomographies, Magnetic Resonance, and Optical Coherence Tomography). The team will discover the relation between PDEs and image segmentation/reconstruction through the level set method, and compare this segmentation approach with deep learning ones based on Convolutional Neural Networks. 

## Project Overview:
Imaging has been revolutionizing medical research and clinical practices for decades. One of the components of medical image processing is “segmentation” which has a wide range of applications. Image segmentation can be defined as the task of deriving the shape of an object from a 2D or 3D image. Segmentation is the image processing step to identify a region of interest (an artery, a bone, etc.) in an image.It suggests that the pixels of an image are partitioned into classes based on the object they belong to in regards to the background. There is not a typical segmentation method that works equally and automatically for all segmentation tasks. In fact, there are many different approaches available. In our research project, we focus on medical images, specifically coronaries based on Optical coherence tomography (OCT). OCT image segmentation is initiated on retinal OCT to localize the intra-retinal boundaries. The broader impact of OCT segmentation in clinical applications offers a tool for greater evaluations of layers and boundaries to allow for better diagnosis and treatment (Lucid, Heartlfow companies that reconstruct the coronaries arteries-this is the effect of segmentation). Using OCT images provided by the Emory School of Medicine, we analyzed two segmentation approaches: the Level-Set Method and Machine Learning based on CNN (Convolutional Neural Networks). Our project aimed at segmenting coronaries based on the OCT images using these two methods. We were able to compare the results of deterministic image-segmentation methods vs deep learning ones. 

<!--Image-->
![mainImage](img/cardio1.jpg "Heart")



<!--Starting new section-->
# Methods and Materials <!--Header-->

## Level Set Methods and VMTK:
The Level Set Method utilizes implicit functions to identify the region of interest in an image, where the implicit function is the numerical solution of a Partial Differential Equation (PDE) that is defined on the image that is being segmented.\cite{cite:1} The basic idea of the Level Set is to correlate the velocity to the gray level of the image in such a way that the gray level of the image is driving the evolution of the phi close to the boundary. The Level Set is a very powerful method that extracts the border of a region or image, and it can handle changing topology well. It is also a great tool because it utilizes physical concepts, such as velocity, mean curvature, and elastic energy for image segmentation problems. We used the image segmentation software, Vascular Modeling ToolKit (VMTK), that is based on the Level Set. VMTK is a collection of tools and libraries for image-based modeling of medical images. This segmentation method is model-driven, meaning that the technique is established on physical concepts of the problem.\cite{cite:2}
<!--Insert Image Here-->

## FEniCS and MATLAB:
The FEniCS Project is a research and software project aimed at creating mathematical methods and software for automated computational mathematical modeling. As the implicit function, the numerical solution of a PDE that is defined on the image that is being segmented, is involved in our project, FEniCS means creating easy, intuitive, efficient, and flexible software for solving PDEs using finite element methods. For MATLAB, Image Processing Toolbox provides a comprehensive set of reference-standard algorithms and workflow apps for image segmentation. Particularly, Volume Segmentor is applied to segment 3-D grayscale or RGB volumetric images. By means of automated, semi-automated, and manual techniques, Volume Segmentor is applied to create and refine a binary or semantic segmentation mask for a 3-D grayscale or an RGB image.
<!--Insert Image Here-->

## Convolutional Neural Networks (CNNs):
Convolutional Neural Networks are a deep learning algorithm for image classification. The CNN's convolutional layer parameters comprise of filters, where the values of the filters are learned during the training phase. The layers are for feature learning and classification, specifically for classifying the pixels in an image with respect to a background or vessel. We used the image processing software, PyTorch. The deep learning (DL) based method involves using training data to train the algorithm in PyTorch. This segmentation method is data-driven, meaning that the technique is established on the training of the neural network on databases of images.
<!--Insert Image Here-->

## Data Sets:
Could insert text here about this or show images.
<!--Insert Image Here (possibly of original OCT data set-->





<!--Starting new section-->
# Our Activities & Experiences <!--Header-->

