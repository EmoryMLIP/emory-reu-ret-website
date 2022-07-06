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
Parkinson's disease (PD) is a slowly progressing neuro-degenerative disease characterized by impaired motor symptoms such as bradykinesia, muscular rigidity, and resting tremors.<sup>1</sup> In industrialized countries, PD affects 0.3% of all people and 1% of people over age 60.<sup>18</sup> The basal ganglia, motor thalamus, and motor cortex are three main components of the brain's motor circuit and are responsible for movement planning and execution; movement disorders such as PD can develop when the typical activity of this circuit is disrupted.<sup>2</sup> We employ a mathematical model to investigate the interactions between motor circuit components in normal and parkinsonian states, ultimately developing a deeper understanding of how PD presents itself in the brain. 

![Parkinson's disease symptoms](symptoms.jpg)
# The Motor Circuit
The basal ganglia, thalmus, and cortex are members of numerous segregated circuits and subcircuits in the brain, including the motor circuit; disruption in the flow of this circuit can lead to Parkinson's disease.<sup>3</sup> The striatum and subthalamic nucleus (STN) function as input receptors in the motor circuit, receiving signals from the supplementary motor area (SMA) and the primary motor cortex (M1). This input passes through the direct and indirect pathways in the motor circuit.<sup>2</sup> The direct pathway is composed of the connection from the striatum to the GPi to the thalamus; the indirect pathway flows from the striatum to the globus pallidus external (GPe), from the GPe to the STN, from the STN to the GPi, and from the GPi to the thalamus.<sup>4,5</sup> After the input has passed through one of these pathways, the internal segment of the globus pallidus (GPi) and the substantia nigra pars reticulata (SNr) subsequently release output signals to the thalamus and brainstem.<sup>2</sup> These relationships are demonstrated in the simplified model below.

![Motor Circuit Simplified Diagram](basal.ganglia.jpg)

The main cause of PD is the loss of dopaminergic neurons in the substantia nigra pars compacta (SNc), which in turn results in decreased levels of dopamine in the striatum.<sup>^6</sup> This dopamine loss results in significant changes in the basal ganglia's neuronal activity, hence disrupting the motor circuit's overall flow and inhibiting the brain's ability to regulate bodily movement.<sup>2</sup> Other projects, such as the 2019 paper by M. Caiola and M. Holmes, have investigated the changes in the basal ganglia neuronal activity from a mathematical modeling perspective, but little research has been done on the parkinsonism-associated changes in the areas of the thalamus and cortex which are involved in the motor circuit.<sup>7</sup> Given the practical limitations associated with directly recording data concerning parkinsonian changes in neuronal activity in the thalamus and cortex, fitting a mathematical model to previously recorded data helps us to further investigate the effects of dopamine loss on thalamocortical neurons specifically.
# Disadvantages of Individual Neuron Models
Many attempts to model the activity of neuron networks are reduced models, which seek to simulate the behavior of a large population of neurons using a much smaller group of individual neurons.<sup>8</sup> The most widely known of these individual neuron mathematical models is the Hodgkin-Huxley model,<sup>9</sup> which provides the following nonlinear system that simulates an individual neuron's action potential firing dynamics with high accuracy:<sup>10,11</sup>

![Hodgkin-Huxley Model](HH_model.png)

In this system, <em>I</em> is the current per unit area, <em>C<sub>m</sub></em> is the cell capacitance, <em>V<sub>i</sub></em> is the equilibrium potential of the <em>i</em>-th ionic current, <em>g<sub>i</sub></em> is the maximum conductance of the <em>i</em>-th ionic current, <em>&alpha;<sub>i</sub></em> and <em>&beta;<sub>i</sub></em> are rate constants for the <em>i</em>-th ionic current (which vary with voltage instead of time), and <em>n</em>, <em>m</em> and <em>h</em> are activation probabilities such that 0 < <em>n</em>, <em>m</em>, <em>h</em> < 1.<sup>12</sup> 

The FitzHugh-Nagumo model was derived from the Hodgkin-Huxley model and shares many of the same characteristics of its predecessor, such as all-or-nothing firing, as well as the lack of a saddle equilibrium and therefore the absence of a well-defined firing threshold.<sup>13</sup> However, the FitzHugh-Nagumo model is much less computationally complex than the Hodgkin-Huxley model since it can be reduced to the following two equations:

![FitzHugh-Nagumo Model](FH-N_model.png)

where <em>v</em> is the membrane potential, <em>w</em> is the recovery variable, <em>I</em> is the magnitude of the stimulus current, and <em>a</em>, <em>b</em>, and <em>&tau;</em> are positive constants, with the added condition that <em>&tau;</em> &Lt; 1.<sup>13</sup> 

Both of the above models, as well as other existing individual neuron firing models, boast the advantage of highly accurate simulation of the firing behavior of an individual neuron, and therefore have many useful applications. However, these models tend to fall short when it comes to understanding the firing rate behavior, interactions, and interconnectedness of a large network of neurons such as the motor circuit.<sup>7</sup> The primate cortex alone contains millions of neurons and is just one component of the motor circuit.<sup>14</sup> Given that our network is on such a large scale, solving and implementing millions of systems of equations for each individual neuron is simply infeasible. Alternatively, some have proposed simulating a large network of neurons using a greatly reduced number of neurons. This approach poses the likely dilemma of over-simplifying the dynamics of a neuron network and hence losing the ability to apply any findings in a clinical setting. There is no clear solution to this issue, as it is unclear how many neurons are necessary to accurately simulate various regions of the brain (it's likely that so many neurons are necessary that even a simplified network would be too computationally expensive to solve using the individual neuron modeling approach).<sup>7</sup> Thus, in order to both accurately and efficiently model the firing rate dynamics of the motor circuit, we must utilize an approach that is not based on the use of individual neuron data.
# Firing Rate Model
Rather than relying on individual neuron models, an alternative approach is to use a network perspective in our model.<sup>15</sup>

In our analysis, we will expand the model developed by Caiola and Holmes<sup>7</sup> from three dimensions (three nuclei model) to five dimensions. The Caiola and Holmes model builds on the findings of Wilson and Cowan,<sup>16</sup> which were further explored by Dayan and Abbot, who hoped to develop an alternative to the preexisting accurate yet computationally complex models.<sup>17</sup> These firing rate models output average firing rates for each of the unit's models rather than individual spikes, which is ideal for a network such as the motor circuit. We can allow each neuron population to be a unit of this firing rate model, examining the firing rate interactions between populations in the form of average firing rates.

In a firing rate model, each unit of the model will produce an average firing rate, thus eliminating the need to rely on individual neurons for our model.<sup>7</sup> This average firing rate <em>y</em> can be found by solving: 

<em>&tau;y'</em> = &minus;<em>y</em> &plus; <em>F</em>(<em>Wy</em> &plus; <em>h</em>)

where <em>&tau;</em> is the vector of membrane time constants, <em>W</em> is the matrix of weights associated with the interactions between populations, <em>h</em> is the input coming from outside of the network, and <em>F</em> is the activation function.<sup>7</sup> This approach to modeling can successfully represent networks, since each unit in the model can represent a population of neurons receiving input (average firing rates) from other neuron populations.

A simplified circuit diagram of the thalamocortical motor circuit network is shown below, and provides the neuroscience basis for our model. The rounded squares each represent a population of neurons, which are connected by either excitatory (arrow-tipped lines) or inhibitory (circle-tipped lines) synaptic weights. The green circle represents the interneuron population of the thalamus and can be treated as a relay neuron or as a series of FitzHugh-Nagumo neurons.

![Thalamocortical Loop Model](Thalamocortical.png)

Treating the interneuron population as a "relay," <em>&gamma;</em>, we can establish the following system of equations:

<em>&tau;<sub>1</sub>y'<sub>1</sub></em> = &minus;<em>y<sub>1</sub></em> &plus; <em>F<sub>1</sub></em>(<em>&beta;<sub>1</sub></em> &plus; <em>h</em>)

<em>&tau;<sub>2</sub>y'<sub>2</sub></em> = &minus;<em>y<sub>2</sub></em> &plus; <em>F<sub>2</sub></em>(<em>w<sub>12</sub>y<sub>1</sub></em> &plus; <em>w<sub>32</sub>y<sub>3</sub></em> &plus; <em>w<sub>42</sub>y<sub>4</sub></em> &minus; <em>w<sub>52</sub>y<sub>5</sub></em> &plus; <em>&gamma;</em> &plus; <em>b<sub>2</sub></em>)

<em>&tau;<sub>3</sub>y'<sub>3</sub></em> = &minus;<em>y<sub>3</sub></em> &plus; <em>F<sub>3</sub></em>(<em>w<sub>23</sub>y<sub>2</sub></em> &plus; <em>w<sub>43</sub>y<sub>4</sub></em> &plus; <em>b<sub>3</sub></em>)

<em>&tau;<sub>4</sub>y'<sub>4</sub></em> = &minus;<em>y<sub>4</sub></em> &plus; <em>F<sub>4</sub></em>(<em>w<sub>34</sub>y<sub>3</sub></em> &plus; <em>b<sub>4</sub></em>)

<em>&tau;<sub>5</sub>y'<sub>5</sub></em> = &minus;<em>y<sub>5</sub></em> &plus; <em>F<sub>5</sub></em>(<em>w<sub>45</sub>y<sub>4</sub></em> &plus; <em>b<sub>5</sub></em>)
  
&gamma; = &minus;<em>w<sub>62</sub></em>(&minus;<em>w<sub>16</sub>y<sub>1</sub></em> &minus; <em>w<sub>56</sub>y<sub>5</sub></em> &plus; <em>w<sub>46</sub>y<sub>4</sub></em> &plus; <em>b<sub>6</sub></em>)

where <em>y<sub>1</sub></em>, <em>y<sub>2</sub></em>, <em>y<sub>3</sub></em>, <em>y<sub>4</sub></em>, <em>y<sub>5</sub></em> are the firing rates for the GPi, thalamocortical loop (TC), corticothalamic layer 5 (CT5), corticothalamic layer 6 (CT6), and reticular nucleus (RTN), respectively. <em>w<sub>jk</sub></em> represents the weight of the firing rate flow from population <em>j</em> to population <em>k</em>. Note that <em>w<sub>23</sub></em> represents the difference between the excitatory and inhibitory inputs from TC to CT5. Note also that <em>w<sub>jk</sub></em> > 0, &tau;<sub><em>i</em></sub> > 0, and <em>F<sub>i</sub></em> represents the activation function for the <em>i</em>-th population.
# Sigmoidal Activation Function and Its Approximations
The choice of activation function for this model is significant, since it informs the behavior of the model. Although many different approaches to developing activation functions for neuronal mathematical modeling exist, previous studies have shown that a sigmoidal function is able to closely approximate the neuron discharge behavior recorded in experiments.<sup>19-21</sup> We closely modeled our sigmoidal activation function off of the model developed by Holgado <em>et al.</em>:<sup>22</sup>

![Sigmoidal Activation Function](sig_act_func.png)

In this model, <em>M<sub>i</sub></em> is the maximum firing rate, and <em>S<sub>i</sub></em> is the maximum slope. Following the example of Holgado <em>et al.</em>, we will assume <em>S<sub>i</sub></em> = 1. The baseline firing rate is <em>b<sub>i</sub></em>, meaning:

<em>F<sub>i</sub></em>(0) = <em>b<sub>i</sub></em>

Although this sigmoidal function closely approximates typical neuron discharge behavior, it creates a nonlinear system of equations for which we are unable to find steady states. In order to attain eigenvalues and be able to comment on the behavior of the model as a whole, we must establish a simpler activation function that still manages to approximate experimental neuron discharge behavior.<sup>7</sup>

Caiola and Holmes established three alternative activation functions to the sigmoidal:
1. a linear function<sup>22</sup>
2. a rectification function<sup>22,23</sup>
3. a semi-linear piecewise function
Caiola and Holmes identify problems with the first two proposed alternative activation functions. In an experimental setting, a population of neurons will never fire at a rate below zero or above its maximum firing rate. The linear function allows the neuron population to fire at negative rates and surpass its maximum rate; the rectification function prevents the neuron population from firing at negative rates, but it still permits the neuron to fire at rates that increase to infinity. Therefore, the choice of either of these activation functions would prevent us from drawing any meaningful conclusions from our study that could be applied to the field of neuroscience, as they both allow the modeled neuron population to fire at rates that are biologically impossible. We instead consider a semi-linear piecewise activation function.
# Piecewise Linear Activation Function
In order to approximate the sigmoidal function and satisfy the realistic constraints on the firing rate ranges of each neuron population, we can use a semi-linear piecewise function as our activation function:

