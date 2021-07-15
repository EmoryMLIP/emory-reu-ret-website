---
title: Tensors for fMRI
date: 2021-05-01
featured: false
tags: ["Summer 2021"]
---

<p align="center">
Understanding the human brain by extracting multidimensional information.

 
<img width="200" height="100" src="img/tensor_neuroimaging_draft1.jpg">
</p>


<!--more-->

### Overview
Can we look at a brain scan and know what the brain's owner is thinking?

We use brain scans called functional MRIs (fMRIs) that show us which parts of the brain are using more oxygen and are therefore most active. [We have fMRIs of test subjects](http://www.cs.cmu.edu/afs/cs.cmu.edu/project/theo-81/www/)  who, as they are being scanned, are also shown either a picture or a sentence. If computers can classify these study subjects into one of these two categories by only studying their scans, then in a sense we can read their minds.

Unlike static MRIs which take a scan at one point in time, fMRIs are repeated every few seconds creating a series of images for each trial. 


Here is an example of an fMRI of one brain during one trial.  The different images are of different slices of the brain.  The abbreviations on the right refer to brain regions, for example "SMA" stands for "Supplementary Motor Area" located at the top center of the organ.  
![mainImage](img/brain1.jpg "brain1")


Images like these consist of 3-dimensional pixels called voxels.  Typically, large data sets like this are stored in matrices, which have some powerful tools for extracting the most relevant components.  This makes it easy for   [computers to learn from data stored in matrices.](https://youtu.be/LlKAna21fLE)

If we have 3-dimensional fMRI brain voxel data for many patients, multiple scans in sequence, then we need to analyze a quantity of data unwieldy even for modern computers.  

When we store fMRI data in a matrix we also lose important relationships between the data points.  For example a computer may not know that a particular voxel representing a part of the brain is that same part of the brain a few seconds later.    

Fortunately we can also store our data in a mathematical structure called a tensor.  A tensor is like matrix but with more than 2 dimensions.  Our tensor of fMRIs have a total of 5 dimensions, shown in the figure below.  The green slices consist of voxels of the brain in 3 dimensions: x,y,z in yellow.  For each trial multiple images are taken over several seconds (blue arrow), and there were multiple trials (red arrow).  

<img width="968" alt="fmri_tensors" src="https://user-images.githubusercontent.com/50922545/125823220-5141e5bd-206c-4cd2-8dc7-5f082c475702.png">

We want to decompose our tensor data using a method analogous to the way [matrices can be decomposed](https://www.youtube.com/watch?v=DG7YTlGnCEo), so we can use far less data and still extract an accurate prediction of what the subject is thinking.

Our research is not only useful for fMRIs; many datasets have multiple dimensions.  Streaming entertaining companies have data on thousands of viewers and what movies they've watched.  Hospitals track thousands of patients, each of whom has had multiple lab tests and other studies.  If our research enables us to classify our fMRI subjects, then we may also be able to predict whether someone will want to watch Terminator, or whether a patient is likely to have cancer.  





---
### Background



Functional Magnetic Resonance Imaging (fMRI) gives us pictures of the brain like the following:


{{< figure src="img/brain1.jpg" caption="Regions of Interest (ROIs) for the [StarPlus fMRI data](http://www.cs.cmu.edu/afs/cs.cmu.edu/project/theo-81/www/) from Carnegie Mellon University." alt="brainROI">}}



