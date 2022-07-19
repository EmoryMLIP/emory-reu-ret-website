---
title: 'Model-based approaches to neuronal network firing and its subsequent validation with a previously recorded in-vivo dataset'
date: 2022-06-27T11:36:49-04:00
lastmod: 2022-06-27T11:36:49-04:00
featured: true
weight : 100
summary: 'The human brain sends signals using around 100 billion neurons connected in a complex and dynamic fashion. The sheer number of neurons makes the task of modeling, particularly at the network level, difficult. Instead of modeling each individual neuron, one can instead approximate the system using a series of coupled ordinary or delay differential equations. Using bifurcation theory, this approximate system can then be manipulated to mimic neuronal level changes that lead to neuronal dysfunction, disease states, and, ultimately, possible trajectories in parameter space that lead back to a healthy neuronal state. These types of models help add to the understanding of neuronal dysfunction but are pretty useless without data to validate the model. Fortunately, a rich dataset of in-vivo primate neuronal data recorded throughout various movement-related brain areas is available to help validate and corroborate findings for this project.'
tags: ["Summer 2022"]
---
# Mathematical Modeling of Healthy and Parkinsonian Firing Patterns in the Primate Thalamocortical Motor Circuit
Parkinson's disease (PD) is a slowly progressing neuro-degenerative disease featuring impaired motor symptoms such as bradykinesia, muscular rigidity, and resting tremors.<sup>1</sup> In industrialized countries, PD affects 0.3% of all people and 1% of people over age 60.<sup>18</sup> The basal ganglia, motor thalamus, and motor cortex are three main components of the brain's motor circuit and are responsible for movement planning and execution; movement disorders such as PD can develop when the typical activity of this circuit is disrupted.<sup>2</sup> Specifically, PD is associated with the loss of dopaminergic neurons and altered neuronal oscillations in the beta-band (13-30 Hz).<sup>6</sup> We employ a mathematical model to investigate network connection changes within the motor circuit in order to better understand the transition from healthy to parkinsonian states in the brain. 
# The Motor Circuit
The basal ganglia, thalamus, and cortex are members of numerous segregated circuits and subcircuits in the brain, including the motor circuuit; disruption in the flow of this circuit can lead to Parkinson's disease.<sup>3</sup> The main cause of PD is the loss of dopaminergic neurons, which results in significant changes in the basal ganglia's neuronal activity, hence disrupting the motor circuit's overall flow and inhibiting the brain's ability to regulate bodily movement.<sup>2,6</sup> Other projects, such as the <a href="https://www.worldscientific.com/doi/epdf/10.1142/S0129065718500211">2019 paper by M. Caiola and M. Holmes</a>, have investigated the changes in the basal ganglia neuronal activity from a mathematical modeling perspective, but little research has been done on the parkinsonism-associated changes in the areas of the thalamus and cortex which are involved in the motor circuit.<sup>7</sup> Given the practical limitations associated with directly recording data concerning parkinsonian changes in neuronal activity in the thalamus and cortex, fitting a mathematical model to previously recorded data helps us to further investigate the effects of dopamine loss on thalamocortical neurons specifically.
# Firing Rate Model
We choose to use a firing rate model to describe our system. This type of model outputs average firing rates for each of the unit's models rather than individual spikes, which is ideal for a network such as the motor circuit. We can allow each neuron population to be a unit of this firing rate model, examining the firing rate interactions between populations in the form of average firing rates.This also eliminates the need to rely on individual neurons for our model.<sup>7</sup> This approach to modeling can successfully represent networks, since each unit in the model can represent a population of neurons receiving input (average firing rates) from other neuron populations.

A simplified circuit diagram of the thalamocortical motor circuit network is shown below, and provides the neuroscience basis for our model. The rounded squares each represent a population of neurons, which are connected by either excitatory (arrow-tipped lines) or inhibitory (circle-tipped lines) synaptic weights. The green circle represents the interneuron population of the thalamus.

![Thalamocortical Loop Model](Thalamocortical.png)

Treating the interneuron population as a "relay," <em>&gamma;</em>, we can establish the following system of equations:

<em>&tau;<sub>1</sub>y'<sub>1</sub></em> = &minus;<em>y<sub>1</sub></em> &plus; <em>f<sub>1</sub></em>(<em>&beta;<sub>1</sub></em> &plus; <em>h</em>)

<em>&tau;<sub>2</sub>y'<sub>2</sub></em> = &minus;<em>y<sub>2</sub></em> &plus; <em>f<sub>2</sub></em>(<em>w<sub>12</sub>y<sub>1</sub></em> &plus; <em>w<sub>32</sub>y<sub>3</sub></em> &plus; <em>w<sub>42</sub>y<sub>4</sub></em> &minus; <em>w<sub>52</sub>y<sub>5</sub></em> &plus; <em>&gamma;</em> &plus; <em>b<sub>2</sub></em>)

<em>&tau;<sub>3</sub>y'<sub>3</sub></em> = &minus;<em>y<sub>3</sub></em> &plus; <em>f<sub>3</sub></em>(<em>w<sub>23</sub>y<sub>2</sub></em> &plus; <em>w<sub>43</sub>y<sub>4</sub></em> &plus; <em>b<sub>3</sub></em>)

<em>&tau;<sub>4</sub>y'<sub>4</sub></em> = &minus;<em>y<sub>4</sub></em> &plus; <em>f<sub>4</sub></em>(<em>w<sub>34</sub>y<sub>3</sub></em> &plus; <em>b<sub>4</sub></em>)

<em>&tau;<sub>5</sub>y'<sub>5</sub></em> = &minus;<em>y<sub>5</sub></em> &plus; <em>f<sub>5</sub></em>(<em>w<sub>45</sub>y<sub>4</sub></em> &plus; <em>b<sub>5</sub></em>)
  
&gamma; = &minus;<em>w<sub>62</sub></em>(&minus;<em>w<sub>16</sub>y<sub>1</sub></em> &minus; <em>w<sub>56</sub>y<sub>5</sub></em> &plus; <em>w<sub>46</sub>y<sub>4</sub></em> &plus; <em>b<sub>6</sub></em>)

where <em>y<sub>1</sub></em>, <em>y<sub>2</sub></em>, <em>y<sub>3</sub></em>, <em>y<sub>4</sub></em>, <em>y<sub>5</sub></em> are the firing rates for the GPi, thalamocortical loop (TC), corticothalamic layer 5 (CT5), corticothalamic layer 6 (CT6), and reticular nucleus (RTN), respectively. Each <em>w<sub>jk</sub></em> represents the weight of the firing rate flow from population <em>j</em> to population <em>k</em>. Note that <em>w<sub>23</sub></em> represents the difference between the excitatory and inhibitory inputs from TC to CT5. Note also that <em>w<sub>jk</sub></em> > 0, &tau;<sub><em>i</em></sub> > 0, and <em>F<sub>i</sub></em> represents the activation function for the <em>i</em>-th population.

This can be represented with vectors and matrices as:

<em>T<strong>y'</strong></em> = &minus;<em><strong>y</strong></em> &plus; <em><strong>F</strong></em>(<em><strong>x</strong></em>) &xrArr; <em>T<strong>y'</strong></em> = <em>A<strong>y</strong></em> &plus; <em><strong>B</strong></em>
# Activation Function Selection
The choice of activation function for this model is significant, since it informs the behavior of the model. Although many different approaches to developing activation functions for neuronal mathematical modeling exist, previous studies have shown that a sigmoidal function is able to closely approximate the neuron discharge behavior recorded in experiments.<sup>19-21</sup> However, this model creates a nonlinear system of equations for which it is impossible to find steady states. In order to attain eigenvalues and be able to comment on the behavior of the model as a whole, we must establish a simpler activation function that still manages to approximate experimental neuron discharge behavior.<sup>7</sup> Thus, we choose a piecewise linear (PWL) function as our activation function:

![Piecewise Linear Activation Function](pwl_act_func.png)

We can break down this system into 3<sup>5</sup> = 243 distinct linear regions in space, each with its own steady state (fixed point in space which the solution tends to as time increases). This allows us to solve for eigenvalues analytically, permitting us to investigate the system further and find a continuous solution. A piecewise linear activation function is ideal in our case, as it allows us to break down a complex system into linear pieces which can be solved and manipulated. 

Below the approximation of the piecewise linear activation function to the sigmoidal approximation is shown, with the middle region outlined in green.

![Accuracy of Piecewise Linear Activation Function to the Sigmoidal Activation Function](color_pws.jpg)

# Data Fitting and Error Functions
This semi-linear firing rate model has a number of constant values that we must locate in experimental data and incorporate, namely the baseline firing rates, maximum firing rates, and membrane time constants for each neuron population involved in our simplified motor circuit model. We were able to find values for these parameters through literature review, although some required that we make estimates informed by information from areas of the brain that behave similarly or data on these parameters from mice, rats, or cats. However, there does not seem to be data that documents the baseline firing rate for the thalamic interneuron population in the primate brain. Given our uncertainty about the true baseline firing rate value for the primate thalamic interneuron population, we decided to create two models, one with the low and one with the high baseline. The parameter values are shown in the table below:

<table>
  <tr>
    <td>Neuron Population</td>
    <td><em>b<sub>i</sub></em></td>
    <td><em>M<sub>i</sub></em></td>
    <td><em>&tau;<sub>i</sub></em></td>
  </tr>
  <tr>
    <td>GPi (<em>y</em><sub>1</sub>)</td>
    <td>55 Hz<sup>7,27,28,29,30</sup></td>
    <td>200 Hz<sup>31</sup></td>
    <td>8 ms<sup>28,32,33</sup></td>
  </tr>
  <tr>
    <td>TC (<em>y</em><sub>2</sub>)</td>
    <td>18.5 Hz<sup>34</sup></td>
    <td>300 Hz</td>
    <td>25 ms</td>
  </tr>
  <tr>
    <td>CT5 (<em>y</em><sub>3</sub>)</td>
    <td>7.25 Hz<sup>35</sup></td>
    <td>200 Hz</td>
    <td>20 ms</td>
  </tr>
  <tr>
    <td>CT6 (<em>y</em><sub>4</sub>)</td>
    <td>7.25 Hz<sup>35</sup></td>
    <td>200 Hz</td>
    <td>15 ms</td>
  </tr>
  <tr>
    <td>RTN (<em>y</em><sub>5</sub>)</td>
    <td>25 Hz<sup>34</sup></td>
    <td>500 Hz<sup>34</sup></td>
    <td>16.51 ms</td>
  </tr>
  <tr>
    <td>IN (<em>&gamma;</em>)</td>
    <td>Low: 6 Hz<sup>36</sup> <br> High: 22.7 Hz<sup>37</sup></td>
    <td>N/A</td>
    <td>N/A</td>
  </tr>
</table>

# Stability and Steady State Conditions
No matter the disease state of our model, the neurons should not be at a state of maximal firing or absent firing for an extended period of time. Additionally, in Parkinsonian solutions, we should expect oscillations of firing rates. Thus the following must hold:
1. Middle region contains its own steady state, and trajectories must not stabilize in another region.
2. <strong>Healthy:</strong> Middle region is stable &xrarr; trajectories are thus forced to stabilize in the middle region, making the system globally asymptotically stable. <br> <strong>Parkinsonian:</strong> Middle region is unstable &xrarr; trajectories are thus forced to oscillate around the middle region, forming a globally stable limit cycle.

To determine stability, the PWL activation function allows us to solve for the eigenvalues of each of the 243 regions explicitly. We found 3 possible cases: 
1. The region is stable regardless of weights.
2. The region's stability is conditional on weight values.
3. The region (including the middle region) has eigenvalues that cannot be solved for analytically. Therefore, we used the <strong>Routh-Hurwitz Stability Criterion</strong> (RH) to derive 3 stability conditions.
# Weight Search
The current literature does not specify the baseline firing rate for the interneuron population, <em>b<sub>6</sub></em>, so we tooka high estimate and a low estimate: <em>b<sub>6</sub></em> = 6 for the low estimate, and <em>b<sub>6</sub></em> = 22.7 for the high estimate. 

Comparing our data to the predicted values our model outputted, we were able to minimize the sum of squared error between the two and find a healthy solution for both the low and the high estimates of <em>b<sub>6</sub></em>, and they are shown below:

Healthy Solution with Low <em>b<sub>6</sub></em>: 

<table>
  <tr>
    <td><em>w<sub>12</sub></em> = 1.520384442</td>
    <td><em>w<sub>16</sub></em> = 1.621278311</td>
    <td><em>w<sub>23</sub></em> = 0.4962387866</td>
    <td><em>w<sub>32</sub></em> = 1.117631687</td>
  </tr>
  <tr>
    <td><em>w<sub>34</sub></em> = 0.1540248925</td>
    <td><em>w<sub>42</sub></em> = 1.217895798</td>
    <td><em>w<sub>43</sub></em> = 0.0672671083</td>
    <td><em>w<sub>45</sub></em> = 1.542582263</td>
  </tr>
  <tr>
    <td><em>w<sub>46</sub></em> = 9.049109867</td>
    <td><em>w<sub>52</sub></em> = 4.5350845</td>
    <td><em>w<sub>56</sub></em> = 0.3330689302</td>
    <td><em>w<sub>62</sub></em> = 7.127373038</td>
  </tr>
</table>

Parkinsonian Solution with Low <em>b<sub>6</sub></em>: 

<table>
  <tr>
    <td><em>w<sub>12</sub></em> = 1.520384442</td>
    <td><em>w<sub>16</sub></em> = 1.621278311</td>
    <td><em>w<sub>23</sub></em> = 0.8691494663</td>
    <td><em>w<sub>32</sub></em> = 0.5043792396</td>
  </tr>
  <tr>
    <td><em>w<sub>34</sub></em> = 0.1540248925</td>
    <td><em>w<sub>42</sub></em> = 1.217895798</td>
    <td><em>w<sub>43</sub></em> = 0.0672671083</td>
    <td><em>w<sub>45</sub></em> = 1.542582263</td>
  </tr>
  <tr>
    <td><em>w<sub>46</sub></em> = 9.049109867</td>
    <td><em>w<sub>52</sub></em> = 4.5350845</td>
    <td><em>w<sub>56</sub></em> = 0.3330689302</td>
    <td><em>w<sub>62</sub></em> = 7.127373038</td>
  </tr>
</table>

insert pics

Each of the solutions tends toward a specific firing rate, showing that the solution is stable.

Although it is impossible to graph a 5-D system, we can choose three dimensions out of the five and graph this in 3-D:

insert pics

It is clear that the line spirals inward to a point, showing that it is stable.

Comparing our data to the predicted values our model outputted, we were able to minimize the sum of squared error between the two and find a parkinsonian solution for both the low and the high estimates of <em>b<sub>6</sub></em>, and they are shown below:

Healthy Solution with High <em>b<sub>6</sub></em>: 

<table>
  <tr>
    <td><em>w<sub>12</sub></em> = 1.369676658</td>
    <td><em>w<sub>16</sub></em> = 1.858041961</td>
    <td><em>w<sub>23</sub></em> = 0.5298526616</td>
    <td><em>w<sub>32</sub></em> = 1.028216437</td>
  </tr>
  <tr>
    <td><em>w<sub>34</sub></em> = 0.1939248305</td>
    <td><em>w<sub>42</sub></em> = 1.246656565</td>
    <td><em>w<sub>43</sub></em> = 0.02150352807</td>
    <td><em>w<sub>45</sub></em> = 1.431595807</td>
  </tr>
  <tr>
    <td><em>w<sub>46</sub></em> = 8.456749369</td>
    <td><em>w<sub>52</sub></em> = 4.381617591</td>
    <td><em>w<sub>56</sub></em> = 0.4765754294</td>
    <td><em>w<sub>62</sub></em> = 5.843896231</td>
  </tr>
</table>

Parkinsonian Solution with High <em>b<sub>6</sub></em>: 

<table>
  <tr>
    <td><em>w<sub>12</sub></em> = 1.369676658</td>
    <td><em>w<sub>16</sub></em> = 1.858041961</td>
    <td><em>w<sub>23</sub></em> = 0.9914473113</td>
    <td><em>w<sub>32</sub></em> = 0.5548923727</td>
  </tr>
  <tr>
    <td><em>w<sub>34</sub></em> = 0.1939248305</td>
    <td><em>w<sub>42</sub></em> = 1.246656565</td>
    <td><em>w<sub>43</sub></em> = 0.02150352807</td>
    <td><em>w<sub>45</sub></em> = 1.431595807</td>
  </tr>
  <tr>
    <td><em>w<sub>46</sub></em> = 8.456749369</td>
    <td><em>w<sub>52</sub></em> = 4.381617591</td>
    <td><em>w<sub>56</sub></em> = 0.4765754294</td>
    <td><em>w<sub>62</sub></em> = 5.843896231</td>
  </tr>
</table>

The solution for the high <em>b<sub>6</sub></em> is plotted below:

![Rates of PD w/ High B](Rates_PD_high.jpg)

The TC solution oscillates around a firing rate, showing that it will produce a limit cycle solution.

Although it is impossible to graph a 5-D system, we can choose three dimensions out of the five and graph this in 3-D:

![3-D of PD w/ High B](3D_PD_high.jpg)

Here, it is clear that the solution produces a limit cycle.
# More About the Team
1. <strong>Carly Ferrell</strong> is a rising senior at Mississippi State University majoring in mathematics and minoring in statistics and music with a concentration in voice. She is interested in utilizing her skills in applied mathematics and statistcs to research music, specifically music theory and sight singing. Outside class, she enjoys reading, dancing, singing, and composing music. 

![Carly Picture](carly_pic.JPG)

 
 
2. <strong> Qile Jiang</strong> is a rising junior at Brown University majoring in Applied Mathematics. His primary research area is in applied dynamical systems, but he also has a keen interest in pure math topics such as algebra. Outside of school, he spends his time training boxing, painting, and going to operas and classical concerts.

![Qile Picture](qile_pic.jpg)

 
 
3. <strong>Margaret Olivia Leu</strong> is a junior at Pomona College double majoring in mathematics and politics. She is interested in working on ways to use mathematics as a tool in the fields of politics and social justice work, and hopes to pursue a career that combines these two interests. Outside academics, she enjoys crocheting, cooking, and listening to music.

![Olivia Picture](olivia_pic.jpg)

 
 
# References
1. Sveinbjornsdottir, S. (2016).The clinical symptoms of Parkinson's disease. <em>Journal of Neurochemistry, 139</em>(1), 318-324. https://doi.org/10.1111/jnc.13691.
2. DeLong, M. R., & Wichmann, T. (2007). Circuits and circuit disorders of the basal ganglia. <em>Archives of Neurology, 64</em>(1), 20–24. https://doi.org/10.1001/archneur.64.1.20.
3. Alexander, G. E., DeLong, M.R., & Strick, P.L. (1986). Parallel Organization of functionally segregated circuits linking basal ganglia and cortex. <em>Annual Review of Neuroscience, 9</em>(1), 357-381. https://doi.org/10.1146/annurev.ne.09.030186.002041
4. DeLong, M. R. (1990). Primate models of movement disorders of basal ganglia origin. <em>Trends in Neurosciences, 13</em>(7), 281–85. https://doi.org/10.1016/0166-2236(90)90110-v.
5. Wichmann, T., & Delong, M.R. (2003). Functional neuroanatomy of the basal ganglia in Parkinson’s disease. <em>Advances in Neurology, 91</em>, 9–18.
6. Galvan, A., Devergnas, A., & Wichmann, T. (2015). Alterations in neuronal activity in basal ganglia-thalamocortical circuits in the parkinsonian state. <em>Frontiers in Neuroanatomy, 9</em>, 5. https://doi.org/10.3389/fnana.2015.00005.
7. Caiola, M., & Holmes, M. H. (2019). Model and analysis for the onset of parkinsonian firing patterns in a simplified basal ganglia. <em>International Journal of Neural Systems, 29</em>(1). https://doi.org/10.1142/S0129065718500211.
8. Rubin, J. E., & Terman, D. (2004). High frequency stimulation of the subthalamic nucleus eliminates pathological thalamic rhythmicity in a computational model. <em>Journal of Computational Neuroscience, 16</em>(3), 211–235. https://doi.org/10.1023/B:JCNS.0000025686.47117.67.
9. Hodgkin, A. L., & Huxley, A. F. (1952). A quantitative description of membrane current and its application to conduction and excitation in nerve. <em>The Journal of Physiology, 117</em>(4), 500–544.
10. Schwiening, C. J. (2012). A brief historical perspective: Hodgkin and Huxley. <em>The Journal of Physiology, 590</em>(Pt 11), 2571–2575. https://doi.org/10.1113/jphysiol.2012.230458
11. Fang, X., Duan, S., & Wang, L. (2021). Memristive Hodgkin-Huxley Spiking Neuron Model for Reproducing Neuron Behaviors. <em>Frontiers in Neuroscience, 15</em>. \\https://www.frontiersin.org/article/10.3389/fnins.2021.730566.
12. Rodríguez-Collado, A., & Rueda, C. (2021). A simple parametric representation of the Hodgkin-Huxley model. <em>PLoS ONE, 16</em>(7), e0254152. https://doi.org/10.1371/journal.pone.0254152
13. Sherwood, W. E. (2014). FitzHugh-Nagumo model. <em>Encyclopedia of Computational Neuroscience</em>. https://link.springer.com/content/pdf/10.1007\%2F978-1-4614-7320-6\_147-1.pdf.
14. Collins, C. E., Airey, D. C., Young, N. A., Leitch, D. B., & Kaas, J. H. (2010). Neuron densities vary across and within cortical areas in primates. <em>Proceedings of the National Academy of Sciences, 107</em>(36), 15927–15932. https://doi.org/10.1073
15. McIntyre, C. C., & Hahn, P. J. (2010). Network Perspectives on the Mechanisms of Deep Brain Stimulation. <em>Neurobiology of Disease, 38</em>(3), 329–337. https://doi.org/10.1016/j.nbd.2009.09.022
16. Wilson, H. R., & Cowan, J. D. (1972). Excitatory and Inhibitory Interactions in Localized Populations of Model Neurons. <em>Biophysical Journal, 12</em>(1), 1–24.
17. Dayan, P., & Abbott, L. F. (2001). Theoretical neuroscience: Computational and mathematical modeling of neural systems. <em>Massachusetts Institute of Technology Press</em>.
18. de Lau, L. M. L., & Breteler, M. M. B. (2006). Epidemiology of Parkinson's disease. <em>The Lancet Neurology, 5</em>(6), 525-535. https://doi.org/10.1016/S1474-4422(06)70471-9.
19. Rall, W. (1955). Experimental monosynaptic input-output relations in the mammalian spinal cord. <em>Journal of Cellular and Comparative Physiology, 46</em>(3), 413–437. https://doi.org/10.1002/jcp.1030460303
20. Wilson, C. J., & Bevan, M. D. (2011). Intrinsic dynamics and synaptic inputs control the activity patterns of subthalamic nucleus neurons in health and in Parkinson’s disease. <em>Neuroscience, 198</em>, 54–68. https://doi.org/10.1016/j.neuroscience.2011.06.049
21. Nambu, A., & Llinaś, R. (1994). Electrophysiology of globus pallidus neurons in vitro. <em>Journal of Neurophysiology, 72</em>(3), 1127–1139. https://doi.org/10.1152/jn.1994.72.3.1127
22. Holgado, A. J. N., Terry, J. R., & Bogacz, R. (2010). Conditions for the Generation of Beta Oscillations in the Subthalamic Nucleus–Globus Pallidus Network. <em>The Journal of Neuroscience, 30</em>(37), 12340–12352. https://doi.org/10.1523/JNEUROSCI.0817-10.2010
23. Ermentrout, G.B., & Terman, D.H. (2010). <em>Mathematical Foundations of Neuroscience</em>. Springer New York. https://doi.org/10.1007/978-0-387-87708-2
24. Isokawa, M. (1997). Membrane time constant as a tool to assess cell degeneration. <em>Brain Research Protocols, 1</em>(2), 114–116. https://doi.org/10.1016/S1385-299X(96)00016-5
25. Pavlides, A., John Hogan, S., & Bogacz, R. (2012). Improved conditions for the generation of beta oscillations in the subthalamic nucleus–globus pallidus network. <em>European Journal of Neuroscience, 36</em>(2), 2229–2239. https://doi.org/10.1111/j.1460-9568.2012.08105.x
26. Pavlides, A., Hogan, S. J., & Bogacz, R. (2015). Computational Models Describing Possible Mechanisms for Generation of Excessive Beta Oscillations in Parkinson’s Disease. <em>PLOS Computational Biology, 11</em>(12), e1004609. https://doi.org/10.1371/journal.pcbi.1004609
