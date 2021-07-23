
---
title: Image-Based Diagnosis of Chiari Disease
date: 2021-05-01
featured: false
tags: ["Summer 2021"]
---

Machine Learning for Chiari

<!--more-->

### Overview
Chiari malformation is a condition in which brain tissue extends into the spinal canal.  While it can be difficult to diagnose Chari  from  anatomical  images,  a  promising  direction  is  a  novel  functional  Magnetic Resonance Imaging (MRI) technique developed by Dr.  Oshinsky’s group (Dept.  of Radiology).  However,the large number of manual processing steps prohibit its use as a wide-spread screening tool.This  project  aims  at  exploring  the  use  of  machine  learning  algorithms  to  automize  parts  of the image processing pipeline,  most critically the segmentation of the image into different brain regions.  The teams will work with image data that has been collected and labeled by Dr.  Oshinski’s group in a previous research study.  The project is accessible to the team members since we can build  upon  recent  progress  and  software  made  in  image  processing  and  computervision and the image data is two-dimensional and of limited resolution, which enablesfast experimentation.  Despite this simplicity, the project allows us to investigate ML in a realistic setting and investigate the generalization properties and robustness of the approach.

![mainImage](img/ChiariExampleNHS.png "Chiari Malformation Example")

### Symptoms of Chiari Malformation 
Some of the symptoms include: 

- dizziness

- neck pain                 

- poor hand coordinatins                  

- severe headaches

- vision and speech problems 

### Segmentation Approaches for CHiari Malformation Type I 

### Atlas-Based Segementation
   The development of the atlas based image registration method involved primarily working with magnitudinal images. The final tool uses 51 of the magnitudinal images in a bank of templates to which a new reference can be compared to generate a mask for the template. In development of the method, references with known masks were used and similarity measures between known and predicted masks were calculated to inform the methods and parameters chosen.
   
![atlas-based-example](https://user-images.githubusercontent.com/85231953/126829418-afd0c524-cf3f-41bc-9518-dcd75480847b.png)

### Dice/Jaccard
![ssd-dice-scatter](https://user-images.githubusercontent.com/85231953/126829009-f49ec77b-439e-4986-bf61-3c4016f0df77.png)

### What is Machine Learning?
 The study of computer algorithms that improve automatically through experience and by the use of data.
  - U-Net: A Convolutional Neutral Network
  - Cross-Entrophy Loss
  - IBFGS Optimiztion
  - Experimental Setups 
 ![MachLearningDiagram](https://user-images.githubusercontent.com/85231953/126830267-2d826131-7b14-4a08-8c96-e7ca6912d5d9.jpg)

[UNet Arch Diagram.pdf](https://github.com/EmoryMLIP/emory-reu-ret-website/files/6870722/UNet.Arch.Diagram.pdf)

---
### Background

![mainImage](img/Chiari-Synergy.png "Chiari Synergy")

[Lars' Homepage](https://www.mathcs.emory.edu/~lruthot/)



