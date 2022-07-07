---
title: 'Data assimilation for Hurricane Storm Surge Modeling'
date: 2022-06-27T11:36:49-04:00
lastmod: 2022-06-27T11:36:49-04:00
featured: true
weight : 100
summary: 'Numerical models of coastal hydrodynamics play a vital role in understanding hurricane storm surges, particularly as the climate changes. However, uncertainties in model parameters and their representations, e.g., bottom stress and surface wind stress, limit the confidence of model results. Data is becoming increasingly available but also contains uncertainties. In this project we will explore methods of data assimilation, which utilize information about the uncertainties in both modeled and observed data to improve estimates of the coastal system state.'
tags: ["Summer 2022"]
---

 # Blog Post Outline
*Note, these sections are of varying length. Approximate length represented by number of stars.

## Intro: 
This post was written by Emily Corcoran, Hannah Park- Kaufmann, and Logan Knudsen. The project was advised by Dr. Talea Mayo.  <Links to our midterm presentation, blitz video, poster, code, and paper>

(What we've achieved> *

(What the importance of it is> *
## Glaciers
Research has shown that climate change will likely impact storm surge inundation and make modeling this process more difficult. Sea-level rise caused by climate change plays a part in this impact. To better model sea-level rise, glaciers can be modeled. Our group is collaborating with Dr. Robel from Georgia Tech and working with his glacier model. Marine-Terminating Glaciers have a natural flow towards the ocean, which contributes to sea level rise. By the year 2300, the Antarctic ice sheet is projected to cause up to [3 meters of sea level rise](https://go.gale.com/ps/i.do?id=GALE%7CA431965879&sid=googleScholar&v=2.1&it=r&linkaccess=abs&issn=00280836&p=HRCA&sw=w&userGroupName=anon%7Eed4bce0c) globally. Due to the severe impacts of glacial melting, modeling changes in ice sheets is an important task. There are challenges to modeling sea level rise, as ice sheet instability leads to significant sea-level rise uncertainty.


## Main:
(Broad background on Methods in modeling> **

(More detailed background on our ice sheet modeling Methods> *** <br>
[Ice sheet models](https://doi.org/10.1029/2018JF004709) aim to describe the changes in ice mass of marine-terminating glaciers, which may be impacted over time by climate change.
<p align="center"> <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/glacierdiagram%20(1).png">
</p>

(The problem> ***

(Data Assimilation> ** <br>
Data assimilation is a method to move models closer to reality using real world observations by readjusting the model state at specified times.

(How data assimilation applies to our problem> *****

(Tools and implementation> *****
<p align="center">
  <img width="500" height="300"src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/H(t)hndlndbx10.png">
</p>

(Results> ***

## Next Steps and Other Applications
Data assimilation can be used for many geophysical modeling tasks, such as weather forcasting and hurricane storm surge modeling. Going forward, some of our team's goals are to find the minimum frequency at which you can assimilate data, the essential time period of the data, and the smallest amount of data needed to recover the truth in the model. We also plan to determine an acceptable error bound for the parameters and a realistic range of values to use.

## About the Team

### Emily Corcoran
Emily Corcoran is a junior at New Jersey Institute of Technology, majoring in Mathematical Sciences with a concentration in Applied Statistics and Data Analysis. Before this REU, she has worked as a research assistant in her school's Visual Perception Lab. She is a student in the Albert Dorman Honors College and is an active member of NJIT's school yearbook and Knit 'n Crochet club. When she is not in class, she can be found reading, listening to music, or attending a local play.
 
### Logan Knudsen 
Logan Knudsen is a senior at Texas A &amp;  M University majoring in Mathematics with minors in Oceanography and Meteorology. Before the REU, he has worked doing research on Data Analysis using Benford's Law and as a Teaching Assistant. Logan is currently the President of Texas A &amp; M's Math Club and a member of student radio, KANM. When not in class, he can be found reading, playing the guitar or playing video games with his friends.
 
### Hannah Park-Kaufmann
Hannah Park-Kaufmann is a junior at Bard College and Conservatory, majoring in Mathematics and Piano Performance. Before this REU, she conducted research on Numerical Semigroups and Polyhedra, and on Identifying Universal Traits in Healthy Pianistic Posture using Depth Data. She tutors math in the Bard Prison Initiative (BPI). When not doing math, she can be found playing piano, reading scores, reading literature and/or eating.


//: ------Images: --------
<p align="center">
  <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/KiyaRivermanGlacier.png">
</p>
//: Above is the glacier image from the government website taken by Kiya Riverman

<p align="center">
  <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/glacier.jpeg">
</p>
//: Above is another glacier image

<p align="center">
  <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/boxmodel.png">
</p>
//: Above is the diagram of a box model

<p align="center">
  <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/glacierdiagram%20(1).png">
</p>
//: Above is Dr. Robel's glacier model schematic

<p align="center">
  <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/glacierdiagram.jpeg">
</p>
//: Above is again Dr. Robel's glacier model schematic, this time with figure description text

<p align="center">
  <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/groundingline2da.png">
</p>
//: Above is a simple schematic figure of a grounding line



<p align="center">
  <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/H(t)hndlndbx10.png">
</p>
//: Above is one big photo of a single sensitivity analysis diagram: "t vs. H(t) with the initial conditions varied"

<p align="center">
  <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/t_vs_H(t).png">
</p>
//: Above are 3 sensitivity analysis graphs side by side for t vs H(t)

<p align="center">
  <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/t_vs_L(t).png">
</p>
//: Above are 3 sensitivity analysis graphs side by side for t vs L(t)



<p align="center">
  <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/SEFig.pdf">
</p>
//: Above is the Data assimilation schematic from Dr. Mayo's slides

<p align="center">
  <img width="300" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/ensembleKalman_diagram.png">
</p>
//: Above is the Kalman Filter Diagram


