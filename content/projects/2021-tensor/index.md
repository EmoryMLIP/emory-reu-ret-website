---
title: Tensors for fMRI
date: 2021-05-01
featured: false
summary: 'Short summary of project to be shown on the front page.'
tags: ["Summer 2021"]
---



<!--more-->

### Overview
---
Can we look at a brain scan and know what the brain's owner is thinking?

Our research attempts to use computers to correctly classify brian scans into 2 groups, guessing what they are doing during the scan.

### Functional MRI
---
We use [brain scans called functional MRIs](https://en.wikipedia.org/wiki/Functional_magnetic_resonance_imaging) that show us which parts of the brain are using more oxygen and are therefore most active. [We have fMRIs of test subjects](http://www.cs.cmu.edu/afs/cs.cmu.edu/project/theo-81/www/)  who, as they are being scanned, are also shown either a picture or a sentence. If computers can classify these study subjects into one of these two categories by only studying their scans, then in a sense we can read their minds.


### Classification
---
Image classification is using a computer to figure what what an image represents.  Computers can't "see" images, so they use features of the images that it can understand.  For example, we can train a computer to match an image to a numerical digit.  Computers learn  by training on many images, for example [using the MNIST database of handwritten images](http://yann.lecun.com/exdb/mnist/).  MNIST contains a wide variety of images that can represent a 0 or a 1:

<img src="https://user-images.githubusercontent.com/50922545/126396168-5835463f-db60-417b-b4ab-5cc4d6e3b2ef.jpg" width="400" class="aligncenter"/>
<img src="https://user-images.githubusercontent.com/50922545/126396380-f4d0bedb-8a49-455c-bc15-1b73b01a77e5.jpg" width="400"/>


We call this first group Class 0 and the second Class 1. Using a tensor version of the singular value decomposition that we will elaborate upon later, we can construct something called a "basis", which can be thought of as a collection of the most important features shared by all of the images belonging to that class. Here are the bases for each of our classes: 

<img src="https://user-images.githubusercontent.com/50922545/127212660-d7520639-a8e6-4800-b78f-80901f6b7142.jpg" width="100"/>
<img src="https://user-images.githubusercontent.com/50922545/127212640-afe7cd85-5495-4f43-bc67-3a9a1fe4f9aa.jpg" width="100"/>
<img src="https://user-images.githubusercontent.com/50922545/127212651-8047b39b-5aa1-45f7-b0d6-c5fa1f0b986c.jpg" width="100"/>



We see that the basis for Class 0 shows more curved features, while the basis for Class 1 contains traces of more straight and vertical features. When we have a test image of a handwritten digit and want to see if this mathematical method can figure out if it is a 0 or a 1, we compute something called a "projection", which mathematically projects our test image into that basis. Below is an example:

PUT IMAGES HERE

As humans, we clearly know that our test image is a 1. In the projection onto the basis for Class 0, we see some differences and inconsistencies in the image, but we get a nice match in the projection onto the basis for Class 1. Computing this projection shows that the "distance" between our test image and our two classes is smaller for Class 1 than for Class 0, and so our method classifies our test image as a 1. In our project, we extend this method to fMRI, but instead of having classes for zeros and ones, we classify whether or not a test fMRI corresponds to the human subject reading a sentence or viewing a picture. 

By learning from a training set of images a computer can examine the data in a new image and figure out which digit it most resembles.  

We are training our computer to learn how to use the data in an fMRI to classify our study subjects into those who are shown an image and those who are shown a sentence.  Unlike static MRIs which take a scan at one point in time, fMRIs are repeated every few seconds creating a series of images for each trial. 

Here is an example of an fMRI of one brain during one trial.  The different images are of different slices of the brain.  The abbreviations on the right refer to brain regions, for example "SMA" stands for "Supplementary Motor Area" located at the top center of the head.  

<img src="img/brain1.jpg" alt="brain1" width="400"/>

[Here is a link to our code](https://github.com/elizabethnewman/tensor-fmri) stored in the github repository.  


Images like these consist of 3-dimensional pixels called voxels, and the data are numbers representing colors.  Typically, large data sets like this are stored in matrices, which have some powerful tools for extracting the most relevant components.  Matrices make it easy for   [computers to learn from data.](https://youtu.be/LlKAna21fLE)

If we have 3-dimensional fMRI brain voxel data for many patients, multiple scans in sequence, then we need to analyze a quantity of data unwieldy even for modern computers.  

When we store fMRI data in a matrix we lose important relationships between the data points.  For example a computer may not know that a particular voxel representing a part of the brain at one moment is that same part of the brain a few seconds later.    

Fortunately we can also store our data in a different mathematical structure called a tensor.  A tensor is like matrix but with more than 2 dimensions.  Our tensor of fMRIs have a total of 5 dimensions, shown in the figure below.  The green slices consist of voxels of the brain in 3 spatial dimensions: x,y,z (yellow).  For each trial multiple images are taken over several seconds (blue), and there are multiple trials (red).  

<img width="600" alt="fmri_tensors" src="https://user-images.githubusercontent.com/50922545/125823220-5141e5bd-206c-4cd2-8dc7-5f082c475702.png">

When we store our voxel data in tensors instead of matrices, we retain all the information about the 3 dimensional location in the brain, the sequence of the image in time, and the trial.  Now we want to decompose our tensor data using a method analogous to the way [matrices can be decomposed](https://www.youtube.com/watch?v=DG7YTlGnCEo), so we can use far less data and still extract an accurate prediction of what the subject is thinking.  In matrices this is called Singular Value Decomposition; we call our approach tensor-SVD or tSVD.  

Here is a diagram of matrix decomposition using SVD:

<img width="500"  src="https://user-images.githubusercontent.com/50922545/126017121-bd017e2c-7fa1-4d23-8989-c0b69dbbbdf3.jpg">


This what we imagine a tensor SVD would be:


<img width="500"  src="https://user-images.githubusercontent.com/50922545/126017399-7151b4e8-c292-4d34-a1a6-20a7181d6824.png">


You'll notice that we use matrix multiplication in working with matrix SVDs.  What would tensor multiplication look like?  This is what we are trying to figure out.  



Our research is not only useful for fMRIs; many datasets have multiple dimensions.  Streaming entertaining companies have data on thousands of viewers and what movies they've watched.  Hospitals track thousands of patients, each of whom has had multiple lab tests and other studies.  If our research enables us to classify our fMRI subjects, then we may also be able to predict whether someone will want to watch Terminator, or whether a patient is likely to have cancer.  


If you already know python [here is a link to our code](https://github.com/elizabethnewman/tensor-fmri) that we run to test

### Further Reading
For more technical background information 

[Tensor tensor products with invertible linear transforms](https://www.sciencedirect.com/science/article/pii/S0024379515004358)

[Tensor-tensor algebra for optimal representation and compression of multiway data](https://www.pnas.org/content/118/28/e2015851118.short)

[Tensor decompositions and applications](http://www.kolda.net/publication/koba09/)

[Image classification using local tensor singular value decompositions](https://arxiv.org/pdf/1706.09693.pdf)


---


### Singular Value Decomposition







