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


  <center>
  <figure style="width:800px; text-align:left;" class="half"> 
      <a href="/assets/images/IDETC_2021/humanoid_2D.JPG"><img src="/assets/images/IDETC_2021/humanoid_2D.JPG"></a>
      <a href="/assets/images/IDETC_2021/humanoid_2D.JPG"><img src="/assets/images/IDETC_2021/MATLAB_sim_diagram.JPG"></a>
      <figcaption>Humanoid Model: (a) configuration variables describing the degrees of freedom, (b) mass, center of mass, inertia about center of mass, and length parameters </figcaption>
  </figure>
  </center>


Used a 2D, 5-link biped model with four actuators (one in each hip and one in each knee). The model is under-actuated as there are five DOFs (with the addition of torso position) but only four actuated ones. The physics parameter such as link mass and inertia were approximated to those of the average adult male. The simulator was developed in MATLAB where I used two sets of equations for the simulation model. 

### Equations

Using Euler-Lagrange's method I formulated 7 equations of motion for 7 states (x, y, Θ0, Θ1, Θ2, Θ3, Θ4). The first equation used in the simulator is the equation of motion for the 5 DOF states. This equation is used during the single stance phase where one foot is on the ground and the model behaves like an inverted pendulum.

The single stance ends and the foot-strike phase begins when the swing foot C_2 touches the ground. It is assumed that the trailing leg pushes off with an impulseive force I_C1 along the stance leg assimlating ankle push-off. Using the assumption that energy and momentum are conserved and integrating the EOM for the 7 states and taking he limit as time --> 0 the footstrike equation was derived to solve for the states after collision.

<figure class="half">
    <a href="/assets/images/IDETC_2021/single_stance2.JPG"><img src="/assets/images/IDETC_2021/single_stance2.JPG"></a>
    <a href="/assets/images/IDETC_2021/foot-strike.JPG"><img src="/assets/images/IDETC_2021/foot-strike.JPG"></a>
    <figcaption></figcaption>
</figure>
<figure class="half">
    <a href="/assets/images/IDETC_2021/Euler-Lagrange.JPG"><img src="/assets/images/IDETC_2021/Euler-Lagrange.JPG"></a>
    <a href="/assets/images/IDETC_2021/foot-strike-eq.JPG"><img src="/assets/images/IDETC_2021/foot-strike-eq.JPG"></a>
    <figcaption>(Left) Single stance. (Right) Foot-strike.</figcaption>
</figure>

The figure below shows the general equation describing a single step. the repeating unit, that starts and ends at mid-stance. 
* Phase 1: Single stance equation integrated until foot-strike
* Transition 1: Occurs when swing foot (c_2) touches the ground.
* Phase 2: Foot-strike equation is applied and legs are swapped.
* Phase 3: Single stance equation integrated until midstance.
* Transition 2: Occurs when biped is in midstance (Θ0+Θ1=0)


### Controller

As the model is underactuated, the states chosen for control are the swing leg hip, torso, and both knees. Use aprtial feedback linearization (PFL) to balance nonlinear terms and simplify the controller. 

Using Euler-Lagrange's method I formulated 7 equations of motion for 7 states (x, y, Θ0, Θ1, Θ2, Θ3, Θ4). The first equation used in the simulator is the equation of motion for the 5 DOF states. This equation is used during the single stance phase where one foot is on the ground and the model behaves like an inverted pendulum.

The single stance ends and the foot-strike phase begins when the swing foot C_2 touches the ground. It is assumed that the trailing leg pushes off with an impulseive force I_C1 along the stance leg assimlating ankle push-off. Using the assumption that energy and momentum are conserved and integrating the EOM for the 7 states and taking he limit as time --> 0 the footstrike equation was derived to solve for the states after collision.

<iframe width="560" height="315" src="https://www.youtube.com/embed/-UL-wkv4XF8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>






