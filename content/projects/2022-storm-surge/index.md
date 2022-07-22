---
title: 'Data assimilation for Glacier Modeling'
date: 2022-06-27T11:36:49-04:00
lastmod: 2022-06-27T11:36:49-04:00
featured: true
weight : 100
summary: 'Numerical models of coastal hydrodynamics play a vital role in understanding hurricane storm surges, particularly as the climate changes. However, uncertainties in model parameters and their representations, e.g., bottom stress and surface wind stress, limit the confidence of model results. Data is becoming increasingly available but also contains uncertainties. In this project we will explore methods of data assimilation, which utilize information about the uncertainties in both modeled and observed data to improve estimates of the coastal system state.'
tags: ["Summer 2022"]
---

 # Data Assimilation for Glacier Modeling

This post was written by [Emily Corcoran](https://www.linkedin.com/in/emily-corcoran-816278186), Hannah Park-Kaufmann, and Logan Knudsen. The project was advised by Dr. Talea Mayo.  Our team has also created a [midterm presentation](https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/data_assimilation_for_glacier_modeling.pdf), [blitz video](https://www.youtube.com/watch?v=bGeOZ9G6IOc), [poster](https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/REU_Poster.pdf), paper, and has written code.

<!---What we've achieved -->

<!---What the importance of it is -->

## Glaciers
Research has shown that climate change will likely impact [storm surge inundation](https://doi.org/10.3389/fbuil.2020.588049) and make modeling this process more difficult. Sea-level rise caused by climate change plays a part in this impact. To better model sea-level rise, glaciers can be modeled. Marine-Terminating Glaciers have a natural flow towards the ocean, which contributes to sea level rise. By the year 2300, the Antarctic ice sheet is projected to cause up to [3 meters of sea level rise](https://go.gale.com/ps/i.do?id=GALE%7CA431965879&sid=googleScholar&v=2.1&it=r&linkaccess=abs&issn=00280836&p=HRCA&sw=w&userGroupName=anon%7Eed4bce0c) globally. Due to the severe impacts of glacial melting, modeling changes in ice sheets is an important task. There are challenges to modeling sea level rise, as ice sheet instability leads to significant [sea-level rise uncertainty](https://doi.org/10.1073/pnas.1904822116).
<!--- ------Images: -------- -->
<p align="center">
  <img width="500" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/icebergphoto.jpeg">
</p>
<!--- Above is the glacier image from the government website taken by Kiya Riverman -->
<!---<p align="center">
  <img width="500" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/groundingline2da.png"> -->
<p align="center">
Image by W. Bulach, used under <a href="https://creativecommons.org/licenses/by-sa/4.0/legalcode">Creative Commons Attribution-Share Alike 4.0 International License</a>
</p>
</p> <!--- Above is a simple schematic figure of a grounding line -->


## Modeling Glaciers
<!---Broad background on Methods in modeling--> 

<!---More detailed background on our ice sheet modeling Methods-->
Our group is collaborating with [Dr. Robel](https://iceclimate.eas.gatech.edu/group/), a glaciologist, climate scientist, and applied mathematician from Georgia Tech, and working with the glacier model described in his [2018 paper](https://doi.org/10.1029/2018JF004709). This ice sheet model aims to describe the changes in ice mass of marine-terminating glaciers, which may be impacted over time by climate change. 
<p align="center"> <img width="500" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/glacierdiagram%20(1).png"></p>
<p align="center">
Image used with permission from <a href="https://doi.org/10.1029/2018JF004709">Dr. Alexander Robel</a>
</p>
<!--- Above is Dr. Robel's glacier model schematic -->
A glacier can be represented with a simplified box model that has a length $L$, precipitation $P$, and height and flux at the grounding line $h_g$ and $Q_g$. This model is the best approximation for one variable and describes the dominant mode of the glacial system.
<p align="center"> <img width="500" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/boxmodel.png">
</p>
<!--- Above is the diagram of a box model -->
The two-stage model that our group is using incorporates a nested box into the system. This new box has a thickness, $H$, and an interior flux, $Q$. The change in length and height of the glacier can be described with these differential equations: $$\ \dfrac{dH}{dt}=P-\dfrac{Q_g}{L}-\dfrac{H}{h_gL}(Q-Q_g)$$ $$\ \dfrac{dL}{dt}=\dfrac{1}{h_g}(Q-Q_g)$$



## Sensitivity Analysis
Sensitivity analyses study how various sources of uncertainty in a mathematical model contribute to the model's overall uncertainty. This allows us to understand the model better. 

Why do we do this?  Why do we care about the uncertainty of a model? And where do the uncertainties even come from?
In this ice sheet model, just like in any model, there are always going to be simplifications, and these lead to uncertainties. We need to have a good idea of which uncertainties matter the most, so that we better know the limits of where our model does a good job of simulating the real world. <br>

The basic idea is this: We check sensitivity by using different distributions for the input parameters. If the outputs vary significantly, then the output is sensitive to the specification of the input distributions. Hence these should be defined with particular care. We can also look at the sensitivity of the model parameters to inform which parameter we're going to work with in the data assimilation. We want to be working with the most sensitive parameter, because it has the most promise for things we vary later on to matter, in questions like: "if your data is from billions of years ago does that matter? Is it important to have your data from the last 60 years?" or "how much will noise impact the predictions?" <br>

The uncertain model parameters we considered are: initial conditions, sill parameters, and SMB values. For consistency's sake, we vary each parameter by +-10 percent of the nominal values originally given in our model code. Below you can see three graphs, one for each group of parameters varied, for each "time vs H(t)" (Height of the glacier at time) and "time vs L(t)" (Length of the glacier at time).

<p align="center">
  <img width="500" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/t_vs_H(t).png">
</p>
<!--- Above are 3 sensitivity analysis graphs side by side for t vs H(t) -->

<p align="center">
  <img width="500" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/t_vs_L(t).png">
</p>
<!--- Above are 3 sensitivity analysis graphs side by side for t vs L(t) -->

Looking at the distributions, we see that varying initial conditions (Leftmost) seems to produce the greatest spread, but the slopes of the lines there are all very similar. Varying the sill parameters (Middle) produces a lesser spread than varying initial conditions, however there is a greater variation in the slope of the lines. Finally, when varying the smb data (Rightmost) the result actually doesn't change that much and is quite stable. Thus, according to our analysis, the model is the least sensitive to SMB parameters, and between initial and sill parameters judgement varies depending on what you care about more - spread or slope.




## Data Assimilation
<!---Data Assimilation-->
Data assimilation is a method to move models closer to reality using real world observations by readjusting the model state at specified times.
<p align="center">
  <img width="500" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/SEFig.png">
</p>
<p align="center">
Image used with permission from Dr. Talea Mayo.
</p>

In this example we have used the ensemble Kalman filter method (ENKF) in order to perform our data assimilation. In basic terms, we initialize an ensemble( or a series of model runs with perturbed initial conditions) and performed data assimilation on each of the ensemble members, then to get our final analysis we took the mean of the ensemble.
<p align="center">
  <img width="500" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/kalmanExample.png">
</p>
<!--- Above is the Kalman Filter Example -->

The program used to model the glacier behavior and assimilate the data begins with choosing a set of initial conditions. Once the initial conditions are input to the model, which after taking a step using a Runge-Kutta 4th Order Method, is plugged into a Data Assimilation Method. Our main method is ENKF as previously mdentioned. Finally, the analyzed data from the assimilation is output and plugged back into the model. It should be noted that at sometimes the forecast output for the model is the same as the analyzed data.
<p align="center">
  <img width="650" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/ScreenShot2022-07-07at17.21.17.png">
</p>
<!--- Above is the Kalman Filter Diagram -->


<!---Results-->

### Square Difference
The error measure we use in the best ensemble size and observation scheme is the square difference, $d^2$, which we define $$\ d_t^2 = \left(x_t - x^a_t\right)^2 $$
where $x_t$ is the true state from the truth simulation at time $t$ and $x^a_t$ is the analysis state at time $t$.

### Ensemble Size
In the interest of lowering computational costs, we use the square difference in order to minimize ensemble size while also minimizing error. To do this, we choose an ensemble size, calculate the square difference at each $t$, and then calculated the mean of all these square differences. We ran this calculation for ensembles sizes from 2 up to 75, and found that ensembles of size 7-10 were ideal as they were at the point where the average square difference hovers around the same value. 

<p align="center">
  <img width="500" height="400" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/Mean_Square_Difference_of_H.png">
</p>

<p align="center">
  <img width="500" height="400" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/Mean_Square_Difference_of_L.png">
</p>

### Observation Scheme
We ran the model for various observation schemes to find the best observation scheme, i.e. the times frames and frequencies which can produce a sufficiently small average square difference over the course of the model run. We applied this process to our model and found that for before 1900 the best observation frequency, while still using small number of observations, would be every 19 years for a total of 100 observations. Similarly, for the time frame of 1950-2300 we found that yearly observations for a total of 350 observations is the best frequency. 
<p align="center">
  <img width="700" height="400" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/oldDates.png">
</p>
<p align="center">
  <img width="700" height="400" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/newDates.png">
</p>

<!---
#### Mean Square Difference 0-1900
|\# Observations | H | L |
|---|---|---|
| 200 | 0.0044054 | 0.0125222 |
| 100 | 0.0087286 | 0.0212535 |
| 50 | 0.0563252 | 0.0613737 |
| 25 | 0.0834296 | 0.0759587 |
| 10 | 0.0952199 | 0.1685447 |

#### Mean Square Difference 1950-2300
|\# Observations | H | L |
|---|---|---|
| 1400 | 0.0025464 | 0.0015147 |
| 700 | 0.0041299 | 0.0019446 |
| 350 | 0.0115712 | 0.0032547 |
| 175 | 0.0175867 | 0.0067435 |
| 88 | 0.0314155 | 0.0172441 |
| 44 | 0.0787454 | 0.0236401 |
| 22 | 0.2535894 | 0.0575641 |
-->

### Model Runs 
Using the facts we established in the previous two sections, we ran the model using EnKF for the time frame of 0-2022 in order to project $H$ and $L$ into the future up to the year 2300. The following plots show the results of this experiment, which we will use to help calculate $Q$ and $Q_g$ over time, and in turn use it to calculate sea level rise.

<p align="center">
  <img width="500" height="400" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/H(t)projections.png">
</p>

<p align="center">
  <img width="500" height="400" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/L(t)projections.png">
</p>

### Sea Level Rise
Using the formulas for $Q$ and $Q_g$ we can calculate the volume lost across the grounding line
$$\ V_{gz} = W(Q-Q_g)t $$
We then used the to calculate the volume out at all times and add it up to get accumulated volume loss. We then assume that the width of the glacier is 50 km(at least in the case we show here). To convert this to sea level rise, note that 394.67 km$^3$ of ice is equivalent $1$ mm of sea level and get the following projection of sea level rise. 

<p align="center">
  <img width="500" height="400" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/w50.0km_sea_level_projection.png">
</p>

## Next Steps
Using data assimilation can help to inform the glacier modelers and glaciologists who collect data about how to collect data in an efficient way. This can help researchers to more efficiently utilize funding and avoid unnecessarily expensive data collection that does not significantly improve glacier models. Data assimilation should be explored within more complicated glacier models, as the model used here is quite simplified. If more research is performed on this technique, it could greatly improve the practice of glacier modeling. Data assimilation can also be used for many geophysical modeling tasks, such as weather forcasting and hurricane storm surge modeling. Going forward, we plan to integrate the output of the glacier model into the ADCIRC hurricane storm surge model to predict the impact of glacier model on storm surge inundation.

## References
[The long future of Antarctic melting](https://go.gale.com/ps/i.do?id=GALE%7CA431965879&sid=googleScholar&v=2.1&it=r&linkaccess=abs&issn=00280836&p=HRCA&sw=w&userGroupName=anon%7Eed4bce0c) <br>
[Marine ice sheet instability amplifies and skews uncertainty in projections of future sea-level rise](https://doi.org/10.1073/pnas.1904822116) <br>
[Projected climate change impacts on hurricane storm surge inundation in the coastal United States](https://doi.org/10.3389/fbuil.2020.588049) <br>
[Response of marine-terminating glaciers to forcing: time scales, sensitivities, instabilities, and stochastic dynamics](https://doi.org/10.1029/2018JF004709)

## About the Team

### Emily Corcoran
[Emily Corcoran](https://www.linkedin.com/in/emily-corcoran-816278186) is a junior at New Jersey Institute of Technology, majoring in Mathematical Sciences with a concentration in Applied Statistics and Data Analysis. Before this REU, she has worked as a research assistant in her school's Visual Perception Lab. She is a student in the Albert Dorman Honors College and is an active member of NJIT's school yearbook and Knit 'n Crochet club. When she is not in class, she can be found reading, listening to music, or attending a local play.
 
### Logan Knudsen 
[Logan Knudsen](https://www.loganknudsen.com/) is a senior at Texas A&amp;M University majoring in Mathematics with minors in Oceanography and Meteorology. Before this REU, he has worked doing research on Data Analysis using Benford's Law and as a Teaching Assistant. Logan is currently the President of Texas A&amp;M's Math Club and a member of student radio, KANM. When not in class, he can be found reading, playing the guitar or playing video games with his friends.
 
### Hannah Park-Kaufmann
Hannah Park-Kaufmann is a junior at Bard College and Conservatory, majoring in Mathematics and Piano Performance. Before this REU, she conducted research on Numerical Semigroups and Polyhedra, and on Identifying Universal Traits in Healthy Pianistic Posture using Depth Data. She tutors math in the Bard Prison Initiative (BPI). When not doing math, she can be found playing piano, reading scores, reading literature and/or eating.


<!--- <p align="center">
  <img width="500" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/glacier.jpeg">
</p> -->
<!--- Above is another glacier image -->


<!--- <p align="center">
  <img width="500" height="300" src="https://github.com/hakuupi/emory-reu-ret-website/blob/main/content/projects/2022-storm-surge/img/H(t)hndlndbx10.png">
</p> -->
<!--- Above is one big photo of a single sensitivity analysis diagram: "t vs. H(t) with the initial conditions varied" -->



