---
layout: page
mathjax: true
title: 2. Topological Data Analysis and More
published: true
---

### Algoritmo de TDA para persistencia homológica

\begin{figure}[H]
\centering
\includegraphics[width=8.5cm]{1}
\caption{Evolución de un complex con vértices $ a,b,c,d,e,f,g$.}
\end{figure}

Sea $I$ un conjunto ordenado que indexa todos los símplices de la filtración $\{ K^l \}$ de tal forma que si $i,j \in I$ con $i<j$ entonces $\sigma_i \leqslant \sigma_j$ y 
se dice que el símplice $\sigma_i$ nace antes que el símplice $\sigma_j$. Sea $C_p^l$ el grupo abeliano de $p-$cadenas del complex $K^l$, donde se define la suma entre 
cadenas como sigue: si $\{ \sigma_i^l \}_{i \in I_p^l}$ es el conjunto de $p-$símplices de $K^l$, donde $I_p^l$ es una cadena en $I$, entonces cualquier $p-$cadena es de la 
forma $c_p=\sum_{i \in I_p^l} \xi_i \sigma_i^l$ con $\xi_i \in \mathbb{Z}_{2}$ y $c_p+c_p'= \sum_{i \in I_p^l} (\xi_i + \xi_i^{'}) \sigma_i^l$. En ocasiones nos referiremos 
a los símplices $\sigma_i^l$ con coeficiente $\xi \neq 0$ como los eslabones de $\sum_{i \in I_p^l} \xi_i \sigma_i^l$. También se define el operador de frontera $\partial$ como
el homomorfismo

\begin{center}
$
\partial_{p}^l:\begin{matrix}
C_p \rightarrow  C_{p-1}\\ 
\sigma_i^l \mapsto \sum_{k=1}^{p+1} (-1)^{k} \widetilde{\sigma_i^{lk}},
\end{matrix}
$  
\end{center}

donde $\widetilde{\sigma_{i}^{lk}}$ consiste en el $(p-1)-$símplice que se obtiene de quitar la $k-$ésima componente de $\sigma_i^l$ y los -1 únicamente indican orientación 
invertida \footnote{Por ejemplo, si los $1-$símplex están ordenados de tal forma que $a<b<c$, siendo el símplice más joven el mayor en la cadena, entonces la cadena $ab+bc-ac$ 
indica que recorremos el borde del triángulo de vértices $abc$ en sentido antihorario. Aquí el signo negativo del término $ac$ índica que nos dirigimos de $c$ a $a$.}. 
Se satisface la propiedad fundamental $\partial_{p+1}^l \partial_p^l \equiv 0$, de tal forma que si $Z_p^l=ker\partial_p^l$ y $B_p^l=Im\partial_{p+1}^l$, se concluye 
$B_p^l \leq Z_p^l$ y por la conmutatividad de $C_p^l$ es posible construir el conjunto cociente $H_p^l=Z_p^l/B_p^l$, conocido como el grupo de $p-$homología de $K^l$. 
Los conjuntos $Z_p^l$ y $B_p^l$ se denominan el conjunto de $p-$ciclos y $p-$fronteras de $K^l$ respectivamente.

Si existe una cadena $\partial \in B_p^l$ tal que para dos $p-$ciclos $\sigma$ y $\sigma'$ se verifica $\partial=\sigma+\sigma'$ se dirá que dichos ciclos son homólogos.
Además, como $\sigma'= -\sigma'= \sigma-\partial= \sigma+\partial \in \sigma + B_p^l$ \footnote{Recordemos que el signo negativo únicamente indica la orientación del símplex.},
entonces $\sigma + B_p^l \cap \sigma' + B_p^l \neq \O $. Se concluye que $\sigma$ y $\sigma'$ son homólogos si y solo si $\sigma + B_p^l = \sigma' + B_p^l$.

Nótese que $C_p^l=<\sigma_i^l>_{i \in I_p^l}$ implica que $C_p^l$ es un grupo libre y, por lo tanto, para todo subgrupo $A\leqslant C_p^l$ existe $I'_p \subseteq I_p^l$ tal que
$A=<\sigma_i^l>_{i \in I'_p}$. Como las \textit{bases} no son únicas si el grupo no es trivial, existen $p-$cadenas $c_i^l$ con $i \in I_p^l$ tales que 
$C_p^l=<c_i^l>_{i \in I_p^l}$ y lo propio para los subgrupos $A=<\sigma_i^l>_{i \in I''_p}$ con $I''_p \subseteq I_p^l$. De aquí se concluye que existen subconjuntos
$Z,B \leqslant I_p^l$ tales que $Z_p^l=<c_i^l>_{i \in Z}$ y $B_p^l=<c_i^l>_{i \in B}$ y como $B_p^l\leqslant Z_p^l$ el conjunto $\{c_i^l\}_{i \in Z} \setminus B_p^l$ 
contiene a los representantes de las clases en $H_p^l$. Supongamos que cada representante puede ser etiquetado por un único símplex $\sigma_{i*}$. Dichos $p-$símplices y sus
$p-$ciclos correspondientes se denominarán símplices positivos y ciclos no delimitantes respectivamente, y todo símplice que no sea positivo se dirá que es negativo.

Una primera aproximación al estudio de persistencia homológica se hace mediante los grupos de homología, los cuales pueden ser descritos por los representantes de las clases 
no triviales. Así, por la observación del párrafo anterior, los $p-$grupos de homología pueden ser descritos usando solamente los símplices positivos y la persistencia 
homológica sería cuestión de saber cuando un representante nace y cuando muere, y esto último es lo mismo que preguntarse cuando su clase módulo $p-$frontera se 
\textit{mezcla} con otra, es decir, cuando $\sigma_{i*}+B_p^l$ verifica $\sigma_{i*}+B_p^{l+t}=\sigma_{i**}+ B_p^{l+t}$, con $i* \neq i**$.

El algoritmo para determinar qué símplices son positivos se llama Método de Reducción y parte de la representación del operador de frontera por medio de una matriz 
$M_{\partial_p^l}$ de tamaño $rankC_{p-1}^l \times rankC_p^l$, donde a cada $(p-1)-$símplex se le asigna una fila y cada $p-$símplex una columna. Se define 
$M_{\partial_p^l}[i,j]= \xi_i $ si $\partial_p^l [\sigma_{j}^l]=\sum_{i \in I_{p-1}^l}  \xi_i \sigma_{i}^l$ \textbf{(1)}. Se llama Método de Reducción porque consiste en 
reducir $M_{\partial_p^l}$ a su mínima expresión mediante las operaciones fila y columna usuales, (como intercambio de la columna (fila) $i$ por la columna (fila) 
$i'$, el reemplazo de la columna (fila) $i$ por un múltiplo no nulo de si misma y la sustitución de la columna (fila) $i$ por ella más un multiplo de una columna (fila) $i$).
Esta matriz mínima asociada se conoce con el nombre de forma de Smith y su configuración por bloques es 
\[ \left[ \begin{array}{c|c} I_{r} & 0_{r \times (rank C_p^l-r) } \\ \hline 0_{(rank C_{p-1}^l-r)\times r} & 0_{ (rankC_{p-1}^l-r)\times (rank C_p^l-r)} \end{array} \right] \]
donde  $I_{r}$ denota la matriz identidad de tamaño $r \times r$ y los ceros las matrices nulas de los tamaños correspondientes.

Como \textbf{(1)} indica, la columna $j$ representa la $(p-1)-$cadena $\partial_p^l [\sigma_{j}^l]=\sum_{i \in I_{p-1}^l}  \xi_i \sigma_{i}^l$, de modo que las operaciones 
columna también pueden entenderse como suma de cadenas. Por consiguiente, si se tiene en cuenta que el operador de frontera es un homomorfismo, si $\sigma_{j}^l$ es el símplex
asociado a la columna $j$ y $\sigma_{j'}^l$ el asociado a la columna $j'$, la nueva columna $j=j+j'$ puede ser representada por la cadena $\sigma_{j}^l+\sigma_{j'}^l$, pues
$\partial_p^l [\sigma_{j}^l]+\partial_p^l [\sigma_{j'}^l]=\partial_p^l [\sigma_{j}^l+\sigma_{j'}^l]$ y si existen índices $j_1,j_2,...,j_s$ tales que 
$\partial_p^l[ \sigma_{j}^l]=\partial_p^l[\sum_{t=1}^{s}\sigma_{j_t}^l$], entonces  $\partial_p^l [\sigma_{j}^l-\sum_{t=1}^{s}\sigma_{j_t}^l]=0$ y la columna $j$ estaría 
representada por la cadena $\sigma_{j}^l-\sum_{t=1}^{s}\sigma_{j_t}^l \in Z_p^l=ker\partial_p^l$. Luego, como las operaciones columna (fila) preservan el rango de la matriz,
en la forma normal de Smith las cadenas que representan las columnas conforman una nueva base de $C_p^l$ y por lo tanto las que representan las columnas nulas conforma una base
de $ Z_p^l$. De forma análoga, los representantes de las columnas no nulas resultan ser los eslabones de las cadenas cuya frontera es no nula, por consiguiente sus respectivas
imágenes por el operador de frontera forman una base de $B_{p-1}^l=Im\partial_{p}^l$. El tamaño de la matriz identidad inmersa en la forma de Smith indica implísitamente los
valores de $rankZ_p^l$ y $rankB_{p-1}^l$, pues de acuerdo a lo mencionado anteriormente es claro que el número de columnas nulas corresponde al valor de $rankZ_p^l=rankC_p-r$
y $rankB_{p-1}^l=r$

\begin{figure}[H]
\centering
\includegraphics[width=8.5cm]{2}
\caption{Ciclos base $ad$ y $ag$ de $Z^1_1$.}
\end{figure}

Ahora es posible argumentar la existencia de los símplices positivos. Como los $p-$símplex están ordenados según el orden de aparición, en la matriz $M_{\partial_p^l}$ las 
columnas pueden ser organizadas siguiendo este mismo orden, de tal forma que la primer columna nula está representada por una cadena de la forma 
$\sigma_{j}^l-\sum_{t=1}^{s}\sigma_{j_t}^l$, donde $j>$máx$\{j_1,j_2,...,j_s\}$. Esto implica que todos los representantes de las anteriores columnas continúan siendo 
$p-$símplices y también que es posible emplear a $\sigma_{j}^l$ como etiqueta del ciclo sin ambigüedad. De manera análoga, si se da el caso que el representante de la 
columna $j'$ es de la forma $\sigma_{j'}^l-\sum_{t=1}^{s'}\sigma_{j'_t}^l-\sigma_{j}^l$, donde $j'>$máx$\{j'_1,j'_2,...,j'_{s'}\}$ y el único símplex etiquetador es 
$\sigma_{j}^l$ entonces  \begin{equation*}


\begin{split}
\partial_p^l [\sigma_{j'}^l] &= \partial_p^l [\sum_{t=1}^{s'}\sigma_{j'_t}^l+\sigma_{j}^l]   \\
		& = \partial_p^l [\sum_{t=1}^{s'}\sigma_{j'_t}^l] +  \partial_p^l [+\sigma_{j}^l]\\
        & = \partial_p^l [\sum_{t=1}^{s'}\sigma_{j'_t}^l] +  \partial_p^l [\sum_{t=1}^{s}\sigma_{j_t}^l]\\
        & = \partial_p^l [\sum_{t=1}^{s'}\sigma_{j'_t}^l+\sum_{t=1}^{s}\sigma_{j_t}^l]\\
        & = \partial_p^l [\sum_{t=1}^{s''}\sigma_{j''_t}^l]
\end{split}
\end{equation*} donde ninguno de los $\sigma_{j''_t}^l$ es etiquetador. Luego $\sigma_{j'}^l-\sum_{t=1}^{s''}\sigma_{j''_t}^l$ es la cadena representante de la columna $j'$. Así hemos demostrado que todo ciclo puede ser etiquetado de manera única por el símplice asociado inicialmente a la columna y que siempre es posible construir una representación del ciclo que no incluya etiquetadores anteriores. Estos ciclos etiquetadores son precisamente los símplices positivos siempre y cuando su ciclo asociado no sea la frontera de una $(p+1)-$cadena, es decir, siempre y cuando dicha cadena no este en $Im\partial_{p+1}^l=B_p^l$. 
\\


En la figura 3 se muestran dos complex $K^1$ y $K^2$ de una misma filtración, donde $K^1<K^2$ por orden de aparición. La mayor dimensión se alcanza en el complejo $K^2$ con los
2-símplex $abc,abd, acd$ y $bcd$. En el caso de $K^1$, como $C_p=\{0\}$ para $p>1$ se tiene que $B_1^1=\{0\}$ y además, la matriz $M_{\partial_{1}^{1}}$ que representa al 
operador de frontera en dicho complex es\\  

\begin{table}[H]
\centering
\begin{tabular}{|c|cccccccc}
\hline
  & \multicolumn{1}{c|}{ab} & \multicolumn{1}{c|}{bc} & \multicolumn{1}{c|}{cd} & \multicolumn{1}{c|}{ad} & \multicolumn{1}{c|}{de} & \multicolumn{1}{c|}{ef} & \multicolumn{1}{c|}{fg} & \multicolumn{1}{c|}{ag} \\ \hline
a & -1                      & 0                       & 0                       & -1                      & 0                       & 0                       & 0                       & -1                      \\ \cline{1-1}
b & 1                       & -1                      & 0                       & 0                       & 0                       & 0                       & 0                       & 0                       \\ \cline{1-1}
c & 0                       & 1                       & -1                      & 0                       & 0                       & 0                       & 0                       & 0                       \\ \cline{1-1}
d & 0                       & 0                       & 1                       & 1                       & -1                      & 0                       & 0                       & 0                       \\ \cline{1-1}
e & 0                       & 0                       & 0                       & 0                       & 1                       & -1                      & 0                       & 0                       \\ \cline{1-1}
f & 0                       & 0                       & 0                       & 0                       & 0                       & 1                       & -1                      & 0                       \\ \cline{1-1}
g & 0                       & 0                       & 0                       & 0                       & 0                       & 0                       & 1                       & 1                       \\ \cline{1-1}
\end{tabular}
\end{table}

con forma Smith asociada,

\begin{table}[H]
\centering
\begin{tabular}{|c|cccccccc}
\hline
  & \multicolumn{1}{c|}{ab} & \multicolumn{1}{c|}{bc} & \multicolumn{1}{c|}{cd} & \multicolumn{1}{c|}{de} & \multicolumn{1}{c|}{ef} & \multicolumn{1}{c|}{fg} & \multicolumn{1}{c|}{ad-cd-bc-ab} & \multicolumn{1}{c|}{ag-fg-ef-de-cd-bc-ab} \\ \hline
b & 1                       & 0                       & 0                       & 0                       & 0                       & 0                       & 0                                & 0                                         \\ \cline{1-1}
c & 0                       & 1                       & 0                       & 0                       & 0                       & 0                       & 0                                & 0                                         \\ \cline{1-1}
d & 0                       & 0                       & 1                       & 0                       & 0                       & 0                       & 0                                & 0                                         \\ \cline{1-1}
e & 0                       & 0                       & 0                       & 1                       & 0                       & 0                       & 0                                & 0                                         \\ \cline{1-1}
f & 0                       & 0                       & 0                       & 0                       & 1                       & 0                       & 0                                & 0                                         \\ \cline{1-1}
g & 0                       & 0                       & 0                       & 0                       & 0                       & 1                       & 0                                & 0                                         \\ \cline{1-1}
a & 0                       & 0                       & 0                       & 0                       & 0                       & 0                       & 0                                & 0                                         \\ \cline{1-1}
\end{tabular}
\end{table}

Los ciclos $ad-cd-bc-ab$ y $ag-fg-ef-de-cd-bc-ab$ serán etiquetados como $ad$ y $ag$, como se muestra en la figura 2. Como $\beta_1^1=rankH_1^1=rankZ_1^1-rankB_1^1$, donde
$Z_1^1=<ad,ag>= \{ ad,ag,ad+ag,0 \}$ y $B_1^1= \{ 0 \}$, se concluye que $\beta _1^1=2-0=2$, lo cual coincide con lo que se ve en la imagen, pues $K^1$ tiene dos huecos.\\

Como en el caso $K^2$ se tiene $C_2^2 \neq \{0\}$, entonces $B_2^2 \neq \{0\}.$ Dado que nuestra meta es calcular $H^2_1$ es necesario conocer una base para $B^2_1$, la cual 
se obtiene llevando a la forma de Smith la matriz $M_{\partial_2^2}$\\

\begin{table}[H]
\centering
\begin{tabular}{|c|cccc}
\hline
   & \multicolumn{1}{c|}{abc} & \multicolumn{1}{c|}{bcd} & \multicolumn{1}{c|}{acd} & \multicolumn{1}{c|}{abd} \\ \hline
ab & 1                        & 0                        & 0                        & 1                        \\ \cline{1-1}
bc & 1                        & 1                        & 0                        & 0                        \\ \cline{1-1}
cd & 0                        & 1                        & 1                        & 0                        \\ \cline{1-1}
ac & -1                       & 0                        & 1                        & 0                        \\ \cline{1-1}
ad & 0                        & 0                        & -1                       & -1                       \\ \cline{1-1}
bd & 0                        & -1                       & 0                        & 1                        \\ \cline{1-1}
\end{tabular}
\end{table}

que corresponde a\\

\begin{table}[H]
\centering
\begin{tabular}{|c|cccc}
\hline
   & \multicolumn{1}{c|}{abc} & \multicolumn{1}{c|}{bcd} & \multicolumn{1}{c|}{acd} & \multicolumn{1}{c|}{abd-abc-bcd-acd} \\ \hline
bc & 1                        & 0                        & 0                        & 0                                    \\ \cline{1-1}
bd & 0                        & 1                        & 0                        & 0                                    \\ \cline{1-1}
ad & 0                        & 0                        & 1                        & 0                                    \\ \cline{1-1}
ab & 0                        & 0                        & 0                        & 0                                    \\ \cline{1-1}
cd & 0                        & 0                        & 0                        & 0                                    \\ \cline{1-1}
ac & 0                        & 0                        & 0                        & 0                                    \\ \cline{1-1}
\end{tabular}
\end{table}

Por lo tanto, \\
\begin{equation*}
    \begin{split}
        B_1^2 &= <\partial_2^2[abc],\partial_2^2[bcd],\partial_2^2[acd]>\\
        &= <bc-ac+ab,cd-bd+bc,cd-ad+ac>
    \end{split}
\end{equation*}

\begin{figure}[H]
\centering
\includegraphics[width=11.5cm]{3}
\caption{Fronteras base $bc-ac+ab,cd-bd+bc,cd-ad+ac$.}
\end{figure}

Por su parte, $M_{\partial_1^2}$ y su matriz de Smith asociada son

\begin{table}[H]
\centering
\begin{tabular}{|c|cccccccccc}
\hline
  & \multicolumn{1}{c|}{ab} & \multicolumn{1}{c|}{bc} & \multicolumn{1}{c|}{cd} & \multicolumn{1}{c|}{ac} & \multicolumn{1}{c|}{ad} & \multicolumn{1}{c|}{bd} & \multicolumn{1}{c|}{de} & \multicolumn{1}{c|}{ef} & \multicolumn{1}{c|}{fg} & \multicolumn{1}{c|}{ag} \\ \hline
a & -1                      & 0                       & 0                       & -1                      & -1                      & 0                       & 0                       & 0                       & 0                       & -1                      \\ \cline{1-1}
b & 1                       & -1                      & 0                       & 0                       & 0                       & -1                      & 0                       & 0                       & 0                       & 0                       \\ \cline{1-1}
c & 0                       & 1                       & -1                      & 1                       & 0                       & 0                       & 0                       & 0                       & 0                       & 0                       \\ \cline{1-1}
d & 0                       & 0                       & 1                       & 0                       & 1                       & 1                       & -1                      & 0                       & 0                       & 0                       \\ \cline{1-1}
e & 0                       & 0                       & 0                       & 0                       & 0                       & 0                       & 1                       & -1                      & 0                       & 0                       \\ \cline{1-1}
f & 0                       & 0                       & 0                       & 0                       & 0                       & 0                       & 0                       & 1                       & -1                      & 0                       \\ \cline{1-1}
g & 0                       & 0                       & 0                       & 0                       & 0                       & 0                       & 0                       & 0                       & 1                       & 1                       \\ \cline{1-1}
\end{tabular}
\end{table}

\begin{table}[H]
\centering
\begin{tabular}{|c|cccccccccc}
\hline
  & \multicolumn{1}{c|}{ab} & \multicolumn{1}{c|}{bc} & \multicolumn{1}{c|}{cd} & \multicolumn{1}{c|}{de} & \multicolumn{1}{c|}{ef} & \multicolumn{1}{c|}{fg} & \multicolumn{1}{c|}{ac-ab-bc} & \multicolumn{1}{c|}{ad-cd-bc-ab} & \multicolumn{1}{c|}{bd-cd-bc} & \multicolumn{1}{c|}{ag-fg-ef-de-cd-bc-ab} \\ \hline
b & 1                       & 0                       & 0                       & 0                       & 0                       & 0                       & 0                             & 0                                & 0                             & 0                                         \\ \cline{1-1}
c & 0                       & 1                       & 0                       & 0                       & 0                       & 0                       & 0                             & 0                                & 0                             & 0                                         \\ \cline{1-1}
d & 0                       & 0                       & 1                       & 0                       & 0                       & 0                       & 0                             & 0                                & 0                             & 0                                         \\ \cline{1-1}
e & 0                       & 0                       & 0                       & 1                       & 0                       & 0                       & 0                             & 0                                & 0                             & 0                                         \\ \cline{1-1}
f & 0                       & 0                       & 0                       & 0                       & 1                       & 0                       & 0                             & 0                                & 0                             & 0                                         \\ \cline{1-1}
g & 0                       & 0                       & 0                       & 0                       & 0                       & 1                       & 0                             & 0                                & 0                             & 0                                         \\ \cline{1-1}
a & 0                       & 0                       & 0                       & 0                       & 0                       & 0                       & 0                             & 0                                & 0                             & 0                                         \\ \cline{1-1}
\end{tabular}
\end{table}

Lo cual implica

\begin{figure}[H]
\centering
\includegraphics[width=12.5cm]{4}
\caption{Cadenas base de $Z_1^2$.}
\end{figure}


Nótese que $ac=\partial_2^2[abc] \in B_1^2$, $ad=\partial_2^2[abc]+\partial_2^2[acd] \in B_1^2$ y $bd = \partial_2^2[bcd] \in B_1^2$. Por otro lado, algunos elementos 
de $ag+B_1^2$ son \\

\begin{figure}[H]
\centering
\includegraphics[width=9.5cm]{5}
\end{figure}

Como $C_p^{l}\leqslant C_p^{l+ \tau}$, entonces $Z_p^{l} \leqslant C_p^{l+ t}$ y $Z_{p}^{l}\cap B_{p}^{l+\tau}\leqslant Z_{p}^{l}$. Luego, 
$B_{p}^{l} \leqslant Z_{p}^{l}\cap B_{p}^{l+t}$ implica que el cociente $H_{p}^{l,t}=Z_{p}^{l}/(Z_{p}^{l}\cap B_{p}^{l+t})$ está bien definido y además es isomorfo a algún 
subgrupo de $ Z_{p}^{l}/B_{p}^{l}=H_{p}^{l}$. El grupo $H_{p}^{l,t}$ se dice el grupo de $t -$persistencia de $H_{p}^{l}$. \\

La razón por la cual se consideran clases módulo  $Z_{p}^{l}\cap B_{p}^{l+t}$ en lugar de modulo $B_{p}^{l+t}$ es porque fácilmente pueden existir cadenas en $B_{p}^{l+t}$ 
compuestas de $p-$símplices $\sigma_p^{l+t}$ que no existen en $K^{l}$, de modo que si $\sigma_p^{l}$ es positivo en $K^{l}$, la clase $\sigma_p^{l}+B_{p}^{l+t}$ contiene 
cadenas con términos de la forma $\sigma_p^{l}+\sigma_p^{l+t}$, que no aportan ninguna información acerca de la persistencia de la clase $\sigma_p^{l}+B_{p}^{l}$ pues no 
comparables en ninguna forma con los elementos de $Z_p^{l}$. Para resolver este problema se consideran las $p-$cadenas en $Z_{p}^{l}\cap B_{p}^{l+t}$ que corresponden a 
$p-$ciclos construibles en $K^l$ que también pueden verse como como fronteras de $(p+1)-$cadenas que existen en $K^{l + t}$ pero no en $K^{l}$. \\

Considere el homomorfismo\\

\begin{center}
$
\eta _p^{l,t } :\begin{matrix}
H_p^{l} \rightarrow  H_p^{l,t}\\ 
\sigma + B_p^l \mapsto \sigma + Z_{p}^{l}\cap B_{p}^{l+t},
\end{matrix}
$  
\end{center}

Sea $\widetilde{\sigma}=\sigma -\sum_{i \in I_p^l} \xi_i \sigma _i$ un $p-$ciclo base de $Z_p^l$ con $\sigma$ su respectivo $p-$símplice etiquetador. Si es negativo, esto es, 
si $\widetilde{\sigma} \in B_p^l$, entonces $\widetilde{\sigma} \in Z_{p}^{l}\cap B_{p}^{l+t}$ pues $B_p^l \leqslant B_p^{l+t}$. Luego\\

\begin{equation*}
    \begin{split}
      \eta _p^{l,t }(\widetilde{\sigma} + B_p^l) &= \eta _p^{l,t }(B_p^l)\\
      &= Z_{p}^{l}\cap B_{p}^{l+t}
    \end{split}
\end{equation*}

de modo que, las clases triviales de $K^l$ son enviadas en clases triviales de $K^{l+t}$. Resaltar este hecho aparentemente obvio resulta de utilidad cuando se quiere 
contrastar lo que sucede cuando $\widetilde{\sigma}$ es positivo. Si existiese un $(p+1)-$símplex $\sigma^*$ tal que $\partial=\partial_{p+1}^{l+t}[\sigma^*]=\sigma 
+\sum_{i \in I_p^l} \xi'_i \sigma _i$, de tal forma que ningún $\sigma_i$ con coeficiente no nulo sea positivo, y teniendo en cuenta que $Z_p^l=<\widetilde{\sigma}>$, 
el único ciclo base no delimitante de $C_p^l$ empleado para describir $\partial$ es el que corresponde a $\sigma$, es decir

\begin{equation*}
    \begin{split}
        \partial &= (\sigma -\sum_{i \in I_p^l} \xi_i \sigma _i)+ \sum_{i \in I_p^l} \xi''_i \sigma _i\\
        &= \widetilde{\sigma} + \sum_{i \in I_p^l} \xi''_i \sigma _i
    \end{split}
\end{equation*}

Luego, $\sum_{i \in I_p^l} \xi''_i \sigma _i$ \textbf{(2)} se escribe como combinación de $p-$ciclos base etiquetados con símplices negativos de $C_p^l$ y por consiguiente, 
$\sum_{i \in I_p^l} \xi''_i \sigma _i \in B_p^l \leqslant Z_{p}^{l}\cap B_{p}^{l+t}$. Así, hemos concluido que $\widetilde{\sigma}- \partial \in Z_{p}^{l}\cap B_{p}^{l+t}$ y 
por tanto\\

\begin{equation*}
    \eta _p^{l,t }(\widetilde{\sigma} + B_p^l)=\widetilde{\sigma}+Z_{p}^{l}\cap B_{p}^{l+t}=Z_{p}^{l}\cap B_{p}^{l+t}.
\end{equation*}

En palabras, esto quiere decir que la clase no trivial en el momento $l$, $\widetilde{\sigma} + B_p^l$ se trivializa en el furuto $l+t$. \\

Si \textbf{(2)} contuviese un símplice positivo, $\sigma'$ entonces \\

\begin{equation*}
    \begin{split}
        \sum_{i \in I_p^l} \xi''_i \sigma _i &= (\sigma' -\sum_{i \in I_p^l} \xi_i \sigma _i)+ \sum_{i \in I_p^l} \xi'''_i \sigma _i\\
        &= \widetilde{\sigma'} + \sum_{i \in I_p^l} \xi'''_i \sigma _i
    \end{split}
\end{equation*}

donde nuevamente $\sum_{i \in I_p^l} \xi'''_i \sigma _i \in B_p^l \leqslant Z_{p}^{l}\cap B_{p}^{l+t}$. Esto implica $\widetilde{\sigma'} + \sum_{i \in I_p^l} \xi'''_i \sigma _i
\in \widetilde{\sigma'} + Z_{p}^{l}\cap B_{p}^{l+t}$, de donde se concluye $\widetilde{\sigma}- \partial \in \widetilde{\sigma'} + Z_{p}^{l}\cap B_{p}^{l+t}$. Así, de acuerdo a 
lo dicho en el párrafo 3, $\widetilde{\sigma}$ y $\widetilde{\sigma'}$ son ciclos homólogos y, por consiguiente\\

\begin{equation*}
    \begin{split}
        \eta _p^{l,t }(\widetilde{\sigma} + B_p^l) &= \widetilde{\sigma} + Z_{p}^{l}\cap B_{p}^{l+t}\\
        &= \widetilde{\sigma'} + Z_{p}^{l}\cap B_{p}^{l+t}\\
        &= \eta _p^{l,t }(\widetilde{\sigma'} + B_p^l).
    \end{split}
\end{equation*}

Como en el caso anterior, puede decirse que dos clases distintas en el tiempo $l$ se mezclan en el futuro $l+t$, pero si tenemos en cuenta la jerarquía implícita entre los 
símplices dada por el orden en sus índices podría cambiarse la palabra mezcla por \textit{absorción}. Teniendo en cuenta que para todo $p$ el $p-$símplice más viejo siempre 
será el nulo, podemos fijar por convención que la clase representada por el símplex más viejo absorbe la del más joven. De esta forma, en el primer caso, la trivialización de 
la clase $\widetilde{\sigma} + B_p^l$ es en realidad su absorción por la clase $Z_{p}^{l}\cap B_{p}^{l+t}$ y por extensión por la clase $B_{p}^{l+t}$, y en el segundo, si el 
símplex $\widetilde{\sigma}$ es más joven que el símplex $\widetilde{\sigma'}$, entonces, a futuro, la clase $\widetilde{\sigma'} +  B_{p}^{l+t}$ absorbe a la clase 
$\widetilde{\sigma} + B_{p}^{l}$.\\

Y en general si \textbf{(2)} contiene a los símplices positivos $\sigma^{1},...,\sigma^{s}$, entonces 

\begin{equation*}
    \begin{split}
       \sum_{i \in I_p^l} \xi''_i \sigma _i &= \sum_{j=1}^s \left (\sigma^j- \sum_{i \in I_p^l} \xi_{ij} \sigma _i \right ) +  \sum_{i \in I_p^l} \xi''''_i \sigma _i \\
       &= \sum_{j=1}^{s} \widetilde{\sigma^{j}}+  \sum_{i \in I_p^l} \xi''''_i \sigma _i\\
       & \in \sum_{j=1}^{s} \widetilde{\sigma^{j}} + Z_{p}^{l}\cap B_{p}^{l+t}.
    \end{split}
\end{equation*}

Y así $\widetilde{\sigma}- \partial \in \sum_{j=1}^{s} \widetilde{\sigma^{j}} + Z_{p}^{l}\cap B_{p}^{l+t}$ y

\begin{equation*}
    \begin{split}
        \eta _p^{l,t }(\widetilde{\sigma} + B_p^l) &= \widetilde{\sigma} + Z_{p}^{l}\cap B_{p}^{l+t}\\
        &= \sum_{j=1}^{s} \widetilde{\sigma^{j}} + Z_{p}^{l}\cap B_{p}^{l+t}.
    \end{split}
\end{equation*}

Si $j(\sigma^*)$ denota al símplex positivo mas joven no nulo en $\partial$, entonces en el caso que $\sigma=j(\sigma^*)$ diríamos que la clase $\widetilde{\sigma} + B_p^l$ es absorbida en el tiempo $t+l$ por la clase $\sum_{j=1}^{s} \widetilde{\sigma^{j}} + B_{p}^{l+t}$.

En resumen:

\begin{equation*}
    \begin{split}
        \eta^{l,t}_p (j(\sigma^*)+B_p^l)=\left\{\begin{matrix}
        Z_p^l \cap B_p^{l+t} & \text{si $\partial$ no contiene más símplices positivos no nulos.} \\ 
        \sum \widetilde{\sigma^j} + Z_p^l \cap B_p^{l+t} & \text{si los $\sigma^j$ son eslabones de la cadena $\partial$} 
\end{matrix}\right.
    \end{split}
\end{equation*}

Si $\sigma$ es positivo y $\sigma^*$ es el primer símplex cuya frontera contiene a $\widetilde{\sigma}$ diremos que $\sigma^*$ es el ciclo negativo asociado a $\sigma$. 
Finalmente, si $K^l$ es el primer elemento de a filtración donde aparece  $\sigma$ y $K^{l+t}$ el primero donde aparece  $\sigma^*$, entonces la persistencia de $\sigma$ 
es la pareja $(l,l+t)$.\\

Cabe recalcar que el proceso antes descrito se ejecuta para cada símplex positivo que nazca. El Diagrama de Persistencia de la filtración $K$ se define como el conjunto 
$\{ (l,l+t) \}$, donde cada pareja ordenada es la persistencia de alguna clase módulo frontera en $K$. Gráficamente, el cálculo de la homología persistente puede resumirse
con la siguiente imagen:

\begin{figure}
\centering
\includegraphics[,width=10cm]{simplicial.png}
\end{figure}

Intuitivamente hablando, el algoritmo descrito anteriormente sirve para calcular cuanto persiste cada componente conexa en la topología, así como cada hueco circular y cada
vacío, etcétera. El diagrama de persistencia suele representarse sobre un plano cartesiano como se ve en la esquina inferior izquierda de la figura. 

### Distancia Cuello de Botella

En este apartado se define una métrica para comparar los diagramas de persistencia. Sean $P_0= \{ (a_1,b_1), \dots, (a_n,b_n)  \}$ y $P_1= \{ (x_1,y_1), \dots, (x_m,y_m)  \}$ dos diagramas de persistencia. Para cada $(z,w) \in P_0 \cup P_1$ se considera su proyección ortogonal sobre la diagonal $y=x$, donde

\begin{equation*}
    (z,w)^{T}=(z+w)( \frac{1}{2},\frac{1}{2} )
\end{equation*}

Si $P_0^T= \{ (a,b)^T | (a,b) \in P_0 \}$ y $P_1^T= \{ (x,y)^T | (x,y) \in P_1 \}$, entonces los conjuntos 

\begin{equation*}
    \begin{split}
        X=P_0 \cup P_1^T \\
        Y=P_1 \cup P_0^T
    \end{split}
\end{equation*}

tienen el mismo cardinal. Supongamos que tanto $P_0$ como $P_1$ son diagramas de persistencia, entonces la biyección $\nu : X \rightarrow Y$ se dice Emparejamiento. La cantidad $|\nu|= \max ||x- \nu(x)||_{\infty}$ corresponde a la longitud de la arista más larga al emparejar los conjunto $X$ e $Y$ por $\nu$. Entre todas las posibles biyecciones, es de interés aquella $\nu_0$ para la cual se verifica $ |\nu_0| \leq |\nu|$ para cualquier otro emparejamiento  $\nu$. La distancia cuello de botella entre los diagramas $P_0$ y $P_1$ se define como 

\begin{equation*}
    \begin{split}
        D(P_0,P_1) &=\min_{\nu}\max_{x} ||x-\nu(x)||_{\infty} \\
        &= |\nu_0|
    \end{split}
\end{equation*}

Gráficamente el emparejamiento se ve como 

\begin{figure}[H]
    \centering
    \includegraphics[height=6cm,width=6cm]{botella.png}
\end{figure}

\section*{El método}

\subsection*{Intuición}

\begin{figure}[H]
    \centering
    \includegraphics[height=6cm,width=6cm]{intu.png}
\end{figure}
