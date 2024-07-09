---
title: 'Low-Level Ozone Prediction'
date: 2023-12-01
featured: true
weight : 20
summary: 'Low-level ozone is a harmful air pollutant that can cause adverse health effects like coughing and chest pain and can worsen preexisting conditions like asthma. Many low-income communities are near sources of air pollution, causing these communities to be disproportionately impacted.  Low-level ozone is difficult to model since it is not emitted directly into the air but is created by chemical reactions between oxides of nitrogen (NOx) and volatile organic compounds (VOC) in the presence of sunlight. Rising temperatures due to climate change are also increasing low-level ozone levels. Predicting low-level ozone can inform air quality forecasts and help determine which communities are most at risk. Functional linear regression models can be used to predict low levels of ozone. In this project, we will study functional models based on bivariate splines over triangulation to approximate the spatially distributed ozone measurements on a surface. We will explore methods to compute forecasts, quantify the uncertainty associated with our predictions, and identify the spatial distribution of low-level ozone.'
tags: ["Summer 2023"]
authors: [bettinger]
---
<!-- https://docs.google.com/document/d/15wNWsSkCo8XK4YvwSOmb3OCASHk8JbV1BKHrsnoi93M/edit -->


This blog post was written by Antonio Gamboa, Lucretia Gant, Timothy Gant, Andrea Glover, and Julianna Long and published with minor edits. The team was advised by [Bree Ettinger](../author/bree-ettinger).In addition to this post, the team has also given a [midterm presentation](content/2023-Ozone-Slides), filmed a [poster blitz video](https://youtu.be/Cd_eRpne4Ns), created a [poster](content/2023_Ozone-Poster.pdf) and written a [manuscript](content/2023-Ozone-Manuscript.pdf). 

## Motivation

Our team is identifying potential correlations between ground-level ozone pollution and its social and economic disparities, reducing environmental justice. We aim to utilize the results from this investigation to advocate for equitable policies and regulations.

Bringing social justice to communities impacted by unidentified factors depends on the guidance from scientific research that exposes and discovers inequalities. Communities with lower socioeconomic status often experience a disproportionate burden of air pollution, including higher levels of ground-level ozone, due to factors like proximity to industrial areas, transportation hubs, and poorer air quality monitoring. However, it is unclear how ground-level ozone pollution becomes an issue of social justice and equitable protection of public health for all communities.


## What is Ozone, and how is it formed?   

Ozone is a molecule composed of three oxygen atoms; it is highly reactive and mostly found as a colorless and odorless gas. At high altitudes in the stratosphere, it protects us from the damaging UV sun rays> However, at the ground level, in the troposphere, ozone is a secondary pollutant. As a secondary pollutant, ozone, it is formed through complex chemical reactions of molecules in the air.

Ground-level Ozone (O3) is formed when nitrogen oxides (NOx) and volatile organic compounds (VOCs) react in the presence of sunlight. 
NOx is primarily emitted from vehicle exhaust, power plants, and industrial processes, while VOCs come from sources such as gasoline vapors, solvents, and certain industrial activities. These emissions are known as ozone precursors. 

When these precursors mix in the lower atmosphere and are exposed to sunlight, a series of chemical reactions occur, [leading to the formation of ground-level ozone ](https://doi.org/10.3389/fimmu.2019.02518).


## How Mathematics may be used to better monitor and deal with Ozone? 

Mathematics is currently used to study air pollution.  Mathematics provides us with equations and algorithms to solve a problem through computation. The mathematical algorithms act as an exact set of instructions to be followed by the hardware in the computer.  The result of such a combination of mathematics and computer science provides us with important functional models that simulate and predict ozone concentrations.

Mathematical modeling can be done by taking large data sets for ozone collected daily over the years and finding a function that fits the data well with a small percent error.  Furthermore, computation techniques such as machine learning can be applied to the data to predict future ozone levels.
The mathematical prediction of low-level ozone can inform air quality forecasts and help people determine which outside activities are safe.

## What type of Mathematical Applications may be used to better understand Ground Level Ozone?

Functional linear regression models have recently shown their ability to predict low ozone levels. Specifically, functional models based on [bivariate splines over triangulation](https://onlinelibrary.wiley.com/doi/10.1002/env.2147) approximate the spatially distributed ozone measurements on a surface. This powerful computation allows the forecast and the quantifying of the uncertainty associated with the predictions of ozone levels for a given day.
A mathematical functional regression model is a statistical technique combining functional data analysis and regression analysis principles. It is used to model the relationship between a dependent variable and one or more independent variables when both are functions or curves rather than simple numeric values. The data points are considered as functions or curves rather than individual observations. 
Functional principal component regression combines functional principal component analysis (PCA) and regression analysis. It uses the principal components of the functional independent variables to represent the variation in the data and estimates the coefficients for predicting the functional dependent variable.
In this project, we have used PCA as a powerful tool for analyzing and modeling relationships between ground-level ozone and the SVI index for communities near the Atlanta area. 


## How could this modeling be used to address Social Justice?

Our preliminary results suggest a potential correlation between ground-level ozone 
and socially vulnerable neighborhoods.  Social Vulnerability Indexes (SVI) identify communities predisposed to harm if exposed to a natural disaster or harmful conditions.  These communities are particularly at risk because of specific factors related to their socioeconomic status, household characteristics, racial and ethnic minority status, and housing type. An SVI index is helpful to governments and communities because it identifies and acknowledges which additional support and attention is needed to mitigate the harmful impacts of harmful environmental exposure. 
Our model approximates the spatially distributed ozone measurements on a surface, thereby predicting low-level ozone. In addition, by including the SVI and the Environmental Justice Index (EVI), our model calls for a better predictive tool. This tool can inform air quality and help determine which communities are most at risk. Our computational mathematical method also quantifies the uncertainty associated with our predictions and helps us identify the spatial distribution of low-level ozone among the most vulnerable communities.

## Interested in Learning More?
Please see our [manuscript](content/2023-Ozone-Manuscript.pdf) or [poster](content/2023-Ozone-Poster.pdf).
