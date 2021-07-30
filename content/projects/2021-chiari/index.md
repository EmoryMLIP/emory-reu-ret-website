---
title: Image-Based Diagnosis of Chiari Disease
date: 2021-05-01
featured: true
summary: 'Our group explored two methods - a machine learning method and an atlas-based image registration method - to automatically identify the cerebellum and brain stem from a given magnetic resonance image (MRI).  The machine learning method uses convolutional neural networks to learn how to identify features of the MR images, while the atlas based method uses a known brain as a kind of "road map" to find the two regions of interest.  Once the two areas are were identified, we can look at DENSE MRI data - that tell us how much movement occurs in the brain when a subject's heart beats - to compute the average displacement of the patient's cerebellum and brain stem, which can help determine whether or not a subject has a Chiari Malformation.  We compared the strengths and weaknesses of both methods, and how they might work in the future to make Chiari diagnosis cheaper and more efficient.'
tags: ["Summer 2021","Machine Learning","Image Registration","Convolutional Neural Networks", "Atlas-Based Image Registration","Chiari","Diagnosis"]
---

**Emory University Summer 2021 REU/RET**
# Undergraduate students and teacher collaborate on effective segmentation methods to determine patients with Chiari Malformation.

---
### Collaboration Never Sleeps. 
 During our summer research at Emory University 2021 REU/RET program, our project focused on the algorithmic diagnosis of Chiari malformation from DENSE MRIs.  We created an algorithm that can accurately and efficiently segment the cerebellum and brain stem from a magnitudinal image and use displacement data to classify whether or not a patient has the Chiari malformation.  In doing so, we investigated two approaches; one that segments the given image by aligning and comparing the image to a known atlas and another that segments through deep learning.
 
### Did Somebody Say Chiari Malformation?
Chiari malformation is a condition in which brain tissue extends into the spinal canal.  While it can be difficult to diagnose Chari  from  anatomical  images,  a  promising  new direction for diagnosis is a novel functional Magnetic Resonance Imaging (MRI) technique developed by Dr.  Oshinsky’s group (Emory's Dept.  of Radiology).  However, the large number of manual processing steps prohibit its use as a wide-spread screening tool.  This  project  aims  at  exploring  the  use  of  machine  learning  algorithms  to  automize  parts  of the image processing pipeline, most critically the segmentation of the image into different brain regions.  The teams worked with image data that has been collected and labeled by Dr.  Oshinski’s group in a previous research study.  The project is accessible to the team members since we can build  upon  recent  progress  and  software  made  in  image  processing  and  computer vision and the image data is two-dimensional and of limited resolution, which enables fast experimentation.  Despite this simplicity, the project allows us to investigate ML in a realistic setting and investigate the generalization properties and robustness of the approach.

![mainImage](img/Chiari-Synergy.png "Chiari Synergy")

---
### Time Management is Everything! 
 Week 1: 
 - During our first week, we created a working atlas-based image registration example, using FAIR: a MATLAB image registration toolset.  We also began to look at the Machine Learning method, where we used PyTorch. We noticed the Machine Learning process would require adding more time to focus on our research topic and wanted to ensure we utilize our time wisely. 
   
 
 Week 2 
 -  We set a goal to finish the first atlas-based example and begin applying others examples to our project. After working on our atlas-based examples, we begin to look at the machine learning process and create multiple examples for our research. As we explored the machine learning process, we used four different methods: convolutional neural network, cross-entropy loss, lBFGS optimization, and experimental setup. 

 
 Week 3 
- Begin working on midterm presentation
- Finish applying atlas method to remaining examples
- Continue with Machine Learning 
       
 Week 4 
- Work on classification based on our found segmentation
- Continue with Machine Learning and decide its viability
        
 Week 5 
- Finish up with preferred method(s) (Atlas/Machine Learning)
- Begin working on poster and outlining research paper
    
Week 6 
- Construct website and work on manuscript           
---

### Leave the SEGMENTATION to US!


### Atlas Based Image Registration vs Machine Learning. 


### Additional information to learn about Atlas-Based Image Registration and Machine Learning
What is Atlas-Based Learning? - (Information sheet or video) 
[What is Machine Learning?](https://youtu.be/QghjaS0WQQU)

---
### The Deliverables of Confidence 


---
### Chiari Creations
-[Research Paper](.ResearchPaper.md)

-[Presentation](https://github.com/EmoryMLIP/emory-reu-ret-website/blob/f5a9de7a766a012b8202acd87ac4c427d2ec2016/content/projects/2021-chiari/Chiari_Disease_Presentation%20(2).pdf)

-[Poster Blitz](https://youtu.be/tdjXj3JdpQU)

---
### Meet the Team
-[Bios](https://github.com/EmoryMLIP/emory-reu-ret-website/blob/72789f2938cc9b40d8a2c55fa3e46f7d455ace46/content/projects/2021-chiari/Bios)

### Dr. Lars Ruthotto Homepage

[Lars' Homepage](https://www.mathcs.emory.edu/~lruthot/)




