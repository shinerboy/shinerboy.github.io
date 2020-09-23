---
layout: single
title: "Project: Surface EMG Pattern Recognition for Hand Gestures Based on Hierarchical Clustering"
classes: wide
header:
  teaser: /assets/images/yosemite.jpg
  og_image: /test/assets/images/page-header-og-image.png
categories:
  - projects
tags:
  - machine learning
  - EMG recognition
last_modified_at: 2017-10-26T15:12:19-04:00
---
This project was presented at the Artificial Inteligence symposium as part of my Machine Learning course final project.

Myoelectric arm prosthetics offer more diverse functionalities than other prosthetic types. However, most myoelectric prosthetics have limitations to their functionality due to difficulty in classifying muscle data defining the intent of the user’s actions. This project demonstrates an application of Machine Learning to classify and predict hand gesture patterns using Electromyography (EMG) muscle activity data samples. Data preprocessing was done to denoise frequency signals for a smooth feature extraction. Three classification models were tested based on kNN: a) A conditional probability prediction of new sample sets based on the similarities to the training set, b) A k-means categorical cluster with a fixed k cluster grouping data points(gestures and features) based on their similarities, c) A hybrid hierarchical cluster, modified to address variations in signal activity from different subjects. Overall, the subject k-means model yielded an 84% prediction accuracy and 22.01 response time, which was an optimal metric in comparison to the other proposed models.





