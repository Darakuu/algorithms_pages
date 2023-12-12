---
tags:
  - Algoritmi/PrimaProva
  - Algoritmi
  - Algoritmi/AnalisiAmmortizzata
---
Per analizzare sequenze di $n$ operazioni.
Si determina un tempo complessivo $T(n)$ che viene in qualche modo ripartito tra le $n$ operazioni.

$\dfrac{T(n)}{n}:\text{costo ammortizzato per operazione.}$

La stima ottenuta non è probabilistica, si tratta di una media nel caso peggiore.

**Tre Metodi**:
- [[Metodo dell'Aggregazione]]
- [[Metodo degli Accantonamenti]]
- [[Metodo del Potenziale]]

**Esempi**
* [[Stack Multipop]]
* [[Contatore binario]]

**Applicazione Reale**
- [[Tabella Dinamica]]
