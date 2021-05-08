---
layout: single
title: "Control of a 5-Link Biped Using Quadratic Polynomial"
permalink: /2021-06-08-post-IDETC-project/
classes: wide
header:
  teaser: /assets/images/IDETC_2021/overview.JPG
  og_image: /assets/images/IDETC_2021/overview.JPG
categories:
  - projects
tags:
  - machine learning
  - EMG recognition
last_modified_at: 2020-09-22T15:12:19-04:00
---

To walk over constrained environments, bipedal robots must meet concise control objectives of speed and foot placement. The decisions made at the current step need to factor in their effects over a time horizon. Such step-to-step control is formulated as a two-point boundary value problem (2-BVP). As the dimensionality of the biped increases, it becomes increasingly
difficult to solve this 2-BVP in real-time. The common method to use a simple linearized model for real-time planning followed by mapping on the high dimensional model cannot capture the
nonlinearities and leads to potentially poor performance for fast walking speeds. I developed a framework for real-time control based on using partial feedback linearization for model reduction, followed by a data-driven approach to find a quadratic polynomial model for the 2-BVP. This simple step-to-step model along with constraints is then used to formulate and solve a quadratically constraint quadratic program to generate real-time control commands. We demonstrate the efficacy of the approach in simulation on a 5-link biped following a reference velocity profile and on a terrain with ditches.

<figure>
    <a href="/assets/images/IDETC_2021/overview.JPG"><img src="/assets/images/IDETC_2021/overview.JPG"></a>
    <figcaption>(a) Partial feedback linearization reduces the stance phase dynamics from Θ = [Θu,Θc] (10 dimensions) to Θ = Θu (2 dimensions). (b) A Poincare section is chosen at mid-stance. I generate random input state at the Poincar´e section and controls at the step and simulate till the next Poincare section to generate data for the Poincar´e map given by F, Θi+1 u = F(Θi u ,U i). (c) The Poincare map is curve fitted Θi+1u = F(Θiu,Ui) where F is a quadratic polynomial model and support vector machine is used to identify the boundary of the model. (d) Nonlinear programming is used to solve a suitably formulated quadratically constrained quadratic program</figcaption>
</figure>



<figure style="width:300px;">
    <a href="/assets/images/IDETC_2021/humanoid_2D.JPG"><img src="/assets/images/IDETC_2021/humanoid_2D.JPG" style="width:100%"></a>
    <figcaption>Humanoid Model: (a) configuration variables describing the degrees of freedom, (b) mass, center of mass, inertia about center of mass, and length parameters </figcaption>
</figure>

Used a 2D, 5-link biped model with physics parameter such as link mass and inertia approximated to those of the average adult male. Used two sets of equations for the simulation model. One equation is for single stance phase where one foot is on the ground and the second if for the foot-strike phase where both legs are on the groud and exchange roles. The swing leg becomes the stance leg and the stance leg becomes the swing leg.



<figure class="half">
    <a href="/assets/images/EMG_pattern_recognition/Conclusion.JPG"><img src="/assets/images/EMG_pattern_recognition/Conclusion.JPG"></a>
    <figcaption></figcaption>
</figure>




