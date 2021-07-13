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

We use brain scans called functional MRIs (fMRIs) that show us which parts of the brain are using more oxygen and are therefore most active. [We have fMRIs for hundreds of patients](http://www.cs.cmu.edu/afs/cs.cmu.edu/project/theo-81/www/) who, as they are being scanned, are also shown either a picture or a sentence. If computers can classify these study subjects into one of these two categories by only studying their scans, then in a sense we can read their minds.

Unlike static MRIs which take a scan at one point in time, fMRIs are repeated every few seconds creating a series of images for each trial. 


Here is an example of an fMRI.  
![mainImage](img/brain1.jpg "brain1")


We store the fMRI images digitally as individual 3-dimensional pixels called voxels.  [_Emory_REU_RET__Summer_2021__Tensor_fMRI_Presentation.pdf](https://github.com/EmoryMLIP/emory-reu-ret-website/files/6812415/_Emory_REU_RET__Summer_2021__Tensor_fMRI_Presentation.pdf)
[_Emory_REU_RET__Summer_2021__Tensor_fMRI_Presentation.pdf](https://github.com/EmoryMLIP/emory-reu-ret-website/files/6812443/_Emory_REU_RET__Summer_2021__Tensor_fMRI_Presentation.pdf)
If we have fMRI voxel data for hundreds of patients, multiple scans, 3-dimensional brain data, over time, then we need to analyze an unwieldy amount of data even for modern computers.  And it turns out that we may not need every single data point, but only a representative sample.  
Storing that data in traditional matrices is useful because we can use techniques like singular value decomposition to streamline the data without losing important information.

If you aren't sure how matrices can help computers to learn, [watch this video](https://youtu.be/LlKAna21fLE).

If you are not familiar with Singular Value Decompositon,  [watch this video](https://www.youtube.com/watch?v=DG7YTlGnCEo).  

But when we store fMRI data as matrices we lose important relationships which are maintained in a tensor.  A tensor is like matrix but with more than 2 dimensions.  The tensors we study have a total of 5 dimensions.  Three dimensions correspond to the physical 3 dimensions of the brain itself.  The fourth dimension represents the sequence of brain images taken over time.  The fifth dimension represents the many trials of test subjects that are studied.  You can see how the number of data points is very large.  

***how large?***

We are looking for a way to decompose our tensor data in a way analogous to the way matrices can be decomposed, so we can use far less data and still extract an accurate prediction of what the subject is thinking.

Our research is not only useful for fMRIs; many datasets have multiple dimensions.  Streaming entertaining companies have data on thousands of viewers and what movies they've watched.  Hospitals track thousands of patients, each of whom has had multiple lab tests and other studies.  If our research enables us to classify our fMRI subjects, then we may also be able to predict whether someone will want to watch Terminator, or whether a patient is likely to have cancer.  





---
### Background



Functional Magnetic Resonance Imaging (fMRI) gives us pictures of the brain like the following:


{{< figure src="img/brain1.jpg" caption="Regions of Interest (ROIs) for the [StarPlus fMRI data](http://www.cs.cmu.edu/afs/cs.cmu.edu/project/theo-81/www/) from Carnegie Mellon University." alt="brainROI">}}




