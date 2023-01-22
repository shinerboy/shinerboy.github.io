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
  <figure style="width:800px; text-align:left;" class="half"> 
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

By choosing a constant stepping frequency, we can use the S2S map to solve for the foot placement required to achieve the desired velocity or position of the COM wrt the stance foot at foot strike. 
<center>
  <figure style="width:800px; text-align:left;" >
      <a href="/assets/images/2022_Humanoids/Controller_eqsJPG"><img src="/assets/images/2022_Humanoids/Controller_eqs.JPG"></a>
    </figure>
</center>

<iframe width="560" height="315" src="https://www.youtube.com/embed/MniABg2jGEA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>









