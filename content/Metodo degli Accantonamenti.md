---
tags:
  - Algoritmi/PrimaProva
  - Algoritmi/AnalisiAmmortizzata
---
# Metodo degli Accantonamenti

Siano $op_{1},op_{2},\dots,op_{n}$ le nostre operazioni, e <br>
$c_{i}=_{def}\text{costo-reale}(op_{i})$ <br>
$\hat{c}_{i}=_{def}\text{costo-ammortizzato}(op_{i}) \qquad$ <ins>Definito da noi</ins>.

Obiettivo: definire i costi ammortizzati in modo tale che valga:

$T(n) = \displaystyle\sum^n_{i=1}c_{i}\leq \sum^n_{i=1}\hat{c}_{i}$

Se $\hat{c}_{i}>c_{i}, \text{ allora } c_{i}$ unità di costo sono utilizzate per pagare il costo della i-esima operazione $op_{i}$. <br>
Se $\hat{c}_{i}<c_{i},$ la differenza $c_{i}-\hat{c}_{i}$ viene recuperata da crediti immagazzinati nella struttura dati.

A questo punto, viene raggiunto l'obiettivo prefissato pocanzi.

Esempi:
- [[Stack Multipop#Multipop con Metodo degli Accantonamenti Accantonamenti|Stack Multipop]]
- [[Contatore binario#Contatore Binario con Metodo degli Accantonamenti Accantonamenti|Contatore Binario]]