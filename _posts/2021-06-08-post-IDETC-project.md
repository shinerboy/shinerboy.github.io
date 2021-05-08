---
layout: single
title: ""Control of a 5-Link Biped Using Quadratic Polynomial""
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
To walk over constrained environments, bipedal robots must meet concise control objectives of speed and foot placement. The decisions made at the current step need to factor in their effects over a time horizon. Such step-to-step control is formulated as a two-point boundary value problem (2-BVP). As the dimensionality of the biped increases, it becomes increasingly
difficult to solve this 2-BVP in real-time. The common method to use a simple linearized model for real-time planning followed by mapping on the high dimensional model cannot capture the
nonlinearities and leads to potentially poor performance for fast walking speeds. I developed a framework for real-time control based on using partial feedback linearization for model reduction, followed by a data-driven approach to find a quadratic polynomial model for the 2-BVP. This simple step-to-step model along with constraints is then used to formulate and solve a quadratically constraint quadratic program to generate real-time control commands. We demonstrate the efficacy of the approach in simulation on a 5-link biped following a reference velocity profile and on a terrain with ditches.

<figure class="half">
    <a href="/assets/images/IDETC_2021/overview.JPG"><img src="/assets/images/IDETC_2021/overview.JPG"></a>
    <a href="/assets/images/IDETC_2021/humanoid_2D.JPG"><img src="/assets/images/IDETC_2021/humanoid_2D.JPG"></a>
    <figcaption></figcaption>
</figure>

<figure class="half">
    <a href="/assets/images/EMG_pattern_recognition/Results.JPG"><img src="/assets/images/EMG_pattern_recognition/Results.JPG"></a>
    <a href="/assets/images/EMG_pattern_recognition/Discussion.JPG"><img src="/assets/images/EMG_pattern_recognition/Discussion.JPG"></a>
    <figcaption></figcaption>
</figure>

<figure class="half">
    <a href="/assets/images/EMG_pattern_recognition/Conclusion.JPG"><img src="/assets/images/EMG_pattern_recognition/Conclusion.JPG"></a>
    <figcaption></figcaption>
</figure>




