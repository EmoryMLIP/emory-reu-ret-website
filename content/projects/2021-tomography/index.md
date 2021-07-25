**REU/RET Emory University**
# New algorithm helps make portable CT machine images clearer.
*Mathematics: College students and math teachers have developed a new, better way of improving image resolution with mathematical methods.* 

![Portable Device](https://user-images.githubusercontent.com/84742324/126884202-538cc1b4-04f1-4acf-a83b-5f618de46056.jpg)

Research work done at the 2021 REU/RET summer program at Emory University has proven a way to make medical diagnoses more effectively. The work behind this new way relies heavily upon mathematical techniques that connect linear algebra with numerical and optimization methods. 

The research work done is a collaborative effort between a group of students and teachers. This truly has opened up numerous possibilities for the REU/RET Emory Program, which has been seeking to explore new approaches to analyze imaging data -for example, image reconstruction -to produce better quality images.   

Some of the most important aspects of this work focuses on setting up a linear least squares problem, to which the solution may be approximated  by  using  an alternating descent scheme known as block coordinate descent or (BCD). They also find the solution to the non-linear least squares problem by using imfil and the MATLAB function, lsqnonlin.  

The results obtained from their work have offered other students mathematicians a different way to study these problems and possibly radiology doctors an efficient way to accurately diagnose illnesses and keep saving patients' lives. This work has been one of the most interesting pieces of work ever accomplished because CT images in portable devices are a lot clearer. 

![ZoomINOUt](https://user-images.githubusercontent.com/84742324/126884324-8cfa15ae-0fe2-4945-8530-4f1d2918785e.jpg)

# Saving People’s Lives: COVID-19
The 2021 REU/RET Emory program focuses on computational mathematics and its applications in data science.The research goal of the Point-of-Care Tomographic Imaging group is to develop numerical methods to jointly estimate the geometry parameters of portable CT scan devices to reconstruct an image. The mathematical ideas involved in this project are of great importance. With these mathematical methods, imaging becomes a possibility to patients in all parts of the world allowing them to live a healthy and happy life.   

The medical field depends greatly on imaging methods. In  medical  imaging,  computed  tomography  (CT)  techniques  are  becoming  more  and  more  popular  for  their ability to produce high quality images of the human body.  The COVID-19 pandemic brought challenges and setbacks to many doctors around the world  and imaging played a vital role in helping diagnose the virus. Doctors have been able to use CT scans to diagnose COVID-19, examine the lungs in patients, who were at high risk of infection, and those recovered from the virus.  

CT methods use a combination of computer processes and mathematics to reconstruct images. Many mathematicians have influenced this field of computed tomography, including Johann Radon; Allan McLeod Cormack and Godfrey Newbold Hounsfield developed the first scanning device.  

![COVID-19](https://user-images.githubusercontent.com/84742324/126884217-ccaf8e58-305f-4824-9fb8-5ada4f58da30.jpg)


# Point-of-Care Tomographic Imaging

A CT scanner is a device that is composed of a scanning gantry, x-ray generator, computer system, console panel and a physician’s viewing console. The scanning gantry is the part that will produce and detect x-rays. In a typical CT scan, a patient lays on a bed that would move through the gantry. An X-ray tube rotates around the patient and shoots X-ray beams through the human body at different angles. These X-ray measurements are then processed on a computer using mathematical algorithms to create tomographic(cross-sectional) images of the tissues inside the body. [How Does a CT Scan Work?](https://youtu.be/l9swbAtRRbg)

Two parameters that are associated with the geometry of portable CT scanning devices are: 1) R - distance between source and detector and 2) θ - orientation of source to detector. In point-of-care imaging, these parameters are essential during the data imaging process, as they may possibly change when the CT scanner is adjusted.

![MultipleRow Detector](https://user-images.githubusercontent.com/84742324/126884377-8af7b40d-2d9b-41f9-9c62-3c1762e9c760.jpg)

Limitations arise when using CT scanners for these medical procedures since these devices require extensive care, such as regular maintenance (calibration) for effective performance. Plus, transporting these to remote locations is not an easy task. Point-of-care imaging addresses these challenges by allowing radiologists to add portable CT scanners to their departments to increase patient satisfaction and improve medical outcomes. 
Two parameters that relate to the geometry of portable CT scanning devices are: 1)R - distance between source and detector and 2) θ - orientation of source to detector. 

![Source Rotation](https://user-images.githubusercontent.com/84742324/126884410-dacf0650-7696-42a7-b86c-af15fb269c05.png)

During the CT acquisition process, the x-ray source rotates around the patient. Each time the x-ray source moves to a new position, these parameters change. In point-of-care imaging, these parameters are essential during the data imaging process. Imprecise parameters yield to the reconstruction of poor quality images. 
Because these para The distance from the x-ray source to the center of the patient changes each time the x-ray source moves to a new position. The angles and the distance from  
How were these geometry parameters estimated to obtain better reconstructed images? 

![SheppLogan Reconstructed](https://user-images.githubusercontent.com/84742324/126884434-a47ee15e-2df5-45f1-8b5f-f1af63e894ad.png)

# Beer’s Law & Linear Algebra 
By the 1700s, scientists had discovered ways that could connect science to mathematics, to fields, such as tomographic imaging. Beer-Lambert Law or Beer’s Law was first developed in 1729 by Pierre Bouguer, and in 1852, Beer added to the law. Beer’s law states that as an x-ray source emits an x-ray beam and it passes through an object, then it loses energy exponentially.  To create a 2-D image, an imaginary grid of pixels is placed atop the object, and an x-ray beam is then shot through the object. Beer’s Law is used to create a system of linear equations. 

![Beer'sLaw](https://user-images.githubusercontent.com/84742324/126884449-423a5fc2-3aa9-4d37-84ca-a8d2c73e3f5a.png)

From Algebra, it is known that a system of equations has three types of solutions, infinitely many, exactly one, or no solution. When there is no solution, the system is called inconsistent, as opposed to consistent when there exists a solution. When there are more equations  than unknowns, then the system is overdetermined. In the case of computed tomography, there will be more x-rays than pixels. When there are more unknowns than equations, then the system is underdetermined, more pixels than x-ray beams. 
In each equation, every unknown represents a physical property, called attenuation, for each  pixel value. Pixels that have the same amount of material have the same attenuation; an image is then created. The images obtained based on these attenuation values allow doctors to make diagnoses. For example, bones have a different attenuation than lungs. 

![BonesLungsAttenuation](https://user-images.githubusercontent.com/84742324/126884468-eb8b75df-ba4d-4c33-89ca-77455e598e24.jpg)

A system of linear equations can be solved in Precalculus by the Gauss-Jordan elimination method. In linear algebra, a matrix equation of the form Ax=b is solved to find x. Ideally, this could easily be done. Unfortunately, for this project, this might not be possible for several reasons: 1) b has noise in it,  and 2) the exact matrix A may not be known because the parameters R and θ may be perturbed (CT machine is not calibrated correctly). Matrix A may also be a huge matrix containing millions of rows and columns. Typical approaches learned in Pre-Calculus or a linear algebra class cannot be used to solve this problem. The tomographic imaging research group uses other methods to solve these large problems, referred to as ill-posed. 
An ill-posed problem is often referred to as one that is not well-posed. In the 20th Century, French mathematician Jacques Hadamard defined well-posed by having three properties: 1) a solution exists, 2) the solution is unique, 3) the solution depends on initial values. An ill-posed problem needs to be approached differently, e.g. -regularization. Tikhonov regularization is a common form of regularization for ill-posed problems. 

# The Linear & NonLinear Least Squares Problem 
Throughout the 1800s, mathematicians such as Legendre, Gauss, and Laplace contributed ideas to the method of least squares. The method of least squares finds the line that minimizes the distance to the line and the data points. 

In computed tomography, a problem arises that involves the least squares, a regularized linear least squares problem. This regularized linear least squares problem is composed of x, the image, A(p), a matrix that is constructed by the geometry parameters, R and θ, b, the measured data, and a parameter α, called the regularization parameter. The nonlinear least squares problem does not include the regularization parameter.   


The solution to this problem is found by the block coordinate descent (BCD). The BCD is an optimization algorithm that solves this problem iteratively. The BCD algorithm works by minimizing the parameters R and θ and x one at a time, just like finding the distance from the line and data points.  The linear least squares problem is considered first. It takes the initial parameters R and θ, generate matrix A, to get x, the image. Here the parameters, R and θ are known and x is approximated. Then, the nonlinear least squares problem is considered next. Once x is known, then x is used to approximate the parameters, R and θ. Here x is known and the parameters R and θ are approximated. The pattern continues until a good image is produced.  

# Filter - Based Regularization 
Since it is impossible to get data exactly from the detector due to numerous reasons, regularization is needed to lower the noise levels. Tikhonov regularization is one of the most common ways to handle these noise levels. The method was named after mathematician Andrew Tikhonov. Tikhonov worked in numerous topics and different fields of mathematics. His best contributions are in topology. 

Singular value decomposition (SVD) plays an important role in understanding the basic idea behind Tikhonov Regularization. The singular values of the matrix A are significant. To achieve good reconstructed images with small noise large singular values need to be considered to minimize the error produced. 

# Acceleration Techniques & Tests

Estimating the geometry parameters in this project can be viewed as a fixed point iteration technique. Acceleration techniques speed up the convergence of these iterations, in this case, until a good quality image is produced. The research imaging group used three fixed point acceleration schemes in their numerical experiments: 1) Irons-Tuck method, 2) Crossed - second method, 3) Anderson Acceleration. Acceleration tests were performed and seemed to improve image resolution. MATLAB was used including the optimization, signal processing, and image processing toolboxes. IR Tools, AIR Tools II, and Imfil packages were also used. 










































































---
title: Point-of-Care Tomographic Imaging
date: 2021-05-01
featured: true
tags: ["Summer 2021"]
---

Portable Medical Machinery Powered by Mathematics

<!--more-->

Computed tomography (CT) is well known for its ability to produce high-quality images needed for medical diagnostic purposes. Unfortunately, standard CT machines are extremely large, heavy, require careful and regular calibration, and are expensive, limiting their availability in many parts of the world. An alternative approach is to use portable machines. Still, parameters related to the geometry of these devices (e.g., the distance between source and detector, the orientation of the source to the detector) cannot always be precisely calibrated in point-of-care situations. These parameters may change slightly when the machine is adjusted during the image acquisition process, which causes severe degradations in the resulting image. The team working on this project will develop a numerical method to jointly estimate the geometry parameters of the portable device and to reconstruct the image.

---
# Background

![mainImage](img/tomography1.png "Tomography")


# Point-of-Care Tomographic Imaging
