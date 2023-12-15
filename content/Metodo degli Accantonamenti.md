---
tags:
  - Algoritmi/PrimaProva
  - Algoritmi/AnalisiAmmortizzata
---
# Metodo degli Accantonamenti

Nel metodo degli accantonamenti assegnamo costi variabili a operazioni differenti: cioè qualche operazione potrebbe avere costo maggiore o minore del suo effettivo costo reale. Quando il costo assegnato di un'operazione supera il costo effettivo, la differenza viene assegnata a specifici oggetti della struttura dati sotto forma di _credito_. (concetto logico, assolutamente virtuale). 
 

Questo credito, sempre **non negativo**, viene depositato o prelevato a seconda delle esigenze. 

In questo caso, le operazioni hanno costo variabile (e quindi non è lo stesso per tutte le operazioni), per cui, la scelta dei costi ammortizzati è di fondamentale importanza.  
Siano $op_{1},op_{2},\dots,op_{n}$ le nostre operazioni, e 
 

$c_{i}=_{def}\text{costo-reale}(op_{i})$ 

$\hat{c}_{i}=_{def}\text{costo-ammortizzato}(op_{i}) \qquad$ <ins>Definito da noi</ins>. 

Obiettivo: definire i costi ammortizzati in modo tale che valga: 

$T(n) = \displaystyle\sum^n_{i=1}c_{i}\leq \sum^n_{i=1}\hat{c}_{i}$ 

Se $\hat{c}_{i}>c_{i}, \text{ allora } c_{i}$ unità di costo sono utilizzate per pagare il costo della i-esima operazione $op_{i}$. 

Se $\hat{c}_{i}<c_{i},$ la differenza $c_{i}-\hat{c}_{i}$ viene recuperata da crediti immagazzinati nella struttura dati. 

In altre parole: paghiamo prima delle operazioni future. Quando il costo reale supera il costo ammortizzato, usiamo il credito per pagare. 

A questo punto, viene raggiunto l'obiettivo prefissato pocanzi. 

>[!example] Esempi:
>- [[Stack Multipop#Multipop con Metodo degli Accantonamenti Accantonamenti|Stack Multipop]]
>- [[Contatore binario]]

