---
title: From Images to Patient-Specific Models in Cardiology
date: 2021-05-01
featured: true
summary: 'Short summary of project to be shown on the front page.'
tags: ["Summer 2021"]
---



<!--more-->
---
# Emory REU Cardiology Project: Comparison of Segmentation Techniques  <!--Our title-->

<!--Starting new section-->
---
# Mathematically Modeling from the Heart <!--Header-->
### Introduction:
The role of mathematical modeling in clinics is particularly evident in cardiology, as computational mechanics for many historical reasons is a mature field of applied mathematics; on the other hand, many important cardiovascular pathologies have a significant mechanical component, in terms of fluid, structure and their interactions. The clinical impact of mathematical models strongly relies on reconstructing patient geometries to customize and personalize numerical simulations. Advances in medical image processing made over the last two decades have enabled virtual patient-specific models. A key step of the processing pipeline in Cardiology is the extraction of complex vascular geometries like an aortic dissection from medical images (typically, Computed Tomographies, Magnetic Resonance, and Optical Coherence Tomography). The team will discover the relation between PDEs and image segmentation/reconstruction through the level set method, and compare this segmentation approach with deep learning ones based on Convolutional Neural Networks. 
<!--Image-->
![mainImage](img/cardio1.jpg "Heart")

### Project Overview:
Imaging has been revolutionizing medical research and clinical practices for decades. One of the components of medical image processing is “segmentation” which has a wide range of applications. Image segmentation can be defined as the task of deriving the shape of an object from a 2D or 3D image. Segmentation is the image processing step to identify a region of interest (an artery, a bone, etc.) in an image.It suggests that the pixels of an image are partitioned into classes based on the object they belong to in regards to the background. There is not a typical segmentation method that works equally and automatically for all segmentation tasks. In fact, there are many different approaches available. In our research project, we focus on medical images, specifically coronaries based on Optical coherence tomography (OCT). OCT image segmentation is initiated on retinal OCT to localize the intra-retinal boundaries. The broader impact of OCT segmentation in clinical applications offers a tool for greater evaluations of layers and boundaries to allow for better diagnosis and treatment (Lucid, Heartlfow companies that reconstruct the coronaries arteries-this is the effect of segmentation). Using OCT images provided by the Emory School of Medicine, we analyzed two segmentation approaches: the Level-Set Method and Machine Learning based on CNN (Convolutional Neural Networks). Our project aimed at segmenting coronaries based on the OCT images using these two methods. We were able to compare the results of deterministic image-segmentation methods vs deep learning ones. 
<!--Image-->
![mainImage](img/Picture1.png "Picture1")




<!--Starting new section-->
---
# Methods and Materials <!--Header-->
### Level Set Methods and VMTK:
The Level Set Method utilizes implicit functions to identify the region of interest in an image, where the implicit function is the numerical solution of a Partial Differential Equation (PDE) that is defined on the image that is being segmented.\cite{cite:1} The basic idea of the Level Set is to correlate the velocity to the gray level of the image in such a way that the gray level of the image is driving the evolution of the phi close to the boundary. The Level Set is a very powerful method that extracts the border of a region or image, and it can handle changing topology well. It is also a great tool because it utilizes physical concepts, such as velocity, mean curvature, and elastic energy for image segmentation problems. We used the image segmentation software, Vascular Modeling ToolKit (VMTK), that is based on the Level Set. VMTK is a collection of tools and libraries for image-based modeling of medical images. This segmentation method is model-driven, meaning that the technique is established on physical concepts of the problem.\cite{cite:2}
<!--Insert Image or math equations Here-->

### FEniCS and MATLAB:
The FEniCS Project is a research and software project aimed at creating mathematical methods and software for automated computational mathematical modeling. As the implicit function, the numerical solution of a PDE that is defined on the image that is being segmented, is involved in our project, FEniCS means creating easy, intuitive, efficient, and flexible software for solving PDEs using finite element methods. For MATLAB, Image Processing Toolbox provides a comprehensive set of reference-standard algorithms and workflow apps for image segmentation. Particularly, Volume Segmentor is applied to segment 3-D grayscale or RGB volumetric images. By means of automated, semi-automated, and manual techniques, Volume Segmentor is applied to create and refine a binary or semantic segmentation mask for a 3-D grayscale or an RGB image.
<!--Insert Image or math equations Here-->

### Convolutional Neural Networks (CNNs):
Convolutional Neural Networks are a deep learning algorithm for image classification. The CNN's convolutional layer parameters comprise of filters, where the values of the filters are learned during the training phase. The layers are for feature learning and classification, specifically for classifying the pixels in an image with respect to a background or vessel. We used the image processing software, PyTorch. The deep learning (DL) based method involves using training data to train the algorithm in PyTorch. This segmentation method is data-driven, meaning that the technique is established on the training of the neural network on databases of images.
<!--Insert Image Here-->




<!--Starting new section-->
---
# Our Activities & Experiences <!--Header-->
### Research Week 1 and 2:
Using CNNs we generated OCT segmentation maps in PyTorch on the original data provided by Dr. Molony.  
The same data were used in VMTK slice by slice. 

### Research Week 3:
We added 15 new images to our OCT data set in PyTorch. With more training data, the loss value went down, and the accuracy increased. We worked to find the most accurate segmentation process in VMTK to  extract the level set for the boundary of the coronary. We cleaned a sample image using GIMP. To create a 3D stack of images, each slice was replicated 30 times. After extracting the surface in VMTK, ParaView extracted the outline of the region. We were then in a good position to start comparing the contours from the two methods.

### Research Week 4:
We  explored different metrics for comparing the results visually and numerically. One option is the Jaccard Index, which quantifies the percent overlap between the segmented images. Another option was to extract the VMTK and PyTorch contour lines and boundary points in ParaView and then use Python or Matlab code to plot the x and y coordinates of the results as overlapping figures. Then, we could use integration to calculate the difference between the two curves (L^2 metrics) .
<!--Insert Image Here about our activities if we want-->


<!--Starting new section-->
---
# Comparison <!--Header-->
### Which method was faster?
The deep learning method was much faster than VMTK, but it still required a waiting period to complete the epochs. This might be because our training data and development data was relatively small. We came to recognize that a limitation of the deep learning approach was that labeled and large data sets are required for preventing CNN overfitting and increasing accuracy.

### Which method required more human intervention?
VMTK segmentation required far more human intervention than the DL method.  With VMTK, we had to initialize the image by selecting an initialization type, identifying a lower and upper threshold of pixel values, and placing seeds that identified the region we planned to segment. We also selected the numerical values for the level set conditions, including number of iterations, propagation, curvature, and advection. We actively supervised the segmentation and chose whether to accept or reject the results.  On the other hand, the DL method required much less decision making. With the DL algorithm, we empirically set a few parameters associated with training the CNN, such as training rate and number of epochs. Then,the DL algorithm trained itself and segmented the OCT images without user participation. 

### Other advantages and limitations?
PyTorch is better at handling noise suppression than VMTK. On the other hand, VMTK handles the data normalization, contrast enhancement, and conversion of color images to grayscale better.
<!--Insert Comparison Visualizatoin/Implementation Image Here-->



<!--Starting new section-->
---
# Our Results & Conclusions <!--Header-->
After evaluating the benefits and limitations of both methods, we have come to the conclusion that instead of preferring one over the other, we can combine the two for better results. We could train a neural network with an optimal parameter selection to use in VMTK segmentation for setting the parameters. We can have a CNN trained on the OCT data to tell us what the correct parameter set is. This could prove to be useful, especially since we encountered a set-back in determining the initialization type, thresholds, and parameters to set for the best segmentation result in VMTK. We should not have a competition over the two techniques, rather, we should combine the strengths and benefits of both \textbf{models} and \textbf{data}. 

Future works should focus on improved segmentation using unsupervised Deep Learning where the machine uses image-derived features, or supervised learning that requires Gold Standard (GS) segmentation to train it. The deep learning-based algorithm demonstrated high accuracy based on Jaccard Index. We should look into Edge-based deformable models, and approaches using blood vessel tracking algorithms and seeding points to find the minimum path according to image-derived metrics. 
<!--Insert Image Here-->



<!--Starting new section-->
---
# Additional Information & Materials <!--Header-->
1. Cardiology Presentation Slides (attach link)
2. Poster Blitz (attach link)
3. Poster (attach link)
4. Codes 
   1. PyTorch (attack link)
   1. Python and MATLAB codes used for comparison (attack link)
   2. FEniCS (attach link)



<!--Starting new section-->
---
# Get to know our team! <!--Header-->
* Minxing (Matt) Zhang, 
* Shannon Lee, Southern Methodist University
* Kai Chang, Emory  
* Allison Dennis, Texas A&M University
* Mohamad Hindawi, Tucker High School 
* Michele Perry, University of South Alabama 








