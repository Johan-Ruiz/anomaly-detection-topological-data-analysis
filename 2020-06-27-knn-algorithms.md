---
layout: page
mathjax: true
title: 1. Nearest Neighbor Algorithms 
published: true
---
## Small algorithms

[GU16]
[TCFC02]

Let $\chi$ be our data set and $d$ a metric over $\chi$. 

$k-$NN type algoritms [GU16] rely on the **Similarity on Nearby Behavior** principle which means that the common behavior is said to be strongly related to small distances within points inside big masses or cores and outliers are labeled because of their *evident distancing* from them. An *anomaly score* is computed for every $x \in \chi$, whose value is given by some function $f$ and some variation of the set $N_k(x):= ${ $x_i \in \chi: d(x,x_i) \leq d(x,x_{i+1}) \wedge k=1,...,k $} of the $k-$nearest neighbors. 

The Nearest Neighbors simplest models are $k-$NN and $k^{th}-$NN. $k-$NN algorithm sets the $f$ function simply by computing the average distance from $x$ to its neighbors in $N_k(x)$, that is $f(x)=\frac{1}{k}\sum_{i=1}^{k}d(p,x_i)$; and $k^{th}-$NN algorithm chooses the distance to the farthest neighbor $f(x)=d(x, x_{k})$. Once the anomaly score is computed for every point $x$, the expert selects a real threshold $L>0$ in order to compare the scores and decide which one to label to an outlier. 

Other algorithms select the threshold in a different way. For example, the $DB(n,r)-$outlier algorithm [TCFC02] a point $x$ is said to be outlier with respect to $n$ and $r$ if the ball $B_{r}(x)=${ $y : d(x,y)<r$ } contains less than $n$ elements. 


### Local Outlier Factor (LOF) 

LOF algorithm [GU16] was desing as an improvement of the basic $k-$NN and $k^{th}-$NN algorithms. 

LOF algorithm starts to compute a cost function called Local Reachability Distance $LRD(x)= \left ( \frac{1}{k}\sum_{i=1}^{k}d(x,x_i) \right )^{-1}$. The $LRD$ quantities may be seen as the inverse of the values given by the $k-$NN algorithm but the idea is to compute the *local density* of every point for a subsequent comparisson set by the $f$ function, here defined as $LOF(x)= \frac{1}{k}\sum_{i=1}^{k}\frac{LDR(x_i)}{LDR(x)}$. In this case the more $LOF(x) \approx 1$ the more normal a point is.  

Aunque LOF aparenta ser el algoritmo definitivo no se tardó en encontrar situaciones donde su desempeño era pobre. En la figura 2  se tienen las siguientes condiciones: \cite{tang2002enhancing}\\

* $Card(C_1)=91$ and given two consecutive points $x,y \in C_1$, equation $d(x,y)=1$ holds.
* 8 uniformly distributed points over the unit disk assemble $C_2$ set.
* $C_1$ middle point, $C_2$ center and $o_1$ are collinear points.
* $d(C_2,o_1)=1000$ y $d(C_1,o_1)=2$
* Points belonging to $C_2 \cup$ {$ o_1 $} are anomalous.

<center>
<img src="https://user-images.githubusercontent.com/67338552/86149156-33478100-bac1-11ea-90ef-e990eadf6972.png" height="200" width="400">
</center>

Under these conditions,  $k \leqslant 7$ LOF algorithm does not label any point in $C_2$ as anomalous (e.g., $k=4$ means $LOF_4(o_1)=2,055$ but $LOF_4(x_i)=1$ for every $x_i \in C_2$ so the Local Reachability Distance is the same for every point). Otherwise, $k \geq 8$ implies LOF algorithm does not label $o_1$ as anomalous because $LOF_8(o_1)=1,4209$ 
and $LOF(\overline{x_1})=1,0951$, where $\overline{x_1}$ is the middle point of $C_1$ and $x_1$ is the nearest point to $o_1$ in $C_2$ while $LOF(x_1)=6,425$. Therefore the anomaly score given to $o_1$ is pretty small in front of $x_1$ score in such a way it may be confused as a $C_1$ point. 

 Nótese que las escalas de anomalía se incrementan progresivamente a medida que un punto se acerca a los bordes de la recta. Esto ocurre porque la forma de medir, en este caso, mediante la métrica usual de $\mathbb{R}^2$, obliga a los puntos en los extremos a buscar puntos vecinos muy lejanos dado que todos ellos están a un solo lado, (derecha o izquierda dependiendo del extremo en que se encuentre). \\
