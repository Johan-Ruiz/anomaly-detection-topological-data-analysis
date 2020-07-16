---
layout: post
mathjax: true
title: Counting Pieces for Anomaly Detection
published: true
---

In this post I am going to introduce you the main task we solve using TDA and a brief explanation on how to use it as an anomaly detection tool.

### Main Problem

$k-$Nearest Neighbors algorithms ($k-$NN) are widely used for anomaly detection regardless their high sensibility to changes in scale parameter $k$. This shortcoming, here named 
Local-Global Duality, occurs independently to the way nearest neighbors are selected. Topological description of data sets by persistent homology leads to a new model for 
anomaly detection where the multi scale nature of the topological featuring brought by homology persistence solves Local-Global Duality for single anomalies. The proposed 
anomaly detection model leans on the comparison between noteworthy topological changes inducted by single point extractions and the relative topological variation inherent 
to the data set. The relevant changes are measured using the Bottleneck Distance to compare persistent diagrams associated to deformations in data when a single point is 
removed. The proposed model and some $k-$NN algorithms  are compared in some experiments.

<center>
<img src="https://user-images.githubusercontent.com/67338552/85931694-fcd4f080-b88b-11ea-81c4-62b6b1efa17f.png" height="400" width="400">
</center>

### Intuition 

In the image above, section **a)** shows the $\chi$ data set where the *normal* behavior is labeled in blue color and the single anomaly in red color. In this case the amount *pieces* $\beta_0$, better said Connected Components, equals the size of $\chi$, $Card(\chi)$. If $\mathbb{R}^2$ usual topology is held, for a certain radius $r>0$ the subsequent $\chi$ cover of neighborhoods will contain overlapped elements $\{ N_r(x) \}$ in such way all normal points are going to merge in a single piece and the red point remains as a single one, as shown in section **b)**. Therefore we compute $\beta_0 = 2$. 

If a blue point is removed, the connected component assembled by normal dots will keeps its structure as a single piece. Then, as shown in **c)**, we get $\beta_0 = 2$ and roughly speaking *we have done nothing from the topological point of view.* Otherwise, the red anomalous point extraction implies a connected component extraction also. Therefore we can get *subtantial changes* in the $\chi$ cover topology by removing an anomaly and then counting the remaing pieces, computed $\beta_0 = 1$ in the last section **d)**.

The previous analysis shows how anomalies can be characterize by the topological changes they induce. Formally speaking, point extraction leads to point cloud deformations whose topology is then summarized using Persistent Diagrams. Finally, applying Bottleneck Distance, each diagram is compared to the original point cloud topology. It shoud be emphasized every deformation means topological changes from the original shape, even if the come from normal points, howerever its asociated variation creates a pettern whose outline is easy to recognize and then outliers are far away from this *mean variation*.

### Contents
- $k-$NN Algorithms and how the may fail
	- Local Outlier Factor (LOF) Algorithm
    - Connectivity-Based Outlier Factor (COF) Algorithm
- What´s TDA and How it works
	- Computing Persisten Homology
    - Bottleneck Dsitance
- The model
