---
tags:
  - Algoritmi/StruttureDati
  - Algoritmi/PrimaProva
---
# Alberi Binomiali

>[!def] Definizione
>$\forall\ k \in \mathbb{N}\ \exists \text{ un albero binomiale } B_{k} \text{ di grado } k$, definito in base alla seguente ricorsione:
>- $B_{0}$ è l'albero formato da un solo nodo;
>- Dato $B_{k-1}$ definiamo $B_{k}$ combinando due copie di $B_{k-1}$ nella seguente maniera:
> ![[Pasted image 20231219021406.png|512]]


## Lemma (Proprietà degli alberi binomiali)

Per ogni $k=0,1,2\dots$ valgono le seguenti proprietà: 

1. $B_{k}$ ha $2^k$ nodi;
2. L'altezza di $B_{k}$ è $k$;
3. $B_{k}$ ha $\displaystyle\binom{k}{i}$ nodi a profondità $i\ (i=0,1,\dots,k)$
4. La radice di $B_{k}$ ha grado $k$ ed ogni altro nodo in $B_k$ ha grado $<k$.
   Inoltre, i figli della radice di $B_{k}$ sono radici di $B_{k-1},B_{k-2},\dots,B_{2},B_{1},B_{0}$ nell'ordine dato. 

<ins>DImostrazione</ins> per induzione 

Caso Base: $k=0$ 

1. $B_{0}$ ha $1=2^0$ nodi.
2. L'altezza di $B_{0}$ è $0$
3. $B_{0}$ ha $1=\displaystyle\binom{0}{0}$ nodi a profondità $0$
4. La radice di $B_{0}$ ha grado $0$

Passo Induttivo: Supponiamo che il Lemma sia vero per $k-1$, con $k\geq1$
1. $B_{k}$ ha $\#(B_{k-1}+)+\#(B_{k-1})=2\cdot2^{k-1}=2^k$ nodi.
2. L'altezza di $B_{k}$ è $(k-1)+1=k$
3. Sia $1 \leq i \leq k-1$, il numero di nodi di $B_{k}$ a profondità $i$ è uguale a:  

   $\displaystyle\binom{k-1}{i}+\binom{k-1}{i-1}=\binom{k}{i}$
   Inoltre, $B_{k}$ ha $\displaystyle\binom{k}{0}=1$ nodi a profondità 0, quindi avrà $\displaystyle\binom{k}{k}$ nodi a profondità $k$. 
4. La radice di $B_{k}$ ha grado $degree{B_{k-1}}+1 = k$
	- Inoltre ciascun altro nodo appartiene ad un $B_{k-1}$ e pertanto per ipotesi induttiva ha grado $\leq k-1$, cioè $<k$.
	- Il primo figlio della radice di $B_{k}$ è radice di $B_{k-1}$. Inoltre, per ipotesi induttiva, I successivi $k-1$ figli della radice di $B_{k}$ sono radici di $B_{k-2},...,B_1,B_{0}. \quad \blacksquare$

## Corollario

Sia $B$ un albero binomiale con $m$ nodi, allora ogni nodo in $B$ ha al più grado $\log n$. 

<ins>DImostrazione</ins> 

Per qualche $k \in \mathbb{N}$ si ha $B=B_{k}$. 

Quindi $n=2^k$.  

Ogni nodo in $B_{k}$ ha grado $\leq k$. 

Ma $k=\log n$, da cui la tesi $\quad \blacksquare$

 


Una foresta di alberi binomiali implementa un [[Heap Binomiali|Heap Binomiale]] H.