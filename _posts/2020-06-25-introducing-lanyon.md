---
layout: post
mathjax: true
title: Counting Pieces for Anomaly Detection
published: true
---

![](https://user-images.githubusercontent.com/67338552/85931694-fcd4f080-b88b-11ea-81c4-62b6b1efa17f.png){: style="center" height="350px" width="350px"}

20 In this post I am going to introduce you to TDA and how to use it as an anomaly detection tool.

## Main Problem

$k-$Nearest Neighbor algorithms ($k-$NN) are widely used for anomaly detection regardless their high sensibility to changes in scale parameter $k$. This shortcoming, here named 
Local-Global Duality, occurs independently to the way nearest neighbors are selected. Topological description of data sets by persistent homology leads to a new model for 
anomaly detection where the multi scale nature of the topological featuring brought by homology persistence solves Local-Global Duality for single anomalies. The proposed 
anomaly detection model leans on the comparison between noteworthy topological changes inducted by single point extractions and the relative topological variation inherent 
to the data set. The relevant changes are measured using the Bottleneck Distance to compare persistent diagrams associated to deformations in data when a single point is 
removed. The proposed model and some $k-$NN algorithms  are compared in some experiments.
