---
tags:
  - Algoritmi/AnalisiAmmortizzata
  - Algoritmi/PrimaProva
---
# Tabelle Dinamiche

Si tratta di tabelle soggette a riallocazione, per evitare overflow.
Sia $T$ una tabella, poniamo: 

>[!def] Definizioni Preliminari:
>- $size[T]=_{def}$ Dimensione della tabella
>- $num[T]=_{def}$ Numero degli elementi in T
>- $\alpha(T)=_{def}\dfrac{num[T]}{size[T]}\qquad \text{Se } Size[T]>0$
>	- $\ =_{def} 1 \quad\qquad\qquad\text{ altrimenti}$

($\alpha(T)$: Fattore di Carico) 

Skippiamo lo pseudocodice di $\text{Table\_Insert}$ e $\text{Allocate\_Table}$.

## Analisi grossolana

Analisi di $n$ inserimenti su una tabella inizialmente nulla.

Abbiamo $n=2^k$ inserimenti. 

Il costo dell'inserimento $(2^{k-1}+1)\text{-esimo}=2^{k-1}+1 = \dfrac{n}{2}+1$ 
Perciò, il costo di un inserimento è $O(n)$, e il costo di $n$ inserimenti è $O(\textcolor{red}{n^2})$

## Con Metodo dell'[[Metodo dell'Aggregazione|Aggregazione]]

|             |   | $c_{i}$           |
|:-----------:|:-----------:|:-----------------:|
| Inserimento | Costo Copia | Costo Inserimento |
|           1 | /           |                 1 |
|           2 |           1($2^0$) |                 1 |
|           3 |           2($2^1$) |                 1 |
|           4 | /           |                 1 |
|           5 |           4($2^2$) |                 1 |
|           6 | /           |                 1 |
|           7 | /           |                 1 |
|           8 | /           |                 1 |
|           9 |           8($2^3$) |                 1 |
|          10 | /           |                 1 |
| ...         | ...         | ...               |  

#todo , è improbabile siano presenti alla prima prova in itinere.