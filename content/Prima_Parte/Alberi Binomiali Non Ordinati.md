---
tags:
  - Algoritmi/PrimaProva
  - Algoritmi/StruttureDati
---
# Alberi Binomiali Non Ordinati

Implementano gli [[Heap di Fibonacci]].

>[!def] Definizione
>$\forall\ k \in \mathbb{N}\ \exists \text{ un albero binomiale non ordinato } U_{k} \text{ di grado } k$, definito in base alla seguente ricorsione:
>- $U_{0}$ è l'albero formato da un solo nodo;
>- Dato $U_{k-1}$ definiamo $U_{k}$ combinando due copie di $U_{k-1}$ nella seguente maniera:
> ![[Pasted image 20231219225217.png|256]]

## Lemma (Proprietà degli alberi binomiali NON Ordinati)

Per ogni $k=0,1,2\dots$ valgono le segu\enti proprietà: 

1. $U_{k}$ ha $2^k$ nodi;
2. L'altezza di $U_{k}$ è $k$;
3. $U_{k}$ ha $\displaystyle\binom{k}{i}$ a profondità $i\ (i=0,1,\dots,k)$
4. La radice di $U_{k}$ ha grado $k$ ed ogni altro nodo in $U_k$ ha grado $<k$.
   Inoltre, i figli della radice di $U_{k}$ sono radici di $U_{k-1},U_{k-2},\dots,U_{2},U_{1},U_{0}$ **in un qualsiasi ordine** $\textcolor{red}{(unico\ cambiamento)}$. 

- Si osservi che da questo lemma segue immediatamente che $D(n)=O(\log n)$, almeno quando l'heap è formato soltanto da alberi binomiali non ordinati.
- La strategia di mantenimento degli Heap di Fibonacci prevede di <ins>ritardare il più possibile il lavoro di ristrutturazione dell'heap</ins>.

<ins>DImostrazione</ins> per induzione 

Caso Base: $k=0$ 

1. $U_{0}$ ha $1=2^0$ nodi.
2. L'altezza di $U_{0}$ è $0$
3. $U_{0}$ ha $1=\displaystyle\binom{0}{0}$ nodi a profondità $0$
4. La radice di $U_{0}$ ha grado $0$

Passo Induttivo: Supponiamo che il Lemma sia vero per $k-1$, con $k\geq1$
1. $U_{k}$ ha $\#(U_{k-1}+)+\#(U_{k-1})=2\cdot2^{k-1}=2^k$ nodi.
2. L'altezza di $U_{k}$ è $(k-1)+1=k$
3. Sia $1 \leq i \leq k-1$, il numero di nodi di $U_{k}$ a profondità $i$ è uguale a:  

   $\displaystyle\binom{k-1}{i}+\binom{k-1}{i-1}=\binom{k}{i}$
   Inoltre, $U_{k}$ ha $\displaystyle\binom{k}{0}=1$ nodi a profondità 0, quindi avrà $\displaystyle\binom{k}{k}$ nodi a profondità $k$. 
4. La radice di $U_{k}$ ha grado $degree{U_{k-1}}+1 = k
	- Inoltre ciascun altro nodo appartiene ad un $U_{k-1}$ e pertanto per ipotesi induttiva ha grado $\leq k-1$, cioè $<k$.
	- Il primo figlio della radice di $U_{k}$ è radice di $U_{k-1}$. Inoltre, per ipotesi induttiva, I successivi $k-1$ figli della radice di $U_{k}$ sono radici di $U_{k-2},...,U_1,U_{0}. \quad \blacksquare$
