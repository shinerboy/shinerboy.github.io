---
layout: single
title: "Passive Swinging-Arms Exoskeleton for Angular Momentum Reduction"
permalink: /2022-02-06-post-Arms-Exo/
classes: wide
header:
  teaser: /assets/images/Swinging_Exo/Exo_01.JPG
  og_image: /assets/images/Swinging_Exo/Exo_01.JPG
categories:
  - projects
tags:
  - exoskeleton
  - walking model
last_modified_at: 2020-09-22T15:12:19-04:00
---

Robotic rehabilitation is important in assisting patients who are physically challenged in order to improve their mobility. For my Assistive Robotics course my team and I developed a novel low-cost passive exoskeleton with swinging arms that helps in assisting people with upper-body limb disabilities. The team hypothesized that the swinging arms help by reducing the metabolic cost of arm-amputated patients and in reducing their Angular Momentum (AM) along the vertical axis. Various configurations of the swinging arms were studied and the results between no assistance and the exo-assisted conditions were compared. The results showed that the swinging arm of the device help in reducing the AM along the vertical axis. However, the metabolic cost was not reduced by the wearable device

  <center>
  <figure style="width:800px; text-align:left;" class="half"> 
      <a href="/assets/images/Swinging_Exo/Exo_02.JPG"><img src="/assets/images/Swinging_Exo/Exo_02.JPG"></a>
      <a href="/assets/images/Swinging_Exo/Exo_03.JPG"><img src="/assets/images/Swinging_Exo/Exo_03.JPG"></a>
      <figcaption>(Left) CAD model od the device. (Right) Subject wearing the improved exoskeleton design with slider joint during single-stance (a), push-off (b), and heel-strike (c). </figcaption>
  </figure>
  </center>

The weight and placement of the weight were varied to find the optimal configuration. Three weights were tested based on a percentage of the subject’s weight. The arm design accounts for two weight placements (6 inches and 12 inches) from the hip. By placing the weight at different points along the arm, the angular momentum of the arm will vary and affect the vertical angular momentum of the user. 

### Physics Model

A human five-segment physics model consisting of one torso, two thighs and two shins was used for computing the AM. Feet were assumed to be point-feet and mass-less, shown in the figure. Anthropometric properties such as segment center of mass, inertia tensor and axis frame location and orientation were calculated from methods in literature.


  <figure class="half">
    <a href="/assets/images/Swinging_Exo/Exo_04.JPG"><img src="/assets/images/Swinging_Exo/Exo_04.JPG"></a>
    <a href="/assets/images/Swinging_Exo/Exo_06.JPG"><img src="/assets/images/Swinging_Exo/Exo_06.JPG"></a>
    <figcaption>(Left) Five-segment physics model. (Right) TExperimental setup of a trial with exo on condition and 3.75 lbs of weight place at the 12 inch configuration.  </figcaption>
</figure>

The data was used to solve for AM along the x-axis (foreaft direction) and y-axis (vertical direction) at every step with respect to the world frame. Segment center of mass velocity data was approximated using numerical integration and the central difference theorem. Each segment contributes to a remote AM and a local AM where the sum gives the total AM of the segment.

  <center>
  <figure style="width:800px; text-align:left;" > 
      <a href="/assets/images/Swinging_Exo/Exo_05.JPG"><img src="/assets/images/Swinging_Exo/Exo_05.JPG"></a>
      <figcaption>Whole-body angular momentum equation</figcaption>
  </figure>
  </center>

### Results

The experiments conducted yielded evidence of significant differences in x-axis AM in the exo no weights and exo stiff arms (no swing) condition showing a 6.12% (p-value: 2.72e-9) and 12.10% (p-value: 2.72e-37) reduction, respectively. Significant differences in y-axis AM were also seen in which all four exo on conditions showed reduction. The exo placed at 6 inches from hip and with 3.75 lbs of weight showed the best improvement with an 11.55% (p-value: 8.63e-8) reduction, followed by the 6in 1.25lbs configuration with an improvement of 9.86% (p-value: 1.61e-5), followed by the no weight condition and the 12in 3.75lbs condition with reductions of 8.64% and 7.57% respectively and p-values of 2.73e-5 and 9.63e-5 respectively. Y-axis AM was reduced in all exo configurations. Most configurations show a lower absolute y-axis AM between 0-25% and between 60-100% of a stride cycle. No significant change in x-axis AM was seen for any of the weighted exo configurations.

<figure class="half">
    <a href="/assets/images/Swinging_Exo/Exo_07.JPG"><img src="/assets/images/Swinging_Exo/Exo_07.JPG"></a>
    <a href="/assets/images/Swinging_Exo/Exo_08.JPG"><img src="/assets/images/Swinging_Exo/Exo_08.JPG"></a>
    <figcaption>(Left) Experimental data detailing the exoskeleton effects on AM about x-axis (top) and vertical axis (bottom) during the gait cycle. (Right) Top: Mean x and vertical AM expereinced during one gait cycle. Bottom: Percent improvement in AM when compared to no exo condition.  </figcaption>
</figure>








