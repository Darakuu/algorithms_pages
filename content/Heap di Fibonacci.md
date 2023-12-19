---
tags:
  - Algoritmi/PrimaProva
  - Algoritmi/StruttureDati
  - Algoritmi/MergeableHeap
draft: false
---
# Heap di Fibonacci

Uno Heap di Fibonacci è una collezione di alberi con la proprietà Heap. 
 
Gli alberi di uno Heap di Fibonacci non devono necessariamente essere binomiali. 

![[Pasted image 20231219223345.png|256]]

- $p[x]$: Padre;
- $left[x]:$ Fratello sinistro;
- $right[x]:$ Fratello destro;
- $child[x]:$ un figlio;
- $degree[x]:$ numero di figli;
- $mark[x]:$ indica se il nodo $x$ ha perduto un figlio dall'ultima volta in cui $x$ è diventato figlio di un altro nodo.

Inoltre:

- $min[H]:$ punta al minimo, indica la radice contenente la chiave minima e dà accesso alla struttura;
- $n[H]:$ contiene il numero di nodi in H.

>[!example]- Esempio
>![[Pasted image 20231219224018.png|512]]

## Funzione Potenziale

$\Phi(H)=t(H)+2m(H)\geq 0$

Dove:
- t(H): numero alberi nella lista delle radici di H;
- m(H): numero nodi marcati in H
- Sia $\{H_{i}\}_{i \in I}$ una collezione finita di Heap, poniamo: $\Large\Phi(\{H_{i}\}_{i \in I})=\displaystyle\sum_{i \in I}\Phi(H_{i})\geq 0 = \Phi(\emptyset)$
 
# Stima di D(n)

$\large D(n)$ è il massimo grado di un nodo. 

- L'analisi verrà effettuata in funzione di un upper bound $D(n)$ sul massimo grado di un nodo qualunque in uno heap con n nodi.
- Dimostreremo che si ha: $\large \textcolor{red}{D(n)=O(\log n)}$

## Operazioni presenti e mancanti

Se vengono eseguite <ins>SOLO</ins> operazioni del tipo:
- Make-Heap; $\qquad O(1)$
- Insert; $\qquad O(1)$
- Minimum; $\qquad O(1)$
- Extract-Min; $\qquad O(\log n)=O(D(n))$
- Union. $\qquad O(1)$

Ciascuno Heap di Fibonacci è rappresentabile come collezione di alberi binomiali non ordinati. 

$D^*(n)=$ massimo grado di un nodo in un heap di fibonacci con $n$ nodi costruito senza mai usare le operazioni di **Decrease-Key** e **Delete**.

Vedremo che $D^*(n)\leq D(n)$. Inoltre, i costi di complessità sono ammortizzati.

## Lemma 3 (quello che c'è all'esame da qui in poi, ndr)

(Abbiamo saltato i primi due perché indicano proprietà dei numeri di fibonacci). 

Sia $x$ un nodo in un heap di fibonacci e sia $grado(x)=k$. 

Siano $y_{1},y_{2},\dots,y_{k}$ i figli di $x$ nell'ordine in cui sono stati innestati in $x$. 

Allora, $grado[y_{i}]\geq i-2,$ per $i=3,4,\dots,k$

<ins>Dimostrazione</ins>

...

## Altro Lemma

Sia x un nodo in uno heap di fibonacci, e sia $grado[x]=k$. 

Allora $size(x)\geq F_{k+2},$ dove $size(x)$ è il numero di nodi nel sottoalbero radicato in $x$.

<ins>Dimostrazione</ins>

...

## Corollario 1

$\Large size[x]\geq \Phi^{grado[x]}$
## Corollario 2

$\Large D(n)\leq \left\lfloor {\log_{\Phi}n} \right\rfloor,$ da cui $\Large D(n)=O(\log n)$ .

<ins>Dimostrazione</ins>