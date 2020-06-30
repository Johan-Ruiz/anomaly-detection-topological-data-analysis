---
layout: page
mathjax: true
title: 1. Nearest Neighbor
published: true
---
## $k-$NN Algorithms

Let $\chi$ be our data set. Any $k-$NN algorithm can be characterize by the way it complete the next three processes: 

- Definition of a neighborhood $N_{k}(x)$ for every point $x \in \chi$.
- Computing of the average behavior inside this neighborhood by means of a certain function $f$ over $N_{k}(x)$.
- Comparisson of the $f$ values.

### Local Outlier Factor (LOF) 

LOF algorithm was desing as an improvement of the basic $k-$NN and $k^{th}-$NN algorithms whose neighborhoods are defined by proximity $N_k(x)={x_i \in \chi: d(x,x_i) \leq 
d(x,x_{i+1}) \wedge k=1,...,k}$

El algoritmo LOF se diseñó teniendo en cuenta que la sola idea de aislamiento no era suficiente para caracterizar una anomalía. Intuitivamente, LOF calcula nuevamente el costo en términos de distancia de cada punto para alcanzar a sus $k$ vecinos, y luego compara este costo entre los mismos vecinos en busca de una comportamiento común, de tal forma que $LOF_k(x) \approx 1$ implica que $x$ es normal. Es decir, si los $k$ vecinos de $x$, $x_1 \dots x_k$, están muy cerca de él, de tal forma que los $k$ vecinos de $x_i$ son, a su vez, muy próximos a él entonces se tendrá un comportamiento común que es estar en un grupo denso. \\

Como $d(o,C_2)=d(o,x_1)<d(o,x_i)$, para $i=2 \dots k$, entonces $kd(o,x_1)<\sum_{i=1}^{k} d(o,x_i)$ y

\begin{equation*}
\begin{split}
d(o,x_1)< \frac{1}{k}\sum_{i=1}^{k} d(o,x_i)= (LDR_k(o))^{-1}
\end{split}
\end{equation*}

y teniendo en cuenta que $C_1$ y $C_2$ son localmente densos, para valores de $k$ adecuados, $LOF_k(x)=1$ para cada cualquier $x \neq o$. Además para cualesquiera $x_i \in N_k(o)$ y $x_j^{(i)} \in N_k(x_i)$ se tiene que $d(x_i,x_{j}^{(i)}) \leq j \epsilon $, y \\

\begin{equation*}
    \begin{split}
        (LRD_k(x_i))^{-1} &= \frac{1}{k} \sum_{j=1}^{k}d(x_i,x_{j}^{(i)}) \\
         &\leq \frac{1}{k} \sum_{j=1}^{k} j \epsilon\\
        &= \frac{(k+1)\epsilon}{2}, 
    \end{split}
\end{equation*}

es decir, $\frac{2}{\epsilon (k+1)} \leq LRD_k(x_i)$, para todo $x_i \in N_k(o).$ De esto se concluye que 

\begin{equation*}
\begin{split}
LOF_k(o)=& \frac{1}{k}\sum_{i=1}^{k} \frac{LRD(x_i)}{LRD(o)}\\ &>\frac{1}{k}\sum_{i=1}^{k} d(o,C_2)LRD(x_i)\\
& \geq \frac{1}{k} \sum_{i=1}^{k} d(o,C_2) \frac{2}{\epsilon (k+1)} \\
&= d(o,C_2) \frac{2}{\epsilon (k+1)} \\
&= \frac{2d(o,C_2)}{(k+1)d(p_0,q_0)}|C_1|
\end{split}
\end{equation*}

Por ejemplo, si $d(p_0,q_0)=d(o,C_2)+0.1$ y teniendo en cuenta que $k \leq 50$ para $Card(C_1)>52$, $LOF_k(0) > 2$, es decir, su escala de anomalía será muy alta en comparación a la de cualquier otro punto y por ende será etiquetado como anómalo.\\

Aunque LOF aparenta ser el algoritmo definitivo no se tardó en encontrar situaciones donde su desempeño era pobre. En la figura 2  se tienen las siguientes condiciones: \cite{tang2002enhancing}\\


* Dados $x,y \in C_1$ consecutivos, $d(x,y)=1$ y tiene 91 puntos.
* $C_2$ esta conformada por 8 puntos uniformemente distribuidos sobre una circunferencia de radio 1.
* El centro de $C_1$ es colineal con $o_1$ y el punto central de $C_1$.
* $d(C_2,o_1)=1000$ y $d(C_1,o_1)=2$
* $C_2 \cup \left \{ o_1 \right \}$ son puntos anómalos.



<center>
<img src="https://user-images.githubusercontent.com/67338552/86149156-33478100-bac1-11ea-90ef-e990eadf6972.png" height="400" width="400">
</center>


En estas condiciones para $k \leqslant 7$, el algoritmo no reconoce ningún punto de $C_2$ como anómalo. Por ejemplo, si $k=4$, entonces $LOF_4(o_1)=2,055$ pero $LOF(x_i)=1$ para todo $x_i \in C_2$ pues el Local Reachability Distance de todos los puntos es el mismo. Pero si $k \geq 8$ el algoritmo ya no reconoce a $o_1$ como anómalo pues $LOF_8(o_1)=1,4209$ y $LOF(\overline{x_1})=1,0951$, donde $\overline{x_1}$ es el punto central de $C_1$ y $x_1$ el punto de $C_2$ más cercano a $o_1$, mientras que $LOF(x_1)=6,425$, es decir, la marca de anomalía asignada a $o_1$ es irrisoria en comparación a la de $x_1$, de tal forma que puede confundirse con los puntos de $C_1$. Nótese que las escalas de anomalía se incrementan progresivamente a medida que un punto se acerca a los bordes de la recta. Esto ocurre porque la forma de medir, en este caso, mediante la métrica usual de $\mathbb{R}^2$, obliga a los puntos en los extremos a buscar puntos vecinos muy lejanos dado que todos ellos están a un solo lado, (derecha o izquierda dependiendo del extremo en que se encuentre). \\
