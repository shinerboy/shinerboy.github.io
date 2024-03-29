---
layout: single
title: 2D Approximation of the step-to-step map
permalink: /2022-10-14-post-Humanoids22/
classes: wide
header:
  teaser: /assets/images/2022_Humanoids/LIPM_stepping_MJ3.PNG
  og_image: /assets/images/2022_Humanoids/LIPM_stepping_MJ3.PNG
categories:
  - projects
tags:
  - control
  - Robotics
  - MATLAB
last_modified_at: 2020-09-22T15:12:19-04:00
---

Most bipedal systems are underactuated at the ankle joint because their actuators are not strong enough to counteract the weight of the robot and because the foot starts to rotate when the COM falls outside of the base of support at the foot. This poses a challenge to locomotion that humans and other bipedal animals have been able to overcome by "falling controllably". Walking is in essence falling while breaking the fall by placing the foot in front. Robotic mechanisms seeking to mimic this walking method must understand the dynamics of the system which can be done by integrating the equations of motion much like is done with simulators. Integrating EOM from one instance of a gait cycle to the next as a function of current states and control inputs yields a Poincare map.

<center>
  <figure style="width:600px; text-align:left;" class="half"> 
     <a href="/assets/images/2022_Humanoids/Integration.JPG"><img src="/assets/images/2022_Humanoids/Integration.JPG"></a>
      <a href="/assets/images/2022_Humanoids/LIPM_model.jpg"><img src="/assets/images/2022_Humanoids/LIPM_model.jpg"></a>
      <figcaption>(Left) Integrating EOM yields analytical step-to-step map. (Right) General LIPM </figcaption>
    </figure>
</center>

The drawback of numerically solving for the Poincare map is that it slows down the computation. One alternative solution is using a simplified model. We used the LIPM to simplify the robot dynamics and develop a stepping controller for Digit. The equations of motion of the inverted pendulum become linear by keeping the vertical height of the mass constant. Integrating the EOM gives a S2S map, also known as the Poincare map.

<center>
  <figure style="width:800px; text-align:left;" >
      <a href="/assets/images/2022_Humanoids/EOM.JPG"><img src="/assets/images/2022_Humanoids/EOM.JPG"></a>
    </figure>
</center>
By choosing a constant stepping frequency, we can use the S2S map to solve for the foot placement required to achieve the desired velocity or position of the COM wrt the stance foot at foot strike. The S2S map is reformaulated such that the control input is step length (u). A feedback term is introduced making the controller a discrete controller with feedback. Gains can be tuned such that the system reaches orbital stability. 
<center>
  <figure style="width:1000px; text-align:left;" class="half">
      <a href="/assets/images/2022_Humanoids/Controller_eqs.JPG"><img src="/assets/images/2022_Humanoids/Controller_eqs.JPG"></a>
      <a href="/assets/images/2022_Humanoids/LIPM_stepping_MJ3.PNG"><img src="/assets/images/2022_Humanoids/LIPM_stepping_MJ3.PNG"></a>
    </figure>
</center>
<center>
  <iframe width="560px" height="200px" src="https://www.youtube.com/embed/_9bOyELROho" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</center>
One major drawback from using the simpplified model dynamics of the LIPM is that there might be a steady-state error that arises due to the dynamic differences between the LIPM and robot dynamics. 
<center>
  <figure style="width:500px; text-align:left;" >
      <a href="/assets/images/2022_Humanoids/Error.JPG"><img src="/assets/images/2022_Humanoids/Error.JPG"></a>
    </figure>
</center>
An alternative way of extracting the S2S dynamics of the system is by capturing the dynamics of certain points of interest such as COM position and velocity and using them as Poincare map parameters. We ran physics simulations of the system walking under LIPM-based stepping and collected waveform kinematic data. The data was converted into point-of-interest data as function of controller inputs. The points of interest are then run through a Support Vector Machine (SVM) classifier where we use the classification hyperplane equation to classify the data as either feasible or infeasible. Basically, separating data for which the robot succesfully takes a step and when the robot falls or slips. The feasible data is then fitten to a function using polynomial regression. This function is now an analytical version of the Poincare map equation.

<center>
  <figure style="text-align:left;" class="half"> 
     <a><iframe width="560" height="315" src="https://www.youtube.com/embed/MniABg2jGEA?start=4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></a>
     <a href="/assets/images/2022_Humanoids/Decision.JPG"><img src="/assets/images/2022_Humanoids/Decision.JPG" style="height:280px;"></a>
      <figcaption>(Left) Training was done in MuJoCo. (Right) The classification decision boundary </figcaption>
    </figure>
</center>
The feasible data was fitted to an analytical polynomial S2S map shown below. A discrete and non-linear controller was formulated. The error S2S dynamics were linearized about an equilibrium point and the gain K was solved for such that the system became asymptotically stable. 
<center>
  <figure style="width:900px; text-align:left;"> 
      <div class="row">
        <div class="column">
          <img src="/assets/images/2022_Humanoids/S2S_eqs.JPG" style="width:60%">
          <img src="/assets/images/2022_Humanoids/Nonlinear_controller.JPG" style="width:30%">
        </div>
      </div>
      <figcaption>(Left) Polynomial S2S map (Right) Discrete and nonlinear stepping controller </figcaption>
    </figure>
</center>
Having such types of analytical maps and analytical boundaries allows the formulation of an optimization problem that can be used to optimize foot placement to achieve desired walking speed, recover from a fall, or walk through a constrained environment. The best part is that these analytical models are typically of low order and can be solved for very fast for real-time control. 
<center>
  <figure style="width:900px; text-align:left;" >
      <a href="/assets/images/2022_Humanoids/QCQP.JPG"><img src="/assets/images/2022_Humanoids/QCQP.JPG"></a>
      <figcaption>The formulated quadratically constrained quadratic program (QCQP) can be used to minimize the walking parameter (e.g. COM velocity or position at foot strike) error. The analytical model is used as an equality constraint and the feasible boundary is used as an inequality constrained. Furthermore, stepping constraints can be added to acount for safe and unsafe regions that the robot can step on. </figcaption>
    </figure>
</center>
QCQP implementation:
<iframe height="100px" src="https://www.youtube.com/embed/MniABg2jGEA?start=151" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
A foot strike corrected stepping controller was also implemented to account for interstep disturbances that may occur during walking. 
<center>
  <figure style="width:900px;" >
      <a href="/assets/images/2022_Humanoids/Footstrike_corrected.JPG"><img src="/assets/images/2022_Humanoids/Footstrike_corrected.JPG"></a>
      <figcaption> The footstrike-corrected controller updates the robot states continuously as opposed to discretely. This allows for the stepping controller to continuously update the footplacement up the swing foot during the single support phase of walking. </figcaption>
    </figure>
</center>
<center>
  <figure style="text-align:left;"> 
     <iframe height="100" src="https://www.youtube.com/embed/MniABg2jGEA?start=4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
      <figcaption>The footstrike-corrected stepping controller was tested by pushing the robot during the single support phase during walking. The new controller allowed the robot to recover from the push. </figcaption>
    </figure>
</center>









