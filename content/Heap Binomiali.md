---
tags:
  - Algoritmi/PrimaProva
  - Algoritmi/StruttureDati
  - Algoritmi/MergeableHeap
---
# Heap Binomiali

>[!def] Definizione
>Uno Heap Binomiale H è una foresta di [[Alberi Binomiali]] tale che:
>- Ciascun albero binomiale in H gode della proprietà di min-heap;
>- Per ogni $k \in \mathbb{N}$, H contiene al più un solo albero binomiale di grado k.


# Maggiorazione Grado Massimo di un Nodo

Conseguenze immediate della definizione:
- In ciascun albero binomiale in un heap binomiale, la radice contiene la chiave minima dell'albero;
- Uno heap binomiale H con n nodi è formato al più da $\left\lfloor {\log n} \right\rfloor+1$ alberi binomiali.
- Infatti, sia $B_{k}$ l'albero binomiale di grado massimo in H, si ha $2^k\leq n$, da cui $k\leq \log n$, e quindi $k\leq \left\lfloor {\log n} \right\rfloor$.
- Pertanto il numero di alberi binomiali in H è al più $k+1\leq \left\lfloor {\log n} \right\rfloor+1$