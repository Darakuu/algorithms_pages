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

Analisi di $n$ inserimenti su una tabella inizialmente nulla

#todo